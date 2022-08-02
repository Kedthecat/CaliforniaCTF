Welcome to the writeup for CaliforniaCTF that i made!

First off let’s start the machine up and wait 5 mins.
	
	Enumeration

I always start my enumeration with nmap.

as you can see there are 3 ports open

![image](https://user-images.githubusercontent.com/73278123/156879493-1cc4106d-62df-4a1d-b40b-2b281c87fea8.png)

Let's look which services are they

![image](https://user-images.githubusercontent.com/73278123/156879515-61b1190d-082b-4922-8d0e-1af740cf332e.png)

21 = FTP with anonymous login !

22 = SSH

80 = HTTP web server

	FTP login

So anonymous login looks cool let's login with anonymous credentials

![image](https://user-images.githubusercontent.com/73278123/156879562-fda0e074-8c0f-4ca1-9883-0e8346103828.png)

We got a file. Let's look what is that

So it's all about web server let's look at it..

![image](https://user-images.githubusercontent.com/73278123/156879605-dca58440-3d94-40bd-b7bf-e01058bd67e4.png)


	WEB application

We have just default apache page, so let's use some tools

As you can see there is a directory called "hotelbx". Let's check it!

![image](https://user-images.githubusercontent.com/73278123/156879741-1579a1c6-d921-4fb6-8d76-5d2cda542fb3.png)

It seems the page is using "Hotel Reservation System". Let's check if there was an exploit to use

![image](https://user-images.githubusercontent.com/73278123/156879778-5d736f2d-abe1-481a-a223-efd9f6c0c879.png)

![image](https://user-images.githubusercontent.com/73278123/156879809-1ee5bf38-5c47-40ee-98df-a51b88fac9f8.png)

	SQL Injection

Cool let's try to use them. First try to login with 'or 1=1 --

![image](https://user-images.githubusercontent.com/73278123/156879874-285d0160-9e50-4d47-a46b-9a846331f0e2.png)

and it works..

Now let's try other sql exploit at this page with sqlmap

![image](https://user-images.githubusercontent.com/73278123/156879938-9572b202-0d87-4631-828f-75609f7ef1de.png)

We got 2 hashes Let's try to crack them

![image](https://user-images.githubusercontent.com/73278123/156880015-98fbb7d1-ed31-49d1-a77f-5d0c6d4ac68a.png)

so we got scott's credentials let's login with ssh

![image](https://user-images.githubusercontent.com/73278123/156880078-fa798983-520b-4577-a05b-f526a8a2545c.png)
![image](https://user-images.githubusercontent.com/73278123/156880118-19912c38-f938-40ad-860e-214fe01eccee.png)

	USER & ROOT

So first things first let's get the user flag.

![image](https://user-images.githubusercontent.com/73278123/156880159-a9c4e381-3921-44ef-94ea-362216468597.png)

Now we can try to escalate our privileges.

That file looks suspicious.

![image](https://user-images.githubusercontent.com/73278123/156880202-707c25fb-2d54-44db-9773-eaf5e1e5ce7a.png)

If we go and look gtfobins we can escelate our privilege with this command. Let's try

![image](https://user-images.githubusercontent.com/73278123/156880225-e5d183be-73bb-4622-82c8-97a750dc340d.png)
![image](https://user-images.githubusercontent.com/73278123/156880243-179905a1-89ca-433e-89ed-cfc42775da62.png)
![image](https://user-images.githubusercontent.com/73278123/156880261-b86c3cbc-5252-4b84-9af3-2962cf1b2c3b.png)

and we are root!!


