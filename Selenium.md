v4.22
# Introduction
Selenium is a library for [[automation]] testing of browser interactions of an application, such as UI interactions. It can be done in [[Python]], [[Java]] and [[JavaScript]].
- [YouTube Video Intro on what is Selenium](https://www.youtube.com/watch?v=TdwwPP9oW4c&ab_channel=Simplilearn)

In older version of Selenium, a driver was required for each browser you wanted to test on. As of v4.8, this is no longer needed. Selenium includes these drivers.
# Installation
1. Install Python or Python3
2. Install pip or pip3
3. Use pip/pip3 to Install Selenium

# How To Use

The following example snippet makes Selenium:
1. open a headless Chrome browser, with a default download directory set to a folder called 'downloads' relative to this script's location
2. navigate to YouTube main page
3. wait for the page to load finish
4. click on an HTML element with a class of "blabla"
5.  close the browser

```
#!/usr/bin/python3

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

#webdriver options
options = webdriver.ChromeOptions()
options.add_argument("--headless")
options.add_argument("--no-sandbox")
options.add_argument("--disable-dev-shm-usage")
# options.add_experimental_option('excludeSwitches', ['enable-logging'])
prefs = {"profile.default_content_settings.popups": 0,    
        "download.default_directory":"downloads", ### Set the path accordingly
        "download.prompt_for_download": False, ## change the downpath accordingly
        "download.directory_upgrade": True}
options.add_experimental_option("prefs", prefs)
driver = webdriver.Chrome(options=options)

# start download
driver.get("https://www.youtube.com/")
WebDriverWait(driver, 5).until(EC.presence_of_element_located((By.CLASS_NAME, "blabla")))
driver.find_element(By.CLASS_NAME, "blabla").click()

driver.quit()
```

Generally, there are a lot of documentation available online for syntax, examples and use cases.