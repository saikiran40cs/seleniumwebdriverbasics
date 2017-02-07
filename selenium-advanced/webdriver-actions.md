# Webdriver actions {#webdriver-actions}

Various webpage actions like mouseHover, sliding element etc. can be performed using Webdriver.

Mouse Hover first approach

```
@Test
    public void webDriverActions() {
        driver.get("http://someURl.com");
        // Get element to be hovered upon
        WebElement hoverElement = driver.findElement(By
                .xpath("//div[@class='hoverElement']"));

        // Perform hover action
        Actions builder = new Actions(driver);
        builder.moveToElement(hoverElement).build().perform();

        // Click the element that is now visible after hover
        driver.findElement(By.xpath("//div[@class='visibleElementOnHover']"))
                .click();
    }

```

Mouse Hover second approach

```
@Test
    public void webDriverMouseActions() {
        driver.get("http://someURl.com");
        // Get element to be hovered upon
        WebElement hoverElement = driver.findElement(By
                .xpath("//div[@class='hoverElement']"));

        // Perform hover action using Mouse object
        Locatable hoverItem = (Locatable) hoverElement;
        Mouse mouse = ((HasInputDevices) driver).getMouse();
        mouse.mouseMove(hoverItem.getCoordinates());

        // Click the element that is now visible after hover
        driver.findElement(By.xpath("//div[@class='visibleElementOnHover']"))
                .click();
    }

```

Move Slider to an offset

```
@Test
    public void dragSlider() {
        driver.get("http://someURl.com");
        // Get sliding element
        WebElement sliderElement = driver.findElement(By.id("sliderId"));
        // drag the slider
        Actions builder = new Actions(driver);
        builder = new Actions(driver);
        // Move 120px on x axis
        Action dragAndDrop = builder.clickAndHold(sliderElement)
                .moveByOffset(120, 0).release().build();
        dragAndDrop.perform();
    }
```



