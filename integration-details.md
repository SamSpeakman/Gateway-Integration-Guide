# Integration details

## 1.5.1 HTTP Requests

A request can be sent to the Gateway by submitting a HTTP POST request to the integration URL provided.

The request should have a Content-Type: application/x-www-form-urlencoded HTTP header and the request should be name, value pairs URL encoded as per RFC 1738.

Example URL encoding:

merchantID=100001&action=SALE&type=1&amount=1001¤cyCode=826&countryCode=826&transactionUnique=55f6db1c81d95&orderRef=Test+purchase&customerPostCode=NN17+8YG&responseCode=0&responseMessage=AUTHCODE%3A350333&state=captured&xref=15091702MG47WN32MM88LPK&cardNumber=4929+4212+3460+0821&c ardExpiryDate=1215

**Please note that the field names are cAsE sEnSiTiVe**

The response will use the same URL encoding and return the request fields in addition to any dedicated response field. If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

## 1.5.2 Hosted HTTP Requests

When using the Hosted Integration, the request must be sent from the Customer’s web browser as the response will be a HTML Hosted Payment Page \(HPP\), used to collect the Customer’s details. The format of the request is designed so that it can be sent using a standard HTML form with the data in hidden form fields. The browser will then automatically encode the request correctly according to application/x-www-form-urlencoded format.

When the Hosted Payment Page has been completed and the payment processed, the Customer’s browser will be automatically redirected to the URL provided via the redirectURL field. The response will be returned to this page in application/x-www-form-urlencoded format, using a HTTP POST request.

If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

An example of a Hosted Integration request is provided in appendix A-21.1 and sample code is provided in appendix A-22.1.

## 1.5.3 Direct HTTP Requests

When using the Direct Integration, the response will be received in the same URL encoded format, unless a redirectURL field is provided.

If a redirectURL field is provided, then the response will be a HTML page designed to redirect a browser to the URL provided, using a HTTP POST request containing the response. This allows you to collect the Cardholder’s payment details on your own server, using a HTML form which POSTs to the Direct Integration, which then effectively POSTs the results back to this URL your webserver, where you can display the transaction outcome.

If the request contains a field that is also intended as a response field, then any incoming request value will be overwritten by the correct response value.

An example of a Direct Integration request is provided in appendix A-21.1 and sample code is provided in appendix A-22.1.

## 1.5.4 Batch HTTP Requests

When using the Batch Integration, a single HTTP POST request can contain multiple individual requests using the _multipart/mixed_ content type with a boundary string specified. Within that main HTTP request, each of the parts contains a nested Direct Integration HTTP request, separated by the boundary string.

Each part should begin with a Content-Type: application/x-www-form-urlencoded HTTP header and contain a single Direct Integration HTTP request, as documented in section 1.5.3.

You can optionally specify a Content-Id HTTP header to identify each part message uniquely; if not provided, the Gateway will assign a unique id to each part. The Content-Id HTTP header is returned in the response. The Gateway will not validate the uniqueness of any id provided. After the mandatory Content-type and the optional Content-Id header, two carriage return/line feed pairs must follow \(i.e. \r\n\r\n\). Any deviation from this structure might lead to the part being rejected or incorrectly interpreted. The part request payload, formatted as a regular HTTP URL encoded request, must follow the two-line breaks directly.

To reduce the size of large batch requests, the Gateway supports compression using a ContentEncoding HTTP header with either a ‘gzip’ or ‘x-gzip’ value. This header can be provided in the main request or in the part request or both.

An Authorization HTTP header can be used in the request to provide the username and password of a Gateway Merchant Management System user account. If correct, the batch details will be recorded as having been submitted by that user; if invalid, then the request will fail and respond with a 401 \(Unauthorised\) HTTP status code.

The Gateway will respond in the same manner as the request with a multipart/mixed content type; each part is the response to one of the requests in the batched request. In addition, the response will contain a standard Location HTTP header, providing a URL from which further batch update responses can be downloaded; and a standard Content-Disposition header, allowing a browser to download the response to a file. If the request contained an Authorization HTTP header, then the response will contain an X-P3-Token HTTP header containing an authentication token that can be sent in future requests instead of the username and password. The authentication token has a limited life span, but each future request will return a new token and thus effectively rejuvenate the token’s life.

Like the parts in the request, each response part contains a HTTP response, including headers and body. Each response part is preceded by a Content-Type HTTP header and Content-ID HTTP header. In addition, an X-Transaction-ID HTTP header is added containing the requests transaction id together with an X-Transaction-Response HTTP header containing a textual description of the transaction processing status.

The Gateway will not process the transactions immediately but will queue them up to process over time. The transactions may not be processed in the order provided, so should not have interdependencies. Transactions will only appear in the Merchant Management System when they have been processed. The status of queued transaction is only available by querying the status of the batch.

The current status of a batch can be queried at any time by issuing a HTTP GET request to the URL provided in the initial responses Location HTTP header.

An Authorization HTTP header must be provided in the status request, containing either the username and password of a Gateway Merchant Management System user account or an authentication token returned in the batch submission response’s X-P3-Token HTTP header. If a valid username and password or a valid token is provided, then the response will be an updated version of the initial submission response providing the current status of each transaction. The response will only contain transactions that the authenticated user has permission to view.

An example of a Batch Integration request is provided in appendix A-21.3 and sample code is provided in appendix A-22.3.

## 1.5.6 Redirect URL

The redirectURL request field is used to provide the URL of a webpage on your server.

When provided, the Gateway will respond with a HTML page designed to redirect the Customer’s browser to the URL provided, using a HTTP POST request containing the URL encoded response.

For the Hosted Integration, this will redirect the Customer from the Hosted Payment Page back to this URL on your website.

For the Direct Integration, this allows you to collect the Cardholder’s payment details on your own server using a HTML form that POSTs to the Direct Integration. which then effectively POSTs the results back to this URL on your webserver, where you can display the transaction outcome. This usage is not recommended as it makes it harder to sign the message.

The URL is mandatory for the Hosted Integration and optional for the Direct Integration. It is not supported by the Batch Integration.

The redirectURL must be a fully qualified URL, containing at least the scheme and host components.

