---
title: "Grocer Documentation"
keywords: 
sidebar: 
hide_sidebar: true
search: false
permalink: index.html
summary: These instructions will help you in setup server and mobile application.
---
# Introduction
The app is connected with Woocommerce (WordPress) using REST APIs, the following documentation will guide you through the process to connect the app with your Woocommerce Store.
   
# Setting up your wordpress
1. ### Install Wordpress
   Follow this link to get help in installing **Wordpress**:
                
        https://codex.wordpress.org/Installing_WordPress

2. ### Install and setup Woocommerce
   Follow this link to get help in installing and setup **Woocommerce**:
        
        https://docs.woocommerce.com/document/installation-2/

3. ### REST APIs for Woocommerce

    To use the latest version of the REST API you must be using:
    - WooCommerce 2.6+.
    - WordPress 4.4+.
    - You may access the API over either HTTP or HTTPS, but HTTPS is recommended where possible.
    - **IMPORTANT**: If your website uses **https** protocol i.e your website url is **https**://www.example.com, you will need to generate
      **CONSUMER KEY** and **CONSUMER SECRET**.
      Go to `WooCommerce` > `Settings` > `Advanced` > `REST API` > `ADD Key`. Copy both **CONSUMER KEY** and **CONSUMER SECRET**,
      these values will be required when we setup mobile application further in this document. You are not required to follow this step if your website uses **http** protocol.
    - Setup Pretty permalinks in Settings > Permalinks so that the custom endpoints are supported. Default permalinks will not work. 
    <h1 align="center"> Step 1</h1>
    <p align="center"><img src="{{ "images/3.1-rest-api-permalink-menu-highlight.png" }}"/></p>
    <h1 align="center"> Step 2</h1>
    <p align="center"><img src="{{ "images/3.2-rest-api-permalink-highlight.png" }}"/></p>

    - You also need to ensure that you web serve(Apache/Nginx) supports `HTTP Authorization Header`. If you are using shared hosting and it has 
      disabled the HTTP Authorization Header, then you need to enable it.
      To enable Authorization Header, please follow the following steps
      - Login to your shared hosting
      - Visit file manager and go to the root directory of your website.
      - You'll find a .htaccess file, in this file after `RewriteEngine on` line add following two lines:
    ```
    RewriteCond %{HTTP:Authorization} ^(.*)
    RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1]
    ```

      - After this change, ensure that a section of your file looks as below:
    ```
    RewriteEngine on
    RewriteCond %{HTTP:Authorization} ^(.*)
    RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1]
    ```
    ![image-4-7]
    ![image-4-8]
    
4. ### Plugins

    - **mobile-ecommerce.zip (Required)**
    
       You will find the file named `mobile-ecommerce.zip` in `wordpress-plugins` folder in the package you downloaded from envato.
       It provides multiple capabilities to our app and is neccessary to install.
       It enables `Authorization Header` based authentication for Woocommerce Rest APIs for websites that use **http** protocol. You need to install this plugin in your wordpress. If you are not aware of how to install the wordpress plugin, follow the following steps:
       - In your wordpress admin, go to **Admin Menu** > **Plugins** > **Add New** > **Upload Plugin**
       - Choose the file `mobile-ecommerce.zip`
       - Click on **Install Now**
       - Click on **Activate Plugin**
        
   -  **WooCommerce PayU India (Optional)**
      
      You only need to install this plugin if you need to integrate PayUMoney payment gateway.
      Follow the following link to install and setup this plugin:

            https://wordpress.org/plugins/woocommerce-payu-paisa/
     
       ![image-4-9]
       ![image-4-10]
       ![image-4-11]

# Mobile App

