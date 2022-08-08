## 課題１に関して
- Postのtag1,tag2,tag3とカラムを設けて管理すると、Aカラムはtag1と使用上の制約をまず開発サイドでドキュメントを整備しないといけない。極力ドキュメントに落とし込まない設定が良いと考える。
また、Aカラムはtag1という制約があった場合、アプリケーション側でミスがあれば、タグAをtag2といった具合に間違えてinsertするするリスクがあるし、DB側ではそれを制御することができない。
- こういったカラムの持ち方をしてしまうと、タグの種類が増えた時にカラムが追加され、さらに上記の制約が増える。
- updatesする時に複雑性がます。対処のカラムに格納されたデータが本当に更新対処のデータなのかは、アプリサイドで一回取得してデータを確認した上で更新しないといけない。追加、削除も同様
- sqlで必ず、3つのカラムの検索をwhere句でかけてやらないといけない
- nullを制御できない。nullが増えるといんでindexが参照されない。ネットではいろいろnullの弊害があったけど印象に残ったのは https://qiita.com/wanko5296/items/141d7ff41cd9ab8a72f2


## このアンチパターン
- マルチカラムアトリビュートに相当する

### マルチカラムアトリビュートとは
- 複数の意味合いを持ったデータに対し、それぞれカラム追加する(tag1, tag2, tag3など。)

### 何が問題なのか？
- カラムの検索をする際に値のそれぞれ定義したカラムを全て検索対象にしないといけない
  - それぞれのカラムに決められたデータが格納されるとは限らないから。間違えてtag1に格納するデータをtag2のに格納するリスクがある
  - 対応するカラムが増えれば増えるほど、where or句が増えていく。保守大変
- updateに対する考慮することが増える
　-　updatesする時に複雑性がます。対処のカラムに格納されたデータが本当に更新対処のデータなのかは、アプリサイドで一回取得してデータを確認した上で更新しないといけない。
　- 追加削除も同様
- 一意性の保証ができない。
　- 例えば、tagAがtag1カラムにtagAがtag2と格納できてしまうのでunique差が欠如する
- 対応したカラムが増殖していく