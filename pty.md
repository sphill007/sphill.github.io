# 切换shell
有时候直接反弹回来的shell不好用或者无法使用，可以尝试下面方式得到好看好用的shell
```
python -c 'import pty;pty.spawn("/bin/bash")'
```
