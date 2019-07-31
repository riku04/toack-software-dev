# Gitテンプレート使用方法

### Commit
1. 本Repositoryのcommit_templateを対象Repository内ににコピー
3. GitBashで以下を入力
<pre>
git config --global commit.template ".commit_template"
</pre>
3. Commit後のエディターにテンプレートが挿入されているので、それに倣ってcommitメッセージを記述する  

※Bash以外でのCommitでは未確認
***
### Issue/Pull Request
1. 本Repositoryの.githubを対象Repository内ににコピー
1. GitHubでIssue作成時にテンプレートが選択できるようになるので見合ったものを選択
GitHubでPullRequest作成時にテンプレートが挿入されているのでそれにあわせて記述



