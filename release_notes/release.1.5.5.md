![Logo](../img/logo_default.png)  

### *Documentation for the trnsACT Framework*

## trnsACT 1.5.5 Version Notes

### Support for Application Environment Variable

Environment variables are a common MSBuild (via Visual Studio) feature when building web applications that are published to different locations like testing, staging and production sites. Environment variables allow conditional code to be written based upon the type of environment so you might, for example, have a special message for the staging site that did not appear on production. And because this type of information is critical when publishing to the cash cow that is Azure, Microsoft has elevated the humble environment variable from a publish (build) feature to a project feature in Visual Studio project templates that target >= .NET 4.5.2. and in ASP.NET 5.0 where versioned libraries of the .NET framework are included as part of the web application. This will allow ASP.NET 5.0 applications to also be run outside of IIS (e.g., Linux, iOS), so environment variables are a critical way to let the ASP.NET 5.0 application know how to mount the framework.

But now, for ACB Memphis developers who code using Web Sites projects (and not Web Application projects) using environment variables is not possible. Web site projects allow the developer to edit in place and then XCOPY her changes to a file system location. But publishing the project --and optionally using environment variables while doing it-- is a feature of Web Application projects only. Using Web Sites is simple, direct and suited for Classic ASP development; it is also limiting. On the flip side, using Web Applications offers greater features but offers another set of headaches challenges. 

The 1.5.5 version of trnsACT allows us to use the benefits of Environment Variables in web site projects. The pattern is to add the environment variable as a special app settings that we can then leverage. Here’s how:
First, add the default Microsoft environment variable as an application setting in the web.config file. 
<add key="ASPNET_ENV" value="Development" />
Then, in trnsACT Web Controls select the Environment attribute to filter control content. 
When the "ASPNET_ENV" Setting in the web.config file is set to "Development":

<trnsACT:NetPanel Environments="Development" runat="server">
        This panel content is shown...
</trnsACT:NetPanel>
<trnsACT:NetPanel Environments="Development,Production" runat="server">
        And this panel content is shown...
</trnsACT:NetPanel>
<trnsACT:NetPanel runat="server">
        Also this content in a panel without an Environments attribute is shown...
</trnsACT:NetPanel>
<trnsACT:NetPanel Environments="all" runat="server">
        Plus content intended for all environments is shown...
</trnsACT:NetPanel>
<trnsACT:NetPanel Environments="Production" runat="server">
        But this content for a different environment is hidden.
</trnsACT:NetPanel>
The Environments attributed has been added to all of the trnsACT web controls that support conditional display attributes like NetLabel, NetLiteral, NetPlaceholder, MenuBar, MenuList, SuperMenu and others that implement the trnsACTControl Interface. 
Note: Application Environment Variables should not be confused with Desktop/Server Environment Variables that allow ASP.NET developers to get basic information about the server operating system. The Debug Information tool now lists the Server Environment Variables.

### Debug Properties

The trnsACT site contains a debug information page. This has been a long-cherished tool at ACB that allows the developer is see all the elements of a session. The trnsACT version also includes information about the forms authentication ticket, user cookies, account settings and even path constructions. This is my first stop when trying to troubleshoot an issue. 
The debug information page calls a trnsACT method that returns markup of tables of useful information. But what if you want to customize this? The trnsACT.Application.Debug class now supports a Properties list method that allows you to conveniently access (and manipulate of the output of) the debug items.
This code

    Dim debugInformation As New trnsACT.Application.Debug
    For Each item As trnsACT.Base.CollectionItem In debugInformation.Properties
        Response.Write(String.Format("{0} >> {1}: {2}", item.Group, item.Label, item.ValueString).AddWebBreak)
    Next
    debugInformation = Nothing

will produce this rendered HTML like this:

    Current User Settings >> Membership Setting: Primary Role: anonymous
    Current User Settings >> Membership Setting: Start Page: ~/Account/Register
    Current User Settings >> Membership Setting: Default User Theme: default
    Current User Settings >> Membership Setting: Unique User Id: 
    User Cookies >> Cookie culture: en
    User Cookies >> Cookie websitetheme: piscataway
    User Cookies >> Cookie xeroxmdf: accountreference=ZFrorsjUH9suXcazDuVw0w==
    User Cookies >> Cookie trnsact: 

But remember that you can also use linq to query the Properties list. In this example, I want to see only the items with the group name of “Current User Settings”:

    Dim debugInformation As New trnsACT.Application.Debug
    Dim items As IQueryable(Of trnsACT.Base.CollectionItem) = debugInformation.Properties.AsQueryable
    Dim membershipSettings = From item In items
                            Where item.Group = "Current User Settings"
                            Order By item.Label
    For Each item As trnsACT.Base.CollectionItem In membershipSettings
        Response.Write(String.Format("{0} >> {1}: {2}", item.Group,
                                    item.Label,
                                    item.ValueString).AddWebBreak)
    Next
    membershipSettings = Nothing
    items = Nothing
    debugInformation = Nothing

With output like this:

    Current User Settings >> Membership Setting: Account Database: data
    Current User Settings >> Membership Setting: Account Reference: 0000
    Current User Settings >> Membership Setting: Application Name: trnsact
    Current User Settings >> Membership Setting: Country Code: 840
    Current User Settings >> Membership Setting: Default User Theme: default


[Home](../README.md) | [Release Notes](releasenotes.md)