# Security Aspects for a Web Application in Azure

1. Always configure the application configuration from the portal.azure.com. Ex: Sensitive <appSettings>

2. Move all the SQL Config connectionstrings to portal.azure.com

3. Move all the files to Azure Blob or Azure File Storage Service

4. Move all secret keys / passwords to Azure Key Vault.
