Annie [options] URL [URL... ]

下载视频：annie https://www.youtube.com/watch?v=dQw4w9WgXcQ 

注意：如果url包含特殊字符，则需要用单引号或者双引号包裹起来。

-i 参数显示所有有效的视频的质量(分辨率)，但是不下载

使用 annie -f stream "URL" 下载由 -i 选项列出来的视频

如果给annie一个资源的链接，那么他就会被自动下载

-p 选项下载视频列表列出的全部视频

- ​	-start x  : 以x开始的视频列表，如果没指定则默认是1
- ​	-end y   : 以y结束的视频列表，如果没指定则默认是last 
- ​	-items x,y,z   : 指定视频列表的第 x,y,z 视频下载

你也可以一次下载多个视频：annie -i url1 url2 url3 ... ,这些视频链接会被一个接一个下载。

也可以指定一个包含url列表的文件，然后从该文件中读取链接逐一下载。



