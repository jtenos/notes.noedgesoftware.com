---
layout: home
---

Copied from:
- [https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit](https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit)
- [https://www.git-tower.com/learn/git/faq/change-author-name-email](https://www.git-tower.com/learn/git/faq/change-author-name-email)

Worked for me, but there's some scary stuff here, so I wouldn't recommend this unless you know what you're doing - I certainly didn't.

Find the last good commit:

```
git rebase -i -p hash-of-last-commit
```

Editor opens: change all "pick" to "edit" for the ones you want to edit, then save.

You'll be stopped one at a time until it's done - put this in each time:

```
git commit --amend --author="My Name <myname@example.com>" --no-edit
git rebase --continue
```

Once complete:

```
git push --force --tags origin 'refs/heads/*'
```
