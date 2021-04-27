|
 |
 |
 |
| --- | --- | --- |

## Gateway Integration Guide

V1.06

| **Version** | **Date** | **Update information** |
| --- | --- | --- |
| 1.01 | 13/11/2020 | Added version and version control to guide. |
| 1.02 | 10/12/2020 | Added Stored Credentials section. |
| 1.03 | 12/12/2020 | Removed reference to E-Receipts. |
| 1.04 | 27/01/2021 | Added Section 23 – Digital Wallets (only Google Pay). |
| 1.05 | 28/01/2021 | Added Apple Pay to Digital Wallets section. |
| 1.06 | 17/03/2021 | Integrated separate 3DSv2 Guide. |

**Contents**

**[1](#_Toc66871497)****Gateway Integration 4**

**[2](#_Toc66871498)****New Transactions 21**

**[3](#_Toc66871499)****Management Requests 25**

**[4](#_Toc66871500)****Hosted Payment Page Options 27**

**[5](#_Toc66871501)****AVS/CV2 Checking 29**

**[6](#_Toc66871502)****3-D Secure Authentication 33**

**[7](#_Toc66871503)****Risk Checking 49**

**[8](#_Toc66871504)****Payment Facilitators 57**

**[9](#_Toc66871505)****UK MCC 6012 Merchants 58**

**[10](#_Toc66871506)****Billing Descriptor 60**

**[11](#_Toc66871507)****Surcharges 62**

**[12](#_Toc66871508)****Receipts and Notifications 66**

**[13](#_Toc66871509)****Recurring Transaction Agreements 70**

**[14](#_Toc66871510)****Duplicate Transaction Checking 74**

**[15](#_Toc66871511)****Purchase Data 75**

**[16](#_Toc66871512)****Custom Data 79**

**[17](#_Toc66871513)****Advanced Data 80**

**[18](#_Toc66871514)****Gateway Wallet 87**

**[19](#_Toc66871515)****Masterpass Wallet 94**

**[20](#_Toc66871516)****PayPal Transactions 105**

**[21](#_Toc66871517)****Amazon Pay Transaction 130**

**[22](#_Toc66871518)****PPRO Transactions 142**

**[23](#_Toc66871519)****Digital Wallet Transactions 154**

**[A-1](#_Toc66871520)****Response Codes 159**

**[A-2](#_Toc66871521)****AVS / CV2 Check Response Codes 167**

**[A-3](#_Toc66871522)****3-D Secure Enrolment/Authentication Codes 169**

**[A-4](#_Toc66871523)****3-D Secure Enrolment/Authentication Only 170**

**[A-5](#_Toc66871524)****SCA Exemptions 171**

**[A-6](#_Toc66871525)****Secure Legacy API 172**

**[A-7](#_Toc66871526)****Request Checking Only 178**

**[A-8](#_Toc66871527)****Merchant Account Mapping 179**

**[A-9](#_Toc66871528)****Velocity Control System (VCS) 180**

**[A-10](#_Toc66871529)****Capture Delay 181**

**[A-11](#_Toc66871530)****Types of card 182**

**[A-12](#_Toc66871531)****Integration Testing 184**

**[A-13](#_Toc66871532)****Sample Signature Calculation 190**

**[A-14](#_Toc66871533)****Transaction Life cycle 192**

**[A-15](#_Toc66871534)****Transaction types 196**

**[A-16](#_Toc66871535)****Payment Tokenisation 197**

**[A-17](#_Toc66871536)****Repeat Transactions 200**

**[A-18](#_Toc66871537)****Transaction Cloning 203**

**[A-19](#_Toc66871538)****Stored Credentials Framework 209**

**[A-20](#_Toc66871539)****Integration Libraries 215**

**[A-21](#_Toc66871540)****Example HTTP Requests 249**

**[A-22](#_Toc66871541)****Example Integration Code 257**

**[A-23](#_Toc66871542)****Example Library Code 266**

**[A-24](#_Toc66871543)****Frequently Asked Questions 281**

**[Index ………………………………………………………………………………………………………………………….282](#_Toc66871544)**

1.
# Gateway Integration

  1.
## About This Guide

This guide provides the information required to integrate with our Payment Gateway and gives a very basic example of code for doing so It is expected that you have some experience in server-side scripting with languages such as PHP or ASP; or that an off-the-shelf software package is being used that has inbuilt or plug-in support for our Gateway.

  1.
## Terminology

The following terms are used throughout this guide:

**Gateway**

The Payment Gateway.

**Merchant**

The Merchant using the Gateway&#39;s services.

**Our**

The Payment Gateway Provider.

**You/your**

The Merchant or its representative performing the integration.

**Acquirer**

The bank or financial institution used by the Merchant.

**Customer**

A Customer of the Merchant making a payment.

**Card**

A payment credit, debit, prepayment or gift card issued by the Card Schemes.

**Card Scheme**

The operator of a payment Card network, such as Visa, Mastercard, et al.

**Cardholder**

The person who owns the payment Card, usually the Customer.

**Issuer**

The bank or financial institution that issued the payment Card to the Cardholder.

**Merchant Account**

An account on the Gateway mapped to an Acquirer-provided account.

**Checkout**

Third-party checkout solution such as PayPal, Amazon Pay other alternative payment methods.

**Wallet**

Third-party wallet solution such as Masterpass.

**Hosted Payment Page (HPP)**

A page hosted on our secure server used to collect Customer details.

**Hosted Payment Field (HPF)**

An individual form field hosted on our secure server used to collect sensitive Cardholder data.

  1.
## Integration Methods

There are three methods of integration provided to process your transactions through the Gateway, allowing for different levels of control and communication from your website.

    1.
### Hosted Integration

The Hosted Integration method makes it easy to add secure payment processing to your ecommerce business, using our Hosted Payment Pages (HPP). You can use this method if you do not want to collect and store Cardholder data.

The Hosted Integration method works by redirecting the Customer to our Gateway&#39;s Hosted Payment Page, which will collect the Customer&#39;s payment details and process the payment before redirecting the Customer back to a page on your website, letting you know the payment outcome. This allows you the quickest path to integrating with the Gateway.

The standard Hosted Payment Page is designed to be shown in a lightbox over your website and styled with logos and colours to match. Alternatively, you can arrange for fully customised Hosted Payment Pages to be produced that can match your website&#39;s style and layout. These fully customised pages are usually provided using a browser redirect, displaying full-page in the browser, or can be displayed embedded in an iframe on your website.

For greater control over the customisation of the payment page, our Gateway offers the use of Hosted Payment Fields, where only the individual input fields collecting the sensitive Cardholder data are hosted by the Gateway while the remainder of the payment form is provided by your website. These Hosted Payment Fields fit seamlessly into your payment page and can be styled to match your payment fields. When your payment form is submitted to your server, the Gateway will submit a payment token representing the sensitive card data it collected and your webserver can then use the Direct Integration to process the payment without ever being in contact with the collected Cardholder data. For more information please refer to our Hosted Payment Fields SDK Guide.

    1.
### Direct Integration

The Direct Integration works by allowing you to keep the Customer on your system throughout the checkout process, collecting the Customer&#39;s payment details on your own secure server before sending the collected data to our Gateway for processing. This allows you to provide a smoother, more complete checkout process to the Customer.

In addition to basic sales processing, the Direct Integration can be used to perform other actions such as refunds and cancellations, which can provide a more advanced integration with our Gateway.

    1.
### Batch Integration

The Batch Integration is an enhancement to the Direct Integration, allowing you to send multiple transactions in a single request and monitor their status. This is useful if you wish to capture multiple transactions or collect multiple payments – for example, collecting subscription charges or loan repayments.

In addition to basic sales processing, the Batch Integration can be used to perform other actions, such as refunds and cancellations, which can provide a more advanced integration with our Gateway.

Unlike the Hosted and Direct Integrations, the Batch Integration does not process transactions sent to it immediately. Instead, the Gateway queues these transactions to be processed and returns a batch reference number which can be used to download a file that contains the current status of the transactions.

Batch Processing does not support transactions that require Customer interaction such as 3D Secure transactions, or alternative payment methods with interactive Wallet or Checkout pages.

  1.
## Integration Libraries

We can provide a range of libraries to help you to integrate with the Gateway.

These libraries include simple server-side classes in many popular programming languages, through to client-side scripts to help with the integration of the Hosted Payment Page or Hosted Payment Fields.

For more information about these libraries, please refer to appendix 23.7A-20.

  1.
## Security and Compliance

Each method requires a different level of server security and compliance with the Payment Card Industry Data Security Standard (PCI DSS).

If you use Hosted Payment Pages with the Hosted Integration or Hosted Payment Fields with the Direct or Batch Integrations, then your webserver does not need an SSL certificate and you require the lowest level of PCI DSS compliance.

If your website collects and/or stores sensitive Cardholder data, such as the card number (PAN) or card security code (CVV/CV2), then your webserver must have an SSL certificate and serve all payment forms using HTTPS. You will also need a higher level of PCI DSS compliance and to complete a PCI validation form annually.

For more information, please see https://www.pcisecuritystandards.org/

## Integration Details

    1.
### HTTP Requests

A request can be sent to the Gateway by submitting a HTTP POST request to the integration URL provided.

The request should have a Content-Type: application/x-www-form-urlencoded HTTP header and the request should be name, value pairs URL encoded as per RFC 1738.

Example URL encoding:

merchantID=100001&amp;action=SALE&amp;type=1&amp;amount=1001&amp;currencyCode=826&amp;countryCode=826&amp;transactionUnique=55f6db1c81d95&amp;orderRef=Test+purchase&amp;customerPostCode=NN17+8YG&amp;responseCode=0&amp;responseMessage=AUTHCODE%3A350333&amp;state=captured&amp;xref=15091702MG47WN32MM88LPK&amp;cardNumber=4929+4212+3460+0821&amp;cardExpiryDate=1215

_ **Please note that the field names are cAsE sEnSiTiVe** __._

The response will use the same URL encoding and return the request fields in addition to any dedicated response field. If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

    1.
### Hosted HTTP Requests

When using the Hosted Integration, the request must be sent from the Customer&#39;s web browser as the response will be a HTML Hosted Payment Page (HPP), used to collect the Customer&#39;s details. The format of the request is designed so that it can be sent using a standard HTML form with the data in hidden form fields. The browser will then automatically encode the request correctly according to application/x-www-form-urlencoded format.

When the Hosted Payment Page has been completed and the payment processed, the Customer&#39;s browser will be automatically redirected to the URL provided via the **redirectURL** field. The response will be returned to this page in application/x-www-form-urlencoded format, using a HTTP POST request.

If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

An example of a Hosted Integration request is provided in appendix A-21.1 and sample code is provided in appendix A-22.1.

    1.
### Direct HTTP Requests

When using the Direct Integration, the response will be received in the same URL encoded format, unless a **redirectURL** field is provided.

If a **redirectURL** field is provided, then the response will be a HTML page designed to redirect a browser to the URL provided, using a HTTP POST request containing the response. This allows you to collect the Cardholder&#39;s payment details on your own server, using a HTML form which POSTs to the Direct Integration, which then effectively POSTs the results back to this URL your webserver, where you can display the transaction outcome.

If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

An example of a Direct Integration request is provided in appendix A-21.1 and sample code is provided in appendix A-22.1.

    1.
### Batch HTTP Requests

When using the Batch Integration, a single HTTP POST request can contain multiple individual requests using the multipart/mixed content type with a boundary string specified. Within that main HTTP request, each of the parts contains a nested Direct Integration HTTP request, separated by the boundary string.

Each part should begin with a Content-Type: application/x-www-form-urlencoded HTTP header and contain a single Direct Integration HTTP request, as documented in section 1.5.3.

You can optionally specify a Content-Id HTTP header to identify each part message uniquely; if not provided, the Gateway will assign a unique id to each part. The Content-Id HTTP header is returned in the response. The Gateway will not validate the uniqueness of any id provided. After the mandatory Content-type and the optional _Content-Id_ header, two carriage return/line feed pairs must follow (i.e. _\r\n\r\n_). Any deviation from this structure might lead to the part being rejected or incorrectly interpreted. The part request payload, formatted as a regular HTTP URL encoded request, must follow the two-line breaks directly.

To reduce the size of large batch requests, the Gateway supports compression using a Content-Encoding HTTP header with either a &#39;gzip&#39; or &#39;x-gzip&#39; value. This header can be provided in the main request or in the part request or both.

An Authorization HTTP header can be used in the request to provide the username and password of a Gateway Merchant Management System user account. If correct, the batch details will be recorded as having been submitted by that user; if invalid, then the request will fail and respond with a 401 (Unauthorised) HTTP status code.

The Gateway will respond in the same manner as the request with a multipart/mixedcontent type; each part is the response to one of the requests in the batched request. In addition, the response will contain a standard Location HTTP header, providing a URL from which further batch update responses can be downloaded; and a standard Content-Disposition header, allowing a browser to download the response to a file. If the request contained an Authorization HTTP header, then the response will contain an X-P3-Token HTTP header containing an authentication token that can be sent in future requests instead of the username and password. The authentication token has a limited life span, but each future request will return a new token and thus effectively rejuvenate the token&#39;s life.

Like the parts in the request, each response part contains a HTTP response, including headers and body. Each response part is preceded by a Content-Type HTTP header and Content-ID HTTP header. In addition, an X-Transaction-ID HTTP header is added containing the requests transaction id together with an X-Transaction-Response HTTP header containing a textual description of the transaction processing status.

_The Gateway will not process the transactions immediately but will queue them up to process over time. The transactions may not be processed in the order provided, so should not have interdependencies. Transactions will only appear in the Merchant Management System when they have been processed. The status of queued transaction is only available by querying the status of the batch._

The current status of a batch can be queried at any time by issuing a HTTP GET request to the URL provided in the initial responses Location HTTP header.

An Authorization HTTP header must be provided in the status request, containing either the username and password of a Gateway Merchant Management System user account or an authentication token returned in the batch submission response&#39;s X-P3-Token HTTP header. If a valid username and password or a valid token is provided, then the response will be an updated version of the initial submission response providing the current status of each transaction. The response will only contain transactions that the authenticated user has permission to view.

An example of a Batch Integration request is provided in appendix A-21.3 and sample code is provided in appendix A-22.3.

    1.
### Handling Errors

When the Gateway is uncontactable due to a communications error, or problem with the internet connection, you may receive a HTTP status code in the 500 to 599 range. In this situation, you may want to retry the transaction. If you do choose to retry a transaction, then we recommend that you perform a limited number of attempts with an increasing delay between each attempt.

If the Gateway is unavailable during a scheduled maintenance period, you will receive a HTTP status code of 503 &#39;Service Temporarily Unavailable&#39;. In this situation, you should retry the transaction after the scheduled maintenance period has expired. You will be notified of the times and durations of any such scheduled maintenance periods in advance, by email, and given a time when transactions can be reattempted.

If you are experiencing these errors, then we recommend you consider the following steps as appropriate for the integration method being used:

- Ensure the request is being sent to HTTPS and not HTTP. HTTP is not supported and is not redirected.
- Send transactions sequentially rather than concurrently.
- Configure your integration code with try/catch loops around individual transactions to determine whether they were successful or not and retry if required, based on the return code or HTTP status returned.
- Configure the integration so that if one transaction fails, the entire batch does not stop at that point – i.e. log the failure to be checked and then skip to the next transaction rather than stopping entirely.

    1.
### Redirect URL

The **redirectURL** request field is used to provide the URL of a webpage on your server.

When provided, the Gateway will respond with a HTML page designed to redirect the Customer&#39;s browser to the URL provided, using a HTTP POST request containing the URL encoded response.

For the Hosted Integration, this will redirect the Customer from the Hosted Payment Page back to this URL on your website.

For the Direct Integration, this allows you to collect the Cardholder&#39;s payment details on your own server using a HTML form that POSTs to the Direct Integration. which then effectively POSTs the results back to this URL on your webserver, where you can display the transaction outcome. This usage is not recommended as it makes it harder to sign the message.

The URL is mandatory for the Hosted Integration and optional for the Direct Integration. It is not supported by the Batch Integration.

The **redirectURL** must be a fully qualified URL, containing at least the scheme and host components.

    1.
### Callback URL

The **callbackURL** request field allows you optionally to request that the Gateway sends a copy of the response to an alternative URL. In this case, each response will then be POSTed to this URL in addition to the normal response. This allows you to specify a URL on a secure shopping cart or backend order processing system, which will then fulfil any order associated with the transaction.

The URL is optional for both the Hosted Integration and the Direct Integration. It is not supported by the Batch Integration.

The **callbackURL** must be a fully qualified URL, containing at least the scheme and host components.

    1.
### Field Formats

Most integration field values are either numerical or textual; and either free format or from a range of predetermined values. Some field values are records or arrays of records.

Unless otherwise stated, numerical values are whole integer values with no decimal points. Textual values should use the UTF-8 character set and will be automatically truncated if too long, unless stated otherwise in the field&#39;s description. Textual values may be transliterated
# 0
 when sending to third parties such as Acquirers but the original value is stored by Gateway and displayed in the Merchant Management System.

Field values should use the following formats unless otherwise stated in the field&#39;s description:

| **Field Type** | **Value Format** |
| --- | --- |
| **Monetary Amounts** | Either major currency units by providing a value that includes a single decimal point such as &#39;10.99&#39;; or in minor currency units by providing a value that contains no decimal points such as &#39;1099&#39;. |
| --- | --- |
| **Timestamps** | Date in the format &#39;YYYY-MM-DD HH:MM:SS&#39; |
| **Dates** | Date in the format &#39;YYYY-MM-DD&#39; |
| **Country Codes** | Either the ISO-3166-1 2-letter, 3-letter or 3-digit code. |
| **Currency Codes** | Either the ISO-4217 3-letter or 3-digit code. |
| **Records** | Records can be provided using the _[XX]_ notation, where _XX_ is the record&#39;s field name (sub-field). Records can be multi-dimensional or be sequentially indexed. For example: to send a value for the sub-field _Y_ in the integration field _X,_ use the field name _X[Y]_; however, to send a value for the sub-field _Y_ in the fourth record for integration field _X,_ then use the field name _X[4][Y]_ etc. |
| **Serialised Records** | Records can be sent as a JSON, XML or URL serialised string. The first character of the serialised string determines its format: &#39;[&#39; indicates JSON format; &#39;\&lt;&#39; indicates XML format; and anything else is assumed to be RFC 1738 URL encoded format. |

Note: Nested records are useful when posting sub-fields direct from a HTML FORM. However, unlike the main integration fields, a nested record&#39;s sub-fields are not sorted when constructing the signature and are processed in the order received. Serialised records can overcome any problems caused by a nested record&#39;s fields being received in a different order to that used when generating the signature.

  1.
## Authentication

All requests must specify which Merchant Account they are for, using the **merchantID** request field. In addition to this, the following security measures can be used:

    1.
### Password Authentication

You can configure a password for each Merchant Account, using the Merchant Management System (MMS). This password must then be sent in the **merchantPwd** field in each request. If an incorrect password is received by the Gateway, then the transaction will be aborted and an error response is returned.

![](RackMultipart20210427-4-13xkgeo_html_8136cf6329938ee9.gif)

Warning: Use of a password is discouraged in any integration where the transaction is posted from a form in the client browser as the password may appear in plain text in code.

    1.
### Message signing

You must configure a signing secret phrase for each Merchant Account using the Merchant Management System (MMS). Each request will need to be &#39;signed&#39; by providing a **signature** field containing a hash generated from the combination of the serialised request and this signing secret phrase. On receipt, the Gateway will then re-generate the hash and compare it with the one sent. If the two hashes are different then the request received must not be the same as that sent and so the contents must have been tampered with and the transaction will be aborted and an error response is returned.

The Gateway will also return hash of the response message in the returned **signature** field, allowing you to create your own hash of the response (minus the **signature** field) and verify that the hashes match.

If message signing is enabled, then the data POSTed to any callback URL will also be signed.

See appendix A-13 for information on how to create the hash.

    1.
### Allowed IP addresses

You can configure a list of IP addresses using the Merchant Management System (MMS). Two different address lists can be configured, one for standard requests, such as sales; and one for advanced requests, such as refunds and cancellations. If a request is received from an address other than those configured, then it will be aborted and an error response is returned.

  1.
## Supported Actions

All requests must specify what action they require the Gateway to perform, using the **action** request field. The Direct and Batch Integrations support all actions; however, the Hosted Integration only supports the basic payment actions.

    1.
### SALE

This will create a new transaction and attempt to seek authorisation for a sale from the Acquirer. A successful authorisation will reserve the funds on the Cardholder&#39;s account until the transaction is settled.

The **captureDelay** field can be used to state whether the transaction should be authorised only and settled at a later date. For more details on delayed capture, refer to appendix A-10.

    1.
### VERIFY

This will create a new transaction and attempt to verify that the card account exists with the Acquirer. The transaction will result in no transfer of funds and no hold on any funds on the Cardholder&#39;s account. It cannot be captured and will not be settled. The transaction **amount** must always be zero.

This transaction type is the preferred method for validating that the card account exists and is in good standing; however, it cannot be used to validate that it has sufficient funds.

    1.
### PREAUTH

This will create a new transaction and attempt to seek authorisation for a sale from the Acquirer. If authorisation is approved, then it is immediately voided (where possible) so that no funds are reserved on the Cardholder&#39;s account. The transaction will result in no transfer of funds. It cannot be captured and will not be settled.

![](RackMultipart20210427-4-13xkgeo_html_18948d07562c2eaa.gif)

Warning: If the transaction is to be completed then a new authorisation must be sought using the SALE action. If the PREAUTH authorisation could not be successfully voided, then this will result in the funds&#39; being authorised twice effectively putting two holds on the amount on the Cardholder&#39;s account and thus requiring twice the amount to be available in the Cardholder&#39;s account. It is therefore recommended only to PREAUTH small amounts, such as £1.00 to check mainly account validity.

This transaction type can be used to check whether funds are available and that the account is valid. However, due to the problem highlighted below, it is recommended that Merchants use the VERIFY action when supported by their Acquirer.

    1.
### REFUND\_SALE

This will create a new transaction and attempt to seek authorisation for a refund of a previous SALE from the Acquirer. The transaction will then be captured and settled if and when appropriate. It can only be performed on transactions that have been successfully settled. Up until that point, a CANCEL or partial CAPTURE can be refunded or partially refunded from the original SALE transaction. The previous SALE transaction should be specified using the **xref** field.

Partial refunds are allowed by specifying the **amount** to refund. Any amount must not be greater than the original received amount minus any already refunded amount. Multiple partial refunds may be made while there is still a portion of the originally received amount un-refunded.

The **captureDelay** field can be used to state whether the transaction should be authorised only and settled at a later date. For more details on delayed capture refer to appendix A-10.

_ **This action is not supported by the Hosted Integration.** _

    1.
### REFUND

This will create a new transaction and attempt to seek authorisation for a refund from the Acquirer. The transaction will then be captured and settled if and when appropriate. This is an independent refund and need not be related to any previous SALE. The amount is therefore not limited by any original received amount.

The **captureDelay** field can be used to state whether the transaction should be authorised only and settled at a later date. For more details on delayed capture refer to appendix A-10.

_ **This action is not supported by the Hosted Integration.** _

    1.
### CAPTURE

This will capture an existing transaction, identified using the **xref** request field, making it available for settlement at the next available opportunity. It can only be performed on transactions that have been authorised but not yet captured. An **amount** to capture may be specified but must not exceed the original amount authorised.

The original transaction must have been submitted with a **captureDelay** value that prevented immediate capture and settlement leaving the transaction in an authorised but un-captured state. For more details on delayed capture refer to appendix A-10.

_ **This action is not supported by the Hosted Integration.** _

    1.
### CANCEL

This will cancel an existing transaction, identified using the **xref** request field, preventing it from being settled. It can only be performed on transactions, which have been authorised but not yet settled, and it is not reversible. Depending on the Acquirer it may not reverse the authorisation and release any reserved funds on the Cardholder&#39;s account. In such cases, authorisation will be left to expire as normal releasing the reserved funds. This may take up to 30 days from the date of authorisation.

_ **This action is not supported by the Hosted Integration.** _

    1.
### QUERY

This will query an existing transaction, identified using the **xref** request field, returning the original response. This is a simple transaction lookup action.

_ **This action is not supported by the Hosted Integration.** _

1.
# New Transactions

You can perform a new transaction, such as a sale, by sending a request with the required action and transaction type together with details about the order and payment method.

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **merchantID** | Yes | Your Gateway Merchant ID. |
| --- | --- | --- |
| **merchantPwd** | No
# 1
 | Any password used to secure this account.Refer to section 1.6.1 for details. |
| **signature** | Yes
# 2
 | Any hash used to sign this request.Refer to section 1.6.2 for details. |
| **action** | Yes | The action requested.Refer to section 1.7 for supported actions.
Possible values are: **PREAUTH, VERIFY, SALE, REFUND, REFUND\_SALE.** |
| **amount** | Yes
# 3
 | The amount of the transaction. |
| **type** | Yes3 | The type of transaction.Refer to appendix A-15 for details.
Possible values are: **1** – E-commerce (ECOM) **2** – Mail Order/Telephone Order (MOTO). **9** – Continuous Authority (CA). |
| **countryCode** | Yes3 | Merchant&#39;s location. |
| **currencyCode** | Yes3 | Transaction currency. |
| **paymentMethod** | No | The payment method required. For card payments either omit this field or use the value **card**. |
| **cardNumber** | Yes3,
# 4
 | The primary account number (PAN) as printed on the front of the payment card. Digits and spaces only. |
| **cardExpiryMonth** | Yes3,4 | Payment card&#39;s expiry month from 1 to 12. |
| **cardExpiryYear** | Yes3,4 | Payment card&#39;s expiry year from 00 to 99. |
| **cardExpiryDate** | No3,4 | Payment card&#39;s expiry date in MMYY format as an alternative to sending a separate **cardExpiryMonth** &amp; **cardExpiryYear**. |
| **cardCVV** | Yes3,4 | Payment card&#39;s security number. The 3-digit number printed on the signature strip. |
| **transactionUnique** | No3 | You can supply a unique identifier for this transaction. This is an added security feature to combat transaction spoofing. |
| **orderRef** | No3 | Free format text field to store order details, reference numbers, etc. for the Merchant&#39;s records. |
| **orderDate** | No | Optional date to record with the transaction. |
| **captureDelay** | No | Number of days to wait between authorisation of a payment and subsequent settlement.Refer to appendix A-10 for details. |
| **xref** | No
# 5

 | Reference to a previous transaction.Refer to appendix A-16 for details. |
| **redirectURL** | No6 | A public URL which the hosted form will redirect the Customer&#39;s browser after the transaction has been completed. The URL must be fully qualified and include at least the scheme and host components.Refer to section 1.5.6 for details. |
| **callbackURL** | No
# 6
 | A non-public URL which will receive a copy of the transaction result by POST.The URL must be fully qualified and include at least the scheme and host components.Refer to section 1.5.7 for details. |
| **remoteAddress** | No
# 7
 | IP address of client making the transaction. This should be provided where possible to aid fraud prevention. |

If the REFUND\_SALE action is used, then the request may not attempt to change the payment details, or the request will fail with a **responseCode** of **65542 (REQUEST MISMATCH)** because the refund must be made to the original card.

  1.
## Response Fields

The response will contain all the fields sent in the request (minus any **cardNumber** and **cardCVV** ) plus the following:

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **responseCode** | Always | A numeric code providing the specific outcome.
Common values are: **0** - Successful / authorised transaction. **1** - Card referred – Refer to card issuer. **2** - Card referred – Special condition. **4** - Card declined – Keep card. **5** - Card declined.
Check **responseMessage** for more details of any error that occurred. |
| --- | --- | --- |
| **responseStatus** | Always | A numeric code providing the outcome category.
Possible values are: **0** – Authorisation Approved / No reason to decline **1** – Authorisation Declined. **2** – Authorisation Error / Transaction malformed. |
| **responseMessage** | Always | Message received from the Acquiring bank, or any error message. |
| **transactionID** | Always | A unique ID assigned by the Gateway. |
| **xref** | Always | You may store the cross reference for repeat transactions.Refer to appendix A-16 for details. |
| **state** | Always | Transaction state.Refer to appendix A-14.2 for details. |
| **timestamp** | Always | Time the transaction was created or last modified. |
| **transactionUnique** | If supplied | Any value supplied in the initial request. |
| **authorisationCode** | On success | Authorisation code received from Acquirer. |
| **referralPhone** | If provided | Telephone number supplied by Acquirer to phone for voice authorisation when provided. |
| **amountReceived** | On success | Amount the Acquirer authorised. This should always be the full **amount** requested. |
| **amountRefunded** | If refund | Total amount of original SALE that has so far been refunded. Returned when **action** is REFUND\_SALE. |
| **orderRef** | If supplied | Any value supplied in the initial request. |
| **cardNumberMask** | Always | Card number masked for Merchant storage. |
| **cardTypeCode** | Always | Code identifying the type of card used.Refer to appendix A-11 for details. |
| **cardType** | Always | Description of the type of card used.Refer to appendix A-11 for details. |
| **cardSchemeCode** | Always | Code identifying the Card Scheme used.Refer to appendix A-11 for details. |
| **cardScheme** | Always | Description of the card scheme used.Refer to appendix A-11 for details. |
| **cardIssuer** | Always | Card Issues name (when known). |
| **cardIssuerCountry** | Always | Card issuing country&#39;s name (when known). |
| **cardIssuerCountryCode** | Always | Card issuing country&#39;s ISO-3166 2-letter code (when known). |
| **acquirerResponseCode** | Conditional | Response code supplied by the Acquirer, maybe prefixed with &#39;G:&#39; if the Acquirer is itself a payment Gateway. |
| **acquirerResponseMessage** | Conditional | Response message supplied the Acquirer. |
| **acquirerResponseDetails** | Conditional | Details about the Acquirer response containing any error messages and codes. This can be used together with the normal **responseCode** / **responseMessage** response fields to further determine the reason for any failure. |
| **acquirerTransactionID** | Conditional | Transaction identifier/reference used to identify the transaction in the Acquirer&#39;s system. |

Other response fields may be returned as documented elsewhere in this guide. Undocumented fields may be returned at the Gateways discretion but should not be relied upon.

The **acquirerResponse** _ **XXXX** _ fields are dependent on the Acquirer in use and are supplied for additional information only.

The response is also POSTed to any URL provided by optional **callbackURL**.

1.
# Management Requests

You can perform a management action on an existing transaction, such as a capture or cancellation, by sending a request with the required action together with the cross reference for the transaction to act on.

**Management request are supported by the Direct and Batch Integrations, they are not supported by the Hosted Integration.**

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **merchantID** | Yes | Your Gateway Merchant ID. |
| --- | --- | --- |
| **merchantPwd** | No
# 8
 | Any password used to secure this account.Refer to section 1.6.1 for details. |
| **signature** | Yes
# 9
 | Any hash used to sign this request.Refer to section 1.6.2 for details. |
| **action** | Yes | The action requested.Refer to section 1.7 for supported actions.
Possible values are: **AUTHORISE** , **CAPTURE, CANCEL, QUERY**. |
| **xref** | Yes
 | Reference to a previous transaction.Refer to appendix A-16 for details. |
| **amount** | No
# 10
 | The amount to capture or refund. |
| **callbackURL** | No | A non-public URL which will receive a copy of the transaction result by POST.The URL must be fully qualified and include at least the scheme and host components. Refer to section 1.5.7 for details. |

  1.
## Response Fields

Apart from the fields below, the response will be the same as for a new transaction but will contain the details of the existing transaction.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **responseCode** | Always | A numeric code providing the outcome of the management request.
Check **responseMessage** for more details of any error that occurred. |
| --- | --- | --- |
| **responseStatus** | Always | A numeric code providing the outcome category.
Possible values are: **0** – Authorisation Approved / No reason to decline **1** – Authorisation Declined. **2** – Authorisation Error / Transaction malformed. |
| **responseMessage** | Always | Description of above response code. |
| **action** | Always | The requested action and original action separated by a colon.For example. **CANCEL:SALE** |

Other response fields may be returned as documented elsewhere in this guide. Undocumented fields may be returned at the Gateways discretion but should not be relied upon.

The response is also POSTed to any URL provided by optional **callbackURL**.

.

1.
# Hosted Payment Page Options

You can customise the appearance of the Hosted Payment Page by sending additional fields in the request. Not all fields may be supported if you have a customised Hosted Payment Page.

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **cardNumber** | No
# 11
 | Default value for the Card number field. |
| **cardCVV** | No
# 12
 | Default value for the Card security number field. |
| **cardExpiryMonth** | No | Default value for the Card expiry month field. |
| **cardExpiryYear** | No | Default value for the Card expiry year field. |
| **cardExpiryDate** | No | Alternative to **cardExpiryMonth** / **cardExpiryYear** |
| **customerName** | No | Default value for the Cardholder&#39;s name field. |
| **customerAddress** | No | Default value for the Cardholder&#39;s address field. |
| **customerPostcode** | No | Default value for the Cardholder&#39;s postcode field. |
| **customerEmail** | No | Default value for the Cardholder&#39;s email field. |
| **customerPhone** | No | Default value for the Cardholder&#39;s phone number field. |
| **cardCVVMandatory** | No | Force a Card security number to be entered. |
| **customerAddressMandatory** | No | Force a Cardholder&#39;s address to be entered. |
| **customerPostcodeMandatory** | No | Force a Cardholder&#39;s postcode to be entered. |
| **customerEmailMandatory** | No | Force a Cardholder&#39;s email address to be entered. |
| **customerPhoneMandatory** | No | Force a Cardholder&#39;s phone number to be entered. |
| **formResponsive** | No | Request the Hosted Payment Page adjust its layout according to the browser display size etc.
Possible values are: **N** – Set to standard mode. **Y** – Set to responsive mode. |
| **formAllowCancel** | No | Request the Hosted Payment Page show a cancel button to allow the payment to be cancelled resulting in a transaction **responseCode** of 65576 **(REQUEST CANCELLED)**. |
| **paymentMethod** | No | Request the Hosted Payment Page invoke an alternative payment method on display without the need for the Customer to select it. |
| **allowedPaymentMethods** | No | Comma separated list of **paymentMethod** s supported by the Merchant to show on Hosted Payment Page where supported. |

1.
# AVS/CV2 Checking

  1.
## Background

AVS and CV2 fraud checking is available on all card transactions processed by the Gateway where supported by the Acquirer.

These fraud prevention checks are performed by the Acquirer while authorising the transaction. You can choose how to act on the outcome of the check (or even to ignore them altogether).

    1.
### AVS Checking

The Address Verification System (AVS) uses the address details that are provided by the Cardholder to verify that the address is registered to the card being used. The address and postcode are checked separately.

    1.
### CV2 Checking

CV2, CVV, or Card Verification Value is a 3-digit or 4-digit security code. The check verifies that the code is the correct one for the card used.

For most cards, the CVV is a 3 digit number to the right of the signature strip. For American Express cards, this is a 4 digit number printed, not embossed, on the front right of the card.

The AVS/CV2 checking preferences can be configured per Merchant Account within the Merchant Management System (MMS). These preferences can be overridden per transaction by sending one of the preference fields documented in section 5.3 that hold a comma separated list of the check responses that should be allowed in order to continue to completion. Responses not in the list will result in the transaction being declined with a **responseCode** of **5 (AVS/CV2 DECLINED)**.

![](RackMultipart20210427-4-13xkgeo_html_b4252721920c66af.gif)

_AVS/CV2 fraud checking is not available with every Acquirer and must be enabled on your Merchant Account before it can be used. Please contact support to find out whether your Acquirer supports it and if it can be enabled on your Merchant Account._

  1.
## Benefits and Limitations

    1.
### Benefits

- Can be enabled with just a few extra integration fields.

- The results are available immediately and returned as part of the transaction.

- The checks can be managed independently, allowing you the utmost control over how the results are used.

- The checks can be configured to decline a transaction automatically, where required.

- There are no extra costs for using AVS/CV2 checking with your transactions.

- Fully configurable within the Merchant Management System (MMS).

    1.
### Limitations

- The AVS checks are mainly supported by Visa, MasterCard and American Express in the USA, Canada and United Kingdom. Cardholders with a bank that does not support the checks might receive declines due to the lack of data.

- Because AVS only verifies the numeric portion of the address and postcode, certain anomalies such as apartment numbers and house names can cause false declines.

- The checks are meant for consumer cards. Company cards are not fully supported due to the Acquirers&#39; not having access to this information.

  1.
## Request Fields

These fields should be sent in addition to basic request fields in section 2.1.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **customerAddress** | Yes
# 13
 | For AVS checking, this must be a registered billing address for the card. |
| **customerPostCode** | Yes
# 14
 | For AVS checking, this must be a registered postcode for the card. |
| **cardCVV** | Yes
# 15
 | For CVV checking, this must be the Card Verification Value printed on the card. |
| **avscv2CheckRequired** | No
# 16
 | Is AVS/CV2 checking required for this transaction?
Possible values are: **N** – Checking is not required. **Y** – Abort if checking is not enabled. |
| **cv2CheckPref** | No4 | List of **cv2Check** response values that are to be accepted; any other value will cause the transaction to be declined.
Value is a comma separated list containing one or more of the following **: not known, not checked, matched, not matched, partially matched**. |
| **addressCheckPref** | No4 | List of **addressCheck** values that are to be accepted; any other value will cause the transaction to be declined.
Value is a comma separated list containing one or more of the following: **not known, not checked, matched, not matched, partially matched**. |
| **postcodeCheckPref** | No4 | List of **postcodeCheck** response values that are to be accepted; any other value will cause the transaction to be declined.
Value is a comma separated list containing one or more of the following: **not known, not checked, matched, not matched, partially matched**. |

##


  1.
## Response Fields

These fields will be returned in addition to the AVS/CV2 request fields in section 5.3 and the basic response fields in section 2.2.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **avscv2CheckEnabled** | Always | Is AVS/CV2 checking enabled for this Merchant Account?
Possible values are: **N** – Merchant account is not enabled. **Y** – Merchant account is enabled. |
| --- | --- | --- |
| **avscv2ResponseCode** | If checks performed | The result of the AVS/CV2 check.Refer to appendix A-2 for details. |
| **avscv2ResponseMessage** | If checks performed | The message received from the Acquiring bank, or any error message with regards to the AVS/CV2 check.Refer to appendix A-2 for details. |
| **avscv2AuthEntity** | If checks performed | Textual description of the AVS/CV2 authorising entity as described in appendix A-2.
Possible values are: **not known, merchant host, acquirer host, card scheme, issuer.** |
| **cv2Check** | If checks performed | Description of the AVS/CV2 CV2 check as described in appendix A-2.
Possible values are **: not known, not checked, matched, not matched, partially matched**. |
| **addressCheck** | If checks performed | Description of the AVS/CV2 address check as described in appendix A-2.
Possible values are **: not known, not checked, matched, not matched, partially matched**. |
| **postcodeCheck** | If checks performed | Description of the AVS/CV2 postcode check as described in appendix A-2.
Possible values are **: not known, not checked, matched, not matched, partially matched**. |

1.
# 3-D Secure Authentication

  1.
## Background

3-D Secure authentication is an additional fraud prevention scheme that is on all ecommerce card transactions processed by the Gateway, where supported by the Acquirer.

It allows the Cardholder to assign a password to their card that is then verified whenever a transaction is processed through a site that supports the use of the scheme. The addition of password protection allows extra security on transactions that are processed online.

3-D Secure stands for Three Domain Server. There are 3 parties that are involved in the 3-D Secure process:

- The company from which the purchase is being made.
- The Acquiring Bank (the bank of the company)
- VISA and Mastercard (the card issuers themselves)

The gateway supports 3-D Secure as implemented by Visa, Mastercard and American Express and marketed under the brand names of Verified by VISA (VBV), Mastercard Secure Code (MSC) and American Express (SafeKey). Implementations by JCB (J/Secure) and DCI (ProtectBuy) are not currently supported.

3-D Secure is also the only fraud prevention scheme available that offers you liability cover for transactions that are verified by the checks. This provides additional protection for transactions using the scheme as distinct from those that do not.

The 3-D Secure preferences can be configured per Merchant Account within the Merchant Management System (MMS). These preferences can be overridden per transaction by sending one of the preference fields documented in section 6.5.1, which hold a comma separated list of the check responses that should be allowed to continue to completion. Responses not in the list will result in the transaction being declined with a **responseCode** of **65803 (3DS\_NOT\_AUTHENTICATED)**.

The Gateway supports both 3-D Secure version 1.0.2 and version 2.1.0 and will use the highest version available. Version 2.2.0 will be supported in the future.

![](RackMultipart20210427-4-13xkgeo_html_b4252721920c66af.gif)

_3-D Secure is not available with all Acquirers and must be enabled on your Merchant Account before it can be used. Please contact support to find out whether your Acquirer supports it and if it can be enabled on your Merchant Account._

**3-D Secure is supported by the Hosted and Direct Integrations. It is not supported by the Batch Integration.**

  1.
## Benefits and Limitations

    1.
### Benefits

- The results are available immediately and returned as part of the transaction.

- The checks can be managed independently allowing you the utmost control over how the results are used.

- The checks can be configured to decline the transaction automatically, where required.

- If authentication is completed, liability for any subsequent fraud-related chargeback on that transaction shifts from you to the card issuer (but note the limitations below and check your Acquirer&#39;s Terms and Conditions fully on this point).

- There are no extra Gateway costs for using 3-D Secure. Your Acquirer may charge to add this onto your business account; however you may also find that your transaction charges are lower as a result of using 3-D Secure.

- Fully configurable within the Merchant Management System (MMS).

    1.
### Limitations

- Authenticated 3-D Secure transactions do not guarantee a liability shift and chargebacks can still occur. This is decided at the discretion of your Acquirer, with whom you should check its policy.

- The gateway does not support 3-D Secure for JCB or Diner&#39;s club cards.

- 3-D Secure transactions require a browser in order to display the Customer authentication dialog.

  1.
## Hosted Implementation

If your Merchant Account is set up for 3-D Secure, the Hosted Payment Page will automatically attempt to display the 3-D Secure authentication page for the Customer&#39;s bank.

The 3-D Secure authentication form is designed and controlled by the Customer&#39;s Issuing bank, but you can change the Merchant name and website address that is displayed on the form by sending the **merchantName** and/or **merchantWebsite** request fields.

Any **merchantWebsite** must be a fully qualified URL containing at least the scheme and host components.

  1.
## Direct Implementation

If your Merchant account is set up for 3-D Secure, the Gateway will require further authentication details provided by the 3-D Secure system.

    1.
### Initial Request (Verify Enrolment)

If no 3-D Secure authentication details are provided in the initial request, the Gateway will determine if the transaction is eligible for 3-D Secure by checking whether the card is enrolled in the 3-D Secure scheme.

If the Gateway determines that the transaction is not eligible for 3-D Secure, then it will continue to process it as a normal transaction without 3-D Secure, unless the **threeDSRequired** request field indicates that the transaction should be aborted instead.

To support 3-D Secure, you must pass the **threeDSRedirectURL** field in the initial request. This field must contain the complete URL to a web page on your server that the Access Control Server (ACS) will HTTP POST the authentication results back to, when the authentication has been completed.

For 3-D Secure v2 you must also provide details about the Cardholder&#39;s device, using the fields documented in the separate 3DS Integration Guide. You may also pass additional information about the transaction and Cardholder, using the **threeDSOptions** field as documented in section 6.5.4. This extra information can be sent to help facilitate fraud checks by the ACS.

If the Gateway determines that the transaction is eligible, it will respond with a **responseCode** of **65802 (3DS AUTHENTICATION REQUIRED)** and included in the response will be a **threeDSReqest** containing data that should be sent to the ACS at the **threeDSURL** using a HTTP POST request. The response will also contain a **threeDSRef** that can be used to continue the transaction when the authentication has been completed.

    1.
### Continuation Request (Check AuthenticationandAuthorise)

On completion of the 3-D Secure authentication the ACS will send the challenge results to the **threeDSRedirectURL** provided in the initial request using a HTTP POST request. The contents of this POST request should be return to the Gateway unmodified in the **threeDSResponse** field together with the **threeDSRef** received in the initial response. This new request will check the authentication results and either response with the details for a further challenge, send the transaction to the Acquirer for approval or abort the transaction depending on the authentication result and your preferences, either sent in the **threeDSPref** field or set in the Merchant Management System (MMS).

If you would like an example of a 3-D Secure integration, please refer to our sample code appendix **A-22.2.**

    1.
### Multiple Challenges and Frictionless Flow

The API supports the issuing of multiple challenges where the continuation request may indicate the requirement to perform another challenge by responding with a **responseCode** of **65802 (3DS AUTHENTICATION REQUIRED)** and including a further **threeDSReqest** , **threeDSURL** and **threeDSRef**. When this happens, these further challenge details should be treated the same as the first and POSTed to the ACS.

For 3-D Secure version 1, a single challenge is performed. However, for version 2, there may be zero, one or two challenges.

With 3-D Secure version 2, an initial device fingerprinting method might have to be invoked on the ACS, the results of which are used to determine whether the Cardholder must complete a challenge or whether a frictionless flow can be achieved where the transaction can continue unchallenged.

    1.
### Cardholder Challenge

The Cardholder challenge takes place with the Cardholder&#39;s browser, usually within an IFRAME embedded on the payment form. To start the challenge, the IFRAME should contain a HTML FORM with hidden INPUT fields storing the **threeDSRequest** name/value data. JavaScript should then be used to submit the form automatically, causing the form data to be sent via a HTTP POST to the **threeDSURL**.

The IFRAME should be of sufficient size to display the ACS challenge form. For 3-D Secure version 1, this is a minimum size of 390x400 pixels. However, version 2 allows different sizes to be specified giving the Merchant more flexibility in the design of its payment form. The required size can be set using the &#39;challengeWindowSize&#39; option, passed in the **threeDSOptions** field in the initial request.

    1.
### Device Fingerprinting Challenge

The device fingerprinting method invocation is handled in the same way as a normal Cardholder challenge, except that it can be done silently in a hidden IFRAME, invisible to the normal payment flow. This silent device fingerprinting method request can be determined by the presence of a **threeDSMethodData** element in the **threeDSRequest** data. This method should take no longer than 10 seconds and therefore if the ACS has not POSTed the results back within 10 seconds then the browser can stop waiting and the transaction can be continued as normal but the **threeDSResponse** field should be returned indicating the timeout by including a **threeDSMethodData** element with the value of &#39;timeout&#39;.

    1.
### External Authentication Request

You can choose to obtain the 3-D Secure authentication details from a third-party, in which case they should provide them as part of a standard request. If the Gateway receives valid third-party authentication details, then it will use those and not attempt to contact the 3-D Secure system itself.

  1.
## Request Fields

    1.
### Initial Request (Hosted and Direct Integration)

These fields should be sent in addition to basic request fields in section 2.1.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **merchantName** | No
# 17
 | Merchant name to use on 3DS form. |
| **merchantWebsite** | No1 | Merchant website to use on 3DS form. The website must be a fully qualified URL and include at least the scheme and host components. |
| **threeDSRequired** | No1 | Is 3DS required for this transaction?
Possible values are: **N** – 3DS is not required. **Y** – Abort if 3DS is not enabled. |
| **threeDSCheckPref** | No1 | List of **threeDSCheck** response values that are to be accepted, any other value will cause the transaction to be declined.
Value is a comma separated list containing one or more of the following values: **&#39;not known&#39;, &#39;not checked&#39;, &#39;**** not authenticated&#39;, &#39;attempted authentication&#39;, &#39;authenticated&#39;**. |
| **threeDSRedirectURL** | Yes | A URL on the Merchant&#39;s server to which the ACS can POST the challenge results, thus redirecting the challenge IFRAME to this page. |
| **threeDSOptions** | No | Further 3-D Secure options that can be used by the ACS for advance fraud checking. |

    1.
### Continuation Request (Direct Integration)

These fields may be sent alone
# 18
.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **threeDSRef** | Yes
 | The value of the **threeDSRef** field in the initial Gateway response. |
| **threeDSResponse** | Yes | The data POSTed back from the ACS when the challenge has completed. |

    1.
### External Authentication Request (Direct Integration)

These fields should be sent in addition to basic request fields from section 2.1.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **threeDSEnrolled** | If 3DS enabled | The 3DS enrolment status for the credit card.Refer to appendix A-3 for details.
Possible values are: **Y** – Enrolled. **N** - Not Enrolled. **U** - Unable to Verify. |
| **threeDSAuthenticated** | If 3DS enrolled | The 3DS authentication status for the credit card.Refer to appendix A-3 for details.
Possible values are: **Y** - Authentication Successful. **N** - Not Authenticated. **U** - Unable to Authenticate. **A** - Attempted Authentication. |
| **threeDSXID** | If 3DS authenticated | The unique identifier for the transaction in the 3DS system. |
| **threeDSECI** | If 3DS authenticated | The Electronic Commerce Indicator (ECI). |
| **threeDSCAVV** | If 3DS authenticated | The Cardholder Authentication Verification Value (CAVV). |

Note: If 3-D Secure is not enabled for the Merchant Account, then any 3-D Secure authentication fields sent in the request are ignored and the transaction is processed as normal without 3-D Secure.

    1.
### 3-D Secure 2 Options (Hosted and Direct Integration)

The following options may be sent in the **threeDSOptions** field to help customise the 3-D Secure 2 experience or can be used by the ACS for advance fraud checking. There are currently no options supported for 3-D Secure 1.

Some options are automatically initialised by the Gateway from other standard integration fields as shown in square brackets in the options description. The standard integration field should be used rather than the option, apart from the very rare circumstances where the two must have different values.

The field may be sent as a URL encoded string, JSON encoded string or an array of key/value pairs.

| **Field Name** | **Description** |
| --- | --- |
| **accountAgeIndicator** | Cardholder Account Age Indicator |
| --- | --- |
| **accountChangeDate** | Cardholder Account Change Date |
| **accountChangeIndicator** | Cardholder Account Change Indicator |
| **accountDate** | Date Cardholder account opened |
| **accountDayTransactions** | Number of account transactions in the last day |
| **accountId** | Cardholder Account Identifier |
| **accountPasswordChangeDate** | Cardholder Account Password Change Date |
| **accountPasswordChangeIndicator** | Cardholder Account Password Change Indicator |
| **accountPurchaseCount** | Cardholder Account Purchase Count |
| **accountProvisioningAttempts** | Number of account provisioning attempts in the last day |
| **accountType** | Indicates the type of account |
| **accountYearTransactions** | Number of account transactions in the last year |
| **acquirerBIN** | Acquiring institution identification code(Default on file) |
| **acquirerCountryCode** | Acquirer country code when the Acquirer country differs from the Merchant country and the Acquirer is in the EEA (this could mean that the transaction is covered by PSD2). (Default on file) |
| **acquirerMerchantID** | Acquirer-assigned merchant identifier(Default on file) |
| **acsChallengeMandatedIndicator** | ACS Challenge Mandated Indicator |
| **addressMatch** | Shipping and Billing addresses are the same |
| **authenticationECI** | Value to be passed in the authorisation message |
| **authenticationIndicator** | Indicates the type of authentication request |
| **billingAddressCity** | The city of the address[**customerTown**] |
| **billingAddressCountryCode** | The country of the address[**customerCountryCode**] |
| **billingAddressLine1** | The first line of the street address or equivalent local portion of the address[**customerAddress**] |
| **billingAddressLine2** | The second line of the street address or equivalent local portion of the address |
| **billingAddressLine3** | The third line of the street address or equivalent local portion of the address |
| **billingAddressPostcode** | The ZIP or other postcode of the address [**customerPostcode**] |
| **billingAddressState** | The state or province of the address |
| **browserAcceptHeader** | HTTP accept header sent from the Cardholder&#39;s browser[**browserAcceptContent**] |
| **browserIPAddress** | IP address of the Cardholder&#39;s browser [**remoteAddress**] |
| **browserJavaEnabledVal** | Ability of the Cardholder&#39;s browser to execute Java [**browserCapabilities**] |
| **browserJavaScriptEnabled** | Ability of the Cardholder&#39;s browser to execute JavaScript[**browserCapabilities**] |
| **browserLanguage** | The Cardholder&#39;s browser language [**browserAcceptLanguage**] |
| **browserScreenColorDepth** | The screen colour depth of the Cardholder&#39;s browser [**browserScreenResolution**] |
| **browserScreenHeight** | The screen height of the Cardholder&#39;s browser [**browserScreenResolution**] |
| **browserScreenWidth** | The screen width of the Cardholder&#39;s browser [**browserScreenResolution**] |
| **browserTimeZone** | The timezone offset of the Cardholder&#39;s browser [**browserTimeZone**] |
| **browserUserAgent** | The User-Agent provided by the Cardholder&#39;s browser[**browserUserAgent**] |
| **cardholderEmail** | The Cardholder&#39;s email address[**customerEmail**] |
| **cardholderHomePhone** | The Cardholder&#39;s home phone number[**customerPhone**] |
| **cardholderMobilePhone** | The Cardholder&#39;s mobile phone number[**customerMobile**] |
| **cardholderName** | Name of the Cardholder[**customerName**] |
| **cardholderWorkPhone** | The Cardholder&#39;s work phone number |
| **challengeWindowSize** | Challenge window size(Default 02 – 390x400) |
| **deliveryEmailAddress** | Merchandise Delivery Email Address[**deliveryEmail**] |
| **deliveryTimeframe** | Merchandise Delivery Timeframe |
| **giftCardAmount** | Total gift card(s) amount |
| **giftCardCount** | Total number of gift cards purchased |
| **giftCardCurrencyCode** | Gift Card Currency |
| **instalmentPaymentData** | Max authorisations permitted for instalment payments |
| **merchantCategoryCode** | Merchant category code[**merchantCategoryCode**] |
| **merchantCountryCode** | Country code of the merchant[**countryCode**] |
| **merchantFraudRate** | Merchant fraud rate in the EEA (all EEA card fraud divided by EEA card volumes) calculated as per PSD2 RTS. This value is sent to Mastercard only who will not calculate or validate the fraud score:Value will be a numeric value, between 1 and 99, representing the fraud rate, such as:
- 1 (less than or equal to 1 basis point [bp], which is 0.01%)
- 2 (between 1 bp +- and 6 bps)
- 3 (between 6bps +- and 13 bps)
- 4 (between 13 bps +- and 25 bps)
- 5 (greater than 25 bps)
 |
| **merchantName** | Merchant name[**merchantName**] |
| **paymentAccountAge** | Payment Account Age |
| **paymentAccountAgeIndicator** | Payment Account Age Indicator |
| **preOrderDate** | Expected date pre-ordered purchase will be available |
| **preOrderPurchaseIndicator** | Pre-Order Purchase Indicator |
| **priorAuthData** | 3DS Requestor Prior Transaction Authentication Data |
| **priorAuthMethod** | 3DS Requestor Prior Transaction Authentication Method |
| **priorAuthTimestamp** | 3DS Requestor Prior Transaction Authentication Timestamp |
| **priorReference** | 3DS Requestor Prior Transaction Reference |
| **recurringExpDate** | Recurring expiration date |
| **recurringFrequency** | The number of days between recurring payments |
| **reorderItemsIndicator** | Reorder Items Indicator |
| **reqAuthData** | 3DS Requestor Authentication Data |
| **reqAuthMethod** | 3DS Requestor Authentication Method |
| **reqAuthTimestamp** | 3DS Requestor Authentication Timestamp |
| **requestorChallengeInd** | 3DS Requestor Challenge Indicator |
| **requestorID** | Directory server assigned 3DS Requestor identifier(Default on file) |
| **requestorName** | Directory server assigned 3DS Requestor name_(Default on file)_ |
| **requestorURL** | 3DS Requestor website or customer care site[**merchantWebsite**] |
| **secureCorporatePaymentIndicator** | Indicates dedicated payment processes and procedures were used, potential secure corporate payment exemption applies. |
| **serverOperatorID** | 3DS Server identifier_(Default on file)_ |
| **serverRefNumber** | Assigned server reference number_(Default on file)_ |
| **shipAddressUsageDate** | Shipping address first usage date |
| **shipAddressUsageIndicator** | Shipping address usage indicator |
| **shipIndicator** | Shipping method indicator |
| **shipNameIndicator** | Shipping Name Indicator |
| **shippingAddressCity** | The city of the address[**deliveryTown**] |
| **shippingAddressCountryCode** | The country of the address[**deliveryCountryCode**] |
| **shippingAddressLine1** | The first line of the street address or equivalent local portion of the address[**deliveryAddress**] |
| **shippingAddressLine2** | The second line of the street address or equivalent local portion of the address |
| **shippingAddressLine3** | The third line of the street address or equivalent local portion of the address |
| **shippingAddressPostcode** | The ZIP or other postcode of the address[**deliveryPostcode**] |
| **shippingAddressState** | The state or province of the address |
| **suspiciousAccountActivity** | Suspicious account activity indicator |
| **transactionType** | Transaction Type_(Default 01 – Goods/Service Purchase)_ |
| **whitelistStatus** | Whitelist Status |

  1.
## Response Fields

    1.
### Initial Response (Direct Integration)

These fields will be returned in addition to the request fields from section 6.5.1 and the basic response fields in section 2.2.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **threeDSEnabled** | Always | Is 3DS enabled for this Merchant Account?
Possible values are: **N** – Merchant Account is not enabled. **Y** – Merchant Account is enabled. |
| --- | --- | --- |
| **threeDSXID** | If 3DS enabled | The unique identifier for the transaction in the 3DS system. |
| **threeDSVETimestamp** | If 3DS enabled | The time the card was checked for 3DS enrolment and any initial challenge determined. |
| **threeDSEnrolled** | If 3DS enabled | The 3DS enrolment status for the credit card. Refer to appendix A-3 for details.
Possible values are: **Y** – Enrolled. **N** - Not Enrolled. **U** - Unable to Verify. **E** - Error Verifying Enrolment. |
| **threeDSRef** | If 3DSenabled | Value to return in the continuation request. |
| **threeDSURL** | If 3DS enrolled | The URL of the ACS to which the challenge data should be sent via a HTTP POST request from the Cardholder&#39;s browser. |
| **threeDSRequest** | If 3DS enrolled | The challenge data that should be sent to the ACS via HTTP POST request from the Cardholder&#39;s browser. |

    1.
### Continuation Response (Direct Integration)

These fields will be returned in addition to the request fields from section 6.5.1; the initial response fields in section 6.6.1; and the basic response fields in section 2.2.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **threeDSResponse** | If 3DS enrolled | The data POSTed back from the ACS when the challenge has completed. |
| --- | --- | --- |
| **threeDSCATimestamp** | If 3DS enrolled | The time the last challenge was checked. |
| **threeDSAuthenticated** | If 3DS enrolled | The 3DS authentication status for the credit card.Refer to appendix A-3 for details.
Possible values are: **Y** - Authentication Successful. **N** - Not Authenticated. **U** - Unable to Authenticate. **A** - Attempted Authentication. **E** - Error Checking Authentication.
For 3DS version 2.2 only.
**I** – Acknowledges request not to challenge cardholder. **E** – Rejects request for authentication and requests that authorisation is not attempted. The Gateway will automatically abort the transaction, and this cannot be overridden by any Merchant preferences. |
| **threeDSECI** | If 3DS authenticated | This contains a two-digit Electronic Commerce Indicator (ECI) value, which is to be submitted in a credit card authorisation message.
This value indicates to the processor that the Customer data in the authorisation message has been authenticated.
The data contained within this property is only valid if the **threeDSAuthenticated** value is **Y** or **A**. |
| **threeDSCAVV** | If 3DS authenticated | This contains a 28-byte Base-64 encoded Cardholder Authentication Verification Value (CAVV).
The data contained within this property is only valid if the **threeDSAuthenticated** value is **Y** or **A**. |
| **threeDSErrorCode** | If 3DS error | Any error response code returned by the ACS if there is an error in determining the card&#39;s 3DS status. |
| **threeDSErrorDescription** | If 3DS error | Any error response description returned by the ACS if there is an error in determining the card&#39;s 3DS status. |

    1.
### External Authentication Response (Direct Integration)

These fields will be returned in addition to the request fields from section 6.5.3 and the basic response fields in section 2.2.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **threeDSEnabled** | Always | Is 3DS enabled for this Merchant Account?
Possible values are: **N** – Merchant Account is not enabled. **Y** – Merchant Account is enabled. |

Note: If 3-D Secure is not enabled for the Merchant Account, then any 3-D Secure authentication fields sent in the request are ignored and the transaction is processed as normal without 3-D Secure.

    1.
### Cardholder Information (Hosted and Direct Integration)

In the case of a frictionless flow, the card Issuer may sometimes wish to provide a message to the Cardholder. In this case, the **threeDSResponseMessage** will start with the text &#39;Cardholder Info: &#39; and be followed by the message from the card Issuer.

1.
# Risk Checking

  1.
## Background

The Gateway is integrated with Kount, the leading solution for digital fraud prevention.

If you have an existing account with Kount, or sign up for one, you can request that the Gateway pass your transactions to them for risk checking before they are sent to the Acquirer for authorisation.

Kount&#39;s patented fraud prevention technology combines device fingerprinting; supervised and unsupervised machine learning; a robust policy and rules engine; business intelligence tools; and a web-based case-management and investigation system.

Their team of experts can help you understand and identify the rules necessary to optimise your protection, as well as provide ongoing support. To get the most out of your investment, you may want to dedicate an individual or a team to monitor your rules and ensure they continue to work as intended.

The risk checking preferences can be configured per Merchant Account within the Merchant Management System (MMS). These preferences can be overridden per transaction by sending new preferences as documented in section 7.4.1. You must use the Kount management portal to configure your risk parameters and thresholds.

![](RackMultipart20210427-4-13xkgeo_html_c1e585bbc072d56b.gif)

_Risk checking is an advanced feature and must be enabled on your Merchant Account before it can be used. Please contact support if you wish to have it enabled._

  1.
## Benefits and Limitations

    1.
### Benefits

- The results are available immediately and returned as part of the transaction.

- The checks can be managed independently, allowing you the utmost control over how the results are used.

- The checks can be configured to decline the transaction automatically where required.

- Leverage the ability to review transactions and decide what course of action to take.

- The checks can reduce chargebacks by blocking transactions made without the Cardholder&#39;s consent that would have resulted in the Cardholder raising a chargeback to recover the fraudulent transaction amount.

- Providing enhanced risk checking increases Customer confidence and thus increases the likelihood of their making a purchase.

- Fully configurable within the Merchant Management System (MMS).

    1.
### Limitations

- Checking cannot prevent all fraudulent transactions and could even prevent some non-fraudulent transactions.

- There are additional fees associated with having a Kount account.

- You will have to spent time analysing your transactions and establishing fraud rules.

  1.
## Implementation

When risk checking is required, each transaction will be sent to Kount for checking and the result of the check will be returned in the **riskCheck** response field with one of the following values:

- **not known** - the checks could not be performed due to our error
- **not checked** - the checks could not be performed by Kount
- **approve** - the transaction is not risky and should proceed
- **decline** - the transaction is risky and should be declined
- **review** - the transaction is risky but proceed with caution
- **escalate** - the transaction is risky but proceed with caution

The actions to take for each **riskCheck** response can be configured for the Merchant Account, using the Merchant Management System. Alternatively, the preferred actions can be passed with the transaction request in the **riskCheckPref** field. The possible actions are as follows:

- **continue** - continue processing as normal
- **authonly** - authorise only, don&#39;t capture
- **decline1** - decline without reason
- **decline2** - decline with reason
- **finished** - abort with reason

The **continue** action allows the transaction to continue as normal and be sent to the Acquirer for authorisation. _A_ _ **riskCheck** _ _value of_ _ **approve** _ _will always be treated as if the action was_ _ **continue,** _ _regardless of whether the preferences say otherwise._

The **authonly** action allows the transaction to be authorised but not automatically captured giving you time to review it and decide whether you want to take the risk and capture the transaction or assume it to be fraudulent and cancel it.

The **decline1** and **decline2** actions will cause the transaction to be declined. Both decline the transaction and return with a **responseCode** of **5** ( **DECLINED** ) and a **responseMessage** of &#39;DECLINED&#39; or &#39;RISK DECLINED&#39; respectively. The first action should be used if you don&#39;t wish to alert the Customer to the fact that you suspected that their transaction was fraudulent and declined it for that reason.

The finished action will abort the transaction, causing it to return with a **responseCode** of either **65857** ( **RISK\_CHECK\_ERROR** ) or **65862** ( **RISK\_CHECK\_DECLINED** ) depending on whether an error prevented the transaction from being checked by Kount, resulting in a **riskCheck** value of &#39;not known&#39; or &#39;not checked&#39;.

The **riskCheckPref** field can be provided in the request to override any settings configured in the Merchant Management System (MMS) for this Merchant Account. The value should be a comma separated list of _result_=_actions_ pairs. If a result is not specified in the list, then an action of **decline1** is assumed. For example: &quot; **decline=decline1,review=authonly,escalate=authonly**&quot;.

  1.
## Request Fields

    1.
### Request Fields

These fields should be sent in addition to basic request fields in section 2.1.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **riskCheckRequired** | No
# 19
 | Is risk checking required for this transaction?
Possible values are: **N** – risk checking is not required. **Y** – risk checking is required. |
| **riskCheckPref** | No1 | List of **riskCheck** response values and the action to be taken for those responses.
Value is a comma separated list containing one or more of the following risk check results and associated actions:Results: **not known** , **not checked** , **approve, decline, review, escalate**.Actions: **continue** , **decline1** , **decline2** , **authonly** , **finished**. |
| **riskCheckOptions** | No | Record containing options used to customise the risk checking. Refer to section 7.4.2 for values. |

    1.
### Risk Check Options

The following options may be sent in the **riskCheckOptions** field to customise the risk checking. Where possible, the options will be initialised from standard integration fields as shown in square brackets in the option&#39;s description.

| **Field Name** | **Description** |
| --- | --- |
| **IPAD** | Customer&#39;s IPv4 address ( **X.X.X.X** ).[**remoteAddress**] |
| --- | --- |
| **MACK** | Merchants acknowledgement to ship/process the order ( **Y** or **N** ). |
| **SESS** | Unique Session ID
# 20
. Used to link to Kount&#39;s browser device data collector. |
| **ANID** | Automatic Number Identification (ANI) submitted with order. |
| **CASH** | Total cash amount in currency submitted. |
| **ORDR** | Merchant&#39;s Order Number.[**merchantOrderRef**] |
| **UNIQ** | Merchant assigned account number for Customer.[**merchantCustomerRef**] |
| **EPOC** | Date Customer account was created by merchant. |
| **NAME** | Customer&#39;s name (or name submitted with the order).[**customerName**] |
| **GENDER** | Customer&#39;s gender ( **M** or **F** )[**customerGender**] |
| **BPREMISE** | Customer&#39;s billing address premises name (UK only).[**customerCompany**] |
| **BSTREET** | Customer&#39;s billing address street (UK only).[**customerStreet** , **customerAddress**] |
| **B2A1** | Customer&#39;s billing address county/state.[**customerAddress**] |
| **B2A2** | Customer&#39;s billing address county/state.[**customerAddress2**] |
| **B2CI** | Customer&#39;s billing address county/state.[**customerTown**] |
| **B2ST** | Customer&#39;s billing address county/state.[**customerCounty**] |
| **B2PC** | Customer&#39;s billing address postcode.[**customerPostcode**] |
| **B2CC** | Customer&#39;s billing address country code.[**customerCountryCode**] |
| **EMAL** | Cardholder&#39;s email address.[**customerEmail**] |
| **B2PN** | Cardholder&#39;s phone number.[**customerPhone**] |
| **DOB** | Cardholder&#39;s date of birth.[**customerDateOfBirth** , **recipientDateOfBirth**] |
| **S2NM** | Name of person receiving the delivery.[**deliveryName**] |
| **SPREMISE** | Delivery premises name (UK only).[**deliveryCompany**] |
| **SSTREET** | Delivery street address (UK only).[**deliveryStreet** , **deliveryAddress**] |
| **S2A1** | Delivery address line 1.[**deliveryAddress**] |
| **S2A2** | Deliver address line 2.[**deliveryAddress2**] |
| **S2CI** | Delivery town/city.[**deliveryTown**] |
| **S2ST** | Delivery county/state.[**deliveryCounty**] |
| **S2PC** | Delivery postcode.[**deliveryPostcode**] |
| **S2CC** | Delivery country code.[**deliveryCountryCode**] |
| **S2EM** | Delivery email address.[**deliveryEmail**] |
| **S2PN** | Phone number of delivery location.[**deliveryPhone**] |
| **SHTP** | Shipping type.[**shippingType** , **shippingMethod**] |
| **PROD\_TYPE[**_ **XX** _**]** | Type for the _XX_th item purchased.[**items**. **XX**. **description**] |
| **PROD\_ITEM[**_ **XX** _**]** | SKU for the _XX_th item purchased.[**items.XX**. **productCode**] |
| **PROD\_DESC[**_ **XX** _**]** | Description _XX_th item purchased.[**items**. **XX**. **description**]
 |
| **PROD\_QUANT[**_ **XX** _**]** | Quantity of _XX_th item purchased.[**items**. **XX**. **quantity**] |
| **PROD\_PRICE[**_ **XX** _**]** | Unit amount for _XX_th item purchased.[**items**. **XX**. **amount**] |
| **UDF[**_ **XXXX** _**]** | User defined field _XXXX_. |

For further information on the options, refer to the Kount Integration documentation: [https://kount.github.io/docs/ris-data-submission/](https://kount.github.io/docs/ris-data-submission/).

The options should be passed as either a nested record or serialised record as described in section 1.5.8. The option names are case sensitive.

  1.
## Response Fields

These fields will be returned in addition to the risk check request fields in section 7.4 and the basic response fields in section 2.2.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **riskCheckEnabled** | Always | Is risk checking enabled for this Merchant Account?
Possible values are: **N** – Merchant account is not enabled. **Y** – Merchant account is enabled. |
| --- | --- | --- |
| **riskCheck** | If checked | The result of the risk check.
Possible values are: **approve** – ok, recommend proceed to authorisation. **decline** – probably fraudulent, recommend decline. **review** – possibly fraudulent, recommend review. **escalate** – possibly fraudulent, recommend review. |
| **riskCheckDetails** | If checked | The raw response received from Kount minus any sensitive data. |
| **riskCheckResponseCode** | If checked | Response code for the risk processing stage. |
| **riskCheckResponseMessage** | If checked | Response message for the risk processing stage. |

1.
# Payment Facilitators

  1.
## Background

If you are a Payment Facilitator (PayFac/PF) or Independent Sales Organisation (ISO), then you must send additional fields to identify yourself and your sub-merchants.

These fields must be sent with every new transaction; however, they can be cloned from an existing transaction if using an **xref** as described in appendix A-18.

![](RackMultipart20210427-4-13xkgeo_html_d1b7412550b0d170.gif)

_Payment Facilitator support is not available with every Acquirer. Please contact support to find out if your Acquirer supports it and what fields are required._

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **facilitatorID** | Yes | Your facilitator identifier as assigned by the Scheme. |
| **facilitatorName** | No
# 21
 | Your trading name as registered with the Scheme. |
| **isoID** | No1 | Your ISO identifier as assigned by the Scheme. |
| **subMerchantID** | No1 | Unique identifier assigned to this SubMerchant. |
| **merchant** _ **XXXX** _ | No1 | SubMerchant details as documented in section 17.2. |
| **statementNarrative** _ **X** _ | No1 | Statement details as documented in section 10.1.2. |

1.
# UK MCC 6012 Merchants

  1.
## Background

Every Merchant Account has a category code, also known as the MCC code, attached to it. This category code identifies the market that the payment is related to, allowing issuing banks to identify what product or service is, or was, being provided.

The merchant category code 6012 is related to payments taken for financial institutions, primarily those merchants that deal with loan payments or other credit-related activities. According to Visa, this is the most fraudulent merchant category in the UK market due to compromised debit card details being used to pay or transfer balances to other cards. Acquirers are therefore unable to confirm whether a payment is genuine, despite matching the full CVV2 with AVS.

To address this situation, issuing banks have requested additional payment information to be provided with payment requests in order to verify that the cardholder is knowingly entering into a credit-related contractual agreement with the merchant.

If you are a Merchant who has been assigned the MCC 6012 you must collect the following data for the primary recipient for each UK domestic Visa or Mastercard transaction
# 0
:

- Unique account identifier for the loan or outstanding balance funded. For example, the loan account number or the PAN (Primary Account Number) if it is a credit card balance.
- Last name (family name)
- Date of Birth (D.O.B)
- Postcode

Primary recipients are the entities (people or organisations) that have a direct relationship with the financial institution. Also, these primary recipients have agreed to the terms and conditions of the financial institution.

The new fields are not currently mandatory. However, some Acquirers are now declining transactions that are missing this information and so we recommend the information is always provided, even if your Acquirer doesn&#39;t currently mandate them.

_If you are not a UK MCC 6012 Merchant or the payment is not a UK domestic one, then you need not provide these additional authentication details though the Gateway will accept them if you do._

  1.
## Request Fields

To comply with the rules, an MCC6012 Merchant must send these additional fields:

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **merchantCategoryCode** | Yes
# 22
 | Merchant&#39;s VISA MCC (should be 6012). |
| **receiverName** | Yes | Surname only - up to 6 letters allowed. |
| **receiverAccountNo** | Yes | Account number. If a PAN is supplied only the first 6 and last 4 digits will be used. |
| **receiverDateOfBirth** | Yes | Primary recipient&#39;s date of birth. |
| **receiverPostcode** | Yes | Primary recipient&#39;s postcode.(Only the district is required but full postcodes are accepted, therefore &#39;W12 8QT&#39; or just &#39;W12&#39; are acceptable values). |

1.
# Billing Descriptor

  1.
## Background

The Billing Descriptor is how your details appear on the Cardholder&#39;s statement. It is set up with the Acquirer when the Merchant Account is opened. It is used by the Cardholder to identify who a payment was made to on a particular transaction.

Selecting a clear Billing Descriptor is important for you to avoid a chargeback when the Cardholder does not recognise the name on the transaction.

    1.
### Static Descriptor

The Static Descriptor is the descriptor agreed between yourself and your Acquirer when the Merchant Account is opened. The descriptor used is typically your trading name, location and contact phone number.

    1.
### Dynamic Descriptor

The Dynamic Descriptor is a descriptor sent with the transaction that includes details on the goods purchased or service provided, this is often used by large companies that provide many services and where the brand of the service is more familiar than the company name. The Dynamic Descriptor usually replaces any Static Descriptor on a per transaction basis.

Not all Acquirers accept Dynamic Descriptors and, for those that do, the required format varies.Often, your Merchant name is shortened to three (3) letters, followed by an asterisk (\*), followed by a short description of the service or product that the [business](https://en.wikipedia.org/wiki/Business) provides. This field typically has a limit of twenty-five (25) characters including the phone number.

For more information on whether your Acquirer allows Dynamic Descriptor and the format in which they should be sent, please contact customer support.

  1.
## Request Fields

The Dynamic Descriptor is built using one or more of the following narrative fields.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **statementNarrative1** | No | Merchant&#39;s name. |
| **statementNarrative2** | No | Product, service or other descriptive info. |

1.
# Surcharges

  1.
## Background

Surcharges are an additional charge that you can apply to the transactions that are processed through your Merchant Account.

Transactions that are sent for authorisation are subject to processing charges from your Acquirer and surcharges enable you to pass the processing charges that you incur on to your Customers.

You may, for example, be charged a fixed amount for debit card transactions and a percentage amount for credit card transactions. Consequently, the Gateway gives you the option to add both a fixed amount and percentage amount when applying a surcharge.

Surcharges should only be added to cover the processing charges that are incurred by your business. There is no Gateway imposed limit to the value of the surcharges that can be added to your transaction, although there are legal requirements. As a rule, the surcharge must not exceed the processing costs that you pay.

Some businesses apply surcharges to cover the costs that they incur; while others use the surcharges to subsidise the charges.

![](RackMultipart20210427-4-13xkgeo_html_80fc69256a5fb150.gif)

_Surcharge amounts may be limited or illegal in your jurisdiction. For example, surcharging is illegal in the European Union and many US states. It is up to you to check with your Acquirer and comply with any laws._

![](RackMultipart20210427-4-13xkgeo_html_d1b7412550b0d170.gif)

_Surcharges is an advanced feature and must be enabled on your Merchant Account before it can be used. Please contact support if you wish to have it enabled._

  1.
## Implementation

    1.
### Surcharge Rules

The **surchargeRules** field allows you to provide multiple rules specifying what surcharges should be applied to a transaction. If a transaction matches multiple rules, then the most specific rule will be used; or the first in the list.

Each surcharge rule contains the following fields:

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **cardType** | Yes | One or more 2-letter card type codes for which this rule applies (see)
The following two card type codes are also supported, in addition to the codes listed in appendix A-11: **CC** – matches any credit card. **DD** – matches any debit card. |
| **currency** | No | Zero or more 3-letter ISO-4217 currency codes. |
| **surcharge** | Yes | Surcharge amount in minor (N) or major (N.N) units or a percentage (N%). |

The surcharge rules should be passed in a sequential array of records, either as nested records or serialised records as described in section 1.5.8. The record field names are case sensitive.

    1.
### Surcharge Amounts

The Gateway doesn&#39;t usually validate that any **amount** and **grossAmount** fields are the same and that any **netAmount** , **taxAmount** and **taxRate** tally. However, in order to update them when a surcharge is applied, the amount and **grossAmount** must match and the correct **taxRate** must be provided or be able to be calculated from one or more of the other fields. Failure in this respect can cause the Gateway to return one of the following **responseCode** values; **66360** ( **INVALID\_GROSSAMOUNT** ), **66361** ( **INVALID\_NETAMOUNT** ), **66338** ( **INVALID\_TAXAMOUNT** ), **66362** ( **INVALID\_TAX\_RATE** ).

If the request contains a **surchargeAmount** field, then the Gateway will assume that surcharging has already been performed externally and will not attempt to apply any further surcharges.

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **surchargeRequired** | No
# 23
 | Is surcharging required for this transaction?
Possible values are: **N** – Surcharging is not required. **Y** – Surcharging is required. |
| **surchargeRules** | No1 | Surcharge rules as documented in section 11.2.1. |
| **surchargeAmount** | No | Surcharge amount already added. A further surcharge will not be added. |

  1.
## Response Fields

These fields will be returned in addition to the Surcharge request fields in section 11.3 and the basic response fields in section 2.2.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **surchargeEnabled** | Always | Is surcharging enabled on this Merchant Account? |
| **surchargeAmount** | Always | Surcharge amount added. |
| **amount** | Always | Original request value with additional surcharge. |
| **grossAmount** | Conditional | Original request value adjusted for new **amount**. |
| **netAmount** | Conditional | Original request value adjusted for new **amount**. |
| **taxAmount** | Conditional | Original request value adjusted for new **amount**. |

1.
# Receipts and Notifications

  1.
## Background

The Gateway can be configured to email transaction receipts automatically to the Customer and notifications to the Merchant.

    1.
### Customer Email Receipts

The Customer can be emailed a transaction receipt automatically each time a transaction is processed by the Gateway. Receipts are sent at the time the transaction is authorised and only for transactions where the Acquirer has approved the authorisation. Receipts are not sent for declined or referred authorisations or aborted transactions.

This functionality is enabled globally on a per Merchant Account basis using the Merchant Management System (MMS). This global setting can also be overridden per transaction if required, using the **customerReceiptsRequired** field.

Customer receipts require the Customer to provide an email address; if no email address is provided using the **customerEmail** field, then no receipt will be sent.

    1.
### Merchant Email Notifications

You can be automatically emailed a transaction notification each time a transaction is processed by the Gateway. Notifications are sent at the time the transaction is authorised and only for transactions where the Acquirer approved, declined or referred the authorisation. Notifications are not sent for aborted transactions.

This functionality is enabled globally on a per Merchant Account basis, using the Merchant Management System (MMS). This global setting can also be overridden per transaction if required, using the **notifyEmailRequired** field.

  1.
## Request Fields

    1.
### General Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **customerReceiptsRequired** | No
# 24
 | Send a Customer receipt if possible.
Possible values are: **N** – Don&#39;t send a receipt. **Y** – Send if Customer&#39;s email provided. |
| **customerEmail** | No | Customer&#39;s email address. |
| **notifyEmailRequired** | No | Send a notification email if possible.
Possible values are: **N** – Don&#39;t send a notification. **Y** – Send if notification email provided. |
| **notifyEmail** | No | Merchant&#39;s notification email address. |

    1.
###
  1.
## Response Fields

The request fields for the required receipts and notifications are returned together with the appropriate fields from the following:

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **customerReceiptsResponseCod**** e** | If required | Result of sending email to Customer. |
| **customerReceiptsResponseMessag**** e** | If required | Description of above response code. |
| **notifyEmailResponseCode** | If required | Result of sending email to Merchant.
 |
| **notifyEmailResponseMessag**** e** | If required | Description of above response code. |

1.
#

1.
# Recurring Transaction Agreements

  1.
## Background

A Recurring Transaction Agreement (RTA) is used to request that the Gateway should perform repeat payments on your behalf, using pre-agreed amounts and schedules.

An RTA can be configured easily and quickly, using the Merchant Management System (MMS). An RTA can also be set up while performing the initial transaction request, by including the integration request fields described in section 13.3. The RTA is only set up in the transaction results in a successful payment authorisation.

The transaction should be either SALE or VERIFY transaction and the **rtAgreementType** field should be provided to indicate the type of Continuous Authority/Repeat Billing agreed between you and your Customer. This will dictate whether the subsequent repeat transactions are taken as part of a CPA agreement or as just standard MOTO transactions.

Merchants who use this system to implement billing or subscription type payments are encouraged to use Continuous Authority (CA) transactions to comply with Card Payment Scheme practices. _Your Acquirer may refuse to accept the recurring transactions if they are not subject to an agreement between yourself and your Customer._

Refer to appendix A-17 for more information on the different types of repeat or recurring transactions.

  1.
## Scheduling

There are two different types of scheduling available when requesting the Gateway to take recurring transactions automatically on the Merchant&#39;s behalf. In addition, a start date can be provided to allow for a recurring subscription with an initial free trial period.

    1.
### Fixed Scheduling

Fixed scheduling causes the subsequent transaction to be taken at fixed intervals of time and for fixed amounts. A different initial date and amount or final date and amount can be provided for use when the agreed payment term or amount doesn&#39;t exactly divide by the fixed time intervals.

Fixed scheduling is specified by providing an **rtScheduleType** field with a value of &#39;fixed&#39; and providing the **rtCycleDuration** , **rtCycleDuration** and **rtCycleCount** fields to define the interval at which transactions should be taken and the number of transactions to take.

An **rtCycleCount** field value of 0 can be provided to indicate that transactions should be taken ad-infinitum until the RTA is stopped.

    1.
### Variable Scheduling

Variable scheduling causes the subsequent transaction to be taken on prespecified dates and for prespecified amounts.

Variable scheduling is specified by providing an **rtScheduleType** field with a value of &#39;variable&#39; and providing the **rtSchedule** field with a value containing an array of one or more schedule records.

Each schedule record must contain the following fields:

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **date** | Yes | Date on which to take a payment. |
| **amount** | Yes | Amount to take on the provided date. |

The schedule records should be passed in a sequential array of records, either as nested records or serialised records as described in section 1.5.8. The record field names are case sensitive.

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **rtName** | No | Free format short name for the agreement. |
| **rtDescription** | No | Free format longer description for the agreement. |
| **rtPolicyRef** | No | Merchant Reference (MPRN). |
| **rtAgreementType** | No | Recurring transaction agreement type. Indicates the type of Continuous Payment Authority or Repeat Billing agreement made with the Cardholder.Possible values are:\&lt;not provided\&gt; - no CPA agreed. **recurring** – recurring type CPA agreed. **instalment** – instalment type CPA agreed. |
| **rtMerchantID** | No | Merchant ID to use for the recurring transactions (defaults to **merchantID** ). |
| **rtStartDate** | No | Start date of agreement (defaults to date received). |
| **rtScheduleType** | No | Schedule type.
Possible values are: **fixed** – fixed interval schedule (default). **variable** – variable interval schedule. |
| **rtSchedule** | Yes
# 25
 | Nested array or serialised string containing payment schedule information as per section 13.2.2. |
| **rtInitialDate** | No
# 26
 | Date of initial payment (defaults to **rtStartDate** ). |
| **rtInitialAmount** | No2 | Amount of initial payment (defaults to **rtCycleAmount** ). |
| **rtFinalDate** | No2 | Date of final payment. |
| **rtFinalAmount** | No2 | Amount of final payment (defaults to **rtCycleAmount** ). |
| **rtCycleAmount** | No2 | Amount per cycle (defaults to **amount** ). |
| **rtCycleDuration** | Yes2 | Length of each cycle in **rtCycleDurationUnit** units. |
| **rtCycleDurationUnit** | Yes2 | Cycle duration unit.One of: **day** , **week** , **month** or **year**. |
| **rtCycleCount** | Yes2 | Number of cycles to repeat (zero to repeat forever). |
| **rtMerchantData** | No | Free format Merchant data field. |

  1.
## Response Fields

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **rtID** | Always | Recurring Transaction Agreement ID. |
| **rtResponseCode** | Always | Result of setting up RT Agreement. |
| **rtResponseMessage** | Always | Description of above response code. |

1.
# Duplicate Transaction Checking

  1.
## Background

Duplicate transaction checking prevents transaction requests from accidentally processing more than once. This can happen if a Customer refreshes your checkout page or clicks a button that issues a new transaction request repeatedly in short succession. While duplicate checking can help prevent repeat transactions from going through, we recommend talking with your developers to see whether changes can be made to your form to reduce the likelihood of this occurring (e.g. disabling the Submit button after it has been clicked).

  1.
## Implementation

To help prevent duplicate transactions, each transaction can specify a time window during which previous transactions will be checked to see whether they could be possible duplicates.

This time window is specified using the **duplicateDelay** field. The value for this field can range from 0 to 9999 seconds (approximately 2 ¾ hours).

If the transaction request does not include the **duplicateDelay** field or specifies a value of zero, then a default delay of 300 seconds (5 minutes) is used.

The following fields are used in transaction comparison and must be the same for a transaction to be regarded as a duplicate:

- **merchantID**
- **action**
- **type**
- **amount**
- **transactionUnique**
- **currencyCode**
- **xref** (if provided in lieu of card details)
- **cardNumber** (may be specified indirectly via cross reference)

If a transaction is regarded as being a duplicate, then a **responseCode** of **65554 (REQUEST DUPLICATE**) will be returned.

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **duplicateDelay** | No | Duplicate transaction time window in seconds. **Numeric value between 0 and 9999.** |

1.
# Purchase Data

  1.
## Background

The Gateway can be sent advanced purchase information with each transaction, where required.

The Gateway provides several fields that you can use to store advanced purchase information about the transaction, including details on individual items purchased. These fields are only sent to the Acquirer if needed. The stored data can be obtained by sending a QUERY request.

The details may also be used for advanced purposes, such as displaying shopping cart information on the MasterPass Wallet and PayPal Checkout.

    1.
### American Express Purchases

Purchases using American Express cards will send a subset of this information to the card scheme as appropriate.

With American Express, you can provide tax _ **or** _ discount reason (but not both). If **taxAmount** is provided, then **taxReason** is used; if **discountAmount** is provided, then **discountAmount** is used. If both are provided, then **taxReason** is used.

Only the first six line item details are sent to American Express and then only the **item** _ **XX** _ **Description** , **item** _ **XX** _ **Quantity** and **item** _ **XX** _ **GrossAmount** fields are sent.

    1.
### Purchase Orders

These fields together with other advanced fields, as detailed in section 16, can be used to send full information relating to a purchase order and related invoice indicating types; quantities; and agreed prices for products or services. Details on the supplier; shipping; delivery can also be included.

_At present, this information is not sent to the Acquirer, unless needed, but future enhancements to the Gateway may include sending such information as Level 2 or 3 Purchasing data as defined by the relevant card schemes._

  1.
## Request Fields

The following request fields may be sent to provide more information on the breakdown of the purchase amount:

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **grossAmount** | No | Total gross amount of sale. |
| **netAmount** | No | Total net amount of sale. |
| **taxRate** | No | Total tax rate (percentage). |
| **taxAmount** | No
# 27
 | Total tax amount of sale. |
| **taxReason** | No1 | Reason for above tax (e.g. VAT). |
| **discountAmount** | No1 | Total discount amount of sale. |
| **discountReason** | No1 | Reason for above discount. |
| **handlingAmount** | No | Handling costs. |
| **insuranceAmount** | No | Insurance costs. |

The following request fields may be sent to provide more information on the purchased items:

| **item** _ **XX** _ **Amount**** 1** | No | Amount for _XX_th item purchased. |
| --- | --- | --- |
| **item** _ **XX** _ **Description**
 **# 28** | No | Description of _XX_th item purchased. |
| **item** _ **XX** _ **Quantity**** 1** | No | Quantity of _XX_th item purchased. |
| **item** _ **XX** _ **GrossAmount**** 1** | No | Gross amount for _XX_th item purchased. |
| **item** _ **XX** _ **Net**** Amount ****1** | No | Net amount for _XX_th item purchased. |
| **item** _ **XX** _ **TaxAmount**** 1** | No | Tax amount for _XX_th item purchased. |
| **item** _ **XX** _ **TaxRate**** 1** | No | Total tax rate for _XX_th item purchased. |
| **item** _ **XX** _ **TaxReason**** 1** | No | Tax reason for _XX_th item purchased. |
| **item** _ **XX** _ **DiscountAmount**** 1** | No | Total discount for _XX_th item purchased. |
| **item** _ **XX** _ **DiscountReason**** 1** | No | Discount reason for _XX_th item purchased. |
| **item** _ **XX** _ **ProductCode**** 1** | No | Product code for _XX_th item purchased. |
| **itemXXProductURL**** 1** | No | Shopping cart URL for XXth item purchased. |
| **item** _ **XX** _ **CommodityCode**** 1** | No | Commodity code for _XX_th item purchased. |
| **item** _ **XX** _ **UnitOfMeasure**** 1** | No | Unit of measure for _XX_th item purchased. |
| **item** _ **XX** _ **UnitAmount**** 1** | No | Unit amount for _XX_th item purchased. |
| **itemXXImageUrl**** 1** | No | Image of XXth item purchased. |
| **itemXXSize**** 1** | No | Size of XXth item purchased in the format &#39;LengthxWidthxHeight Unit&#39;. |
| **itemXXWeight**** 1** | No | Weight of XXth item purchased in the format &#39;Weight Unit&#39;. |
| **Items** | No | Nested line item records (see below). |

1.

1. The purchased items can be passed as either individual **item** _ **XXField** _ fields; or as a single **items** field whose value is a sequential array of nested records as described in section 1.5.8.

Both formats cannot be used together. The presence of an **items** field will cause the Gateway to ignore any individual fields.

The Gateway does not currently support **items** to be given as a serialised array of records.

Note: no attempt is made to check that any gross, net and tax amounts are correct with respect to each other. It is the sender&#39;s responsibility to ensure alternative amount formats are correct.

Line item fields can either be sent &#39;flat&#39; using field names containing the item row number as a sequential number from 1 to 99; or be sent using nested arrays of the form **items[**_ **XX** _**][**_ **field** _**]** where _ **XX** _ is the row number from 1 to 99 and _ **field** _ is the field name from the above table without the **item** _ **XX** _ prefix and starting with a lowercase first letter. For example, the tax rate for item 5 can be sent either as **item5TaxRate;** or as **items[5][taxRate]**. The two formats should not be mixed. If a request field of **items** is seen, then the &#39;flat&#39; fields are ignored.

1.
# Custom Data

You may send arbitrary data with the request by appending extra fields, which will be returned unmodified in the response. These extra fields are merely &#39;echoed&#39; back and not stored by the Gateway.

Caution should be made to ensure that any extra fields do not match any currently documented fields or possible future fields. One way to do this is to prefix the field names with a value unique to you, the Merchant.

You can also use the **merchantData** field to store custom data with the transaction. This stored data can then be retrieved at a later date, using a QUERY request. Associative data can be serialised using the notation **merchantData[name]=value**; or, alternatively, a JSON or XML encoded string could be stored.

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **merchantData** | No | Arbitrary data to be stored together with this transaction. |

1.
# Advanced Data

The Gateway provides a number of fields that you can use to store information about the transaction. These fields are only sent to the Acquirer if needed. The stored data can be obtained by sending a QUERY request.

  1.
## Customer Request Fields

These fields can be used to store details about the Customer and any relationship between the Customer and Merchant such as any purchase order raised.

If AVS checks are in use, then the Customer and Cardholder are assumed to be the same person and the address and postcode fields are taken as being the registered billing address of the card.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **customerName** | No | Cardholder&#39;s name. |
 |
| --- | --- | --- | --- |
| **customerCompany** | No | Cardholder&#39;s company (if applicable). |
 |
| **customerAddress** | No
# 29
 | Cardholder&#39;s address. |
 |
| **customerPostcode** | No1 | Cardholder&#39;s postcode. |
 |
| **customerTown** | No | Cardholder&#39;s town/city. |
 |
| **customerCounty** | No | Cardholder&#39;s county/province. |
 |
| **customerCountryCode** | No | Cardholder&#39;s country. |
 |
| **customerPhone** | No | Cardholder&#39;s phone number. |
 |
| **customerMobile** | No | Cardholder&#39;s mobile phone number. |
 |
| **customerFax** | No | Cardholder&#39;s fax number. |
 |
| **customerEmail** | No | Cardholder&#39;s email address. |
 |
| **customerOrderRef** | No | Customer&#39;s reference for this order(Purchase Order Reference). |
 |
| **customerMerchantRef** | No | Customer&#39;s reference for the Merchant. |
 |
| **customerTaxRef** | No | Customer&#39;s tax reference number. |
 |

  1.
##
  2. Merchant Request Fields

These fields can be used to store details about the Merchant and any relationship between the Merchant and Customer such as any invoice reference.

| **Field Name** | **Mandatory?** | **Description/Value** |
| --- | --- | --- |
| **merchantName** | No | Merchant&#39;s contact name. |
| **merchantCompany** | No | Merchant&#39;s company name. |
| **merchantAddress** | No | Merchant&#39;s contact address. |
| **merchantTown** | No | Merchant&#39;s contact town/city. |
| **merchantCounty** | No | Merchant&#39;s contact county. |
| **merchantPostcode** | No | Merchant&#39;s contact postcode. |
| **merchantCountryCode** | No | Merchant&#39;s contact country. |
| **merchantPhone** | No | Merchant&#39;s phone. |
| **merchantMobile** | No | Merchant&#39;s mobile phone number. |
| **merchantFax** | No | Merchant&#39;s fax number. |
| **merchantEmail** | No | Merchant&#39;s email address. |
| **merchantWebsite** | No | Merchant&#39;s website. The website must be a fully qualified URL and include at least the scheme and host components. |
| **merchantOrderRef** | No | Merchant&#39;s reference for this order(Invoice/Sales Reference). |
| **merchantCustomerRef** | No | Merchant&#39;s reference for the Customer. |
| **merchantTaxRef** | No | Merchant&#39;s tax reference number. |
| **merchantOriginalOrderRef** | No | Reference to a back order. |
| **merchantCategoryCode** | No | Scheme assigned Merchant Category Code (MCC). |

  1.
## Supplier Request Fields

These fields can be used to store details about the Supplier address. This is where any purchased goods are being supplied from if different from the Merchant&#39;s address.

| **Field Name** | **Mandatory?** | **Description/Value** |
| --- | --- | --- |
| **supplierName** | No | Supplier&#39;s contact name. |
| **supplierCompany** | No | Supplier&#39;s company name. |
| **supplierAddress** | No | Supplier&#39;s contact address. |
| **supplierTown** | No | Supplier&#39;s contact town/city. |
| **supplierCounty** | No | Supplier&#39;s contact county. |
| **supplierPostcode** | No | Supplier&#39;s contact postcode. |
| **supplierCountryCode** | No | Supplier&#39;s contact country. |
| **supplierPhone** | No | Supplier&#39;s phone. |
| **supplierMobile** | No | Supplier&#39;s mobile phone number. |
| **supplierFax** | No | Supplier&#39;s fax number. |
| **supplierEmail** | No | Supplier&#39;s email address. |

  1.
## Delivery Request Fields

These fields can be used to store details about the delivery address. This is where any purchased goods are being delivered to if different from the Customer&#39;s address.

| **Field Name** | **Mandatory?** | **Description/Value** |
| --- | --- | --- |
| **deliveryName** | No | Name of person receiving the delivery. |
| **deliveryCompany** | No | Name of company receiving the delivery. |
| **deliveryAddress** | No | Delivery address. |
| **deliveryTown** | No | Delivery town/city. |
| **deliveryCounty** | No | Delivery county. |
| **deliveryPostcode** | No | Delivery postcode. |
| **deliveryCountryCode** | No | Delivery country. |
| **deliveryPhone** | No | Phone number of delivery location. |
| **deliveryMobile** | No | Mobile phone number of delivery location. |
| **deliveryFax** | No | Fax number of delivery location. |
| **deliveryEmail** | No | Delivery email address. |

  1.
## Receiver Request Fields

These fields can be used to store details about the recipient of the purchased goods where different from the Customer&#39;s and Delivery details. It is most commonly used by Financial Institutions (MCC 6012 Merchants) who need to record the primary recipient of a loan.

| **Field Name** | **Mandatory?** | **Description/Value** |
| --- | --- | --- |
| **receiverName** | No | Receiver&#39;s contact name. |
| **receiverCompany** | No | Receiver&#39;s company name. |
| **receiverAddress** | No | Receiver&#39;s contact address. |
| **receiverTown** | No | Receiver&#39;s contact town/city. |
| **receiverCounty** | No | Receiver&#39;s contact county. |
| **receiverPostcode** | No | Receiver&#39;s contact postcode. |
| **receiverCountryCode** | No | Receiver&#39;s contact country. |
| **receiverPhone** | No | Receiver&#39;s phone. |
| **receiverMobile** | No | Receiver&#39;s mobile phone number. |
| **receiverFax** | No | Receiver&#39;s fax number. |
| **receiverEmail** | No | Receiver&#39;s email address. |
| **receiverAccountNo** | No | Receiver&#39;s account number. |
| **receiverDateOfBirth** | No | Receiver&#39;s date of birth. |

  1.
## Shipping Request Fields

These fields can be used to store details about the shipping method and costs.

| **Field Name** | **Mandatory?** | **Description/Value** |
| --- | --- | --- |
| **shippingTrackingRef** | No | Shipping tracking reference. |
| **shippingMethod** | No | Shipping method (e.g. Courier, Post, etc.). |
| **shippingAmount** | No | Cost of shipping. |
| **shippingGrossAmount** | No | Gross cost of shipping. |
| **shippingNetAmount** | No | Net cost of shipping. |
| **shippingTaxRate** | No | Tax rate as percentage to 2 decimal places. |
| **shippingTaxAmount** | No | Tax cost of shipping. |
| **shippingTaxReason** | No | Tax reason (e.g. VAT). |
| **shippingDiscountAmount** | No | Discount on shipping. |
| **shippingDiscountReason** | No | Reason for discount. |

Note: No attempt is made to check that any gross, net and tax amounts are correct with respect to each other. It is the sender&#39;s responsibility to ensure alternative amount formats are correct.

##


1.
# Gateway Wallet

  1.
## Background

The Gateway supports an internal digital Wallet that is available to all Merchants using the Gateway.

The Gateway allows you to store your Customer&#39;s payment card, billing and delivery address details and other information securely encrypted in its internal Wallet. You can then allow your Customer to select from stored payment cards to check out faster on your website.

Management of this Wallet is done using the Gateway&#39;s REST API. However, you can use the Hosted, Direct or Batch Integrations to perform transactions, using cards and addresses stored in the Wallet; or to store new cards and address used with successful transactions.

  1.
## Benefits and Limitations

    1.
### Benefits

- Details can be used from or added to the Wallet with just a few extra integration fields.

- Customers can select from previously stored details, making the checkout process more streamlined, resulting in fewer abandoned carts and thus increasing sales.

- Compatible with existing card base fraud solutions such as Address Verification Service (AVS), 3-D Secure and third-party fraud providers.

- There are no extra costs to use the internal Gateway Wallet.

- The Wallet transactions are controlled within the Merchant Management System (MMS) in the same manner as normal card transactions.

    1.
### Limitations

- The payment details are stored internally by the Gateway and not available for use with other Gateway Merchants or other payment gateways.

  1.
## Hosted Implementation

Customers who have payment details already saved will have the option to select from those details rather than having to renter them. Customers will also have the option to delete stored details1

The details are only saved if the transaction is successful, ensuring that the Wallet is not filled up with invalid payment details.

The details requiring to be stored in the Wallet are validated when the transaction is performed, prior to any authorisation with the Acquirer. If any of the details are invalid, then the transaction will be aborted with a **responseCode** of **66304** ( **INVALID\_REQUEST** ) and a **responseMessage** indicating which data could not be stored in the Wallet. Any failure that occurs post authorisation will not abort the transaction but will be available in the appropriate _ **xxxx** _ **StoreResponseCode** response fields.

The **walletOwnerRef** field can be used to assign a unique Customer reference to the Wallet, allowing you to identify which of your Customers owns the Wallet. This could be the Customer reference you use within your own Customer accounts or Shopping Cart software. You must ensure that this value is less than 50 characters, or the transaction will be aborted with a **responseCode** of **65xxx** ( **INVALID\_WALLETCUSTOMERREF** ).

  1.
## Direct Implementation

If a transaction is sent to the Direct Integration, then with the addition of a few extra integration fields, it can be instructed to use payment details stored in the Wallet and/or store the used payment details.

Using stored payment details is similar to performing cross-referenced transactions where the payment details are cloned from a previous transaction1. However, in this case the payment details are taken from the Wallet and not a previous transaction.

The details are only saved if the transaction is successful, ensuring that the Wallet is not filled up with invalid payment details.

The details requiring to be stored in the Wallet are validated when the transaction is performed prior to any authorisation with the Acquirer. If any of the details are invalid, then the transaction will be aborted with a **responseCode** of **66304** ( **INVALID\_REQUEST** ) and a **responseMessage** indicating which data could not be stored in the Wallet. Any failure that occurs post authorisation will not abort the transaction but will be available in the appropriate _ **xxxx** _ **StoreResponseCode** response fields.

The **walletOwnerRef** field can be used to assign a unique Customer reference to the Wallet allowing you to identify which of your Customers owns the Wallet. This could be the Customer reference you use within your own Customer accounts or Shopping Cart software. You must ensure that this value is less than 50 characters, or the transaction will be aborted with a **responseCode** of **65xxx** ( **INVALID\_WALLETCUSTOMERREF** ).

  1.
## Request Fields

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **walletID** | No | Identifier for an existing Wallet to use. |
| **walletName** | No | Name for any new Wallet created. |
| **walletDescription** | No | Description for any new Wallet created. |
| **walletOwnerRef** | No | Owner Reference for any new Wallet created. |
| **walletData** | No | Merchant Data for any new Wallet created. |
| **walletStore** | No | Request that all payment details be stored in the Wallet. A new Wallet will be created if needed.
Possible values are: **Y** - store all payment details. **N** - store details according to their **xxxStore** value. |
| **cardID** | No | Identifier for an existing card stored in a Wallet. |
| **cardName** | No | Name for any new card stored. |
| **cardDescription** | No | Description for any new card stored. |
| **cardData** | No | Merchant Data for any new card stored. |
| **cardStore** | No | Request that the payment card details be stored in the Wallet. A new Wallet will be created if needed.
Possible values are: **Y** - store the card details. **N** - do not store the card details. |
| **customerAddressID** | No | Identifier for an existing address stored in a Wallet. |
| **customerAddressName** | No | Name for any new address stored. |
| **customerAddressDescription** | No | Description for any new address stored. |
| **customerAddressData** | No | Merchant Data for any new address stored. |
| **customerAddressStore** | No | Request that the customer address details be stored in the Wallet. A new Wallet will be created if needed.
Possible values are: **Y** - store the customer address details. **N** - do not store the customer address details. |
| **deliveryAddressID** | No | Identifier for an existing address stored in a Wallet. |
| **deliveryAddressName** | No | Name for any new address stored. |
| **deliveryAddressDescription** | No | Description for any new address stored. |
| **deliveryAddressData** | No | Merchant Data for any new address stored. |
| **deliveryAddressStore** | No | Request that the delivery address details be stored in the Wallet. A new Wallet will be created if needed.
Possible values are: **Y** - store the delivery address details. **N** - do not store the delivery address details. |

  1.
## Response Fields

These fields will be returned in addition to the request fields from section.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **walletStoreResponseCode** | No | Result of creating or updating the Wallet details.Refer to appendix A-1 for details. |
| **walletStoreResponseMessage** | No | Description of above response code. |
| **cardStoreResponseCode** | No | Result of creating or updating the card details.Refer to appendix A-1 for details. |
| **cardStoreResponseMessage** | No | Description of above response code. |
| **customerAddresStoreResponseCod**** e** | No | Result of creating or updating the address details.Refer to appendix A-1 for details. |
| **customerAddressStoreResponseMessag**** e** | No | Description of above response code. |
| **deliveryAddressStoreResponseCod**** e** | No | Result of creating or updating the address details.Refer to appendix A-1 for details. |
| **deliveryAddressStoreResponseMessag**** e** | No | Description of above response code. |

If new items are stored in the Wallet, then their identifiers will be returned in the appropriate **walletID** , **cardID** , **customerAddressID** and **deliveryAddressID** together with any values provided for or assigned by default to the other item fields.

Failure to store any of the details in the Wallet will be reported using the appropriate _ **xxxx** _ **StoreResponseCode** response field.

1.
# Masterpass Wallet

  1.
## Background

Masterpass is a digital wallet from Mastercard that is available to all Merchants using the Gateway.

It allows customers to store their payment and shipping information in one central, secure location. With Masterpass, customers can shop, click, and check out faster on your website.

Masterpass transactions process and settle just like credit card transactions. You can identify Masterpass transactions in the Merchant Management System by their unique payment type logo, which includes the credit card brand name at the bottom.

There are no additional fees for processing Masterpass transactions – pricing for Masterpass is the same as your other credit card transactions.

Masterpass versions 6 and 7 are supported by the Gateway.

![](RackMultipart20210427-4-13xkgeo_html_d1b7412550b0d170.gif)

_Masterpass has upgraded to Mastercard&#39;s new guest checkout option and Customers can no longer sign up. As such this integration is subject to change._

![](RackMultipart20210427-4-13xkgeo_html_d1b7412550b0d170.gif)

_Masterpass is an advanced feature and must be enabled on your Merchant Account before it can be used. Please contact support if you wish to have it enabled._

**Masterpass is supported by the Hosted and Direct Integrations. It is not supported by the Batch Integration.**

  1.
## Benefits and Limitations

    1.
### Benefits

- The Wallet details are stored externally to the Gateway and available with any third-party Checkout that supports Masterpass.

- Customers can select from previously stored details, making the checkout process more streamlined, resulting in fewer abandoned carts and thus increasing sales.

- Compatible with existing card base fraud solutions such as Address Verification Service (AVS), 3-D Secure and third-party fraud providers.

- There are no extra costs to add Masterpass to your Gateway account.

- The Masterpass transactions are controlled within the Merchant Management System (MMS) in the same manner as normal card transactions.

    1.
### Limitations

- Your Customer will need a Masterpass Wallet with some stored card details in order to make full use of this payment method.

- Repeat transactions using the retrieved payment details are supported but may require permission from Masterpass.

  1.
## Hosted Implementation

If a transaction is sent to the Hosted Integration using a **merchantID** that has Masterpass enabled, then the Hosted Payment Page will display a MasterPass payment button that, when clicked, will open the Masterpass Wallet and allow the Customer to select their payment card and address details.

To customise the Masterpass Wallet experience, you may send various options in the masterPassCheckoutOptions field in your initial request.

Additional information available from the Masterpass Wallet will be made available in the masterPassCheckoutDetails response field.

_Note: Custom Hosted Payment Pages might not support the displaying of the Masterpass button. If you have a custom page that doesn&#39;t support this, then please contact support to have your Hosted Payment Page upgraded._

  1.
## Direct Implementation

Masterpass transactions require you to display the Masterpass Wallet to your Customer as part of the transaction flow. The transaction must be done in two stages, with the Wallet being displayed between the stages. They can optionally also be done in three stages, allowing you to display an order confirmation after the Wallet and before authorising the transaction. You can change the amount at this stage to allow for shipping costs when you know the confirmed delivery address the Customer selected from the Wallet.

    1.
### Initial Request (Checkout Preparation)

To request that a transaction be processed using details selected from the Customer&#39;s Masterpass Wallet, the request must contain a **paymentMethod** of &#39;masterpass&#39; and a **masterPassCallbackURL** containing the URL of a page on your server to return to when the Wallet is closed. In addition, you may send **masterPassCheckoutOptions** to customise the Wallet experience. When the Gateway receives these two fields, assuming there are no other errors with the request, it will attempt to find a suitable Masterpass enabled Merchant Account in the current account mapping group (refer to appendix A-6).

If the Gateway is unable to find a suitable account, then the transaction will be aborted and it will respond with a **responseCode** of **65569 (MASTERPASS\_NOT\_SUPPORTED)**.

Otherwise the Gateway will respond with a **responseCode** of **65572 (MASTERPASS\_CHECKOUT REQUIRED)** and the response will include a **masterPassCheckoutURL** field containing the URL required to load the Masterpass Wallet and a **masterPassCheckoutOptions** containing any data required to be sent to the Wallet. The response will also contain a unique **masterPassData** field that must be echoed back in the continuation requests. No transaction will have been created by the Gateway at this stage and this request will not appear in the Merchant Management System.

At this point your server must redirect the Customer&#39;s browser to the Masterpass Wallet at the provided **masterPassCheckoutURL**. Alternatively, the **masterPassCheckoutURL** can be used in conjunction with the Masterpass JavaScript code to implement a lightbox style Wallet that allows the Merchants website to remain visible in the background. Further details on how to use the Masterpass JavaScript SDK can be obtained from Masterpass.

    1.
### Continuation Request (Checkout Details and Authorise)

On completion of the Masterpass Wallet, it will redirect the Customer&#39;s browser to the **masterPassCallbackURL** provided, including an OAuth token, OAuth verifier and status URL parameters. If the checkout was successful, the status will be &#39;success&#39;. Alternatively, if the checkout was cancelled the status will be &#39;cancel&#39;.

These URL parameters should be sent to the Gateway in the **masterPassToken** , **masterPassVerifier** and **masterPassStatus** fields of a new request. The new request must contain the **masterPassData** received in the initial response. This new request will retrieve the Customer&#39;s chosen payment and delivery details from Masterpass and then send the transaction to the Acquirer for authorisation, returning the result similarly to a normal card-based authorisation transaction.

_If the continuation request contains any details that would normally be read from the Masterpass Wallet, then these will take precedence and overwrite the Wallet details. Note: in such cases, the transaction will no longer class as being a Masterpass transaction and will be treated by the Acquirers as if the Wallet was not used._

If the chosen details cannot be retrieved or if the **masterPassStatus** field indicated that the Wallet was cancelled, then the Gateway will return a **responseCode** of **65570 (MASTERPASS\_CHECKOUT\_FAILURE).**

    1.
### Separate Checkout Details and Authorisation Requests

You can choose to obtain the Wallet details before sending the transaction for authorisation by sending the **masterPassOnly** field in the above continuation request. If this field is sent with a value of &#39;Y&#39;, then the Gateway will load the Wallet details and then return them to you without sending the request for authorisation. You can then display them and/or adjust the amount, for example, according to delivery charges appropriate to the received delivery address. You should then send a new request, containing the **masterPassData** received, to continue the transaction and authorise it.

_If the continuation request contains any details that would normally be read from the Masterpass Wallet, then these will be ignored and the Wallet details returned. Note: this is different from usual processing, where incoming fields usually take precedence._

The outcome of this request will depend on the value of the **masterPassStatus** field and the ability to communicate with Masterpass. On success, the Gateway will return a **responseCode** of **65571 (MASTERPASS\_CHECKOUT\_SUCCESS)** and response will include the chosen payment card and address details. If the Wallet was cancelled or if the chosen details cannot be retrieved, then the Gateway will return a **responseCode** of **65570 (MASTERPASS\_CHECKOUT\_FAILURE).**

Note: this stage can be repeated multiple times by including the **masterPassOnly** field with a value of &#39;Y&#39; each time. To complete the transaction, the final request must not contain the **masterPassOnly** field or it must not have a value of &#39;Y&#39;.

  1.
## Request Fields

    1.
### Initial Request (Hosted and Direct Integrations)

These fields should be sent in addition to basic request fields in section 2.1 excluding any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **paymentMethod** | Yes
# 30
 | Must contain the value &#39;masterpass&#39; in lower case letters only. |
| **masterPassCallbackURL** | Yes
# 31
 | URL on Merchant&#39;s server to return to when the Masterpass Wallet is closed. |
| **masterPassCheckoutOptions** | No | Record containing options used to customise the Masterpass Wallet. Refer to section 20.5.3 for values. |
| **masterPassCheckoutID** | No | Merchant&#39;s unique checkout identifier as provided by Masterpass. |

    1.
### Continuation Request (Direct Integration)

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **masterPassData** | Yes
 | Unique reference returned in the initial response. |
| **masterPassStatus** | Yes
# 32
 | The Wallet status returned to the Merchant. |
| **masterPassToken** | Yes1 | The OAuth token returned to the Merchant. |
| **masterPassVerifier** | Yes1 | The OAuth verifier returned to the Merchant. |
| **masterPassOnly** | No | Pass **Y** to complete the processing as far as the next Wallet stage and then return with the loaded Wallet details. |

    1.
### Wallet Options (Hosted and Direct Integrations)

The following options may be set in the **masterPassCheckoutOptions** field to customise the Masterpass Wallet.

| **Field Name** | **Description** |
| --- | --- |
| **version** | Masterpass version required.
Possible values are: **v6** – use version 6 of the Masterpass API (default). **v7** – use version 7 of the Masterpass API (preferred). |
| --- | --- |
| **requireLightboxCheckout** | Use the lightbox version of the Masterpass Wallet rather than the full screen checkout when possible.
Possible values are: **false** – use the full screen Wallet. **true** – use the lightbox Wallet if possible. |
| **suppress3Ds** | Suppress Masterpass 3-D Secure processing. This allows the Gateway to do the 3-D Secure processing using the chosen card details.
Possible values are: **false** – allow the Wallet to handle 3-D Secure. **true** – allow the Gateway to handle 3-D Secure. |
| **requestBasicCheckout** | Deprecated name for **suppress3Ds.** |
| **suppressShippingAddress** | Suppress the requirement for the Customer to select a shipping address as well as payment card details.
Possible values are: **false** – shipping address must be selected. **true** – shipping address need not be selected. |
| **requestShippingAddressEnable** | Deprecated name for **suppressShippingAddress.** |
| **shippingLocationProfile** | Provide a Masterpass shipping profile. Refer to the Masterpass document for details. |
| **rewardsProgram** | Enable the Masterpass loyalty program. Refer to the Masterpass document for details. |
| **loyaltyEnabled** | Deprecated name for **rewardsProgram.** |
| **suppressWalletSelector**
 | Suppress the ability to select alternative Wallet providers from within the Masterpass Wallet.
Possible values are: **false** – allow alternative Wallets to be selected. **true** – don&#39;t allow alternative Wallets to be selected. |
| **walletSelectorBypassEnable** | Deprecated name for **suppressWalletSelector** |
| **merchantCheckoutId** | Merchant&#39;s unique checkout identifier as provided by Masterpass. Either as passed in the initial request or as configured on the Gateway for your account. |
| **allowedCardTypes** | List of Masterpass card types to allow selection from within the Wallet. Will be returned in the response from the card types configured for your Merchant Account. |

The options should be passed as either a nested record or serialised record as described in section 1.5.8. The option names are case sensitive.

The deprecated options were originally used with v6 of the Masterpass API and the Gateway will accept both the newer v7 option name and the original v6 option name regardless of the value of any version option provided. The Gateway may return the correct name for the version when it returns the **masterPassCheckoutOptions** in the initial response.

The nature of the URL returned in the **masterPassCheckoutURL** response field depends on whether the Masterpass lightbox or full-page redirect checkout is required as specified using the **requireLightboxCheckout** option. If the option is passed as &#39;true&#39;, then the URL will reference the Masterpass JavaScript file that should be loaded to provide the code required to open the lightbox style Wallet. The **masterPassCheckoutOptions** response values should then be passed to the JavaScript call to open the lightbox. If the option is not passed or not &#39;true&#39;, then the URL will be an address to redirect the Customer&#39;s browser to in order to display the MasterPass Checkout pages. This URL will have its query component initialised from any **masterPassCheckoutOptions** request values, and any response values need not be used.

If the **suppress3Ds** or **requestBasicCheckout** option is not passed, then it will be defaulted to &#39;true&#39;, so that the Gateway&#39;s 3-D Secure processing will be used as opposed to the Wallet&#39;s 3-D Secure processing. This ensures your 3-D Secure preferences are followed.

If the suppressShippingAddress **or suppressShippingAddressEnable** option is passed as &#39;true&#39; then no attempt will be made to return the delivery address fields. Any delivery address fields passed in the transaction will be echoed back unaltered.

Any **merchantCheckoutId** or **allowedCardTypes** options will be overwritten and therefore should not be passed in the request but will be available in the response.

    1.
### Purchase details (Hosted and Direct Integrations)

The following request fields may be sent to provide information on the purchased items and to populate the cart on the Masterpass Wallet (v6 only).

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **item** _ **XX** _ **Description** | No | Description of _XX_th item purchased. |
| **item** _ **XX** _ **Quantity** | No | Quantity of _XX_th item purchased. |
| **item** _ **XX** _ **Gross**** Amount** | No | Gross amount for _XX_th item purchased. |
| **item** _ **XX** _ **TaxAmount** | No | Tax amount for _XX_th item purchased. |
| **item** _ **XX** _ **ProductCode** | No | Product code for _XX_th item purchased. |
| **itemXXImageUrl** | No | Shopping cart URL for _XX_th item purchased. |
| **item** _ **XX** _ **Size** | No | Size of _XX_th item purchased in the format &#39;LengthxWidthxHeight Unit&#39;. |
| **item** _ **XX** _ **Weight** | No | Weight of X_X_th item purchased in the format &#39;Weight Unit&#39;. |
| **items** | No | Nested array of line items. |

Refer to section 15.2 for more information on these fields.

  1.
## Response Fields

    1.
### Initial Response (Direct Integration)

These fields will be returned in addition to the request fields from section 19.5.1 and the basic response fields in section 2.2minus any card details.

| **Field Name** | **Mandatory?** | **Description** |
 |
| --- | --- | --- | --- |
|
 | **masterPassData** | Yes
 | Unique reference required to continue this transaction when the Masterpass Wallet has completed. |
|
 | **masterPassCheckoutURL** | Yes | URL required to load the Masterpass Checkout |
|
 | **masterPassCheckoutOptions** | No | Any checkout options passed in the request. |

    1.
### Continuation Response (Direct Integration)

These fields will be returned in addition to the request fields from section 19.5.2; the initial response fields in section 19.6.1; and the basic response fields in section 2.2 minus any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **masterPassData** | No
 | Provided, if **masterPassOnly** was used in the continuation response to indicate that a further request will be sent to finalise the transaction. |
| **masterPassWalletID** | Yes | Masterpass Wallet ID. |
| **masterPassCheckout** | Yes | Masterpass Wallet details in original retrieved XML format minus any card numbers. |
| **card** _ **XXXX** _ | Yes | Card details chosen in the Masterpass Wallet as documented in section 2.2. |
| **customer** _ **XXXX** _ | No
# 33
 | Customer details if provided by the Masterpass Wallet as documented in section 17.1 |
| **delivery** _ **XXXX** _ | No1 | Delivery details if provided by the Masterpass Wallet as documented in section 17.4 |

1.
# PayPal Transactions

  1.
## Background

PayPal is an additional payment method that is available to all Merchants using the Gateway who have a PayPal account.

To use PayPal, you will be supplied with a separate PayPal Merchant Account that can be grouped with your main Merchant Account using the account mapping facility as documented in appendix A-8. This allows transactions to be sent using your main Merchant Account and then routed automatically to the PayPal Merchant Account in the same mapping group.

It allows you to offer payment via PayPal in addition to normal card payments.

PayPal transactions will appear in the Merchant Management System (MMS) alongside any card payments and can be captured, cancelled and refunded in the same way as card payments.

PayPal transactions can also be used for recurring billing but require you to indicate in the initial transaction that it will be the basis for recurring billing and that a billing agreement will be entered into between your Customer and PayPal when they agree to the payment.

PayPal transactions cannot be used for ad-hoc &#39;Card On File&#39; repeat transactions unless a billing agreement has been set up.

For more information on how to accept PayPal transactions, please contact customer support.

**PayPal is supported by the Hosted and Direct Integrations. It is not supported by the Batch Integration.**

  1.
## Benefits and Limitations

    1.
### Benefits

- Provides your customers with the flexibility of paying by using their PayPal account when this is more suitable to them than using a traditional credit or debit card.

- The in-context PayPal Express Checkout helps improve conversion rates with an easier way to pay without customers leaving your website.

- There are no extra costs for adding a PayPal Merchant Account. However, you will still be liable for the PayPal transaction fees.

- The full PayPal transaction information is available and returned as part of the transaction.

- Transactions are controlled within the Merchant Management System (MMS) in the same manner as normal card transactions.

    1.
### Limitations

- You will need a PayPal account.

- Recurring transactions are not supported unless as part of a prearranged billing agreement.

- Independent refunds that are not tied to a previous sale transaction are not supported without prior agreement.

- Transactions require a browser in order to display the PayPal Checkout.

- The PayPal Checkout cannot be opened from within a browser IFRAME and so care must be taken to ensure that any PayPal Checkout button is not placed within such an IFRAME.

  1.
## Hosted Implementation

If a transaction is sent to the Hosted Integration using a **merchantID** that is part of a routing group containing a PayPal Merchant, then the Hosted Payment Page will display a PayPal payment button that, when clicked, will open the PayPal Checkout and allow the Customer to pay using their PayPal account.

To customise the PayPal Checkout experience, you may send various options in the **payPalCheckoutOptions** field in your initial request.

Additional information available from the PayPal Checkout will be made available in the **checkoutDetails** response field.

_Note: Custom Hosted Payment Pages might not support the displaying of the PayPal Checkout button. If you have a custom page that doesn&#39;t support this, then you would need to contact support to have your Hosted Payment Page upgraded._

  1.
## Direct Implementation

PayPal transactions require you to display the PayPal Checkout to your Customer as part of the transaction flow. The transaction must be done in two stages, with the Checkout being displayed between the stages. They can also be optionally done in three stages allowing you to display an order confirmation after the Checkout and before authorising the transaction. You can change the amount at this stage to allow for shipping costs when you know the confirmed delivery address the Customer selected as part of the PayPal Checkout.

PayPal supports the normal payment and management actions. This section explains how to make payment requests. Management requests are performed as detailed in section 3.

    1.
### Initial Request (Checkout Preparation)

To request that a transaction be processed via PayPal the request must contain a **paymentMethod** of &#39;paypal&#39; and a **checkoutRedirectURL** containing the URL of a page on your server to return to when the Checkout is closed. In addition, you may send **checkoutOptions** to customise the Checkout experience. When the Gateway receives this **paymentMethod** , assuming there are no other errors with the request, it will attempt to find a suitable PayPal Merchant Account in the current account mapping group.

If the Gateway is unable to find a suitable account, then the transaction will be aborted and it will respond with a **responseCode** of **66364 (INVALID PAYMENTMETHOD)**.

Otherwise the Gateway will respond with a **responseCode** of **65826 (CHECKOUT REQUIRED)** and included in the response will be a **checkoutURL** field containing the URL required to load Checkout and a **checkoutRequest** containing any data required to be sent to the Checkout. The response will also contain a unique **checkoutRef** which must be echoed back in the continuation requests.

At this point your server must redirect the Customer&#39;s browser to the provided **checkoutURL**. Alternatively, the **checkoutURL** can be used in conjunction with the PayPal In-Context JavaScript code to implement an In-context Checkout which allows the Merchants website to remain visible in the background. Further details on how to use the In-Context Checkout are provided in the PayPal guide at [https://developer.paypal.com/docs/classic/express-checkout/in-context/enable\_in\_context\_checkout/](https://developer.paypal.com/docs/classic/express-checkout/in-context/enable_in_context_checkout/).

    1.
### Continuation Request (Checkout Details and Authorise)

On completion of the PayPal Checkout it will redirect the Customer&#39;s browser to the **checkoutRedirectURL** provided including a **token** and **status** URL parameters. If the checkout was successful, the status will be &#39;success&#39; alternatively if the Checkout was cancelled the status will be &#39;cancel&#39;. The received redirect request parameters inclusive of these **token** and **status** parameters should then be sent to the Gateway in the **checkoutResponse** fields of a new request. The **checkoutResponse** field can be sent either as the original URL query string received or as an array of the decoded query parameters. This new request will load the Checkout details including any delivery address if required and send the transaction to PayPal for authorisation, returning the result as per a normal authorisation transaction. The new request must contain the **checkoutRef** received in the initial response.

    1.
### Separate Checkout Details and Authorisation Requests

You can choose to obtain the Checkout details before actually sending the transaction for authorisation by sending the **checkoutOnly** field in the above continuation request. If this field is sent with a value of &#39;Y&#39; then the Gateway will load the Checkout details and then return them to you without sending the request for authorisation. You can then display them and/or adjust the amount, for example, according to delivery charges appropriate to the received delivery address. You should then send a new request containing the **checkoutRef** received to continue the transaction and authorise it.

Note: this stage can be repeated multiple times by including the **checkoutOnly** field with a value of &#39;Y&#39; each time. To complete the transaction, the final request must not contain the **checkoutOnly** field or it must not have a value of &#39;Y&#39;.

  1.
## Request Fields

    1.
### Initial Request (Hosted and Direct Integrations)

These fields should be sent in addition to basic request fields in section 2.1 excluding any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **paymentMethod** | Yes
# 34
 | Must contain the value &#39;paypal&#39; in lower case letters only. |
| **checkoutRedirectURL** | Yes
# 35
 | URL on Merchant&#39;s server to return to when the PayPal Checkout is closed. |
| **checkoutOptions** | No
# 36
 | Record containing options used to customise the PayPal Checkout. Refer to section 20.5.3 for values. |
| **payPalCheckoutOptions** | No
# 37
 | Record containing options used to customise the PayPal Checkout. Refer to section 20.5.3 for values. |

    1.
### Continuation Request (Direct Integration)

These fields may be sent alone
# 38
.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutRef** | Yes
 | Unique reference return in the initial response. |
| **checkoutResponse** | Yes | The GET and or POST data received by the **checkoutRedirectURL** page. |
| **checkoutOnly** | No | Pass **Y** to complete the processing as far as the next Checkout stage and then return with the loaded Checkout details. |

    1.
### Checkout Options (Hosted and Direct Integrations)

The following options may be set in the **payPalCheckoutOptions** Hosted Integration field or the **checkoutOptions** Direct Integration field to customise the PayPal Checkout.

| **Field Name** | **Description** |
| --- | --- |
| **inContext** | Use the in-context PayPal Checkout rather than the full screen Checkout when possible.
Possible values are: **0** – use the full screen Checkout. **1** – use the in-context Checkout if possible. |
| --- | --- |
| **userAction** | Determines whether buyers complete their purchases on PayPal or on your website.
Possible values are: **commit** – sets the submit button text to &#39;Pay Now&#39; on the PayPal Checkout. This text lets buyers know that they complete their purchases if they click the button. **continue** – sets the submit button text to &#39;Continue&#39; on the PayPal Checkout. This text lets buyers know that they will return to the Merchant&#39;s cart to complete their purchases if they click the button. |
| **maxAmount**
# 0
 | The expected maximum total amount of the order, including shipping and taxes. |
| **reqBillingAddress** | Determines whether the buyer&#39;s billing address on file with PayPal is returned. **This feature must be enabled by PalPal**. |
| **reqConfirmShipping** | Determines whether the buyer&#39;s shipping address on file with PayPal must be a confirmed address.
Possible values are: **0** – does not need to be confirmed **1** – must be confirmed |
| **noShipping** | Determines whether PayPal displays shipping address.
Possible values are: **0** – display the shipping address **1** – do not display shipping address and remove shipping information **2** – If no **delivery** _ **XXXX** _ fields passed, PayPal obtains them from the buyer&#39;s account profile. |
| **addrOverride** | Determines whether the PayPal Checkout displays the shipping address sent using the **delivery** _ **XXXX** _ fields and not the shipping address on file with PayPal for this buyer. Displaying the PayPal street address on file does not allow the buyer to edit that address.
Possible values are: **0** – PayPal should not display the address. **1** – PayPal should display the address. |
| **localeCode** | Locale of the pages displayed by PayPal during Express Checkout. It is either a two-letter country code or five-character locale code supported by PayPal. |
| **allowNote** | Enables the buyer to enter a note to the merchant on the PayPal page during Checkout. The note is returned in the checkoutDetails response field. |
| **pageStyle** | Name of the Custom Payment Page Style used for the PayPal Checkout. It is the same name as the Page Style Name used when adding styles in the PayPal Account. |
| **payflowColor** | The HTML hex colour code for the PayPal Checkout&#39;s background colour. By default, the colour is white (FFFFFF). |
| **cardBorderColor** | The HTML hex colour code for the PayPal Checkout&#39;s principal identifying colour. The colour will be blended to white in a gradient fill that borders the cart review area. |
| **hdrImg** | URL for the image you want to appear at the top left of the payment page. The image has a maximum size of 750 pixels wide by 90 pixels high. PayPal requires that you provide an image that is stored on a secure (https) server. If you do not specify an image, the business name displays. |
| **logoImg** | A URL to your logo image. Use a valid graphics format, such as .gif, .jpg, or .png. Limit the image to 190 pixels wide by 60 pixels high. PayPal crops images that are larger. PayPal places your logo image at the top of the cart review area. |
| **landingPage** | Type of PayPal Checkout to display.
Possible values are: **Billing** – Non-PayPal account **Login** – PayPal account login |
| **channelType** | Type of channel.
Possible values are: **Merchant** – Non-auction seller **eBayItem** – eBay auction |
| **solutionType** | Type of Checkout flow.
Possible values are: **Sole** – Buyer does not need to create a PayPal account to check out. This is referred to as PayPal Account Optional. **Mark** – Buyer must have a PayPal account to check out. |
| **totalType** | Type declaration for the label to be displayed in MiniCart for UX.
Possible values are: **Total**** EstimatedTotal** |
| **brandName** | A label that overrides the business name in the PayPal account on the PayPal Checkout. |
| **customerServiceNumber** | Merchant Customer Service number displayed on the PayPal Checkout. |
| **buyerEmailOptInEnable** | Enables the buyer to provide an email address on the PayPal pages to be notified of promotions or special events.
Possible values are: **0** – Do not enable buyer to provide email. **1** – Enable the buyer to provide email. |
| **noteToBuyer** | A note from the merchant to the buyer that will be displayed in the PayPal Checkout. |
| **paymentAction** | Defines how to obtain payment. This can be used to override any captureDelay setting that can also be used to indicate a **Sale** or **Authorisation** only.
Possible values are: **Sale** – sale with immediate capture. **Authorization** – authorisation subject to later capture (note spelling). **Order** – order subject to later authorisation and capture. |
| **allowedPaymentMethod** | The payment method type. Specify the value InstantPaymentOnly |
| **insuranceOptionOffered** | Indicates whether insurance is available as an option that the buyer can choose on the PayPal Review page.
Possible values are: **true** – The Insurance option displays &#39;Yes&#39; and the insuranceAmount. If true, the total shipping insurance for this order must be a positive number. **false** – The Insurance option displays &#39;No&#39;. |
| **multiShipping** | Indicates whether this payment is associated with multiple shipping addresses.
Possible values are: **0** – Single/No shipping address. **1** – Multiple shipping addresses. |
| **noteText** | Note to the Merchant. |
| **bucketCategoryType** | The category of a payment.
Possible values are: **1** – International shipping **2** – Local delivery **3** – BOPIS, Buy online pick-up in store **4** – PUDO, Pick-up drop-off |
| **locationType** | Type of merchant location. Required if the items purchased will not be shipped, such as, BOPIS (Buy Online Pick-up In Store) or PUDO (Pick-Up Drop-Off) transactions.
Possible values are: **1** – Consumer. **2** – Store, for BOPIS transactions. **3** – PickupDropoff, for PUDO transactions. |
| **locationID** | Location ID specified by the merchant for BOPIS (Buy Online Pick-up In Store) or PUDO (Pick-Up Drop-Off) transactions. |
| **sellerPayPalAccountID** | Unique identifier for the Merchant. For parallel payments, this field is required and must contain the Payer Id or the email address of the Merchant. |
| **invNum** | Merchant&#39;s invoice or tracking number. |
| **custom** | Custom field for your own use. |
| **buyerID** | The unique identifier provided by eBay for this buyer. The value may or may not be the same as the username. In the case of eBay, it is different. |
| **buyerUsername** | The user name of the user at the marketplaces site. |
| **buyerRegistrationDate** | Date when the user registered with the marketplace. In UTC/GMT format, for example, 2013-08-24T05:38:48Z. |
| **allowPushFunding** | Indicates whether the Merchant can accept push funding.
Possible values are: **0** – Merchant cannot accept push funding. **1** – Merchant can accept push funding. |
| **userSelectedFundingSourc**** e **| This element could be used to specify the preferred funding option for a guest user. However, the landingPage Checkout option must also be set to** Billing**, otherwise it is ignored.
Possible values are: **ChinaUnionPay.**** CreditCard. ****ELV.**** QIWI.** |
| **billingType** | Type of billing agreement for reference transactions. You must have permission from PayPal to use this field.
Possible values are: **MerchantInitiatedBilling** – PayPal creates a billing agreement for each transaction associated with buyer. **MerchantInitiatedBillingSingleAgreement** – PayPal creates a single billing agreement for all transactions associated with buyer. Use this value unless you need per-transaction billing agreements. |
| **billingAgreementDescriptio**** n** | Description of goods or services associated with the billing agreement. This field is required for each recurring payment billing agreement. PayPal recommends that the description contain a brief summary of the billing agreement terms and conditions. For example, buyer is billed at &quot;9.99 per month for 2 years&quot;.




 |
| **paymentType** | Type of PayPal payment you require for the billing agreement.
Possible values are: **Any** – The merchant accepts any payment method for the billing agreement, even if it could take a few working days for the movement of funds to the merchant account. This includes echeck, in addition to credit or debit cards and PayPal balance.
**InstantOnly** – The payment options accepted by the merchant are credit cards, debit cards or PayPal balance only because the merchant expects immediate payment. |
| **taxIDType** | Buyer&#39;s tax ID type. This field is required for Brazil and used for Brazil only.
For Brazil use only: The tax ID type is BR\_CPF for individuals and BR\_CNPJ for businesses. |
| **taxID** | Buyer&#39;s tax ID. This field is required for Brazil and used for Brazil only.
For Brazil use only: The tax ID is 11 single-byte characters for individuals and 14 single-byte characters for businesses |
| **returnFMFDetails** | Flag to indicate whether you want the results returned by Fraud Management Filters when doing a recurring/reference transaction.
Possible values are: **0** – Do not receive FMF details (default). **1** – Receive FMF details. |
| **riskSessionCorrelationID** | The ID of the risk session for correlation purposes when doing a recurring/reference transaction. |
| **merchantSessionID** | The buyer session identification token when doing a recurring/reference transaction. |
| **buttonSource**
 **# 39** | PayPal Partner&#39;s BN Code (if required). |

For further information on the options, refer to the PayPal Express Checkout documentation: [https://developer.paypal.com/docs/classic/api/merchant/SetExpressCheckout\_API\_Operation\_NVP/](https://developer.paypal.com/docs/classic/api/merchant/SetExpressCheckout_API_Operation_NVP/).

The options should be passed as either a nested record or serialised record as described in section 1.5.8. The option names are case sensitive.

    1.
### Purchase details (Hosted and Direct Integrations)

The following request fields may be sent to provide information on the purchased items and to populate the cart on the PayPal Checkout.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **shippingAmount** | No | Shipping costs. |
| **shippingDiscountAmount** | No | Discount applied to shipping costs. |
| **handlingAmount** | No | Handling costs. |
| **insuranceAmount** | No | Insurance costs. |
| **item** _ **XX** _ **Description** | No | Description of _XX_th item purchased. |
| **item** _ **XX** _ **Quantity** | No | Quantity of _XX_th item purchased. |
| **item** _ **XX** _ **Amount** | No | Gross amount for _XX_th item purchased. |
| **item** _ **XX** _ **TaxAmount** | No | Tax amount for _XX_th item purchased. |
| **item** _ **XX** _ **ProductCode** | No | Product code for _XX_th item purchased. |
| **itemXXProductURL** | No | Shopping cart URL for _XX_th item purchased. |
| **item** _ **XX** _ **Size** | No | Size of _XX_th item purchased in the format &#39;LengthxWidthxHeight Unit&#39;. |
| **item** _ **XX** _ **Weight** | No | Weight of X_X_th item purchased in the format &#39;Weight Unit&#39;. |
| **items** | No | Nested array of line items. |

Refer to section 15.2 for more information on these fields.

Note: The shopping cart items must total to the amount specified in the transaction. If they do not, cart items will not be sent to the PayPal Checkout.

  1.
## Response Fields

    1.
### Initial Response (Direct Integration)

These fields will be returned, in addition to the request fields from section 20.5.1 and the basic response fields in section 2.2minus any card details.

| **Field Name** | **Mandatory?** | **Description** |
 |
| --- | --- | --- | --- |
|
 | **checkoutRef** | Yes
 | Unique reference required to continue this transaction when the PayPal Checkout has completed. |
|
 | **checkoutName** | Yes | Unique name of the Checkout. For PayPal this is the value **paypal**. |
|
 | **checkoutURL** | Yes | URL required to load the PayPal Checkout |
|
 | **checkoutRequest** | No | Not required for PayPal. |
|
 | **checkoutOptions** | No | Any Checkout options passed in the request. |
|
 | **acquirerResponseDetails** | Yes | Details about the PayPal response containing any error messages and codes. This can be used together with the normal **responseCode** and **responseMessage** response fields to determine further the reason for any failure. |

    1.
### Continuation Response (Direct Integration)

These fields will be returned, in addition to the request fields from section 20.5.2, the initial response fields in section 20.6.1 and the basic response fields in section 2.2 minus any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutRef** | Yes
 | Provided if **checkoutOnly** was used in the continuation response to indicate that a further request will be sent to finalise the transaction. |
| **checkoutName** | Yes | Unique name of the Checkout. For PayPal, this is the value **paypal**. |
| **checkoutDetails** | Yes | Record containing options used to customise the PayPal Checkout. Refer to section 20.6.3 for values. |
| **customer** _ **XXXX** _ | No1 | Customer details if provided by the PayPal Checkout as documented in section 17.1 |
| **delivery** _ **XXXX** _ | No1 | Delivery details if provided by the PayPal Checkout as documented in section 17.4 |
| **acquirerResponseDetails** | Yes | Details about the PayPal response containing any error messages and codes. This can be used together with the normal **responseCode** and **responseMessage** response fields to determine further the reason for any failure. |

    1.
### Checkout Details (Hosted and Direct Integration)

The following details may be provided in the **checkoutDetails** field included in the response.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **correlationID** | No | Correlation ID, which uniquely identifies the transaction to PayPal. |
| --- | --- | --- |
| **checkoutStatus** | No | Status of the Checkout session. If payment is completed, the transaction identification number of the resulting transaction is returned.
Possible values are: **PaymentActionNotInitiated**** PaymentActionFailed ****PaymentActionInProgress**** PaymentActionCompleted** |
| **invNum** | No | Merchant&#39;s invoice or tracking number, as set sent in **checkoutDetails.invNum** or assigned by the Gateway. |
| **custom** | No | Merchant&#39;s invoice or tracking number, as set sent in **checkoutDetails.custom** or assigned by the Gateway. |
| **payPalAdjustment** | No | A discount or gift certificate offered by PayPal to the buyer. This amount is represented by a negative amount. If the buyer has a negative PayPal account balance, PayPal adds the negative balance to the transaction amount, which is represented as a positive value. |
| **buyerMarketingEmail** | No
# 0
 | Buyer&#39;s marketing email address. |
| **note** | No
# 0
 | Buyer&#39;s note to the Merchant. |
| **cartChangeTolerance** | No | Indicates whether a cart&#39;s contents can be modified. If this parameter is not returned, then assume the cart can be modified. This will return **NONE** if financing was used in Germany.
Possible values are: **NONE** – The cart cannot be changed. **FLEXIBLE** – The cart can be changed. |
| **payerID** | No | Buyer&#39;s PayPal Customer Account ID.

 |
| **payerStatus** | No | Buyer&#39;s PayPal status.
Possible values are: **verified**** unverified** |
| **billingName** | No
# 0
 | Buyer&#39;s name.Also returned in **customerName**. |
| **firstName** | No
# 0
 | Buyer&#39;s first name.Also returned in **customerName**. |
| **middleName** | No2 | Buyer&#39;s middle name.Also returned in **customerName**. |
| **lastName** | No2 | Buyer&#39;s last name.Also returned in **customerName**. |
| **suffix** | No2 | Buyer&#39;s name suffix.Also returned in **customerName**. |
| **business** | No | Buyer&#39;s business name.Also returned in **customerCompany**. |
| **street** | No | Buyer&#39;s street first line.Also returned in **customerAddress**. |
| **street2** | No | Buyer&#39;s street second line.Also returned in **customerAddress**. |
| **city** | No | Buyer&#39;s city
 Also returned in **customerTown**. |
| **state** | No | Buyer&#39;s state.Also returned in **customerCounty**. |
| **zip** | No | Buyer&#39;s postal code.Also returned in **customerPostcode**. |
| **countryCode** | No | Buyer&#39;s country code. (ISO 2 char. code)Also returned in **customerCountryCode**. |
| **countryName** | No | Buyer&#39;s country name. |
| **phoneNum** | No | Buyer&#39;s contact phone number.Also returned in **customerPhone**. |
| **email** | No | Buyer&#39;s email address.Also returned in **customerEmail**.

 |
| **shipToName** | No | Name of person/entity to ship to.Also returned in **deliveryName**. |
| **shipToStreet** | No | Ship to street first line.Also returned in **deliveryAddress**. |
| **shipToStreet2** | No | Ship to street second line.Also returned in **deliveryAddress**. |
| **shipToCity** | No | Ship to city.Also returned in **deliveryTown**. |
| **shipToState** | No | Ship to state.Also returned in **deliveryCounty**. |
| **shipToZip** | No | Ship to postal code.Also returned in **deliveryPostcode**. |
| **shipToCountryCode** | No | Ship to country code. (ISO 2 char. code)Also returned in **deliveryCountryCode**. |
| **shipToCountryName** | No | Ship to country name. |
| **shipToPhoneNum** | No | Ship to phone number.Also returned in **deliveryPhone**. |
| **shipToAddressStatus** | No | Status of shipping address on file with PayPal.
Possible values are: **none**** Confirmed ****Unconfirmed** |
| **addressNormalizationStatu**** s** | No
# 0
 | The PayPal address normalisation status for Brazilian addresses.
Possible values are: **None**** Normalized ****Unnormalized**** UserPreferred** |
| **amount** | No | Total amount for this order. |
| **itemAmount** | No | Total item amount for this order. |
| **taxAmount** | No | Tax amount for this order. |
| **exchangeRate** | No | Exchange rate for this order. |
| **shippingAmount** | No | Shipping amount for this order. |
| **handlingAmount** | No | Handling amount for this order. |
| **insuranceAmount** | No | Insurance amount for this order. |
| **shipDiscountAmount** | No | Shipping discount amount for this order. |
| **desc** | No | Description of items the buyer is purchasing. |
| **currencyCode** | No | ISO 3-letter currency code. |
| **isFinancing** | No | Indicates whether the Customer ultimately was approved for and chose to make the payment using the approved instalment credit.
Possible values are: **FALSE** – financing not in use **TRUE** – financing approved and used |
| **financingFeeAmount** | No | The transaction financing fee associated with the payment. This will be set to the instalment fee amount that is the same as the estimated cost of credit or the interest/fees amount the user will have to pay during the lifetime of the loan. This field will only be included in instalment credit orders. In the case of &quot;same as cash&quot; or &quot;no interest&quot; offers, this will be set to 0. |
| **financingTerm** | No | The length of the financing term, in months. Example values are 6, 12, 18 and 24 months. |
| **financingMonthlyPayment** | No | This is the estimated amount per month that the Customer will need to pay including fees and interest. |
| **financingTotalCost** | No | This is the estimated total payment amount including interest and fees that the user will pay during the lifetime of the loan. |
| **financingDiscountAmount** | No | Discount amount for the buyer if paid in one instalment. |
| **regularTakeFeeAmount** | No | Fee of the regular take rate on the transaction amount. It could be equal to **financingDiscountAmount** in the case of non-instalment transactions. |
| **noteText** | No | Note to Merchant. |
| **transactionID** | No | PayPal transaction ID. |
| **allowedPaymentMethod** | No | The payment method type as specified in the initial request. |
| **paymentRequestID** | No | A unique identifier of the specific payment request. |
| **bucketCategoryType** | No | The category of a payment as specified in the initial request. |
| **instrumentCategory** | No | Identifies the category of the promotional payment instrument.
Possible values are: **1** – PayPal Credit® (formerly Bill Me Later®). **2** – A Private Label Credit Card (PLCC) or co-branded payment card. |
| **instrumentID** | No | An instrument ID (issued by the external party) corresponding to the funding source used in the payment. |
| **shippingCalculationMode** | No | Describes how the options that were presented to the buyer were determined.
Possible values are: **API – Callback**** API – Flatrate** |
| **insuranceOptionSelected** | No | The option that the buyer chose for insurance.
Possible values are: **Yes –** opted for insurance. **No**** –** did not opt for insurance. |
| **shippingOptionIsDefault** | No | Indicates whether the buyer chose the default shipping option.
Possible values are: **true –** chose the default shipping option. **false**** –** did not choose the default shipping option. |
| **shippingOptionAmount** | No | The shipping amount that the buyer chose. |
| **shippingOptionName** | No | The name of the shipping option, such as Air or Ground. |
| **scheduledShippingDate** | No | The scheduled shipping date is returned only if scheduled shipping options are passed in the request. |
| **scheduledShippingPeriod** | No | The scheduled shipping period is returned only if scheduled shipping options are passed in the request. |
| **sellerPayPalAcountID** | No | Unique identifier for the merchant. For parallel payments, this field contains either the Payer ID or the email address of the merchant. |
| **taxIDType** | No | Buyer&#39;s tax ID type. This field is required for Brazil and used for Brazil only.
For Brazil use only: The tax ID type is BR\_CPF for individuals and BR\_CNPJ for businesses. |
| **taxID** | No | Buyer&#39;s tax ID. This field is required for Brazil and used for Brazil only.
For Brazil use only: The tax ID is 11 single-byte characters for individuals and 14 single-byte characters for businesses |
| **billingAgreementID** | No | Identification number of the billing agreement. When the buyer approves the billing agreement, it becomes valid and remains valid until it is cancelled by the buyer. |
| **billingAgreementAcceptedStatu**** s** | No | Indicates whether the buyer accepted the billing agreement for a recurring payment. Currently, this field is always returned in the response for agreement-based products, such as subscriptions; reference transactions; recurring payments; and regular single payment transactions.
**0**** – **Not accepted.** 1 –** Accepted. |
| **paymentStatus** | No | Status of the payment.
Possible values are: **None**** – **No status.** Canceled-Reversal ****–** A reversal has been cancelled: for example, when you win a dispute and the funds for the reversal have been returned to you. **Completed**** – **The payment has been completed and the funds have been added successfully to your account balance.** Denied ****–** You denied the payment. This happens only if the payment was previously pending because of possible reasons described for the **pendingReason** element. **Expired**** – **The authorisation period for this payment has been reached.** Failed ****–** The payment has failed. This happens only if the payment was made from your buyer&#39;s bank account. **In-Progress**** – **The transaction has not terminated: for example, an authorisation may be awaiting completion.** Partially-Refunded ****–** The payment has been partially refunded. **Pending**** – **The payment is pending. See the** pendingReason **field for more information.** Refunded ****–** You refunded the payment. **Reversed**** – **A payment was reversed due to a chargeback or other type of reversal. The funds have been removed from your account balance and returned to the buyer. The reason for the reversal is specified in the** reasonCode **element.** Processed ****–** A payment has been accepted. **Voided**** –** An authorisation for this transaction has been voided. |
| **refundStatus** | No | Status of the refund.
Possible value are: **none**** – **returned if the refund fails** instant **– refund was instant** delayed** – refund was delayed |
| **pendingReason** | No
# 0
 | The reason the payment is pending.
Possible values are: **none**** – **No pending reason.** address ****–** The payment is pending because your buyer did not include a confirmed shipping address and your Payment Receiving Preferences is set such that you want to accept or deny each of these payments manually. To change your preference, go to the Preferences section of your Profile. **authorization**
 **# 0**** – **The payment is pending because it has been authorised but not settled. You must capture the funds first.** echeck ****–** The payment is pending because it was made by an eCheck that has not yet cleared. **intl**** – **The payment is pending because you hold a non-U.S. account and do not have a withdrawal mechanism. You must manually accept or deny this payment from your Account Overview.** multi-currency ****–** You do not have a balance in the currency sent, and you do not have your Payment Receiving Preferences set to automatically convert and accept this payment. You must manually accept or deny this payment. **order**** – **The payment is pending because it is part of an order that has been authorised but not settled.** payment-review ****–** The payment is pending while it is being reviewed by PayPal for risk. **regulatory-review**** – **The payment is pending while we make sure it meets regulatory requirements. You will be contacted again from 24 to 72 hours with the outcome of the review.** unilateral ****–** The payment is pending because it was made to an email address that is not yet registered or confirmed. **verify**** – **The payment is pending because you are not yet verified. You must verify your account before you can accept this payment.** other ****–** The payment is pending for a reason other than those listed above. For more information, contact PayPal Customer Service. |
| **reasonCode** | No | The reason for a reversal if the transaction type is reversal.
Possible values are: **none**** – **No reason code.** chargeback ****–** A reversal has occurred on this transaction due to a chargeback by your buyer. **guarantee**** – **A reversal has occurred on this transaction due to your buyer triggering a money-back guarantee.** buyer-complaint ****–** A reversal has occurred on this transaction due to a complaint about the transaction from your buyer. **refund**** – **A reversal has occurred on this transaction because you have given the buyer a refund.** other ****–** A reversal has occurred on this transaction due to a reason not listed above. |
| **protectionEligibilityType** | No | The kind of seller protection in force for the transaction.
Possible values are: **ItemNotReceivedEligible**** – **Merchant is protected by PayPal&#39;s Seller Protection Policy for Item Not Received.** UnauthorizedPaymentEligible**
**# 40**** – **Merchant is protected by PayPal&#39;s Seller Protection Policy for Unauthorised Payments.** Ineligible ****–** Merchant is not protected under the Seller Protection Policy.(Multiple values are separated by commas) |
| **feeAmount** | No | PayPal fee amount charged for the transaction. |
| **settleAmount** | No | Amount deposited in your PayPal account after a currency conversion. |
| **storeID** | No | Store identifier as entered in the transaction. |
| **terminalID** | No | Terminal identifier as entered in the transaction. |

The details will be returned as a nested record as described in section 1.5.8. The detail names are case sensitive.

  1.
## Transaction Lifecycle

PayPal transactions will use the normal Authorise, Capture life cycle as documented in appendix A-14.1 with the following differences. In addition, the PayPal **paymentAction** option can be included in the **checkoutOptions** field to alter the normal payment lifecycle further, to allow an Order, Authorise, Capture model or a straight Sale model to be specified.

    1.
### Order

If a **paymentAction** with a value of &#39;Order&#39; is sent, then PayPal will store the transaction but delay authorising it until instructed. To instruct PayPal to authorise the transaction, a further management request can be sent to the Gateway with an **action** of &#39;AUTHORISE&#39; and the **xref** of the transaction to authorise. Alternatively, the AUTHORISE command can be selected in the Merchant Management System (MMS). The transaction will be left in the &#39;received&#39; state.

    1.
### Authorise

If no **paymentAction** is specified or a **paymentAction** with a value of &#39;Authorize&#39; is sent, then PayPal will authorise the transaction on receipt as per a standard card transaction and you can capture it later if you used the **captureDelay** field. _Note that the value uses the PayPal spelling &#39;Authorize&#39;, and not the British spelling &#39;Authorise&#39;._

For the first three days (by default) of the authorisation, funds are reserved. This is known as the honour period. After the honour period, captures can still be attempted, but may be returned with insufficient funds.

Authorisations have a fixed expiry period of 29 days.

    1.
### Sale

If a **paymentAction** with a value of &#39;Sale&#39; is sent, then PayPal will immediately capture the transaction after authorisation. The transaction will be regarded as having been settled and you will not be able to capture it manually and it will not be sent for settlement that evening. The transaction will be left in either the **accepted** or **rejected** terminal states depending on whether PayPal accepted or rejected the transaction.

    1.
### Capture

Transactions that have been authorised by PayPal and not immediately settled due to a **paymentAction** of &#39;Sale&#39; will be able to be captured as normal.

Captures are sent to PayPal immediately and the PayPal response and the transaction will be left in either the **accepted** or **rejected** terminal state depending on whether PayPal accepted or rejected the capture request.

There is no need to wait for the nightly settlement batch to run as with normal card transactions. This means that it is not possible to change the amount to be captured or cancel the transaction one a capture has been requested.

Note: PayPal allows multiple captures where they sum the individual capture amounts – i.e. in a different manner from the Gateway&#39;s, where only a single capture operation can be processed.

    1.
### Refund

PayPal transactions can be refunded in the same way as normal card transactions. However, in the same way as capture requests, these will be sent to PayPal immediately and not batched up to be sent as part of the nightly settlement process. This means that the transaction will be left in either the **accepted** or **rejected** terminal state, depending on whether PayPal accepted or rejected the refund request.

Refunds can be made for full or partial amounts, with multiple refunds allowed up to the original authorised amount.

By default, PayPal allows a Merchant up to 60 days from the original authorised transaction date to perform refunds.

    1.
### Cancel

You should cancel any transactions that you do not wish to capture in order to prevent &#39;pending&#39; transactions on the Customer&#39;s PayPal account.

Authorisations should be cancelled when an initial authorisation was created to confirm the validity of funds during checkout, but the goods will not ship for a significant amount of time (\&gt;29 days). Cancelling the transaction will mean that you will have to contact the Customer for an alternative payment method.

All transactions must be completed by being captured or cancelled.

    1.
### Pending Payments

PayPal may put a transaction into a pending state when flagged for additional fraud review. This state is known to PayPal as payment review or IPR.

IPR transactions will be automatically cancelled by the Gateway and treated as referred transactions with a **responseCode** of **2** and a **responseMessage** indicating the reason that the transaction was put into a pending state. Unlike card referred transactions, an authorisation code cannot be obtained from PayPal verbally and then the transaction resent.

  1.
## Reference Transactions

PayPal does not allow ad hoc &#39;Card On File&#39; type repeat or recurring transactions using the **xref** of a reference transaction unless that transaction has specifically started a PayPal Billing Agreement.

If you want to be able to make future repeat or recurring transactions, then the initial transaction must include the **billingType** and **billingAgreementDescription** options in the **checkoutOptions** to identify this transaction as the start of a recurring billing sequence.

This will cause the Gateway to request PayPal to set up a Billing Agreement between you and the Customer. In this case, the PayPal Billing Agreement ID will be returned as part of the **checkoutDetails** and displayed on the Merchant Management System (MMS) as part of the payment details, so that you can easily see which PayPal transactions can be used for recurring billing.

1.
# Amazon Pay Transaction

  1.
## Background

Amazon Pay is an additional payment method that is available to all Merchants using the Gateway that have an Amazon Pay account.

To use Amazon Pay, you will be supplied with a separate Amazon Pay Merchant account that can be grouped with your main Merchant account using the account mapping facility as documented in appendix A-8. This allows transactions to be sent using your main Merchant Account and then routed automatically to the Amazon Pay Merchant Account in the same mapping group.

It allows you to offer payment via Amazon Pay in addition to normal card payments.

Amazon Pay transactions will appear in the Merchant Management System (MMS) alongside any card payments and can be captured, cancelled and refunded in the same way as card payments.

Amazon Pay transactions can also be used for recurring billing but require you to indicate in the initial transaction that it will be the basis for recurring billing and a billing agreement will be entered into between your Customer and Amazon Pay when they agree to the payment.

Amazon Pay transactions cannot be used for ad-hoc &#39;Card On File&#39; repeat transactions unless a billing agreement has been set up.

For more information on how to accept Amazon Pay transactions, please contact customer support.

**Amazon Pay is supported by the Hosted and Direct Integrations. It is not supported by the Batch Integration.**

  1.
## Benefits and Limitations

    1.
### Benefits

- Provides your customers with the flexibility of paying using their Amazon Pay account when this is more suitable to them.

- The Amazon Pay Checkout can be added as an overlay on the standard checkout to help improve conversion rates with an easier way to pay without customers leaving your website.

- There are no extra costs to add an Amazon Pay Merchant Account. However, you will still be liable for the Amazon Pay transaction fees.

- The full Amazon Pay transaction information is available and returned as part of the transaction.

- Transactions are controlled within the Merchant Management System (MMS) in the same manner as normal card transactions.

    1.
### Limitations

- You will need an Amazon Pay account.

- Recurring transactions are not supported unless part of a prearranged billing agreement.

- Independent refunds that are not tied to a previous sale transaction are not supported without prior agreement.

- Transactions require a browser in order to display the Amazon Pay Checkout widgets.

  1.
## Hosted Implementation

If a transaction is sent to the Hosted Integration using a **merchantID** that is part of a routing group containing an Amazon Pay Merchant, then the Hosted Payment Page will display an Amazon Pay payment button which, when clicked, will open the Amazon Pay Checkout and allow the Customer to pay using their Amazon Pay account.

To customise the Amazon Pay Checkout experience, you may send various options in the **Amazon PayCheckoutOptions** field in your initial request.

Additional information available from Amazon Pay will be made available in the **checkoutDetails** response field.

_Note: Custom Hosted Payment Pages might not support the displaying of the Amazon Pay Checkout button. If you have a custom page that doesn&#39;t support this, then you would need to contact support to have your Hosted Payment Page upgraded._

  1.
## Direct Implementation

Amazon Pay transactions require you to display an Amazon Pay Checkout to your Customer as part of the transaction flow. The transaction must be done in two stages, with the Checkout page being displayed between the stages. They can also optionally be done in three stages, allowing you to display an order confirmation after the Checkout page and before authorising the transaction. You can change the amount at this stage to allow for shipping costs when you know the confirmed delivery address the Customer selected as part of the Amazon Pay Checkout.

Amazon Pay do not provide a ready built Checkout page and require you to create one on your servers using the JavaScript widget toolkit they provide.

Amazon Pay supports the normal payment and management actions. This section explains how to make payment requests. Management requests are performed as detailed in section 3.

    1.
### Initial Request (Checkout Preparation)

To request that a transaction be processed via Amazon Pay, the request must contain a **paymentMethod** of &#39;Amazon Pay&#39; In addition, you may send **checkoutOptions** to customise the Checkout experience. When the Gateway receives this **paymentMethod** , assuming there are no other errors with the request, it will attempt to find a suitable Amazon Pay Merchant Account in the current account mapping group.

If the Gateway is unable to find a suitable account, then the transaction will be aborted, and it will respond with a **responseCode** of **66364 (INVALID PAYMENTMETHOD)**.

Otherwise, the Gateway will respond with a **responseCode** of **65826 (CHECKOUT REQUIRED)** and the response will include a **checkoutURL** field containing the URL required to load the Amazon Pay JavaScript Widgets; and a **checkoutRequest** containing any data required by those Widgets. The response will also contain a unique **checkoutRef** that must be echoed back in the continuation requests.

At this point, your server must create an Amazon Pay Checkout page using their JavaScipt Widgets. Further details on how to use the Widgets are provided in the Amazon Pay guide at [https://developer.Amazon Pay.com/docs/classic/express-checkout/in-context/enable\_in\_context\_checkout/](https://pay.amazon.com/us/developer/documentation/lpwa/201954000).

    1.
### Continuation Request (Checkout Details and Authorise)

On completion of the Amazon Pay Widgets, the Merchant should send the information created by the Widgets to the Gateway together with a **status** value. If the Checkout was successful, the status will be &#39;success&#39;; alternatively, if the Checkout was cancelled, the status will be &#39;cancel&#39;. Any **accessToken** generated by the Amazon Pay Login Widget; **orderReferenceID** , generated by the Wallet or Address Widgets; and **billingAgreementID** generated by the optional Billing Widget, must be added to the **checkoutResponse** field and sent in a new request to the Gateway. The **checkoutResponse** field can be sent either as a URL query string; as a JSON encoded string; or as an array of parameters. This new request will load the Checkout details, including any purchaser and delivery address details as required, and send the transaction to Amazon Pay for authorisation, returning the result as in the case of a normal authorisation transaction. The new request must contain the **checkoutRef** received in the initial response.

    1.
### Separate Checkout Details and Authorisation Requests

You can choose to obtain the Checkout details before sending the transaction for authorisation by sending the **checkoutOnly** field in the above continuation request. If this field is sent with a value of &#39;Y&#39; then the Gateway will load the Checkout details and then return them to you without sending the request for authorisation. You can then display them and/or adjust the amount, for example, according to delivery charges appropriate to the received delivery address. You should then send a new request containing the **checkoutRef** received to continue the transaction and authorise it.

Note: this stage can be repeated multiple times by including the **checkoutOnly** field with a value of &#39;Y&#39; each time. To complete the transaction, the final request must not contain the **checkoutOnly** field or it must not have a value of &#39;Y&#39;.

  1.
## Request Fields

    1.
### Initial Request (Hosted and Direct Integration)

These fields should be sent in addition to basic request fields in section 2.1 excluding any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **paymentMethod** | Yes
# 41
 | Must contain the value &#39;Amazon Pay&#39; in lower case letters only. |
| **checkoutRedirectURL** | No
# 42
 | Reserved for future use. |
| **checkoutOptions** | No
# 43
 | Record containing options used to customise the Amazon Pay Checkout. Refer to section [22.5.3](#_Checkout_Options_(Hosted) for values. |
| **Amazon PayCheckoutOptions** | No
# 44
 | Record containing options used to customise the Amazon Pay Checkout. Refer to section [22.5.3](#_Checkout_Options_(Hosted) for values. |

    1.
### Continuation Request (Direct Integration)

These fields may be sent alone
# 45
.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutRef** | Yes
 | Unique reference return in the initial response. |
| **checkoutResponse** | Yes | The data received from the Amazon Pay Checkout Widgets together with a status value. |
| **checkoutOnly** | No | Pass **Y** to complete the processing as far as the next Checkout stage and then return with the loaded Checkout details. |

    1.
### Checkout Options (Hosted and Direct Integration)

The following options may be sent in the **Amazon PayCheckoutOptions** Hosted Integration field or the **checkoutOptions** Direct Integration field to customise the Amazon Pay Checkout.

| **Field Name** | **Description** |
| --- | --- |
| **billingAgreementRequired** | Can be used to specify that a billing agreement must be started. Alternatively, the **rtAgreementType** standard integration field can be used with a value of &#39;recurring&#39; or &#39;instalment&#39;. |
| --- | --- |
| **shippingAddressRequired** | Indication that the shipping address is required, and the Address Checkout Widget will be used. |
| **sellerOrderID** | The Merchant specified identifier for this order. If not sent, then any value in the **merchantOrderRef** standard integration field is used. |
| **sellerNote** | Represents a description of the order that is displayed in emails to the buyer. |
| **sellerAuthorizationNote** | A description for the authorisation transaction that is shown in emails to the buyer. |
| **sellerCaptureNote** | A description for the capture that is displayed in emails to the buyer. |
| **sellerBillingAgreementID** | The Merchant specified identifier for this billing agreement. If not sent, then any value in the **rtPolicyRef** standard integration field is used. |
| **customInformation** | Any additional information that you want to include with this order reference |
| **supplementaryData** | Supplementary data. |
| **softDescriptor** | The description to be shown on the buyer&#39;s payment statement |
| **billingAgreementRequired** | Can be used to specify that a billing agreement must be started. Alternatively, the **rtAgreementType** standard integration field can be used with a value of &#39;recurring&#39; or &#39;instalment&#39;. |
| **shippingAddressRequired** | Indication that the shipping address is required, and the Address Checkout Widget will be used. |

For further information on the options refer to the Amazon Pay API Reference Guide: [https://pay.amazon.com/us/developer/documentation/apireference/201751630](https://pay.amazon.com/us/developer/documentation/apireference/201751630)

The options should be passed as either a nested record or serialised record as described in section 1.5.8. The option names are case sensitive.

    1.
### Response Fields
    2.
### Initial Response (Direct Integration)

These fields will be returned in addition to the request fields from section [22.5.1](#_Initial_Request_(Hosted) and the basic response fields in section 2.2minus any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutRef** | Yes
 | Unique reference required to continue this transaction when the Amazon Pay Checkout has completed. |
| **checkoutName** | Yes | Unique name of the Checkout. For Amazon Pay this is the value **Amazon Pay**. |
| **checkoutURL** | Yes | URL required to load the Amazon Pay JavaScript Widgets. |
| **checkoutRequest** | No | Information required for the Amazon Pay Widgets such as:
- **merchantID** – Amazon Pay merchant ID
- **clientID** – Amazon Pay client ID
- **sandbox** – true if Amazon Pay sandbox
- **region** – Amazon Pay API region code
- **scope** – Login Widget scope parameter
 |
| **checkoutOptions** | No | Any Checkout options passed in the request. |
| **acquirerResponseDetails** | Yes | Details about the Amazon Pay response containing any error messages and codes. This can be used together with the normal **responseCode** and **responseMessage** response fields to further determine the reason for any failure. |

    1.
### Continuation Response (Direct Integration)

These fields will be returned in addition to the request fields from section [22.5.2](#_Continuation_Request_(Direct), the initial response fields in section 20.6.1 and the basic response fields in section 2.2 minus any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutRef** | Yes
 | Provided if **checkoutOnly** was used in the continuation response to indicate that a further request will be sent to finalise the transaction. |
| **checkoutName** | Yes | Unique name of the Checkout. For Amazon Pay this is the value **Amazon Pay**. |
| **checkoutDetails** | Yes | Record containing values made available by the Amazon Pay Checkout. Refer to section 21.5.7 for values. |
| **customer** _ **XXXX** _ | No
# 0
 | Customer details if provided by the Amazon Pay Checkout as documented in section 17.1 |
| **delivery** _ **XXXX** _ | No | Delivery details if provided by the Amazon Pay Checkout as documented in section 17.4 |
| **receiver** _ **XXXX** _ | No | Buyer details if provided by Amazon Pay as documented in section 17.5. Amazon Pay will usually provide the buyer&#39;s name, postcode and email only, which are returned in the **receiverName** , **receiverPostcode** and **receiverEmail** fields accordingly |
| **acquirerResponseDetails** | Yes | Details about the Amazon Pay response containing any error messages and codes. This can be used together with the normal **responseCode** and **responseMessage** response fields to further determine the reason for any failure. |

    1.
### Checkout Details (Hosted and Direct Integration)

The **checkoutDetails** field included in the response above will contain the following values and any further values received from Amazon Pay allowing the Merchant to see the full Amazon Pay order information.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **referenceID** | No | Amazon Pay reference id. Either the **orderReferenceID** or the **billingReferenceID** where appropriate. |
| --- | --- | --- |
| **accessToken** | No | Amazon Pay order reference id as sent in the continuation request **checkoutResponse** data. |
| **bilingAgreementID** | No | Amazon Pay order reference id as sent in the continuation request **checkoutResponse** data. |
| **orderReferenceID** | No | Amazon Pay order reference id as sent in the continuation request **checkoutResponse** data. |

The details will be returned as a nested record as described in section 1.5.8. The detail names are case sensitive.

  1.
## Transaction Lifecycle

Amazon Pay transactions will use the normal Authorise, Capture life cycle as documented in appendix A-14.1 with the following differences.

    1.
### Capture

Captures made by the Direct Integration or Merchant Management System (MMS) are sent to Amazon Pay immediately. The transaction will be left in either the **accepted** or **rejected** terminal state depending on whether Amazon Pay accepted or rejected the capture request. Unlike card payments, captures do not flag the transaction to be included in the nightly settlement batch and therefore when done they cannot be redone. This means that it is not possible to change the amount to be captured or cancel the transaction when a capture has been requested.

Captures that are not explicitly performed such as normal transactions or those with a captureDelay are still done as part of the nightly settlement batch.

Transactions that are not captured within 3 days will be placed in a pending state in the Amazon Pay system which is reflected as the **tendered** state in the Gateway and will show on the Merchant Management System as being settled.

    1.
### Refund Sale

Amazon Pay transactions can be refunded the same as normal card transactions however, like capture requests, these will be sent to Amazon Pay immediately and not batched up and sent as part of the nightly settlement process. This means the transaction will be left in either the **accepted** or **rejected** terminal state depending on whether Amazon Pay accepted or rejected the refund request.

Refunds can be made for full or partial amounts, with multiple refunds allowed up to the original authorised amount.

  1.
## Reference Transactions

Amazon Pay does not allow ad hoc &#39;Card On File&#39; type repeat or recurring transactions using the **xref** of a reference transaction unless that transaction has specifically started a Amazon Pay Billing Agreement.

If you want to be able to make future repeat or recurring transactions, then the initial transaction must include an **rtAgreementType** of **recurring** or **instalment**. Alternatively, the **billingAgreementRequired** option can be included in the **checkoutOptions** to identify this transaction as the start of a recurring billing sequence.

This will cause the Gateway to request Amazon Pay setup a Billing Agreement between you and the Customer. In this case the Amazon Pay Billing Consent Widget must be used in the Checkout and the **billingAgreementID** it creates sent in the **checkoutResponse** data in the continuation request. Any billing agreement ID will be displayed on the Merchant Management System (MMS) as part of the payment details so that you can easily see which Amazon Pay transactions can be used for recurring billing.

1.
# PPRO Transactions

  1.
## Background

PPRO is an additional payment method that is available to all Merchants using the Gateway that have a PPRO account.

To use PPRO, you will be supplied with a separate PPRO Merchant account that can be grouped with your main Merchant Account using the account mapping facility as documented in appendix A-8. This allows transactions to be sent using your main Merchant Account and then routed automatically to the PPRO Merchant Account in the same mapping group.

PPRO is an Acquirer that offers many Alternative Payment Methods (APM), that you can then offer to your Customers.

E-wallets, SMS payments and PSP services are some of the many payment methods PPRO support (e.g. Alipay, EasyPay, Bancontact). This could allow a business to facilitate overseas transactions or alternative payment methods using a different payment method suitable for that country or business plan.

All transactions created with this payment method will appear in the Merchant Management System (MMS) together with the payment method that was used to process the transaction.

PPRO transactions cannot be used for ad-hoc &#39;Card On File&#39; repeat transactions or for recurring billing.

For more information on how to accept PPRO transactions please contact customer support.

**PPRO is supported by the Hosted and Direct Integrations. It is not supported by the Batch Integration.**

  1.
## Benefits and Limitations

    1.
### Benefits

- Multiple alternative payment methods could be used.

- Expands range of payment methods for international use.

- Supports a variety of e-wallets, SMS and PSP&#39;s.

- Ability to perform refunds on supported payment methods.

- Transactions are controlled within the Merchant Management System (MMS) in the same manner as normal card transactions.

    1.
### Limitations

- You will need a PPRO account.

- Payment authorisation is not always instantaneous and may require additional &#39;QUERY&#39; requests.

- An alternative payment method may only support one or a limited set of currencies or countries.

- Alternative payment methods require a browser in order to display their Checkout.

  1.
## Hosted Implementation

If a transaction is sent to the Hosted Integration using a **merchantID** which is part of a routing group containing a PPRO Merchant Account, then the Hosted Payment Page will show alternative payment method buttons for each payment method listed in the **allowedPaymentMethods** field. When clicked on the Hosted Payment Page may request further details from the Customer before opening the APM Checkout allowing the Customer to pay using that APM.

To customise the alternative payment methods checkout experience, you may send various options in the **pproCheckoutOptions** field in your initial request.

Additional information available from PPRO will be made available in the **checkoutDetails** response field.

_Note: Custom Hosted Payment Pages might not support the displaying of the Alternative Payment Methods. If you have a custom page that doesn&#39;t support this, then you would need to contact support to have your Hosted Payment Page upgraded._

  1.
## Direct Implementation

PPRO transactions require you to display the alternative payment method&#39;s Checkout to your Customer as part of the transaction flow. The transaction must be done in two stages with the Checkout being displayed between the stages.

PPRO supports only supports the SALE, REFUND\_SALE actions. This section explains how to make payment requests. Management request are performed as detailed in section 3.

    1.
### Payment Request

To request that a transaction be processed via PPRO the request must contain a **paymentMethod** of &#39;ppro._XXXX_&#39;, where _XXXX_ is the PPRO payment method tag listed in section 22.4.3 below. The request must also have a **checkoutRedirectURL** containing the URL of a page on your server to return to when the alternative payment method&#39;s Checkout is closed. In addition, you may send **checkoutOptions** to provide further custom fields requited by the alternative payment method as details in section 22.4.2 below.

When the Gateway receives these fields, assuming there are no other errors with the request, it will attempt to find a suitable PPRO Merchant Account in the current account mapping group.

If the Gateway is unable to find a suitable account, then the transaction will be aborted, and it will respond with a **responseCode** of **66364 (INVALID PAYMENTMETHOD)**.

Otherwise the Gateway will respond with a **responseCode** of **65826 (CHECKOUT REQUIRED)** and included in the response will be a **checkoutURL** field containing the URL that the buyer&#39;s browser should be redirected to in order to complete the payment. The response will also contain a unique **checkoutRef** which must be echoed back in the continuation requests.

On completion of the third-party payment the browser will be directed to the **checkoutRedirectURL** you provided, complete with information about the payment in a HTTP POST request. The posted data will contain a **checkoutResponse** field that will contain any specific response data for the payment method.

    1.
### Payment Specific Fields

Most of the information required by the alternative payment methods can be supplied using the standard Gateway request fields. However, there may be specific mandatory fields required by a payment method which are not available using the standard fields. In these cases, these fields can be sent in the **checkoutOptions** data.

For example, most European services may require the **nationalid** and **consumerref** fields.

Recurring transactions will require the use of **iban** (optionally **sequencetype** ) and in follow-uppayments; **mandatereference** , **mandatesignaturedate** , and **sequencetype**.

Customer support will be able to help guide you on any missing fields you may find the transaction will come up with a **responseCode** of **65550 (PROCESSOR\_ERROR -** Invalid request data).

    1.
### Payment Method Tags

To specify which alternative payment method is required you need to send the

**paymentMethod** field with a value using the format is &#39;ppro._XXXX&#39;_, where _XXXX_ is the alternative payment method&#39;s tag name as assigned by PPRO.

For example; to use the alternative payment method AstroPay Card that has a tag name of &quot;astropaycard&quot; (all lowercase); the resulting payment method code would be &quot;ppro.astropaycard&quot;. This allows the Gateway to know that you&#39;re attempting to use AstroPay Card using the PPRO payment method.

The table below is a guide to the tag names available. This list is fluid as PPRO add and remove methods.

_If you know of a payment method that is not on this list or the payment method cannot be used; please contact customer support for advice._

| **Tag** | **Name** |
| --- | --- |
| **affinbank** | Affin bank |
| **alipay** | AliPay |
| **ambank** | AmBank |
| **argencard** | Argencard |
| **astropaycard** | AstroPay Card |
| **astropaydirect** | AstroPay Direct |
| **aura** | Aura |
| **baloto** | Baloto |
| **banamex** | Banamex |
| **bancodobrasil** | Banco do Brasil |
| **bancodechile** | Banco de Chile |
| **bancodeoccidente** | Banco de Occidente |
| **bancomer** | Bancomer |
| **bankislam** | Bank Islam |
| **bcmc** | Bancontact |
| **bitpay** | Bitpay |
| **boleto** | Boleto Bancario |
| **bradesco** | Bradesco |
| **cabal** | Cabal |
| **cartaomercadolivre** | Cartao Mercado Livre |
| **carulla** | Carulla |
| **ccauth** | Credit/Debit Card |
| **ccweb** | Credit/Debit Card |
| **cencosud** | Cencosud |
| **cimbclicks** | CIMB Clicks |
| **cmr** | CMR |
| **davivienda** | Davivienda |
| **directpay** | Sofortüberweisung (Direct Pay) |
| **dragonpay** | Dragonpay |
| **easypay** | EasyPay |
| **efecty** | Efecty |
| **elo** | Elo |
| **empresedeenergia** | Emprese de Energia |
| **enets** | eNETS |
| **entercash** | Entercash |
| **eps** | EPS |
| **estonianbanks** | Estonian Banks |
| **giropay** | Giropay |
| **hipercard** | Hipercard |
| **hongleongbank** | Hong Leong Bank |
| **ideal** | iDEAL |
| **instanttransfer** | Instant Transfer |
| **int\_payout** | International Pay-Outs |
| **itau** | Itau |
| **latvianbanks** | Latvian Banks |
| **lithuanianbanks** | Lithuanian Banks |
| **magna** | Magna |
| **maxima** | Maxima |
| **maybanktwou** | Maybank2u |
| **multibanco** | Multibanco |
| **mybank** | MyBank |
| **myclearfpx** | MyClear FPX |
| **naranja** | Naranja |
| **narvesen** | Narvesen |
| **nativa** | Nativa |
| **oxxo** | OXXO |
| **p24** | Przelewy24 |
| **p24payout** | Przelewy24 Payout |
| **pagofacil** | Pago Facil |
| **paypost** | PayPost |
| **paysafecard** | Paysafe Card |
| **paysbuy** | Paysbuy |
| **paysera** | Paysera |
| **payu** | PayU |
| **perlas** | Perlas Terminals |
| **poli** | OLI |
| **presto** | Presto |
| **pse** | PSE |
| **pugglepay** | Pugglepay |
| **qiwi** | QIWI |
| **qiwipayout** | QIWI Payout |
| **rapipago** | Rapipago |
| **redpagos** | Redpagos |
| **rhbbank** | RHB Bank |
| **safetypay** | SafetyPay |
| **santander** | Santander |
| **sepadirectdebit** | SEPA DirectDebit |
| **sepapayout** | SEPA Payout |
| **seveneleven** | Seveneleven (7eleven) |
| **singpost** | SingPost |
| **skrill** | Skrill |
| **surtimax** | Surtimax |
| **tarjetashopping** | Tarjeta Shopping |
| **trustly** | Trustly |
| **trustpay** | TrustPay |
| **unionpay** | UnionPay |
| **verkkopankki** | Verkkopankki – Finish Online Banking |
| **webpay** | Webpay |
| **yellowpay** | Yellow Pay |

  1.
## Request Fields

    1.
### Initial Request (Hosted and Direct Integration)

These fields should be sent in addition to the basic request fields in section 2.1 excluding any card details.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **paymentMethod** | Yes
# 46
 | Payment method to be used with PPRO (e.g. **ppro.astropay** , **ppro.alipay** , etc.). |
| **checkoutRedirectURL** | Yes
# 47
 | URL on Merchant&#39;s server to return to when the Alternative Payment Method&#39;s Checkout is closed. |
| **checkoutOptions** | No
# 48
,
# 49
 | Record containing options used to customise the alternative payment methods Checkout. Refer to section 22.5.2 for values. |
| **pproCheckoutOptions** | No
# 50
,4 | Record containing options used to customise the alternative payment methods Checkout. Refer to section 22.5.2 for values. |

    1.
### Checkout Options (Hosted and Direct Integration)

The following options may be sent in the **pproCheckoutOptions** Hosted Integration field or the **checkoutOptions** Direct Integration field to customise the Checkout.

| **Field Name** | **Description** |
| --- | --- |
| **nationalid** | Consumer&#39;s national ID (up to 30 characters). |
| **consumerref** | Unique reference identifying the consumer within 1 to 20 characters and a format of A-Za-z0-9.%,&amp;/+\*$- |
| **siteid** | Unique site identifier. Required for clients serving multiple points of sale and forwarded onwards whilst using the qiwi payment method. |
| **iban** | Valid IBAN of consumer/destination account. |
| **sequencetype** | Sequence type of the direct debit.
Possible values are: **oneOff** – The direct debit is executed once (_ **default** _) **first** – First direct debit in a series of recurring ones |
| **mandatereference** | Mandate reference as returned on the first transaction in the sequence (found from mandatereference in checkoutDetails) |
| **mandatesignaturedate** | Date of the initial transaction. |
| **bic** | Valid BIC (8 or 11 alphanumeric letters) – optionally supplied to skip the bank selection page (by using the bank referenced by BIC as supplied) |
| **clientip** | Optional IP address of the consumer during checkout using Trustly (127.0.0.1 is not allowed!) |
| **address** | Customer&#39;s billing address
# 51
 |
| **city** | Customer&#39;s billing city1 |
| **phone** | Customer&#39;s phone1 |
| **mobilephone** | Customers mobile phone1 |
| **dob** | MCC 6012 Date of Birth1 |
| **dynamicdescriptor** | Statement narrative1 |

  1.
## Response Fields

    1.
### Initial Response (Direct Integration)

The fields below will be returned in addition to the basic response fields in section 2.2 for the start of a PPRO transaction and the PPRO checkout process.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutRef** | Yes
 | Unique reference required to continue this transaction when the PPRO Checkout has completed. |
| **checkoutName** | Yes
 | The **paymentMethod** you used to identify the PPRO payment method. |
| **checkoutRedirectURL** | Yes
 | The URL to redirect the Customer to, to start the checkout process. |
| **checkoutOptions** | Yes | The same **checkoutOptions** used for the request. |
| **checkoutDetails** | Yes
 | Additional information provided from the payment method used during checkout. |
| **checkoutRef** | Yes
 | The unique reference required to continue the transaction when PPRO checkout is complete. |
| **checkoutRequest** | Yes
 | Containing the redirect secret, checksum and request status. |

    1.
### Completion Response (Hosted and Direct Integration)

Fields from the initial response in the previous section may be present as well as the fields below and will not contain any card details.

| **Field name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkoutResponse** | Yes
 | Containing additional information provided by the Checkout. Any change in the payment&#39;s status will be given in **responseMessage** and **responseCode**
 **# 52** |
| **checkoutStatus** | Yes
 | A string containing the result of the checkout process. **This is not used to identify the transaction&#39;s payment status.** |

    1.
### Notifications and &quot;Tendered&quot; Payments

Whilst some payment methods give an immediate payment status (i.e. direct card payment methods rather than SMS and e-wallet systems), some payments may come back with the status of &#39;tendered&#39;. At this time, online shopping modules will not be able to monitor the transaction status. The use of a QUERY request may be of use as seen in section 1.7.8. Please ask customer support in this matter who will be able to give more information and may be able to provide better advice for your situation.

Notifications from PPRO regarding the payment status, seconds, minutes or hours after the checkout will automatically update the transaction status.

1.
# Digital Wallet Transactions

  1.
## Background

The Gateway currently supports payments made using the following Digital Wallets:

- Google Pay™
- Apple Pay

These are collectively known as &#39;The Pays&#39;.

These wallets can be used to enhance mobile purchasing experiences for customers with supported devices and produce a payment token which can be passed to the Gateway instead of the Cardholder&#39;s actual card details.

You can use these wallets with any Merchant Account that has been configured to accept them.

For more information on how to accept payment tokens, please contact customer support.

**Digital Wallets are currently supported by the Direct Integration only. They are not supported by the Hosted or Batch Integration.**

**Note, both Apple Pay and Google Pay are available via accredited Acquirers only.**

  1.
## Benefits and Limitations

    1.
### Benefits

- The payment details are stored externally to the Gateway and can be used with any Merchant that supports the appropriate payment tokens.

- Customers can select from previously stored payment details, making the checkout process more streamlined, resulting in fewer abandoned carts and thus increasing sales.

- Compatible with existing card base fraud solutions such as Address Verification Service (AVS), 3-D Secure and third-party fraud providers.

- There are no extra costs to add these payment methods to your Gateway account.

- The transactions are controlled within the Merchant Management System (MMS) in the same manner as normal card transactions.

    1.
### Limitations

- Your Customer will need a digital wallet enabled device with some stored card details in order to make full use of this payment method.

- The device needs to be integrated with the gateway using third-party provided software.

- Repeat transactions using the retrieved payment details are supported.

  1.
## Configuration

The Merchant Account being used for the payments must be configured with your Digital Wallet credentials so that the Gateway can decrypt the payment token.

    1.
### Apple Pay configuration

Apple Pay requires the Gateway to generate public/private key pair and then the public key must be shared with your Android Pay enabled application in the guise of an Apple Pay _payment process certificate_.

To configure an Apple Pay [_payment processing certificate_](https://help.apple.com/developer-account/#/devb2e62b839?sub=devf31990e3f) you must have enrolled in the [Apple Developer Program](https://developer.apple.com/programs/) and [created a unique Apple Pay merchant identifier](https://help.apple.com/developer-account/#/devb2e62b839?sub=dev103e030bb).

The _payment processing certificate_ is associated with your merchant identifier and used to encrypt payment information. The certificate expires every 25 months. If the certificate is revoked, you can recreate it.

You would normally use the Merchant Management System (MMS) to configure your [payment processing certificate](https://help.apple.com/developer-account/#/devb2e62b839?sub=devf31990e3f) by following the steps outlined below:

1. Open the [Apple Developer Certificates, Identifiers &amp; Profiles](https://developer.apple.com/account/resources) webpage and select &#39;Identifiers&#39; from the sidebar.
2. Under &#39;Identifiers&#39;, select &#39;Merchant IDs&#39; using the filter in the top-right.
3. On the right, select your merchant identifier.
4. Under &#39;Apple Pay Payment Processing Certificate&#39;, click &#39;Create Certificate&#39;.
5. Download our [certificate signing request](https://www.cardstream.net/admin/preferences.php?process=applepay-csr&amp;ajax=1) (CSR) from the MMS and save to a file.
6. Click &#39;Choose File&#39; and select the CSR you just downloaded.
7. Click &#39;Continue&#39;.
8. Click &#39;Download&#39; to download the _payment processing certificate_ and save to a file.
9. Upload the payment processing certificate to the MMS.

    1.
### Google Pay configuration

Google Pay requires no specific configuration however you must use our Gateway identifier of &#39; **crst&#39;** and the correct Merchant Account identifier when configuring your Google Pay enabled application.

  1.
## Hosted Implementation

Transactions using Digital Wallet payment methods are currently not supported by the Hosted Integration.

  1.
## Direct Implementation

Digital Wallet payments require the secure payment token generated by the wallet enabled application to be sent to the Gateway in the **paymentToken** field. The type of token must be specified by also sending the **paymentMethod** field with a value of &#39; **applepay**&#39; or **&#39;googlepay&#39;**.

  1.
## Request Fields

These fields should be sent instead of the standard card details together with the fields in section 2.1.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **paymentMethod** | Yes | The type of payment token sent.
**applepay** – to indicate an Apple Pay token **googlepay** – to indicate a Google Pay token |
| **paymentToken** | Yes | Must contain the secure payment token produced by the wallet enabled application. |

##


  1.
## Response Fields

There are no additional response fields.

            1. **Response Codes**

The Gateway will always issue a **responseCode** to report the status of the transaction. These codes should be used rather than the **responseMessage** field to determine the outcome of a transaction.

A zero response code always indicates a successful outcome.

Response codes are grouped as follows, the groupings are for informational purposes only and not all codes in a group are used:

| **Acquirer (FI) Error codes: 1-99** |
| --- |
| **Code** | **Description** |
| **0** | Successful / authorised transaction.
Any code other than **0** indicates an unsuccessful transaction. |
| **1** | Card referred – Refer to card issuer. |
| **2** | Card referred – Refer to card issuer, special condition. |
| **4** | Card declined – Keep card. |
| **5** | Card declined. |
| **30** | An error occurred. Check **responseMessage** for more detail. |

| **General Error Codes: 65536 - 65791** |
| --- |
| **Code** | **Description** |
| **65536** | Transaction in progress. Contact customer support if this error occurs |
| --- | --- |
| **65537** | Reserved for future use. Contact customer support if this error occurs |
| **65538** | Reserved for future use. Contact customer support if this error occurs |
| **65539** | Invalid Credentials: **merchantID** is unknown |
| **65540** | Permission denied: caused by sending a request from an unauthorised IP address |
| **65541** | Action not allowed: the transaction state or Acquirer doesn&#39;t support this action |
| **65542** | Request Mismatch: fields sent while completing a request do not match initially requested values. Usually due to sending different card details to those used to authorise the transaction when completing a 3-D Secure transaction or performing a REFUND\_SALE transaction. |
| **65543** | Request Ambiguous: request could be misinterpreted due to inclusion of mutually exclusive fields |
| **65544** | Request Malformed: couldn&#39;t parse the request data |
| **65545** | Suspended Merchant account |
| **65546** | Currency not supported by Merchant |
| **65547** | Request Ambiguous, both **taxValue** and **discountValue** provided when should be one only |
| **65548** | Database error |
| **65549** | Payment processor communications error |
| **65550** | Payment processor error |
| **65551** | Internal Gateway communications error |
| **65552** | Internal Gateway error |
| **65553** | Encryption error. |
| **65554** | Duplicate request. Refer to Section 14. |
| **65555** | Settlement error. |
| **65556** | AVS/CV2 Checks are not supported for this card (or Acquirer) |
| **65557** | IP Blocked: Request is from a banned IP address |
| **65558** | Primary IP blocked: Request is not from one of the primary IP addresses configured for this Merchant Account |
| **65559** | Secondary IP blocked: Request is not from one of the secondary IP addresses configured for this Merchant Account |
| **65560** | Reserved for future use. Contact customer support if this error occurs |
| **65561** | Unsupported Card Type: Request is for a card type that is not supported on this Merchant Account |
| **65562** | Unsupported Authorisation: External authorisation code **authCode** has been supplied and this is not supported for the transaction or by the Acquirer |
| **65563** | Request not supported: The Gateway or Acquirer does not support the request |
| **65564** | Request expired: The request cannot be completed as the information is too old |
| **65565** | Request retry: The request can be retried later |
| **65566** | Test Card Used: A test card was used on a live Merchant Account |
| **65567** | Unsupported card issuing country: Request is for a card issuing country that is not supported on this Merchant Account |
| **65568** | Unsupported payment type: Request uses a payment type which is not supported on this Merchant Account |

| **3-D Secure Error Codes: 65792 - 66047** |
| --- |
| **Code** | **Description** |
| **65792** | 3-D Secure transaction in progress. Contact customer support if this error occurs |
| --- | --- |
| **65793** | Unknown 3-D Secure Error |
| **65794** | 3-D Secure processing is unavailable. Merchant account doesn&#39;t support 3-D Secure |
| **65795** | 3-D Secure processing is not required for the given card |
| **65796** | 3-D Secure processing is required for the given card |
| **65797** | Error occurred during 3-D Secure enrolment check |
| **65798** | Reserved for future use. Contact customer support if this error occurs |
| **65799** | Reserved for future use. Contact customer support if this error occurs |
| **65800** | Error occurred during 3-D Secure authentication check |
| **65801** | Reserved for future use. Contact customer support if this error occurs |
| **65802** | 3-D Secure authentication is required for this card |
| **65803** | 3-D Secure enrolment or authentication failure and Merchant 3-D Secure preferences are to STOP processing |

| **Missing Request Field Error Codes: 66048 - 66303** |
| --- |
| **Code** | **Description** |
| **66048** | Missing request. No data posted to integration URL |
| --- | --- |
| **66049** | Missing **merchantID** field |
| **66050** | Reserved for future use. Contact customer support if this error occurs |
| **66051** | Reserved for internal use. Contact customer support if this error occurs |
| **66052** | Reserved for internal use. Contact customer support if this error occurs |
| **66053** | Reserved for internal use. Contact customer support if this error occurs |
| **66054** | Reserved for internal use. Contact customer support if this error occurs |
| **66055** | Missing **action** field |
| **66056** | Missing **amount** field |
| **66057** | Missing **currencyCode** field |
| **66058** | Missing **cardNumber** field |
| **66059** | Missing **cardExpiryMonth** field |
| **66060** | Missing **cardExpiryYear** field |
| **66061** | Missing **cardStartMonth** field (reserved for future use) |
| **66062** | Missing **cardStartYear** field (reserved for future use) |
| **66063** | Missing **cardIssueNumber** field (reserved for future use) |
| **66064** | Missing **cardCVV** field |
| **66065** | Missing **customerName** field |
| **66066** | Missing **customerAddress** field |
| **66067** | Missing **customerPostCode** field |
| **66068** | Missing **customerEmail** field |
| **66069** | Missing **customerPhone** field (reserved for future use) |
| **66070** | Missing **countyCode** field |
| **66071** | Missing **transactionUnique** field (reserved for future use) |
| **66072** | Missing **orderRef** field (reserved for future use) |
| **66073** | Missing **remoteAddress** field (reserved for future use) |
| **66074** | Missing **redirectURL** field |
| **66075** | Missing **callbackURL** field (reserved for future use) |
| **66076** | Missing **merchantData** field (reserved for future use) |
| **66077** | Missing **origin** field (reserved for future use) |
| **66078** | Missing **duplicateDelay** field (reserved for future use) |
| **66079** | Missing **itemQuantity** field (reserved for future use) |
| **66080** | Missing **itemDescription** field (reserved for future use) |
| **66081** | Missing **itemGrossValue** field (reserved for future use) |
| **66082** | Missing **taxValue** field (reserved for future use) |
| **66083** | Missing **discountValue** field (reserved for future use) |
| **66084** | Missing **taxDiscountDescription** field (reserved for future use) |
| **66085** | Missing **xref** field (reserved for future use) |
| **66086** | Missing **type** field (reserved for future use) |
| **66087** | Missing **signature** field (field is required if message signing is enabled) |
| **66088** | Missing **authorisationCode** field (reserved for future use) |
| **66089** | Missing **transactionID** field (reserved for future use) |
| **66090** | Missing **threeDSRequired** field (reserved for future use) |
| **66091** | Missing **threeDSMD** field (reserved for future use) |
| **66092** | Missing **threeDSPaRes** field |
| **66093** | Missing **threeDSECI** field |
| **66094** | Missing **threeDSCAVV** field |
| **66095** | Missing **threeDSXID** field |
| **66096** | Missing **threeDSEnrolled** field |
| **66097** | Missing **threeDSAuthenticated** field |
| **66098** | Missing **threeDSCheckPref** field |
| **66099** | Missing **cv2CheckPref** field |
| **66100** | Missing **addressCheckPref** field |
| **66101** | Missing **postcodeCheckPref** field |
| **66102** | Missing **captureDelay** field |
| **66103** | Missing **orderDate** field |
| **66104** | Missing **grossAmount** field |
| **66105** | Missing **netAmount** field |
| **66016** | Missing **taxRate** field |
| **66016** | Missing **taxReason** field |
| **66160** | Missing **cardExpiryDate** field |
| **66161** | Missing **cardStartDate** field |

| **Invalid Request Field Error Codes: 66304 - 66559** |
| --- |
| **Code** | **Description** |
| **66304** | Invalid request |
| --- | --- |
| **66305** | Invalid **merchantID** field |
| **66306** | Reserved for future use. Contact customer support if this error occurs |
| **66307** | Reserved for internal use. Contact customer support if this error occurs |
| **66308** | Reserved for internal use. Contact customer support if this error occurs |
| **66309** | Reserved for internal use. Contact customer support if this error occurs |
| **66310** | Reserved for internal use. Contact customer support if this error occurs |
| **66311** | Invalid **action** field |
| **66312** | Invalid **amount** field |
| **66313** | Invalid **currencyCode** field |
| **66314** | Invalid **cardNumber** field |
| **66315** | Invalid **cardExpiryMonth** field |
| **66316** | Invalid **cardExpiryYear** field |
| **66317** | Invalid **cardStartMonth** field |
| **66318** | Invalid **cardStartYear** field |
| **66319** | Invalid **cardIssueNumber** field |
| **66320** | Invalid **cardCVV** field |
| **66321** | Invalid **customerName** field |
| **66322** | Invalid **customerAddress** field |
| **66323** | Invalid **customerPostCode** field |
| **66324** | Invalid **customerEmail** field |
| **66325** | Invalid **customerPhone** field |
| **66326** | Invalid **countyCode** field |
| **66327** | Invalid **transactionUnique** field (reserved for future use) |
| **66328** | Invalid **orderRef** field (reserved for future use) |
| **66329** | Invalid **remoteAddress** field |
| **66330** | Invalid **redirectURL** field |
| **66331** | Invalid **callbackURL** field (reserved for future use) |
| **66332** | Invalid **merchantData** field (reserved for future use) |
| **66333** | Invalid **origin** field (reserved for future use) |
| **66334** | Invalid **duplicateDelay** field. Refer to Section 14. |
| **66335** | Invalid **itemQuantity** field |
| **66336** | Invalid **itemDescription** field |
| **66337** | Invalid **itemGrossValue** field |
| **66338** | Invalid **taxValue** field |
| **66339** | Invalid **discountValue** field |
| **66340** | Invalid **taxDiscountDescription** field (reserved for future use) |
| **66341** | Invalid **xref** field |
| **66342** | Invalid **type** field |
| **66343** | Invalid **signature** field |
| **66344** | Invalid **authorisationCode** field |
| **66345** | Invalid **transactionID** field |
| **66356** | Invalid **threeDSRequired** field |
| **66347** | Invalid **threeDSMD** field |
| **66348** | Invalid **threeDSPaRes** field |
| **66349** | Invalid **threeDSECI** field |
| **66350** | Invalid **threeDSCAVV** field |
| **66351** | Invalid **threeDSXID** field |
| **66352** | Invalid **threeDSEnrolled** field |
| **66353** | Invalid **threeDSAuthenticated** field |
| **66354** | Invalid **threeDSCheckPref** field |
| **66355** | Invalid **cv2CheckPref** field |
| **66356** | Invalid **addressCheckPref** field |
| **66357** | Invalid **postcodeCheckPref** field |
| **66358** | Invalid **captureDelay** field. |
| **66359** | Invalid **orderDate** field |
| **66360** | Invalid **grossAmount** field |
| **66361** | Invalid **netAmount** field |
| **66362** | Invalid **taxRate** field |
| **66363** | Invalid **taxReason** field |
| **66416** | Invalid card expiry date. Must be a date sometime in the next 10 years |
| **66417** | Invalid card start date. Must be a date sometime in the last 10 years |

            1. **AVS / CV2 Check Response Codes**

The AVS/CV2 Check Response Message field **avscv2ResponseMessage** is sent back in the raw form that is received from the Acquiring bank and can contain the following values:

| **Response** | **Description** |
| --- | --- |
| **ALL MATCH** | AVS and CV2 match |
| **SECURITY CODE MATCH ONLY** | CV2 match only |
| **ADDRESS MATCH ONLY** | AVS match only |
| **NO DATA MATCHES** | No matches for AVS and CV2 |
| **DATA NOT CHECKED** | Supplied data not checked |
| **SECURITY CHECKS NOT SUPPORTED** | Card scheme does not support checks |

The AVS/CV2 Response Code **avscv2ResponseCode** is made up of six characters and is sent back in the raw form that is received from the Acquiring bank. The first 4 characters can be decoded as below, the remaining 2 characters are currently reserved for future use:

| **Position 1 Value** | **Description** |
| --- | --- |
| **0** | No Additional information available. |
| **1** | CV2 not checked |
| **2** | CV2 matched. |
| **4** | CV2 not matched |
| **8** | Reserved |

| **Position 2 Value** | **Description** |
| --- | --- |
| **0** | No Additional information available. |
| **1** | Postcode not checked |
| **2** | Postcode matched. |
| **4** | Postcode not matched |
| **8** | Postcode partially matched |

| **Position 3 Value** | **Description** |
| --- | --- |
| **0** | No Additional Information |
| **1** | Address numeric not checked |
| **2** | Address numeric matched |
| **4** | Address numeric not matched |
| **8** | Address numeric partially matched |

| **Position 4 Value** | **Description** |
| --- | --- |
| **0** | Authorising entity not known |
| **1** | Authorising entity – merchant host |
| **2** | Authorising entity – acquirer host |
| **4** | Authorising entity – card scheme |
| **8** | Authorising entity – issuer |

            1. **3-D Secure Enrolment/Authentication Codes**

The 3-D Secure enrolment check field **threeDSEnrolled** can return the following values:

**Y - Enrolled** : The card is enrolled in the 3-D Secure program and the payer is eligible for authentication processing.

**N - Not Enrolled** : The checked card is eligible for the 3-D Secure (it is within the card association&#39;s range of accepted cards) but the card issuing bank does not participate in the 3-D Secure program. If the Cardholder later disputes the purchase, the issuer may not submit a chargeback to you.

**U - Unable To Verify Enrolment** : The card associations were unable to verify whether the Cardholder is registered. As the card is ineligible for 3-D Secure, Merchants can choose to accept the card nonetheless and precede the purchase as non-authenticated and submits authorisation with ECI 7. The Acquirer/Merchant retains liability if the Cardholder later disputes making the purchase.

**E - Error Verify Enrolment** : The Gateway encountered an error. This card is flagged as 3-D Secure ineligible. The card can be accepted for payment, yet you may not claim a liability shift on this transaction in case of a dispute with the Cardholder.

The 3-D Secure authentication check field **threeDSAuthenticated** can return the following values:

**Y - Authentication Successful:** The Issuer has authenticated the Cardholder by verifying the identity information or password. A CAVV and an ECI of 5 is returned. The card is accepted for payment.

**N - Not Authenticated:** The Cardholder did not complete authentication and the card should not be accepted for payment.

**U - Unable To Authenticate:** The authentication was not completed due to technical or another problem. A transmission error prevented authentication from completing. The card should be accepted for payment, but no authentication data will be passed on to authorisation processing and no liability shift will occur.

**A - Attempted Authentication:** A proof of authentication attempt was generated. The Cardholder is not participating, but the attempt to authenticate was recorded. The card should be accepted for payment and authentication information passed to authorisation processing.

**E - Error Checking Authentication:** The Gateway encountered an error. The card should be accepted for payment, but no authentication information will be passed to authorisation processing and no liability shift will occur.

            1. **3-D Secure Enrolment/Authentication Only**

Usually, the Gateway will perform most of the 3-D Secure processing in the background leaving the only the actual contacting of the issuers Access Control Server (ACS) to the Merchant.

However, there may be times when you may wish to gain more control over the Enrolment and Authentication process. The following field allows the request processing to stop after the 3-D Secure enrolment check or authentication check and return:

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **threeDSOnly** | No
 | Complete the processing as far as the next 3-D Secure stage and then return with the appropriate response fields for that stage. |

As this stop is requested then a **responseCode** is returned as **0 (Success)** however it will be recorded in the Merchant Management System (MMS) as **65792 (3DS IN PROGRESS)** indicating that the transaction has been prematurely halted expecting it to be continued to the next 3-D Secure stage when required. In order to continue the process, the **threeDSRef** field is returned together with any relevant 3-D Secure response fields suitable for that stage in the processing.

If this flag is used when 3-D Secure is not enabled on the account or after the 3-D Secure process has been completed for the request (i.e. when the authentication step has completed), then passing the flag will cause the transaction to abort with a **responseCode** of **65795 (3DS PROCESSING NOT REQUIRED)**. This ensures that the transaction does not go on to completion by accident while trying do 3-D Secure enrolment or authentication only.

**3-D Secure Enrolment/Authentication Only is supported by the Direct Integration only.**

            1. **SCA Exemptions**

There are several exemptions to SCA that may be requested:

**Low Value Exemption**

Transactions below 30 EUR are considered low value and are generally exempt from authentication. However, the velocity limits below must be met:

- The cumulative limit of consecutive transactions without the application of SCA must not exceed 100 EUR: or
- The number of consecutive transactions since the last application of SCA must not exceed five.

The Merchant can request this exemption, or it may be automatically applied by the Issuer.

**Trusted Beneficiary Exemption**

The payer may add a trusted Merchant to a whitelist of trusted beneficiaries held by their Issuer, completing an SCA challenge in the process, to prevent further SCA application on subsequent transactions with the trusted Merchant.

The Merchant can request this exemption to allow this trust to be taken into consideration.

**Trusted Risk Analysis (TRA) Exemption**

SCA is not mandated where a PSP, having in place effective risk analysis tools, assesses that the fraud risk associated with a remote payment transaction is low. The ability for a payment to be considered low risk is based on the average fraud levels of the card issuer and acquirer processing the transaction.

The Merchant can request this exemption if agreed to by the PSP.

**Secured Corporate Payment Exemption**

Transactions initiated by a business rather than a Consumer and processed through a secured dedicated payment protocol can be exempt from SCA provided alternative controls are sufficiently secure.

The Merchant can request this transaction to indicate such a secure transaction.

**Delegated Authentication Exemption**

If the Merchant already requires the Consumer to perform sufficient authentication on their website, such as secure account logins etc., then they can use this exemption to request that further SCA is not required.

            1. **Secure Legacy API**

## A 3.1 Background

The 3-D Secure Legacy API was used for 3-D Secure integration prior to the introduction of 3-D Secure version 2. The API details are documented for backwards compatibility and should not be used for new integrations.

## A 3.2 Direct Implementation

If your Merchant account is setup for 3-D Secure the Gateway will require further authentication details provided by the 3-D Secure system.

To ensure the Gateway uses the legacy 3-D Secure API you must not pass any of the following fields used by the current API:

- **threeDSRef**
- **threeDSRedirectURL**
- **threeDSURL**
- **threeDSRequest**
- **threeDSResponse**

The API versions must not be mixed between the initial and continuation requests otherwise an error will occur.

### A-3.2.1 Initial Request (Direct Integration)

If no 3-D Secure authentication details are provided in the initial request the Gateway will determine whether the transaction is eligible for 3-D Secure by checking whether the card is enrolled in the 3-D Secure scheme.

If the Gateway determines that the transaction is not eligible for 3-D Secure, then it will continue and process it as normal transaction without 3-D Secure unless the **threeDSRequired** request field indicates that the transaction should be aborted instead.

If the Gateway determines that the transaction is eligible it will respond with a **responseCode** of **65802 (3DS AUTHENTICATION REQUIRED)** and included in the response will be a **threeDSACSURL** field containing the URL required to contact the ACS on and a **threeDSMD** and **threeDSPaReq** to send to the provided URL. The latter two values must be posted to the provided ACS URL as the fields **MD** and **PaReq** together with a **TermUrl** field provided by yourself which must contain the URL of a page on your server to return to when authentication has been completed.

### A-3.2.2 Continuation Request (Direct Integration)

On completion of the 3-D Secure authentication the ACS will post the original **MD** together with a **PaRes** value to the **TermUrl** provided. These values should then be sent to the Gateway in the **threeDSMD** and **threeDSPaRes** fields of a new request. This new request will check the 3-D Secure authentication and then either complete or abort the transaction depending on the authentication result and your preferences, either sent in the **threeDSPref** field or set in the Merchant Management System (MMS).

### A-3.2.3 Initial Request (Direct Integration)

These fields should be sent in addition to basic request fields in section [2.1](https://support.cardstream.com/hc/en-gb/articles/360012171277-Integration-Guide-PDF) of the main integration guide.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **merchantName** | No
# 53
 | Merchant name to use on 3DS form. |
| **merchantWebsite** | No1 | Merchant website to use on 3DS form. The website must be a fully qualified URL and include at least the scheme and host components. |
| **threeDSRequired** | No
# 54
 | Is 3DS required for this transaction?
Possible values are: **N** – 3DS is not required. **Y** – Abort if 3DS is not enabled. |
| **threeDSCheckPref** | No1 | List of **threeDSCheck** response values that are to be accepted, any other value will cause the transaction to be declined.
Value is a comma separated list containing one or more of the following values: **&#39;not known&#39;, &#39;not checked&#39;, &#39;**** not authenticated&#39;, &#39;attempted authentication&#39;, &#39;authenticated&#39;**. |

### A-3.2.4 Continuation Request (Direct Integration)

These fields may be sent alone
# 55
.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **threeDSMD** | Yes
 | The value of the **threeDSMD** field in the initial Gateway response. |
| **threeDSPaRes** | Yes | The value of the PaRes field POSTed back from the Access Control Sever (ACS). |

## A 3.2 Response Fields

### A-3.2.1 Initial Response (Direct Integration)

These fields should be sent in addition to the basic request fields in [2.2](https://support.cardstream.com/hc/en-gb/articles/360012171277-Integration-Guide-PDF) of the main integration guide.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **threeDSEnabled** | Always | Is 3DS enabled for this Merchant Account?
Possible values are: **N** – Merchant Account is not enabled. **Y** – Merchant Account is enabled. |
| --- | --- | --- |
| **threeDSXID** | If 3DS enabled | The unique identifier for the transaction in the 3DS system. |
| **threeDSVETimestamp** | If 3DS enabled | The time the card was checked for 3DS enrolment. |
| **threeDSEnrolled** | If 3DS enabled | The 3DS enrolment status for the credit card.Refer to appendix A-3 for details.
Possible values are: **Y** – Enrolled. **N** - Not Enrolled. **U** - Unable to Verify. **E** - Error Verifying Enrolment. |
| **threeDSMD** | If 3DSenabled | Value to return in the continuation request. Can be sent to the Access Control Server (ACS) in its MD field or stored locally by your server. |
| **threeDSACSURL** | If 3DS enrolled | The URL of the Access Control Server (ACS) to which the Payer Authentication Request (PaReq) should be sent. |
| **threeDSPaReq** | If 3DS enrolled | Payer Authentication Request (PaReq) that is sent to the Access Control Server (ACS) in order to verify the 3DS status of the credit card. |

### A-3.2.2 Continuation Response (Direct Integration)

These fields will be returned in addition to the request fields, the initial response fields and the basic response fields in section [2.2](https://support.cardstream.com/hc/en-gb/articles/360012171277-Integration-Guide-PDF)of this guide.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **threeDSPaRes** | If 3DS enrolled | Payer Authentication Response (PaRes) that is returned from the Access Control Server (ACS) determining the 3DS status of the credit card. |
| --- | --- | --- |
| **threeDSCATimestamp** | If 3DS enrolled | The time the card was checked for 3DS authentication. |
| **threeDSAuthenticated** | If 3DS enrolled | The 3DS authentication status for the credit card.Refer to appendix A-3 for details.
Possible values are: **Y** - Authentication Successful. **N** - Not Authenticated. **U** - Unable to Authenticate. **A** - Attempted Authentication. **E** - Error Checking Authentication. |
| **threeDSECI** | If 3DS authenticated | This contains a two-digit Electronic Commerce Indicator (ECI) value, which is to be submitted in a credit card authorisation message.
This value indicates to the processor that the Customer data in the authorisation message has been authenticated.
The data contained within this property is only valid if the **threeDSAuthenticated** value is **Y** or **A**. |
| **threeDSCAVV** | If 3DS authenticated | This contains a 28-byte Base-64 encoded Cardholder Authentication Verification Value (CAVV).
The data contained within this property is only valid if the **threeDSAuthenticated** value is **Y** or **A**. |
| **threeDSCAVVAlgorithm** | If 3DS authenticated | This contains the one digit value that indicates the algorithm used by the Access Control Server (ACS) to generate the CAVV.
The data contained within this property is only valid if the **threeDSAuthenticated** value is **Y** or **A**. |
| **threeDSErrorCode** | If 3DS error | Any error response code returned by the Access Control Server (ACS) if there is an error in determining the card&#39;s 3DS status. |
| **threeDSErrorDescription** | If 3DS error | Any error response description returned by the Access Control Server (ACS) if there is an error in determining the card&#39;s 3DS status. |

## A-3.3 3-D Secure Enrolment/Authentication Only (Direct Only)

3-D Secure Enrolment/Authentication checks can be performed using the legacy 3-D Secure API, except that the Gateway will return a **threeDSMD** field instead of a **threeDSRef** field. This field can be passed in the next request to continue the transaction.

            1. **Request Checking Only**

Sometimes, you may wish to submit a request to the Gateway in order for it to be &#39;validated only&#39; and not processed or sent to the Acquirer. In these cases, the following flag can be used that will stop the processing after the integrity verification has been performed:

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **checkOnly** | No
 | Check the request for syntax and field value errors only. Do not attempt to submit the transaction for honouring by the Merchant&#39;s financial institution. |

If the request is OK, then a **responseCode** is returned as **0 (Success)**; otherwise the code that would have prevented the request from completing is returned.

_ **Note:** _ _in these cases, the request is not stored by the Gateway and is not available within the Merchant Management System (MMS)._

            1. **Merchant Account Mapping**

Merchant Accounts can be grouped together so that if a transaction is sent to an account that doesn&#39;t support either the requested card type or currency, then it can be automatically routed to another account in the same group that does support them.

For example, you can group a Merchant Account that only supports American Express cards with a Merchant Account that only supports Visa cards. Then, if a request using an American Express card is sent to the Visa only Merchant Account, the Gateway will automatically route it to the American Express Merchant Account.

This prevents you from needing to know the card type in advance in order to send the request to the correct Merchant Account. This is important when using the Hosted integration, because you don&#39;t know the card type at the time you send the request.

It is usual for you to have one master account to which you direct all requests and then group all your accounts together.

Any Gateway routing of the transaction can be seen from the following additional response fields:

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **requestMerchantID** | Always | ID of Merchant Account request was sent to (usually same as **merchantID** ). |
| **processMerchantID** | Always | ID of Merchant Account request was processed by. |

            1. **Velocity Control System (VCS)**

The Gateway allows you to configure velocity controls using the Merchant Management System (MMS). These can be used to email you declined transactions automatically, where they exceed these controls.

For example, you can set up a control that stops a certain card number from being used more than twice in the space of a few minutes.

If one or more of these controls are broken by a transaction, then the following response fields will show the problem.

If a transaction is declined through breach of one or more of these rules, then a **responseCode** of **5 (VCS DECLINE)** will be returned.

| **Field Name** | **Returned?** | **Description** |
| --- | --- | --- |
| **vcsResponseCode** | Always | VCS error code. Normally **5**.Refer to appendix A-1 for details. |
| **vcsResponseMessage** | Always | Description of above response code or list of rules broken by this transaction. |

            1. **Capture Delay**

Capture Delay enables you to specify a delay between the authorisation of a payment and its capture. This allows you time to verify the order and choose whether to fulfil it or cancel it. This can be very helpful in preventing chargebacks due to fraud.

When NOT using capture delay, payments are authorised and captured immediately - funds are automatically debited from the Customer&#39;s credit or debit card at that time.

When using capture delay, the payment is authorised only at the time of payment - funds are reserved against the credit or debit card and will not be debited until the payment is captured; or not at all if you cancel.

The Customer experience with capture delay is exactly the same as when capture delay is not used. The Customer will not know whether you are using capture delay or not.

If you choose to use capture delay, you specify the number of days for which capture is delayed, within a range of 0 - 30 days. Payments will automatically be captured after that delay unless you manually cancel the transaction (either using the Hosted Integration or via the Merchant Management System (MMS)). (Note that some cards require capture within 4-5 days - if payment is not automatically captured within that 4-5 day period, the transaction will expire and the reserved funds will be released to the Customer.)

**Why Use Capture Delay?**

Capture delay allows you to accept online orders normally but allows you to cancel any transactions that you cannot or will not fulfil, thereby reducing the risks of chargeback. If you receive an order that appears to be fraudulent or that you cannot or do not wish to fulfil, you can simply cancel the transaction.

_Note: Cancelling a transaction will not reverse the authorisation and will not release the funds back to the Customer. The authorisation will be left to expire and release reserved funds. The time taken for this varies between cards._

_Some Acquirers do not support delayed capture, in which case the Hosted Integration will return a_ _ **responseCode** _ _of_ _**66358 (INVALID CAPTURE DELAY)**__._

            1. **Types of card**

The following is a list of primary card types supported by the Gateway.

| **Card Code** | **Card Type** |
| --- | --- |
| **MC** | Mastercard Credit |
| **MD** | Mastercard Debit |
| **MA** | Mastercard International Maestro |
| **MI** | Mastercard/Diners Club |
| **MP** | Mastercard Purchasing |
| **MU** | Mastercard Domestic Maestro (UK) |
| **VC** | Visa Credit |
| **VD** | Visa Debt |
| **EL** | Visa Electron |
| **VA** | Visa ATM |
| **VP** | Visa Purchasing |
| **AM** | American Express |
| **JC** | JCB |
| **CU** | China UnionPay (generic) |
| **CC** | China UnionPay Credit |
| **CD** | China UnionPay Debit |

The Gateway primarily supports Mastercard, Visa and American Express branded cards. Some Acquirers may support JCB cards. Not all Acquirers support all types.

Where cards are provided by a single card scheme, then the primary card code is also used as a code to identify the card scheme (referred to as the **cardSchemeCode** in the transaction response). For example, cards issued by VISA will use the code &#39; **VC**&#39;; cards issued by Mastercard will use the code &#39; **MC**&#39;; and so on. China UnionPay credit &#39; **CC**&#39; and debit &#39; **CD**&#39; will use the scheme code &#39; **CU**&#39;.

The following is a list of secondary card types recognised by the Gateway.

| **Card Code** | **Card Type** |
| --- | --- |
| **CF** | Clydesdale Financial Services |
| **BC** | BankCard |
| **DK** | Dankort |
| **DS** | Discover |
| **DI** | Diners Club |
| **DE** | Diners Club Enroute |
| **DC** | Diners Club Carte Blanche |
| **FC** | FlexCache |
| **LS** | Laser |
| **SO** | Solo |
| **ST** | Style |
| **SW** | Switch |
| **TP** | Tempo Payments |
| **IP** | InstaPayment |
| **XX** | Unknown/unrecognised card type |

These cards may be returned in response to a card lookup, but they are either deprecated or most likely not supported by any current Acquirer.

            1. **Integration Testing**

You can perform test transactions using one of the test Merchant IDs below and using test card details.

For non 3-D Secure testing use Merchant ID **100001**

For 3-D Secure Testing use Merchant ID **100856**

Test Merchant Accounts are not connected to an Acquirer and for that reason simulate their response, depending on the request **amount** , as follows:

| **Amount range from** | **Amount range to** | **Expected authorisation response** | **Expected settlement outcome** |
| --- | --- | --- | --- |
| **100 (£1.00)** | 2499 (£24.99) | AUTH CODE: XXXXXX | ACCEPTED |
| **2500 (£25.00)** | 4999 (£49.99) | AUTH CODE: XXXXXX | REJECTED |
| **5000 (£50.00)** | 9999 (£99.99) | CARD REFERRED | N/A |
| **10000 (£100.00)** | 14999 (£149.99) | CARD DECLINED | N/A |
| **15000+ (£150.00+)** |
 | CARD DECLINED – KEEP CARD | N/A |

              1.
### Test Card Details

DO NOT USE THESE TEST CARDS ON LIVE MERCHANT ACCOUNTS. THEY ARE FOR TEST PURPOSES ONLY.

The expiry date used for each test card should be December of the current year, in two-digit format – e.g. 12/15 for December 2015

                1.
### Visa Credit

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **4929421234600821** | 356 | Flat 6Primrose Rise347 Lavender RoadNorthamptonNN17 8YG |
| **4543059999999982** | 110 | 76 Roseby AvenueManchesterM63X 7TH |
| **4543059999999990** | 689 | 23 RogerhamMansions4578 Ermine StreetBorehamwoodWD54 8TH |

                1.
### Visa Debit

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **4539791001730106** | 289 | Unit 5Pickwick Walk120 Uxbridge RoadHatch EndMiddlesexHA6 7HJ |
| **4462000000000003** | 672 | Mews 57Ladybird DriveDenmark 65890 |

                1.
### Mastercard Credit

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **5301250070000191** | 419 | 25 The LarchesNarboroughLeicesterLE10 2RT |
| **5413339000001000** | 304 | Pear Tree CottageThe GreenMilton KeynesMK11 7UY |
| **5434849999999951** | 470 | 34a Rubbery CloseCloisters RunRugbyCV21 8JT |
| **5434849999999993** | 557 | 4-7 The Hay MarketGranthamNG32 4HG |

                1.
### Mastercard Debit

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **5573 4712 3456 7898** | 159 | Merevale Avenue Leicester LE10 2BU |

**UK Maestro**

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **6759 0150 5012 3445 002** | 309 | The Parkway 5258 Larches Approach Hull North Humberside HU10 5OP |
| **6759 0168 0000 0120 097** | 701 | The Manor Wolvey Road Middlesex TW7 9FF |

**JCB**

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **3540599999991047** | 209 | 2 Middle WallopMerideth-in-the-WoldsLincolnshireLN2 8HG |

**Electron**

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **4917480000000008** | 009 | 5-6 Ross AvenueBirminghamB67 8UJ |

**American Express**

| **Card Number** | **CVV** | **Address** |
| --- | --- | --- |
| **374245455400001** | 4887 | The Hunts WaySouthamptonSO18 1GW |

**Diners Club**

| **Card Number** | **CVV Number** |
| --- | --- |
| **36432685260294** | **111** |

Diners Club do not support AVS. For testing purposes use a separate MID with AVS turned off.

**Visa Test Cards**

| **Card Number** | **CVV** | **Address** | **Postcode** | **Amount** | **Test Scenario** |
| --- | --- | --- | --- | --- | --- |
| **4909630000000008** |
 |
 |
 | £12.01 | Card range not participating |
| **4012010000000000009** |
 |
 |
 | £12.02 | Card registered with VbV(automated ACS response –click on Submit button) |
| **4012001037141112** | 083 | 16 | 155 | £12.03 | Card registered with Visa(automated ACS response –click on Submit button) |
| **4012001037484447** | 450 | 200 | 19 | £12.04 | Failed authentication – issuerdatabase unavailable |
| **4015501150000216** |
 |
 |
 | £12.05 | Attempts processing(automated ACS response –click on Submit button) |

**Mastercard Test Cards**

Note: These test cards are controlled by Mastercard and won&#39;t always act as expected. The 3-D Secure passwords can be changed by anyone during the 3-D Secure testing, which means that the password won&#39;t then work for the next person. The standard fall-back password is dog33cat. Use Visa&#39;s 3-D Secure test cards if these below are not behaving as expected.

| **Card Number** | **CVV** | **Address** | **Postcode** | **Amount** | **Test Scenario** |
| --- | --- | --- | --- | --- | --- |
| **503396198900000818** | 332 | 31 | 18 | £11.01 | Enrolled International Maestroaccount number – validSecureCode (multiplecardholder).Select &#39;MEGAN SANDERS&#39;with SecureCode password:secmegan1 |
| **5453010000070789** | 508 | 20 | 52 | £11.02 | Enrolled account number -valid SecureCode (single)SecureCode password:sechal1 |
| **5453010000070151** | 972 | 22 | 08 | £11.03 | Enrolled account number –mixed SecureCode (multi)SecureCode password:Hannah – sechannah1 (bad)Haley – sechaley1 (good) |
| **5453010000070284** | 305 | 35 | 232 | £11.04 | Enrolled account number –invalid SecureCodeInvalid SecureCode password:invseccode |
| **5453010000084103** | 470 | 73 | 170 | £11.05 | Attempts processing |
| **5453010000070888** | 233 | 1 | 248 | £11.06 | Account number not enrolled |
| **5199992312641465** | 006 | 21 | 14 | £11.07 | Card range not participating |

              1.
### PayPal Sandbox Accounts

PayPal testing is available on the standard **100001** test Merchant account. However, you may wish to contact customer support to have your own PayPal test Merchant account created that connects to your own PayPal sandbox account, thus enabling you to view the transactions as they are sent to PayPal.

              1.
### Amazon Pay Sandbox Accounts

Amazon Pay testing is available on the standard **100001** test Merchant account. However, you may wish to contact customer support to have your own Amazon Pay test Merchant account created that connects to your own Amazon Pay sandbox account, thus enabling you to view the transactions as they are sent to Amazon Pay.

            1. **Sample Signature Calculation**

It is required that transactions are protected using message signing. The signing process offers a quick and simple way to ensure that the message came from an authorised source and has not been tampered with during transmission.

Signing, however, must be completed on your servers and never left for the Customer&#39;s browser to complete in JavaScript, as this would mean revealing your secret signature code to anyone who viewed the JavaScript code in the browser.

Signatures are especially important when a transaction is sent from a browser&#39;s payment form via the use of hidden form fields, because the Customer can easily use tools built into their browser to modify these hidden fields and change items such as the amount they should be charged.

The section below gives a step by step example of how to sign a transaction, complete with coding examples using the PHP language.

**Example Signature Key:**

$key = &#39;DontTellAnyone&#39;

**Example Transaction:**

$tran = **array** (

&#39;merchantID&#39; =\&gt; &#39;100001&#39;,

&#39;action&#39; =\&gt; &#39;SALE&#39;,

&#39;type&#39; =\&gt; &#39;1&#39;,

&#39;currencyCode&#39; =\&gt; &#39;826&#39;,

&#39;countryCode&#39; =\&gt; &#39;826&#39;,

&#39;amount&#39; =\&gt; &#39;2691&#39;,

&#39;transactionUnique&#39; =\&gt; &#39;55f025addd3c2&#39;,

&#39;orderRef&#39; =\&gt; &#39;Signature Test&#39;,

&#39;cardNumber&#39; =\&gt; &#39;4929 4212 3460 0821&#39;,

&#39;cardExpiryDate&#39; =\&gt; &#39;1213&#39;,

)

_ **The transaction used for signature calculation must not include any &#39;signature&#39; field as this will be added after signing when its value is known.** _

**Step 1 - Sort transaction values by their field name**

Transaction fields must be in ascending field name order according to their numeric ASCII value.

ksort($tran);

array ( &#39;action&#39; =\&gt; &#39;SALE&#39;, &#39;amount&#39; =\&gt; &#39;2691&#39;, &#39;cardExpiryDate&#39; =\&gt; &#39;1213&#39;, &#39;cardNumber&#39; =\&gt; &#39;4929 4212 3460 0821&#39;, &#39;countryCode&#39; =\&gt; &#39;826&#39;, &#39;currencyCode&#39; =\&gt; &#39;826&#39;, &#39;merchantID&#39; =\&gt; &#39;100001&#39;, &#39;orderRef&#39; =\&gt; &#39;Signature Test&#39;, &#39;transactionUnique&#39; =\&gt; &#39;55f025addd3c2&#39;, &#39;type&#39; =\&gt; &#39;1&#39; )

**Step 2 - Create url encoded string from sorted fields**

Use RFC 1738 and the application/x-www-form-urlencoded media type, which implies that spaces are encoded as plus (+) signs.

$str = http\_build\_query($tran, &#39;&#39;, &#39;&amp;&#39;);

action=SALE&amp;amount=2691&amp;cardExpiryDate=1213&amp;cardNumber=4929+4212+3460+0821&amp;countryCode=826&amp;currencyCode=826&amp;merchantID=100001&amp;orderRef=Signature+Test&amp;transactionUnique=55f025addd3c2&amp;type=1

**Step 3 - Normalise all line endings in the url encoded string**

Convert all CR NL, NL CR, CR character sequences to a single NL character.

$str = str\_replace( **array** (&#39;%0D%0A&#39;, &#39;%0A%0D&#39;, &#39;%0D&#39;), &#39;%0A&#39;, $str);

action=SALE&amp;amount=2691&amp;cardExpiryDate=1213&amp;cardNumber=4929+4212+3460+0821&amp;countryCode=826&amp;currencyCode=826&amp;merchantID=100001&amp;orderRef=Signature+Test&amp;transactionUnique=55f025addd3c2&amp;type=1

**Step 4 - Append your signature key to the normalised string**

The signature key is appended to the normalised string with no separator characters.

$str .= &#39;DontTellAnyone&#39;

action=SALE&amp;amount=2691&amp;cardExpiryDate=1213&amp;cardNumber=4929+4212+3460+0821&amp;countryCode=826&amp;currencyCode=826&amp;merchantID=100001&amp;orderRef=Signature+Test&amp;transactionUnique=55f025addd3c2&amp;type=1DontTellAnyone

**Step 5 - Hash the string using the SHA-512 algorithm**

The normalised string is hashed to a more compact value using the secure SHA-512 hashing algorithm1.

$signature = hash(&#39;SHA512&#39;, $str);

da0acd2c404945365d0e7ae74ad32d57c561e9b942f6bdb7e3dda49a08fcddf74fe6af6b23b8481b8dc8895c12fc21c72c69d60f137fdf574720363e33d94097

**Step 6 - Add the signature to the transaction form or post data**

The signature should be sent as part of the transaction in a field called &#39;signature&#39;.

\&lt; **input** type=&quot;hidden&quot;name=&quot;signature&quot;value=&quot;\&lt;?=$signature?\&gt;&quot;\&gt;

or

$tran[&#39;signature&#39;] = $signature;

            1. **Transaction Life cycle**

Each transaction received by the Gateway follows a pre-determined life cycle from receipt to completion. The stages in the life cycle are determined by the type of transaction and its success or failure at different stages in its life.

              1.
### Authorise, Capture and Settlement

The key stages in the transaction&#39;s life cycle can be grouped into the Authorisation, Capture and Settlement stages as follows:

                1.
### Authorisation

An authorisation places a hold on the transaction amount in the Cardholder&#39;s issuing bank. No money changes hands yet. For example, let&#39;s say that you are going to ship a physical product from your website. First, you authorise the amount of the transaction; then you ship the product. You only capture the transaction after the product is shipped.

                1.
### Capture

A capture essentially marks a transaction as ready for settlement. As soon as the product is shipped, you can capture an amount up to the amount of the authorisation. Usually, the full amount is captured. An example of a situation in which the whole amount is not captured is where the Customer ordered multiple items and one of them is unavailable.

The Gateway will normally automatically capture all authorisations as soon as they are approved, freeing up you from having to do this.

However, it is usually more desirable to delay the capture either for a period of time or indefinitely. The **captureDelay** field can be used for this purpose and will allow you to state the number of days to delay any automatic capture or never to automatically capture. For more details on delayed capture, refer to appendix A-10.

                1.
### Settlement

Within 24 hours, the Gateway will instruct your Acquirer to settle the captured transaction. The Acquirer then transfers the funds between the Cardholder&#39;s and your accounts.

              1.
### Transaction States

At any time during the transaction&#39;s life cycle, it is in one of a number of states as follows:

                1.
### Received

The transaction has been received by the Gateway and stored away. This is the first stage. The Gateway will examine the transaction and pass it on to the next stage, as appropriate.

                1.
### Approved

The transaction has been sent to the Acquirer for authorisation and the Acquirer has approved it and is holding the Cardholder&#39;s funds.

This is an intermediate state and follows the **received** state.

                1.
### Verified

The transaction has been sent to the Acquirer for verification and the Acquirer has confirmed that the account is valid.

This is a terminal state and follows the **received** state. The transaction will never be settled and no funds will ever be transferred

                1.
### Declined

The transaction has been sent to the Acquirer for authorisation and the Acquirer declined it.

The Acquirer will not usually give any reason for a decline and will not have held any funds.

The transaction has now completed its life cycle and no more processing will be done on it.

This is a terminal state and follows the **received** state. The transaction will never be settled and no funds will ever be transferred. The transaction **responseCode** will be **5 (Declined)**.

                1.
### Referred

The transaction has been sent to the Acquirer for authorisation and the Acquirer referred it for verbal approval.

You can choose not to seek verbal approval and treat these transactions the same as a normal &#39;declined&#39; authorisation.

To seek verbal approval, you must phone the Acquirer and ask for an authorisation code. They will probably ask for more information about the transaction and might require you to gather other forms of identification from the Cardholder. If an authorisation code is provided, then a new transaction can be sent to the Gateway specifying the **xref** of this transaction and the received **authorisactionCode**. This new request will not be sent for authorisation and will be in the &#39;approved&#39; state ready for capture and settlement.

This is a terminal state and follows the **received** state. The transaction will never be settled and no funds will ever be transferred. The transaction **responseCode** will be **2 (Referred)**.

                1.
### Reversed

The transaction was sent to the Acquirer for authorisation and the Acquirer approved it. However, the transaction has been voided and the approval reversed. The Acquirer will have been asked to reverse any approval previously received, effectively cancelling the authorisation and returning any held funds back to the Cardholder.

The gateway will reverse an authorisation if it declines the transaction post authorisation due to any AVS/CV checking. The PREAUTH action will also automatically reverse an authorisation before return.

This is a terminal state and follows the **approved** state. The transaction will never be settled and no funds will ever be transferred.

If the transaction was reversed due to AVS/CV2 checking, then the transaction **responseCode** will be **5 (AVS/CV2 Declined)**.

                1.
### Captured

The transaction has been captured and the Acquirer will be asked to capture the approved held funds when the settling process next runs. The settling process usually runs each evening but the Acquirer may take up to 3 days to transfer the funds.

The **capture** state can either be entered automatically if the transaction requested an immediate or delayed capture; or it can be manually requested by sending a CAPTURE request. You are free to change the amount to be captured to a value less than that initially approved by issuing one or more CAPTURE commands. When captured, there is no way to un-capture a transaction. If not explicitly cancelled, it will be sent for settlement at the next opportunity.

This is an intermediate state and follows the **approved** state.

                1.
### Tendered

The transaction has been sent to the Acquirer for settlement by the settling process and is awaiting confirmation that it has been accepted.

At this point, the transaction can no longer be cancelled or re-captured.

This is an intermediate state and follows the **captured** state.

                1.
### Deferred

The transaction could not be settled due to some temporary problem such as a communications loss. It will be attempted again the next time the settling process runs – usually first thing the next day.

This is an intermediate state and follows the **tendered** state. It will normally be accompanied by a transaction response that indicates why the settlement process could not settle the transaction.

                1.
### Accepted

The transaction has been accepted for settlement by the Acquirer. The held funds will be transferred between the Merchant and Cardholder in due course.

The transaction has now completed its life cycle and no more processing will be done on it, unless it is subject to a rejection while the Acquirer is settling it.

This is a terminal state and follows the **tendered** state.

                1.
### Rejected

The transaction has been rejected for settlement by the Acquirer. The held funds will not be transferred between the Merchant and Cardholder.

Only a few Acquirers inform the Gateway that they have rejected a transaction: they usually inform you directly. Therefore, a transaction may show as **accepted** even if was ultimately rejected or it may change from **accepted** to **rejected** if the Acquirer does inform the Gateway.

The transaction has now completed its life cycle and no more processing will be done on it.

This is a terminal state and follows the **tendered** or **accepted** states. The transaction response will normally indicate the reason the transaction was rejected.

                1.
### Canceled

The transaction has been cancelled by the Merchant by sending a cancellation request to the Gateway either using the CANCEL action or via the Merchant Management System (MMS).

You can cancel any transaction that is not in a terminal state or in the &#39;tendered&#39; state. When cancelled, any further processing that would have normally taken place will be halted. Cancelling a transaction may or may not release any funds held on the Cardholder&#39;s card, depending on support from the Acquirer and card scheme. Note: the state is spelt American style, with a single &#39;l&#39; as **canceled**.

This is a terminal state and follows any non-terminal state that occurs before the transaction reaches the **tendered** state.

                1.
### Finished

The transaction has finished and reached the end of its lifespan but did not reached one of the other terminal states. Usually this indicates that a problem has occurred with the transaction that prevents it continuing with its normal life cycle.

This is a terminal state and can follow any other state. The transaction response will normally indicate the reason that the transaction failed.

            1. **Transaction types**

The Gateway only supports card not present (CNP) types of transactions, made where the Cardholder does not or cannot physically present the card for a your visual examination at the time that an order is placed and payment effected.

The type of transaction required is specified using the type request field when performing a new payment transaction.

              1.
### E-commerce (ECOM)

E-commerce transactions are supported by the Gateway by using a transaction **type** of **1**. They are designed for you to accept payments via a website, such as a shopping cart payment. E-commerce transactions can use advance fraud detection, such as 3-D Secure.

In accordance with Mastercard stipulations, the Gateway will not allow Maestro cards to be used for new e-commerce transactions without the use of 3-D Secure.

              1.
### Mail Order/Telephone Order (MOTO)

Mail Order/Telephone Order transactions are supported by the Gateway by using a transaction **type** of **2**. They are designed for you to build your own virtual terminal system to enter remote order details. You will need to ensure when processing such transactions, that your Acquirer understands that the transaction is a MOTO transaction. This is because your Acquirer will have different requirements in order to classify a transaction as secure: e.g. 3-D Secure is often required for internet transactions, but impossible for MOTO transactions.

              1.
### Continuous Authority (CA)

Continuous Authority transactions are supported by the Gateway by using a transaction **type** of **9**. They are designed for you to make subscription transactions. For further details on how to use Continuous Authority transactions, please refer to appendix A-17.2.

The Gateway offers a means of automating the taking of regular CA transactions using Recurring Transaction Agreements (RTA) as detailed in section 13.

            1. **Payment Tokenisation**

All new transactions stored by the gateway are assigned a unique reference number that is referred to as the cross reference and returned in the **xref** response field. This cross reference is displayed on the Merchant Management System (MMS) and used whenever a reference to a previous transaction is required.

The cross reference can be sent as part of a transaction request, in the **xref** request field, to tell the Gateway to perform an action on an existing transaction. This is usually for management actions such as **CANCEL** or **CAPTURE**.

The cross reference can also be sent with new transactions such as **PREAUTH** , **SALE** , and **REFUND** actions, to request that the Gateway uses the values from the existing transaction if they have not been specified in the new request. For more information on how the existing values are used, please refer to appendix A-18. This allows an existing transaction to be effectively repeated without your needing to know the original card number. The only exception to this is the card&#39;s security code (CVV) which the Gateway cannot store, due to PCI DSS restrictions. Accordingly, it will have to be supplied in the new request (unless the new request is a Continuous Authority transaction, refer to appendix A-15.3).

The use of cross references to perform repeat transactions is referred to as Payment Tokenisation and should not be confused with Card Tokenisation which is a separate service offered by the Gateway.

Refer to section 13 for details on how to instruct the Gateway to repeat a payment automatically.

The way each action handles any supplied **xref** is as follows:

              1.
### PREAUTH, SALE, REFUND, VERIFY requests

These requests will always create a new transaction.

The **xref** field can be provided to reference an existing transaction, which will be used to complete any missing fields in the current transaction. The previous transaction will not be modified. For more information on how the existing values are used, please refer to appendix A-18. If the existing transaction cannot be found, then an error will be returned and recorded against the new transaction

The request is expected to contain any transaction information required.

The **xref** will only be used to complete any missing card and order details, relieving you from having to store card details and reducing your PCI requirements.

              1.
### REFUND\_SALE requests

These requests will always create a new transaction.

The **xref** field can be provided to reference an existing transaction that is going to be refunded. This existing transaction will be marked as have been fully or partially refunded and the amounts will be tallied to ensure that you cannot refund more than the original amount of this existing transaction. If the existing transaction cannot be found, then an error will be returned and recorded against the new transaction.

The request is expected to contain any transaction information required.

The **xref** will not only be used to find the transaction to be refunded: additionally, that transaction will be used to complete any missing card and order details, relieving you from having to store card details and reducing your PCI requirements.

              1.
### CANCEL or CAPTURE requests

These requests will always modify an existing transaction.

The **xref** field must be provided to reference an existing transaction, which will be modified to the desired state. If the existing transaction cannot be found, then an error is returned but no record of the error will be recorded against any transaction.

The request must not contain any new transaction information any attempt to send any new transaction information will result in an error. The exception is that a CAPTURE request can send in a new lesser **amount** field when a lesser amount, than originally authorised, must be settled.

              1.
### QUERY requests

These requests will not create or modify any transaction.

The **xref** field must be provided to reference an existing transaction, which will be returned as if it had just been performed. If the existing transaction cannot be found, then an error is returned but no record of the error will be recorded against any transaction.

The request must not contain any new transaction information and any attempt to send any new transaction information will result in an error.

              1.
### SALE or REFUND Referred Authorisation requests

These will always create a new transaction.

The **xref** field must be provided to reference an existing transaction, which must be of the same request type and be in the **referred** state. A new transaction will be created based upon this transaction. If the existing transaction cannot be found or is not in the **referred** state, then an error will be returned and recorded against the new transaction.

The new transaction will be put in the **approved** state and captured when specified by the existing or new transaction details. It will not be sent for authorisation again first.

The request may contain new transaction details, but any card details or order amount must be the same as the existing transaction. Any attempt to send different card details or order details will result in an error.

NB: This usage is very similar to a normal SALE or REFUND request sent with an **authorisationCode** included. The difference is that the **xref** must refer to an existing **referred** transaction whose full details are used if required and not simply an existing transaction whose card details are used if required.

This means it is not possible to create a pre-authorised SALE or REFUND request and use a **xref** (i.e. to use the card and order details from an existing transaction). As a soon as the **xref** field is seen, the Gateway identifies that it is a **referred** transaction that you wish to authorise.

            1. **Repeat Transactions**

The Gateway supports two main types of repeat transactions and the option for the Gateway to take the repeat transactions automatically on behalf of the Merchant.

Repeat transactions take advantage of the Payment Tokenisation feature of the Gateway as described in appendix A-16, where each transaction is assigned a unique cross reference and allows the details from a previous transaction to be used in a later transaction.

Refer to section 13 for information on how the Gateway can be instructed to take repeat payments automatically, according to a pre-determined schedule.

              1.
### MOTO Transactions

A Mail Order/Telephone Order (MOTO) repeat transaction, is where the Merchant makes a repeat transaction using card details that have been captured as part of a previous transaction without the Cardholder giving permission to continue to take money from their debit or credit card.

Merchants who use this system to implement billing or subscription type payments are encouraged to use the Continuous Payment Agreement method, as described in section A-17.2, to comply with Card Payment Scheme practices. _Your Acquirer may refuse to accept the repeat transactions if they are not subject to an agreement between yourself and your Customer._

.

                1.
### Initial Transaction

The initial transaction can be any transaction that has successfully stored valid credit card details and returned a **xref** response field. The transaction does not have to have resulted in a successful authorisation but would normally be a successful VERIFY, PREAUTH or SALE request.

                1.
### Repeat Transaction

The repeat transaction would send the **xref** returned by the initial transaction (or previous repeat transaction) as the **xref** request field. This transaction should use a **type** of **2** (MOTO) indicating that it is a Merchant initiated transaction.

The repeat transaction would be a clone of the cross referenced transaction, including any payment details with the exception of any new data provided in the repeat transaction. The **cloneFields** request field can also be used to control which fields in the cross referenced transaction are used in the repeat transaction (refer to appendix A-18).

Because the card CVV number is never stored, repeat transactions will either require the Cardholder to re-enter their CVV or the transaction must be performed with no CVV. In such cases, the Gateway will automatically suppress CVV checking. However, some Acquirers will not allow transactions to be performed with no CVV.

              1.
### Continuous Payment Agreements

A Continuous Payment Authority (CPA), which is sometimes referred to as a recurring payment or a &#39;continuous payment transaction&#39;, is where the Cardholder gives a Merchant permission to take money regularly from their debit or credit card, whenever they consider that they are owed money. Often, payday loan companies, online DVD rental subscriptions, magazine subscriptions and gym memberships use this method of payment.

                1.
### Initial Transaction

The initial transaction must be any successful VERIFY, PREAUTH or SALE request. If no payment is required at the same time, then a Merchant must use a VERIFY request.

The initial transaction must be subject to the highest level of authentication supported. This therefore means that eCommerce transactions must use 3-D Secure when available.

In order to indicate that the initial transaction is the first in a Continuous Payment Authority, then the type of agreement between the Merchant and the Cardholder must be specified, using the **rtAgreementType** field.

The **rtAgreementType** can be one of the following values:

- **recurring** – this is used when each recurring payment may be for a variable or fixed amount and the agreement shall not have a specified end date.
- **instalment** – this is used when each recurring payment may be for a variable or fixed amount but the total of all the recurring payments will be for a fixed amount that shall be specified in the agreement with the Cardholder. Therefore, the agreement has a specified end date and the total amount to be paid is known.

                1.
### Repeat Transaction

The repeat transaction would send the **xref** returned by the initial transaction (or previous repeat transaction) as the **xref** request field. This transaction must use a **type** of **9** (CA) indicating that it is a Continuous Authority transaction.

The repeat transaction would be a clone of the cross referenced transaction, including any payment details with the exception of any new data provided in the repeat transaction. The **cloneFields** request field can also be used to control which fields in the cross referenced transaction are used in the repeat transaction (refer to appendix A-18).

Because the card CVV number is never stored, repeat transactions will not require a card CVV to be supplied.

Acquirers may insist that a separate acquiring account must be used for any Continuous Authority payment, in which case this would be associated with a different Merchant Account. In such cases, the initial transaction would be performed against your normal Merchant Account and the repeat transactions would be performed against your Continuous Authority Merchant Account.

It is the responsibility of the Merchant to regulate the transaction values and frequencies. Please be aware that as a rule of thumb, the banks expect Continuous Authority payments to be a predictable transaction amount on a regular or predictable frequency. Any deviation from this can be viewed as an abuse of the Merchant&#39;s Continuous Authority acquiring account. You must also only ever process a Continuous Authority transaction on a card for which you have obtained full authorisation and authentication via your normal Merchant Account.

Mastercard stipulates that the Gateway will not allow Maestro cards to be used with Continuous Authority transactions.

            1. **Transaction Cloning**

If a new transaction request is received with the Cross Reference ( **xref** ) of an existing transaction, then the values of certain fields in the existing transaction will be used to initialise the new transaction where new values have not been provided in the new request. This copying of fields from a base transaction is termed &#39;transaction cloning&#39;, and the copied-over value is termed the &#39;cloned value&#39;.

Appendix A-18.1 shows all the fields whose values can be copied over from the existing transaction. To allow for easy addition of future fields, the fields are grouped into logical groupings and each group is given a name (as show in brackets after the group title).

Certain groups of fields, such as address fields, can only be copied as a whole entity and any new value provided in the new request will prevent the whole group from being copied from the existing transaction. Please note that line item data (items) cannot be merged.

By default, the values of all the fields listed in appendix A-18.1 are copied from the existing transaction where appropriate. However, you can control exactly which fields are copied using the **cloneFields** field in the new request. The value of **cloneFields** should be a comma separated list of field names or group names that should be copied over. Alternatively, if you wish to specify a list of fields not to copy, then prefix the list with a single exclamation mark (!).

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **cloneFields** | N | Comma separated list of field names or group names whose values should be cloned. |

**Examples**

To copy over only the value of **customerName** and any values for the fields in the _ **customerAddressFields** _ group:

cloneFields=&quot;customerName, customerAddressFields&quot;

To copy over the values of all supported fields apart from the value of **customerName** and **merchantName** :

cloneFields=&quot;!customerName,merchantName&quot;

              1.
### Cloned Fields

Transaction fields currently cloned are as follows:

- Order Details Fields ( **orderFields** )
  - **type**
  - **countryCode**
  - **currencyCode**
  - **amount**
  - **grossAmount**
  - **netAmount**
  - **taxRate**
  - **taxAmount**
  - **taxReason**
  - **discountAmount**
  - **discountReason**
  - **handlingAmount**
  - **insuranceAmount**

- Order Reference Fields ( **orderRefFields** )
  - **transactionUnique**
  - **orderRef**
  - **orderDate**

- Card Fields ( **cardFields** )
  - **paymentMethod**
  - **cardToken**
  - **cardNumber**
  - **cardExpiryDate**
  - **cardExpiryMonth**
  - **cardExpiryYear**
  - **cardStartDate**
  - **cardStartMonth**
  - **cardStartYear**
  - **cardIssueNumber**

- Cardholder Fields ( **cardholderFields** )
  - **customerName**
  - **customerAddress**
  - **customerPostcode**
  - **customerEmail**
  - **customerPhone**

- Purchase Fields ( **purchaseFields** )
  - **Items**

- Statement Narrative Fields ( **narrativeFields** )
  - **statementNarrative1**
  - **statementNarrative2**
- 3D Secure Fields ( **threedsFields** )
# 0

  - **threeDSRequired**
  - **threeDSCheckRef**

- AVS/CV2 Fields ( **avscv2Fields** )
  - **avscv2Required**
  - **cv2CheckPref**
  - **addressCheckPref**
  - **postcodeCheckPref**
  - **customerAddress**
  - **customerPostcode**

- Merchant Email Notification Fields ( **notifyFields** )
  - **notifyEmailRequired**
  - **notifyEmail**

- Customer Receipt Fields ( **cReceiptFields** )
  - **customerReceiptRequired**
  - **customerEmail**

- Merchant Information Fields ( **merchantFields** )
  - **merchantName**
  - **merchantCompany**
  - **merchantAddress** \*
  - **merchantTown** \*
  - **merchantCounty** \*
  - **merchantPostcode** \*
  - **merchantCountryCode** \*
  - **merchantPhone**
  - **merchantMobile**
  - **merchantFax**
  - **merchantEmail**
  - **merchantWebsite**
  - **merchantData**
  - **merchantOrderRef**
  - **merchantCustomerRef**
  - **merchantTaxRef**
  - **merchantOriginalOrderRef**
  - **merchantCategoryCode**
  - **merchantType**

Customer Information Fields ( **customerFields** )

  - **customerName**
  - **customerCompany**
  - **customerAddress** \*
  - **customerTown** \*
  - **customerCounty** \*
  - **customerPostcode** \*
  - **customerCountryCode** \*
  - **customerPhone**
  - **customerMobile**
  - **customerFax**
  - **customerEmail**
  - **customerOrderRef**
  - **customerMerchantRef**
  - **customerTaxRef**

Supplier Information Fields ( **supplierFields** )

  - **supplierName**
  - **supplierCompany**
  - **supplierAddress** \*
  - **supplierTown** \*
  - **supplierCounty** \*
  - **supplierPostcode** \*
  - **supplierCountryCode** \*
  - **supplierPhone**
  - **supplierMobile**
  - **supplierFax**
  - **supplierEmail**

- Receiver Information Fields ( **receiverFields** )
  - **receiverName**
  - **receiverCompany**
  - **receiverAddress** \*
  - **receiverTown** \*
  - **receiverCounty** \*
  - **receiverPostcode** \*
  - **receiverCountryCode** \*
  - **receiverPhone**
  - **receiverMobile**
  - **receiverFax**
  - **receiverEmail**
  - **receiverAccountNo**
  - **receiverDateOfBirth**

- Delivery Information Fields ( **deliveryFields** )
  - **deliveryName**
  - **deliveryCompany**
  - **deliveryAddress** \*
  - **deliveryTown** \*
  - **deliveryCounty** \*
  - **deliveryPostcode** \*
  - **deliveryCountryCode** \*
  - **deliveryPhone**
  - **deliveryMobile**
  - **deliveryFax**
  - **deliveryEmail**

- Shipping Information Fields ( **shippingFields** )
  - **shippingMethod**
  - **shippingTrackingRef**
  - **shippingAmount**
  - **shippingGrossAmount**
  - **shippingNetAmount**
  - **shippingTaxRate**
  - **shippingTaxAmount**
  - **shippingTaxReason**
  - **shippingDiscountAmount**
  - **shippingDiscountReason**

- MCC 6012 Additional Authorisation Data ( **mcc6012Fields** )
  - **receiverName**
  - **receiverPostcode**
  - **receiverAccountNo**
  - **receiverDateOfBirth**

- Payment Facilitator Data ( **facilitatorFields** )
# 0

  - **subMerchantID**
  - **facilitatorID**
  - **facilitatorName**

              1.
### Cloned Groups

To allow for easy future addition of new fields, the existing fields are grouped into logic groupings. Each group is given a name (as shown in brackets after the group title). It is recommended that this group name be used in any **cloneFields** value instead of listing all the fields separately.

                1.
### Compound Groups

To help maintain transaction integrity, certain groups of fields, such as address fields, can only be copied as a whole entity and any new value provided in the new request will prevent the whole group from being copied from the existing transaction.

These compound fields are marked with an asterisk in appendix A-18.1 and can be referred to in **cloneFields** as logical groups using the following group names; _ **merchantAddressFields** _, _ **customerAddressFields** _, _ **deliveryAddressFields** _, _ **supplierAddressFields** _ and _ **receiverAddressFields** __._

                1.
### Line Item Data

Any line item data ( **items** ) is copied over in its entirety and there is no way to merge the line item from an existing transaction with any sent in a new transaction.

                1.
### Amount Consistency

The Gateway does not validate that the various sub-amount fields, such as **netAmount** , **grossAmount,** all add up to the actual requested **amount**. Therefore, these fields are currently not treated as a compound group.

If a new **amount** value is passed that is different from the value in the existing transaction, then the following fields should also be passed so that they tally with the new amount.

- **grossAmount**
- **netAmount**
- **taxRate**
- **discountAmount**

            1. **Stored Credentials Framework**

To make sure merchants use their customers&#39; details responsibly, Visa and Mastercard have introduced a new framework for the storing of card details and new rules for any associated transactions. This framework identifies stored credentials as Credentials on File (COF) and classifies the transaction that use them as either Consumer Initiated Transactions (CIT) or Merchant Initiated Transactions (MIT).

If you process transactions using stored credentials, you may need to make changes to comply with these rules.

Currently the only credentials stored are card details and so the terms Consumer, Customer and Cardholder can be used interchangeably.

| **Field Name** | **Mandatory?** | **Description** |
| --- | --- | --- |
| **initiator** | N | Indicate who initiated the transaction.
Possible values are:consumer – consumer initiated (CIT)merchant – merchant initiated (MIT) |
| **rtAgreementType** | No | Consumer/Merchant agreement type.
Possible values are:cardonfile – credential storage agreed (CIT/MIT).recurring – recurring type CPA agreed (CIT/MIT).instalment – instalment type CPA agreed (CIT/MIT).unscheduled – adhoc COF payment (MIT)incremental
# 0
 – authorisation amount increment (MIT)resubmission – failed authorisation retry (MIT)reauthorisation – expired authorisation refresh (MIT).delayedcharges – post authorisation charges (MIT).noshow – missed reservation penalty (MIT) |

For backwards compatibility, the Gateway will try to automatically identify if a transaction is a Consumer Initiated Transaction or a Merchant Initiated Transaction from the value provided for the **action** , **type** and **rtAgreementType** fields.

You may also pass the **initiator** field in the request to force a classification. This can be used if the Gateway is unable to correctly determine classify the transaction. If, however, the requested classification is incompatible with the provided request fields then the transaction will fail with a **responseCode** of **66944** (INVALID INITIATOR).

The **initiator** field will be returned in the response with either the value passed in the request or the automatically identified value.

              1.
### Credentials on File (CoF)

Credentials on File (CoF) is the process when the Consumer authorises you to store their credentials (including, but not limited to, an account number or payment token) for future transactions. This includes for future Recurring or Instalment payments and Unscheduled ad-hoc payments, where the Consumer does not need to enter their payment credentials again.

These transactions must always be identified with the reason for storing or using the stored credentials and who initiated the transaction - Consumer (CIT) or Merchant (MIT).

You may store the credentials and send them with the future transaction, or you may store the details in the Gateway&#39;s Wallet as described in section 18 or by taking advantage of the Payment Tokenisation feature of the Gateway as described in appendix A-16. Either way you must tell the Gateway of your intentions, we will not assume that just because you have asked, for example, to store credentials in the Wallet that those are legitimate stored credentials and follow all the requirements laid out below.

If you store credentials on file, then you must:

- Disclose to consumers how those credentials will be used.
- Obtain consumers&#39; consent to store the credentials.
- Notify consumers when any changes are made to the terms of use.
- Inform the card issuer via a transaction that payment credentials are now stored on file.
- Identify transactions with appropriate **rtAgreementType** when using stored credentials.
- Perform a PREAUTH, SALE or VERIFY transaction during the initial credential setup.

Note: Credentials stored to complete a single transaction (or a single purchase) for a Consumer, including multiple authorisations related to that particular transaction or future refunds are not considered stored credentials and can be stored and used without the following the above rules.

              1.
### Consumer Initiated Transactions (CIT)

Consumer Initiated Transactions (CIT) are any transaction where the Consumer is actively participating in the transaction. This can be either through a checkout experience online, via a mail order or telephone order, with or without the use of an existing stored credential.

A Consumer Initiated Transaction is one whose **action** field is one of **PREAUTH** , **SALE** or **VERIFY** and whose **type** is one of **1** (ECOM) or **2** (MOTO).

To indicate that the card details are to be stored as, or were stored as, Credentials on File then send the **rtAgreementType** field as one of the following values:

- **cardonfile** – card details stored as Credential on File
- **recurring** – initial payment as the start of a recurring payment agreement.
- **instalment** – initial payment as the start of an instalment payment agreement.

If the card details are cloned from an existing transaction or loaded from a Gateway Wallet which also stored the Credentials on File then the transaction will be flagged as subsequent use of stored credentials rather than first use of them
# 0
.

Refer to section 13 for more information on **recurring** or **instalment** payment agreements.

              1.
### Merchant Initiated Transactions (MIT)

Merchant Initiated Transactions (MIT) are any transaction where you have performed the transaction without the active participation of the Consumer. This would always be as a follow-up to a previous Consumer Initiated Transaction (CIT).

Merchant Initiated Transactions are broken down in to two categories as follows.

                1.
### Standing Instruction MITs

Merchant Initiated Transactions defined under this category are performed to address pre-agreed standing instructions from the Consumer for the provision of goods or services.

The following transaction types are standing instructions transactions:

- Instalment Payments: A transaction in a series of transactions that use a stored credential and that represent Consumer agreement for the merchant to initiate one or more future transactions over a period for a single purchase of goods or services.

- Recurring Payments: A transaction in a series of transactions that use a stored credential and that are processed at fixed, regular intervals (not to exceed one year between transactions), representing Consumer agreement for the merchant to initiate future transactions for the purchase of goods or services provided at regular intervals.

- Unscheduled Credential on File (UCOF): A transaction using a stored credential for a fixed or variable amount that does not occur on a scheduled or regularly occurring transaction date, where the Consumer has provided consent for the merchant to initiate one or more future transactions. An example of such transaction is an account auto-top up transaction.

                1.
### Industry-Specific Business Practice MIT

Merchant Initiated Transactions defined under this category are performed to fulfil a business practice as a follow-up to an original Consumer-Merchant interaction that could not be completed with one single transaction. Not every industry practice Merchant Initiated Transaction requires a stored credential, for example, if you store card details for a single transaction or a single purchase, it is not considered as a stored credential transaction.

The following transaction types are industry specific transactions
# 0
:

- Incremental
# 0
: Incremental authorizations can be used to increase the total amount authorised if the authorised amount is insufficient. An incremental authorization request may also be based on a revised estimate of what the Consumer may spend.

- Resubmission: You can perform a resubmission in cases where it requested an authorization but received a decline due to insufficient funds; however, the goods or services were already delivered to the Consumer. In such scenarios, you can resubmit the request to recover outstanding debt from Consumers.

- Reauthorization: You can initiate a reauthorization when the completion or fulfilment of the original order or service extends beyond the authorization validity limit set by the card scheme.

- Delayed Charges: Delayed charges are performed to make a supplemental account charge after original services have been rendered and payment has been processed.

- No Show: Consumers can use their payment credentials to make a guaranteed reservation with certain merchant segments. A guaranteed reservation ensures that the reservation will be honoured and allows you to perform a No Show transaction to charge the Consumer a penalty according to your cancellation policy. If no payment is made to guarantee a reservation, then it is necessary to perform a VERIFY Consumer Initiated Transaction at the time of reservation to be able perform a No Show transaction later.

A Merchant Initiated Transaction is one whose **action** field is one of **PREAUTH** , **SALE** or **VERIFY** and whose **type** is one of **2** (MOTO) or **9** (CA) depending on the category.

To indicate the type of MIT, send the **rtAgreementType** field as one of the following values:

- **recurring** – subsequent payment as the start of a recurring payment agreement (CA).
- **instalment** – subsequent payment as the start of an instalment payment agreement (CA).
- **unscheduled** – subsequent payment not to a fixed schedule (MOTO)
- **incremental** – subsequent payment to increment initial amount authorised (MOTO)
- **resubmission** – subsequent payment due to failed initial payment (MOTO)
- **reauthorisation** – subsequent payment to refresh expired initial payment (MOTO)
- **delayedcharges** – subsequent payment for additional charges (MOTO)
- **noshow** – subsequent payment as penalty for missed reservation (MOTO)

The **xref** of the initial Consumer Initiated Transaction must be provided as follows:

- For standing order MITs the initial authorisation must have been a successful Consumer Initiated Transaction with Credentials on File. This MIT will be a subsequent use of those Credentials on File. For **recurring** and **instalment** MITs the initial authorisation must have used the same **rtAgreementType**. The xref can be to the previous MIT in which case the Gateway will follow the chain of transactions back to the initial CIT.

- For industry practice MITs the initial authorisation must be successful (apart from for a **resubmission** ) but need not have Credentials on File. For example, it may not be known at the time of the initial authorisation that the MIT would be required and so the initial authorisation would not necessarily have stored the Credentials on File. This is an example of when an industry practice Merchant Initiated Transaction does not require a stored credential

Note: For compatibility with existing practices, Instalment Payments and Recurring Payments MITs use Continuous Authority (CA) **type** transactions while other MITs Mail Order/Telephone Order (MOTO) **type** transactions. This use of MOTO is different to its use with a Consumer Initiated Transaction (CIT).

Refer to section 13 for more information on **recurring** or **instalment** Continuous Authority payment agreements.

            1. **Integration Libraries**

We can provide a range of libraries to help you to integrate with the Gateway.

These libraries include simple sever-side classes in many popular programming languages through to client-side scripts to help with the integration of the Hosted Payment Page or Hosted Payment Fields.

The server-side libraries can be obtained by contacting customer support.

The client-side libraries can be downloaded directly from the Gateway server.

              1.
### Gateway Integration Library

A simple server-side integration library is available to simplify the preparation and transmission of Hosted and Direct Integration requests.

The library is available in many popular programming languages and is based around a single class: the **Gateway** class.

**The Gateway integration library does not currently support the preparation and transmission of Batch Integration requests.**

                1.
### Library Namespace

To avoid polluting the global namespace, the library uses the &#39;P3/SDK&#39; namespace where supported by the language.

                1.
### Gateway Configuration

Before you can use the **Gateway** class, you will need to configure the following properties to match your integration parameters and authentication parameters documented in section 1.6.

| **Property Name** | **Type** | **Description** |
| --- | --- | --- |
| **hostedURL** | string | Absolute URL provided for the Hosted Integration.[Default: Gateway&#39;s Hosted Integration URL] |
| **directURL** | string | Absolute URL provided for the Direct Integration.[Default: Gateway&#39;s Direct Integration URL] |
| **merchantID** | string | Your unique Merchant ID to be passed in the **merchantID** integration field.[Default: 100001] |
| **merchantPwd** | string | Any password configured on your Merchant Account as per section 1.6.1.[Default: null] |
| **merchantSecret** | string | Any secret configured on your Merchant Account as per section 1.6.2.[Default: Circle4Take40Idea] |
| **proxyUrl** | string | Absolute URL to any proxy required for connections. (eg https://www.proxy.com:3128)[Default: null] |
| **debug** | boolean | True to enable debugging output.[Default: false] |

                1.
### Gateway Methods

The follow methods are made available by the **Gateway** class:

**string hostedRequest(mixed[] request, string[] options)**

Return an HTML fragment that can be included in your webpage to render a \&lt;form\&gt; which will send the provided request data to the Gateway&#39;s Hosted Integration when submitted.

The **request** parameter should be an associative array containing the request fields required to be sent. The request fields are not validated.

The following class properties are used unless alternative values are provided in the **request** array: **directUrl** , **merchantID** , **merchantPwd** , **merchantSecret**.

The **options** parameter is an optional associative array containing options that can be used to modify the returned HTML fragment as follows:

- **formAttrs** – string containing additional attributes to include in the form tag.
- **submitAttrs** – string containing additional attributes to include in the submit button tag.
- **submitImage** – string containing the URL to use as the submit button.
- **submitHtml** – string containing HTML to use as the label on the submit \&lt;button\&gt;.
- **submitText** – string containing text to use as the label on the submit \&lt;input\&gt;.

The **submitImage** , **submitHtml** and **submitText** options are mutually exclusive and will be checked for in that order. If none is provided, then a **submitText** value of &#39;Pay Now&#39; is assumed.

If a **merchantSecret** is provided, then the method will add the correct **signature** field to the request.

An exception is thrown if the HTML fragment cannot be composed.

The **verifyResponse()** method can be used to validate and decode any response POSTed back to your website.

Please refer to appendix A-23.1.1 for an example of how to use this method.

Returns a string containing the HTML fragment if successful; throws an exception otherwise.

**mixed[] directRequest(mixed[] request, string[] options)**

Return the response received when sending the provided request to the Gateway&#39;s Direct Integration.

The **request** parameter should be an associative array containing the request fields required to be sent. The request fields are not validated.

The following class properties are used unless alternative values are provided in the **request** array: **directUrl** , **merchantID** , **merchantPwd** , **merchantSecret**.

The **options** parameter is not used and reserved for future use.

If a **merchantSecret** is provided, then the method will add the correct **signature** field to the request and check the **signature** field on the response.

An exception is thrown if the request cannot be sent; or the response cannot be received; or if the response&#39;s **signature** is incorrect.

Please refer to appendix A-23.1.2 for an example of how to use this method.

Returns an associative array containing the received response fields; otherwise, throws an exception.

**void prepareRequest(mixed[] &amp;request, string[] &amp;options,**

**string &amp;secret, string &amp;direct\_url, string &amp;hosted\_url)**

Prepare a request for sending to the Gateway&#39;s Direct Integration.

The **request** parameter should be a reference to an associative array containing the request fields required to be sent. The request fields are not validated.

The **merchantSecret** , **directUrl**** and ****hostedUrl** configuration properties will be returned in the **secret** , **direct** \_ **url** and **hosted** \_ **url** method parameters. These properties can be overridden by providing them in the **request,** in which case they will be extracted and removed from the request.

The **merchantID** and **merchantPwd** configuration properties will be added to the **request**.

A few known Gateway response fields will be removed from the request, if present, to avoid confusion, notably the **responseCode** , **responseMessage** , **responseStatus** , **state** fields.

An exception will be thrown if the request does not contain an action element or a merchantID element (and none could be inserted).

**void verifyResponse(mixed[] &amp;response, string secret)**

Verify a response received from the Gateway&#39;s Hosted or Direct Integration.

The **response** parameter should be a reference to an associative array containing the response received from the Gateway, either from the Direct Integration or as POSTed from the Hosted Integration.

The **secret** parameter should be any Merchant secret to use when checking the response&#39;s **signature** element. If not provided, then the value of the **merchantSecret** property is used.

Any **signature** element is removed from the **response**.

An exception is thrown if the response is not valid, does not contain a **responseCode** element or its **signature** is incorrect.

Please refer to appendix A-23.1.1 for an example of how to use this method.

**string sign(mixed[] request, string secret, mixed partial = false)**

Return the signature for the provided request data.

The **request** parameter should be a reference to an associative array containing the request fields required to be sent. The request fields are not validated.

The **secret** parameter should be the Merchant secret to use when signing the request.

The **partial** parameter should be either the boolean **false** or comma separated string; or an array of strings containing the names of the request elements to sign.

Returns a string containing the correct signature for the request.

              1.
### Hosted Payment Page Library

A simple client-side script is available to simplify the displaying of the Hosted Payment Page in a lightbox overlaying your website.

The library is available as a JavaScript script and is based around a single class: the **Form** class. The script is compatible with most modern web browsers.

The script can be loaded directly from our Gateway server as follows
# 0
:

1. \&lt;script src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedforms.min.js&quot;\&gt;\&lt;/script\&gt;

If the script detects the presence of the jQuery API, then it will extend the jQuery object with its own plugin method. However, jQuery is not needed in order to use the script.

                1.
### Hosted Payment Pages

Hosted Payment Pages are a prebuilt webpage residing on our server that you can use to collect sensitive payment details without those details&#39; touching your server. The standard Hosted Payment Page is designed so that it can be displayed in a transparent overlay over your website, thus making the Customer feel as though they never left your shopping cart.

The standard Hosted Integration examples redirect the Customer&#39;s browser to the Hosted Payment Page, resulting it appearing on a new browser page and not overlaying your website. The Hosted Payment Page library provides the scripting necessary to result in the redirection, causing the Hosted Payment Page to appear in an overlay and not a new browser page, without your having to make any modifications to your website. The library can also simplify the creation of the Hosted Integration redirection FORM if required.

                1. **Library Namespace**

To avoid polluting the global namespace, the library extends the global window object with a **hostedForms** object containing the following properties:

- **forms** – array containing all the instantiated **Form** objects.
- **classes** – array containing all the instantiable classes.
  - **form** – **Form** class prototype.

                1.
### Form Construction

The construction method can be used to build and prepare a HTML FORM element for use with the modal Hosted Payment Page; or to prepare an existing element. The method signature is as follows:

**Form(element, data)**

The **element** parameter should be either the id or DOM node of an existing FORM or DIV DOM element.

If the **element** is a DIV node, then the data is used to create a new FORM node within the **element**.

If the **element** is a FORM node, then the data is used to modify the existing FORM **element**.

The **data** parameter should be an object containing construction details and can contain the following optional properties:

- **id** – string containing the value to use as the FORM tag&#39;s id attribute.
- **url** – string containing the URL to use as the FORM tag&#39;s src attribute.
- **attrs** – object whose properties are added as additional attributes on the FORM tag.
- **modal** – boolean indicating that the HPP should open in a modal overlay.
- **data** – object whose properties are added as hidden input elements in the FORM.
- **submit** – object containing details for a submit button that should be added to the FORM.
  - **type** – type of submit button, either &#39;auto&#39;, &#39;image&#39;, &#39;button&#39;, &#39;input&#39;
  - **id** – string containing the value to use as the submit button&#39;s id attribute.
  - **attrs** – object whose properties are added as additional attributes on the submit button.
  - **label** – string containing button label (or &#39;alt&#39; attribute for &#39;image&#39; buttons)
  - **src** – string containing image URL for &#39;image&#39; buttons.

The constructor will submit the FORM immediately after preparation if the **data.submit.type** property is &#39;auto&#39;; or if the existing FORM **element** has a data-hostedform-autosubmit attribute. Otherwise, an event handler will be attached to the submit button to disable it automatically when clicked, to help prevent your Customer from clicking it twice.

The constructor will prepare the FORM so that the Hosted Payment Page (HPP) will be opened in a modal overlay if the **data.modal** property is true; or if the existing FORM **element** has a data-hostedform-modal attribute; or has an action attribute containing the string &#39;modal/&#39; or ending in the string &#39;modal&#39;.

The modal overlay is automatically created as a semi-opaque IFRAME element that fills the browser display. The Hosted Payment Page is then loaded into this IFRAME and, being semi-opaque, your shopping cart will remain visible beneath, but greyed out and noninteractive. When the Customer closes the Hosted Payment Page, then their browser will be redirected to the URL you provided using the **redirectURL** parameter. This will cause the original page and IFRAME to be replaced by your new page.

                1. **Form Methods**

The follow methods are made available by the **Form** class:

**void destroy()**

Destroys the **Form,** reverting its **element** back to its original state.

                1. **jQuery Plugin**

If the jQuery API has been loaded into the browser before the script, then it will extend the jQuery object with its own plugin method.

Construction and destruction can then be done as follows:

**$(element).hostedForm(data);**

**$(element).hostedForm(&#39;destroy&#39;);**

              1.
### Hosted Payment Fields Library

A simple client-side script is available to support the displaying of Hosted Payment Fields in your payment form.

The library is available as a JavaScript script and is based around two classes: the **Form** and **Field** classes. The script is compatible with most modern web browsers.

The script can be loaded directly from our Gateway server as follows
# 0
:

1. \&lt;script src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedfields.min.js&quot;\&gt;\&lt;/script\&gt;

The script requires the jQuery API, which must be loaded prior to the script.

                1.
### Hosted Payment Fields

Hosted Payment Fields are a set of prebuilt JavaScript UI components that can be used by your website&#39;s HTML payment form to collect sensitive payment details without those details touching your server. They provide you with the PCI benefits of using a Hosted Payment Page, while allowing you the ability to design and implement your own payment forms.

There are 6 predefined Hosted Payment Fields available as follows:

- **cardNumber** – collects the card number.
- **cardCVV** – collects the card cvv.
- **cardExpiryDate** – collects the card expiry month and year.
- **cardStartDate** – collects the card start/issue month and year.
- **cardIssueNumber** – collects the card issue number.
- **cardDetails** – collects the card number, expiry date and cvv in a single field.

The **cardNumber** field is designed to collect a card number, including an icon used to display the card type. The field will only accept digits and spaces and validate that any entered value is a correctly formatted card number and insert spaces at the correct positions for the card type as the number is typed.

The **cardCVV** field is designed to collect a card CVV. The field will only accept digits and will validate that any entered value is a correctly formatted CVV, taking into account the card type as determined by an associated **cardNumber** field.

The **cardExpiryDate** and **cardStartDate** fields are designed to collect a card expiry date and card issue date respectively. The fields can render as a pair of select controls containing the months and a suitable range of years; or as an input control that will only allow digits to be entered and automatically formatted as a month / year entry. The field will validate that any entered value is a valid month and year combination.

The **cardIssueNumber** field is designed to collect a card issue number. The field will only accept digits and will validate that any entered value is a correctly formatted issue number.

The **cardDetails** field is designed to collect all of the essential card details. It combines the **cardNumber** , **cardExpiryDate** and **cardCVV** fields into a single line compound field design to allow easy entry of the card details and to complement the look of your checkout.

The field type is either: passed as the value of the **type** option the **Field** construction, provided by the HTML element&#39;s meta data; or provided via the HTML element&#39;s type attribute (prefixed with the &#39;hostedfield:&#39; name space).

The following example shows all three approaches to specifying the field type:

1. **\&lt;input**  type=&quot;hostedfield:cardNumber&quot; name=&quot;card-number&quot; **\&gt;**
2. **\&lt;div**  class=&quot;hostedfield&quot; data-hostedfield-type=&quot;cardExpiryDate&quot; **\&gt;\&lt;/div\&gt;**
3. **\&lt;input**  data-hostedfield=&#39;{&quot;type&quot;:&quot;cardCVV&quot;}&#39; **\&gt;**

It is highly recommended that you adopt a single approach as above and don&#39;t mix and match.

Each field type has its own additional configuration options, as detailed in section A-20.3.6.

                1. **Library Namespace**

To avoid polluting the global namespace, the library extends the global window object with a **hostedFields** object containing the following properties:

- **forms** – array containing all the instantiated **Form** objects.
- **classes** – array containing all the instantiable classes.
  - **form** – **Form** class prototype.

                1. **Form Construction**

The construction method can be used to prepare a HTML FORM for use with Hosted Payment Field components. The method signature is as follows:

**Form(element, options)**

The **element** parameter should be the DOM node of an existing FORM tag.

The **options** parameter should be object containing one of more of the following optional properties:

- **autoSetup** – boolean indicating whether setup should be handled automatically.
- **autoSubmit** – boolean indicating whether submission should be handled automatically.
- **merchantID** – string containing the **merchantID** the payment request is for.
- **stylesheet** – string containing DOM selector for any stylesheets to be used.
- **tokenise** – string/array/object specifying fields whose values should be tokenised.
- **fields** – object containing field configuration by field type.
- **locale** – string containing the desired locale.
- **classes** – object containing names of extra CSS classes to use.
- **submitOnEnter** – boolean indicating whether the enter key should cause the form to submit.
- **nativeEvents** – boolean indicating that native browser events should be fired.

Any **options** parameter will be merged with those provided via meta data supplied, using data-hostedfield and/or data-hostedfield-_\&lt;option\&gt;_ attributes; or via existing attributes or properties of the **element**.

The **autoSetup** option can be used to disable the automatic creation of **Field** objects for the FORM child controls by calling the **autoSetup()** method during the **Form** construction. If automatic setup is disabled, then you must manually instantiate **Field** objects and attach them to the **Form** as required, using the **addField()** method. This option or manually calling the **autoSetup()** method minimises the amount of JavaScript you have to write. Automatic operation is good if you don&#39;t need to customise the operation or can&#39;t customise it by reacting to the **Form** or **Field** events. The option defaults to true and cannot be changed once the **Form** has been created.

The **autoSubmit** option can be used to disable the automatic handling of the FORM submission via the **autoSubmit()** method. If automatic submission is disabled, then you must manually retrieve the sensitive payment details by calling **getPaymentDetails()** and include them in the form submission data. This option or manually calling the **autoSubmit()** method minimises the amount of JavaScript you have to write. Automatic operation is good if you don&#39;t need to customise the operation or can&#39;t customise it by reacting to the **Form** or **Field** events. The option defaults to true and cannot be changed once the **Form** has been created.

The **merchantID** option can be used to specify the **merchantID** with which the final **paymentToken** will be used. The option defaults to the value of any child INPUT node whose name is &#39;merchantID&#39; and can be changed at runtime by calling the **setMerchantID()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **stylesheet** option can be used to specify a DOM selector used to locate stylesheets that should be parsed for styles related to the Hosted Payment Fields. Refer to section A-20.3.10 for how to style the Hosted Payment Fields using CSS stylesheets. The option defaults to the DOM selector string &#39;link.hostedfield[rel=stylesheet], style.hostedfield&#39; and can be changed at runtime by calling the **setStylesheet()** method; or by altering the options using the jQuery **hostedForm()** plugin method.

The **tokenise** option can be used to specify addition FORM controls whose values, as returned by the jQuery.val() method, should be included in the final **paymentToken**.

The option&#39;s value must be either:

- A string containing a DOM selector used to select one or more controls.
- An array containing values used to jQuery.filter() down to one or more controls.
- An object whose properties are the name of fields to tokenise and whose values are objects containing a **selector** property used to select a control.

For the first two, the tokenised field&#39;s name be will be taken from the controls data-hostedfield-tokenise attribute or name attribute. For the third, the name is property name in the **tokenise** object. If the field&#39;s name is of the format &#39;paymentToken[\&lt;name\&gt;]&#39;, then only the &#39;\&lt;name\&gt;&#39; part is used. The option defaults to the DOM selector string &#39;INPUT.hostedfield-tokenise:not(:disabled), INPUT[data-hostedfield-tokenise]:not(:disabled), INPUT[name^=&quot;paymentToken[&quot;]:not(:disabled)&#39; and cannot be changed once the **Form** has been created.

The **fields** options can be used to specify default options for the different types of Hosted Payment Fields. The option&#39;s value should be an object whose properties are the fields type or the wildcard type &#39;any&#39; and whose values are objects whose properties are the default options for fields of that type. The values can also contain a **selector** property containing a DOM selector that is used during the automatic setup stage to select a FORM&#39;s child element to add as a **Field** of the specified type automatically. The option has no default value and cannot be changed once the **Form** has been created.

The **locale** option can be used to specify the language that should be used by the Hosted Payment Fields attached to this **Form**. The option defaults to the value provided by any lang attribute on the **element** or closest ancestor and cannot be changed once the **Form** has been created.

The **classes** options can be used to specify additional CSS class names to add in addition to the default classes documented in section A-20.3.9. The value is an object whose properties are the default class name and whose values are a string containing the additional class name(s) to use. The option has no default and cannot be changed once the **Form** has been created.

The **submitOnEnter** option can be used to specify if pressing the enter key when typing a **Field** value should cause the **Form** to submit. The option defaults to false and cannot be changed once the **Form** has been created.

The **nativeEvents** option can be used to specify that any associated native event should be fired when a &#39;hostedField:&#39; prefixed **Field** event is fired (as documented in section A-20.3.8). For example, when enabled if the &#39;hostedfield:mouseover&#39; event is fired, then the native &#39;mouseover&#39; event is also fired. The option defaults to false and cannot be changed once the **Form** has been created.

If not explicitly constructed, a **Form** object will be automatically instantiated and attached to the FORM DOM node as soon as any **Field** object is instantiated on a child DOM node.

Example **Form** construction is as follows:

1. **var**  form =  **new**  window.hostedFields.classes.Form(document.forms[0],{
2.     // Auto setup the form creating all hosted fields (default)
3.     autoSetup:  **true** ,
4.
5.     // Auto validate, tokenise and submit the form (default)
6.     autoSubmit:  **true** ,
7.
8.     // Additional fields to tokenise
9.     tokenise: &#39;.add-to-token&#39;,
10.
11.     // Stylesheet selection
12.     stylesheets: &#39;#hostedfield-stylesheet&#39;,
13.
14.     // Optional field configuration (by type)
15.     fields: {
16.         any: {
17.             nativeEvents:  **true**
18.         },
19.         cardNumber: {
20.             selector: $(&#39;#form2-card-number&#39;),
21.             stylesheet: $(&#39;style.hostedform, style.hostedform-card-number&#39;)
22.         }
23.     },
24.
25.     // Additional CSS classes
26.     classes: {
27.         invalid: &#39;error&#39;
28.     }
29. });

Or using meta data on the HTML FORM element:

1. **\&lt;form**  data-hostedfields=&#39;{&quot;autoSetup&quot;:true,&quot;autoSubmit&quot;:true,&quot;tokenise&quot;:&quot;.add-to-token&quot;,&quot;stylesheets&quot;:&quot;#hostedfield-stylesheet&quot;,&quot;fields&quot;:{&quot;any&quot;:{&quot;nativeEvents&quot;:true},&quot;cardNumber&quot;:{&quot;selector&quot;:&quot;#form2-card-number&quot;,&quot;stylesheet&quot;:&quot;style.hostedform, style.hostedform-card-number&quot;}},&quot;classes&quot;:{&quot;invalid&quot;:&quot;error&quot;}}&#39; method=&quot;post&quot; novalidate=&quot;novalidate&quot; lang=&quot;en&quot; **\&gt;**
2. **\&lt;script\&gt;**
3. var form = new window.hostedFields.classes.Form{document.forms[0]);
4. **\&lt;/script\&gt;**

                1. **Form Methods**

The follow methods are made available by the **Form** class:

**void autoSetup()**

Automatically setup the form by scanning the Form element for child nodes to control as Hosted Payment Fields. Child nodes are selected if they:

- have atype attribute with a hostedfield:_\&lt;type\&gt;_ value _(INPUT nodes only)_.
- have adata attribute with a hostedfield._\&lt;type\&gt;_ property.
- match a DOM selector provided by the fields_.\&lt;type\&gt;_.selector option.

If multiple selection criteria are present, then they must all specify the same **Field** type or an exception is thrown.

This method is called during the **Form** construction unless the **autoSetup** option is false.

**void autoSubmit()**

Automatically handles any attempted FORM submission by checking the FORM&#39;s controls are valid by calling the **validate()** method; and then requesting the **paymentToken** using the **getPaymentDetails()** method; and finally adding the token to the forms fields using the **addPaymentToken()** method. Failure to validate or request the payment token will cause the form submission to be stopped.

You can affect the automatic submission stages by listening for events and preventing their default actions. The full list of events is documented in section A-20.3.5.

This method is attached to the FORM submit event during the **Form** construction unless the **autoSubmit** option is false, or the **autoSubmit** option is null and the **autoSetup** option is false.

If automatic submission is disabled, then you must react to the FORM&#39;s submit event and then request the **paymentToken** using the **getPaymentDetails()** method and ensure that the token is sent as part of the form&#39;s data.

**boolean addField(Field f)**

Add a hosted **Field** to the Form.

Returns true if successful, false otherwise.

**boolean delField(Field f)**

Remove a hosted **Field** from the **Form**.

Returns true if successful, false otherwise.

**promise validate(boolean submitting)**

Validate all **Field** values on the **Form** , either during submission or not.

Returns a promise that will be resolved when the validation is complete.

**object[] getInvalidElements()**

Get details about all invalid FORM controls (not just invalid hosted **Field** elements).

Returns an array of objects containing the following properties:

- **element** – DOM element.
- **message** – DOM elements validationMessage property or &#39;Invalid value&#39;.
- **label** – associated LABEL text.
- **field** – **Field** instance (if DOM element is a hosted **Field** ).

**object getValidationErrors()**

Get the validation errors for all invalid FORM controls (not just invalid hosted **Field** elements).

Returns an object whose properties are the associated labels, names or id of the invalid FORM controls and whose values are the error message for that control.

**promise getPaymentDetails(object tokenData, boolean validate)**

Gets the payment details, generating a **paymentToken** containing the hosted Field values; any values specified by the **tokenise** option; and any passed **tokenData**. The Form will be validated first if required.

Returns a promise that will be resolved when the payment details have been obtained, passing the details as an object containing the following properties:

- **success** – boolean true if successful, false otherwise.
- **message** – string containing message to display if not successful.
- **errors** – object containing details about invalid payment data.
- **invalid** – object as returned by **getValidationErrors()** method.
- **paymentToken** – string containing generated **paymentToken**.

**void addPaymentToken(string token)**

Add the payment token as the value of a Form child INPUT whose name is &#39;paymentToken&#39;, creating the control if needed. Any created control will be given a type of &#39;hidden&#39;.

**void setMerchantID(string merchantID)**

Set the **merchantID** used by the payment form.

**void setStylesheet(string selector)**

Set the DOM selector used to select the stylesheet(s) used by the **Form**.

**object defaultFieldOptions(string type)**

Get any default field options specified via the **fields** option, resulting from the merger of its optional **any** and _ **\&lt;type\&gt;** _ properties.

Returns an object whose properties are the default options.

**void forceSubmit()**

Forcefully submit the FORM **element** as if a child submit button had been clicked.

**void reset()**

Reset all the **Form** , setting all **Field** values back to their initial values.

**void destroy()**

Destroys the **Form,** reverting its **element** back to its original state.

                1. **Form Events**

The following events may be fired by the **Form** object and you can use these to hook into and modify the object&#39;s behaviour:

| **Event Name**
 **# 56** | **Description** |
| --- | --- |
| **create** | Fired when a **Form** has been created. |
| **destroy** | Fired when a **Form** has been destroyed. |
| **presubmit** | Fired by the **autoSubmit()** method prior to handling the submission. You can prevent the handling of the submission and handle it yourself by calling the Events preventDefault() method. |
| **valid** | Fired by the **autoSubmit()** method if the FORM contains valid data prior to requesting the payment details. You can prevent the continued handling of the submission and handle it yourself by calling the Events preventDefault() method or by invalidating the FORM. |
| **submit-invalid** | Fired by the **autoSubmit()** method if the FORM contains invalid data prior to displaying the validity using the DOM reportValidity() method. You can prevent the reportValidity() call and display the validity yourself by calling the Events preventDefault() method. |
| **submit** | Fired by the **autoSubmit()** method prior to submitting the FORM. You can prevent the FORM from submitting by calling the Events preventDefault() method. |
| **error** | Fired by the **autoSubmit()** method if an exception is caught prior to displaying the error, using the JavaScript alert() function. You can prevent the alert() call and display the error yourself by calling the Events preventDefault() method. |

The **presubmit** , **valid** , **submit-invalid** , **submit** and **error** events fired by the **autoSubmit()** method the payload is an object with the following properties:

- **success** – boolean false.
- **message** – error message if **error** otherwise null.
- **invalid** – result of **getValidationErrors()** method if **Form** invalid.
- **submitting** – boolean true.

.

                1. **Field Construction**

The construction method can be used to prepare a HTML INPUT control as a Hosted Payment Field or to create a new field in HTML DIV container. The method signature is as follows:

**Field(element, options)**

The **element** parameter should be the DOM node of an existing INPUT or DIV tag.

The **options** parameter should be object containing one of more of the following optional properties:

- **type** – string containing the desired field type.
- **value** – string containing the initial value.
- **placeholder** – string containing any placeholder text.
- **style** – string containing any inline CSS styles.
- **stylesheet** – string containing DOM selector for any stylesheets to be used.
- **disabled** – boolean indicating if initially disabled.
- **required** – boolean indicating if the value is required.
- **readOnly** – boolean indicating if initially read only.
- **validity** – boolean or string indicating the initial validity.
- **locale** – string containing the desired locale.
- **classes** – object containing names of extra CSS classes to use.
- **submitOnEnter** – boolean indicating if the enter key should cause the form to submit.
- **nativeEvents** – boolean indicating that native browser events should be fired.
- **validationMessages** – object containing alternative validation messages.
  - **required** – string containing validation message to use when a value is required.
  - **invalid** – string containing validation message to use when a value is invalid.
- **format** – string containing select option format for date fields.
- **minYear** – integer containing minimum year (relative to current year) for date fields.
- **maxYear** – integer containing maximum year (relative to current year) for date fields.

Any **options** parameter will be merged with those provided via meta data supplied using data-hostedfield and/or data-hostedfield-_\&lt;option\&gt;_ attributes, or via existing attributes or properties of the **element** or provided via the **getDefaultOptions()** method of the parent **Form**.

The **type** option can be used to specify the type of Hosted Payment Field required. It defaults to the value provided by any type attribute on the **element** (prefixed with the &#39;hostedfield:&#39; namespace). The option cannot be changed once the **Field** has been created. Valid types are **cardDetails** , **cardNumber** , **cardCVV** , **cardExpiryDate** , **cardStartDate** , **cardIssueNumber**.

The **value** option can be used to specify any initial value that should be used by the **Field**. It defaults to the value provided by any value attribute or property on the **element**. Obviously, due to the purpose of the Hosted Payment Fields, any initial value is not wise for card number and CVV fields. The option can be changed at runtime by calling the **setValue()** method.

The **placeholder** option can be used to specify any initial text that should be used as a placeholder by the **Field**. It defaults to the value provided by any placeholder attribute or property on the **element**. When used with the **CardDetails** type **Field** the placeholder contains three parts separated by a pipe character, the first part contains the **cardNumber** placeholder, the second part contains the **cardExpiry** placeholder, and the third part contains the **cardCVV** placeholder. The option can be changed at runtime by calling the **setPlaceholder()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **style** option can be used to specify any initial inline CSS style that should be used by the **Field**. It defaults to the value provided by any style attribute or property on the **element**.The option can be changed at runtime by calling the **setStyle()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **stylesheet** option can be used to specify a DOM selector used to locate stylesheets that should be parsed for styles related to this **Field**. Refer to section on styling fields. The option can be changed at runtime by calling the **setStylesheet()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **disabled** option can be used to specify if the **Field** should be initially disabled. It defaults to the value provided by any disabled attribute or property on the **element**. The option can be changed at runtime by calling the **setDisabled()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **required** option can be used to specify if the **Field** value is required. It defaults to the value provided by any required attribute or property on the **element**. The option can be changed at runtime by calling the **setRequired()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **readOnly** option can be used to specify if the **Field** should be initially read-only. It defaults to the value provided by any readOnly attribute or property on the **element**. The option can be changed at runtime by calling the **setReadOnly()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **validity** option can be used to specify if the **Field** should be initially marked as invalid. It defaults to the value provided by any validity property on the **element**. The option can be changed at runtime by calling the **setValidity()** method or by altering the options using the jQuery **hostedForm()** plugin method.

The **locale** option can be used to specify the language that should be used by the **Field**. It defaults to the value provided by any lang attribute or property on the **element** or closest ancestor. The option cannot be changed once the **Field** has been created.

The **classes** options can be used to specify additional CSS class names to add in addition to the default classes documented in section A-20.3.9. The value is an object whose properties are the default class name and whose values are a string containing the additional class name(s) to use. This option will be merged with any classes option provided to the **Form** constructor. The option cannot be changed once the **Form** has been created.

The **submitOnEnter** option can be used to specify if pressing the enter key when typing the **Field** value should cause the **Form** to submit. The option defaults to false and cannot be changed once the **Field** has been created.

The **nativeEvents** option can be used to specify that any associated native event should be fired when a &#39;hostedfield:&#39; prefixed event is fired. Events are documented in section A-20.3.8. For example, when enabled if the &#39;hostedfield:mouseover&#39; event is fired then the native &#39;mouseover&#39; event is also fired. The option defaults to false and cannot be changed once the **Field** has been created.

The **validationMessages** option can be used to specify alternative validation messages that should be displayed when a value is required or invalid. The option defaults to suitable messages depending on the locale and cannot be changed once the **Field** has been created.

The **dropdown** option can be used to specify that a **cardStartDate** or **cardExpiryDate**** Field **should be displayed as a pair of select controls to select the month and year, otherwise the month and year are entered via a formatted input box instead. The option defaults to false and cannot be changed once the** Field** has been created.

The **format** option can be used in conjunction with the **dropdown** option to specify the format used to display the month and year in the dropdowns. The month and year parts of the format are separated by a pipe character. The option defaults to &#39;N – M | Y&#39; (e.g. &#39;01 – January | 2020&#39;) and cannot be changed once the **Field** has been created.

The following formatting characters are understood:

- **n** – month number (no zero prefixing).
- **N** – month number (zero prefixed to two digits when required).
- **m** – short month name (e.g. Jan, Feb, Mar)
- **M** – long month name (e.g. January, February, March)
- **y** – two digit year number.
- **Y** – four digit year number.

The **minYear** and **maxYear** options can be used in conjunction with the **dropdown** option to specify the minimum and maximum years that are included in the year dropdown. The option defaults to minus 20 to zero for a **cardStartDate**** Field **or zero to plus 20 for a** cardExpiryDate ****Field** and cannot be changed once the **Field** has been created.

Example **Field** construction is as follows:

1. var field =  **new**  window.hostedFields.classes.Field(document.forms[0].elements[0], {
2.     // Field type
3.     type: &#39;cardNumber&#39;,
4.
5.     // Stylesheet selection
6.     stylesheets: &#39;#hostedfield-stylesheet&#39;,
7.
8.     // Additional CSS classes
9.     classes: {
10.         invalid: &#39;error&#39;
11.     }
12. });

Or using meta data on the HTML INPUT element:

1. **\&lt;input**  type=&quot;hostedfield:cardNumber&quot; data-hostedfields=&#39;{&quot;stylesheet&quot;:&quot;style.hostedform, style.hostedform-card-number&quot;}},&quot;classes&quot;:{&quot;invalid&quot;:&quot;error&quot;}}&#39; **\&gt;**
2. **\&lt;script\&gt;**
3. var field = new window.hostedFields.classes.Field{document.forms[0].elements[0]);
4. **\&lt;/script\&gt;**

                1. **Field Methods**

The follow methods are made available by the **Field** class:

**promise validate()**

Validate the **Field** value. This will normally be called automatically when the **Field** loses focus or the form is submitted, or when an invalid value is modified.

Returns a promise that will be resolved when the validation is complete.

**boolean isEmpty()**

Check if the **Field** has a value.

Returns true if the field has a value, false otherwise.

**boolean isComplete()**

Check if the **Field** has a complete, but not necessarily valid, value. This is mainly used by compound fields such as **cardDetails** , **cardExpiryDate** , **cardStartDate** , which contain multiple input controls and are deemed complete when all their required input controls have values.

Returns true if the value is complete, false otherwise.

**void setStyle()** / **string getStyle()**

Set or gets the field&#39;s inline CSS style data.

Returns void when setting, or a CSS style string when getting.

**void setStylesheet(string selector)** / **string getStylesheet()**

Sets or gets the DOM selector used to select the stylesheet(s) used by the **Field**. When setting, the stylesheets are parsed and applied to the **Field**.

Returns void when setting, or a DOM selector string when getting.

**void setPlaceholder(string text)** / **string getPlaceholder()**

Sets or gets the placeholder text to be shown when the **Field** has no value.

When used with the **CardDetails** type **Field** the placeholder contains three parts separated by a pipe character, the first part contains the **cardNumber** placeholder, the second part contains the **cardExpiry** placeholder, and the third part contains the **cardCVV** placeholder.

Returns void when setting, or a text string when getting.

**void setDisabled(boolean disabled)** / **string getDisabled()**

Sets or gets the disabled state of the **Field**. When disabled, the field will be greyed out and not be focusable and thus will not react to any input events.

A disabled **Field** will have the &#39;hf-disabled&#39; class added otherwise the &#39;hf-enabled&#39; class is added.

Returns void when setting, or a boolean representing the state when getting.

**void setRequired(boolean required)** / **string getRequired()**

Sets or gets the required state of the **Field**. When required, the field will be invalid if it contains no value or a blank value.

A required **Field** will have the &#39;hf-required&#39; class added otherwise the &#39;hf-optional&#39; class is added.

Returns void when setting, or a boolean representing the state when getting.

**void setReadOnly(boolean read\_only)** / **string getRequired()**

Sets or gets the read-only state of the **Field**. When read-only, the field will be not be focusable and thus will not react to any input events.

A read-only **Field** will have the &#39;hf-readonly&#39; class added otherwise the &#39;hf-readwrite&#39; class is added.

Returns void when setting, or a boolean representing the state when getting.

**void setFocused(boolean focused)**

Moves the browser&#39;s focus to the **Field**. When focused, the field will react input events.

A focused **Field** will have the &#39;hf-focus&#39; class added otherwise the &#39;hf-blur&#39; class is added.

Returns void when setting, or a boolean representing the state when getting.

**void setValidity(string validity)** / **string getValidity()**

Sets or gets the validity of the **Field**. When valid, the validity will be true or a blank string. When invalid, the validity will be an error message explaining the reason the value is invalid.

When used with the **CardDetails** type **Field** the error message contains three parts separated by a pipe character, the first part contains the **cardNumber** value, the second part contains the **cardExpiry** value, and the third part contains the **cardCVV** value.

A valid **Field** will have the &#39;hf-valid&#39; and &#39;hf-user-valid&#39; classes added otherwise the &#39;hf-invalid&#39; and &#39;hf-user-invalid&#39; classes are added.

Returns void when setting, or an error message string when getting.

**void setValue()** / **string getValue()**

Set or gets the **Field** value. Because Hosted Payment Fields are designed for the entry of sensitive payment details, then these methods are not normally used. There is no means to retrieve the actual sensitive data and so any returned value will be an empty string if the field has no value or a single asterisk if the field has a value.

When used with the **CardDetails** type **Field** the value contains three parts separated by a pipe character, the first part contains the **cardNumber** value, the second part contains the **cardExpiry** value, and the third part contains the **cardCVV** value.

Returns void when setting, or a mask string when getting.

**void getState()**

Get the current state of the **Field** as an object with the following boolean properties:

- **isReady** – the **Field** has been created, initialised and is ready for use.
- **isValid** – the value is valid (refer to the **setValidity()** method).
- **isEmpty** – the value is empty (refer to the **isEmpty()** method).
- **isComplete** – the value is complete (refer to the **isComplete()** method).
- **isDisabled** – the value is complete (refer to the **setDisabled()** method).
- **isRequired** – the value is complete (refer to the **setRequired()** method).
- **isReadOnly** – the value is complete (refer to the **setReadOnly()** method).

Returns an object containing the states.

**void reset()**

Reset **Field** value back to the initial value.

**void destroy()**

Destroys the **Form,** reverting its **element** back to its original state.

_Note: A field&#39;s options or properties cannot be changed while a field is initialising: that is between construction and firing of the &#39;ready&#39; event. Attempts to change field options or properties before this will be ignored._

                1.
### Field Events

The following events may be fired by the **Field** object and you can use these to hook into and modify the object&#39;s behaviour:

| **Event Name**
 **# 57** | **Description** |
| --- | --- |
| **create** | Fired when a **Field** has been created. |
| **destroy** | Fired when a **Field** has been destroyed. |
| **ready** | Fired when a **Field** style is has finished initialising and is ready. |
| **style** | Fired when a **Field** style is changed. |
| **autofill** | Fired when a **Field** has a value auto filled by the browser. |
| **autofillcancel** | Fired when a **Field** has an auto filled value removed. |
| **valid** | Fired when a **Field** is checked for validity and passes the check. |
| **invalid** | Fired when a **Field** is checked for validity and fails the check. |
| **uservalid** | Fired when the valid event is fired but only after user interaction has occurred, such as focusing a **Field** , leaving a **Field** or attempting to submit a **Form**. |
| **userinvalid** | Fired when the invalid event is fired but only after user interaction has occurred, such as focusing a **Field** , leaving a **Field** or attempting to submit a **Form**. |
| **disabled** | Fired when a **Field** changes to disabled. |
| **enabled** | Fired when a **Field** changes from disabled. |
| **required** | Fired when a **Field** changes to required. |
| **optional** | Fired when a **Field** changes from required. |
| **readonly** | Fired when a **Field** changes to read-only. |
| **readwrite** | Fired when a **Field** changed from read-only. |
| **focus** | Fired when a **Field** receives focus. |
| **blur** | Fired when a **Field** loses focus. |
| **mouseenter** | Fired when a pointing device is moved into the **Field**. |
| **mouseleave** | Fired when a pointing device is moved out of the **Field**. |
| **mouseover** | Fired when a pointing device is moved into the **Field**. |
| **mouseout** | Fired when a pointing device is moved out of the **Field**. |
| **mousemove** | Fired when a pointing device is moved over the **Field**. |
| **keydown** | Fired when a key is pressed in the **Field**. |
| **keyup** | Fired when a key is released in a **Field**. |
| **keypress** | Fired when a key except Shift, Fn, CapsLock is in a pressed position in a **Field**. |
| **change** | Fired when an alteration to the value of a **Field** is committed by the user. |
| **input** | Fired when the value of a **Field** is changed. |

                1.
### Field CSS Classes

The following CSS class names will be added to a **Field** object depending on its state and you can use these to style the object as required:

| **Event Name** | **Description** |
| --- | --- |
| **hostedfield** | Present on all **Field**** elements**. |
| **hf-autofill** | Present when the value was auto filled by the browser. |
| **hf-invalid** | Present when in the invalid state. |
| **hf-valid** | Present when in the valid state. |
| **hf-user-invalid** | Present when in the invalid state and user interaction has occurred, such as focusing a **Field** , leaving a **Field** or attempting to submit a **Form**. |
| **hf-user-valid** | Present when in the valid state and user interaction has occurred, such as focusing a **Field** , leaving a **Field** or attempting to submit a **Form**. |
| **hf-disabled** | Present when in the disabled state. |
| **hf-enabled** | Present when not in the disabled state. |
| **hf-required** | Present when in the required state. |
| **hf-optional** | Present when not in the required state. |
| **hf-readonly** | Present when in the read-only state. |
| **hf-readwrite** | Present when not in the read-only state. |
| **hf-focus** | Present when in the focused state. |
| **hf-blur** | Present when not in the focused state. |
| **hf-empty** | Present when in the empty state. |
| **hf-complete** | Present when in the complete state. |
| **hf-hover** | Present when a pointing device is over the **Field**. |
| **hf-placeholder-show**** n** | Present when the placeholder text is displayed. |

In addition to these class names, the **Field** will add any corresponding class names provided by the **classes** option provided when the **Field** is constructed.

For example if the **Field** is constructed with a **classes** option as follows &#39;{disabled: &#39;text-blur text-grey&#39;, enabled: &#39;text-normal&#39;}&#39;, then the &#39;text-blur&#39; and &#39;text-grey&#39; class names will be present whenever the &#39;hf-disabled&#39; class is present and the &#39;text-normal&#39; class name will be present whenever the &#39;hf-enabled&#39; class name is present.

                1.
### Field Styling

The Hosted Payment Fields are styled using CSS as normal.

However, styles have to be transferred from your website to the controls served from our website, therefore styles must be isolated and easily identifiable. To aid with identification, all styles intended for a **Field** must contain the &#39;hostedfield&#39; class name in their selector or &#39;-hostedfield&#39; extension on any id in the selector.

As a website may contain lots of stylesheets, a **Field** cannot be expected to parse every stylesheet present on the page and therefore it only parses those selected using the stylesheets construction option or using the **setStylesheet()** method. By default, this is any stylesheet referenced via a \&lt;link\&gt; tag or \&lt;style\&gt; tag with the &#39;hostedfield&#39; class name: ie any HTML node that matches the following DOM selector &#39;link.hostedfield[rel=stylesheet], style.hostedfield&#39;.

CSS styles using the **Field** state classes, pseudo classes and pseudo elements are supported as follows:

- :focus
- .hf-focus
- :hover
- .hf-hover
- :enabled
- .hf-enabled,
- :disabled
- .hf-disabled
- :valid
- .hf-valid
- :invalid
- .hf-invalid
- :user-valid
- .hf-user-valid
- :user-invalid
- .hf-user-invalid
- :required
- .hf-required
- :optional
- .hf-optional
- :empty
- .hf-empty
- :complete
- .hf-complete
- :autofill
- .hf-autofill
- :placeholder-shown
- .hf-placeholder-shown
- :readonly
- .hf-readonly
- :readwrite
- .hf-readwrite
- :-webkit-auto-fill
- .hf-icon
- ::placeholder
- ::-moz-placeholder
- ::-webkit-input-placeholder
- ::-ms-input-placeholder

The styles can contain any valid CSS rules and will be used to style both the public elements and internal private elements. For security only, styles that relate to the textual representation of the **Field** are passed to the internal private elements. This include styles such as colours, font weights and text decorations. At present, it is not possible to specify custom fonts as they would require the font files to be available on our servers.

The following styles can be used to style the **Field** internal private elements:

- caret-color
- color
- cursor
- direction
- fill
- filter
- font
- font-family
- font-feature-settings
- font-kerning
- font-language-override
- font-size
- font-size-adjust
- font-smooth
- font-stretch
- font-style
- font-synthesis
- font-variant
- font-variant-alternates
- font-variant-caps
- font-variant-east-asian
- font-variant-ligatures
- font-variant-numeric
- font-variant-position
- font-weight
- letter-spacing
- line-height
- stroke
- text-align
- text-decoration
- text-decoration-color
- text-decoration-line
- text-decoration-style
- text-emphasis
- text-emphasis-color
- text-emphasis-position
- text-emphasis-style
- text-indent
- text-rendering
- text-shadow
- text-transform
- text-underline-position
- -moz-osx-font-smoothing
- -webkit-font-smoothing
- -webkit-text-fill-color

The &#39;.hf-icon&#39; class name can be used to target the icon sub element in a **cardDetails**** Field**.

Individual controls can be targeted by using DOM ids, which will have a &#39;-hostedfield&#39; extension added to the DOM id of the original **element**.

It is advisable to keep CSS selectors and rules as simple as possible to avoid styling errors caused by a failure to parse and filter the rules.

Example stylesheet:

1. **\&lt;style**  class=&quot;hostedfield&quot; **\&gt;**
2.     /\*
3.      \* Style hosted field internals
4.      \* - only accept font, foreground and background styling
5.      \*/
6.
7.     /\* Copy of Bootstrap styles \*/
8.     .hostedfield:disabled {
9.         cursor: not-allowed;
10.         background-color: #eee;
11.         opacity: 1;
12.     }
13.
14.     /\* Change text to red when invalid \*/
15.     .form-control:invalid,
16.     .hostedfield:invalid {
17.         border-color: #a94442 !important;
18.         color: #a94442 !important;
19.     }
20.
21.     /\* Change text to light grey when readonly \*/
22.     .form-control:readonly,
23.     .hostedfield:readonly {
24.         color: lightgrey !important;
25.     }
26.
27.     /\* Emulate webkit auto fill style \*/
28.     .form-control.hf-autofill,
29.     .hostedfield.hf-autofill {
30.         background-color: rgb(250, 255, 189) !important;
31.         background-image: none !important;
32.         color: rgb(0, 0, 0) !important;
33.     }
34.
35.     /\* Add pink placeholder \*/
36.     .form-control::placeholder,
37.     .hostedfield::placeholder {
38.         color: pink;
39.     }
40.
41.     /\* Show hovering over the control \*/
42.     .form-control.hf-hover,
43.     .hostedfield.hf-hover {
44.         font-style: italic;
45.     }
46.
47.     /\* Style by id (hosted field will have &#39;-hostedfield&#39; appended to the id) \*/
48.     #form1-card-details.hostedfield, #form1-card-details-hostedfield {
49.         color: blue;
50.     }
51.
52. **\&lt;/style\&gt;**

                1. **jQuery Plugin**

The script will extend the jQuery object with its own plugin methods to allow easy access to **Form** and **Field** objects attached to an **element** as follows:

**$(element).hostedForm(options);**

**$(element).hostedForm(&#39;instance&#39;);**

**$(element).hostedForm(&#39;options&#39;, options);**

**$(element).hostedForm(method, parameters);**

**$(element).hostedForm(&#39;destroy&#39;);**

**$(element).hostedField(options);**

**$(element).hostedField(&#39;instance&#39;);**

**$(element).hostedField(&#39;options&#39;, options);**

**$(element).hostedField(method, parameters);**

**$(element).hostedField(&#39;destroy&#39;);**

The script will also add a &#39;:hostedfield&#39; pseudo selector allowing **Field** elements to be selected using the following example notation:

**$(&#39;INPUT:hostedfield&#39;)**

:

            1. **Example HTTP Requests**
              1.
### Hosted Integration

                1.
### Transaction Request HTTP Headers

The following HTTP headers are sent for transaction request:

| **HTTP Header** | **Mandatory** | **Description** |
| --- | --- | --- |
| **content-type** | **Y** | Content type of the request. This must be &#39;application/x-www-form-urlencoded&#39;, A charset parameter is optional and any non UTF-8 request will be converted to UTF-8. |

                1.
### Transaction Response HTTP Headers

The following HTTP headers are received for a transaction response:

| **HTTP header** | **Description** |
| --- | --- |
| **Status** | HTTP status header. Possible value are: **200** – Transaction request processed **500** – Internal Server Error **503** – Service Temporarily Unavailable |
| **content-type** | Content type of the response. This will be &#39;application/x-www-form-urlencoded&#39; |

                1.
### Submission Example

The following shows an example of a transaction request:

1. HTTP/1.1 200 OK
2. POST /hosted/ HTTP/1.1
3. Host: gateway.example.com
4. Accept: \*/\*
5. Content-Length: 314
6. Content-Type: application/x-www-form-urlencoded
7.
8. merchantID=100001&amp;action=SALE&amp;type=1&amp;currencyCode=826&amp;countryCode=826&amp;amount=680&amp;transactionUnique=5de651c7c5379&amp;orderRef=Test+Transaction&amp;redirectURL=https%3A%2F%2Fmyshop.com&amp;signature=ba12b0766a3412782448f154be15e8f61eea390387b1b23d4688c82c9f28f81df593de5890426546cca365943cc7b5c4897c9721b663a0e17680e1e796f1ad55

The following shows an example of a transaction response:

1. HTTP/1.1 200 OK
2. Date: Tue, 01 Jan 2019 09:30:45 GMT
3. Server: Apache/2.4.23 (Win64) OpenSSL/1.0.2k-fips PHP/5.4.12
4. Vary: Host
5. X-Powered-By: PHP/5.4.12
6. Expires: Thu, 19 Nov 1981 08:52:00 GMT
7. Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
8. Pragma: no-cache
9. Content-Length: 4129
10. Content-Type: text/html
11.
12. \&lt;!DOCTYPE html\&gt;
13. \&lt;html\&gt;
14. --- Hosted Payment Page HTML Removed ---
15. \&lt;/html\&gt;

              1.
### Direct Integration

                1.
### Transaction Request HTTP Headers

The following HTTP headers are sent for transaction request:

| **HTTP Header** | **Mandatory** | **Description** |
| --- | --- | --- |
| **content-type** | **Y** | Content type of the request. This must be &#39;application/x-www-form-urlencoded&#39;, A charset parameter is optional and any none UTF-8 request will be converted to UTF-8. |

                1.
### Transaction Response HTTP Headers

The following HTTP headers are received for a transaction response:

| **HTTP header** | **Description** |
| --- | --- |
| **Status** | HTTP status header. Possible value are:200 – Hosted Payment Form returned500 – Internal Server Error503 – Service Temporarily Unavailable |
| **content-type** | Content type of the response. This will be &#39;text/html&#39; |

                1.
### Submission Example

The following shows an example of a transaction request:

1. POST /direct/ HTTP/1.1
2. Host: gateway.example.com
3. Accept: \*/\*
4. Content-Length: 397
5. Content-Type: application/x-www-form-urlencoded
6.
7. merchantID=100001&amp;action=SALE&amp;type=1&amp;currencyCode=826&amp;countryCode=826&amp;amount=680&amp;transactionUnique=5de65b552499e&amp;orderRef=Test+Transaction&amp;cardNumber=4929+4212+3460+0821&amp;cardCVV=356&amp;cardExpiryDate=1219&amp;threeDSRequired=N&amp;avscv2CheckRequired=N&amp;duplicateDelay=0&amp;signature=06b01e06c8fc761943d676d5f3aa2e9264758fed72e7bcb058a2a35cf23e8e45403099537bb0363054d6bc8ea951ce1ad86e582dbf0b435855b9c97507fcf844

The following shows an example of a transaction response:

1. HTTP/1.1 200 OK
2. Date: Tue, 01 Jan 2019 09:30:45 GMT
3. Server: Apache/2.4.23 (Win64) OpenSSL/1.0.2k-fips PHP/5.4.12
4. Vary: Host
5. X-Powered-By: PHP/5.4.12
6. Content-Length: 2532
7. Content-Type: text/html
8.
9. merchantID=100001&amp;threeDSEnabled=Y&amp;avscv2CheckEnabled=Y&amp;riskCheckEnabled=N&amp;caEnabled=Y&amp;rtsEnabled=Y&amp;cftEnabled=Y&amp;threeDSCheckPref=not+known%2Cnot+checked%2Cauthenticated%2Cattempted+authentication&amp;cv2CheckPref=matched&amp;addressCheckPref=not+known%2Cnot+checked%2Cmatched%2Cpartially+matched&amp;postcodeCheckPref=not+known%2Cnot+checked%2Cmatched%2Cpartially+matched&amp;cardCVVMandatory=Y&amp;riskCheckPref=not+known%3Dfinished%2Cnot+checked%3Ddecline2%2Capprove%3Dcontinue%2Cdecline%3Ddecline1%2Creview%3Ddecline2%2Cescalate%3Dfinished&amp;notifyEmail=an.operator%40merchant.com&amp;customerReceiptsRequired=Y&amp;eReceiptsEnabled=Y&amp;eReceiptsApiKey=C282ZTF885MN0BPL80Q3&amp;eReceiptsStoreID=2&amp;merchantCategoryCode=6013&amp;surchargeEnabled=Y&amp;surchargeRequired=N&amp;surchargeRules%5B0%5D%5BcardType%5D=CC&amp;surchargeRules%5B0%5D%5Bsurcharge%5D=10.1235&amp;surchargeRules%5B1%5D%5BcardType%5D=CC&amp;surchargeRules%5B1%5D%5Bcurrency%5D=GBP&amp;surchargeRules%5B1%5D%5Bsurcharge%5D=2.5000&amp;surchargeRules%5B2%5D%5BcardType%5D=VC&amp;surchargeRules%5B2%5D%5Bsurcharge%5D=3.5000&amp;surchargeRules%5B3%5D%5BcardType%5D=VC&amp;surchargeRules%5B3%5D%5Bcurrency%5D=GBP&amp;surchargeRules%5B3%5D%5Bsurcharge%5D=4.5000&amp;surchargeRules%5B4%5D%5BcardType%5D=DD&amp;surchargeRules%5B4%5D%5Bsurcharge%5D=5.5000&amp;action=SALE&amp;type=1¤cyCode=826&amp;countryCode=826&amp;amount=680&amp;transactionUnique=5de65b552499e&amp;orderRef=Test+Transaction&amp;cardExpiryDate=1219&amp;threeDSRequired=N&amp;avscv2CheckRequired=N&amp;duplicateDelay=0&amp;requestID=5de65b562496f&amp;responseCode=0&amp;responseMessage=AUTHCODE%3A347414&amp;state=captured&amp;requestMerchantID=100001&amp;processMerchantID=100001&amp;paymentMethod=card&amp;cardType=Visa+Credit&amp;cardTypeCode=VC&amp;cardScheme=Visa+&amp;cardSchemeCode=VC&amp;cardIssuer=BARCLAYS+BANK+PLC&amp;cardIssuerCountry=United+Kingdom&amp;cardIssuerCountryCode=GBR&amp;cardFlags=8323072&amp;cardNumberMask=492942%2A%2A%2A%2A%2A%2A0821&amp;cardNumberValid=Y&amp;xref=19120312NG55CM51QH35JRL&amp;cardExpiryMonth=12&amp;cardExpiryYear=19&amp;authorisationCode=347414&amp;transactionID=10018201&amp;responseStatus=0×tamp=2019-12-03+12%3A55%3A52&amp;amountApproved=680&amp;amountReceived=680&amp;amountRetained=680&amp;avscv2ResponseCode=244100&amp;avscv2ResponseMessage=SECURITY+CODE+MATCH+ONLY&amp;avscv2AuthEntity=merchant+host&amp;cv2Check=matched&amp;addressCheck=not+matched&amp;postcodeCheck=not+matched&amp;notifyEmailResponseCode=0&amp;notifyEmailResponseMessage=Email+successfully+queued&amp;vcsResponseCode=0&amp;vcsResponseMessage=Success+-+no+velocity+check+rules+applied&amp;currencyExponent=2&amp;signature=e5c65e5d0340e0ec0de8782affcb6caba2e4d202a6873a1677ddbf6415cb1dd52cc597e43c758b233afd121367d300a57d0faade7abf6b4b88a1a1b974e55d33

              1.
### Batch Integration

                1.
### Submission Request HTTP Headers

The following HTTP headers are sent for batch submission request:

| **HTTP Header** | **Mandatory** | **Description** |
| --- | --- | --- |
| **content-type** | **Y** | Content type of the batch request. This must be &#39;multipart/mixed&#39; andcontain a boundary parameter to separate each transaction request. A charset parameter is optional and any none UTF-8 request will be converted to UTF-8. |
| **content-encoding** | **N** | Optional content encoding applied to the request. The value should be a comma separated list of one or more: **x-gzip** , **gzip** , **base64**. |
| **authorization** | **N** | Optional username and password to authenticate the submitter |

The following HTTP headers are sent on each individual part request:

| **HTTP Header** | **Mandatory** | **Description** |
| --- | --- | --- |
| **content-type** | **Y** | Content type of the individual request. This must be &#39;application/x-www-form-urlencoded&#39;, A charset parameter is optional and any none UTF-8 request will be converted to UTF-8. |
| **content-encoding** | **N** | Optional content encoding applied to the request. The value should be a comma separated list of one or more: **x-gzip** , **gzip** , **base64**. |
| **content-id** | **N** | Optional identifier for each individual transaction with the batch. The Gateway will return this identifier in the submission response.If not sent, the Gateway will generate a unique identifier for each transaction. |

                1.
### Submission Response HTTP Headers

The following HTTP headers are received for batch submission response:

| **HTTP header** | **Description** |
| --- | --- |
| **status** | HTTP status header. Possible value are: **200** – Batch submission status response ok **201** – Batch submission received and stored **400** – Batch submission invalid **401** – Unauthorised (none or incorrect credentials) **405** – HTTP method was not POST/PUT or GET **500** – Internal Gateway error |
| **location** | URL to use to monitor the status of the batch. A unique batch reference number will be provided in the URL in the format: XXXX-XXXX-XXXX-XXXX (e.g. 1A23-B4C5-DEF6-G7HI)
This reference number is used to request information about the status of a batch via HTTP GET requests to the URL endpoint as outlined in section 1.3.3. |
| **x-p3-token** | If user authentication was sent in the initial request, this header will contain a token that can be used for future requests for the status of the batch instead of having to use a username/password. |
| **content-type** | Content type of the HTTP batch request. This will be &#39;multipart/mixed&#39; andcontain a boundary parameter to separate each transaction request. |

The following HTTP headers are received on each individual part response:

| **HTTP header** | **Description** |
| --- | --- |
| **content-type** | Content type of the individual request. This will be &#39;application/x-www-form-urlencoded&#39;, A charset parameter is optional and any none UTF-8 request will be converted to UTF-8. |
| **content-id** | The content ID sent in the initial request as outlined in A-21.3.1. If no content-id header was sent, the Gateway will return a unique content ID per transaction. |
| **x-transaction-id** | The Gateway transaction ID. This will be empty if the transaction is currently pending in this stage. |
| **x-transaction-response** | A message containing the current status of the transaction.
Possible value are: **skipped** – insufficient permissions to view transaction **pending** – queued for processing **success** – (Response Message) **failure** – (Response Message) |

                1.
### Status Request HTTP Headers

The following HTTP headers are used during a batch status request:

| **HTTP Header** | **Mandatory** | **Description** |
| --- | --- | --- |
| **authorization** | **Y** | Mandatory username and password to authenticate the submitter |

                1.
### Status Response HTTP Headers

The batch status response is identical to the submission status response as documented in section A-21.3.2.

                1.
### Submission Example

The following shows an example of a batch submission request:

1. PUT /batch/?validate=0 HTTP/1.1
2. Authorization: Basic bmljay50dXJuZXI6dGVzdGluZzI=
3. Host: gateway.example.com
4. Accept: \*/\*
5. Content-type: multipart/mixed; charset=UTF-8; boundary=5de63a42507a9
6. Content-length: 1404
7.
8. --5de63a42507a9
9. Content-Id: TX5de63a42507ac
10. Content-Type: application/x-www-form-urlencoded; charset=UTF-8
11.
12. merchantID=100001&amp;action=SALE&amp;type=1&amp;currencyCode=826&amp;countryCode=826&amp;amount=680&amp;transactionUnique=5de63a42507ac&amp;orderRef=Test+Transaction&amp;cardNumber=4929+4212+3460+0821&amp;cardExpiryDate=1219&amp;duplicateDelay=0&amp;signature=3cd686fdd40449ef33534baa62732c95fc127ff591fae3b5b611ccb38573ad921d199396e27cffd14faa4f46df8dde310252920fd1b33607b029b9b6ff669e2b
13.
14. --5de63a42507a9
15. Content-Id: TX5de63a42af062
16. Content-Type: application/x-www-form-urlencoded; charset=UTF-8
17.
18. merchantID=100001&amp;action=SALE&amp;type=1&amp;currencyCode=826&amp;countryCode=826&amp;amount=681&amp;transactionUnique=5de63a42af062&amp;orderRef=Test+Transaction&amp;cardNumber=4929+4212+3460+0821&amp;cardExpiryDate=1219&amp;duplicateDelay=0&amp;signature=55f411d40954be7f7089e84fe489438f09fc1b37c0964e46b0fab8bdcb44e13ed3ea11b9deb9da89a6d7b45133709a126bd3581f6329bf888b83231184597231
19.
20. --5de63a42507a9
21. Content-Id: TX5de63a42ca9cd
22. Content-Type: application/x-www-form-urlencoded; charset=UTF-8
23.
24. merchantID=100001&amp;action=SALE&amp;type=1&amp;currencyCode=826&amp;countryCode=826&amp;amount=682&amp;transactionUnique=5de63a42ca9cd&amp;orderRef=Test+Transaction&amp;cardNumber=4929+4212+3460+0821&amp;cardExpiryDate=1219&amp;duplicateDelay=0&amp;signature=c296266cb9bc8082957c700da9651d98add176dd8bd62eb3b7098566c7d8e23a3426b776de815e99149c6681978b1addedac762339563732d8a449b6cca3a3c2
25.
26. --5de63a42507a9--

The following shows an example of a batch submission response:

1. HTTP/1.1 201 Created
2. Date: Tue, 01 Jan 2019 09:30:45 GMT
3. Server: Apache/2.4.23 (Win64) OpenSSL/1.0.2k-fips PHP/5.4.12
4. X-Powered-By: PHP/5.4.12
5. x‑p3‑token: YTo1OntzOjc6InZlcnNpb24iO3M6ODoiUDNUSy8yLjAiO3M6NzoicHVycG9zZSI7czo0OiJhdXRoIjtzOjc6ImNyZWF0b3IiO3M6NToiQkFUQ0giO3M6NzoiY3JlYXRlZCI7aToxNTc1MzY5Mjg1O3M6NzoiZXhwaXJlcyI7aToxNTc1MzcyODg1O30.czozOiI2MjkiOw.zdfxxXYtC2Wc4yyk-lEos-wZ99pEJtPGYpXR4KCiWW\_56nmOysarOaMucrWPIt-NzwFzgq3-7u4Ud6uYkQcWBQ
6. Location: /batch/2D6D-AC2C-BF55-2A8C
7. Content-disposition: attachment; filename=&quot;batch-2D6D-AC2C-BF55-2A8C&quot;
8. Content-Length: 1857
9. Content-Type: multipart/mixed; charset=UTF-8; boundary=5de63a5c1a071
10.
11. Transaction &#39;TX5de63a42507ac&#39; - pending - queued for processing
12. Transaction &#39;TX5de63a42af062&#39; - pending - queued for processing
13. Transaction &#39;TX5de63a42ca9cd&#39; - pending - queued for processing
14.
15. --5de63a5c1a071
16. Content-Id: TX5de63a42507ac
17. Content-Type: application/x-www-form-urlencoded; charset=UTF-8
18. X-Transaction-ID:
19. X-Transaction-Response: pending - queued for processing
20.
21. merchantID=100001&amp;action=SALE&amp;type=1¤cyCode=826&amp;countryCode=826&amp;amount=680&amp;transactionUnique=5de63a42507ac&amp;orderRef=Test+Transaction&amp;cardNumber=492942%2A%2A%2A%2A%2A%2A0821&amp;cardExpiryDate=1219&amp;duplicateDelay=0&amp;signature=0384bbf6ca0fc153e1e27a0cfc51f3b1cd1c2cff7a49aa4e9439bba38262183e9ac7d156f218eba1ef8d04f9e6a7fa6fbc9c2b3ab990c70e06dc7c6923e5b27b
22.
23. --5de63a5c1a071
24. Content-Id: TX5de63a42af062
25. Content-Type: application/x-www-form-urlencoded; charset=UTF-8
26. X-Transaction-ID:
27. X-Transaction-Response: pending - queued for processing
28.
29. merchantID=100001&amp;action=SALE&amp;type=1¤cyCode=826&amp;countryCode=826&amp;amount=681&amp;transactionUnique=5de63a42af062&amp;orderRef=Test+Transaction&amp;cardNumber=492942%2A%2A%2A%2A%2A%2A0821&amp;cardExpiryDate=1219&amp;duplicateDelay=0&amp;signature=1e13e23c2b90a30f4403d604ac20302b5504b886b0b5c9ace0764fc8d966d120f5a1beca975805292780c22953b4e6ca71f67f499804f19d2718518463a598c4
30.
31. --5de63a5c1a071
32. Content-Id: TX5de63a42ca9cd
33. Content-Type: application/x-www-form-urlencoded; charset=UTF-8
34. X-Transaction-ID:
35. X-Transaction-Response: pending - queued for processing
36.
37. merchantID=100001&amp;action=SALE&amp;type=1¤cyCode=826&amp;countryCode=826&amp;amount=682&amp;transactionUnique=5de63a42ca9cd&amp;orderRef=Test+Transaction&amp;cardNumber=492942%2A%2A%2A%2A%2A%2A0821&amp;cardExpiryDate=1219&amp;duplicateDelay=0&amp;signature=c456aa211f8e3e568a40051bfd38406be02566fcd72d3bb1547f4d43e75db1d069eaa4158aa035337cac084633df945a13471db6b1a3fcd6c0749626d9bc0044
38.
39. --5de63a5c1a071--

            1. **Example Integration Code**

The follow section provides samples of how to integrate with the Gateway using the PHP scripting language to communicate directly with the API without the use of any our SDKs.

              1.
### Hosted Integration

                1.
### Sale Transaction

The following example PHP code shows how to send a SALE transaction:

1. \&lt;?PHP
2.
3. // Signature key entered on MMS. The demo account is fixed to this value,
4. $key = &#39;Circle4Take40Idea&#39;;
5.
6. // Gateway URL
7. $url = &#39;https://gateway.example.com/hosted/&#39;;
8.
9.
10. **if**  (!isset($\_POST[&#39;responseCode&#39;])) {
11.     // Send request to gateway
12.
13.     // Request
14.     $req =  **array** (
15.         &#39;merchantID&#39; =\&gt; &#39;100001&#39;,
16.         &#39;action&#39; =\&gt; &#39;SALE&#39;,
17.         &#39;type&#39; =\&gt; 1,
18.         &#39;countryCode&#39; =\&gt; 826,
19.         &#39;currencyCode&#39; =\&gt; 826,
20.         &#39;amount&#39; =\&gt; 1001,
21.         &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
22.         &#39;transactionUnique&#39; =\&gt; uniqid(),
23.         &#39;redirectURL&#39; =\&gt; ($\_SERVER[&#39;HTTPS&#39;] == &#39;on&#39; ? &#39;https&#39; : &#39;http&#39;) . &#39;://&#39; . $\_SERVER[&#39;HTTP\_HOST&#39;] . $\_SERVER[&#39;REQUEST\_URI&#39;],
24.     );
25.
26.     // Create the signature using the function called below.
27.     $req[&#39;signature&#39;] = createSignature($req, $key);
28.
29.     echo &#39;\&lt;form action=&quot;&#39; . htmlentities($url) . &#39;&quot; method=&quot;post&quot;\&gt;&#39; . PHP\_EOL;
30.
31.      **foreach**  ($req  **as**  $field =\&gt; $value) {
32.         echo &#39;    \&lt;input type=&quot;hidden&quot; name=&quot;&#39; . $field . &#39;&quot; value=&quot;&#39; . htmlentities($value) . &#39;&quot;\&gt;&#39; . PHP\_EOL;
33.     }
34.
35.     echo &#39;    \&lt;input type=&quot;submit&quot; value=&quot;Pay Now&quot;\&gt;&#39; . PHP\_EOL;
36.     echo &#39;\&lt;/form\&gt;&#39; . PHP\_EOL;
37.
38. // Check the return signature
39.      **if**  (!$signature || $signature !== createSignature($res, $key)) {
40.         // You should exit gracefully
41.          **die** (&#39;Sorry, the signature check failed&#39;);
42.     }
43.
44.     // Check the response code
45.      **if**  ($res[&#39;responseCode&#39;] === &quot;0&quot;) {
46.         echo &quot;\&lt;p\&gt;Thank you for your payment.\&lt;/p\&gt;&quot;;
47.     }  **else**  {
48.         echo &quot;\&lt;p\&gt;Failed to take payment: &quot; . htmlentities($res[&#39;responseMessage&#39;]) .  &quot;\&lt;/p\&gt;&quot;;
49.     }
50.
51. }
52.
53. // Function to create a message signature
54. **function**  createSignature( **array**  $data, $key) {
55.     // Sort by field name
56.     ksort($data);
57.
58.     // Create the URL encoded signature string
59.     $ret = http\_build\_query($data, &#39;&#39;, &#39;&amp;&#39;);
60.
61.     // Normalise all line endings (CRNL|NLCR|NL|CR) to just NL (%0A)
62.     $ret = str\_replace( **array** (&#39;%0D%0A&#39;, &#39;%0A%0D&#39;, &#39;%0D&#39;), &#39;%0A&#39;, $ret);
63.
64.     // Hash the signature string and the key together
65.      **return**  hash(&#39;SHA512&#39;, $ret . $key);
66. }
67.
68. ?\&gt;

              1.
### Direct Integration

                1.
### Sale Transaction (with 3-D Secure)

The following example PHP code shows how to send a SALE transaction with support for 3-D Secure:

1. \&lt;?PHP
2.
3. // Signature key entered on MMS. The demo account is fixed to this value,
4. $key = &#39;Circle4Take40Idea&#39;;
5.
6. // Gateway URL
7. $url = &#39;https://gateway.example.com/direct/&#39;;
8.
9. // Request
10. $req =  **array** (
11.     &#39;merchantID&#39; =\&gt; &#39;100856&#39;,
12.     &#39;action&#39; =\&gt; &#39;SALE&#39;,
13.     &#39;type&#39; =\&gt; 1,
14.     &#39;countryCode&#39; =\&gt; 826,
15.     &#39;currencyCode&#39; =\&gt; 826,
16.     &#39;amount&#39; =\&gt; 1001,
17.     &#39;cardNumber&#39; =\&gt; &#39;4012001037141112&#39;,
18.     &#39;cardExpiryMonth&#39; =\&gt; 12,
19.     &#39;cardExpiryYear&#39; =\&gt; 15,
20.     &#39;cardCVV&#39; =\&gt; &#39;083&#39;,
21.     &#39;customerName&#39; =\&gt; &#39;Test Customer&#39;,
22.     &#39;customerEmail&#39; =\&gt; &#39;test@testcustomer.com&#39;,
23.     &#39;customerAddress&#39; =\&gt; &#39;16 Test Street&#39;,
24.     &#39;customerPostCode&#39; =\&gt; &#39;TE15 5ST&#39;,
25.     &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
26.     &#39;transactionUnique&#39; =\&gt; (isset($\_POST[&#39;transactionUnique&#39;]) ? $\_POST[&#39;transactionUnique&#39;] : uniqid()),
27.     &#39;threeDSMD&#39; =\&gt; (isset($\_POST[&#39;MD&#39;]) ? $\_POST[&#39;MD&#39;] : null),
28.     &#39;threeDSPaRes&#39; =\&gt; (isset($\_POST[&#39;PaRes&#39;]) ? $\_POST[&#39;PaRes&#39;] : null),
29.     &#39;threeDSPaReq&#39; =\&gt; (isset($\_POST[&#39;PaReq&#39;]) ? $\_POST[&#39;PaReq&#39;] : null)
30. );
31.
32. // Create the signature using the function called below.
33. $req[&#39;signature&#39;] = createSignature($req, $key);
34.
35. // Initiate and set curl options to post to the gateway
36. $ch = curl\_init($url);
37. curl\_setopt($ch, CURLOPT\_POST, true);
38. curl\_setopt($ch, CURLOPT\_POSTFIELDS, http\_build\_query($req));
39. curl\_setopt($ch, CURLOPT\_HEADER, false);
40. curl\_setopt($ch, CURLOPT\_FOLLOWLOCATION, true);
41. curl\_setopt($ch, CURLOPT\_RETURNTRANSFER, true);
42.
43. // Send the request and parse the response
44. parse\_str(curl\_exec($ch), $res);
45.
46. // Close the connection to the gateway
47. curl\_close($ch);
48. // Extract the return signature as this isn&#39;t hashed
49. $signature = null;
50. **if**  (isset($res[&#39;signature&#39;])) {
51.     $signature = $res[&#39;signature&#39;];
52.     unset($res[&#39;signature&#39;]);
53. }
54.
55. // Check the return signature
56. **if**  (!$signature || $signature !== createSignature($res, $key)) {
57.     // You should exit gracefully
58.      **die** (&#39;Sorry, the signature check failed&#39;);
59. }
60.
61. // Check the response code
62. **if**  ($res[&#39;responseCode&#39;] == 65802) {
63.
64.     // Send details to 3D Secure ACS and the return here to repeat request
65.     $pageUrl = (@$\_SERVER[&#39;HTTPS&#39;] == &#39;on&#39;) ? &#39;https://&#39; : &#39;http://&#39;;
66.      **if**  ($\_SERVER[&#39;SERVER\_PORT&#39;] != &#39;80&#39;) {
67.         $pageUrl .= $\_SERVER[&#39;SERVER\_NAME&#39;] . &#39;:&#39; . $\_SERVER[&#39;SERVER\_PORT&#39;] . $\_SERVER[&#39;REQUEST\_URI&#39;];
68.     }  **else**  {
69.         $pageUrl .= $\_SERVER[&#39;SERVER\_NAME&#39;] . $\_SERVER[&#39;REQUEST\_URI&#39;];
70.     }
71.
72.     echo &quot;
73. \&lt;p\&gt;Your transaction requires 3D Secure Authentication\&lt;/p\&gt;
74. \&lt;form action=\&quot;&quot; . htmlentities($res[&#39;threeDSACSURL&#39;]) . &quot;\&quot;method=\&quot;post\&quot;\&gt;
75. \&lt;input type=\&quot;hidden\&quot; name=\&quot;MD\&quot; value=\&quot;&quot; . htmlentities($res[&#39;threeDSMD&#39;]) . &quot;\&quot;\&gt;
76. \&lt;input type=\&quot;hidden\&quot; name=\&quot;PaReq\&quot; value=\&quot;&quot; . htmlentities($res[&#39;threeDSPaReq&#39;]) . &quot;\&quot;\&gt;
77. \&lt;input type=\&quot;hidden\&quot; name=\&quot;TermUrl\&quot; value=\&quot;&quot; . htmlentities($pageUrl) . &quot;\&quot;\&gt;
78. \&lt;input type=\&quot;submit\&quot; value=\&quot;Continue\&quot;\&gt;
79. \&lt;/form\&gt;
80. &quot;;
81.
82. }  **else**   **if**  ($res[&#39;responseCode&#39;] === &quot;0&quot;) {
83.     echo &quot;\&lt;p\&gt;Thank you for your payment.\&lt;/p\&gt;&quot;;
84. }  **else**  {
85.     echo &quot;\&lt;p\&gt;Failed to take payment: &quot; . htmlentities($res[&#39;responseMessage&#39;]) .  &quot;\&lt;/p\&gt;&quot;;
86. }
87.
88. // Function to create a message signature
89. **function**  createSignature( **array**  $data, $key) {
90.     // Sort by field name
91.     ksort($data);
92.
93.     // Create the URL encoded signature string
94.     $ret = http\_build\_query($data, &#39;&#39;, &#39;&amp;&#39;);
95.
96.     // Normalise all line endings (CRNL|NLCR|NL|CR) to just NL (%0A)
97.     $ret = str\_replace( **array** (&#39;%0D%0A&#39;, &#39;%0A%0D&#39;, &#39;%0D&#39;), &#39;%0A&#39;, $ret);
98.
99.     // Hash the signature string and the key together
100.      **return**  hash(&#39;SHA512&#39;, $ret . $key);
101. }
102.
103. ?\&gt;

                1.
### Sale Transaction (without 3-D Secure)

The following sample PHP code shows how to send a SALE transaction without support for 3-D Secure:

1. \&lt;?PHP
2.
3. // Signature key entered on MMS. The demo account is fixed to this value,
4. $key = &#39;Circle4Take40Idea&#39;;
5.
6. // Gateway URL
7. $url = &#39;https://gateway.example.com/direct/&#39;;
8.
9. // Request
10. $req =  **array** (
11.     &#39;merchantID&#39; =\&gt; &#39;100001&#39;,
12.     &#39;action&#39; =\&gt; &#39;SALE&#39;,
13.     &#39;type&#39; =\&gt; 1,
14.     &#39;countryCode&#39; =\&gt; 826,
15.     &#39;currencyCode&#39; =\&gt; 826,
16.     &#39;amount&#39; =\&gt; 1001,
17.     &#39;cardNumber&#39; =\&gt; &#39;4012001037141112&#39;,
18.     &#39;cardExpiryMonth&#39; =\&gt; 12,
19.     &#39;cardExpiryYear&#39; =\&gt; 15,
20.     &#39;cardCVV&#39; =\&gt; &#39;083&#39;,
21.     &#39;customerName&#39; =\&gt; &#39;Test Customer&#39;,
22.     &#39;customerEmail&#39; =\&gt; &#39;test@testcustomer.com&#39;,
23.     &#39;customerPhone&#39; =\&gt; &#39;+44 (0) 123 45 67 890&#39;,
24.     &#39;customerAddress&#39; =\&gt; &#39;16 Test Street&#39;,
25.     &#39;customerPostCode&#39; =\&gt; &#39;TE15 5ST&#39;,
26.     &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
27. &#39;transactionUnique&#39; =\&gt; uniqid(),
28. );
29.
30. // Create the signature using the function called below.
31. $req[&#39;signature&#39;] = createSignature($req, $key);
32.
33. // Initiate and set curl options to post to the gateway
34. $ch = curl\_init($url);
35. curl\_setopt($ch, CURLOPT\_POST, true);
36. curl\_setopt($ch, CURLOPT\_POSTFIELDS, http\_build\_query($req));
37. curl\_setopt($ch, CURLOPT\_HEADER, false);
38. curl\_setopt($ch, CURLOPT\_FOLLOWLOCATION, true);
39. curl\_setopt($ch, CURLOPT\_RETURNTRANSFER, true);
40.
41. // Send the request and parse the response
42. parse\_str(curl\_exec($ch), $res);
43.
44. // Close the connection to the gateway
45. curl\_close($ch);
46.
47. // Extract the return signature as this isn&#39;t hashed
48. $signature = null;
49. **if**  (isset($res[&#39;signature&#39;])) {
50.     $signature = $res[&#39;signature&#39;];
51.     unset($res[&#39;signature&#39;]);
52. }
53.
54. // Check the return signature
55. **if**  (!$signature || $signature !== createSignature($res, $key)) {
56.     // You should exit gracefully
57.      **die** (&#39;Sorry, the signature check failed&#39;);
58. }
59.
60. // Check the response code
61. **if**  ($res[&#39;responseCode&#39;] === &quot;0&quot;) {
62.     echo &quot;\&lt;p\&gt;Thank you for your payment.\&lt;/p\&gt;&quot;;
63. }  **else**  {
64.     echo &quot;\&lt;p\&gt;Failed to take payment: &quot; . htmlentities($res[&#39;responseMessage&#39;]) .  &quot;\&lt;/p\&gt;&quot;;
65. }
66.
67. // Function to create a message signature
68. **function**  createSignature( **array**  $data, $key) {
69.     // Sort by field name
70.     ksort($data);
71.
72.     // Create the URL encoded signature string
73.     $ret = http\_build\_query($data, &#39;&#39;, &#39;&amp;&#39;);
74.
75.     // Normalise all line endings (CRNL|NLCR|NL|CR) to just NL (%0A)
76.     $ret = str\_replace( **array** (&#39;%0D%0A&#39;, &#39;%0A%0D&#39;, &#39;%0D&#39;), &#39;%0A&#39;, $ret);
77.
78.     // Hash the signature string and the key together
79.      **return**  hash(&#39;SHA512&#39;, $ret . $key);
80. }
81.
82. ?\&gt;

              1.
### Batch Integration

                1.
### Batch Submission

The following example PHP code shows how to send a batch request containing three SALE transactions:

1. \&lt;?PHP
2.
3. // Signature key entered on MMS. The demo account is fixed to this value,
4. $key = &#39;Circle4Take40Idea&#39;;
5.
6. // Gateway URL
7. $url = &#39;https://gateway.example.com/batch/&#39;;
8.
9. // Create a unique multipart boundary
10. $boundary = uniqid();
11.
12. // Requests
13. $reqs =  **array** (
14.      **array** (
15.         &#39;merchantID&#39; =\&gt; 100001,
16.         &#39;action&#39; =\&gt; &#39;SALE&#39;,
17.         &#39;type&#39; =\&gt; 1,
18.         &#39;currencyCode&#39; =\&gt; 826,
19.         &#39;countryCode&#39; =\&gt; 826,
20.         &#39;amount&#39; =\&gt; 1001,
21.         &#39;cardNumber&#39; =\&gt; &#39;4012001037141112&#39;,
22.         &#39;cardExpiryMonth&#39; =\&gt; 12,
23.         &#39;cardExpiryYear&#39; =\&gt; 15,
24.         &#39;cardCVV&#39; =\&gt; &#39;083&#39;,
25.         &#39;customerName&#39; =\&gt; &#39;Test Customer&#39;,
26.         &#39;customerEmail&#39; =\&gt; &#39;test@testcustomer.com&#39;,
27.         &#39;customerAddress&#39; =\&gt; &#39;16 Test Street&#39;,
28.         &#39;customerPostCode&#39; =\&gt; &#39;TE15 5ST&#39;,
29.         &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
30.         &#39;transactionUnique&#39; =\&gt; uniqid(),
31.         &#39;threeDSRequired&#39; =\&gt; &#39;N&#39;,
32.         &#39;avscv2CheckRequired&#39; =\&gt; &#39;N&#39;,
33.     ),
34.      **array** (
35.         &#39;merchantID&#39; =\&gt; 100001,
36.         &#39;action&#39; =\&gt; &#39;SALE&#39;,
37.         &#39;type&#39; =\&gt; 1,
38.         &#39;currencyCode&#39; =\&gt; 826,
39.         &#39;countryCode&#39; =\&gt; 826,
40.         &#39;amount&#39; =\&gt; 2002,
41.         &#39;cardNumber&#39; =\&gt; &#39;4012001037141112&#39;,
42.         &#39;cardExpiryMonth&#39; =\&gt; 12,
43.         &#39;cardExpiryYear&#39; =\&gt; 15,
44.         &#39;cardCVV&#39; =\&gt; &#39;083&#39;,
45.         &#39;customerName&#39; =\&gt; &#39;Test Customer&#39;,
46.         &#39;customerEmail&#39; =\&gt; &#39;test@testcustomer.com&#39;,
47.         &#39;customerAddress&#39; =\&gt; &#39;16 Test Street&#39;,
48.         &#39;customerPostCode&#39; =\&gt; &#39;TE15 5ST&#39;,
49.         &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
50.         &#39;transactionUnique&#39; =\&gt; uniqid(),
51.         &#39;threeDSRequired&#39; =\&gt; &#39;N&#39;,
52.         &#39;avscv2CheckRequired&#39; =\&gt; &#39;N&#39;,
53.     ),
54.      **array** (
55.         &#39;merchantID&#39; =\&gt; 100001,
56.         &#39;action&#39; =\&gt; &#39;SALE&#39;,
57.         &#39;type&#39; =\&gt; 1,
58.         &#39;currencyCode&#39; =\&gt; 826,
59.         &#39;countryCode&#39; =\&gt; 826,
60.         &#39;amount&#39; =\&gt; 3003,
61.         &#39;cardNumber&#39; =\&gt; &#39;4012001037141112&#39;,
62.         &#39;cardExpiryMonth&#39; =\&gt; 12,
63.         &#39;cardExpiryYear&#39; =\&gt; 15,
64.         &#39;cardCVV&#39; =\&gt; &#39;083&#39;,
65.         &#39;customerName&#39; =\&gt; &#39;Test Customer&#39;,
66.         &#39;customerEmail&#39; =\&gt; &#39;test@testcustomer.com&#39;,
67.         &#39;customerAddress&#39; =\&gt; &#39;16 Test Street&#39;,
68.         &#39;customerPostCode&#39; =\&gt; &#39;TE15 5ST&#39;,
69.         &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
70.         &#39;transactionUnique&#39; =\&gt; uniqid(),
71.         &#39;threeDSRequired&#39; =\&gt; &#39;N&#39;,
72.         &#39;avscv2CheckRequired&#39; =\&gt; &#39;N&#39;,
73.     ),
74. );
75.
76. // Create the batch parts
77. $parts =  **array** ();
78. **foreach**  ($reqs  **as**  $req) {
79.
80.     // Create the signature using the function called below.
81.     $req[&#39;signature&#39;] = createSignature($req, $key);
82.
83.     $parts[] =
84.         &quot;Content-Id: TX{$req[&#39;transactionUnique&#39;]}\r\n&quot; .
85.         &quot;Content-Type: application/x-www-form-urlencoded; charset=\&quot;UTF-8\&quot;\r\n&quot; .
86.         &quot;\r\n&quot; .
87.         http\_build\_query($req);
88. }
89.
90. // Join the parts together separated by the boundary string
91. $post = &quot;\r\n--{$boundary}\r\n&quot; . join(&quot;\r\n--{$boundary}\r\n&quot;, $parts) . &quot;\r\n--{$boundary}--\r\n&quot;;
92.
93. // Initiate and set curl options to post to the gateway
94. $ch = curl\_init($url);
95. curl\_setopt($ch, CURLOPT\_POST, true);
96. curl\_setopt($ch, CURLOPT\_POSTFIELDS, $post);
97. curl\_setopt($ch, CURLOPT\_HEADER, true);
98. curl\_setopt($ch, CURLOPT\_FOLLOWLOCATION, true);
99. curl\_setopt($ch, CURLOPT\_RETURNTRANSFER, true);
100. curl\_setopt($ch, CURLOPT\_HTTPHEADER,  **array** (
101.     &#39;Content-type: multipart/mixed; charset=&quot;UTF-8&quot;; boundary=&#39; . $boundary,
102.     &#39;Content-length: &#39; . strlen($post),
103. ));
104.
105. // Send the request
106. $res = curl\_exec($ch);
107.
108. // Normally would process the response here, but for this example just echo it out
109. header (&#39;Content-Type: text/plain&#39;);
110. echo $res . PHP\_EOL;
111.
112. // Close the connection to the gateway
113. curl\_close($ch);
114.
115. // Function to create a message signature
116. **function**  createSignature( **array**  $data, $key) {
117.     // Sort by field name
118.     ksort($data);
119.
120.     // Create the URL encoded signature string
121.     $ret = http\_build\_query($data, &#39;&#39;, &#39;&amp;&#39;);
122.
123.     // Normalise all line endings (CRNL|NLCR|NL|CR) to just NL (%0A)
124.     $ret = str\_replace( **array** (&#39;%0D%0A&#39;, &#39;%0A%0D&#39;, &#39;%0D&#39;), &#39;%0A&#39;, $ret);
125.
126.     // Hash the signature string and the key together
127.      **return**  hash(&#39;SHA512&#39;, $ret . $key);
128. }
129.
130. ?\&gt;

            1. **Example Library Code**

The follow section provides samples of how to integrate with the Gateway using our integration libraries as documented in section A-20.1.

              1.
### Gateway Integration Library

                1.
### Hosted Sale Transaction

The following example PHP code shows how to send a SALE transaction using the Gateway library:

1. \&lt;?PHP
2. **require** (&#39;gateway.php&#39;);
3.
4. **use**  \P3\SDK\Gateway;
5.
6. // Signature key entered on MMS. The demo account is fixed to this value,
7. Gateway::$merchantSecret = &#39;Circle4Take40Idea&#39;;
8.
9. // Gateway URL
10. Gateway::$hostedUrl = &#39;https://gateway.example.com/hosted/&#39;;
11.
12. **if**  (!isset($\_POST[&#39;responseCode&#39;])) {
13.     // Send request to gateway
14.     $req =  **array** (
15.         &#39;merchantID&#39; =\&gt; 100001,
16.         &#39;action&#39; =\&gt; &#39;SALE&#39;,
17.         &#39;type&#39; =\&gt; 1,
18.         &#39;currencyCode&#39; =\&gt; 826,
19.         &#39;countryCode&#39; =\&gt; 826,
20.         &#39;amount&#39; =\&gt; 1001,
21.         &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
22.         &#39;redirectURL&#39; =\&gt; ($\_SERVER[&#39;HTTPS&#39;] == &#39;on&#39; ? &#39;https&#39; : &#39;http&#39;) . &#39;://&#39; . $\_SERVER[&#39;HTTP\_HOST&#39;] . $\_SERVER[&#39;REQUEST\_URI&#39;],
23.     );
24.
25.     try {
26.         echo Gateway::hostedRequest($req);
27.     } catch (\Exception $e) {
28.         // You should exit gracefully
29.          **die** (&#39;Sorry, the request could not be sent: &#39; . $e);
30.     }
31.
32. }  **else**  {
33.     // Received response from gateway
34.     try {
35.         Gateway::verifyResponse($\_POST);
36.     } catch(\Exception $e) {
37.         // You should exit gracefully
38.          **die** (&#39;Sorry, the request could not be sent: &#39; . $e);
39.     }
40.
41.     // Check the response code
42.      **if**  ($\_POST[&#39;responseCode&#39;] === 0) {
43.         echo &quot;\&lt;p\&gt;Thank you for your payment.\&lt;/p\&gt;&quot;;
44.     }  **else**  {
45.         echo &quot;\&lt;p\&gt;Failed to take payment: &quot; . htmlentities($\_POST[&#39;responseMessage&#39;]) .  &quot;\&lt;/p\&gt;&quot;;
46.     }
47. }
48.
49. ?\&gt;

                1.
### Direct Sale Transaction (with 3-D Secure)

The following example PHP code shows how to send a SALE transaction with support for 3-D Secure using the Gateway library:

1. \&lt;?PHP
2.
3. **require** (&#39;gateway.php&#39;);
4.
5. **use**  \P3\SDK\Gateway;
6.
7. // Signature key entered on MMS. The demo account is fixed to this value,
8. Gateway::$merchantSecret = &#39;Circle4Take40Idea&#39;;
9.
10. // Gateway URL
11. Gateway::$directUrl = &#39;https://gateway.example.com/direct/&#39;;
12.
13. // Requests
14. $req =  **array** (
15.     &#39;merchantID&#39; =\&gt; 100001,
16.     &#39;action&#39; =\&gt; &#39;SALE&#39;,
17.     &#39;type&#39; =\&gt; 1,
18.     &#39;currencyCode&#39; =\&gt; 826,
19.     &#39;countryCode&#39; =\&gt; 826,
20.     &#39;amount&#39; =\&gt; 1001,
21.     &#39;cardNumber&#39; =\&gt; &#39;4012001037141112&#39;,
22.     &#39;cardExpiryMonth&#39; =\&gt; 12,
23.     &#39;cardExpiryYear&#39; =\&gt; 15,
24.     &#39;cardCVV&#39; =\&gt; &#39;083&#39;,
25.     &#39;customerName&#39; =\&gt; &#39;Test Customer&#39;,
26.     &#39;customerEmail&#39; =\&gt; &#39;test@testcustomer.com&#39;,
27.     &#39;customerAddress&#39; =\&gt; &#39;16 Test Street&#39;,
28.     &#39;customerPostCode&#39; =\&gt; &#39;TE15 5ST&#39;,
29.     &#39;orderRef&#39; =\&gt; &#39;Test purchase&#39;,
30.     &#39;threeDSMD&#39; =\&gt; (isset($\_POST[&#39;MD&#39;]) ? $\_POST[&#39;MD&#39;] : null),
31.     &#39;threeDSPaRes&#39; =\&gt; (isset($\_POST[&#39;PaRes&#39;]) ? $\_POST[&#39;PaRes&#39;] : null),
32.     &#39;threeDSPaReq&#39; =\&gt; (isset($\_POST[&#39;PaReq&#39;]) ? $\_POST[&#39;PaReq&#39;] : null)
33. );
34.
35. try {
36.     $res = Gateway::directRequest($req);
37. } catch (\Exception $e) {
38.     // You should exit gracefully
39.      **die** (&#39;Sorry, the required could not be sent: &#39; . $e);
40. }
41.
42. // Check the response code
43. **if**  ($res[&#39;responseCode&#39;] === 65802) {
44.
45.     // Send details to 3D Secure ACS and the return here to repeat request
46.     $pageUrl = (@$\_SERVER[&#39;HTTPS&#39;] == &#39;on&#39;) ? &#39;https://&#39; : &#39;http://&#39;;
47.      **if**  ($\_SERVER[&#39;SERVER\_PORT&#39;] != &#39;80&#39;) {
48.         $pageUrl .= $\_SERVER[&#39;SERVER\_NAME&#39;] . &#39;:&#39; . $\_SERVER[&#39;SERVER\_PORT&#39;] . $\_SERVER[&#39;REQUEST\_URI&#39;];
49.     }  **else**  {
50.         $pageUrl .= $\_SERVER[&#39;SERVER\_NAME&#39;] . $\_SERVER[&#39;REQUEST\_URI&#39;];
51.     }
52.
53.     echo &quot;
54. \&lt;p\&gt;Your transaction requires 3D Secure Authentication\&lt;/p\&gt;
55. \&lt;form action=\&quot;&quot; . htmlentities($res[&#39;threeDSACSURL&#39;]) . &quot;\&quot;method=\&quot;post\&quot;\&gt;
56. \&lt;input type=\&quot;hidden\&quot; name=\&quot;MD\&quot; value=\&quot;&quot; . htmlentities($res[&#39;threeDSMD&#39;]) . &quot;\&quot;\&gt;
57. \&lt;input type=\&quot;hidden\&quot; name=\&quot;PaReq\&quot; value=\&quot;&quot; . htmlentities($res[&#39;threeDSPaReq&#39;]) . &quot;\&quot;\&gt;
58. \&lt;input type=\&quot;hidden\&quot; name=\&quot;TermUrl\&quot; value=\&quot;&quot; . htmlentities($pageUrl) . &quot;\&quot;\&gt;
59. \&lt;input type=\&quot;submit\&quot; value=\&quot;Continue\&quot;\&gt;
60. \&lt;/form\&gt;
61. &quot;;
62.
63. }  **else**   **if**  ($res[&#39;responseCode&#39;] === 0) {
64.     echo &quot;\&lt;p\&gt;Thank you for your payment.\&lt;/p\&gt;&quot;;
65. }  **else**  {
66.     echo &quot;\&lt;p\&gt;Failed to take payment: &quot; . htmlentities($res[&#39;responseMessage&#39;]) .  &quot;\&lt;/p\&gt;&quot;;
67. }
68.
69. ?\&gt;

              1.
### Hosted Payment Page Library

                1.
### Hosted Sale Transaction

The following example code shows how to prepare a payment form to open the Hosted Payment Page in a lightbox style overlay on your website using the Hosted Payment Page library:

1. **\&lt;html\&gt;**
2.    **\&lt;head\&gt;**
3.     \&lt;!-- Load the Hosted Payment Page library --\&gt;
4.      **\&lt;script**  src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedforms.min.js&quot; **\&gt;\&lt;/script\&gt;**
5.    **\&lt;/head\&gt;**
6.    **\&lt;body\&gt;**
7.     \&lt;!--
8.       Hosted Payment  **\&lt;form\&gt;**  as created by the Gateway Integration Library hostedRequest() method
9.       with addition of &#39;data-hostedforms-modal&#39; attribute to signify a modal form is required.
10.     -- **\&gt;**
11.      **\&lt;form**  name=&quot;payment-form&quot; method=&quot;post&quot; action=&quot;https://gateway.example.com/hosted/&quot; data-hostedforms-modal **\&gt;**
12.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;merchantID&quot; value=&quot;100001&quot;  **/\&gt;**
13.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;action&quot; value=&quot;SALE&quot;  **/\&gt;**
14.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;type&quot; value=&quot;1&quot;  **/\&gt;**
15.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;currencyCode&quot; value=&quot;826&quot;  **/\&gt;**
16.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;countryCode&quot; value=&quot;826&quot;  **/\&gt;**
17.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;amount&quot; value=&quot;1001&quot;  **/\&gt;**
18.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;orderRef&quot; value=&quot;Test purchase&quot;  **/\&gt;**
19.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;redirectURL&quot; value=&quot;https://www.merchant.com/payment/&quot;  **/\&gt;**
20.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;signature&quot; value=&quot;07599ef4cdb2e26cb2bf34a9c65190a7ce82494bc1df144c3bb0d20ee2655d8278dc663b2b0421ef12b8f081e821151bb4c644277c5d65b5523a96539b53b5aa&quot;  **/\&gt;**
21.        **\&lt;input**  type=&quot;submit&quot; value=&quot;Pay Now&quot; **\&gt;**
22.      **\&lt;/form\&gt;**
23.      **\&lt;script\&gt;**
24.         // Create a new Hosted Form object which will cause the above  **\&lt;form\&gt;**  to load into a modal
25.         // overlay over this page.
26.         var form = new window.hostedForms.classes.Form(document.forms[0]);
27.      **\&lt;/script\&gt;**
28.    **\&lt;/body\&gt;**
29. **\&lt;/html\&gt;**

                1.
### Hosted Sale Transaction (jQuery)

The following example code shows how to prepare a payment form to open the Hosted Payment Page in a lightbox style overlay on your website using the Hosted Payment Page and jQuery libraries:

1. **\&lt;html\&gt;**
2.    **\&lt;head\&gt;**
3.     \&lt;!-- Load the jQuery library --\&gt;
4.      **\&lt;script**  src=&quot;https://code.jquery.com/jquery-3.4.1.min.js&quot; integrity=&quot;sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=&quot; crossorigin=&quot;anonymous&quot; **\&gt;\&lt;/script\&gt;**
5.
6.     \&lt;!-- Load the Hosted Payment Page library --\&gt;
7.      **\&lt;script**  src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedforms.min.js&quot; **\&gt;\&lt;/script\&gt;**
8.    **\&lt;/head\&gt;**
9.    **\&lt;body\&gt;**
10.     \&lt;!--
11.       Hosted Payment  **\&lt;form\&gt;**  as created by the Gateway Integration Library hostedRequest() method
12.       with addition of &#39;data-hostedforms-modal&#39; attribute to signify a modal form is required.
13.     -- **\&gt;**
14.      **\&lt;form**  name=&quot;payment-form&quot; method=&quot;post&quot; action=&quot;https://gateway.example.com/hosted/&quot; data-hostedforms-modal **\&gt;**
15.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;merchantID&quot; value=&quot;100001&quot;  **/\&gt;**
16.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;action&quot; value=&quot;SALE&quot;  **/\&gt;**
17.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;type&quot; value=&quot;1&quot;  **/\&gt;**
18.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;currencyCode&quot; value=&quot;826&quot;  **/\&gt;**
19.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;countryCode&quot; value=&quot;826&quot;  **/\&gt;**
20.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;amount&quot; value=&quot;1001&quot;  **/\&gt;**
21.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;orderRef&quot; value=&quot;Test purchase&quot;  **/\&gt;**
22.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;redirectURL&quot; value=&quot;https://www.merchant.com/payment/&quot;  **/\&gt;**
23.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;signature&quot; value=&quot;07599ef4cdb2e26cb2bf34a9c65190a7ce82494bc1df144c3bb0d20ee2655d8278dc663b2b0421ef12b8f081e821151bb4c644277c5d65b5523a96539b53b5aa&quot;  **/\&gt;**
24.        **\&lt;input**  type=&quot;submit&quot; value=&quot;Pay Now&quot; **\&gt;**
25.      **\&lt;/form\&gt;**
26.      **\&lt;script\&gt;**
27.         // Create a new Hosted Form object which will cause the above  **\&lt;form\&gt;**  to load into a modal
28.         // overlay over this page.
29.         var form = $(document.forms[0]).hostedForm();
30.      **\&lt;/script\&gt;**
31.    **\&lt;/body\&gt;**
32. **\&lt;/html\&gt;**

                1.
### Hosted Sale Transaction #2

The following example code shows how to create a payment form to open the Hosted Payment Page in a lightbox style overlay on your website using the Hosted Payment Page library:

1. **\&lt;html\&gt;**
2.    **\&lt;head\&gt;**
3.     \&lt;!-- Load the Hosted Payment Page library --\&gt;
4.      **\&lt;script**  src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedforms.min.js&quot; **\&gt;\&lt;/script\&gt;**
5.    **\&lt;/head\&gt;**
6.    **\&lt;body\&gt;**
7.     \&lt;!— Pay button placeholder --\&gt;
8.      **\&lt;div**  id=&quot;paynow&quot; **\&gt;\&lt;/div\&gt;**
9.      **\&lt;script\&gt;**
10.         // Create a new Hosted Form object which will render a payment button which will load
11.         // the Hosted Payment Pageo load into a modal overlay over this page.
12.
13.         // The request can be provided from your server.
14.         var req = {
15.           merchantID: &#39;100001&#39;,
16.           action: &#39;SALE&#39;,
17.           type: &#39;1&#39;,
18.           currencyCode: &#39;826&#39;,
19.           countryCode: &#39;826&#39;,
20.           amount: &#39;1001&#39;,
21.           orderRef: &#39;Test purchase&#39;,
22.           redirectURL: &#39;https://www.merchant.com/payment/&#39;,
23.           signature: &#39;07599ef4cdb2e26cb2bf34a9c65190a7ce82494bc1df144c3bb0d20ee2655d8278dc663b2b0421ef12b8f081e821151bb4c644277c5d65b5523a96539b53b5aa&#39;,
24.         };
25.
26.         var data = {
27.           id: &#39;my-payment-form&#39;,
28.           url: &#39;https://gateway.example.com/hosted/&#39;,
29.           modal: true,
30.           data: req,
31.           submit: {
32.             type: &#39;button&#39;,
33.             label: &#39;Pay  **\&lt;i\&gt;** Now **\&lt;/i\&gt;**&#39;
34.           }
35.         };
36.
37.         var form = new window.hostedForms.classes.Form(&#39;paynow&#39;, data);
38.      **\&lt;/script\&gt;**
39.    **\&lt;/body\&gt;**
40. **\&lt;/html\&gt;**

                1.
### Hosted Sale Transaction #2 (jQuery)

The following example code shows how to create a payment form to open the Hosted Payment Page in a lightbox style overlay on your website using the Hosted Payment Page and jQuery libraries:

1. **\&lt;html\&gt;**
2.    **\&lt;head\&gt;**
3.     \&lt;!-- Load the jQuery library --\&gt;
4.      **\&lt;script**  src=&quot;https://code.jquery.com/jquery-3.4.1.min.js&quot; integrity=&quot;sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=&quot; crossorigin=&quot;anonymous&quot; **\&gt;\&lt;/script\&gt;**
5.
6.     \&lt;!-- Load the Hosted Payment Page library --\&gt;
7.      **\&lt;script**  src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedforms.min.js&quot; **\&gt;\&lt;/script\&gt;**
8.    **\&lt;/head\&gt;**
9.    **\&lt;body\&gt;**
10.     \&lt;!— Pay button placeholder --\&gt;
11.      **\&lt;div**  id=&quot;paynow&quot; **\&gt;\&lt;/div\&gt;**
12.      **\&lt;script\&gt;**
13.         // Create a new Hosted Form object which will render a payment button which will load
14.         // the Hosted Payment Pageo load into a modal overlay over this page.
15.
16.         // The request can be provided from your server.
17.         var req = {
18.           merchantID: &#39;100001&#39;,
19.           action: &#39;SALE&#39;,
20.           type: &#39;1&#39;,
21.           currencyCode: &#39;826&#39;,
22.           countryCode: &#39;826&#39;,
23.           amount: &#39;1001&#39;,
24.           orderRef: &#39;Test purchase&#39;,
25.           redirectURL: &#39;https://www.merchant.com/payment/&#39;,
26.           signature: &#39;07599ef4cdb2e26cb2bf34a9c65190a7ce82494bc1df144c3bb0d20ee2655d8278dc663b2b0421ef12b8f081e821151bb4c644277c5d65b5523a96539b53b5aa&#39;,
27.         };
28.
29.         var data = {
30.           id: &#39;my-payment-form&#39;,
31.           url: &#39;https://gateway.example.com/hosted/&#39;,
32.           modal: true,
33.           data: req,
34.           submit: {
35.             type: &#39;button&#39;,
36.             label: &#39;Pay  **\&lt;i\&gt;** Now **\&lt;/i\&gt;**&#39;
37.           }
38.         };
39.
40.         var form = $(&#39;#paynow&#39;).hostedForm(data);
41.      **\&lt;/script\&gt;**
42.    **\&lt;/body\&gt;**
43. **\&lt;/html\&gt;**

              1.
### Hosted Payment Fields Library

The following example code shows how to create and manage Hosted Payment Fields using the Hosted Payment Field library.

The example shows how to style fields using an inline stylesheet and how to listen and react to the field&#39;s events.

The example also shows how to set up the payment form both automatically and manually and integrate with the jQuery validator plugin. You should choose the set up method best suited for your needs and whatever validation plugin or functions you are familiar with.

_Note: The example code demonstrates including the static transaction information, such as the_ _ **merchantID** _ _and_ _ **amount** __, in hidden form fields and POSTing the form directly to the Gateway&#39;s Direct Integration using partial message signing. We would however recommend that you capture just the information you require and then POST this data to your own website where you can use it to build a new fully signed request to send to the Gateway&#39;s Direct Integration as a server to server request._

1. **\&lt;html\&gt;**
2.    **\&lt;head\&gt;**
3.     \&lt;!-- Load the jQuery library --\&gt;
4.      **\&lt;script**  src=&quot;https://code.jquery.com/jquery-3.4.1.min.js&quot; integrity=&quot;sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=&quot; crossorigin=&quot;anonymous&quot; **\&gt;\&lt;/script\&gt;**
5.
6.     \&lt;!-- Load the jQuery Validator plugin --\&gt;
7.      **\&lt;script**  src=&quot;https://cdn.jsdelivr.net/npm/jquery-validation@1.19.1/dist/jquery.validate.min.js&quot; **\&gt;\&lt;/script\&gt;**
8.
9.     \&lt;!-- Load the Hosted Payment Field library --\&gt;
10.      **\&lt;script**  src=&quot;https://gateway.example.com/sdk/web/v1/js/hostedfields.min.js&quot; **\&gt;\&lt;/script\&gt;**
11.
12.     \&lt;!-- General styles --\&gt;
13.      **\&lt;style\&gt;**
14.       body {
15.         font-size: 14px;
16.       }
17.
18.       .form-group {
19.         margin: 4px 0 15px 0;
20.       }
21.
22.       .form-group LABEL {
23.         display: inline-block;
24.         max-width: 100%;
25.         margin-bottom: 5px;
26.         font-weight: bold;
27.       }
28.
29.       .form-control {
30.         display: block;
31.         box-sizing: border-box;
32.         height: 34px;
33.         width: 400px;
34.         padding: 6px 12px;
35.         font-size: 14px;
36.         color: #555;
37.         background-color: #fff;
38.         background-image: none;
39.         border: 1px solid #ccc;
40.         border-radius: 4px;
41.         -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
42.         box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
43.         -webkit-transition: border-color ease-in-out .15s, -webkit-box-shadow ease-in-out .15s;
44.         -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
45.         transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
46.       }
47.
48.       .form-control.hf-focus {
49.         border-color: #66afe9;
50.         outline: 0;
51.         -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102,175,233,.6);
52.         box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102,175,233,.6);
53.       }
54.
55.       .has-error .form-control.hf-focus {
56.         border-color: #843534;
57.         -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 6px #ce8483;
58.         box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 6px #ce8483;
59.       }
60.      **\&lt;/style\&gt;**
61.
62.     \&lt;!-- Hosted Field internal styles --\&gt;
63.      **\&lt;style**  class=&quot;hostedfield&quot; **\&gt;**
64.       /\* Grey out when disabled \*/
65.       .hostedfield:disabled {
66.         cursor: not-allowed;
67.         background-color: #eee;
68.         opacity: 1;
69.       }
70.
71.       /\* Change border and text to green when valid \*/
72.       .form-control:valid,
73.       .hostedfield:valid {
74.         border-color: #28a745 !important;
75.         color: #28a745 !important;
76.       }
77.
78.       /\* Change border and text to red when invalid \*/
79.       .form-control:invalid,
80.       .hostedfield:invalid {
81.         border-color: #a94442 !important;
82.         color: #a94442 !important;
83.       }
84.
85.       /\* Change text to light grey when readonly \*/
86.       .form-control:readonly,
87.       .hostedfield:readonly {
88.         color: lightgrey !important;
89.       }
90.
91.       /\* Emulate webkit auto fill style \*/
92.       .form-control.hf-autofill,
93.       .hostedfield.hf-autofill {
94.         background-color: rgb(250, 255, 189) !important;
95.         background-image: none !important;
96.         color: rgb(0, 0, 0) !important;
97.       }
98.
99.       /\* Add light blue placeholder \*/
100.       .form-control::placeholder,
101.       .hostedfield::placeholder {
102.         color: lightblue;
103.       }
104.
105.       /\* Show hovering over the control \*/
106.       .form-control:hover,
107.       .hostedfield:hover {
108.         font-style: italic;
109.       }
110.
111.       /\* Style by id (hosted field will have &#39;-hostedfield&#39; appended to the id) \*/
112.       #form-card-number, #form-card-number-hostedfield {
113.         color: darkcyan;
114.       }
115.
116.      **\&lt;/style\&gt;**
117.
118.     \&lt;!-- Hosted Field card-number internal styles --\&gt;
119.      **\&lt;style**  class=&quot;card-number&quot; **\&gt;**
120.
121.       .hostedfield::placeholder {
122.         color: orange;
123.       }
124.
125.      **\&lt;/style\&gt;**
126.    **\&lt;/head\&gt;**
127.
128.    **\&lt;body\&gt;**
129.     \&lt;!-- tokenise payment data and send directly to the Gateway --\&gt;
130.      **\&lt;form**  id=&quot;form&quot; method=&quot;POST&quot; novalidate=&quot;novalidate&quot; lang=&quot;en&quot;
131.       action=&quot;https://gateway.example.com/direct/&quot;
132.       data-hostedform-tokenize=&#39;{&quot;#form-customer-name&quot;: &quot;customerName&quot;}&#39; **\&gt;**
133.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;merchantID&quot; value=&quot;100001&quot; **\&gt;**
134.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;action&quot; value=&quot;SALE&quot; **\&gt;**
135.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;type&quot; value=&quot;1&quot; **\&gt;**
136.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;countryCode&quot; value=&quot;826&quot; **\&gt;**
137.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;currencyCode&quot; value=&quot;826&quot; **\&gt;**
138.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;amount&quot; value=&quot;1001&quot; **\&gt;**
139.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;orderRef&quot; value=&quot;Test purchase&quot; **\&gt;**
140.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;transactionUnique&quot; value=&quot;1234&quot; **\&gt;**
141.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;redirectURL&quot; value=&quot;https://www.merchant.com/payment/&quot; **\&gt;**
142.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;signature&quot; value=&quot;5a0dd6fed71ef68bb3f20175b6a04bbd9d1c904d32ae3f160bd3b8f55740207e5d1e8de5e7e9960b136407e7454b82e428b8378003aa0146df3efa91a3e61b17|merchantID,action,type,countryCode,currencyCode,amount,orderRef,transactionUnique,redirectURL&quot; **\&gt;**
143.        **\&lt;input**  type=&quot;hidden&quot; name=&quot;paymentToken&quot; value=&quot;&quot; **\&gt;**
144.
145.        **\&lt;div**  class=&quot;form-group&quot; **\&gt;**
146.          **\&lt;label**  for=&quot;form-customer-name&quot; **\&gt;** Name on card: **\&lt;/label\&gt;**
147.          **\&lt;input**  id=&quot;form-customer-name&quot; type=&quot;text&quot; name=&quot;paymentToken[customerName]&quot; autocomplete=&quot;cc-name&quot; class=&quot;form-control form-control-native hostedfield-tokenise&quot; placeholder=&quot;Firstname Surname&quot; required **\&gt;**
148.        **\&lt;/div\&gt;**
149.
150.        **\&lt;div**  class=&quot;form-group&quot; **\&gt;**
151.          **\&lt;label**  for=&quot;form-card-number&quot; **\&gt;** Card Number: **\&lt;/label\&gt;**
152.          **\&lt;input**  id=&quot;form-card-number&quot; type=&quot;hostedfield:cardNumber&quot; name=&quot;card-number&quot; autocomplete=&quot;cc-number&quot; class=&quot;form-control form-control-hosted&quot; style=&quot;background: #f2f8fb;&quot; placeholder=&quot;\*\*\*\* \*\*\*\* \*\*\*\* \*\*\*\*&quot; required **\&gt;**
153.        **\&lt;/div\&gt;**
154.
155.        **\&lt;div**  class=&quot;form-group&quot; **\&gt;**
156.          **\&lt;label**  for=&quot;form-card-expiry-date&quot; **\&gt;** Card Expiry Date: **\&lt;/label\&gt;**
157.          **\&lt;input**  id=&quot;form-card-expiry-date&quot; type=&quot;hostedfield:cardExpiryDate&quot; name=&quot;card-expiry-date&quot; autocomplete=&quot;cc-exp&quot; class=&quot;form-control form-control-hosted&quot; required **\&gt;**
158.        **\&lt;/div\&gt;**
159.
160.        **\&lt;div**  class=&quot;form-group&quot; **\&gt;**
161.          **\&lt;label**  for=&quot;form-card-start-date&quot; **\&gt;** Card Issue Date: **\&lt;/label\&gt;**
162.          **\&lt;input**  id=&quot;form-card-start-date&quot; type=&quot;hostedfield:cardStartDate&quot; name=&quot;card-start-date&quot; autocomplete=&quot;cc-iss&quot; class=&quot;form-control form-control-hosted&quot; data-hostedfield=&#39;{&quot;dropdown&quot;:true}&#39; data-hostedfield-format=&quot;N - m | y&quot; data-hostedfield-min-date=&quot;-40&quot; data-hostedfeld-max-date=&quot;0&quot; **\&gt;**
163.        **\&lt;/div\&gt;**
164.
165.        **\&lt;div**  class=&quot;form-group&quot; **\&gt;**
166.          **\&lt;label**  for=&quot;form-card-cvv&quot; **\&gt;** CVV: **\&lt;/label\&gt;**
167.          **\&lt;input**  id=&quot;form-card-cvv&quot; type=&quot;hostedfield:cardCVV&quot; name=&quot;card-cvv&quot; autocomplete=&quot;cc-csc&quot; class=&quot;form-control form-control-hosted&quot; required **\&gt;**
168.        **\&lt;/div\&gt;**
169.
170.        **\&lt;button**  id=&quot;form-submit&quot; type=&quot;submit&quot; **\&gt;** Pay  **\&lt;span\&gt;** ▷ **\&lt;/span\&gt;\&lt;/button\&gt;**
171.      **\&lt;/form\&gt;**
172.
173.      **\&lt;script\&gt;**
174.       // This example demonstrates both automatic and manual form setup
175.       var automatic\_setup = true;
176.
177.       $(document).ready(function () {
178.
179.         var $form = $(&#39;#form&#39;);
180.
181.         // Listen for events on the form to see those sent from the Hosted Payment Fields
182.         // (For demonstration purposes only)
183.         $form.on(events);
184.
185.         if (automatic\_setup) {
186.           ///////////////////////////////////////////////////////////////
187.           // FORM AUTOMATIC SETUP
188.           ///////////////////////////////////////////////////////////////
189.
190.           var opts = {
191.             // Auto setup the form creating all hosted fields (default)
192.             autoSetup: true,
193.
194.             // Auto validate, tokenise and submit the form (default)
195.             autoSubmit: true,
196.
197.             // Optional field configuration (by type)
198.             fields: {
199.               any: {
200.                 nativeEvents: true,
201.               },
202.               cardNumber: {
203.                 selector: $(&#39;#form-card-number&#39;),
204.                 style: &#39;text-decoration: green wavy underline;&#39;,
205.                 stylesheet: $(&#39;style.hostedfields, style.card-number&#39;)
206.               }
207.             }
208.           };
209.
210.           try {
211.             // Create form, automatically creating all child Hosted Payment Fields
212.             $form.hostedForm(opts);
213.           } catch(e) {
214.             showError(&#39;Failed to create hosted form: &#39; + e);
215.             throw e; // Can&#39;t continue with this script
216.           }
217.
218.           // Listen for some events from the form thrown by the auto methods
219.           $form.on({
220.             // Let jQuery Validator check the form on submission
221.             &#39;hostedform:presubmit&#39;: function (event) {
222.               console.log(&#39;Form submitting&#39;);
223.               return $form.valid();
224.             },
225.
226.             // Show form is valid
227.             &#39;hostedform:valid&#39;: function (event) {
228.               console.log(&#39;Form valid&#39;);
229.               return true;
230.             },
231.
232.             // Show any validation errors
233.             &#39;hostedform:invalid&#39;: function (event, details) {
234.               console.log(&#39;Form invalid&#39;);
235.               showFieldErrors(details.invalid);
236.               return true;
237.             },
238.
239.             // Show general error
240.             &#39;hostedform:error&#39;: function (event, details) {
241.               showError(details.message);
242.               return true;
243.             }
244.           });
245.
246.           // Use jQuery validator to validate the form
247.           $form.validate();
248.
249.           // End of form automatic setup
250.
251.         } else {
252.           ///////////////////////////////////////////////////////////////
253.           // FORM MANUAL SETUP
254.           ///////////////////////////////////////////////////////////////
255.
256.           try {
257.             // Create the card number field with custom options
258.             $(&#39;#form-card-number&#39;).hostedField({
259.               nativeEvents: true,
260.               style: &#39;text-decoration: green wavy underline;&#39;,
261.               stylesheet: $(&#39;style.hostedfields, style.card-number&#39;)
262.             });
263.
264.             // Create the remaining hosted fields
265.             $(&#39;.form-control-hosted:input&#39;, $form).hostedField({nativeEvents: true});
266.
267.           } catch (e) {
268.             showError(&#39;Failed to create hosted fields: &#39; + e);
269.             throw e; // Can&#39;t continue with this script
270.           }
271.
272.           $form.validate({
273.             // Get the hosted form widget for the submitted form (Form1 only)
274.             submitHandler: function () {
275.               try {
276.                 console.log(&#39;getPaymentToken&#39;);
277.
278.                 // Check we have some enabled fields to submit
279.                 if ($($form[0].elements).filter(&#39;:enabled:not([type=&quot;hidden&quot;])&#39;).length === 0) {
280.                   showError(&#39;You must enable some fields&#39;);
281.                   return false;
282.                 }
283.
284.                 var hostedform = $form.hostedForm(&#39;instance&#39;);
285.
286.                 var also = {
287.                   customerName: $(&#39;#form-customer-name&#39;).val()
288.                 };
289.
290.                 hostedform.getPaymentDetails(also, true).then(
291.
292.                   // Success validating the form and requesting a payment token
293.                   function (details) {
294.                     if (details.success) {
295.                       $form[0].elements[&#39;paymentToken&#39;].value = details.paymentToken;
296.                       $form[0].submit();
297.                     } else if (details.invalid) {
298.                       $form.valid();
299.                       showFieldErrors(details.invalid);
300.                     } else {
301.                       showError(&#39;There was a problem fetching the payment token. Please seek assistance.&#39;);
302.                     }
303.                   },
304.
305.                   // Failure either validating the form or requesting the payment details
306.                   function (e) {
307.                     showError(&#39;There was a problem fetching the payment token. Please seek assistance.&#39;);
308.                   }
309.                 );
310.
311.               } catch (e) {
312.                 showError(&#39;There was a problem fetching the payment token. Please seek assistance.&#39;);
313.               }
314.             }
315.           });
316.
317.           // End of form manual setup
318.
319.         }
320.
321.         // Hide errors once all fields are valid
322.         $(&#39;#form :input&#39;).on(&#39;valid&#39;, function () {
323.           if ($(this.form).find(&#39;:invalid&#39;).length === 0) {
324.             hideError($(this.form));
325.           }
326.         })
327.
328.         // Listen for some events on the none Hosted Fields
329.         $(&#39;.form-control-native&#39;).on(&#39;invalid&#39;, bsMarkInvalid);
330.         $(&#39;.form-control-native&#39;).on(&#39;valid&#39;, bsMarkValid);
331.
332.         // Check we can see the Hosted Fields via their new class
333.         // (For demonstration purposes only)
334.         console.log($(&#39;.form-control-hosted.hostedfield-element&#39;));
335.
336.         // Check we can see the Hosted Fields via the psuedo element
337.         // (For demonstration purposes only)
338.         console.log($(&#39;.form-control:hostedfield&#39;));
339.
340.       });
341.
342.       ///////////////////////////////////////////////////////////////////
343.       // Supporting functions
344.       ///////////////////////////////////////////////////////////////////
345.
346.       // Display events that are passed from hosted field
347.       var events = {
348.         &#39;hostedfield:create.example&#39;                           : showEvent,
349.         &#39;hostedfield:destroy.example&#39;                          : showEvent,
350.         &#39;hostedfield:ready.example&#39;                            : showEvent,
351.         &#39;hostedfield:style.example&#39;                            : showEvent,
352.         &#39;hostedfield:placeholder.example&#39;                      : showEvent,
353.         &#39;hostedfield:invalid.example invalid.example&#39;          : showEvent,
354.         &#39;hostedfield:userinvalid.example userinvalid.example&#39;  : showEvent,
355.         &#39;hostedfield:valid.example valid.example&#39;              : showEvent,
356.         &#39;hostedfield:uservalid.example uservalid.example&#39;      : showEvent,
357.         &#39;hostedfield:disabled.example disabled.example&#39;        : showEvent,
358.         &#39;hostedfield:enabled.example enabled.example&#39;          : showEvent,
359.         &#39;hostedfield:required.example required.example&#39;        : showEvent,
360.         &#39;hostedfield:optional.example optional.example&#39;        : showEvent,
361.         &#39;hostedfield:readonly.example readonly.example&#39;        : showEvent,
362.         &#39;hostedfield:readwrite.example readwrite.example&#39;      : showEvent,
363.         &#39;hostedfield:focus.example focus.example&#39;              : showEvent,
364.         &#39;hostedfield:blur.example blur.example&#39;                : showEvent,
365.         &#39;hostedfield:mouseenter.example mouseenter.example&#39;    : showEvent,
366.         &#39;hostedfield:mouseleave.example mouseleave.example&#39;    : showEvent,
367.         &#39;hostedfield:mouseover.example mouseover.example&#39;      : showEvent,
368.         &#39;hostedfield:mouseout.example mouseout.example&#39;        : showEvent,
369.         &#39;hostedfield:mousemove.example mousemove.example&#39;      : showEvent,
370.         &#39;hostedfield:keydown.example keydown.example&#39;          : showEvent,
371.         &#39;hostedfield:keypress.example keypress.example&#39;        : showEvent,
372.         &#39;hostedfield:keyup.example keyup.example&#39;              : showEvent,
373.         &#39;hostedfield:change.example change.example&#39;            : showEvent,
374.         &#39;hostedfield:input.example input.example&#39;              : showEvent,
375.
376.         &#39;hostedfield:invalid.example invalid.example&#39;          : bsMarkInvalid,
377.         &#39;hostedfield:valid.example valid.example&#39;              : bsMarkValid,
378.         &#39;hostedfield:valid.example valid.example&#39;              : hideError,
379.       };
380.
381.       function isInvalid(element) {
382.         return !element[0].checkValidity();
383.       }
384.
385.       function showError(msg) {
386.         $(&#39;#error-info&#39;).html(msg).show();
387.       }
388.
389.       function hideError($form, msg) {
390.         $(&#39;#error-info&#39;, $form).hide();
391.       }
392.
393.       function showFieldErrors(errors) {
394.         var msg = &#39;\&lt;h5\&gt;Error\&lt;/h5\&gt;\&lt;p\&gt;The following fields are invalid:\&lt;/p\&gt;\&lt;ul\&gt;&#39;;
395.         for (var p in errors) {
396.           msg += &#39; **\&lt;li\&gt;\&lt;b\&gt;**&#39; + p + &#39;: **\&lt;/b\&gt;**  &#39; + errors[p] + &#39; **\&lt;/li\&gt;**&#39;;
397.         }
398.         msg += &#39; **\&lt;/ul\&gt;**&#39;
399.         showError(msg);
400.       }
401.
402.       function bsMarkInvalid(e) {
403.         var element = (e instanceof $.Event ? this : e);
404.         $(element).closest(&#39;.form-group&#39;).addClass(&#39;has-error&#39;);
405.       }
406.
407.       function bsMarkValid(e) {
408.         var element = (e instanceof $.Event ? this : e);
409.         $(element).closest(&#39;.form-group&#39;).removeClass(&#39;has-error&#39;);
410.       }
411.
412.       function showEvent(event) {
413.         console.log(event);
414.         console.log(&#39;Field &#39; + event.type + &#39; event: &#39;, this, arguments);
415.       }
416.
417.       jQuery.validator.setDefaults({
418.         ignore: [],
419.         rules: {
420.           &#39;customer-name&#39;: {
421.             checkValidity: true,
422.             required: false
423.           },
424.           &#39;card-details&#39;: {
425.             checkValidity: true,
426.             required: false
427.           },
428.           &#39;card-number&#39;: {
429.             checkValidity: true,
430.             required: false
431.           },
432.           &#39;card-expiry-date&#39;: {
433.             checkValidity: true,
434.             required: false
435.           },
436.           &#39;card-start-date&#39;: {
437.             checkValidity: true,
438.             required: false
439.           },
440.           &#39;card-issue-number&#39;: {
441.             checkValidity: true,
442.             required: false
443.           },
444.           &#39;card-cvv&#39;: {
445.             checkValidity: true,
446.             required: false
447.           }
448.         },
449.         keyup: null, // Don\&#39;t validate on keyup
450.         showErrors: function (errorMap, errorList) {
451.           if (errorList &amp;&amp; errorList.length) {
452.             var errors = {};
453.             for (var i = 0, max\_i = errorList.length; i  **\&lt;**   **max\_i** ; i++ ) {
454.               var label = $(&#39;label[for=&quot;&#39; + errorList[i].element.id + &#39;&quot;]:not(&quot;.error&quot;)&#39;).text();
455.               errors[label] = errorList[i].message;
456.             }
457.             showFieldErrors(errors);
458.           }
459.           this.defaultShowErrors(errorMap, errorList);
460.         },
461.         highlight: bsMarkInvalid,
462.         unhighlight: bsMarkValid,
463.         errorPlacement: function (error, element) {
464.           $(element).closest(&#39;.form-control:not(&quot;.hostedfield-element&quot;)&#39;).after(error);
465.         }
466.       });
467.
468.       $.validator.addMethod(&#39;checkValidity&#39;,
469.         function (value, element, params, message) {
470.           element.checkValidity();
471.           var valid = (element.validationMessage === &#39;&#39;);
472.           $(element).attr(&#39;aria-invalid&#39;, !valid);
473.           return valid;
474.         },
475.         function (params, element) {
476.           return element.validationMessage;
477.         }
478.       );
479.
480.      **\&lt;/script\&gt;**
481.
482.    **\&lt;/body\&gt;**
483. **\&lt;/html\&gt;**

            1. **Frequently Asked Questions**

**1. I&#39;m getting Invalid Credentials. What do I do?**

- Check your Merchant ID in your integration is correct. Our Gateway Merchant IDs typically begin with 1 and are currently 6 digits long, e.g. 100001.

**2. I&#39;m getting an invalid signature error message. How do I fix it?**

- Check that you are using the correct method for calculating the signature and the correct secret signature key for the Merchant Account used.

- Make sure that you are not using an image form submit button because that will add fields to the post that cannot be removed and will render the signature useless.

Refer to appendix A-13 for a step by step guide to creating a signature. If you use the same values as in the example, you can check if your signature generation routine produces the same results.

This test step by step generator is available from the Gateway by adding the following to your Gateway URL:

[/devtools/sigtest.php](/C:%5Cdevtools%5Csigtest.php)

**3. I have more than one Merchant ID - how do I use more than one?**

- You have a couple of options here. You can set up separate integrations for each MID, which can be a bit inconvenient. Your other option is to request they are connected together. Please contact our support team to get your MIDs connected and you will then only need to use one.

**4. I receive a &#39;Bad Testcard Usage&#39; error message. Why?**

- If you receive this error message, you are using test cards on a live Merchant ID. Please only use live cards on live Merchant IDs. Our test cards will only work on the test Merchant ID provided when you sign up with us.

# Index

**[1](#_Toc66871546)****Gateway Integration 4**

[1.1About This Guide 4](#_Toc66871547)

[1.2Terminology 5](#_Toc66871548)

[1.3Integration Methods 6](#_Toc66871549)

_[1.3.1](#_Toc66871550)__Hosted Integration 6_

_[1.3.2](#_Toc66871551)__Direct Integration 7_

_[1.3.3](#_Toc66871552)__Batch Integration 7_

[1.4Integration Libraries 8](#_Toc66871553)

[1.5Security and Compliance 9](#_Toc66871554)

[Integration Details 10](#_Toc66871555)

_[1.5.1](#_Toc66871556)__HTTP Requests 10_

_[1.5.2](#_Toc66871557)__Hosted HTTP Requests 11_

_[1.5.3](#_Toc66871558)__Direct HTTP Requests 11_

_[1.5.4](#_Toc66871559)__Batch HTTP Requests 12_

_[1.5.5](#_Toc66871560)__Handling Errors 14_

_[1.5.6](#_Toc66871561)__Redirect URL 15_

_[1.5.7](#_Toc66871562)__Callback URL 15_

_[1.5.8](#_Toc66871563)__Field Formats 16_

[1.6Authentication 17](#_Toc66871564)

_[1.6.1](#_Toc66871565)__Password Authentication 17_

_[1.6.2](#_Toc66871566)__Message signing 17_

_[1.6.3](#_Toc66871567)__Allowed IP addresses 17_

[1.7Supported Actions 18](#_Toc66871568)

_[1.7.1](#_Toc66871569)__SALE 18_

_[1.7.2](#_Toc66871570)__VERIFY 18_

_[1.7.3](#_Toc66871571)__PREAUTH 18_

_[1.7.4](#_Toc66871572)__REFUND\_SALE 19_

_[1.7.5](#_Toc66871573)__REFUND 19_

_[1.7.6](#_Toc66871574)__CAPTURE 19_

_[1.7.7](#_Toc66871575)__CANCEL 20_

_[1.7.8](#_Toc66871576)__QUERY 20_

**[2](#_Toc66871577)****New Transactions 21**

[2.1Request Fields 21](#_Toc66871578)

[2.2Response Fields 23](#_Toc66871579)

**[3](#_Toc66871580)****Management Requests 25**

[3.1Request Fields 25](#_Toc66871581)

[3.2Response Fields 26](#_Toc66871582)

**[4](#_Toc66871583)****Hosted Payment Page Options 27**

[4.1Request Fields 27](#_Toc66871584)

**[5](#_Toc66871585)****AVS/CV2 Checking 29**

[5.1Background 29](#_Toc66871586)

_[5.1.1](#_Toc66871587)__AVS Checking 29_

_[5.1.2](#_Toc66871588)__CV2 Checking 29_

[5.2Benefits and Limitations 30](#_Toc66871589)

_[5.2.1](#_Toc66871590)__Benefits 30_

_[5.2.2](#_Toc66871591)__Limitations 30_

[5.3Request Fields 31](#_Toc66871592)

[5.4Response Fields 32](#_Toc66871593)

**[6](#_Toc66871594)****3-D Secure Authentication 33**

[6.1Background 33](#_Toc66871595)

[6.2Benefits and Limitations 34](#_Toc66871596)

_[6.2.1](#_Toc66871597)__Benefits 34_

_[6.2.2](#_Toc66871598)__Limitations 34_

[6.3Hosted Implementation 35](#_Toc66871599)

[6.4Direct Implementation 36](#_Toc66871600)

_[6.4.1](#_Toc66871601)__Initial Request (Verify Enrolment) 36_

_[6.4.2](#_Toc66871602)__Continuation Request (Check AuthenticationandAuthorise) 36_

_[6.4.3](#_Toc66871603)__Multiple Challenges and Frictionless Flow 37_

_[6.4.4](#_Toc66871604)__Cardholder Challenge 37_

_[6.4.5](#_Toc66871605)__Device Fingerprinting Challenge 37_

_[6.4.6](#_Toc66871606)__External Authentication Request 37_

[6.5Request Fields 38](#_Toc66871607)

_[6.5.1](#_Toc66871608)__Initial Request (Hosted and Direct Integration) 38_

_[6.5.2](#_Toc66871609)__Continuation Request (Direct Integration) 39_

_[6.5.3](#_Toc66871610)__External Authentication Request (Direct Integration) 40_

_[6.5.4](#_Toc66871611)__3-D Secure 2 Options (Hosted and Direct Integration) 41_

[6.6Response Fields 46](#_Toc66871612)

_[6.6.1](#_Toc66871613)__Initial Response (Direct Integration) 46_

_[6.6.2](#_Toc66871614)__Continuation Response (Direct Integration) 47_

_[6.6.3](#_Toc66871615)__External Authentication Response (Direct Integration) 48_

_[6.6.4](#_Toc66871616)__Cardholder Information (Hosted and Direct Integration) 48_

**[7](#_Toc66871617)****Risk Checking 49**

[7.1Background 49](#_Toc66871618)

[7.2Benefits and Limitations 50](#_Toc66871619)

_[7.2.1](#_Toc66871620)__Benefits 50_

_[7.2.2](#_Toc66871621)__Limitations 50_

[7.3Implementation 51](#_Toc66871622)

[7.4Request Fields 52](#_Toc66871623)

_[7.4.1](#_Toc66871624)__Request Fields 52_

_[7.4.2](#_Toc66871625)__Risk Check Options 53_

[7.5Response Fields 56](#_Toc66871626)

**[8](#_Toc66871627)****Payment Facilitators 57**

[8.1Background 57](#_Toc66871628)

[8.2Request Fields 57](#_Toc66871629)

**[9](#_Toc66871630)****UK MCC 6012 Merchants 58**

[9.1Background 58](#_Toc66871631)

[9.2Request Fields 59](#_Toc66871632)

**[10](#_Toc66871633)****Billing Descriptor 60**

[10.1Background 60](#_Toc66871634)

_[10.1.1](#_Toc66871635)__Static Descriptor 60_

_[10.1.2](#_Toc66871636)__Dynamic Descriptor 60_

[10.2Request Fields 61](#_Toc66871637)

**[11](#_Toc66871638)****Surcharges 62**

[11.1Background 62](#_Toc66871639)

[11.2Implementation 63](#_Toc66871640)

_[11.2.1](#_Toc66871641)__Surcharge Rules 63_

_[11.2.2](#_Toc66871642)__Surcharge Amounts 63_

[11.3Request Fields 64](#_Toc66871643)

[11.4Response Fields 65](#_Toc66871644)

**[12](#_Toc66871645)****Receipts and Notifications 66**

[12.1Background 66](#_Toc66871646)

_[12.1.1](#_Toc66871647)__Customer Email Receipts 66_

_[12.1.2](#_Toc66871648)__Merchant Email Notifications 66_

[12.2Request Fields 67](#_Toc66871649)

_[12.2.1](#_Toc66871650)__General Fields 67_

[12.3Response Fields 69](#_Toc66871651)

**[13](#_Toc66871652)****Recurring Transaction Agreements 70**

[13.1Background 70](#_Toc66871653)

[13.2Scheduling 71](#_Toc66871654)

_[13.2.1](#_Toc66871655)__Fixed Scheduling 71_

_[13.2.2](#_Toc66871656)__Variable Scheduling 71_

[13.3Request Fields 72](#_Toc66871657)

[13.4Response Fields 73](#_Toc66871658)

**[14](#_Toc66871659)****Duplicate Transaction Checking 74**

[14.1Background 74](#_Toc66871660)

[14.2Implementation 74](#_Toc66871661)

[14.3Request Fields 74](#_Toc66871662)

**[15](#_Toc66871663)****Purchase Data 75**

[15.1Background 75](#_Toc66871664)

_[15.1.1](#_Toc66871665)__American Express Purchases 75_

_[15.1.2](#_Toc66871666)__Purchase Orders 75_

[15.2Request Fields 76](#_Toc66871667)

**[16](#_Toc66871668)****Custom Data 79**

[16.6Request Fields 79](#_Toc66871669)

**[17](#_Toc66871670)****Advanced Data 80**

[17.1Customer Request Fields 80](#_Toc66871671)

[17.2Merchant Request Fields 81](#_Toc66871672)

[17.3Supplier Request Fields 82](#_Toc66871673)

[17.4Delivery Request Fields 83](#_Toc66871674)

[17.5Receiver Request Fields 84](#_Toc66871675)

[17.6Shipping Request Fields 85](#_Toc66871676)

**[18](#_Toc66871677)****Gateway Wallet 87**

[18.1Background 87](#_Toc66871678)

[18.2Benefits and Limitations 88](#_Toc66871679)

_[18.2.1](#_Toc66871680)__Benefits 88_

_[18.2.2](#_Toc66871681)__Limitations 88_

[18.3Hosted Implementation 89](#_Toc66871682)

[18.4Direct Implementation 90](#_Toc66871683)

[18.5Request Fields 91](#_Toc66871684)

[18.6Response Fields 93](#_Toc66871685)

**[19](#_Toc66871686)****Masterpass Wallet 94**

[19.1Background 94](#_Toc66871687)

[19.2Benefits and Limitations 95](#_Toc66871688)

_[19.2.1](#_Toc66871689)__Benefits 95_

_[19.2.2](#_Toc66871690)__Limitations 95_

[19.3Hosted Implementation 96](#_Toc66871691)

[19.4Direct Implementation 97](#_Toc66871692)

_[19.4.1](#_Toc66871693)__Initial Request (Checkout Preparation) 97_

_[19.4.2](#_Toc66871694)__Continuation Request (Checkout Details and Authorise) 97_

_[19.4.3](#_Toc66871695)__Separate Checkout Details and Authorisation Requests 98_

[19.5Request Fields 99](#_Toc66871696)

_[19.5.1](#_Toc66871697)__Initial Request (Hosted and Direct Integrations) 99_

_[19.5.2](#_Toc66871698)__Continuation Request (Direct Integration) 99_

_[19.5.3](#_Toc66871699)__Wallet Options (Hosted and Direct Integrations) 100_

_[19.5.4](#_Toc66871700)__Purchase details (Hosted and Direct Integrations) 102_

[19.6Response Fields 103](#_Toc66871701)

_[19.6.1](#_Toc66871702)__Initial Response (Direct Integration) 103_

_[19.6.2](#_Toc66871703)__Continuation Response (Direct Integration) 104_

**[20](#_Toc66871704)****PayPal Transactions 105**

[20.1Background 105](#_Toc66871705)

[20.2Benefits and Limitations 106](#_Toc66871706)

_[20.2.1](#_Toc66871707)__Benefits 106_

_[20.2.2](#_Toc66871708)__Limitations 106_

[20.3Hosted Implementation 107](#_Toc66871709)

[20.4Direct Implementation 108](#_Toc66871710)

_[20.4.1](#_Toc66871711)__Initial Request (Checkout Preparation) 108_

_[20.4.2](#_Toc66871712)__Continuation Request (Checkout Details and Authorise) 108_

_[20.4.3](#_Toc66871713)__Separate Checkout Details and Authorisation Requests 109_

[20.5Request Fields 110](#_Toc66871714)

_[20.5.1](#_Toc66871715)__Initial Request (Hosted and Direct Integrations) 110_

_[20.5.2](#_Toc66871716)__Continuation Request (Direct Integration) 110_

_[20.5.3](#_Toc66871717)__Checkout Options (Hosted and Direct Integrations) 111_

_[20.5.4](#_Toc66871718)__Purchase details (Hosted and Direct Integrations) 116_

[20.6Response Fields 117](#_Toc66871719)

_[20.6.1](#_Toc66871720)__Initial Response (Direct Integration) 117_

_[20.6.2](#_Toc66871721)__Continuation Response (Direct Integration) 118_

_[20.6.3](#_Toc66871722)__Checkout Details (Hosted and Direct Integration) 119_

[20.7Transaction Lifecycle 127](#_Toc66871723)

_[20.7.1](#_Toc66871724)__Order 127_

_[20.7.2](#_Toc66871725)__Authorise 127_

_[20.7.3](#_Toc66871726)__Sale 127_

_[20.7.4](#_Toc66871727)__Capture 127_

_[20.7.5](#_Toc66871728)__Refund 128_

_[20.7.6](#_Toc66871729)__Cancel 128_

_[20.7.7](#_Toc66871730)__Pending Payments 128_

[20.8Reference Transactions 129](#_Toc66871731)

**[21](#_Toc66871732)****Amazon Pay Transaction 130**

[21.1Background 130](#_Toc66871733)

[21.2Benefits and Limitations 131](#_Toc66871734)

_[21.2.1](#_Toc66871735)__Benefits 131_

_[21.2.2](#_Toc66871736)__Limitations 131_

[21.3Hosted Implementation 132](#_Toc66871737)

[21.4Direct Implementation 133](#_Toc66871738)

_[21.4.1](#_Toc66871739)__Initial Request (Checkout Preparation) 133_

_[21.4.2](#_Toc66871740)__Continuation Request (Checkout Details and Authorise) 133_

_[21.4.3](#_Toc66871741)__Separate Checkout Details and Authorisation Requests 134_

[21.5Request Fields 135](#_Toc66871742)

_[21.5.1](#_Toc66871743)__Initial Request (Hosted and Direct Integration) 135_

_[21.5.2](#_Toc66871744)__Continuation Request (Direct Integration) 135_

_[21.5.3](#_Toc66871745)__Checkout Options (Hosted and Direct Integration) 136_

_[21.5.4](#_Toc66871746)__Response Fields 137_

_[21.5.5](#_Toc66871747)__Initial Response (Direct Integration) 137_

_[21.5.6](#_Toc66871748)__Continuation Response (Direct Integration) 138_

_[21.5.7](#_Toc66871749)__Checkout Details (Hosted and Direct Integration) 139_

[21.6Transaction Lifecycle 140](#_Toc66871750)

_[21.6.1](#_Toc66871751)__Capture 140_

_[21.6.2](#_Toc66871752)__Refund Sale 140_

[21.7Reference Transactions 141](#_Toc66871753)

**[22](#_Toc66871754)****PPRO Transactions 142**

[22.1Background 142](#_Toc66871755)

[22.2Benefits and Limitations 143](#_Toc66871756)

_[22.2.1](#_Toc66871757)__Benefits 143_

_[22.2.2](#_Toc66871758)__Limitations 143_

[22.3Hosted Implementation 144](#_Toc66871759)

[22.4Direct Implementation 145](#_Toc66871760)

_[22.4.1](#_Toc66871761)__Payment Request 145_

_[22.4.2](#_Toc66871762)__Payment Specific Fields 145_

_[22.4.3](#_Toc66871763)__Payment Method Tags 146_

[22.5Request Fields 150](#_Toc66871764)

_[22.5.1](#_Toc66871765)__Initial Request (Hosted and Direct Integration) 150_

_[22.5.2](#_Toc66871766)__Checkout Options (Hosted and Direct Integration) 151_

[22.6Response Fields 152](#_Toc66871767)

_[22.6.1](#_Toc66871768)__Initial Response (Direct Integration) 152_

_[22.6.2](#_Toc66871769)__Completion Response (Hosted and Direct Integration) 152_

_[22.6.3](#_Toc66871770)__Notifications and &quot;Tendered&quot; Payments 153_

**[23](#_Toc66871771)****Digital Wallet Transactions 154**

[23.1Background 154](#_Toc66871772)

[23.2Benefits and Limitations 155](#_Toc66871773)

_[23.2.1](#_Toc66871774)__Benefits 155_

_[23.2.2](#_Toc66871775)__Limitations 155_

[23.3Configuration 156](#_Toc66871776)

_[23.3.1](#_Toc66871777)__Apple Pay configuration 156_

_[23.3.2](#_Toc66871778)__Google Pay configuration 156_

[23.4Hosted Implementation 157](#_Toc66871779)

[23.5Direct Implementation 158](#_Toc66871780)

[23.6Request Fields 158](#_Toc66871781)

[23.7Response Fields 158](#_Toc66871782)

**[A-1](#_Toc66871783)****Response Codes 159**

**[A-2](#_Toc66871784)****AVS / CV2 Check Response Codes 167**

**[A-3](#_Toc66871785)****3-D Secure Enrolment/Authentication Codes 169**

**[A-4](#_Toc66871786)****3-D Secure Enrolment/Authentication Only 170**

**[A-5](#_Toc66871787)****SCA Exemptions 171**

**[A-6](#_Toc66871788)****Secure Legacy API 172**

[A 3.1 Background 172](#_Toc66871789)

[A 3.2 Direct Implementation 172](#_Toc66871790)

_[A-3.2.1 Initial Request (Direct Integration) 173](#_Toc66871791)_

_[A-3.2.2 Continuation Request (Direct Integration) 173](#_Toc66871792)_

_[A-3.2.3 Initial Request (Direct Integration) 174](#_Toc66871793)_

_[A-3.2.4 Continuation Request (Direct Integration) 174](#_Toc66871794)_

[A 3.2 Response Fields 175](#_Toc66871795)

_[A-3.2.1 Initial Response (Direct Integration) 175](#_Toc66871796)_

_[A-3.2.2 Continuation Response (Direct Integration) 176](#_Toc66871797)_

[A-3.3 3-D Secure Enrolment/Authentication Only (Direct Only) 177](#_Toc66871798)

**[A-7](#_Toc66871799)****Request Checking Only 178**

**[A-8](#_Toc66871800)****Merchant Account Mapping 179**

**[A-9](#_Toc66871801)****Velocity Control System (VCS) 180**

**[A-10](#_Toc66871802)****Capture Delay 181**

**[A-11](#_Toc66871803)****Types of card 182**

**[A-12](#_Toc66871804)****Integration Testing 184**

[A-12.1 Test Card Details 184](#_Toc66871805)

_[A-12.1.1 Visa Credit 184](#_Toc66871806)_

_[A-12.1.2 Visa Debit 185](#_Toc66871807)_

_[A-12.1.3 Mastercard Credit 185](#_Toc66871808)_

_[A-12.1.4 Mastercard Debit 185](#_Toc66871809)_

[A-12.2 PayPal Sandbox Accounts 189](#_Toc66871810)

[A-12.3 Amazon Pay Sandbox Accounts 189](#_Toc66871811)

**[A-13](#_Toc66871812)****Sample Signature Calculation 190**

**[A-14](#_Toc66871813)****Transaction Life cycle 192**

[A-14.1 Authorise, Capture and Settlement 192](#_Toc66871814)

_[A-14.1.1 Authorisation 192](#_Toc66871815)_

_[A-14.1.2 Capture 192](#_Toc66871816)_

_[A-14.1.3 Settlement 192](#_Toc66871817)_

[A-14.2 Transaction States 193](#_Toc66871818)

_[A-14.2.1 Received 193](#_Toc66871819)_

_[A-14.2.2 Approved 193](#_Toc66871820)_

_[A-14.2.3 Verified 193](#_Toc66871821)_

_[A-14.2.4 Declined 193](#_Toc66871822)_

_[A-14.2.5 Referred 193](#_Toc66871823)_

_[A-14.2.6 Reversed 194](#_Toc66871824)_

_[A-14.2.7 Captured 194](#_Toc66871825)_

_[A-14.2.8 Tendered 194](#_Toc66871826)_

_[A-14.2.9 Deferred 194](#_Toc66871827)_

_[A-14.2.10 Accepted 195](#_Toc66871828)_

_[A-14.2.11 Rejected 195](#_Toc66871829)_

_[A-14.2.12 Canceled 195](#_Toc66871830)_

_[A-14.2.13 Finished 195](#_Toc66871831)_

**[A-15](#_Toc66871832)****Transaction types 196**

[A-15.1 E-commerce (ECOM) 196](#_Toc66871833)

[A-15.2 Mail Order/Telephone Order (MOTO) 196](#_Toc66871834)

[A-15.3 Continuous Authority (CA) 196](#_Toc66871835)

**[A-16](#_Toc66871836)****Payment Tokenisation 197**

[A-16.1 PREAUTH, SALE, REFUND, VERIFY requests 197](#_Toc66871837)

[A-16.2 REFUND\_SALE requests 198](#_Toc66871838)

[A-16.3 CANCEL or CAPTURE requests 198](#_Toc66871839)

[A-16.4 QUERY requests 198](#_Toc66871840)

[A-16.5 SALE or REFUND Referred Authorisation requests 199](#_Toc66871841)

**[A-17](#_Toc66871842)****Repeat Transactions 200**

[A-17.1 MOTO Transactions 200](#_Toc66871843)

_[A-17.1.1 Initial Transaction 200](#_Toc66871844)_

_[A-17.1.2 Repeat Transaction 200](#_Toc66871845)_

[A-17.2 Continuous Payment Agreements 201](#_Toc66871846)

_[A-17.2.1 Initial Transaction 201](#_Toc66871847)_

_[A-17.2.2 Repeat Transaction 201](#_Toc66871848)_

**[A-18](#_Toc66871849)****Transaction Cloning 203**

[A-18.1 Cloned Fields 204](#_Toc66871850)

[A-18.2 Cloned Groups 208](#_Toc66871851)

_[A-18.2.1 Compound Groups 208](#_Toc66871852)_

_[A-18.2.2 Line Item Data 208](#_Toc66871853)_

_[A-18.2.3 Amount Consistency 208](#_Toc66871854)_

**[A-19](#_Toc66871855)****Stored Credentials Framework 209**

[A-19.1 Credentials on File (CoF) 210](#_Toc66871856)

[A-19.2 Consumer Initiated Transactions (CIT) 211](#_Toc66871857)

[A-19.3 Merchant Initiated Transactions (MIT) 212](#_Toc66871858)

_[A-19.3.4 Standing Instruction MITs 212](#_Toc66871859)_

_[A-19.3.5 Industry-Specific Business Practice MIT 213](#_Toc66871860)_

**[A-20](#_Toc66871861)****Integration Libraries 215**

[A-20.1 Gateway Integration Library 216](#_Toc66871862)

_[A-20.1.1 Library Namespace 216](#_Toc66871863)_

_[A-20.1.2 Gateway Configuration 216](#_Toc66871864)_

_[A-20.1.3 Gateway Methods 217](#_Toc66871865)_

[A-20.2 Hosted Payment Page Library 221](#_Toc66871866)

_[A-20.2.1 Hosted Payment Pages 221](#_Toc66871867)_

_[**A-20.2.2**  **Library Namespace** 221](#_Toc66871868)_

_[A-20.2.3 Form Construction 222](#_Toc66871869)_

_[**A-20.2.4**  **Form Methods** 223](#_Toc66871870)_

_[**A-20.2.5**  **jQuery Plugin** 224](#_Toc66871871)_

[A-20.3 Hosted Payment Fields Library 225](#_Toc66871872)

_[A-20.3.1 Hosted Payment Fields 225](#_Toc66871873)_

_[**A-20.3.2**  **Library Namespace** 226](#_Toc66871874)_

_[**A-20.3.3**  **Form Construction** 227](#_Toc66871875)_

_[**A-20.3.4**  **Form Methods** 230](#_Toc66871876)_

_[**A-20.3.5**  **Form Events** 233](#_Toc66871877)_

_[**A-20.3.6**  **Field Construction** 234](#_Toc66871878)_

_[**A-20.3.7**  **Field Methods** 238](#_Toc66871879)_

_[A-20.3.8 Field Events 242](#_Toc66871880)_

_[A-20.3.9 Field CSS Classes 244](#_Toc66871881)_

_[A-20.3.10 Field Styling 245](#_Toc66871882)_

_[**A-20.3.11**  **jQuery Plugin** 248](#_Toc66871883)_

**[A-21](#_Toc66871884)****Example HTTP Requests 249**

[A-21.1 Hosted Integration 249](#_Toc66871885)

_[A-21.1.1 Transaction Request HTTP Headers 249](#_Toc66871886)_

_[A-21.1.2 Transaction Response HTTP Headers 249](#_Toc66871887)_

_[A-21.1.3 Submission Example 250](#_Toc66871888)_

[A-21.2 Direct Integration 251](#_Toc66871889)

_[A-21.2.1 Transaction Request HTTP Headers 251](#_Toc66871890)_

_[A-21.2.2 Transaction Response HTTP Headers 251](#_Toc66871891)_

_[A-21.2.3 Submission Example 252](#_Toc66871892)_

[A-21.3 Batch Integration 253](#_Toc66871893)

_[A-21.3.1 Submission Request HTTP Headers 253](#_Toc66871894)_

_[A-21.3.2 Submission Response HTTP Headers 254](#_Toc66871895)_

_[A-21.3.3 Status Request HTTP Headers 255](#_Toc66871896)_

_[A-21.3.4 Status Response HTTP Headers 255](#_Toc66871897)_

_[A-21.3.5 Submission Example 255](#_Toc66871898)_

**[A-22](#_Toc66871899)****Example Integration Code 257**

[A-22.1 Hosted Integration 257](#_Toc66871900)

_[A-22.1.1 Sale Transaction 257](#_Toc66871901)_

[A-22.2 Direct Integration 259](#_Toc66871902)

_[A-22.2.1 Sale Transaction (with 3-D Secure) 259](#_Toc66871903)_

_[A-22.2.2 Sale Transaction (without 3-D Secure) 261](#_Toc66871904)_

[A-22.3 Batch Integration 263](#_Toc66871905)

_[A-22.3.1 Batch Submission 263](#_Toc66871906)_

**[A-23](#_Toc66871907)****Example Library Code 266**

[A-23.1 Gateway Integration Library 266](#_Toc66871908)

_[A-23.1.1 Hosted Sale Transaction 266](#_Toc66871909)_

_[A-23.1.2 Direct Sale Transaction (with 3-D Secure) 267](#_Toc66871910)_

[A-23.2 Hosted Payment Page Library 269](#_Toc66871911)

_[A-23.2.1 Hosted Sale Transaction 269](#_Toc66871912)_

_[A-23.2.2 Hosted Sale Transaction (jQuery) 270](#_Toc66871913)_

_[A-23.2.3 Hosted Sale Transaction #2 271](#_Toc66871914)_

_[A-23.2.4 Hosted Sale Transaction #2 (jQuery) 272](#_Toc66871915)_

[A-23.3 Hosted Payment Fields Library 273](#_Toc66871916)

**[A-24](#_Toc66871917)****Frequently Asked Questions 281**

**[Index 282](#_Toc66871918)**

[0](#sdfootnote1anc) Transliteration involves the changing of character case, stripping of accents from characters and removal of unsupported characters so that the values meet the requirements of the third-party.

[0](#sdfootnote2anc) The additional details are currently only required by Visa and Mastercard however we recommend sending for all card types in order to be prepared for when other card Schemes follow suite.

[0](#sdfootnote3anc) PayPal refer to this field as MAXAMT.

[0](#sdfootnote4anc)1 The response will include Customer/billing address and delivery address details if provided by the PayPal Checkout.

[0](#sdfootnote5anc) Only available if the leaving of notes was enabled in the initial request using **checkoutOptions.allowNote** option.

[0](#sdfootnote6anc) Permission is needed from PayPal to support this field.

[0](#sdfootnote7anc) These fields are used when no permission to use billingName.

[0](#sdfootnote8anc) This field is passed directly to PayPal and therefore the field name and value must be spelt &#39;ize&#39; and not &#39;ise&#39;.

[0](#sdfootnote9anc) **pendingReason** is returned in the response only if **paymentStatus** is **Pending**.

[0](#sdfootnote10anc) This value is received directly from PayPal and so will use the &#39;ize&#39; and not &#39;ise&#39; spelling.

[0](#sdfootnote11anc) The response will include Customer/billing address and delivery address details if provided by the Amazon Pay Checkout.

[0](#sdfootnote12anc) 3D Secure fields are only cloned if both the existing and new transaction support 3-D Secure.

[0](#sdfootnote13anc) Payment facilitator fields are only cloned if the existing transaction uses the same **merchantID** as the new transaction.

[0](#sdfootnote14anc) MIT type **incremental** is not currently supported but reserved for future use.

[0](#sdfootnote15anc) For flagging of subsequent use the existing credentials will usually need to have been stored with the same Acquirer.

[0](#sdfootnote16anc) Not all Acquirers support all transaction types.

[0](#sdfootnote17anc) The Gateway does not currently support incremental authorisations.

[0](#sdfootnote18anc) Please use the correct hostname as provided in section 1.6.

[0](#sdfootnote19anc) Please use the correct hostname as provided in section 1.6.

[1](#sdendnote1anc) A password is not recommended if using the Hosted Integration, use a signature instead.

[2](#sdendnote2anc) A signature is recommended if using the Hosted Integration.

[3](#sdendnote3anc) Optional if an **xref** is provided as the value will be taken from the cross-referenced transaction.

[4](#sdendnote4anc) Optional if using the Hosted Integration, any value provided will be used to initialise any HPP input field.

[5](#sdendnote5anc) Mandatory for a REFUND\_SALE request to specify the original SALE transaction.

[6](#sdendnote6anc) Mandatory for Hosted Integration. Not supported by the Batch Integration.

[7](#sdendnote7anc) Not supported by the Hosted Integration, which will automatically use the Customer&#39;s IP address.

[8](#sdendnote8anc) A password is not recommended if using the Hosted Integration, use a signature instead.

[9](#sdendnote9anc) A signature is mandatory if using the Hosted Integration.

[10](#sdendnote10anc) An amount is only required for partial refunds or partial captures.

[11](#sdendnote11anc) This should only be used by Merchants who are storing Card numbers as per PCI DSS requirements.

[12](#sdendnote12anc) This should only be used for test purposed as Merchants are not allowed to store Card CVV numbers.

[13](#sdendnote13anc) Mandatory if AVS address checking is required.

[14](#sdendnote14anc) Mandatory if AVS postcode checking is required.

[15](#sdendnote15anc) Mandatory if CV2 checking is required.

[16](#sdendnote16anc) Overrides any Merchant Account setting configured via the Merchant Management System (MMS).

[17](#sdendnote17anc) Overrides any Merchant Account setting configured via the Merchant Management System (MMS).

[18](#sdendnote18anc) Note: It is only necessary to send the **threeDSRef** and the **threeDSResponse** in the continuation request, because the **threeDSRef** will identify the Merchant Account and initial request. The message does not need to be signed. However, you can send any of the normal request fields to modify or supplement the initial request. Any card details and transaction amount sent in the second request must match those used in the first request, else the second request will fail with a **responseCode** of **64442 (REQUEST MISMATCH)**.

[19](#sdendnote19anc) Overrides any Merchant Account setting configured via the Merchant Management System (MMS).

[20](#sdendnote20anc) SESS, the unique session id, is automatically sent from the Kount Device Collector loaded in the Hosted Payment Page.

[21](#sdendnote21anc) Which additional fields are mandatory will depend on your Acquirer.

[22](#sdendnote22anc) Only required if the Merchants Category Code is not configured on their gateway account.

[23](#sdendnote23anc) Overrides any Merchant Account setting configured via the Merchant Management System (MMS).

[24](#sdendnote24anc) Overrides any Merchant Account setting configured via the Merchant Management System (MMS).

[25](#sdendnote25anc) For use with variable schedules only.

[26](#sdendnote26anc) For use with fixed schedules only.

[27](#sdendnote27anc) Amex/Diners require either tax or discount, not both.

[28](#sdendnote28anc) XX is a number between 1 and 99.

[29](#sdendnote29anc) Mandatory if AVS checking required.

[30](#sdendnote30anc) Optional for Hosted Integration.

[31](#sdendnote31anc) Not required for Hosted Integration.

[32](#sdendnote32anc) The **masterPassStatus** , **masterPassToken** and **MasterPassVerifier** should be initialised with values received by your website when the wallet redirects to your **masterPassCallbackURL** URL. If the checkout was cancelled, then only the **masterPassStatus** field need be sent to the Gateway.

[33](#sdendnote33anc) The response will include Customer/billing address and delivery address details if provided by the Masterpass Wallet.

[34](#sdendnote34anc) Optional for Hosted Integration.

[35](#sdendnote35anc) Not required for Hosted Integration.

[36](#sdendnote36anc) Direct Integration Only

[37](#sdendnote37anc) Hosted Integration Only

[38](#sdendnote38anc) It is only necessary to send the **checkoutRef** and the **checkoutResponse** in the continuation request because the **checkoutRef** will identify the Merchant Account and initial request. The message does not need to be signed. You can send any of the normal request fields to modify or supplement the initial request – however, in this case the request should be signed. The **checkoutRedirectURL** and **checkoutOptions** fields sent in the initial request cannot be modified and any sent in the second request must match those used in the first request, or the second request will fail with a **responseCode** of **64442** ( **REQUEST**** MISMATCH**).

[39](#sdendnote39anc)The BN code is the unique button source code provided by PayPal to its partners and added by its partners to the PayPal buttons used by merchants to offer the PayPal Services that are enabled through Partner Product. The button source code provides a means of identifying and tracking referred merchants&#39; payments.

[40](#sdendnote40anc) This value is received directly from PayPal and so will use the &#39;ize&#39; and not &#39;ise&#39; spelling.

[41](#sdendnote41anc) Optional for Hosted Integration

[42](#sdendnote42anc) Not required for Hosted Integration.

[43](#sdendnote43anc) Direct Integration Only

[44](#sdendnote44anc) Hosted Integration Only

[45](#sdendnote45anc) It is only necessary to send the **checkoutRef** and the **checkoutResponse** in the continuation request because the **checkoutRef** will identify the Merchant Account and initial request. The message does not have to be signed. You can send any of the normal request fields to modify or supplement the initial request – however, in this case the request should be signed. The **checkoutRedirectURL** and **checkoutOptions** fields sent in the initial request cannot be modified and any sent in the second request must match those used in the first request, or the second request will fail with a **responseCode** of **64442 (REQUEST MISMATCH)**.

[46](#sdendnote46anc) Optional in Hosted Integration.

[47](#sdendnote47anc) Not required for Hosted Integration.

[48](#sdendnote48anc) Direct Integration only.

[49](#sdendnote49anc)Whilst the Gateway does not see this field as mandatory, PPRO may have payment methods that require additional configuration using checkout options.

[50](#sdendnote50anc) Hosted Integration Only

[51](#sdendnote51anc)This information is supplied to PPRO by default using the following fields: customerAddress, customerPostcode, customerTown, customerEmail, customerPhone, customerMobile, receiverDateOfBirth, statementNarrative1.

The options should be passed as either a nested record or serialised record as described in section 1.5.8. The option names are case sensitive.

[52](#sdendnote52anc)Not all payment methods give an immediate payment status. This will require a further QUERY to the Gateway to see whether this value has changed to a status of &#39;tendered&#39;.

[53](#sdendnote53anc) If the value is not supplied, then the default account preferences will be used.

[54](#sdendnote54anc) The default value is **Y** if 3-D Secure is enabled on the Merchant Account, otherwise **N.**

[55](#sdendnote55anc) It is only necessary to send the threeDSMD and the threeDSPaRes in the continuation request as the threeDSMD will identify the Merchant Account and initial request. The message does not need to be signed. However, you can send any of the normal request fields to modify or supplement the initial request. Any card details and transaction amount sent in the second request must match those used in the first request, or the second request will fail with a responseCode of **64442 (REQUEST MISMATCH)**.

[56](#sdendnote56anc) Event names are prefixed with the &#39;hostedform:&#39; namespace not shown in the table.

[57](#sdendnote57anc) Event names are prefixed with the &#39;hostedfield:&#39; namespace not shown in the table.

20