# Connect Azure compute resources to Azure SQL with Managed Identity

## Objectives
1. To use [MSI token-based authentication][1] to replace connection string containing secret (e.g. username/password or key).
1. The benefit is that only those whitelisted Azure resources can access target SQL databases. There's no secret so no risk of leakage. This also eliminates the need to create, manage, and rotate secret.
1. Official documentation is not very comprehensive, thus I'm adding documentation here.

## Pros/ cons
1. Pros: 
    * No need to manage/rotate secret.
	* No risk of secret/certificate leakage.
	* No need to workaround AAD PPE stamp as in AAD authentication (for Microsoft first party applications).

1. Cons:
    * Still need to go in DB and add resources as users with SQL query (for Microsoft 1st party apps, it's tricky in confidential/military clouds). 
    * Cannot debug the connection process locally.
	* Need to handle long-connection token expiration (e.g. hours-long deamon jobs).
    * Need to add config switch to fall back to regular connection since it does not work in local environment.


## Steps
1. Enable managed identity for compute resources
    * Go to a resource
    * Select "Identity" menu item
	* Enable system assigned identity
    * Alternatively, this step can be replaced by [ARM template][2]
    * After this step, you can find the resource names under Azure Portal > Azure AD > Enterprise Apps
    * Note: Essentially every resource is represented by a service principal in AAD. You can find the service principal under Azure AD > Enterprise Applications. The service principal name is the name we use in the next step.
1. Whitelist identities in SQL databases and add read/write permission
    * Obtain admin permission for SQL (usually via JIT)
	* Login SQL database with AAD integrated authentication
	* Run [this query][3] for every Azure resource identity
        ```
        CREATE USER "test-app" FROM EXTERNAL PROVIDER
        ALTER ROLE db_datareader ADD MEMBER "test-app"
        ALTER ROLE db_datawriter ADD MEMBER "test-app"
        ```
1. Update code to open SQL connection by injecting access token
    * Import Microsoft.Azure.Services.AppAuthentication dependency (>1.0.0)
    * [Acquire token][4] based on [resource ID][5] and open SQL connection with token and connection string
    * Pass opened SQL connection to DbContext as a [constructor parameter][6]

[1]: https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview
[2]: https://docs.microsoft.com/en-us/azure/app-service/overview-managed-identity?context=azure%2Factive-directory%2Fmanaged-identities-azure-resources%2Fcontext%2Fmsi-context&tabs=dotnet#using-an-azure-resource-manager-template
[3]: https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-connect-msi#grant-permissions-to-managed-identity
[4]: https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-connect-msi#modify-aspnet-core
[5]: https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/services-support-managed-identities#azure-services-that-support-azure-ad-authentication
[6]: https://docs.microsoft.com/en-us/dotnet/api/system.data.entity.dbcontext.-ctor?view=entity-framework-6.2.0#System_Data_Entity_DbContext__ctor_System_Data_Common_DbConnection_System_Boolean_