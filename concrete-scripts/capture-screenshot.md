# Capture screenshot {#capture-screenshot}

In order to capture screenshot, copy the below method to your common functions Class. The method create a folder named screenShots in your project root folder and saves the screenShot in .png format. The capture method can be called at any line of code by provide driver object and screenshot name as arguments.

```
public void capture(WebDriver driver, String ImageName) {
        File screenshot = null;

        screenshot = ((TakesScreenshot) driver)
                .getScreenshotAs(OutputType.FILE);

        try {
            FileUtils.copyFile(screenshot, new File("screenShots/" + ImageName
                    + ".png"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```



