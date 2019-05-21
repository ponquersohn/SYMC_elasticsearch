# Introduction
Everything here is made for the purpose of learning. This is still work in progress and there is absolutely no warranty that it will work. In fact it will not work almost certainly but if you are willing to give it a try then ill gladly help you.
You can contact me on lech.lachowicz@gmailthisshouldberemoved.com

~~As of now only event schema is supported. Im working on a object schema where a single document covers the whole email flow. This will allow to answer joined questions like "Top20 accept ip countries with spam verdicts"~~

The events schema is no longer supported because i've created object schma where a single document covers whole email flow. I didn't update saved objects so its up to you to make something reasonable out of the data. I'll create new visualizations as soon as possible.

# Supported event types
Almost all event types are already supported for SMG. Here is the list:
VERDICT
TD_RESULT - partially - parsing works as expected but there is huge problem with scale. ES stops responding if there are too many of events per document and here its very likely to occure. Work in progress to solve this.
UNTESTED
TRACKERID
TLS_RECEIVED
SUBJECT
SOURCE
SENDER
ORCPTS
MSG_SIZE
MSGID
LOGICAL_IP
IRCPTACTION
FIRED
DELIVERY_FAILURE
TRANS_FAILURE
DELIVER
ATTACH
VIRUS
UNSCANNABLE
SPF
DKIM
RECEIVED
RESUBMIT
PMC

I didnt add DKIM because I dont have those events yet.

CAS should work but i didn't test it yet. I'll do it as soon as i get access to fresh events. If you want to get it tested just send me events.

# Setup:
1. install ELK - tested on 7.0
2. configure rsyslog:
local1.*                                                /var/log/smg.log
:msg, contains, "Sending response"
local2.*                                                /var/log/cas.log
3. configure SMG according to "Symantec Messaging Gateway - Log Settings.png" from install_images folder.
4. configure CAS according to "Content Analysis System - *.png" from install_images folder.
5. use the files from etc_logstash to configure logstash
~~6. use kibana_saved_objects.json to import Kibana visualizations and dashboard.~~
6. Create visualizations.
Done.

Notes:
1. if you dont want to use syslog and have a bunch of log files that you want to parse you will have to adjust both patterns for smg and cas accordingly. Bare SMG and CAS logs don't have syslog fields!
~~2. keep the time synchronised! Index patterns use CAS and smg local time as Time Filter field but its still a best practice to have the time synced.~~






