# ANT Basics {#ant-basics}

Apache ANT – “Another Neat Tool” is a build tool provided by Apache Foundation. The tool is used to compile java source code, package and deploy. The tool can be downloaded from Apache ANT link. Once the ANT zip file is downloaded, extract the zip to a folder. The path can be something link C:ANT. Once the contents are extracted we need to set classpath variables. Follow the below steps carefully, to get this done.

Step 1. Prior to ANT installation, when you type ant in the command prompt you will get message as shown in below picture.

Step 2. Get the folder locations for ANT and jdk. On my machine I have below paths. Apache Installation –&gt; C:apache-ant-1.8.4 jdk Installation –&gt; C:Program FilesJavajdk1.7.0\_02

Step 3. update the below text as per your above paths. JAVA\_HOME : C:Program FilesJavajdk1.7.0\_02 ANT\_HOME : C:apache-ant-1.8.4

Step 4. Open your environment variables window \(Right click Computer &gt; properties &gt;Advance System Settings &gt; Click Environment Variable\)

Step 5. Under SystemVariables click New, fill in the details as shown in below picture and click OK.

![](https://ajaymore.gitbooks.io/selenium/content/continuous_integration/img/set-java-home.jpg "Setting PATH")

Step 6. Under System Variables click New again and create ANT\_HOME providing correct variable value.

Step 7. Search for a variable named “PATH” under System variables list. Select this variable and click Edit. append the below line to the existing content. Remove the first semicolon from the below text if there is already a semicolon at the end of the opened text and click OK.

;%JAVA\_HOME%bin;%ANT\_HOME%bin;

Step 8. Close the command prompt if previously open. Open again ant type ant. Now you should be able to view the below message which implies that the ANT is working properly.

Once ANT is installed and working, you can refer the tutorial

[Tutorial: Hello World with Apache Ant](http://ant.apache.org/manual/tutorial-HelloWorldWithAnt.html). to get and idea about ANT scripting.

