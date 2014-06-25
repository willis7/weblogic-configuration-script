# weblogic-configuration-script

weblogic-configuration-script is a [Jython](http://www.jython.org/) set of scripts that abstract creation, management and monitor of Weblogic Server domains. It uses the [WLST - WebLogic Scripting Tool](http://docs.oracle.com/cd/E15051_01/wls/docs103/config_scripting/using_WLST.html) under the roof, creating an abstraction layer and a two-ways interface to easily integrate with tools like [jenkins](http://jenkins-ci.org/) for automation.


## Dependencies

**[Jython](http://www.jython.org/)**

**[WebLogic](http://www.python.org/)**

**[WLST](http://docs.oracle.com/cd/E15051_01/wls/docs103/config_scripting/using_WLST.html)**

**[Apache ant](http://ant.apache.org/)**


## Usage Ant

Start your project development with right foot. Proceed with **[weblogic installation](http://onlineappsdba.com/index.php/2011/12/11/how-to-install-weblogic-12c-1211-on-mac/)**, after that set everything using automated scripts, and let all your collegues with the same configuration pattern so you all can evolve it together, fixing what's needed from there.

1. Execute the managed server configuration, e.g. ```SET```, ```RESET``` and ```SAVE```, for SPECIFIC environments, e.g. ```LOCAL```, ```DEV```, ```HLG``` and ```PROD```, using scripts:

	```shell
	cd $WL_CONFIG_SCRIPT/cmds/sh/
	./createManagedServerConfig.sh LOCAL SET
	```
2. Execute the managed server classpath configuration, e.g. ```SET```, ```RESET``` and ```SAVE```, for SPECIFIC environments, e.g. ```LOCAL```, ```DEV```, ```HLG``` and ```PROD```, using scripts:

	```shell
	cd $WL_CONFIG_SCRIPT/cmds/sh/
	./createClasspathConfig.sh LOCAL SET
	```	

3. Execute the managed server Virtual Machine arguments configuration, e.g. ```SET```, ```RESET``` and ```SAVE```, for SPECIFIC environments, e.g. ```LOCAL```, ```DEV```, ```HLG``` and ```PROD```, using scripts:

	```shell
	cd $WL_CONFIG_SCRIPT/cmds/sh/
	./createVMArgsConfig.sh LOCAL SET
	```	
	
## Usage Gradle

These Gradle scripts require the ```$WEBLOGIC_CLASSPATH``` environment variable to be set. This can be achieved by running the ```. ./setWLSEnv.sh``` or ```setWLSEnv``` script found in the ```$WL_CONFIG_SCRIPT/cmds/``` directory or Weblogic install.

Gradle comes with a wrapper that will install its dependencies so no install is required for Gradle other than ensuring Java is on ```$PATH``` .

1. Execute the managed server configuration, e.g. ```SET```, ```RESET``` and ```SAVE```, for SPECIFIC environments, e.g. ```LOCAL```, ```DEV```, ```HLG``` and ```PROD```, using scripts:

	```shell
	cd $WL_CONFIG_SCRIPT/gradle/
	./gradlew.sh createManagedServerConfig -PconfigEnv=VM -PconfigAction=SET
	```
2. Execute the managed server classpath configuration, e.g. ```SET```, ```RESET``` and ```SAVE```, for SPECIFIC environments, e.g. ```LOCAL```, ```DEV```, ```HLG``` and ```PROD```, using scripts:

	```shell
	cd $WL_CONFIG_SCRIPT/gradle/
	./gradlew.sh createClasspathConfig -PconfigEnv=VM -PconfigAction=SET
	```	

3. Execute the managed server Virtual Machine arguments configuration, e.g. ```SET```, ```RESET``` and ```SAVE```, for SPECIFIC environments, e.g. ```LOCAL```, ```DEV```, ```HLG``` and ```PROD```, using scripts:

	```shell
	cd $WL_CONFIG_SCRIPT/gradle/
	./gradlew.sh createVMArgsConfig -PconfigEnv=VM -PconfigAction=SET
	```	
	
### Task properties
To configure the `WLST` task you can choose to set the following properties within the task DSL:

* `fileName` : Name and location of the WLST script file that you would like to execute. If the specified WLST script file does not exist, this task fails.
* `properties` : Name and location of a properties file that contains name-value pairs that you can reference in your WLST script. *Optional*.
* `arguments` : List of arguments to pass to the script. These arguments are accessible using the sys.argv variable. *Optional*.
* `failOnError` : Boolean value specifying whether the Ant build will fail if this task fails. *Optional*. default is true.
* `debug` : Boolean value specifying whether debug statements should be output when this task is executed.. *Optional*. default is false.

```groovy
    task myWLSTTask( type: WLST ){
        fileName "../wlst/mySuperScript.py"
        properties "../conf/${configEnv}_wlst.properties" 
        debug true
        failOnError false
    }
```

## Setup

In order to run it locally you'll need a basic server setup.

1. Install **[WebLogic](http://onlineappsdba.com/index.php/2011/12/11/how-to-install-weblogic-12c-1211-on-mac/)**;

2. Access **[WebLogic Admin Server](http://localhost:7001/console)**;

3. Log into it with an admin credentials set during the install;

4. Open the **conf/LOCAL_wlst.properties** and fill it with your expected configuration;

5. Clone the project: ```git clone https://github.com/helmedeiros/weblogic-configuration-script```

6. Define configuration folder:	```export WL_CONFIG_SCRIPT= ~/weblogic-configuration-script```


## Contributing

1. Fork it!
2. Create your feature branch: ```git checkout -b my-new-feature```
3. Commit your changes: ```git commit -m 'Add some feature'```
4. Push to the branch: ```git push origin my-new-feature```
5. Submit a pull request :D


## License

[MIT License](http://opensource.org/licenses/MIT)
