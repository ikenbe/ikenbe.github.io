---
type: posts
title:  "给 PLEX 服务器批量缩图的脚本"
date:   2021-05-21 13:55:00 -0700
---
## 起因

在家里使用 Plex 来管理手头的各种媒体不知不觉已经很多年了。 最近发现 Plex Server 里面的 Metadata 文件夹异常地大，几乎占了我的 NAS 的 SSD 容量的一半。分析得知其中一些搜刮器(Scraper)自动下载到的图片分辨率超过千万像素，而这些图片的用途只是媒体的封面图和页面背景图，这么大的尺寸根本没用。于是写了点代码来自动处理这个东西。

因为 Plex 的插件使用的都是 Python， 我一开始也打算用 Python。 看了一下 Pillow (Python 的图片处理库) 之后感觉效率不佳，就还是用了 Shell Script 来写。 所以这东西的依赖是 bash 和 imagemagick， 在不同的 distro 下表现或者使用的命令可能略有不同。

## 代码如下

```bash
#!/bin/bash
OIFS="$IFS"
IFS=$'\n'

## Parameter how many folders you want to optimize, default @100 
target=${1:-100}
## Use parameter "clear" to clean up marks of 
## EDIT BELOW TO MATCH YOUR OWN PATH TO PLEX SERVER!!!
path1=/home/plex/config/Library/Application\ Support/Plex\ Media\ Server/Metadata/Movies
## EDIT HERE TO CHANGE DESIRE IMAGE SIZE
size=900x900

suffix1=/Contents/com.plexapp.agents.phoenixadult
count=0
if [[ $1 == "clear" ]];then
    find "$path1"/ -name "opted" -exec rm -f {} \;
    exit 0
fi

for folder_1 in "$path1"/*/; do
    for folder_2 in "$folder_1"*; do
        if (( count < target )) && [ -d "$folder_2""$suffix1" ] && [ ! -f "$folder_2""$suffix1"/opted ];then
            mogrify -resize $size "$folder_2""$suffix1""/art/"*
            mogrify -resize $size "$folder_2""$suffix1""/posters/"*
            touch "$folder_2""$suffix1"/opted
            echo "${folder_2:79}"" done"
            let count+=1
        fi
    done
done
echo $count


IFS="$OIFS"
```

## 效果

空间减负15GB， 比预想中差一点但是可以接受。 也许 imagemagick 有更详细的压缩/优化选项，暂不深究了。
