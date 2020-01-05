# Objectives
1. To use [MSI authentication][1] to replace connection string containing secret (e.g. username/password or key).
1. The benefit is that only those whitelisted Azure resources can access target SQL databases. There's no secret so no risk of leakage. This also eliminates the need to create, manage, and rotate secret.

# Steps
1. Enable managed identity for compute resources
    * Go to a resource
    * Select "Identity" menu item
	* Enable system assigned identity
    * Alternatively, this step can be replaced by ARM template
    * After this step, you can find the resource names under Azure Portal > Azure AD > Enterprise Apps
1. Whitelist identities in SQL databases and add read/write permission
    * Obtain admin permission for SQL (usually via JIT)
	* Login SQL database with AAD integrated authentication
	* Run this query for every Azure resource identity
        ```
        CREATE USER "test-app" FROM EXTERNAL PROVIDER
        ALTER ROLE db_datareader ADD MEMBER "test-app"
        ALTER ROLE db_datawriter ADD MEMBER "test-app"
        ```
1. Update code to open SQL connection by injecting access token



[1]: https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview