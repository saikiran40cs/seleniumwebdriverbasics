# JavascriptExecutor {#javascriptexecutor}

It’s possible to execute your custom JavaScript on a webpage. The code below helps in scrolling the page.

```
@Test
    public void pageScroll() {
        driver.get("http://someURl.com");

        // invoke javascript executor
        JavascriptExecutor executor = (JavascriptExecutor) driver;
        executor.executeScript("window.scrollBy(0,500);scrolldelay = setTimeout('pageScroll()',50);");
    }
```



