### Gitを使った開発の流れ
- CommitおよびPull request,Issue作成時は当Repositoryのテンプレートを用いる。

***
### 作業時の流れ
1. master branchから記述的なbranchをローカル、GitHub上に同名で作成する。  
ローカルで作成して --set-upstream　をつけてpushでも可。  
<pre>
　　　例）user-content-cache  
　　　　　add-user-notice  
</pre>
　　 Comment追加、Indent修正などでもそれぞれbranchを作成してcommitの粒度を細かくする。  
　　 Commitの粒度は切りの良い単位、もしくは戻したい単位などで行うとよい。

2. 作業を行う  
&nbsp;branchは定期的にpushして他の担当者に作業状況を共有するとともに、不意の喪失からを防ぐ。  
&nbsp;助言やFeedbackが欲しい時は 、Pull Request 名の頭に [WIP] をつけた[WIP]Pull Requestを送る。   
&nbsp;WIP(Work In Progress)

3. GitHubの同名Repositoryにpushする。  
4. Pull Requestを送り、他の開発者にレビューしてもらう  
&nbsp;問題があれば2に戻る。
5. レビューが終わったらmasterにmergeして、このbranchを削除する

***
### リリース時
1. master branchからrelease branchを作成  
&nbsp;リリースの際は*中央repositoryのmasterを用いる。　　
1. 回帰テストやDeployテストをおこなう
1. リリースが終わったらmasterにmergeしてtagを打った後、このbranchを削除

#
*Repositoryを管理者している人のRepository