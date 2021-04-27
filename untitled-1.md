# 1.3 - 1.7.8

## Integration Methods

There are three methods of integration provided to process your transactions through the Gateway, allowing for different levels of control and communication from your website.

### Hosted Integration

The Hosted Integration method makes it easy to add secure payment processing to your ecommerce business, using our Hosted Payment Pages \(HPP\). You can use this method if you do not want to collect and store Cardholder data.

The Hosted Integration method works by redirecting the Customer to our Gateway’s Hosted Payment Page, which will collect the Customer’s payment details and process the payment before redirecting the Customer back to a page on your website, letting you know the payment outcome. This allows you the quickest path to integrating with the Gateway.

The standard Hosted Payment Page is designed to be shown in a lightbox over your website and styled with logos and colours to match. Alternatively, you can arrange for fully customised Hosted Payment Pages to be produced that can match your website’s style and layout. These fully customised pages are usually provided using a browser redirect, displaying full-page in the browser, or can be displayed embedded in an iframe on your website.

For greater control over the customisation of the payment page, our Gateway offers the use of Hosted Payment Fields, where only the individual input fields collecting the sensitive Cardholder data are hosted by the Gateway while the remainder of the payment form is provided by your website. These Hosted Payment Fields fit seamlessly into your payment page and can be styled to match your payment fields. When your payment form is submitted to your server, the Gateway will submit a payment token representing the sensitive card data it collected and your webserver can then use the Direct Integration to process the payment without ever being in contact with the collected Cardholder data. For more information please refer to our Hosted Payment Fields SDK Guide.

### Direct Integration

The Direct Integration works by allowing you to keep the Customer on your system throughout the checkout process, collecting the Customer’s payment details on your own secure server before sending the collected data to our Gateway for processing. This allows you to provide a smoother, more complete checkout process to the Customer.

In addition to basic sales processing, the Direct Integration can be used to perform other actions such as refunds and cancellations, which can provide a more advanced integration with our Gateway.

### Batch Integration

The Batch Integration is an enhancement to the Direct Integration, allowing you to send multiple transactions in a single request and monitor their status. This is useful if you wish to capture multiple transactions or collect multiple payments – for example, collecting subscription charges or loan repayments.

In addition to basic sales processing, the Batch Integration can be used to perform other actions, such as refunds and cancellations, which can provide a more advanced integration with our Gateway.

Unlike the Hosted and Direct Integrations, the Batch Integration does not process transactions sent to it immediately. Instead, the Gateway queues these transactions to be processed and returns a batch reference number which can be used to download a file that contains the current status of the transactions.

Batch Processing does not support transactions that require Customer interaction such as 3D Secure transactions, or alternative payment methods with interactive Wallet or Checkout pages.

## Integration Libraries

We can provide a range of libraries to help you to integrate with the Gateway.

These libraries include simple server-side classes in many popular programming languages, through to client-side scripts to help with the integration of the Hosted Payment Page or Hosted Payment Fields.

For more information about these libraries, please refer to appendix 23.7A-20.

## Security and Compliance

Each method requires a different level of server security and compliance with the Payment Card Industry Data Security Standard \(PCI DSS\).

If you use Hosted Payment Pages with the Hosted Integration or Hosted Payment Fields with the Direct or Batch Integrations, then your webserver does not need an SSL certificate and you require the lowest level of PCI DSS compliance.

If your website collects and/or stores sensitive Cardholder data, such as the card number \(PAN\) or card security code \(CVV/CV2\), then your webserver must have an SSL certificate and serve all payment forms using HTTPS. You will also need a higher level of PCI DSS compliance and to complete a PCI validation form annually.

For more information, please see https://www.pcisecuritystandards.org/

## Integration Details

### HTTP Requests

A request can be sent to the Gateway by submitting a HTTP POST request to the integration URL provided.

The request should have a Content-Type: application/x-www-form-urlencoded HTTP header and the request should be name, value pairs URL encoded as per RFC 1738.

Example URL encoding:

