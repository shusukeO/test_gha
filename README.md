# test_gha

GHA(GitHub Actions) を試す

## メモ

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
