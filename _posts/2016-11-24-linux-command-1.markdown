---
layout: post
title:  "Linux command"
date:   2016-11-24 22:49:20 +0800
categories: Linux
---

#### 1.批量创建文件
{% highlight shell %}
mkdir playground
touch playground/{A..Z}cadcs{2..3}.txt
{% endhighlight %}
注: 要在bash下执行, zsh下会存在{A..Z}无法展开的情况

#### 2.查找以.txt结尾文件，并统计此类文件的个数
{% highlight shell %}
find playground -name *.txt | wc -l
find ./playground -name *.txt | grep 3.txt | wc -l
等同于
find ./playground -name *3.txt | wc -l

区分
find ./playground -name *.txt | grep [^YO]cadcs3.txt$
find ./playground -name *.txt | grep -v [YO]cadcs3.txt$
find ./playground -name *.txt | grep -c [^YO]cadcs3.txt$
{% endhighlight %}

#### 3.往找到的文件中，批量写入内容
{% highlight shell %}
find . -name \*.txt -exec sh -c 'echo "abcdef" >> "$1"' -- {} \;
find . -type f -name \*.txt -exec sh -c 'echo "abcdef" >> "$1"' -- {} \;
{% endhighlight %}
注: 确保find出来的都是文件，否则写入的时候会报错

#### 4.查找文件中的内容
{% highlight shell %}
grep -h hhh *.txt # -h 不显示文件名，只显示查到的结果
grep hhh *.txt | grep -n abc  # -n 显示行号
grep -E h{4} *.txt  # -E 支持正则
{% endhighlight %}

#### 5.生成随机的电话号码
{% highlight shell %}
for i in {1..10}; do echo "(${RANDOM:0:3}) ${RANDOM:0:3}-${RANDOM:0:4}" >> phonelist.txt; done
grep -E '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$' phonelist.txt   #找到符合规则的号码
grep -Ev '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$' phonelist.txt   #找到不符合规则的号码
{% endhighlight %}

#### 6.查找文件，排序
{% highlight shell %}
find . -name \*.txt | sort | head -n 5
find . -name \*.txt | xargs du -h | sort -r | head -n 5  #按大小排序，找到最大的5个
find . -type f -name \*.txt | xargs ls -lt | head -n 5   #按时间排序，找到最晚创建的5个, -t 按时间排序
find . -type f -name \*.txt | xargs ls -ltr | head -n 5  #按时间排序，找到最早创建的5个, -r 倒序
{% endhighlight %}
注: sort默认是按从小到大排序


#### 备注:
* [文本处理](https://billie66.github.io/TLCL/book/zh/chap21.html)
* [查找文件](https://billie66.github.io/TLCL/book/zh/chap18.html)
