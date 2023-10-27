# WhatsApp Bulk Messages Without Saving Contacts

It is a python script that sends WhatsApp message automatically from WhatsApp web application without saved contact numbers. It can be configured to send advertising messages to recipients. It read data from an excel sheet and send a configured message to people.

## Contact me over Telegram: https://t.me/inforkgodara

## Important Note
* WhatsApp Business released API on May 2022, no longer needed this repository. You can accomplish your same requirements through WhatsApp Business APIs.

## Prerequisites

In order to run the python script, your system must have the following programs/packages installed and the contact number not need to be saved in your phone (You can use bulk contact number saving procedure of email). It has limitation of sending attachment but you can refer to my another repo which has functionality to send document file like pdf, image, etc.
* Python 3.8: Download it from https://www.python.org/downloads
* Chrome v79: Download it from https://chrome.google.com
* Pandas : Run in command prompt **pip install pandas**
* Xlrd : Run in command prompt **pip install xlrd**
* Selenium: Run in command prompt **pip install selenium** 
* Web Driver: Run in command prompt **pip install webdriver_manager**
* Openpyxl: Run in command prompt **pip install openpyxl**

## Approach
* First need to clone this respiratory
* Run python script script.py using py script.py in the terminal
* The script opens WhatsApp web using chrome.
* User needs to scan QR code from his/her phone.
* Enter in command prompt to execute further.
* The script hit url with contact number and message from excel sheet.
* Once all the message will be sent chrome driver will automatically closed.

Note: If you wish to send an image instead of text you can write attachment selection python code.

## Legal
* This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by WhatsApp or any of its affiliates or subsidiaries. This is an independent and unofficial software. Use at your own risk. Commercial use of this code/repo is strictly prohibited.

## Code
```
# Program to send bulk messages through WhatsApp web from an excel sheet without saving contact numbers
# Author @inforkgodara

from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from webdriver_manager.chrome import ChromeDriverManager
from time import sleep
import pandas

excel_data = pandas.read_excel('Recipients data.xlsx', sheet_name='Recipients')

count = 0

driver = webdriver.Chrome(ChromeDriverManager().install())
driver.get('https://web.whatsapp.com')
input("Press ENTER after login into Whatsapp Web and your chats are visiable.")
for column in excel_data['Contact'].tolist():
    try:
        url = 'https://web.whatsapp.com/send?phone=' + str(excel_data['Contact'][count]) 
        + '&text=' + excel_data['Message'][0]
        sent = False
        # It tries 3 times to send a message in case if there any error occurred
        driver.get(url)
        try:
            click_btn = WebDriverWait(driver, 35).until(
                EC.element_to_be_clickable((By.CLASS_NAME, '_3XKXx')))
        except Exception as e:
            print("Sorry message could not sent to " + str(excel_data['Contact'][count]))
        else:
            sleep(2)
            click_btn.click()
            sent = True
            sleep(5)
            print('Message sent to: ' + str(excel_data['Contact'][count]))
        count = count + 1
    except Exception as e:
        print('Failed to send message to ' + str(excel_data['Contact'][count]) + str(e))
driver.quit()
print("The script executed successfully.")
```
Note: The script may not work in case if the HTML of web WhatsApp is changed. If you face any problem please do let me know. Surely I will help you out. You can expect response on weekend only others days extremely busy with my routine activities.
