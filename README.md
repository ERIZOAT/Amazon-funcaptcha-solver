# Amazon Funcaptcha Solver, how to solve Funcaptcha on Amazon

According to many surveys, bot attacks and automated web-scraping programs pose a huge challenge to websites and online platforms. In response to these threats, many websites have adopted CAPTCHA (Completely Automated Public Turing Test to Differentiate Computers from Humans) systems to verify that users are human and not zombies.One such CAPTCHA system is Funcaptcha, which has gained popularity due to its advanced security features and ease of integration.

## Bonus Code
 A bonus code for [Capsolver](https://www.capsolver.com/): **AMN**. After redeeming it, you will get an extra 5% bonus after each recharge, Unlimited
 ![image](https://github.com/ERIZOAT/solve-amazon-captcha-python/assets/157081315/fc2a6424-a77d-48f1-a33d-458d1dfae0d9)

## What is Funcaptcha?  
Funcaptcha is a modern CAPTCHA solution that relies on JavaScript-based challenges instead of traditional image or audio-based CAPTCHAs. It presents users with a series of interactive tasks, such as dragging and dropping objects, solving puzzles, or entering text into a field. 

## Amazon and Funcaptcha 
Amazon, being a leading e-commerce platform, is no stranger to bot attacks and web scraping attempts. To protect their website and ensure a smooth user experience, Amazon has implemented Funcaptcha on various pages, particularly those related to product listings, checkout and login processes.  

## Sample scripts for Capsolver to solve Funcaptcha on Amazon

This repository contains sample code for solving CAPTCHA challenges using [Capsolver](https://www.capsolver.com/). These tools that utilize the Capsolver API include python and Node.js


## Solving Amazon Funcaptcha

### Create Task

Create a task with the [createTask](../api-createtask.md) to create a task.

### Task Object Structure

| Properties               | Type   | Required | Description                                                                                                                                                                                                                                                                                                                |
|--------------------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type                     | String | Required | `FunCaptchaTaskProxyLess`                                                                                                                                                                                                                                                                                                  |
| websiteURL               | String | Required | Web address of the website using funcaptcha, generally it's fixed value. (Ex: https://google.com)                                                                                                                                                                                                                          |
| websitePublicKey         | String | Required | The domain public key, rarely updated. (Ex: E8A75615-1CBA-5DFF-8031-D16BCF234E10)                                                                                                                                                                                                                                          |
| funcaptchaApiJSSubdomain | String | Optional | A special subdomain of [funcaptcha.com](http://funcaptcha.com/), from which the JS captcha widget should be loaded. Most FunCaptcha installations work from shared domains.                                                                                                                                                |
| data                     | String | Optional | Additional parameter that may be required by FunCaptcha implementation. Use this property to send "blob" value as a stringified array. See example how it may look like. {"\blob\":\"HERE_COMES_THE_blob_VALUE\"}  Learn [how to get FunCaptcha blob data](https://www.capsolver.com/blog/FunCaptcha/funcaptcha-data-blob) |
| proxy                    | String | Optional | Learn [Using proxies](../api-how-to-use-proxy)                                                                                                                                                                                                                                                                             |

### Example Request

``` json
POST https://api.capsolver.com/createTask
Host: api.capsolver.com
Content-Type: application/json

{
    "clientKey": "YOUR_API_KEY_HERE",
    "task": {
        "type":"FunCaptchaTaskProxyLess", //Required
        "websiteURL":"", //Required
        "websitePublicKey":"", //Required
        "data": "{\"blob\": \"flaR60YY3tnRXv6w.l32U2KgdgEUCbyoSPI4jOxU...\"}" // Optional
    }
}
```


After you submit the task to us, you should receive in the response a 'Task id' if it's successfull. Please
read [errorCode: full list of errors](https://captchaai.atlassian.net/wiki/spaces/CAPTCHAAI/pages/394062/FuncaptchaTask+solving+FunCaptcha#)
if you didn't receive the task id.

### Example Response

``` json
{
    "errorId": 0,
    "status": "idle",
    "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}

```

### **Getting Result**

Use the [getTaskResult](../api-gettaskresult.md) method to get the recognition results

Depending on the system load, you will get the results within the interval of `1s` to `20s`

### Example Request

``` json
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json

{
    "clientKey": "YOUR_API_KEY",
    "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}
```

### Example Response

``` json
{
    "errorId": 0,
    "solution": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
        "token": "3AHJ_q25SxXT-pmSeBXjzScW-EiocHwwpwqtk1QXlJnGnU......"
    },
    "status": "ready"
}
```



## Capolver Supported CAPTCHA types:
- FunCaptcha
- hCaptcha
- hCaptchaEnterprise
- reCAPTCHA v2/v3
- reCAPTCHA v3 Enterprise
- ImageToText
- Geetest v3/v4
- MtCaptcha
- AwsWafCaptcha

And Many more

## Documentation 
[Capsolver API documentation](https://docs.capsolver.com/guide/api-server.html)
