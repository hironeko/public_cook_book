## VSCodeでの便利機能

- 簡単なAPIデバックが行う方法
VSCodeの`RESTClient`を使用する方法

1. 作業ディレクトリに`request.http`というfileを用意する
2. 下記のように記述を行う

POST https://URL
Content-Type: application/json

{
    // 何か
}

3. URLの上に`Send Request`が表示されているのでクリックする

これだけでリクエストのデバックが可能になるので重宝していいかもしれない
リクエスト結果は右に出力される