---
title: "My Software Universe Cheat Sheet"
layout: post
date: 2017-11-10 11:15
image: /assets/images/markdown.jpg
headerImage: false
tag:
- java
- tmux
- shell
star: false
category: blog
author: peterbelko
description: Markdown summary with different options
---

List of useful commands for all technologies I regularly use.

## Content:

* [JVM](#jvm)
* [Shell](#shell)
* [Tmux](#tmux)
* [AWS CLI] (#aws-cli)

## JVM

Show running Java processes:
{% highlight shell %}
jps
{% endhighlight %}

Show thread stack trace for Java process:
{% highlight shell %}
jstack <PID>
{% endhighlight %}

Every 500ms print GC cause of the running JVM process
{% highlight shell %}
jstat -gccause <PID> 500ms
{% endhighlight %}

## Shell

#### misc
Show all process as a tree
{% highlight shell %}
ps ufax
{% endhighlight %}

Watch file size of the file
{% highlight shell %}
watch du -sh file.txt
{% endhighlight %}

Find text in files
{% highlight shell %}
find . -name "*.txt" -exec grep -n -H "text" {} \\;
{% endhighlight %}

#### netcat
listen on specific port and forward output to the file
{% highlight shell %}
nc -l 5555 > output.raw
{% endhighlight %}

connect to host and port and send some text
{% highlight shell %}
nc localhost 5555
> Hello World!
{% endhighlight %}

#### tcpdump
Sniff communication on localhost interface (`lo`) and port `5555` and write it to the file
{% highlight shell %}
tcpdump -i lo -w recording.pcap port 5555
{% endhighlight %}

#### awk
Remove empty lines from a file
{% highlight shell %}
awk 'length($0) > 0 {print $0}' file_with_blanks > new_file_wo_blanks
{% endhighlight %}

#### sed
Escape quotes int the file `$f`
{% highlight shell %}
sed 's/\"/\\\"/g' $f
{% endhighlight %}

## Tmux

Set start directory for current tmux session
{% highlight raw %}
Press 'Ctrl+B + :' and then write 'attach -c /path/to/start/directory'
{% endhighlight %}

## AWS CLI

List all instances with the project tag set to <value>

{% highlight shell %}
aws ec2 describe-instances --filters "Name=tag:Project,Values=<value>" --output text --query 'Reservations[*].Instances[*].[ImageId,State.Name,PublicIpAddress,Tags[*]]' | column -t
{% endhighlight %}
