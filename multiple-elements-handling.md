# Multiple Elements {#multiple-elements}

---

When we have multiple elements to work with, and wish to use few of them based on business requirement, then we need a logical loop to take those decisions. In this demo we will be demonstrating how we can make a choice based action.

Below is the snapshot of seleniumhq.org website. Using firebug and firepath I have calculated a xpath : “.//\*\[@id='header'\]//li/a” which highlights all the seleniumhq links on the header. We use this xpath to fetch all these links in our code and then click the link that matches the link text of our choice. In this demo it will be “Documentation”. More on xpath in our tutorial Robust Xpath.

![](https://ajaymore.gitbooks.io/selenium/content/selenium_beginner/img/multiple-elements.jpg "Xpath")

In the code below we are using cssSelector instead of xpath, to use xpath uncomment the xpath code and comment cssSelector code block.

```
package code;

import java.util.List;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class MultipleElements {

    private WebDriver driver;
    private String baseUrl;

    @BeforeTest
    public void initialization() {
        driver = new FirefoxDriver();
        baseUrl = "http://seleniumhq.org/";
        driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
        driver.manage().window().maximize();
    }

    @Test
    public void testMethod() throws InterruptedException {
        // Open seleniumhq.org website..
        driver.get(baseUrl);

        // Print title of the page..
        System.out.println("Title : " + driver.getTitle());

        // Locate all the Menulinks present in header..
        List<WebElement> menuLinks = driver.findElements(By.cssSelector("#header ul a"));

        /* Elements can also be selected by xpath */
        /* List<WebElement> menuLinks = driver.findElements(By.xpath(".//*[@id='header']//li/a"));       */

        // Print the number of links present..
        System.out.println(menuLinks.size());

        /*
         * Iterate over the list and click the link that matches text
         * Documentation
         */
        for (WebElement option : menuLinks) {
            String linkName = option.getText();
            if (linkName.equals("Documentation")) {
                option.click();
                break; // Exit from the loop, this is important
            }
        }
        Thread.sleep(3000);
    }

    @AfterTest
    public void cleanup() {
        driver.quit();
    }

}
```



