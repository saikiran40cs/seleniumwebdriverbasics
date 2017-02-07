# Assertions {#assertions}

---

Assertions are statements of the code that check whether the pages loading are as per the requirements. A failed assertion will lead to a failed script. testNG provides quite a many assertion methods of which we will use a few.

Verification are statements of the code that do the exact same things that assertions do, however a failed verification won’t lead to a failed script. testNG does not provide verification methods as such but we can design our own verification methods and add them to our reusable code.

In the code example below we will visit the seleniumhq.org website and assert Title of the page and assert if the selenium logo is present, also we will verify if the text “Browser Automation” is visible on the page.

```
package code;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.Assert;
import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

public class AssertionsNVerifications {

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
    public void testMethod() {
        driver.get(baseUrl + "/");

        // Assert presence of an element
        Assert.assertTrue(isElementPresent(By
                .cssSelector("img[alt=\"Selenium Logo\"]")));

        // Assert presence of page title
        Assert.assertTrue("Selenium - Web Browser Automation".equals(driver
                .getTitle()));

        // Assert absence of wrong title
        Assert.assertFalse("Selenium False Title".equals(driver.getTitle()));

        /*
         * Below we verify presence of a text.Below we are just printing out
         * true or false, based on whether text is present on the page.
         */
        WebElement header = driver.findElement(By.id("header"));
        System.out.println("Browser Automation text presence = "
                + isTextPresent(header, "Browser Automation"));
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

    private boolean isTextPresent(WebElement element, String searchText) {
        try {
            return element.getText().contains(searchText);
        } catch (NoSuchElementException e) {
            return false;
        }
    }
}
```



