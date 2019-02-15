# zabbix-freeradius

Zabbix template for Freeradius 2.x

## Items

Authentication coutners per 1 sec

* FreeRADIUS-Total-Access-Accepts
* FreeRADIUS-Total-Access-Rejects
* FreeRADIUS-Total-Access-Requests
* FreeRADIUS-Total-Auth-Dropped-Requests
* FreeRADIUS-Total-Auth-Duplicate-Requests
* FreeRADIUS-Total-Auth-Responses

Accounting coutners per 1 sec

* FreeRADIUS-Total-Accounting-Requests 
* FreeRADIUS-Total-Accounting-Responses 
* FreeRADIUS-Total-Acct-Duplicate-Requests 
* FreeRADIUS-Total-Acct-Malformed-Requests 
* FreeRADIUS-Total-Acct-Invalid-Requests
* FreeRADIUS-Total-Acct-Dropped-Requests
* FreeRADIUS-Total-Acct-Unknown-Types

Proxy authentication coutners per 1 sec

* FreeRADIUS-Total-Proxy-Access-Requests
* FreeRADIUS-Total-Proxy-Access-Accepts
* FreeRADIUS-Total-Proxy-Access-Rejects
* FreeRADIUS-Total-Proxy-Access-Challenges
* FreeRADIUS-Total-Proxy-Auth-Responses
* FreeRADIUS-Total-Proxy-Auth-Duplicate-Requests
* FreeRADIUS-Total-Proxy-Auth-Malformed-Requests
* FreeRADIUS-Total-Proxy-Auth-Invalid-Requests
* FreeRADIUS-Total-Proxy-Auth-Dropped-Requests
* FreeRADIUS-Total-Proxy-Auth-Unknown-Types

Proxy accounting coutners per 1 sec

* FreeRADIUS-Total-Proxy-Accounting-Requests
* FreeRADIUS-Total-Proxy-Accounting-Responses
* FreeRADIUS-Total-Proxy-Acct-Duplicate-Requests
* FreeRADIUS-Total-Proxy-Acct-Malformed-Requests
* FreeRADIUS-Total-Proxy-Acct-Invalid-Requests
* FreeRADIUS-Total-Proxy-Acct-Dropped-Requests
* FreeRADIUS-Total-Proxy-Acct-Unknown-Types

## Install

##### 1. Enable status server in Freeradius

Enable status server functionality you need to set the following in radiusd.conf:

<code>
status_server = yes
</code>

FreeRADIUS will only respond to status-server messages, if the status-server virtual server has been enabled. To do this, create a link from the sites-enabled directory to the status file in the sites-available directory:

```
cd sites-enabled
ln -s ../sites-available/status status
```

and restart/reload your RADIUS server. You will notice that a new server listens on port 18121/udp of localhost. If you want other clients than localhost to query this server, change the listen section of the new server. You should also change the default password in the client section of the server. Add more clients as needed.

##### 2. Add configuration userparameter_radius.conf in zabbix-agent

```
cp userparameter_radius.conf /etc/zabbix/zabbix_agentd.d/
usermod -aG radiusd zabbix
```

##### 3. Import zabbix-freeradius-template
Change macros {$RADIUS_SECRET} for password. (default adminsecret)
