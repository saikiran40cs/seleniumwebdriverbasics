# PROXIES, PROFILES, CERTIFICATES {#proxies-profiles-certificates}

---

This tutorial will teach how to create a firefox profile. In order to use various add-ons installed on your native browser, we will be required to create a custom profile. Follow the below steps to create a profile.

1. Create a folder with name “tools” at the root of your project. Now create a folder with name “firefox” in the same folder.

2. Open the mozilla Installation path in your computer – In my case it’s “C:Program FilesMozilla Firefox”. Copy the entire contents of this folder into the folder created at step 1. – The firefox folder under tools folder.

3. Create a folder with name “DefaultProfile” in the firefox folder. This folder already has the contents you copied from your mozilla installation directory.

4. Now go to firefox profile directory on your machine. In my case it’s “C:UsersmysticAppDataRoamingMozillaFirefoxProfileswp8ks7au.default”. – copy the contents of this folder to the DefaultProfile folder created in step 3.

Now there are two ways of setting proxy, either we set the proxy using ip and port number. or we set by the URL. The code snippet shows how to achieve the same using both the methods. The code snippet for setting proxy via URL is commented. Uncomment this code if you wish to use it and comment the other part.

Finally the code to accept security certificates is also mentioned in the snippet.

```
package code;

import java.io.File;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Proxy;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxBinary;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.firefox.FirefoxProfile;
import org.openqa.selenium.remote.CapabilityType;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class ProxiesCertificates {
    WebDriver driver;
    String baseUrl;

    @BeforeTest
    public void setup() {

        // The below proxy is a string that contains proxy ip and port
        // The port and ip is separated by ":" below you can see port is 80
        Proxy proxy = new Proxy();
        String proxyIp = "10.76.122.32:80";

        // Below lines sets the proxy defiend above
        proxy.setHttpProxy(proxyIp);
        proxy.setSslProxy(proxyIp);
        proxy.setFtpProxy(proxyIp);

        // In case you wish to set proxy with URL uncomment below code. and
        // comment the above 3 lines

        /*
         * proxy.setProxyType(Proxy.ProxyType.PAC);
         * proxy.setProxyAutoconfigUrl("http://someServer/server.pac");
         */

        // Below code create capability with mentioned proxy
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability(CapabilityType.PROXY, proxy);

        // Path to the copy of firefox installation. Here you can provide direct
        // path to your firefox installation also.
        System.setProperty("webdriver.firefox.bin",
                System.getProperty("user.dir")
                        + "toolsfirefoxfirefox.exe");

        // This is the path to the firefox profile you copied in your project.
        FirefoxProfile fp = new FirefoxProfile(new File(
                System.getProperty("user.dir")
                        + "toolsfirefoxDefaultProfile"));

        // Below code accepts security certificates..
        fp.setPreference("setAcceptUntrustedCertificates", "true");
        fp.setAcceptUntrustedCertificates(true);
        fp.setAssumeUntrustedCertificateIssuer(true);

        // Create browser instance with above mentioned requsites
        driver = new FirefoxDriver(new FirefoxBinary(), fp, capabilities);
        driver.manage().timeouts().implicitlyWait(50, TimeUnit.SECONDS);
        driver.manage().deleteAllCookies();
        driver.manage().window().maximize();
    }

    @Test
    public void testMethod() {
        baseUrl = "http://docs.seleniumhq.org/";
        driver.get(baseUrl);
    }

    @AfterTest
    public void teardown() {
        driver.quit();
    }

}
```



