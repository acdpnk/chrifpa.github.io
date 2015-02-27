---
permalink: /2015-02-11-faking-email-sender-101
date: 2015-02-11 12:33
title: "Faking eMail sender 101"
layout: post
tags:
---

For years I've been telling anyone willing to listen that the sender's address shown in an email is about as reliable as that on a letter made from a dead tree. 

If you want to try it for yourself, here's how I did it.

{% highlight python %}
# coding: UTF-8

# Import smtplib for the actual sending function
import smtplib

# Import the email modules we'll need
from email.mime.text import MIMEText

# me == the sender's email address
# you == the recipient's email address
me = "css+clusterbench@rrzn.uni-hannover.de"
you = "chrifpa@gmail.com"

# Create a text/plain message
msg = MIMEText("¯\_(ツ)_/¯")

msg['Subject'] = 'Message'
msg['From'] = me
msg['To'] = you

# Send the message via our own SMTP server, but don't include the
# envelope header.
s = smtplib.SMTP('smtp.uni-hannover.de', 587)
s.starttls()
s.login("Your Username", "Your Password")
s.sendmail(me, [you], msg.as_string())
s.quit()
{% endhighlight %}
