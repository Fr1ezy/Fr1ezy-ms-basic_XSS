# ms-basic_XSS

Version
Maven: net. microsoft: ms basic<=2.1.13.4

There is an XSS vulnerability in the search function

<img width="815" alt="image" src="https://github.com/Fr1ezy/Fr1ezy-ms-basic_XSS/assets/54392222/fc1fd1d6-f7bc-432f-9c66-bf6d07c044d8">

It can be seen that the XSS was caused by the page returning an error message
<img width="820" alt="image" src="https://github.com/Fr1ezy/Fr1ezy-ms-basic_XSS/assets/54392222/abbd1333-17b6-4803-851d-f26dd12e8011">

The server will encounter errors
![image](https://github.com/Fr1ezy/Fr1ezy-ms-basic_XSS/assets/54392222/390a83ac-a6b2-4125-8b2c-9ea0b9401e00)

As you can see, the error page returned two messages ${code} and ${msg}
![image](https://github.com/Fr1ezy/Fr1ezy-ms-basic_XSS/assets/54392222/47d9baf7-10cb-448b-b381-943d2fe2e70c)

Based on the error message, locate it in the XssHttpServletRequestWrapper.clean method, and you can see that the error message returned by the front-end is the exception thrown by the XssHttpServletRequestWrapper.clean method, which directly returns the exception information leading to XSS
![image](https://github.com/Fr1ezy/Fr1ezy-ms-basic_XSS/assets/54392222/cd4393c6-8ddb-4e72-b5e6-6918dc9607a1)

![image](https://github.com/Fr1ezy/Fr1ezy-ms-basic_XSS/assets/54392222/9267f61c-9c95-4d85-9076-7c9156cfef60)

Due to XssHttpServletRequestWrapper processing user input parameters before Servlet, it can lead to XSS vulnerabilities
