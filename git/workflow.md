New feature
```
git checkout -b feature/my_feature develop
git push -u origin feature/my_feature
```

Merge feature
```
git checkout develop
git merge --no-ff feature/my_feature
git branch -d feature/my_feature
git push origin --delete feature/my_feature
```

Deploy
```
git checkout master
git merge --no-ff develop
git tag -a release/1.1.0
git push --follow-tags
```