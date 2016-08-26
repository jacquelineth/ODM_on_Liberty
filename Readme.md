# Liberty configurations for ODM


 ## This project intent to provide various configuration (branches), in a ready to boot set-up.
 
  The main idea is to not have to deploy/copy any WARS, but use ODM_HOME to retrieve required WARS at startup. 

### Install

- Download Liberty , from [WASdev](https://developer.ibm.com/wasdev/getstarted/)
  - Unzip in a folder that would be the new WLP_USER_DIR
  - ~~create the instance with~~ ~~`bin\server.bat create odm`~~, you may use this zipped repo or checkout/clone git under usr/ folder.
  - Edit servers/odm/server.env to adjust  `JAVA_HOME` , `ODM_HOME` .


### Liberty features and add-ons
 Some optional features are installed to ease deployment and use :
 - ~~adminCenter~~ ref to [Admin Center in WASdev](https://developer.ibm.com/wasdev/downloads/#asset/features-com.ibm.websphere.appserver.adminCenter-1.0) 
 - ~~LDAP~~ ref to [LDAP in WASdev](https://developer.ibm.com/wasdev/downloads/#asset/features-com.ibm.websphere.appserver.ldapRegistry-3.0)

### Start & stop
- Start with `server.bat run odm`
- Stop with `server.bat stop odm`
- [Dump](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_setup_dump_server.html) on running instance with `server dump odm --include=thread,heap,system` 
  - for JVM part `server javadump odm --include=heap,system`


### TCP/IP Mode

Two approaches, zeroconf or permanent. Although created for ODM88 branch, just changing `ODM_HOME` is sufficient.
#### zeroconf
 >  By default servers/odm/server.xml, will overwrite the `management.protocol` to **tcpip**
#### Permanent

>   A new folder ***tcpIP*** provides a batch file (**configTcpip.bat**) to generate the new res.war file which will be deployed in *webapps88*. Set the ODM Home, and modify the default tcip property if required
>   Then in your DecisionService or any XU you must update the ra.xml's plugin definition with 

    {pluginClass=Management,xuName=default,protocol=tcpip,tcpip.port=1883,tcpip.host=localhost,tcpip.retryInterval=2000}

### LDAP 

LDAP support is added to Liberty through a [feature](https://developer.ibm.com/wasdev/downloads/#asset/features-com.ibm.websphere.appserver.ldapRegistry-3.0)


The configured DB is embedded Derby stored in /data, other JDBC jars should be added in /lib.
There is also a setup to use Derby Network server with startDeby.bat/stopDerby.bat, adjust the datasource definition accordingly.


To know more on ODM : [ODM site](http://www-03.ibm.com/software/products/en/category/operational-decision-management)
To know more on Liberty :[infocenter ](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty)