# DNI

#### V1
###### 11/21/2017


## Summary:

Dynamic Number Identification (DNI) identifies the source of the referred site from the parameters present in the url and replaces the phone number based on the source in the webpage. The phone number could be present in multiple places such as in header, cards, list layout, table view, modal popup, carousel, or in any text. It also replaces the phone number inside the html tags where required such as `<a href="tel:123-123-1234"></a>` tags


## How it Works:

Initially a default phone number is displayed which is a generic number. The webpage will call the api which will respond with a list of phone numbers associated with the respective sources. The version 1 of DNI identifies the below sources:
* Google
* Facebook
* Twitter

The api response needs to be in the below format:
```
[
 {"name":"google", "number":"123-123-1111"}, 
 {"name":"facebook", "number":"321-123-4321"}, 
 {"name":"twitter", "number":"312-432-5432"}
]
```

DNI identifies the origin source by getting the value of the `utm_source` from the url and matches with the name from the api response and replaces the phone number associated with this name in the webpage.


## Under the Hood: 

DNI is built using plain javascript in ES6. 
DNI executes in the following steps:

**Step 1:** It calls the api which returns the list of origin names and numbers associated with the origins. 

**Step 2:** It identifies the origin source from the url using the query parameter `utm_source`. In addition it also identifies the origin medium from the url using the query parameter `utm_medium`. But the `utm_medium` is optional.

**Step 3:** It run a loop with the api response and checks if the `utm_source` name matches with the name in the api response data.

**Step 4:** After a match is found, it takes the number associated with the matched origin name and replaces the phone number in the web page. The phone number is replaced when the html document is in ready state.




