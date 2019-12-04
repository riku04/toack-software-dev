# TOACK　ソフトウェア開発ガイド

本RepositoryではTOACKにおけるソフトウェア開発ガイドを提供します。

***

### 1. 原則としてプロジェクト成果物は全てGitHubで管理する

 Git、GitHubについては下記のサイトなどを参照。  
  [今日からはじめるGitHub 〜 初心者がGitをインストールして、プルリクできるようになるまでを解説](https://employment.en-japan.com/engineerhub/entry/2017/01/31/110000)

 管理するのは主に下記のファイルとなる

- Source Code
- 設計書や仕様書などの書類
- DB Schema,Data
- Middlewareなどの設定ファイル
- Libraryなどの依存関係の定義

　.gitignoreを適切に作成し、仮想環境など管理する必要ないファイルは省く。


### 2. 運用は[Git開発フロー](/Gitを使った開発の流れ.md)に従う

### 3. 問題点や課題は全てGitHubのIssuesで管理する

### 4. 原則としてコーディング規則に従う
   
   - [C#](/csharp-guide/)
   - [Python](/python-guide)
   - [Java](/java-guide)
   - [HTML/CSS](/html:css-guide)
   - [Javascript](/javascript-guide)
   - [Dart](/dart-guide)
   
   なお、やむを得ない場合や規則に従わないほうが良いと判断された場合においては従う必要はない。
