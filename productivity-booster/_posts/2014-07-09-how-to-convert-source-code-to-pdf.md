---
layout: post
title: How to convert Ruby source code to pdf in Linux
---

In this post I want to show to convert source code to pdf using Linux. We'll use file **base.rb** from **Sinatra** framework as example.

## Converting Ruby source code to HTML

First thing we need to is to convert our source code to html. To convert it we'll use **code2html**. Install it right now:

{% highlight sh %}
sudo apt-get install code2html
{% endhighlight %}

We want to convert **base.rb** file from Sinatra source code. We want to include line numbers in our conversion so we'll use flag -n to add them.

Let's convert it.

{% highlight sh %}
code2html -n base.rb base.html
{% endhighlight %}

Code2html will take work for conversion. Look at our converted file in browser.

![how to convert source code to html](/images/src2html.png)

Let's see, our source code is well formated with proper indentation, syntax highlighting and line numbers.

## Converting source code to pdf

For converting source code to pdf we can use multiple tools, we'll start with **Libre Office**. 

### Converting HTML source code using LibreOffice

If you haven't already installed LibreOffice, you can do it now.

{% highlight sh %}
sudo apt-get install libreoffice
{% endhighlight %}

 Open your file in LibreOffice Writter and choose **Export** like this:

![how to export file  in libre office](/images/export-file.png)

 Choose PDF from menu

![how to convert html file to pdf](/images/export-file-2.png)

Click on export.

Now you can take a look at PDF file.

![how to convert html to pdf in libre office](/images/html2pdf-libre-office.png)

Looks nice isn't it. It includes syntax highlighting and indentation. Of course you can use other tools, for example **pandoc**.

### Using Pandoc to convert HTML source code to PDF

If you're looking for other solution you can use Pandoc.

First install it.

{% highlight sh %}
sudo apt-get install pandoc
{% endhighlight %}

Now when we have pandoc installed we can use it to convert our source code.

{% highlight sh %}
pandoc base.html -o base.pdf
{% endhighlight %}

We've specified -o flag here, what is output. Take look at the file. 

### Converting HTML using online PDF converter

For converting HTML, we can try great tool for converting webpages and HTML files. Go to [pdfcrowd](https://pdfcrowd.com) website.

 First click on convert HTML file

![how to convert HTML to PDf online](/images/pdfcrowd.png)

Then upload file from your and click on **convert to pdf**

Your file should like previous one.

Ok so we're at the end of our tutorial. If you like it, share it with clicking on sidebar buttons.
