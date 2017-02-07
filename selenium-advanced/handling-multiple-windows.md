# Handling multiple windows {#handling-multiple-windows}

Below is the code snippet to interact with multiple windows using selenium webdriver.

```
@Test
    public void testMethod() {

        WebDriver driver = new FirefoxDriver();
        String newwindowtitle = null;
        // URLs to be verified..
        String expectedresult[] = { "W3Schools Online Web Tutorials", "Google",
                "W3Schools Online Web Tutorials",
                "Sparsh – The Infosys Intranet", "Delicious" };

        int count = 0;
        // We are fetching all the values in dropdown below and clicking one by
        // one
        List<WebElement> elements = driver.findElements(By.xpath("/someXpath/to/dropdownLinks"));
        Iterator<WebElement> it = elements.iterator();
        while (it.hasNext()) {
            // Get the title of current window..
            String parentWindowHandle = driver.getWindowHandle();
            System.out.println(parentWindowHandle);
            // Now we are clicking the next link available in dropdown
            WebElement dropdownlinks = it.next();
            if (dropdownlinks.isDisplayed()) {
                dropdownlinks.click();
            }

            // Here we switch to newly opened window and check if it is correct
            // window
            Set<String> s = driver.getWindowHandles();
            System.out.println(s.size());
            Iterator<String> ite = s.iterator();
            while (ite.hasNext()) {
                String popuphandle = ite.next().toString();
                if (!popuphandle.equals(parentWindowHandle)) {
                    driver.switchTo().window(popuphandle);
                    newwindowtitle = driver.getTitle();
                    System.out.println(newwindowtitle);
                    Assert.assertEquals(newwindowtitle, expectedresult[count]);
                    count++;
                    // Close the new window.
                    driver.close();
                }
            }
            // Switch back to the window from where we arrived at new window
            driver.switchTo().window(parentWindowHandle);
        }
    }
```



