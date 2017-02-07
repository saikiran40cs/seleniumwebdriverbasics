# Webdriver locators {#webdriver-locators}

Webdriver reads the html source code to locate the elements we need to interact with while automating. A typical HTML source code consists of several tags \(div, h1, form, span etc.\), the tags have several attributes \(class, id, name, type etc.\). Webdriver makes use of this tag-attribute structure to find the desired elements and perform actions on them. HTML code looks as below.

```
<div class="wrapper">
<h2>Sample Form</h2>
<form action="#">
<input name="text" type="text" placeholder="Enter name" />
<input name="password" type="password" placeholder="Enter password" />
<button id="submitBtn">Submit</button>
</form>
</div>
```

We can locate elements in following ways

```
driver.findElement(By.id("submitBtn"));
driver.findElement(By.name("username"));
driver.findElement(By.linkText("Link to google"));
driver.findElement(By.className("form"));
driver.findElement(By.cssSelector(".form input"));
driver.findElement(By.xpath("//input[@name='password']"));

```

Follow the below sequence while choosing the method of choosing element. Choose the one that appears higher in the sequence. Choose xpath only if there is a lot of decision making to be done for complex user interface.

1. id
2. name
3. class
4. linkText \(if link\)
5. cssSelector
6. xpath

Create a new package called code and add a class named SampleScript in it. Copy the below code into editor. Run the script and verify it works.

```
package code;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class SampleScript {

    WebDriver driver;
    String baseUrl = "http://ajaymore.net/selenium/demo";

    @BeforeTest
    public void initialize() {
        driver = new FirefoxDriver();
        driver.get(baseUrl);
        driver.manage().window().maximize();
    }

    @Test
    public void testLocators() throws InterruptedException {
        WebElement submitButton = driver.findElement(By.id("submitBtn"));
        driver.findElement(By.name("username")).sendKeys("johnDoe");
        driver.findElement(By.cssSelector(".form .pswd")).sendKeys("ABC@xyz");
        submitButton.click();
        Thread.sleep(3000);
        driver.findElement(By.linkText("Link to google")).click();
        Thread.sleep(3000);
    }

    @AfterTest
    public void tearDown() {
        driver.quit();
    }

}
```



