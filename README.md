This is the home of the Alfresco Hyperic Plugin. The plugin is unsupported by Alfresco. The last known version of Alfresco that this was known to work on was Alfresco 3.4

# Installing the Alfresco Enterprise Plugin for Hyperic

* Ensure that the OS user running the Hyperic Agent and the OS user running Alfresco have permissions to read and write each other's files. E.g. both running as root, or both in the same group with a umask of 2. This is because local JMX communication relies on file handles.
* To enable auto-discovery of Alfresco by Hyperic, ensure that your alfresco startup script includes the following arguments to the application server JVM:
```
-Dalfresco.home=<root Alfresco install directory>
-Dcom.sun.management.jmxremote 
```

For example, in a Tomcat installation
```
  export JAVA_OPTS="${JAVA_OPTS} -Dalfresco.home=${ALF_HOME} -Dcom.sun.management.jmxremote"
```
* Copy alfresco-enterprise-plugin.xml to the hq-plugins directory of your Hyperic installation (or refer to Hyperic documentation on how to install a plugin)
* Restart the hyperic agent
```
/etc/init.d/hyperic-hq-agent restart 
```
* Restart the alfresco server
* Schedule an auto-discovery in Hyperic (refer to Hyperic documentation). You should see that an "Alfresco Enterprise Server" is discovered, along with an array of services.
* To enable log tracking, go to the "Resources" tab, navigate to the Alfresco Server and its "Inventory Tab" and select "Edit" under "Configuration Properties". Then set server.log_track.enable to true and set server.log_track.level if required. Log entries will then be indicated by a blue light at the bottom of the Monitor tab.
