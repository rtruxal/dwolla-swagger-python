dwolla-swagger-python
=========

The new Dwolla API V2 SDK, as generated by [this fork of swagger-codegen](https://github.com/mach-kernel/swagger-codegen). 

## Version

1.0.3

## Installation

`dwollaswagger` is available on [PyPi](https://pypi.python.org/pypi/dwollaswagger), and therefore can be installed automagically via [pip](https://pip.pypa.io/en/latest/installing.html).

*To install via pip:*

```
pip install dwollaswagger
```

*To add to `requirements.txt` and make this a permanent dependency of your package:*

```requirements.txt
YourApp
SomeLibrary==1.2.3
dwollaswagger>=1.0.0
```
```
pip install -r requirements.txt
```

*To install directly from source:*
```
git clone https://github.com/Dwolla/dwolla-swagger-python && cd dwolla-swagger-python && python setup.py install 
```

*OS X users may need to run `setup.py` as a privileged user.*

## Quickstart

`dwollaswagger` makes it easy for developers to hit the ground running with our API. Before attempting the following, you should ideally create [an application key and secret](https://www.dwolla.com/applications).

### Configuring a client

To get started, all you need to set is the `access_token` and `host` values. 

```python
dwollaswagger.configuration.access_token = 'token'

# For UAT/Sandbox
client = dwollaswagger.ApiClient('https://api-uat.dwolla.com')

# For Production
client = dwollaswagger.ApiClient('https://api.dwolla.com')
```

### List 10 customers

Now that we've set up our client, we can use it to make requests to the API. Let's retrieve 10 customer records associated with the authorization token used. 

```python
dwollaswagger.configuration.access_token = 'token'
client = dwollaswagger.ApiClient('https://api-uat.dwolla.com')

customers_api = dwollaswagger.CustomersApi(client)
my_custies =  customers_api.list(limit=10)
```

`my_custies` will be a Python list that consists of `Customer` objects. 

### Creating a new customer

To create a customer, we can either provide a `dict` with the expected values, or a `CreateCustomer` object. 

```python
customers_api = dwollaswagger.CustomersApi(client)

location = customers_api.create(body = {
    'firstName': "Jennifer",
    'lastName': "Smith",
    'email': "jsmith@gmail.com",
    'phone': "7188675309"})
```

#### or 

```python
customers_api = dwollaswagger.CustomersApi(client)

new_cust = dwollaswagger.CreateCustomer
new_cust.first_name = "Jennifer"
new_cust.last_name = "Smith"
new_cust.email = "jsmith@gmail.com"
new_cust.phone = "7188675309"

location = customers_api.create(body=new_cust)
```

`location` will contain a URL to your newly created resource (HTTP 201 / Location header).

## Modules

`dwolla-python-swagger` contains `API` modules which allow the user to make requests, as well as `models` which are [DAOs](https://en.wikipedia.org/wiki/Data_access_object) that the library uses to serialize responses. 

### API
Each API module is named in accordance to ([Dwolla's API Spec](http://docsv2.dwolla.com/) and encapsulates all of the documented functionality. 

* `AccountsApi`
* `BusinessclassificationsApi`
* `CustomersApi`
* `DocumentsApi`
* `EventsApi`
* `FundingsourcesApi`
* `RootApi`
* `TransfersApi`
* `WebhooksApi`
* `WebhooksubscriptionsApi`

----------

API objects take an `ApiClient` argument, which you created [here](##Configuring a client).

##### Example 
```python
doc_api = dwollaswagger.DocumentsApi(your_client_object)
```

### Models

Each model represents the different kinds of requests and responses that can be made with the Dwolla API. 

* `AccountInfo`
* `Amount`
* `ApplicationEvent`
* `BaseObject`
* `BusinessClassification`
* `BusinessClassificationListResponse`
* `CreateCustomer`
* `CreateFundingSourceRequest`
* `CreateWebhook`
* `Customer`
* `CustomerListResponse`
* `Document`
* `DocumentListResponse`
* `EventListResponse`
* `FundingSource`
* `FundingSourceListResponse`
* `HalLink`
* `Money`
* `Transfer`
* `TransferListResponse`
* `TransferRequestBody`
* `Unit`
* `UpdateCustomer`
* `VerificationToken`
* `VerifyMicroDepositsRequest`
* `Webhook`
* `WebhookAttempt`
* `WebhookEventListResponse`
* `WebhookHeader`
* `WebhookHttpRequest`
* `WebhookHttpResponse`
* `WebhookListResponse`
* `WebhookRetry`
* `WebhookRetryRequestListResponse`
* `WebhookSubscription`

## README

In order for the library's README file to display nicely on PyPi, we must use the `*.rst` file format. When making changes to this README file, please [use this tool](http://johnmacfarlane.net/pandoc/try/) to convert the `*.md` file to `*.rst`, and make sure to keep both files updated.

## Changelog

1.0.3
* API schema updated, `RootApi` now added.
* Changed `auth_token` to `access_token` in compliance with [RFC-6749](https://tools.ietf.org/html/rfc6749) recommended nomenclature.

1.0.2
* API schema updated, new methods in `FundingsourcesApi`.
* All methods which take Swagger variables in `path` (e.g, `/resource/{id}`) can now be passed a resource URL to make it easier for HAL-styled API consumption.
* More idiomatic response logic for HTTP 201 responses.
* Fix syntax error in README

1.0.1
* API schema updated, new methods in `CustomersApi` and `TransfersApi`

1.0.0
* Initial release.

## Credits

This wrapper is semantically generated by a fork of [swagger-codegen](http://github.com/mach-kernel/swagger-codegen). 
 - [swagger-codegen contributors](https://github.com/swagger-api/swagger-codegen/network/members)
 - [David Stancu](http://github.com/mach-kernel)

## License

Copyright 2015 Swagger Contributors, David Stancu

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
