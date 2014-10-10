# Errors

The Instagift API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is somehow invalid or missing required information
401 | Unauthorized -- Your authorization credentials are missing or incorrect for the resource you're trying to access
404 | Not Found -- The resource id you provided cannot be found
406 | Not Acceptable -- Your request isn't JSON
429 | Too Many Requests -- You've reached your rate limit
500 | Internal Server Error -- We had a problem with our server. Try again later.