merchantID=100001&action=SALE&type=1&amount=1001&currencyCode=826&countryCode=826&transactionUnique=55f6db1c81d95&orderRef=Test+purchase&customerPostCode=NN17+8YG&responseCode=0&responseMessage=AUTHCODE%3A350333&state=captured&xref=15091702MG47WN32MM88LPK&cardNumber=4929+4212+3460+0821&cardExpiryDate=1215

_**Please note that the field names are cAsE sEnSiTiVe**._

The response will use the same URL encoding and return the request fields in addition to any dedicated response field. If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

### Hosted HTTP Requests

When using the Hosted Integration, the request must be sent from the Customer’s web browser as the response will be a HTML Hosted Payment Page \(HPP\), used to collect the Customer’s details. The format of the request is designed so that it can be sent using a standard HTML form with the data in hidden form fields. The browser will then automatically encode the request correctly according to application/x-www-form-urlencoded format.

When the Hosted Payment Page has been completed and the payment processed, the Customer’s browser will be automatically redirected to the URL provided via the **redirectURL** field. The response will be returned to this page in application/x-www-form-urlencoded format, using a HTTP POST request.

If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

An example of a Hosted Integration request is provided in appendix A-21.1 and sample code is provided in appendix A-22.1.

### Direct HTTP Requests

When using the Direct Integration, the response will be received in the same URL encoded format, unless a **redirectURL** field is provided.

If a **redirectURL** field is provided, then the response will be a HTML page designed to redirect a browser to the URL provided, using a HTTP POST request containing the response. This allows you to collect the Cardholder’s payment details on your own server, using a HTML form which POSTs to the Direct Integration, which then effectively POSTs the results back to this URL your webserver, where you can display the transaction outcome.

If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

An example of a Direct Integration request is provided in appendix A-21.1 and sample code is provided in appendix A-22.1.

### Batch HTTP Requests

When using the Batch Integration, a single HTTP POST request can contain multiple individual requests using the multipart/mixed content type with a boundary string specified. Within that main HTTP request, each of the parts contains a nested Direct Integration HTTP request, separated by the boundary string.

Each part should begin with a Content-Type: application/x-www-form-urlencoded HTTP header and contain a single Direct Integration HTTP request, as documented in section 1.5.3.

You can optionally specify a Content-Id HTTP header to identify each part message uniquely; if not provided, the Gateway will assign a unique id to each part. The Content-Id HTTP header is returned in the response. The Gateway will not validate the uniqueness of any id provided. After the mandatory Content-type and the optional _Content-Id_ header, two carriage return/line feed pairs must follow \(i.e. _\r\n\r\n_\). Any deviation from this structure might lead to the part being rejected or incorrectly interpreted. The part request payload, formatted as a regular HTTP URL encoded request, must follow the two-line breaks directly.

To reduce the size of large batch requests, the Gateway supports compression using a Content-Encoding HTTP header with either a ‘gzip’ or ‘x-gzip’ value. This header can be provided in the main request or in the part request or both.

An Authorization HTTP header can be used in the request to provide the username and password of a Gateway Merchant Management System user account. If correct, the batch details will be recorded as having been submitted by that user; if invalid, then the request will fail and respond with a 401 \(Unauthorised\) HTTP status code.

The Gateway will respond in the same manner as the request with a multipart/mixed content type; each part is the response to one of the requests in the batched request. In addition, the response will contain a standard Location HTTP header, providing a URL from which further batch update responses can be downloaded; and a standard Content-Disposition header, allowing a browser to download the response to a file. If the request contained an Authorization HTTP header, then the response will contain an X-P3-Token HTTP header containing an authentication token that can be sent in future requests instead of the username and password. The authentication token has a limited life span, but each future request will return a new token and thus effectively rejuvenate the token’s life.

Like the parts in the request, each response part contains a HTTP response, including headers and body. Each response part is preceded by a Content-Type HTTP header and Content-ID HTTP header. In addition, an X-Transaction-ID HTTP header is added containing the requests transaction id together with an X-Transaction-Response HTTP header containing a textual description of the transaction processing status.

