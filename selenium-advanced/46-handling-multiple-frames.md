# Handling frames {#handling-multiple-windows}

Below is the code snippet to interact with frames using selenium webdriver.

```
@Test
    public void testMethod() {

        WebDriver driver = new FirefoxDriver();
        // URLs to be verified..
        String expectedresult[] = { "Google","W3Schools Online Web Tutorials","Sparsh", "Delicious" };

        int count = 0;
        // We are fetching all the values in dropdown below and clicking one by one
        driver.findElement(By.xpath("/someXpath/to/dropdownLinks")).click();

        // Here we switch to newly opened frame
        driver.switchTo().frame("frameName");

        //Perform actions in this frame
        System.out.println(driver.getTitle());    

        // Switch back to the window
        driver.switchTo().defaultContent();
    }
```

Also remember you cannot switch between multiple frames.If in case there are three cascaded level of frames then you have to first switch back to default content and then switch to the next frame otherwise you may get NoSuchElementException.

