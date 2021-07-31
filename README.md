## memo

`git push -u origin main` -> `iron` respository

`git push -u master main` -> `github.io` respository

```bash
$ git branch -a
* main
  remotes/master/main
  remotes/origin/main
```

### customize SLD
set `Custom domain` as `iron.magictomagic.com` in [Pages][https://github.com/magictomagic/iron/settings/pages] once git action complete because the deploy method may change the domain back

## TODO

+ 更新`e-linkedin`字段
+ 看对应action涉及的源码或找其它原因，不要让它改回默认
```yml
- name: Deploy
        uses: peaceiris/actions-gh-pages@v3
```