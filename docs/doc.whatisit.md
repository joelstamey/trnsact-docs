![Logo](../img/logo_default.png)  

### *Documentation for the trnsACT Framework*

## Documents About trnsACT

### What is trnsACT?

trnsACT is opinionated, meaning that it offers a proscribed way of handling an application challenge. That single approach is tuned for the realities of SMB development and implements best practices that mitigate risk. 

For example, the trnsDATA data class (DAL) only connects to SQL Servers to run SQL Procedures, which largely side-steps the risk of SQL injection attacks, which can be exposed by inexperienced developers.

And there are hundreds of others. Business and membership data has separate data connections because that is a best practice for keeping membership data secure. Passwords are hashed (one-way) instead of encrypted (two-way). SQL server passwords for the defined data sources must be encrypted. The password for SMTP server must be encrypted, too.

trnsACT assumes that projects will move to complexity, and that full specifications are seldom known when a website is architected. For example, although a site may be English-only at first, content infrastructure automatically supports multi-language scenarios. So you never develop for English-only, instead you develop for a list of languages that only includes English -- to start.

Almost every major website implementation requires that additional roles be added. Business stakeholders routinely forget classes of users that will need access to the site. trnsACT assumes a role-based appoarch to authorization because that is the way that enterprise websites work.

trnsACT is opinated because it selects a particular set of technologies. For example, trnsACT uses a customized version of the ASP.NET Membership provider released in August, 2005. Solutions released since then, like Identity, have been tightly coupled with Entity Framework, which itself privileges code-first implemenations. But most enterprise website applications aren't greenfield projects. Most require connecting to existing domain resources in a database first approach. So EF is not ideally suited, and by extension, Identity, for most enterprise applications. More importantly, the Microsoft Identity solutions have yet to include the full range of the security functions needed for application websites, including basic things like password expiration, account expiration and lockout windows. The trnsACT implementation of ASP.NET Membership includes custom, more maintainable implementations of the Role and Profile providers, and updates to the latest, most robust version of Microsoft cryptography.

trnsACT assumes that your enterprise may not have the latest and greatest technology static. It doesn't require new versions of SQL Server, for example. 

Finally, trnsACT includes code that solves real-world business challenges that all SMBs face. That means that Microsoft has sometimes added .NET APIs that address issues that trnsACT already address. That means that later versions of the Microsoft .NET framework includes the competing alternatives to the approach taken by trnsACT. As a developer, you can choose the best alternative for your situation.

[Home](../README.md) \| [Documents](documents.md)