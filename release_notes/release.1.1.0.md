![Logo](../img/logo_default.png)  

### *Documentation for the trnsACT Framework*

## trnsACT 1.1.0 Version Notes

### Culture

The current culture will be set to the 2-charaction ISO abbreviation only. It’s “fr” and not “fr-CA.” If the site supports various country dialects of the same language, then separate accounts (by country) should be used.

### AutoLogon

Additional optional parameters have been added to the Membership.AutoLogon method to enable greater flexibility for autologon scenarios.

### Support for DisplayFilters in More trnsACT Controls

The trnsACT controls NetImage, NetPanel and NetLink now support filters based themes, cultures, accounts, browsers and roles. Previously, if for example you wanted to set a different url in a NetLink control based upon theme or culture or account, you would test for current value and apply the url attribute value programmatically. Now you can add separate controls that will be rendered based upon context.  

Some examples:

    <trnsACT:NetLink ID="NetLink1" Cultures="fr" NavigateUrl="http://www.microsoft.fr" runat="server" Text="French" />
    <trnsACT:NetLink ID="NetLink2" Cultures="en" runat="server" NavigateUrl="http://www.microsoft.com" Text="English" />
    <trnsACT:NetLink ID="NetLink3" Cultures="!fr,!es" runat="server" NavigateUrl="http://www.microsoft.com" Text="All But French and Spanish" />
    <trnsACT:NetLink ID="NetLink4" Cultures="es" runat="server" NavigateUrl="http://www.microsoft.es" Text="Spanish" />
    <trnsACT:NetLink ID="NetLink6" Cultures="all" runat="server" NavigateUrl="http://www.microsoft.com" Text="All" />

Or if filtering by theme, you might use:

    <trnsACT:NetLink ID="NetLink7" Themes="akron" runat="server" NavigateUrl="http://www.microsoft.es" Text="Akron" />
    <trnsACT:NetLink ID="NetLink8" Themes="buffalo" runat="server" NavigateUrl="http://www.microsoft.nl" Text="Buffalo" />
    <trnsACT:NetLink ID="NetLink9" Themes="!akron" runat="server" NavigateUrl="http://www.microsoft.com" Text="All But Akron" />

As a reminder, the versatile trnsACT:NetPanel control has an additional display date filter:

    <trnsACT:netpanel ID="pnlDisplayFilter" DateFrom="08/06/2014" DateTo="12/31/2014" runat="server">
                    Text and controls filtered by date.
    </trnsACT:netpanel>

### NetPanel Enhancement

The NetPanel control will automatically translate the value of the .Net Panel GroupingText attribute, which renders in HTML as a fieldset legend.

 ![EmailTemplate](../img/site_secure.png)

[Home](../README.md) \| [Release Notes](releasenotes.md)