# Using Tickets

You can issue tickets that grant a specific user access to a specific target, bypassing authorization. This is especially useful for non-interactive sessions where 2FA flows aren't possible, e.g. when connecting an application to a database or an API through Warpgate.

## Creating a ticket

In the admin UI, create a ticket in the _Tickets_ section, selecting a user account and a target:

![](https://user-images.githubusercontent.com/161476/181935119-bd8b1356-ce47-4a1b-a705-e20f78fd3590.png){width="500"}

Once the ticket is created, you'll see the protocol-specific connection instructions. In this case, for an HTTP target, the user can pass the ticket through a query parameter or an `Authorization` header:

![](https://user-images.githubusercontent.com/161476/181935153-d10097a1-4a87-4760-bc3e-35803daa99a3.png){width="500"}
