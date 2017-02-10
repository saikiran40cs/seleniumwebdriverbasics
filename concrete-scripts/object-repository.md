# Object Repository {#object-repository}

We use object repository to store all our page controls in a common class, this way whenever there are changes in the UI, the respective changes can be updated in the Object Repository, without having to go to the actual code. A person with lesser knowledge of java platform can also easily do this.

Below is the script without object Repository. We will prepare an OR \(Object Repository\) for the same script.

```
package com.selenium;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.Assert;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class WithoutOR {

    private WebDriver driver;
    private String baseUrl;

    @BeforeTest
    public void initialization() {
        driver = new FirefoxDriver();
        baseUrl = "http://docs.seleniumhq.org/";
        driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
        driver.manage().window().maximize();
    }

    @Test
    public void testMethod() throws InterruptedException {
        driver.get(baseUrl + "/");
        driver.findElement(By.linkText("Projects")).click();
        driver.findElement(By.linkText("nsaikiran")).click();
        Assert.assertTrue(isElementPresent(By.name("submit")));
    }

    @AfterTest
    public void cleanup() {
        driver.quit();
    }

    private boolean isElementPresent(By by) {
        try {
            driver.findElement(by);
            return true;
        } catch (NoSuchElementException e) {
            return false;
        }
    }
}
```

Create A class named ObjectRepo as below.

```
package com.selenium;

public interface ObjectRepo {
    public String linkProejct = "Projects";
    public String linkDownload = "nsaikiran";
    public String donateBtn = "submit";

}
```

Update the script as below. The script is now totally free of any hardcoding. Whatever changes happen in the UI can be udpated in the object Repository.

```
package com.selenium;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.Assert;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class WithoutOR implements ObjectRepo{

    private WebDriver driver;
    private String baseUrl;

    @BeforeTest
    public void initialization() {
        driver = new FirefoxDriver();
        baseUrl = "http://docs.seleniumhq.org/";
        driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
        driver.manage().window().maximize();
    }

    @Test
    public void testMethod() throws InterruptedException {
        driver.get(baseUrl + "/");
        // All the elements are fetched from Object Repository
        driver.findElement(By.linkText(linkProejct)).click();
        driver.findElement(By.linkText(linkDownload)).click();
        Assert.assertTrue(isElementPresent(By.name(donateBtn)));
    }

    @AfterTest
    public void cleanup() {
        driver.quit();
    }

    private boolean isElementPresent(By by) {
        try {
            driver.findElement(by);
            return true;
        } catch (NoSuchElementException e) {
            return false;
        }
    }
}
```



