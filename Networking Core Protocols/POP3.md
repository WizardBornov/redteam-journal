 The Post Office Protocol version 3 (POP3) is designed to allow the client to communicate with a mail server and retrieve email messages.

Without going into in-depth technical details, an email client sends its messages by relying on SMTP and retrieves them using POP3. SMTP is similar to handing your envelope or package to the post office, and POP3 is similar to checking your local mailbox for new letters or packages.

Some common POP3 commands are:

- `USER <username>` identifies the user
- `PASS <password>` provides the user’s password
- `STAT` requests the number of messages and total size
- `LIST` lists all messages and their sizes
- `RETR <message_number>` retrieves the specified message
- `DELE <message_number>` marks a message for deletion
- `QUIT` ends the POP3 session applying changes, such as deletions

In the terminal below, we can see a POP3 session over telnet. Since the POP3 server listens on TCP port 110 by default, the command to connect to the TELNET port is `telnet MACHINE_IP 110`.  Connecting to a POP3 server requires authentication.

```
user@TryHackMe$ telnet MACHINE_IP 110 
Trying MACHINE_IP... 
Connected to MACHINE_IP. 
Escape character is '^]'. 
+OK [XCLIENT] Dovecot (Ubuntu) ready. 
AUTH 
+OK 
PLAIN 
. 
USER strategos 
+OK 
PASS 
+OK Logged in. 
STAT +OK 3 1264 
LIST +OK 3 messages: 
1 407 
2 412 
3 445 . 
RETR 3 
+OK 445 octets 
Return-path: <user@client.thm> 
Envelope-to: strategos@server.thm 
Delivery-date: Thu, 27 Jun 2024 16:19:35 +0000 
Received: from [10.11.81.126] (helo=client.thm) 
		by example.thm with smtp (Exim 4.95) 
		(envelope-from <user@client.thm>) 
		id 1sMrpq-0001Ah-UT 
		for strategos@server.thm; 
		Thu, 27 Jun 2024 16:19:35 +0000 
From: user@client.thm 
To: strategos@server.thm 
Subject: Telnet email 
Hello. I am using telnet to send you an email! 
. 
QUIT 
+OK Logging out. 
Connection closed by foreign host.
```