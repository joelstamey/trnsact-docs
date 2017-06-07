![Logo](../images/logo_default.png)  

### *Documentation for the trnsACT Framework*

## The Library Topography

**What are the .dlls that make up trnsACT?**

trnACT.dll is the core library. It has a number of namespaces, or domains, packed with helper classes methods. The highlights include,

* Administration
    * Accounts (aka, Tenants)
* Application
    * Startup, a custom implementation of System.Web.HttpApplication
    * Site Audit
    * Settings 
* Business
    * Generic business entities like address, company, contact
* Commerce
    * Currency Conversions driven by configuration files
* Communication
    * Content 
    * Messages
    * Email
* Data
    * Data Consumption with best practices built in
    * Data Connections created from configuration files for defined data sources:
        * Application (default: xml file)
        * Security (aka, Membership, default: SQL Server)
        * Business (default: SQL Server)
        * Communication (aka, Messages, default: SQL Server)
        * Content (default: xml file)
        * Role (default: xml file)
        * Menu (default: xml file)
        * Administration (aka, accounts, default: xml file)
        * Tracking (default: SQL Server)
* Security
    * Membership
    * The New LoginFactory
    * Custom FormsAuthentication Principal
* Web
    * Webform Page Base Classes
    * Customized Webform Controls with Display Filtering
    * Generic Handlers (Internal API)

There are additional libraries that use trnsACT as a dependency to implement website functionality. They include

1.	trnsPAGES, a library of helper methods for implementing Razor-syntax WebPages 2.0.
2.	trnsREPORT, a library for outputting reports in different formats, and	
3.	trnsEVALUATE, a library of helper methods that implement event-driven approval workflows.

Some implementations have included company-specific libraries like
1. trnsDATA, a light-weight business ORM, a repository that allows business objects to be accessed securely returning Linq-friendly IEnumerable lists. trnsDATA also implements the powerful Business Filtering that evaluates member profiles to secure data – regional managers only see regional activity and a retailer only sees data for a single retailer. Developers get the list of business models and trnsDATA automatically does the heavy lifting.

2. trnsLABELS, a convenience library of business labels that pulls from the content store. Instead of translating “promotion”, developers can use BusinessLabel.Promotion instead.

[Home](../README.md) \| [Documents](documents.md)