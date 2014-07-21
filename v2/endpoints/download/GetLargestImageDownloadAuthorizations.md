GetLargestImageDownloadAuthorizations
-------------------------------------
The GetLargestImageDownloadAuthorizations call returns download 
authorizations for the largest available image size, for each applicable product 
offering owned by the customer.

###Product Offerings
Authorization to download images is controlled by the product offerings associated 
with a customer. Product offerings control two aspects of download:

* whether the customer can download the image
* what sizes of the image can be downloaded 

Each image authorization returned by this operation indicates the product offering 
that is authorizing download of the image, as well as the authorized download size. 
Multiple different product offering authorizations may be returned for the same 
image depending on the product offerings associated with the customer. In these 
cases, the client may give the customer the option of which product offering to 
authorize against.

###Image Sizes
The sizes available for download are governed by your product agreement.

###Endpoint
Use the following endpoint to access this operation:

	http://connect.gettyimages.com/v1/download/GetLargestImageDownloadAuthorizations

###Request
The GetLargestImageDownloadAuthorizations JSON request has this form:

	{
	  "RequestHeader": {
	    "Token": "",
	    "CoordinationId": ""
	  },
	  "GetLargestImageDownloadAuthorizationsRequestBody": {
	    "Images": [
	      {
	        "ImageId": ""
	      }
	    ]
	  }
	}

####RequestHeader Fields
The RequestHeader specifies metadata about the request..

| Field          | Type        | Use          | Description                                                                               |
|:---------------|:------------|:-------------|:------------------------------------------------------------------------------------------|
| Token          | String      | Required     | Specify the secure authentication token provided by [CreateSession][].                        | 
| CoordinationId | String      | Optional     | Specify a value to echo in the response to track requests and their associated responses. |

####GetLargestImageDownloadAuthorizationsRequestBody Fields
The GetLargestImageDownloadAuthorizationsRequestBody contains the request arguments.

| Field 				| Type 		| Use 		| Description 																		|
|:----------------------|:----------|:----------|:----------------------------------------------------------------------------------|
| Images 				| Collection| Required 	| Add an Image entry for each image for which download authorizations are requested.| 
| _Image_ _entry_ 		| Object 	| Optional 	| Contains image arguments. 														|
| _ImageSize_.ImageId 	| String 	| Required 	| Specifies the ID of an image for which download authorizations are requested. 	|


###Response
The GetLargestImageDownloadAuthorizations JSON response has this form:

	{
	  "ResponseHeader": {
	    "Status": "",
	    "StatusList": [
	      {
	        "Type": "",
	        "Code": "",
	        "Message": ""
	      }
	    ],
	    "CoordinationId": ""
	  },
	  "GetLargestImageDownloadAuthorizationsResult": {
	    "Images": [
	      {
	        "Authorizations": [
	          {
	            "DownloadIsFree": boolean,
	            "DownloadToken": "",
	            "ProductOfferingInstanceId": "",
	            "ProductOfferingType": "",
	            "SizeKey": ""
	          }
	        ],
	        "ImageId": ""
	      }
	    ]
	  }
	}


####ResponseHeader Fields
The ResponseHeader contains metadata about the operation execution and response.


| Field            | Type        | Description                                                                                                                   |
|:-----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------|
| Status           | String      | Indicates the overall operation processing status notification. Possible values are: <br>• Success <br>• Error <br>• Warning  | 
| StatusList       | Collection  | Contains a _Status_ entry for each detailed processing status notification.                                                   |
| Status _entry_   | Object      | Contains the details of a status notification                                                                                 |
| _Status_.Type    | String      | Indicates the type, or severity, of the status notification. Possible values are: <br>• Information <br>• Warning <br>• Error |
| _Status_.Code    | String      | Identifies the category of the status notification. See [StatusCodes][] for an explanations of the codes.     				 |
| _Status_.Message | String      | Provides a human readable explanation of the status.                                                                          |
| CoordinationId   | String      | Indicates the CoordinationId value provided in the triggering request.                                                        |

####GetLargestImageDownloadAuthorizationsResult Fields
The GetLargestImageDownloadAuthorizationsResult contains these fields.

| Field                 		 		| Type      | Description																							|
|:--------------------------------------|:----------|:------------------------------------------------------------------------------------------------------|
| Images                         		| Collection| Contains an Image entry for each requested image the customer is authorized to download.				|
| Image _entry_                  		| Object    | Contains authorization details for an image.										    				|
| Authorizations                 		| Collection| Contains an Authorization entry for each product offering that authorizes the download of the image.	|
| Authorization _entry_          		| Object 	| Contains authorization details specific to a product offering.										|
| _Authorization_.DownloadIsFree 		| Boolean  	| Indicates the customer is authorized to download the image without incurring a debit against the number of allowed downloads for the associated product offering.|
| _Authorization_.DownloadToken 		| String  	| Provides the token needed to authorize the creation of a download request against the associated product offering. The token expires after 24 hours. Used when calling [CreateDownloadRequest][].|
| _Authorization_.InstanceId 			| Collection| Identifies the product offering instance that authorizes the customer to download the image. Some products cannot have multiple instances, in which case this field has no value.|
| _Authorization_.ProductOfferingType 	| Collection| Identifies the category to which the product offering belongs.										|
| ImageId 								| String    | Identifies the image.																					|

###Workflow Example
1. Call [CreateSession][] with system and user credentials to create an authentication token.
2. Call [SearchForImages][] to find images.
3. Call GetLargestImageDownloadAuthorizations, providing ImageIds from search results, to retrieve download authorizations for the specified images


[StatusCodes]: ../../appendix/StatusCodes.md
[CreateCustomer]: ../account/CreateCustomer.md
[CreateSession]: ../session/CreateSession.md
[CreateApplicationSession]: ../session/CreateApplicationSession.md
[GetCountries]: ../data/GetCountries.md
[CreateLightboxItems]: ../lightbox/CreateLightboxItems.md
[DeleteLightboxItems]: ../lightbox/DeleteLightboxItems.md
[CreateLightbox]: ../lightbox/CreateLightbox.md
[DeleteLightbox]: ../lightbox/DeleteLightbox.md
[GetLightbox]: ../lightbox/GetLightbox.md
[GetLightboxHeaders]: ../lightbox/GetLightboxHeaders.md
[UpdateLightboxHeader]: ../lightbox/UpdateLightboxHeader.md
[CreateDownloadRequest]: ../download/CreateDownloadRequest.md
[GetImageDownloadAuthorizations]: ../download/GetImageDownloadAuthorizations.md
[GetLargestImageDownloadAuthorizations]: ../download/GetLargestImageDownloadAuthorizations.md
[GetEventDetails]: ../search/GetEventDetails.md
[GetImageDetails]: ../search/GetImageDetails.md
[SearchForImages]: ../search/SearchForImages.md
[SearchForVideos]: ../search/SearchForVideos.md

