# Presence of iframe {#presence-of-iframe}

---

If the html source contains an iframe tag then the usual way of locating elements does not work. We get the below exception in such cases.

```
org.openqa.selenium.NoSuchElementException: The element could not be found
(WARNING: The server did not provide any stacktrace information)

```

To tackle the issue use the below line of code, before searching for an element in iframe.

```
driver.switchTo().frame(driver.findElement(By.id("frameID")));
```

You must get the iframe name using the firebug tool as it is much easy to notice.

