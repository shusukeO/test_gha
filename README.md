# test_gha

GHA(GitHub Actions) を試す

## メモ

- 全般のドキュメント

  - https://docs.github.com/ja/actions

- .github/workflows ディレクトリを作成、それ以下に、.yml ファイルで定義した Actions を配置していく

- ２つの変数
  - 違いは、ここを参照
    - https://zenn.dev/hashito/articles/aef4de448f341b
  - ワークフロー内の環境変数
    - .yml で定義して、その場でつかう

```YAML
name: Greeting on variable day

on:
  workflow_dispatch

env:
  DAY_OF_WEEK: Monday

jobs:
  greeting_job:
    runs-on: ubuntu-latest
    env:
      Greeting: Hello
    steps:
      - name: "Say Hello Mona it's Monday"
        run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"
        env:
          First_Name: Mona
```

- 構成変数はブラウザ上で設定できる

  - ここで設定

    - https://github.com/shusukeO/test_gha/settings/variables/actions

  - env で参照

    - env.DAY_OF_WEEK

  - ここに書いてある
    - https://docs.github.com/ja/actions/learn-github-actions/variables

- Go でテストしてビルドする
  - push してテストを回して、テストの結果とともに Github 上に残すことができる
  - 便利そう！
  - 参考
    - https://docs.github.com/ja/actions/automating-builds-and-tests/building-and-testing-go

```YAML
 name: Go
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - name: Setup Go
        uses: actions/setup-go@v4
        with:
          go-version: '1.21.x'
      - name: Install dependencies
        run: go get .
      - name: Build
        run: go build -v ./...
      - name: Test with the Go CLI
        run: go test
```
