# Setting up browsers {#setting-up-browsers}

Selenium supports many browsers, here we provide you with the code to run a few. It is assumed that you have all the necessary jars and tools. Please refer [**Eclipse Project Setup**](https://nsaikiran.gitbooks.io/seleniumautomation/content/1.4-eclipse-project-setup.html)** **for information on how to setup eclipse project.

**1. Firefox**

```
package com.selenium;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

public class BrowserSetup {

    WebDriver driver = null;
    String baseUrl = null;

    @BeforeTest
    public void initialization() {
        // Create Firfox browser Instance..
        driver = new FirefoxDriver();
        // Define URL to be opened..
        baseUrl = "http://www.google.co.in/";
        // Define timeout, selenium will wait maximum of 30 seconds before
        // it quits while searching for an element..
        driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
        driver.manage().deleteAllCookies(); // Delete cookies
        driver.manage().window().maximize(); // Maximize window
    }

    @Test
    public void testMethod() {
        // Open the URL in browser..
        driver.get(baseUrl);
    }

    @AfterTest
    public void cleanup() {
        // Close the browser..
        driver.quit();
    }

}
```

**2. InternetExplorer \(Assuming you have IEDriverServer in your tools directory\)**

Before Running Internet Explorer from your script please ensure that all the security settings \(Tools &gt; Internet Options &gt; Security\) are either checked or unchecked.

```
package com.selenium;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.ie.InternetExplorerDriver;
import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

public class SetupIE {

    WebDriver driver = null;
    String baseUrl = null;

    @BeforeTest
    public void initialization() {
        baseUrl = "http://www.google.co.in/";
        // The path is defined considering you have IEDriverServer_32Bit.exe
        // copied to the path "toolsIE" in your project root directory
        String path = System.getProperty("user.dir")+ "toolsIEIEDriverServer_32Bit.exe";
        System.setProperty("webdriver.ie.driver", path);
        driver = new InternetExplorerDriver();
        driver.manage().timeouts().implicitlyWait(50, TimeUnit.SECONDS);
        driver.manage().deleteAllCookies();
        driver.manage().window().maximize();
    }

    @Test
    public void testMethod() {
        // Open the URL in browser..
        driver.get(baseUrl);
    }

    @AfterTest
    public void cleanup() {
        // Close the browser..
        driver.quit();
    }

}
```

**3. Google Chrome \(We assume you have chromedriver in your tools directory\)**

```
package com.selenium;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

public class SetupChrome {

    WebDriver driver = null;
    String baseUrl = null;

    @BeforeTest
    public void initialization() {
        baseUrl = "http://www.google.co.in/";
        // The path is defined considering you have chromedriver.exe
        // copied to the path "toolschrome" in your project root directory
        String path = System.getProperty("user.dir") + "tools/chromechromedriver.exe";
        System.setProperty("webdriver.chrome.driver", path);
        driver = new ChromeDriver();
        driver.manage().timeouts().implicitlyWait(50, TimeUnit.SECONDS);
        driver.manage().deleteAllCookies();
    }

    @Test
    public void testMethod() {
        // Open the URL in browser..
        driver.get(baseUrl);
    }

    @AfterTest
    public void cleanup() {
        // Close the browser..
        driver.quit();
    }

}
```



