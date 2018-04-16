在liunx中 **ll** 和 **ls -l** 输出的结果是一样的，这是因为 **ll** 就是 **ls -l** 的别名，而命令的别名是通过 **alias** 命令来设置的

alias 的基本使用方法为：

> alias 新的命令='原命令 -选项/参数'

如设置 ** echo hello world ** 的别名为 **ehw**

> alias ehw='echo hello world'

注意'='号两边不要空格

查看系统已经设置的别名：

```
[root@localhost ~]# alias -p
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias ehw='echo hello world'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

```

通过 **unalias** 命令取消刚刚设置的别名

> unalias ehw
	