_The Gateway will not process the transactions immediately but will queue them up to process over time. The transactions may not be processed in the order provided, so should not have interdependencies. Transactions will only appear in the Merchant Management System when they have been processed. The status of queued transaction is only available by querying the status of the batch._

The current status of a batch can be queried at any time by issuing a HTTP GET request to the URL provided in the initial responses Location HTTP header.

An Authorization HTTP header must be provided in the status request, containing either the username and password of a Gateway Merchant Management System user account or an authentication token returned in the batch submission response’s X-P3-Token HTTP header. If a valid username and password or a valid token is provided, then the response will be an updated version of the initial submission response providing the current status of each transaction. The response will only contain transactions that the authenticated user has permission to view.

An example of a Batch Integration request is provided in appendix A-21.3 and sample code is provided in appendix A-22.3.

### Handling Errors

When the Gateway is uncontactable due to a communications error, or problem with the internet connection, you may receive a HTTP status code in the 500 to 599 range. In this situation, you may want to retry the transaction. If you do choose to retry a transaction, then we recommend that you perform a limited number of attempts with an increasing delay between each attempt.

If the Gateway is unavailable during a scheduled maintenance period, you will receive a HTTP status code of 503 ‘Service Temporarily Unavailable’. In this situation, you should retry the transaction after the scheduled maintenance period has expired. You will be notified of the times and durations of any such scheduled maintenance periods in advance, by email, and given a time when transactions can be reattempted.

If you are experiencing these errors, then we recommend you consider the following steps as appropriate for the integration method being used:

* Ensure the request is being sent to HTTPS and not HTTP. HTTP is not supported and is not redirected.
* Send transactions sequentially rather than concurrently.
* Configure your integration code with try/catch loops around individual transactions to determine whether they were successful or not and retry if required, based on the return code or HTTP status returned.
* Configure the integration so that if one transaction fails, the entire batch does not stop at that point – i.e. log the failure to be checked and then skip to the next transaction rather than stopping entirely.

### Redirect URL

The **redirectURL** request field is used to provide the URL of a webpage on your server.

When provided, the Gateway will respond with a HTML page designed to redirect the Customer’s browser to the URL provided, using a HTTP POST request containing the URL encoded response.

For the Hosted Integration, this will redirect the Customer from the Hosted Payment Page back to this URL on your website.

For the Direct Integration, this allows you to collect the Cardholder’s payment details on your own server using a HTML form that POSTs to the Direct Integration. which then effectively POSTs the results back to this URL on your webserver, where you can display the transaction outcome. This usage is not recommended as it makes it harder to sign the message.

The URL is mandatory for the Hosted Integration and optional for the Direct Integration. It is not supported by the Batch Integration.

The **redirectURL** must be a fully qualified URL, containing at least the scheme and host components.

### Callback URL

The **callbackURL** request field allows you optionally to request that the Gateway sends a copy of the response to an alternative URL. In this case, each response will then be POSTed to this URL in addition to the normal response. This allows you to specify a URL on a secure shopping cart or backend order processing system, which will then fulfil any order associated with the transaction.

The URL is optional for both the Hosted Integration and the Direct Integration. It is not supported by the Batch Integration.

The **callbackURL** must be a fully qualified URL, containing at least the scheme and host components.

### Field Formats

Most integration field values are either numerical or textual; and either free format or from a range of predetermined values. Some field values are records or arrays of records.

Unless otherwise stated, numerical values are whole integer values with no decimal points. Textual values should use the UTF-8 character set and will be automatically truncated if too long, unless stated otherwise in the field’s description. Textual values may be transliterated[\[1\]]() when sending to third parties such as Acquirers but the original value is stored by Gateway and displayed in the Merchant Management System.

Field values should use the following formats unless otherwise stated in the field’s description:

