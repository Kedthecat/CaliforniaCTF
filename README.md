Welcome to the writeup for this room!

First off let’s start the machine up and wait 5 mins.
	
	Enumeration

I always start my enumeration with nmap.


as you can see there are 3 ports open



Let's look which services are they

21 = FTP with anonymous login !

22 = SSH

80 = HTTP web server

	FTP login

So anonymous login looks cool let's login with anonymous credentials

We got a file. Let's look what is that

So it's all about web server let's look at it..

	WEB application

We have just default apache page, so let's use some tools

As you can see there is a directory called "hotelbx". Let's check it!

It seems the page is using "Hotel Reservation System". Let's check if there was an exploit to use

	SQL Injection

Cool let's try to use it

and it works.. Let's try to dump the data with sqlmap

We got 2 hashes Let's try to crack them

so we have scott's credentials let's login with ssh


	USER & ROOT


So first things first let's get the user flag.

Now we can try to escalate our privileges.

That file looks suspicious.

If we go and look gtfobins we can escelate our privilege with this command. Let's try

and we are root!!


