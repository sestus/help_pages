
<!--
.. title: SMTP for free users
.. slug: SMTPForFreeUsers
.. date: 2015-05-13 14:35:28 UTC+01:00
.. tags:
.. category:
.. link:
.. description:
.. type: text
-->




Free users are restricted to HTTP/HTTPS only, to a
[whitelist of sites](https://www.pythonanywhere.com/whitelist/). Because
most email services work over SMTP, which is not HTTP or HTTPS, that means you
cannot normally use SMTP on Free accounts.

If you want to send email, you have two options:

##Use an HTTP/HTTPS-based email service

[Mailgun](http://mailgun.com/) is a site that allows you to send email using
HTTP(S) requests, and its API endpoint is on our whitelist.  This is the most
reliable option, and works well so long as your code isn't limited to using
SMTP.


##Use Gmail's SMTP servers

We have added a special exception to our firewall rules for Gmail's SMTP
servers. If you use them, it should work.

However, we have to hard-code the IP addresses of Google's servers into our
firewall, and these sometimes change, which means that, on occasion, Google may
switch to a new Gmail server which we don't know about, and that would
temporarily block email until we are able to update the firewall.

For Django, you can use the settings:

    :::python
    EMAIL_HOST = "smtp.gmail.com"
    EMAIL_HOST_USER = "yourusername@gmail.com"
    EMAIL_HOST_PASSWORD = 'yourpassword'
    EMAIL_PORT = 587
    EMAIL_USE_TLS = True



###Google security blocking and setting up an App-Specific password

Google sometimes blocks SMTP requests from IP addresses it doesn't recognise.
If you're finding emails aren't getting sent, try visiting the security page on
your Google account, and have a look for security notifications. You may need
to approve some requests, or generate an application-specific password.
[This page is often a good starting point](https://support.google.com/accounts/answer/6010255?hl=en>).
*(Some people have reported that they can't access the correct security settings
on that page from the normal web interface and have to use a mobile device to
see them there. Thanks, Google! ;-)*
