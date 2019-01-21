# 21 Jan 2019

## English Apostrophe

source : [apostrophe video](https://www.youtube.com/watch?v=LzzJHwmQ_Oc)

apostrophe, `'` is used in :
- *present continous verb*
For example for word `going`, the letter `g` is removed become `goin'`.
Another examples :
`Where are you goin'`
`What are you doin'`

> This is for *informal* term, do not use in writing formal paper.

- *contraction* : meaning combine to words become 1, in the process some letters is removed.
```
"are not" : `aren't`
"I would" : "I'd"
"They have" : "they've"
```

- *Posession* of a thing that belong to somebody
```
"ST. James's Park"
```

## Git Prune

Problem : How to clean up your local repository by removing *unreachable objects*, such as commits which can not be accessed through branch or tag.

> Question : How this is happened ? How the commits is not accessable from branch/tag ?

> Answer : When You do `git hard reset commit-hashcode` or `squash` the commits become one. All the previous commits still there. Git still keep it. That is why, is so hard to lose data in git repository. You can try `git reflog` command to see the changes in your branches commits.

Solution to fix `*unreachable objects* 

This command will *pretend* to running the `prune` process, which will display *list of commits* need to be removed.
```
git prune --dry-run --verbose --expire=now
```

Actualy run the `prune` process
```
git prune --verbose --expire=now
```

source : https://www.atlassian.com/git/tutorials/git-prune

## Git Remote Prune

Problem : How to clean up *local origin* branch which is staled or deleted on the *origin repository*.

*Pretend* to run the `remote prune` process, which will display *list of branches* need to be removed.
```
git remote prune origin --dry-run --verbose --expire=now
```

Actualy run the `prune` process
```
git remote prune origin --verbose --expire=now
```

https://stackoverflow.com/questions/36082788/what-is-git-pruning?noredirect=1&lq=1https://git-scm.com/docs/git-remote#git-remote-empruneem



