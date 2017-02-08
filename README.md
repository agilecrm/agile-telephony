# **Asterisk WebRTC with AgileCRM**

This article aims at setting up of Asterisk WebRTC widget in AgileCRM.

**Prerequisites**

Asterisk must be installed and running successfully.

##Step1: Configure Asterisk Server##

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


##Step2: Asterisk Settings in AgileCRM##

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

##Step3: Install Chrome Extension##

Install Chrome Extension to make outbound calls

#Managing Calls#

##Inbound Call##
	
- Ringing: 

Call noty is displayed when inbound call started ringing.

<img src="https://cloud.githubusercontent.com/assets/15827609/22747244/8f90d2a8-ee4c-11e6-8dc1-24dd6e65f4dc.png" width="150">

- Hangup: 

Call log is displayed when call is hangup.

<img src="https://cloud.githubusercontent.com/assets/15827609/22747330/cc8b697a-ee4c-11e6-86e5-c224b2df8a41.png" width="150">

##Outboud Call##

- **Click to Call**

In contact view,Click on Asterisk icon against phone number for click to call.

<img src="https://cloud.githubusercontent.com/assets/15827609/22746110/ce8e6fa0-ee48-11e6-9349-6a20f33ea2c9.png" width="150">

- **Ringing** : Call noty is displayed when outbound call is made.

<img src="https://cloud.githubusercontent.com/assets/15827609/22746316/605b1eba-ee49-11e6-89ba-7a1c7ca0128d.png" width="150">

- **Hangup**: Call log is displayed when call is hangup.

<img src="https://cloud.githubusercontent.com/assets/15827609/22746500/e583c344-ee49-11e6-8f54-e086a13a91f3.png" width="150">

##Call History##

###Timeline###

###Call Notes###

##Call Reports##

###Call by User###
###Average Call Duration###
###Call logs###
###Call Outcomes###
###Call Report-Time Based###
###User Activties###

