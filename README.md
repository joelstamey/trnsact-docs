
![Logo](./img/logo_default.png)  

### *Documentation for the trnsACT Framework*

## What is trnsACT?

The trnsACT Framework targets .NET 4.0. It includes one large trnsACT library with multiple namespaces like data, security and communication. Last year additional libraries were introduced including

1.	trnsPAGES, a library of helper methods for implementing Razor-syntax WebPages 2.0.
2.	trnsREPORT, a library for outputting reports,	
3.	trnsEVALUATE, a library of helper methods that implement event-driven workflows tuned to ACB business processes. 

Also, a number of business libraries were created: 
1. trnsDATA, a light-weight business ORM, a repository that allows ACB objects to be accessed securely returning Linq-friendly IEnumerable lists. trnsDATA also implements the powerful Business Filtering that evaluates member profiles to secure data – regional managers only see regional activity and a retailer only sees data for a single retailer. Developers get the list of business models and trnsDATA automatically does the heavy lifting.

2. trnsLABELS, a convenience library of business labels that pulls from the content store. Instead of translating “promotion”, developers can use BusinessLabel.Promotion instead.


## Release Notes

See notes about the [recent versions of trnsACT](./release_notes/releasenotes.md).