5. ### Install Node.js
   You must have **Node.js** installed on your system to begin building our app. Please follow the following step if nodejs is not installed on your system. If already done, you can skip this step
                
        Note: Install Node.js version 8 or above on your system. 

   Download the Node.js as per your operating system from [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
   To ensure that you have correct version of nodejs installed, from the command line issue the following command
   ```
   node -v
   ```
   If you see the string containing version number greater than 8, you are good to go. If you get `command not found error`, that means nodejs is not properly installed on your system. You'll need to troubleshoot the problem.
   ###### **You  may be able to use node version lessser than 8 but we haven't tested the app with these versions**


6. ### Install ionic and cordova
   In order to build our app you need to have installed ionic and cordova on your system. To install these packages issue the following command from command line:
    
        npm install -g ionic@3.9.2 cordova

    This will install the ionic and cordova programs on your system. To ensure that you have successfully installed both the programs, issue following command from the command line
    
        ionic -v && cordova -v

    If version number gets printed on the console, you are good to go. If you get `command not found error`, that means that these programs didn't get properly installed on your system. You'll need to troubleshoot the problem.

    **Make sure you do not accidentally install ionic-v4(beta)**

7. ### Connect the app with your woocommerce store
    In order to connect the app with your woocommerce store, you need to make changes in the `src/app/app.config.ts`. 
    Update the values of the following variables 
    1. **apiBase** - Example Value: `http://www.example.com/wp-json/`. This is the base url of woocommerce's REST APIs. Few of the examples of **apiBase** values are as follows:
      - http://www.example.com/wp-json/
      - http://subdomain.example.com/wp-json/
      - http://www.example.com:8000/wp-json/
      - http://www.example.com/subdirectory/wp-json/
        
        **Note: Replace www.example.com with your domain or IP address**

    2. **consumerKey** - Only set this if your website uses **https** protocol i.e your website url is like this **https**://www.example.com. This is the **Consumer Key** that you generated above while setting up **REST APIs for Woocommerce**. You may leave it blank if your website uses **http** protocol
    
    3. **consumerSecret** - Only set this if your website uses **https** protocol **https**://www.example.com. This is the **Consumer Secret** that you generated above while setting up **REST APIs for Woocommerce**. You may leave it blank if your website uses **http** protocol

    4. **adminUsername** - Only set this if your website uses **http** protocol **http**://www.example.com. This is the admin's username of your wordpress website, that you use while loging in admin section. You may leave it blank if your website uses **https** protocol
    
    5. **adminPassword** - Only set this if your website uses **http** protocol **http**://www.example.com. This is the admin's password of your wordpress website, that you use while loging in admin section. You may leave it blank if your website uses **https** protocol
    
    6. **paypalProduction** - Use your Paypal's PRODUCTION_CLIENT_ID. For more info, please visit [https://ionicframework.com/docs/native/paypal/](https://ionicframework.com/docs/native/paypal/)
    
    7. **paypalSandbox** - Use your Paypal's SANDBOX_CLIENT_ID (you will need this only for testing purpose, otherwise you can leave it blank)
    
    8. **payuSalt**: Your PayUMoney salt 
    
    9. **payuKey**: Your PayUMoney key

    10. **appName**: You can change the home screen title of the app by setting this value. Default: MOBIMALL

    Please make sure that you understand that you need to enter values for **consumerKey** and **consumerSecret** if your website uses **https**. And if your website uses **http**, you need to enter values for **adminUsername** and **adminPassword**.

8. ### Other Installations
    Ionic doesn't bundle all of the tooling required to build an app, it relies on some additional SDKs and software provided by Apple and/or Google. It is good to read and follow the platform guides provided by Ionic to set up for each platorm you wish to work with
    [Android Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html)
    [iOS Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/ios/index.html)
    You can do this at a later time, but you'll need to set up the platform tooling before you can preview or emulate an application on a simulator or device.
    
9. ### PayUMoney:
    - Create an account on [PayUMoney](http://www.payumoney.com)
    - Setup Payumoney key and Salt in variables "payuKey" and "payuSalt" respectively in `src/app/app.config.ts` file.    

10. ### PayPal
    - Setup paypal by creating account here: https://www.paypal.com/in/webapps/mpp/account-selection?pros=1and add keys.
       [How to Find the keys](http://support.berta.me/kb/online-shop/how-to-get-paypal-api-username-password-and-signature-information)
    - Setup PayPal sandbox id in variable "paypalSandbox” in the following file: src/app/app.config.ts

11. ### Deploy App
    Deploying apps on Google Play Store and Apple App Store is out of the scope of this document.
    Kindly refer to this [guide](https://ionicframework.com/docs/intro/deploying/) for further instructions.

**Note: If you are unable to understand any topic or find any topic needs more elaboration. 
Please raise an issue ticket at this link [https://opuslabs.freshdesk.com](https://opuslabs.freshdesk.com)**

[image-3-1]: {{ "images/3.1-rest-api-permalink-menu-highlight.png" }}
[image-3-2]: {{ "images/3.2-rest-api-permalink-highlight.png" }}
[image-4-1]: {{ "images/4.0-jwt-plugin-location.png" }}
[image-4-2]: {{ "images/4.1-plugin-step-1.png" }}
[image-4-3]: {{ "images/4.2-plugin-step-2-upload-button.png" }}
[image-4-4]: {{ "images/4.3-plugin-step-3-choose-file.png" }}
[image-4-5]: {{ "images/4.4-plugin-step-4-install-now.png" }}
[image-4-6]: {{ "images/4.5-plugin-step-5-activate.png" }}
[image-4-7]: {{ "images/4.7-htaccess-original.png" }}
[image-4-8]: {{ "images/4.8-htaccess-authorization-enabled.png" }}
[image-4-9]: {{ "images/6.1-search-payumoney-plugin.png" }}
[image-4-10]: {{ "images/6.2-highlight-payumoney-plugin.png" }}
[image-4-11]: {{ "images/6.6-payumoney-plugin-activate.png" }}
