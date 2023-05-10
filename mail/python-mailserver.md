# Python Aiosmtpd SMTP Server

## GET STARTED
Aiosmtpd is a Python package that provides an SMTP server implementation for asyncio, which is the asynchronous I/O framework in Python.
Aiosmtp allows to create a personal mail server providing an incoming mail handlure.

## PURPOSE
Aiosmtpd alone is not enough to implement a complete mail server that supports SMTP, IMAP, and POP3.
It only provides an implementation of the SMTP protocol for receiving incoming email messages. It does not include support for other protocols such as IMAP or POP3, which are used for retrieving and managing email messages on a server.

## COMPLETE MAIL SERVER HANDLURE

### BASIC PACKAGES
AIOSMTPD => Uses SMTP protocol for receiving incoming email messages.
IMPYLA or IMAPLIB => IMAP protocol handlure
POPLIB => POP3 protocol handlure

### ADDITIONAL COMPONENTS
Additional neccessary components to complete the mail server profile:

#### MTA (Mail Transfer Agent)
MTA is also known as mail server, is a software application that handles the transfer and delivery of email messages between different mail servers on the Internet. 
Aiosmtpd alone is not a full-fledged mail transfer agent (MTA).
Some functionality of a Mail Transfer Agent:
- Routing and forwarding of email messages between different mail servers
- Queue management and message storage
- Spam filtering and virus scanning
- Authentication and authorization of email users and domains
- Configuration and management of various server settings, such as server ports, TLS encryption, and email message size limits.

Aiosmtpd does not include many of the advanced features that are typically found in an MTA.
To use advanced features you should use a full-featured MTA like Postfix or Exim, and integrate them with your aiosmtpd implementation.

