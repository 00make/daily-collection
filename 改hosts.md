# 改HOSTS 

## 改hosts还是传统手法

1.获取hosts文件

具体可以打开下面的网址：https://cdn.jsdelivr.net/gh/googlehosts/hosts/hosts-files/hosts，然后会下载一个名为hosts的文件

2.把老hosts里面自定义的内容复制到下载的hosts里面

3.打开C:\Windows\System32\drivers\etc，把刚才下载的hosts文件复制进去替换就行了。

## 最后刷新一下DNS缓存，加速某些网站。

按下Windows徽标键+R，输入cmd，在出来的框里输入ipconfig /flushdns 就可以