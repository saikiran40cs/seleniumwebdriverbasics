# Using property files {#using-property-files}

For faster access and quick modifications we can store some of our configuration settings in property files. Below you will find the code to access information stored in property files.

Create a property file named Configuration.properties in the folder propertyFiles. and paste the below configuration in file.

applicationTimeout = 30 browser = Firefox

Now create a Class with name “ReadPropertyFile” and copy paste the below code in same. The class contains code to read properties like timeout and browser.

```
package com.selenium;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Properties;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;

public class ReadPropertyFile {
    String browser;
    int timeOut;

    @BeforeTest
    public void initialization() {
        // Below is the code to read property file "Configuration.properties"
        // place in folder propertyFiles
        Properties readProp = new Properties();
        readProp = loadPropertyFile("Configuration.properties");
        browser = readProp.getProperty("browser");
        timeOut = Integer.parseInt(readProp.getProperty("applicationTimeout"));
    }

    @Test
    public void testMethod() {
        System.out.println("Browser is : " + browser);
        System.out.println("Timeout is : " + timeOut);
    }

    public Properties loadPropertyFile(String propFileName) {

        Properties props = new Properties();
        FileInputStream fis;
        try {
            fis = new FileInputStream(System.getProperty("user.dir")+ "propertyFiles" + propFileName);
            props.load(fis);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return props;
    }
}
```