| **Field Type** | **Value Format** |
| :--- | :--- |
| **Monetary Amounts** | Either major currency units by providing a value that includes a single decimal point such as ’10.99’; or in minor currency units by providing a value that contains no decimal points such as ‘1099’. |
| **Timestamps** | Date in the format ‘YYYY-MM-DD HH:MM:SS’ |
| **Dates** | Date in the format ‘YYYY-MM-DD’ |
| **Country Codes** | Either the ISO-3166-1 2-letter, 3-letter or 3-digit code. |
| **Currency Codes** | Either the ISO-4217 3-letter or 3-digit code. |
| **Records** | Records can be provided using the _\[XX\]_ notation, where _XX_ is the record’s field name \(sub-field\). Records can be multi-dimensional or be sequentially indexed. For example: to send a value for the sub-field _Y_ in the integration field _X,_ use the field name _X\[Y\]_; however, to send a value for the sub-field _Y_ in the fourth record for integration field _X,_ then use the field name _X\[4\]\[Y\]_ etc. |
| **Serialised Records** | Records can be sent as a JSON, XML or URL serialised string. The first character of the serialised string determines its format: ‘\[‘ indicates JSON format; ‘&lt;’ indicates XML format; and anything else is assumed to be RFC 1738 URL encoded format. |

Note: Nested records are useful when posting sub-fields direct from a HTML FORM. However, unlike the main integration fields, a nested record’s sub-fields are not sorted when constructing the signature and are processed in the order received. Serialised records can overcome any problems caused by a nested record’s fields being received in a different order to that used when generating the signature.

## Authentication

All requests must specify which Merchant Account they are for, using the **merchantID** request field. In addition to this, the following security measures can be used:

### Password Authentication

You can configure a password for each Merchant Account, using the Merchant Management System \(MMS\). This password must then be sent in the **merchantPwd** field in each request. If an incorrect password is received by the Gateway, then the transaction will be aborted and an error response is returned.

Warning: Use of a password is discouraged in any integration where the transaction is posted from a form in the client browser as the password may appear in plain text in code.

### Message signing

You must configure a signing secret phrase for each Merchant Account using the Merchant Management System \(MMS\). Each request will need to be ‘signed’ by providing a **signature** field containing a hash generated from the combination of the serialised request and this signing secret phrase. On receipt, the Gateway will then re-generate the hash and compare it with the one sent. If the two hashes are different then the request received must not be the same as that sent and so the contents must have been tampered with and the transaction will be aborted and an error response is returned.

The Gateway will also return hash of the response message in the returned **signature** field, allowing you to create your own hash of the response \(minus the **signature** field\) and verify that the hashes match.

If message signing is enabled, then the data POSTed to any callback URL will also be signed.

See appendix A-13 for information on how to create the hash.

### Allowed IP addresses

You can configure a list of IP addresses using the Merchant Management System \(MMS\). Two different address lists can be configured, one for standard requests, such as sales; and one for advanced requests, such as refunds and cancellations. If a request is received from an address other than those configured, then it will be aborted and an error response is returned.

## Supported Actions

All requests must specify what action they require the Gateway to perform, using the **action** request field. The Direct and Batch Integrations support all actions; however, the Hosted Integration only supports the basic payment actions.

### SALE

This will create a new transaction and attempt to seek authorisation for a sale from the Acquirer. A successful authorisation will reserve the funds on the Cardholder’s account until the transaction is settled.

The **captureDelay** field can be used to state whether the transaction should be authorised only and settled at a later date. For more details on delayed capture, refer to appendix A-10.

### VERIFY

This will create a new transaction and attempt to verify that the card account exists with the Acquirer. The transaction will result in no transfer of funds and no hold on any funds on the Cardholder’s account. It cannot be captured and will not be settled. The transaction **amount** must always be zero.

This transaction type is the preferred method for validating that the card account exists and is in good standing; however, it cannot be used to validate that it has sufficient funds.

### PREAUTH

This will create a new transaction and attempt to seek authorisation for a sale from the Acquirer. If authorisation is approved, then it is immediately voided \(where possible\) so that no funds are reserved on the Cardholder’s account. The transaction will result in no transfer of funds. It cannot be captured and will not be settled.

This transaction type can be used to check whether funds are available and that the account is valid. However, due to the problem highlighted below, it is recommended that Merchants use the VERIFY action when supported by their Acquirer.

Warning: If the transaction is to be completed then a new authorisation must be sought using the SALE action. If the PREAUTH authorisation could not be successfully voided, then this will result in the funds’ being authorised twice effectively putting two holds on the amount on the Cardholder’s account and thus requiring twice the amount to be available in the Cardholder’s account. It is therefore recommended only to PREAUTH small amounts, such as £1.00 to check mainly account validity.

### REFUND\_SALE

This will create a new transaction and attempt to seek authorisation for a refund of a previous SALE from the Acquirer. The transaction will then be captured and settled if and when appropriate. It can only be performed on transactions that have been successfully settled. Up until that point, a CANCEL or partial CAPTURE can be refunded or partially refunded from the original SALE transaction. The previous SALE transaction should be specified using the **xref** field.

Partial refunds are allowed by specifying the **amount** to refund. Any amount must not be greater than the original received amount minus any already refunded amount. Multiple partial refunds may be made while there is still a portion of the originally received amount un-refunded.

The **captureDelay** field can be used to state whether the transaction should be authorised only and settled at a later date. For more details on delayed capture refer to appendix A-10.

_**This action is not supported by the Hosted Integration.**_

### REFUND

This will create a new transaction and attempt to seek authorisation for a refund from the Acquirer. The transaction will then be captured and settled if and when appropriate. This is an independent refund and need not be related to any previous SALE. The amount is therefore not limited by any original received amount.

The **captureDelay** field can be used to state whether the transaction should be authorised only and settled at a later date. For more details on delayed capture refer to appendix A-10.

_**This action is not supported by the Hosted Integration.**_

###  CAPTURE

This will capture an existing transaction, identified using the **xref** request field, making it available for settlement at the next available opportunity. It can only be performed on transactions that have been authorised but not yet captured. An **amount** to capture may be specified but must not exceed the original amount authorised.

The original transaction must have been submitted with a **captureDelay** value that prevented immediate capture and settlement leaving the transaction in an authorised but un-captured state. For more details on delayed capture refer to appendix A-10.

_**This action is not supported by the Hosted Integration.**_

### CANCEL

This will cancel an existing transaction, identified using the **xref** request field, preventing it from being settled. It can only be performed on transactions, which have been authorised but not yet settled, and it is not reversible. Depending on the Acquirer it may not reverse the authorisation and release any reserved funds on the Cardholder’s account. In such cases, authorisation will be left to expire as normal releasing the reserved funds. This may take up to 30 days from the date of authorisation.

_**This action is not supported by the Hosted Integration.**_

### QUERY

This will query an existing transaction, identified using the **xref** request field, returning the original response. This is a simple transaction lookup action.

_**This action is not supported by the Hosted Integration.**_

## Integration Libraries

We can provide a range of libraries to help you to integrate with the Gateway.

These libraries include simple server-side classes in many popular programming languages, through to client-side scripts to help with the integration of the Hosted Payment Page or Hosted Payment Fields.

For more information about these libraries, please refer to appendix 23.7A-20.

## Security and Compliance

Each method requires a different level of server security and compliance with the Payment Card Industry Data Security Standard \(PCI DSS\).

If you use Hosted Payment Pages with the Hosted Integration or Hosted Payment Fields with the Direct or Batch Integrations, then your webserver does not need an SSL certificate and you require the lowest level of PCI DSS compliance.

If your website collects and/or stores sensitive Cardholder data, such as the card number \(PAN\) or card security code \(CVV/CV2\), then your webserver must have an SSL certificate and serve all payment forms using HTTPS. You will also need a higher level of PCI DSS compliance and to complete a PCI validation form annually.

For more information, please see https://www.pcisecuritystandards.org/

