## 課題１
### どのような問題を生じるか
- カンマ区切りでデータが格納されている為、
アプリケーションでカンマを取り除くやカンマをつけてデータ格納するなどの考慮することが増える
- sqlで集約関数が使えない。
- タグを用いたpostデータ一覧検索することが難しい。明確にwhere句を使用できないので、like検索になってしまう
- tag付けられた時間を出してほしいという使用があった場合、個別の作成日時が取得できないので不可能
- tagがステータスの意味合いを含んでいる場合、現在のstatusタグの表示ができない。リストの最後の要素が最新であると仮定しても、それを表明する根拠がない。
- tagテーブルを切り出して中間テーブルを用いた時に、マイグレーションをする際に重複タグを考慮する必要がある
- postテーブルにtag付の上限があった際に、リスト形式ではいったんデータを取得して、カンマを取り除き配列に格納して、
要素の長さを取得、上限に足しているかのロジック付け足さないといけない

### 課題２
テーブル設計に関しては別紙参照

### 課題３
- お知らせ管理管理機能
  - お知らせテーブルと既読テーブルがあるとする。既読管理をする際に、誰が既読したかをリスト形式格納するパターン(業務で実際に提案された設計)
