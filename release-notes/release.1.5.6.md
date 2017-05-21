![Logo](../images/logo_default.png)  

### *Documentation for the trnsACT Framework*

## trnsACT 1.5.6 Version Notes

### Accounts Collection

The trnsACT  Administration namespace now has an accounts collection that can be useful when iterating through all the accounts in accounts.config file.

    Dim accountsStore As New trnsACT.Administration.Accounts
    For Each account As trnsACT.Administration.Account In accountsStore
        Response.Write(account.Description.AddWebBreak)
    Next
    accountsStore = Nothing


### Roles Collection Sort

The trnsACT Roles Collection now includes a sort method that allows roles to be sorted by the account id value.

    Dim rolesStore As New trnsACT.Security.RolesCollection
    rolesStore.Sort()
    For Each role As trnsACT.Security.Role In rolesStore
        Response.Write(role.Description.AddWebBreak)
    Next
    rolesStore = Nothing

[Home](../README.md) \| [Release Notes](releasenotes.md)