# Intrude between an application and the server it uses to receive data

I don't know if you have read the article [SOLUTION: Hacking This Site – Application – Application Challenge 2](https://ilfavolosomondodileo-wordpress-com.translate.goog/2023/04/18/soluzione-hacking-this-site-application-application-challenge-2/?_x_tr_sl=it&_x_tr_tl=en&_x_tr_hl=it&_x_tr_pto=wapp)
 in which I explained how to crack a program by sniffing the packets transmitted and received by it.
To summarize, the program would have given us a password, provided that the license code entered, completely unknown to us, had been equivalent to one of those issued by a server.
In this article I will explain how to intervene between you and the server.
It almost looks like a [man in the middle attack](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) with the difference that one of the two parties is completely cut off, in this case the server.
The software will think it is communicating with the server but in reality it will be communicating with us.
This will be possible, thanks to a connection hijacking. The hijacking consists of locking down any connection to the server from our PC, and setting up another server which will simulate it and accept connections from the application.
On the other hand, the server will not receive any communication from the software we want to crack.
Having said that I would say that we can start, but first I think it is essential that you read the article [SOLUTION: Hacking This Site – Application – Application Challenge 2](https://ilfavolosomondodileo-wordpress-com.translate.goog/2023/04/18/soluzione-hacking-this-site-application-application-challenge-2/?_x_tr_sl=it&_x_tr_tl=en&_x_tr_hl=it&_x_tr_pto=wapp)
.
Assuming that you have already read the previous article, let's start by ensuring that our computer cannot communicate with the hackthissite.org server.
If you go to the [Hack This Site](https://hackthissite.org/) site you will see that everything works correctly.
You can consult the site without problems.
To secure the connection, run "Notepad" as administrator and open the following file.

```
C:\Windows\System32\drivers\etc\hosts
```

So let's add the command displayed below to the end of the file.

```
127.0.0.1	hackthissite.org
```

Between the IP 127.0.0.1 which represents our local IP and hackthissite.org there is a space resulting from a tab. In practice you will only have to press the button TAB.
Below I show you the contents of my modified hosts file.
The file is made up exclusively of comments that explain its operation and the record just added.
Comments are preceded by the character #.

```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

127.0.0.1	hackthissite.org
```
This command says that, if any connection to the hackthissite.org domain starts from our PC, this will have to be diverted to our local IP 127.0.0.1.
Thanks to this trick it is possible to do lots of tricks, but at the same time also protect the PC from connection to servers capable of corrupting the computer with malicious programs.
If you have applied the change, and try to go to the [Hack This Site](https://hackthissite.org/) you will get this.

![impossibile-raggiungere-il-sito](https://github.com/user-attachments/assets/ebb17959-e2d6-44b0-a447-a59edd0899f9)

Don't worry, because all you need to do is delete the record previously written in the hosts file to return to the previous condition and thus remove the hijacking.
At this point we must create a server that waits for a connection from any software that tries to connect to hackthissite.org.
Any software present on our computer will be able to communicate with any servers, except those that try to connect to the server that responds to the domain hackthissite.org
In this case the connection will be diverted to our local IP 127.0.0.1
This system can also be useful for monitoring the activity of a program and sniffing its requests, although I recommend you use [Wireshark](https://www.wireshark.org/) which is certainly more advanced.
You can also use this system to create a sort of proxy.
The client tries to communicate with a server but the connection is redirected to our proxy. The proxy that will act as an intermediary then decides whether to unblock the connection by forwarding the requests to the server and returning the data to the client, or to secure the connection.
Obviously these are just a few examples.
Let's go back to creating the server.
To set up a server for this little game you don't have to go crazy. In these cases I use [NETCAT](https://en.wikipedia.org/wiki/Netcat). Better known as the Swiss army knife of networks. It allows you to set up a client or server in just a few seconds. It contains many functions and I would say that it is an indispensable tool.
You can download it from the [NMAP.ORG](https://nmap.org/dist/ncat-portable-5.59BETA1.zip)
website . To make this experience even easier for you, I decided to develop a BATCH file that you can download by clicking on the following image.
FAKE SERVER could be identified as malware, as it integrates NETCAT. By analyzing FAKE SERVER, you will realize that it does not represent a threat in any way. To prevent some software from identifying it as malware, I protected the compressed file with the password **ilfavolosomondodileo.wordpress.com**

**[FAKE SERVER](https://www.ware.altervista.org/ilfavolosomondodileo.wordpress.com/FAKE%20SERVER/FAKE%20SERVER%201.0%20(ilfavolosomondodileo.wordpress.com).zip)**

![screenshot-2023-04-20-15 11 31](https://github.com/user-attachments/assets/64855429-6aa9-47c6-b3b9-fee43fb0eaa3)


**[FAKE SERVER](https://www.ware.altervista.org/ilfavolosomondodileo.wordpress.com/FAKE%20SERVER/FAKE%20SERVER%201.0%20(ilfavolosomondodileo.wordpress.com).zip)**

**VERSION:** 1.0\
**FILE:** FAKE SERVER 1.0 (ilfavolosomondodileo.wordpress.com).zip\
**PASSWORD:** ilfavolosomondodileo.wordpress.com\
**BYTE:** 5.599.683\
**HASH MD5:** b4 23 96 47 ed 67 c1 61 77 55 22 ed 9a 80 68 ab

I called the BATCH FAKE SERVER.
I adopted a revolutionary structure of the source code, also adding a touch of old-fashioned graphics.
I have shown you all the various procedures to use to set up this system, but you are not forced to carry them out manually. FAKE SERVER will take care of everything for you.
Rather than explain every single command that makes up FAKE SERVER, I will show you what it does, but not before explaining what we need.
Let's summarize.
As I wrote, on the PC we need to divert any connection to hackthissite.org at 127.0.0.1
We need to create a server that simulates the server that responds to the hackthissite.org domain.
Subsequently, once our server is running, no all we need to do is start the [Application Challenge 2](https://www.hackthissite.org/missions/application/app2win.zip) application .
After entering a product key, Application Challenge 2 will try to connect to hackthissite.org to download valid product keys and compare them with the one we entered. It will actually connect to our server which will return what hackthissite.org would have returned but with a small change.
In fact, the FAKE SERVER will transmit personalized product keys which will still be considered valid by the Application Challenge 2 program. The program will then return the password to us.
FAKE SERVER, can be used to crack all programs that have similar behavior to Application Challenge 2.
Obviously, not being a professional server, it has some limitations.
Every now and then programs, when connecting to servers to send and receive packets, often request one file and in other cases require the download of multiple files.
To have the software download multiple modified files, you need to have an application that allows you to create a professional server.
Maybe we'll address this later.
To use FAKE SERVER it is also essential to first understand what type of communication takes place between the application we want to crack and the server, as we should then know what data to feed it and how we can modify it.
Now I'll explain how FAKE SERVER works.
Once downloaded, unzip the compressed file and enter the FAKE SERVER folder.
Start FAKE SERVER by double clicking on the file **SERVER.BAT**
FAKE SERVER will present you with a menu.

![screenshot-2023-04-20-15 11 31](https://github.com/user-attachments/assets/d46831ea-1981-48f3-9651-4797b13623d7)

FAKE SERVER was developed in English. In any case, the summary table presented below should help you better understand the function associated with each button.

| **KEY** | **FUNCTION**                                                           |
|:-------:|------------------------------------------------------------------------|
|    1    | START FAKE SERVER                                                      |
|    2    | STOP THE HIGHER                                                        |
|    3    | RESTORE THE BACKUP OF THE hosts FILE                                   |
|    4    | DELETE ALL BACKUP FILES OF THE hosts FILE                              |
|    5    | RESTORE THE ORIGINAL hosts FILE                                        |
|    6    | OPEN THE hosts FILE CURRENTLY USED BY THE SYSTEM                       |
|    7    | OPEN THE FOLDER CONTAINING THE hosts FILE CURRENTLY USED BY THE SYSTEM |
|    8    | EXIT FAKE SERVER                                                       |

To start the server that will be used to crack the application, press the button **1** on your keyboard. Alternatively, you can press the key **TAB** several times until you are prompted with the number associated with the function you wish to perform.
By choosing the function associated with the button **1**, you will be shown the following screen.

![screenshot-2023-04-20-15 12 15](https://github.com/user-attachments/assets/6a5b576b-f522-48fd-b90d-4891d674f7c7)

You will be asked to specify the hostname to which the server we should simulate responds. The one to which the application we are trying to crack will try to connect.
You have two options to do this. Press **TAB** until the desired domain appears, or type directly **hackthissite.org** and then press **RETURN**.
FAKE SERVER will store all hostnames you type. It will save them inside the folder **INPUT\HOSTNAME** and you can browse them during this process by pressing the button **TAB**.

![screenshot-2023-04-20-15 12 19](https://github.com/user-attachments/assets/10752f21-375b-4412-81a7-1d8b3d276709)

You will then be asked to specify a port between **1** and **65535**. For more information I suggest you consult the [List of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers) page .

![screenshot-2023-04-20-15 12 28](https://github.com/user-attachments/assets/f0437293-de96-45cc-997d-8de1f438e31a)

Naturally the port must be the one used by the application we want to crack, to communicate with its server. You will get it when analyzing with packet sniffing software, such as Wireshark.
If no port is specified and you press **RETURN**, the default port is used **80**, which is the port usually used for the HTTP protocol.
Alternatively you can manually type the port number which will be saved inside the folder **INPUT\PORT**.
Subsequently, during this request, you can browse the various ports used previously by pressing the button **TAB**, or alternatively you can type the port number manually. At the moment, using the button **TAB** you can select one of the doors that I consider most important.

![screenshot-2023-04-20-15 12 34](https://github.com/user-attachments/assets/8e19130a-9a15-4086-b06c-1ddbf31ef006)

Subsequently, if no file is found, **OUTPUT.TXT** one will be created and you will be asked to modify it. Alternatively, you will be offered to modify the file **OUTPUT.TXT** already present in the FAKE SERVER folder.

![screenshot-2023-04-20-15 12 45](https://github.com/user-attachments/assets/ba82d05a-a9a9-43b0-98e3-831fe94e3b04)

Remember to save the file **OUTPUT.TXT** after editing.
The file **OUTPUT.TXT** will then be fed to the first application that connects to FAKE SERVER.
At least with Application Challenge 2, you can afford to edit the file **OUTPUT.TXT** in real time to test, as Application Challenge 2 will require receipt of valid product keys every time we click on the "Authenticate" button. FAKE SERVER at that moment will transmit the requested data contained in the file **OUTPUT.TXT**
Below I show you the data present in the file **OUTPUT.TXT** which you can find in the FAKE SERVER folder.
Inside you will already find the data necessary to crack Application Challenge 2.
To feed it to different software, you can modify **OUTPUT.TXT** as you prefer. Obviously it will have to be modified correctly. You will have to enter the customized commands to be fed to the software to be cracked, but based on the packets previously analyzed using software such as Wireshark or another packet sniffer.

```
HTTP/1.1 200 OK
Date: Mon, 17 Apr 2023 22:19:59 GMT
Upgrade: h2,h2c
Connection: Upgrade, close
Vary: Accept-Encoding
Content-Length: 299
Content-Type: text/html
Content-Language: en
Server: HackThisSite
Access-Control-Allow-Origin: *
Content-Security-Policy: child-src 'self' hackthissite.org *.hackthissite.org htscdn.org *.htscdn.org discord.com; form-action 'self' hackthissite.org *.hackthissite.org htscdn.org *.htscdn.org; upgrade-insecure-requests; report-uri https://hackthissite.report-uri.com/r/d/csp/enforce
Referrer-Policy: origin-when-cross-origin
X-XSS-Protection: 0
Feature-Policy: fullscreen *
Public-Key-Pins-Report-Only: pin-sha256="YLh1dUR9y6Kja30RrAn7JKnbQG/uEtLMkBgFF2Fuihg="; pin-sha256="Vjs8r4z+80wjNcr1YKepWQboSIRi63WsWXhIMN+eWys="; max-age=2592000; includeSubDomains; report-uri="https://hackthissite.report-uri.com/r/d/hpkp/reportOnly"
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Report-To: {"group":"default","max_age":31536000,"endpoints":[{"url":"https://hackthissite.report-uri.com/a/d/g"}],"include_subdomains":true}
NEL: {"report_to":"default","max_age":31536000,"include_subdomains":true,"success_fraction":0.0,"failure_fraction":0.1}

11111-11111-11111-11111
22222-22222-22222-22222
33333-33333-33333-33333
44444-44444-44444-44444
55555-55555-55555-55555
66666-66666-66666-66666
77777-77777-77777-77777
88888-88888-88888-88888
99999-99999-99999-99999
```

After editing the file, **OUTPUT.TXT** close it.
After these steps, FAKE SERVER will go into listening mode on the port you have chosen. In this case the door **80**.
During the moment in which FAKE SERVER is waiting for some client, you will be reminded to reopen FAKE SERVER once the operation is completed, and go and execute the function associated with the button **2**. We will talk about this function shortly.

![screenshot-2023-04-20-15 12 57](https://github.com/user-attachments/assets/89136607-635a-4947-b95e-fe6cd2bda61a)

As soon as any application connects to FAKE SERVER, our commands will be transmitted to it.
Obviously, to be able to crack some software, we may be forced to do several tests and therefore modify the file **OUTPUT.TXT** several times.
The file **OUTPUT.TXT** can also be updated in real time, but until the software we are trying to crack requests to receive the data again, the changes applied will not take effect.
If necessary, close and reopen the software you are trying to crack and try to make it start another request to the reference server.
FAKE SERVER also creates a LOG file, which could be very useful for seeing which commands were sent by the software we are trying to crack. The file in question is called **LOG.TXT**
Below is an example of the LOG in which the commands sent by Application Challenge 2 and the commands sent by Google Chrome were saved, during manual connection attempts to 127.0.0.1 which I performed to make some tests.

```
Il Favoloso Mondo di Leo
https://ilfavolosomondodileo.wordpress.com/

FAKE SERVER 1.0 - LOG

----------------------------------------------------------------------------------------------------
19/04/2023  3:18:33 hackthissite.org 80
----------------------------------------------------------------------------------------------------

GET /app2.php?pass=kB2F.b0-sJS,k HTTP/1.0
Host: appchall2.hts

----------------------------------------------------------------------------------------------------
19/04/2023  3:18:35 hackthissite.org 80
----------------------------------------------------------------------------------------------------

GET /app2.php?pass=kB2F.b0-sJS,k HTTP/1.0
Host: appchall2.hts

----------------------------------------------------------------------------------------------------
19/04/2023  3:18:44 hackthissite.org 80
----------------------------------------------------------------------------------------------------

GET / HTTP/1.1
Host: 127.0.0.1
Connection: keep-alive
sec-ch-ua: "Not_A Brand";v="99", "Google Chrome";v="109", "Chromium";v="109"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: it,en;q=0.9
Cookie: HFS_SID_=0.213758566882461
dnt: 1
sec-gpc: 1

----------------------------------------------------------------------------------------------------
19/04/2023  3:18:46 hackthissite.org 80
----------------------------------------------------------------------------------------------------

GET / HTTP/1.1
Host: 127.0.0.1
Accept-Encoding: identity
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.70 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Sec-Fetch-Mode: navigate
Connection: close

----------------------------------------------------------------------------------------------------
19/04/2023  3:19:03 hackthissite.org 80
----------------------------------------------------------------------------------------------------

GET /app2.php?pass=kB2F.b0-sJS,k HTTP/1.0
Host: appchall2.hts
```

To terminate FAKE SERVER simply close the window.
If you want to try to crack Application Challenge 2 with FAKE SERVER using the **OUTPUT.TXT** built-in file, you can use the following product keys.

```
11111-11111-11111-11111
22222-22222-22222-22222
33333-33333-33333-33333
44444-44444-44444-44444
55555-55555-55555-55555
66666-66666-66666-66666
77777-77777-77777-77777
88888-88888-88888-88888
99999-99999-99999-99999
```

You can edit the file **OUTPUT.TXT** as you see fit and test new product keys. The important thing is that you respect the original syntax of the commands that will have to be fed to Application Challenge 2. To avoid problems, I always direct you to the article [SOLUTION: Hacking This Site – Application – Application Challenge 2](https://ilfavolosomondodileo-wordpress-com.translate.goog/2023/04/18/soluzione-hacking-this-site-application-application-challenge-2/?_x_tr_sl=it&_x_tr_tl=en&_x_tr_hl=it&_x_tr_pto=wapp) where you can see the commands that normal conditions are received by Application Challenge 2. Based on these commands you can modify the file **OUTPUT.TXT**
Now it should be clearer to you why every now and then, it may happen that CRACKs are downloaded which invite us to modify the hosts file or to temporarily disconnect from the internet.
Surely CRAKKARE Application Challenge 2 will not make us rich in economic terms but it will teach us a lot.
Do you remember that FAKE SERVER proposed to reopen the file **SERVER.BAT** once the operation was completed and execute the function associated with the button **2**?
This function allows you to restore the initial state of the hosts file and therefore cancel the hijacking, and it is important to perform it every time you finish your operations with the server.
I would say that it is essential to understand the behavior of this function.
FAKE SERVER, following your entry of hostname and port number, will save a record at the end of the hosts file but not before creating two backup copies.

```
BACKUP\hosts.fakeserver
BACKUP\hosts.20230420151207
```

In this example we find a file called **hosts.fakeserver** linked to the current session. We also find the file **hosts.20230420151207** which is also linked to the current session, but unless you decide to start the function associated with the button **4** that allows you to delete any BACKUP of the hosts file created previously, this copy will always remain preserved in such a way that the you can restore in case of problems.
The extension of this file allows you to understand when the hosts file has been backed up.
In this example the backup was performed on **20/04/2023** at **15:12:07**
Below is an image that shows the end of the hijacking by starting the function associated with the button **2**.

![screenshot-2023-04-20-15 13 12](https://github.com/user-attachments/assets/5b7e4e0a-7e10-42f6-9c42-c8fcd9344155)

Finally, if there are problems with the various changes to the hosts file, you can start the function associated with the button **3**, which allows you to manually select an old backup of the hosts file and restore the latter to a previous condition.

![screenshot-2023-04-20-15 15 13](https://github.com/user-attachments/assets/476c49b3-100a-426a-9ac3-27916822447b)

Rather than manually typing the name of the file to restore, I suggest you browse through the various backups by pressing the key **TAB** on the keyboard until the entry relating to the backup file you want to restore appears.

![screenshot-2023-04-20-15 15 20](https://github.com/user-attachments/assets/8927a58b-d460-4be0-a9a1-ad38b34aa7ff)

Following the restoration of the backup file, a binary comparison will also be performed between it and the hosts file currently running on the computer, to ensure that the restoration was performed successfully.

![screenshot-2023-04-20-15 15 27](https://github.com/user-attachments/assets/e7d9d904-9220-44e7-970c-8fb3b40cbc76)

Have you tried using FAKE SERVER?
Do you know of a similar program?
Have you managed to crack any programs using this system?
Write any BUGS or suggestions to improve FAKE SERVER and tell me your experiences in the comments.
