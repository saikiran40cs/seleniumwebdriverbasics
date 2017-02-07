# Generate logs {#generate-logs}

If you have more than 30-40 tests to run in a suite, then it will be very difficult to track which script is being executed at what time. Also error warnings, time elapsed, execution status etc. cannot be tracked. In order to overcome these limitations we introduce logging functionality to our automation framework.

You need to download log4j jar from [Apache log4j 1.2 – Download Apache log4j 1.2](http://logging.apache.org/log4j/1.2/download.html). Place the log4j jar in your lib folder and add the same to build path. create a package with name testListener in your src folder. Create a class with name TestMonitor in this package and copy the below code to this class.

```
package testListener;

package testListener;

import java.io.PrintWriter;
import java.io.StringWriter;

import org.apache.log4j.Logger;
import org.apache.log4j.PropertyConfigurator;
import org.testng.ITestContext;
import org.testng.ITestResult;

public class TestMonitor implements org.testng.ITestListener {

    public Logger log = Logger.getLogger(this.getClass().getName());

    @Override
    public void onFinish(ITestContext arg0) {
        log.info("Test " + arg0.getName() + " Ends");
        log.info("---------------------------------------------------------");
    }

    @Override
    public void onStart(ITestContext arg0) {
        PropertyConfigurator.configure("src/log4j.properties");
        log.info("Test " + arg0.getName() + " Starts");
    }

    @Override
    public void onTestFailedButWithinSuccessPercentage(ITestResult arg0) {
        log.info("Test failed within success Percentage");
    }

    @Override
    public void onTestFailure(ITestResult arg0) {
        log.info("Test run has failed");
        log.error(arg0.getThrowable().getMessage());

        StringWriter sw = new StringWriter();
        arg0.getThrowable().printStackTrace(new PrintWriter(sw));
        String stacktrace = sw.toString();
        log.error(stacktrace.trim());
    }

    @Override
    public void onTestSkipped(ITestResult arg0) {
        log.info("Test skipped");
    }

    @Override
    public void onTestStart(ITestResult arg0) {
        log.info("Test Method " + arg0.getMethod().getMethodName()
                + " executing...");
    }

    @Override
    public void onTestSuccess(ITestResult arg0) {
        log.info("Test run is successful");
    }

}

```

Now create a file name log4j.properties in the src folder and copy paste the below lines to this file.

```
# This sets the global logging level and specifies the appenders
log4j.rootLogger=INFO, file, stdout
# Direct log messages to a log file
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=logsSeleniumLogs.log
log4j.appender.file.MaxFileSize=1MB
log4j.appender.file.MaxBackupIndex=1
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n

# Direct log messages to stdout
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n

```

When your run this suite, the logs will be generated as and when a script is taken up for execution. these logs can be found in the directory seleniumLogs.

