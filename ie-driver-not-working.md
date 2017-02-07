# IE not working {#ie-not-working}

---

There are several reasons why Internet explorer might not open, when you run your webdriver code. Please verify the below things taken care of before running the code.

1. **IEDriverServer.exe** is the file which is most likely to get corrupt when file is transferred from one machine to another. Please ensure the exe is a fresh download from seleniumhq.org. Also note there are different version of IEDriverServer for 32 bit and 64 bit. download the correct version as per your system configuration.

2. A very irritating InternetExplorer setting for running selenium code :**Security settings**, Please ensure all the security settings are either _**checked or unchecked.**_

3. A rather unnoticed but important setting is the browser resolution. Please ensure that the resolution is set to 100%, the code will not work if the resolution is not 100%. You will not even know why your script is not working, if this setting is not correct.

4. However we can tackle the zoom setting using the desired capabilities of IE browser.



