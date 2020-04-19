# design
設計やPullRequestを出す前に確認すべき項目

### 実装全般に言える事

●条件分岐  
・ifはearly return（ガード節）にできないか  
・ture/falseを判定する場合はreturnに条件式を書けないか
・分岐の多いifは辞書(連想配列)で簡潔にできないか  
・「状態」や「タイプ」を参照し始めたら、Stateパターンを使えないか    
    
●命名規則   
・基本はリーダブルコードにあるような事   
・prefixが冗長に感じる場合ファイル名などの名前空間によって何をするのかが担保されていれば内容に関しての名前のみで十分(好みによるが)   
・非同期処理はgetを使わずfetchを使うなど意味の範囲を狭められないか（難しい単語にならないようには注意）   
・booleanを扱う場合はflagやon/offなどは使わずisを使うのが望ましい
  
●責務の分離  
・関数の名前通りの処理になっているか、関係ない処理が入っていないか  
・関数は1処理1関数ぐらいまで分離できているか     
・コマンドとクエリがごっちゃになっていないか→CQS(コマンドとクエリ分離原則)が考えられないか     
CQSはオブジェクト内に定義した関数は、コマンドとクエリに分けることができるというものである。  
コマンド = 状態を変更するための関数（副作用がある）  
クエリ = 状態を取得するための関数（副作用がない）  
・処理単位で分離するのではなく、意味単位で分離できているか（単に長い処理を分割して関数に分けるだけはリファクタリングとは言わない）

●共通化
・共通化の引数にコレクションを入れていないか（int,string,boolean型以外を入れると著しく共通化しにくくなる）

●統一感   
・同じ内容を表すのに別の変数名がつけられていないか 
・書き方のフォーマットなどは統一されているか
  

### バックエンド側

●MVCなど  
・責務の分離はできているか、どこの層で何をするかが明確に区別できているか   
・別のクラスや構造体で似た処理がある場合はinterfaceなどで抽象化できないか    
・バリデーションは適切に行われているか    
    
### フロントエンド側

・コンポーネントに渡されたpropsをその場で書き換えてないか、書き換えるのはemit等で元の層で行う       
・非同期処理を行う関数は特に意図がない限り基本的にpromiseを返す     
・UXを意識した設計になっているか  
セッションが切れていたらログインページにリダイレクトし、ログイン後に元のページに戻してあげる    
フォームバリデーションができているか    
権限がないアクセスはエラーページではなくログイン画面に飛ばす等     

<hr>

### 参考
https://qiita.com/fkrw/items/7646563a2b238fbcff9a    
https://qiita.com/pakkun/items/9bef9132f168ba0befd7       
