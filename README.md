# Python Script for Sending SMS Using Way2SMS API

This repository contains a simple Python script to send SMS messages using the urllib2 and cookielib libraries. The script logs into the SMS service and sends a message to specified mobile numbers.

## Prerequisites

Before running the script, make sure you have Python installed on your system. This script is compatible with Python 2.x.

## How to Run

1. **Clone the Repository:**

    ```sh
    git clone https://github.com/salmanfareeth/Python-Script-for-Sending-SMS-Using-Way2SMS-API.git
    ```

2. **Navigate to the Project Directory:**

    ```sh
    cd Python-Script-for-Sending-SMS-Using-Way2SMS-API
    ```

# Install Required Libraries

Since the script uses urllib2 and cookielib, ensure you have these libraries available. These are included in the standard library for Python 2.x.

# Update Credentials

Open the script and update the username, passwd, message, and number variables with your own details.

 ```sh
    username = "your_username"
    passwd = "your_password"
    message = "Your message here"
    number = ["recipient_mobile_number"]
 ```

# Running the Script

To run the script, use the following command:

 ```sh
 python smsprocess.py
 ```

## The script performs the following steps:

1. **Prepare the Message**
The message to be sent is prepared by replacing spaces with + to conform to URL encoding.

python:

    message = "+".join(message.split(' '))


2. **Log into the SMS Service**

The script logs into the SMS service using the provided username and password.

python:

    url = 'http://site24.way2sms.com/Login1.action?'
    data = 'username=' + username + '&password=' + passwd + '&Submit=Sign+in'

3. **Handle Cookies**

A cookie jar is used to manage cookies during the session.

python:

    cj = cookielib.CookieJar()
    opener = urllib2.build_opener(urllib2.HTTPCookieProcessor(cj))
    opener.addheaders = [('User-Agent','Mozilla/5.0 ...')]

4. **Send the SMS**

For each number in the list, the script sends the SMS by making a request to the appropriate URL with the required data.

python:

    for i in number:
    jession_id = str(cj).split('~')[1].split(' ')[0]
    send_sms_url = 'http://site24.way2sms.com/smstoss.action?'
    send_sms_data = 'ssaction=ss&Token=' + jession_id + '&mobile=' + i + '&message=' + message + '&msgLen=136'
    opener.addheaders = [('Referer', 'http://site25.way2sms.com/sendSMS?Token=' + jession_id)]
    sms_sent_page = opener.open(send_sms_url, send_sms_data)
    
## Troubleshooting:

1. **Error While Logging In**
    If you encounter an error while logging in, ensure that your username and password are correct and that the login URL is accessible.

2. **Error While Sending Message**
    If an error occurs while sending the message, check if the recipient's mobile number is correct and that you have a valid session ID.


## Educational Purpose Only:

This project is created by salmanfareeth and is intended solely for educational purposes. Use it responsibly and modify it according to your needs.


## Privacy and Security:

Be cautious about sharing your credentials and ensure they are stored securely. This script logs into a third-party service using your credentials, so handle your data with care.


## Legal Compliance:

Ensure that your use of this script complies with the terms of service of the SMS provider and any relevant laws and regulations regarding automated messaging.


## Disclaimer:

Any damage or illegal usage resulting from this script is not my responsibility


## Contributing: 

If you would like to contribute to this project, please fork the repository and create a pull request with your changes.
