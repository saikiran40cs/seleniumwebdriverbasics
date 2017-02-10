# ANT Build.xml {#ant-buildxml}

We assume in this tutorial that you have ANT installed on your system. Follow the tutorial ANT Basics to know about how to get it installed. Before running the selenium testSuite via ANT, Download zip file from this location [Downloads – testng-xslt – TestNG XSL Reports – Google Project Hosting](http://code.google.com/p/testng-xslt/downloads/list). Extract the below files from this zip. saxon-8.7.jar SaxonLiaison.jar testng-results.xsl

Create a suite file with name suite.xml in the root directory of your project.

Copy the two jar files to lib folder and add them to build path. copy the testng-results.xsl to the root folder of your project. Once these files are in place create a new file with name Build.xml at the root directory of your project. Copy paste the contents below to this Build.xml

The build can be run through by right click on Build.xml &gt; Run As &gt; Ant Build. Or alternately using command prompt with command line : ant -buildfile **physical Path of Build.xml**

```
<project name="ANT_with_TestNGXslt" default="run" basedir=".">

    <property name="classes.dir" value="bin" />
    <property name="src.dir" value="src" />
    <property name="log4j.dir" value="log4j" />
    <property name="suite.dir" value="TestSuite" />
    <property name="report.dir" value="test-output" />
    <property name="lib.dir" value="Libraries" />

    <path id="build.class.path">
        <pathelement location="${log4j.dir}" />
        <pathelement location="${classes.dir}" />
        <!- You can call either this way if you are sure of the jar files
        <pathelement location="${lib.dir}/testng-6.8.jar" />
        <pathelement location="${lib.dir}/selenium-server-standalone-2.25.0.jar" />
        <pathelement location="${lib.dir}/saxon-8.7.jar" />
        <pathelement location="${lib.dir}/SaxonLiaison.jar" />
        <pathelement location="${lib.dir}/log4j-1.2.17.jar" />
        <pathelement location="${lib.dir}/selenium-java-2.25.0.jar" />
        <pathelement location="${lib.dir}/poi/dom4j-1.6.1.jar" />
        <pathelement location="${lib.dir}/poi/poi-3.9-20121203.jar" />
        <pathelement location="${lib.dir}/poi/poi-ooxml-3.9-20121203.jar" />
        <pathelement location="${lib.dir}/poi/poi-ooxml-schemas-3.9-20121203.jar" />
        <pathelement location="${lib.dir}/poi/stax-api-1.0.1.jar" />
        <pathelement location="${lib.dir}/poi/xmlbeans-2.3.0.jar" /> -->

    </path>

    <target name="run">
        <!--<antcall target="startSeleniumServer" />-->
        <antcall target="clean" />
        <antcall target="compile" />
        <antcall target="runTests" />
        <!--<antcall target="stopSeleniumServer" />-->
    </target>

    <!-- Start the server -->
    <target name="startSeleniumServer">
        <echo>Starting Selenium Server...</echo>
        <java jar="${lib.dir}selenium-server-standalone-2.25.0.jar" fork="true" spawn="true">
            <arg line="-singlewindow -log ${logs.dir}selenium_server_log.txt" />
        </java>
    </target>

    <!-- Delete old data and create new directories -->
    <target name="clean">
        <echo>Initlizing...</echo>
        <delete dir="${classes.dir}" />
        <mkdir dir="${classes.dir}" />
        <delete dir="${report.dir}" />
        <mkdir dir="${report.dir}" />
    </target>

    <!-- Compiles the java files -->
    <target name="compile">
        <echo>Compiling...</echo>
        <javac debug="true" srcdir="${src.dir}" destdir="${classes.dir}" classpathref="build.class.path" includeantruntime="false" includes="**/**" />
        <javac debug="true" srcdir="${suite.dir}" destdir="${classes.dir}" classpathref="build.class.path" includeantruntime="false" includes="**/**" />
        <copy todir="${classes.dir}">
            <fileset dir="${src.dir}" excludes="**/*.java" />
        </copy>
    </target>

    <!-- Runs the file and generate report -->
    <target name="runTests" description="Running tests">
        <echo>Running Tests...</echo>
        <taskdef name="testng" classname="org.testng.TestNGAntTask" classpathref="build.class.path" />
        <testng outputdir="${report.dir}" classpathref="build.class.path" workingdir="${basedir}">
            <xmlfileset dir="${basedir}" includes="suite.xml" />
        </testng>
    </target>

    <!-- Stop the selenium Server -->
    <target name="stopSeleniumServer">
        <echo> Trying to stop selenium server ... </echo>
        <get taskname="selenium-shutdown" src="http://localhost:4444/selenium-server/driver/?cmd=shutDownSeleniumServer" dest="${logs.dir}selenium_server_shutdown_result.txt" ignoreerrors="true" />
        <echo taskname="selenium-shutdown" message="Shutdown complete.." />
    </target>

</project>
```

When the suite is run this way, at the end of your execution you should have two test output folders namely – test-output and testng-xslt.

