![Logo](../img/logo_default.png)  

### *Documentation for the trnsACT Framework*

## trnsACT 1.5.4 Version Notes

### Account Website Name

I’ve wrestled with this issue for some time. As you know, the web.config file contains an appSetting called “title” but this was never meant to be the name displayed to users, although some developers used it so. The “title” setting was meant to be the internal label for the site and would help us disambiguate between dev/test/prod sites or between similar sites for a given client. Several years ago I created an explicit content phrase called “website_title” that I recommended as the title to be shown to users. But to make that work, the “website_title” phrase for the default account “0000” would have to be set with the specific client-specific name. Remember that the aim of the default content to be account-agnostic while overridden account-specific values would be added to the account node in the content store.

Not only did this break our conventions, it also made publishing websites complicated, requiring the use of a brittle third-party transform extension for Visual Studio, namely Slow Cheetah. To sidestep this issue I have added an account property to the account.config provider called websitename. 

### Business Labels

I have standardized a core set of 68 Business Labels. The definitions of these business labels can be set by the business team via a website Management tool. The idea is that changing the definition in is single place will change all the values throughout the site. But that only works when the developer remembers to use the business label instead of the hard coding the value.

In the past a developer could use the trnsACT Translate extension like this: 

Me.gvReport.Columns(1).HeaderText = "promotion".Translate

This this trnsACT build, I have added the standardized set of business labels as static methods, complete with Intellisense support that includes a short description. In this example, the developer can see the use case for the Promotion business label. 

 ![BusinessLabels](../img/businesslabels.png)

Business labels are part of the trnsACT.Communication namespace and I’ve them easier to use in my example by adding the namespace to my application scope via the web.config file namespaces node:

      <namespaces>
        <add namespace="trnsACT" />
        <add namespace="trnsACT.Controls" />
        <add namespace="trnsACT.CustomExtensions" />
        <add namespace="trnsACT.Communication" />       
        <add namespace="Website" />
      </namespaces>

### Recommendation: Pagescriptfooter
Here is a recommended pattern for masterpages on when using trnsACT.

*The problem:* 
With trnsACT it's easy to add a javascript to the head of the site.Master page. From the Page_Load event on a page inherited from the trnsACT.Controls.Page base class, just use the LoadClientScript method: 

                LoadClientScript("jquery.powertip.min.js")

Plus there optional parameters that allow you to filter the action by role, account(client id), theme and culture.

                LoadClientScript("jquery.powertip.min.js", "!developer,!administrator,!owner", "9998", "ClientTheme", "fr")

This is possible because the site.master masterpage includes a header section with a runat="server" tag and so, may be manipulated server-side. All good, useful stuff.

*The solution:*

But the best practices pattern calls for scripts to be added at end the page load, so how does that happen. Recent versions of sample applications that implement trnsACT include a new pageScriptFooter ContentPlaceHolder so that page-specific scripting can be added at the bottom of the page file. This placeholder is outside the runat="server" form tag so it's not meant for instances of asp or trnsACT controls, it's meant to be able to add instances to scripts that only that page needs. 

[Home](../README.md) \| [Release Notes](releasenotes.md)