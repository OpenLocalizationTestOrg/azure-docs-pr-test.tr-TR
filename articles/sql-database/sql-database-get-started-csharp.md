---
title: "C#: Azure SQL Veritabanı'nı kullanmaya başlama | Microsoft Docs"
description: "SQL ve C# uygulamalarını geliştirmek için SQL veritabanı deneyin ve .NET için SQL Database kitaplığı hello kullanarak C# ile bir Azure SQL veritabanı oluşturma."
keywords: SQL, sql c# deneyin
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>C# toocreate bir SQL veritabanı hello SQL Database kitaplığı ile .NET için kullanın.

Nasıl toouse C# toocreate bir Azure SQL veritabanı ile Merhaba öğrenin [.NET için Microsoft Azure SQL Yönetimi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). Bu makalede nasıl toocreate tek bir veritabanı SQL ve C# ile açıklanır. bkz: toocreate esnek havuzlarını [bir esnek havuz oluşturma](sql-database-elastic-pool-manage-csharp.md).

Merhaba .NET için Azure SQL veritabanı yönetimi kitaplığı sağlayan bir [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-hello sarmalar API tabanlı [Resource Manager tabanlı SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Merhaba kullanılırken SQL veritabanı'nın birçok yeni özellik yalnızca desteklenen [Azure Resource Manager dağıtım modeli](../azure-resource-manager/resource-group-overview.md), hello son her zaman kullanmalısınız **.NET için Azure SQL veritabanı yönetimi kitaplığı ([belgeleri](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Merhaba eski [tabanlı kitaplıkları Klasik dağıtım modeli](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) hello yeni Resource Manager temelli kitaplıkları kullanmanızı öneririz, böylece yalnızca geriye dönük uyumluluk için desteklenir.
> 
> 

Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:

* Azure aboneliği. Yalnızca bir Azure aboneliğine ihtiyacınız varsa tıklatın **ücretsiz hesap** üstündeki hello bu sayfa ve toofinish bu makalenin geri dönün.
* Visual Studio. Visual Studio'nun Ücretsiz bir kopya hello bkz [Visual Studio indirmeleri](https://www.visualstudio.com/downloads/download-visual-studio-vs) sayfası.

> [!NOTE]
> Bu makalede, yeni ve boş bir SQL veritabanı oluşturulmuştur. Merhaba değiştirme *CreateOrUpdateDatabase(...)*  yöntemi örnek toocopy veritabanları aşağıdaki hello ölçeklendirme veritabanları, bir havuz, vb. bir veritabanı oluşturun.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Bir konsol uygulaması oluşturun ve hello gerekli kitaplıkları yükleme
1. Visual Studio’yu çalıştırın.
2. **Dosya** > **Yeni** > **Proje**’ye tıklayın.
3. Bir C# **Konsol Uygulaması** oluşturun ve şu şekilde adlandırın: *SqlDbConsoleApp*

SQL veritabanı ile C#, yük hello toocreate gerekli yönetim kitaplıklarını (hello kullanarak [Paket Yöneticisi konsolunda](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.
2. Tür `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello son [Microsoft Azure SQL Yönetimi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Tür `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Tür `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure ortak kimlik doğrulama Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Merhaba bu makaledeki örneklerde her bir API isteğinin ve bloğunun zaman uyumlu bir form üzerinde arka plandaki hizmet hello hello REST çağrısı tamamlanmasından kadar kullanın. Zaman uyumsuz yöntemler de kullanılabilir.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Bir SQL Veritabanı sunucusu, güvenlik duvarı kuralı ve SQL veritabanı oluşturma - C# örneği
Aşağıdaki örnek hello bir kaynak grubu, sunucu, güvenlik duvarı kuralı ve bir SQL veritabanı oluşturur. Bakın, [bir hizmet asıl tooaccess kaynakları oluşturmak](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` değişkenleri.

Hello Değiştir **Program.cs** hello aşağıdaki ve güncelleştirme hello `{variables}` , uygulama değerlerle (Merhaba içermez `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a>Bir hizmet asıl tooaccess kaynakları oluşturun
Merhaba aşağıdaki PowerShell betiğini hello Active Directory (AD) uygulama ve hello hizmet asıl tooauthenticate C# uygulamamıza ihtiyacımız olmadığını oluşturur. Merhaba betik Merhaba önceki C# örnek değerleri çıkarır. Ayrıntılı bilgi için bkz: [kullanım Azure PowerShell toocreate bir hizmet sorumlusu tooaccess kaynakları](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Sonraki adımlar
SQL Database'i ve C# ile bir veritabanını ayarlama göre hello makaleler için hazırsınız:

* [TooSQL veritabanı SQL Server Management Studio ile bağlanma ve örnek T-SQL sorgusu gerçekleştirin](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Ek Kaynaklar
* [SQL Veritabanı](https://azure.microsoft.com/documentation/services/sql-database/)
* [Veritabanı Sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
