# TestSuite Parameterization {#testsuite-parameterization}

This tutorial assumes you know how to create a TestSuite. Please visit the post[Preparing TestSuite](http://ajaymore.gitbooks.io/selenium/content/test_frameworks/testsuite.html)to learn about TestSuite. The below Suite xml file passes the parameter “browser” with value “IE” to the script it’s calling.

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<suite name="Test_Suite" verbose="-1" parallel="tests"    thread-count="1">
<test name="Parameter_Pass-IE" preserve-order="True">
<parameter name="browser" value="IE" />
<classes>
<class name="testng.Parameter_Pass">
<methods>
<include name="testParameterPass" />
</methods>
</class>
</classes>
</test>
</suite>
```

The below Script accepts parameter browser from the Suite, it uses the value if it’s provided from the suite, else it sets to default value when it’s not set by Suite. Ideally when we run standalone script the default value will be used.

```
package testng;

import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Optional;
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class Parameter_Pass {

    @Parameters({ "browser" })
    @BeforeTest
    public void setup(@Optional("Firefox") String browser) {
        System.out.println("Browser setup here..");
        System.out.println("Accepted parameter value here : " + browser);
        System.out
                .println("Please note if the test is run without a parameter from suite the default "
                        + "value will be taken as Firefox as we have provided this "
                        + "argument to @optional annotation");
    }

    @Test
    public void testParameterPass() {
        System.out.println("All the test steps here..");
    }

    @AfterTest
    public void teardown() {
        System.out
                .println("Browser close and other closing activities to finish the Test execution here..");
    }
}
```



