
#Use phone to make calls using AgileCRM#

#####Table of Contents  
[Introduction](#Introduction)

[Setup Asterisk Widget](#ConfigureWidget)  

[Configure Asterisk Server](#ConfigureWidget)  

[Receive Calls](#ReceiveInboundCall)  

[Make Calls](#MakeOutboudCall)  

[Call Directly with Dialpad](#Dialpad)  

[View Call History](#CallHistory)  

[Analayse Call Reports](#CallReports)  

[Consolidated Dashboard Reports](#DashboardReports)  

<a name="Introduction"/>
##Introduction##
AgileCRM automatically track calls made using any hardphone using Asterisk Widget.


<a name="ConfigureWidget"/>
##Configure Widget##

Telephony Widgets can be configured in Preferences section.

<img src="https://cloud.githubusercontent.com/assets/15827609/23210237/b919a5d8-f922-11e6-9671-708f4e99c5ad.png" width="700">

##Configure Asterisk Server##

###A.Enabling Http on Asterisk###

AJAM is used to access Asterisk Manager Interface through Http.Following steps mentioned in the URL below need to be performed on server.

Check [AJAM](http://www.voip-info.org/wiki/view/Asynchronous+Javascript+Asterisk+Manager+(AJAM)) for more details.

Once http is enabled,we need to configure server for https.

In `http.conf` file,following entries to be made,

- `tlsenable=yes`
- `tlsbindaddr`=IP Address of Server with Port
- `tlscertfile`=Path of certificate file

and check [Enabling HTTPS](http://serverfault.com/questions/773217/asterisk-how-to-enable-the-https-mini-server) for more details.

###B.Inbound Setup###

Notifications from Asterisk to AgileCRM is done using CURL function.

and check [CURL](http://www.voip-info.org/wiki/view/Asterisk+func+curl) for more details.

**Inbound Call Notification** is achieved by placing following url in DialPlan of `extension.conf` using Curl function.

https://DOMAIN.agilecrm.com/call?api-key=API_KEY&number=%E&fname=%F&lname=%L&s=asterisk&exten=xxxx&e=inbound

Parameters:

1. `DOMAIN`: name of agilecrm sub-domain
2. `API_KEY`: REST API key available in API section under Admin settings.
3. `number`: Inbound number of customer
4. `fname` : first name of customer
5. `lname`: last name of customer
6. `exten`: user extension


For **Call Log after Hangup**,Following url need to be used,

https://domain.agilecrm.com/call?api-key=API_KEY&number=%E&fname=%F&lname=%L&s=asterisk&t=hangup&d=%D&e=inbound

Parameters:

1. `DOMAIN`: name of agilecrm sub-domain
2. `API_KEY`: REST API key available in API section under Admin settings.
3. `number`: Inbound number from customer
4. `fname` : first name of customer
5. `lname`: last name of customer
6. `exten`: user extension
7. `d`: duration of call

*if duration is greater than 0,Call log is displayed otherwise automatic call log is created with Failed Status

###C.Outbound Setup###

To receive **Call Log after Hangup**,Following url need to be used.

https://domain.agilecrm.com/call?api-key=API_KEY&number=%E&fname=%F&lname=%L&s=asterisk&t=hangup&d=%D&e=outbound

Parameters:

1. `DOMAIN`: name of agilecrm sub-domain
2. `API_KEY`: REST API key available in API section under Admin settings.
3. `number`: Inbound number from customer
4. `fname` : first name of customer
5. `lname`: last name of customer
6. `exten`: user extension
7. `d`: duration of call

*if duration is greater than 0,Call log is displayed otherwise automatic call log is created with Failed Status


##Asterisk Settings in AgileCRM##

Use Widget section under preferences to configure asterisk.Following section wise information need to be updated.

<img src="https://cloud.githubusercontent.com/assets/15827609/22745304/1ba7b47a-ee46-11e6-971e-5d133c3a42ba.png" width="188">


###Manager Details###
- `Username`: Context name
- `Secret`: password of Context
- `IP Address`: Server Configuration

###Inbound Settings###

- `Channel`: Enter extension for inbound

###Outbound Settings###

- `Context`: Enter context for outbound call
- `Extension` : merge field for extension
- `CallerId`: Caller id for outbound call

###Advanced Settings###

- `Variables`: Context variables
- `Priority`: Outbound call priority
- `Timeout`: Timeout duration in seconds.

##Install Chrome Extension##

Install AgileCRM Chrome Extension to make outbound calls

<a name="ReceiveInboundCall"/>
##Receive Inbound Call##

- Notification is displayed when call is received.
- Based on inbound number,contact name is displayed.

<a name="Callnotification"/>
###Inbound notification

- Inbound call can be answered or ignored.
- Notes can be captured while having call.

<img src="https://cloud.githubusercontent.com/assets/15827609/23210900/7c624084-f925-11e6-8718-7c05e6e84e33.png" width="700">

###Call log###

- Call Log is displayed after call answered and hangup.
- Call Note is automatically created for non Answered calls status like Busy,Failed,No-Answer.

<img src="https://cloud.githubusercontent.com/assets/15827609/22877786/0486f412-f1fd-11e6-934f-37f9c62b025a.png" width="700">

<a name="MakeOutboudCall"/>
##Make Outboud Call##

###Click to Call###

- Calls can be made using Phone number in Contact Info section of Contact View.
- When mouse in placed on Phone number,Configured Provider Icons are displayed.
- Click on Icon to make call.

<img src="https://cloud.githubusercontent.com/assets/15827609/22878177/bc7d2824-f1fe-11e6-815c-27a0039fea7a.png" width="700">

###Call Popup###

- Call Popup is displayed when outbound call is made.

<img src="https://cloud.githubusercontent.com/assets/15827609/22878553/4cf629b8-f200-11e6-8f6e-6d231598ab2c.png" width="700">

###Call log###

- Call log is shown when call is hangup after answering.
- Call note is created automaticaly for Non-Answered calls status like Busy,Failed,No-Answer.

<img src="https://cloud.githubusercontent.com/assets/15827609/22878690/c3ebfcaa-f200-11e6-83ea-5af502882fb0.png" width="700">

<a name="Dialpad"/>
##Dialpad##

- Calls to numbers can be made directly using Dialpad.
- Configured Telephony provider can be selected before making call.

<img src="https://cloud.githubusercontent.com/assets/15827609/22878773/0709bb80-f201-11e6-988e-ccf3a594ceb2.png" width="700">


<a name="CallHistory"/>
##Call History##


###Timeline View###

<img src="https://cloud.githubusercontent.com/assets/15827609/22880268/8d1175aa-f207-11e6-8c6b-643c4c426f14.png" width="700">

###Call Notes###

<img src="https://cloud.githubusercontent.com/assets/15827609/22880296/aaf9c28e-f207-11e6-9364-ceda092c11a3.png" width="700">

<a name="CallReports"/>
##Call Reports##

###Call by User###

<img src="https://cloud.githubusercontent.com/assets/15827609/22880380/f20beea4-f207-11e6-839d-041ac79136bf.png" width="700">

###Average Call Duration###

<img src="https://cloud.githubusercontent.com/assets/15827609/22882225/18764442-f210-11e6-9dfd-1beada58726a.png" width="700">

###Call logs###

<img src="https://cloud.githubusercontent.com/assets/15827609/22880340/cc7d8dfa-f207-11e6-81a2-c5e8c8ee5ce5.png" width="700">

###Call Outcomes###

<img src="https://cloud.githubusercontent.com/assets/15827609/22882305/6d4f774a-f210-11e6-8e2d-c2f80956d030.png" width="700">

###Call Report-Time Based###

<img src="https://cloud.githubusercontent.com/assets/15827609/22882330/8e897a32-f210-11e6-8d2f-0824380897b8.png" width="700">

<a name="DashboardReports"/>
##Dashboard Reports##

###Calls Dashlet###

<img src="https://cloud.githubusercontent.com/assets/15827609/22882469/2f7d0706-f211-11e6-9663-3ee50fc48fa7.png" width="700">
