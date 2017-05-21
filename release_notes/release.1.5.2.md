![Logo](../img/logo_default.png)  

### *Documentation for the trnsACT Framework*

## trnsACT 1.5.2 Version Notes

### Better Bootstrap Integration

As you know I have been looking at the performance of the trnsACT sites that use bootstrap. I identified a bottleneck with the menu that I have been working to optimize. Although the menu accounts for a small surface area of a page, it accounts for most of the HTML generated. The menu also uses the translate method for each label and calls the FriendlyURL and ResolveURL methods for the links. That’s a lot happening under the hood.

trnsACT v1.5.1 added providers to streamline how the menu data is fetched. In my testing (and in yours) we achieved a substantial load time reduction. This week I have a new version of trnsACT that looks at the menu code. I will send you the new version tomorrow.

Currently, we  use the MenuFormat Property of the SuperMenuList set to “bootstrap” to render the bootstrap menu. The SuperMenu control is a full-featured and all of those features are evaluated (and then ignored) to create the bootstrap menu. It’s like using a Ferrari as a golf cart. The new trnsACT v1.5.2 includes the new controls NavBar and NavBarList that only create bootstrap menus. After I used these new controls for the XeroxMDF dev site, I realized an overall reduction of 27% in the page load times and for pages without fetches to the business data (the load time of business data remains constant) I saw load reductions of up to 83%. Your mileage may vary.

In the Xerox MDF instance, in the NavBar user control I replaced

    <trnsACT:SuperMenuList ID="smnuAccountNav" Menus="account" MenuFormat="Bootstrap" CssClass="nav navbar-nav navbar-right" runat="server" /> 

with

    <trnsACT:NavBar ID="smnuAccountNav" CssClass="nav navbar-nav navbar-right" runat="server" EnableViewState="false" ClientIDMode="Static">
    <trnsACT:NavbarList id="mnuAccount" menuId="account" runat="server"></trnsACT:NavbarList>
    </trnsACT:NavBar>

and

    <trnsACT:SuperMenuList 
        ID="smnuTasks" 
        Menus="home,divider-vertical,budgets,divider-vertical,approvals,divider-vertical,transactions,divider-vertical,funding,divider-vertical,reports,divider-vertical,resources,divider-vertical,externaljump,divider-vertical,administration,divider-vertical,themes,divider-vertical" 
        MenuFormat="Bootstrap" 
        CssClass="nav navbar-nav navbar-left" 
        runat="server" />
                                
was replaced by 

        <trnsACT:NavBar ID="smnuTasks" CssClass="nav navbar-nav navbar-left" runat="server" EnableViewState="false" ClientIDMode="Static">
            <trnsACT:NavbarList id="mnuHome" menuId="home" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuBudgets" menuId="budgets" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuApprovals" menuId="approvals" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuTransaction" menuId="transactions" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuFunding" menuId="funding" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuReports" menuId="reports" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuResources" menuId="resources" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuAdministration" menuId="administration" runat="server"></trnsACT:NavbarList>
            <trnsACT:NavbarList id="mnuThemes" menuId="themes" runat="server"></trnsACT:NavbarList>
        </trnsACT:NavBar>


For the XeroxMDF dev site, I am also testing using CDNs for bootstrap and jquery files.

In the head of the site.master file I have changed the external file links to

    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
    <link rel="Stylesheet" href="http://ajax.aspnetcdn.com/ajax/jquery.ui/1.11.4/themes/ui-lightness/jquery-ui.css" /><trnsACT:StyleSheet         
        ID="ssSite" 
        HideBootstrapStyleSheet="true" 
        ShowJQueryUIStyleSheet="false"
        HideBootstrapThemeStyleSheet="true" 
        HideGlobalStyleSheet="true" runat="server" />
    <script type="text/javascript" src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js"></script>   

and in the footer, I have changed the jscript links to 

    <script type="text/javascript" src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
    <script type="text/javascript" src="http://ajax.aspnetcdn.com/ajax/jquery.ui/1.11.4/jquery-ui.min.js"></script>
    <script type="text/javascript" src="http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js"></script>
    <script type="text/javascript" src="http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js"></script><trnsACT:JavascriptLinks    
        ID="ftrJSLinks" 
        ShowJQueryUIScriptLink="false" 
        HideBootstrapJavaScriptLink="true" 
        HideJQueryScriptLink="true" 
        ShowModernizrScriptLink="false" 
        ShowRespondScriptLink="false" 
        CustomJavaScriptLink="ie10-viewport-bug-workaround.js" 
        runat="server" />

Notice that the files come from                 bootstrapcdn that offers free bootstrap hosting for bootstrap/Twitter files and aspnetcdn which is Microsoft’s free CDN service.

[Home](../README.md) \| [Release Notes](releasenotes.md)