# Gitテンプレート使用方法

### Commit
1. 本Repositoryのcommit_templateを任意の場所にダウンロードする
2. GitBashで以下を入力
<pre>
git config --global commit.template ファイルパス.commit_template

例：git config --global commit.template C://Users/isobe-h/Desktop/git/.commit_template
</pre>
3. Commit後のエディターにテンプレートが挿入されているので、それに倣ってcommitメッセージを記述する  

※VS Codeなどのエディターでもテンプレート使用可能です
***
### Issue/Pull Request
1. 本Repositoryの.githubフォルダーを対象Repositoryのルートにコピー
1. GitHubでIssue/PR作成時にテンプレートが選択できるようになるので見合ったものを選択
