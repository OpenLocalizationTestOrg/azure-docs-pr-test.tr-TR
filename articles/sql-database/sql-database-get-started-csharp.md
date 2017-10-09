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
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a><span data-ttu-id="9bc23-104">C# toocreate bir SQL veritabanı hello SQL Database kitaplığı ile .NET için kullanın.</span><span class="sxs-lookup"><span data-stu-id="9bc23-104">Use C# toocreate a SQL database with hello SQL Database Library for .NET</span></span>

<span data-ttu-id="9bc23-105">Nasıl toouse C# toocreate bir Azure SQL veritabanı ile Merhaba öğrenin [.NET için Microsoft Azure SQL Yönetimi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="9bc23-105">Learn how toouse C# toocreate an Azure SQL database with hello [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="9bc23-106">Bu makalede nasıl toocreate tek bir veritabanı SQL ve C# ile açıklanır.</span><span class="sxs-lookup"><span data-stu-id="9bc23-106">This article describes how toocreate a single database with SQL and C#.</span></span> <span data-ttu-id="9bc23-107">bkz: toocreate esnek havuzlarını [bir esnek havuz oluşturma](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9bc23-107">toocreate elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="9bc23-108">Merhaba .NET için Azure SQL veritabanı yönetimi kitaplığı sağlayan bir [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-hello sarmalar API tabanlı [Resource Manager tabanlı SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/).</span><span class="sxs-lookup"><span data-stu-id="9bc23-108">hello Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps hello [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="9bc23-109">Merhaba kullanılırken SQL veritabanı'nın birçok yeni özellik yalnızca desteklenen [Azure Resource Manager dağıtım modeli](../azure-resource-manager/resource-group-overview.md), hello son her zaman kullanmalısınız **.NET için Azure SQL veritabanı yönetimi kitaplığı ([belgeleri](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span><span class="sxs-lookup"><span data-stu-id="9bc23-109">Many new features of SQL Database are only supported when you are using hello [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use hello latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="9bc23-110">Merhaba eski [tabanlı kitaplıkları Klasik dağıtım modeli](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) hello yeni Resource Manager temelli kitaplıkları kullanmanızı öneririz, böylece yalnızca geriye dönük uyumluluk için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9bc23-110">hello older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use hello newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="9bc23-111">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bc23-111">toocomplete hello steps in this article, you need hello following:</span></span>

* <span data-ttu-id="9bc23-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9bc23-112">An Azure subscription.</span></span> <span data-ttu-id="9bc23-113">Yalnızca bir Azure aboneliğine ihtiyacınız varsa tıklatın **ücretsiz hesap** üstündeki hello bu sayfa ve toofinish bu makalenin geri dönün.</span><span class="sxs-lookup"><span data-stu-id="9bc23-113">If you need an Azure subscription simply click **FREE ACCOUNT** at hello top of this page, and then come back toofinish this article.</span></span>
* <span data-ttu-id="9bc23-114">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bc23-114">Visual Studio.</span></span> <span data-ttu-id="9bc23-115">Visual Studio'nun Ücretsiz bir kopya hello bkz [Visual Studio indirmeleri](https://www.visualstudio.com/downloads/download-visual-studio-vs) sayfası.</span><span class="sxs-lookup"><span data-stu-id="9bc23-115">For a free copy of Visual Studio, see hello [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="9bc23-116">Bu makalede, yeni ve boş bir SQL veritabanı oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="9bc23-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="9bc23-117">Merhaba değiştirme *CreateOrUpdateDatabase(...)*  yöntemi örnek toocopy veritabanları aşağıdaki hello ölçeklendirme veritabanları, bir havuz, vb. bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bc23-117">Modify hello *CreateOrUpdateDatabase(...)* method in hello following sample toocopy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a><span data-ttu-id="9bc23-118">Bir konsol uygulaması oluşturun ve hello gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="9bc23-118">Create a console app and install hello required libraries</span></span>
1. <span data-ttu-id="9bc23-119">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9bc23-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="9bc23-120">**Dosya** > **Yeni** > **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bc23-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="9bc23-121">Bir C# **Konsol Uygulaması** oluşturun ve şu şekilde adlandırın: *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="9bc23-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="9bc23-122">SQL veritabanı ile C#, yük hello toocreate gerekli yönetim kitaplıklarını (hello kullanarak [Paket Yöneticisi konsolunda](http://docs.nuget.org/Consume/Package-Manager-Console)):</span><span class="sxs-lookup"><span data-stu-id="9bc23-122">toocreate a SQL database with C#, load hello required management libraries (using hello [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="9bc23-123">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bc23-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="9bc23-124">Tür `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello son [Microsoft Azure SQL Yönetimi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="9bc23-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="9bc23-125">Tür `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="9bc23-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="9bc23-126">Tür `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure ortak kimlik doğrulama Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span><span class="sxs-lookup"><span data-stu-id="9bc23-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="9bc23-127">Merhaba bu makaledeki örneklerde her bir API isteğinin ve bloğunun zaman uyumlu bir form üzerinde arka plandaki hizmet hello hello REST çağrısı tamamlanmasından kadar kullanın.</span><span class="sxs-lookup"><span data-stu-id="9bc23-127">hello examples in this article use a synchronous form of each API request and block until completion of hello REST call on hello underlying service.</span></span> <span data-ttu-id="9bc23-128">Zaman uyumsuz yöntemler de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9bc23-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="9bc23-129">Bir SQL Veritabanı sunucusu, güvenlik duvarı kuralı ve SQL veritabanı oluşturma - C# örneği</span><span class="sxs-lookup"><span data-stu-id="9bc23-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="9bc23-130">Aşağıdaki örnek hello bir kaynak grubu, sunucu, güvenlik duvarı kuralı ve bir SQL veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9bc23-130">hello following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="9bc23-131">Bakın, [bir hizmet asıl tooaccess kaynakları oluşturmak](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="9bc23-131">See, [Create a service principal tooaccess resources](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="9bc23-132">Hello Değiştir **Program.cs** hello aşağıdaki ve güncelleştirme hello `{variables}` , uygulama değerlerle (Merhaba içermez `{}`).</span><span class="sxs-lookup"><span data-stu-id="9bc23-132">Replace hello contents of **Program.cs** with hello following, and update hello `{variables}` with your app values (do not include hello `{}`).</span></span>

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





## <a name="create-a-service-principal-tooaccess-resources"></a><span data-ttu-id="9bc23-133">Bir hizmet asıl tooaccess kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="9bc23-133">Create a service principal tooaccess resources</span></span>
<span data-ttu-id="9bc23-134">Merhaba aşağıdaki PowerShell betiğini hello Active Directory (AD) uygulama ve hello hizmet asıl tooauthenticate C# uygulamamıza ihtiyacımız olmadığını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9bc23-134">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="9bc23-135">Merhaba betik Merhaba önceki C# örnek değerleri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="9bc23-135">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="9bc23-136">Ayrıntılı bilgi için bkz: [kullanım Azure PowerShell toocreate bir hizmet sorumlusu tooaccess kaynakları](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="9bc23-136">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="9bc23-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9bc23-137">Next steps</span></span>
<span data-ttu-id="9bc23-138">SQL Database'i ve C# ile bir veritabanını ayarlama göre hello makaleler için hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="9bc23-138">Now that you've tried SQL Database and set up a database with C#, you're ready for hello following articles:</span></span>

* [<span data-ttu-id="9bc23-139">TooSQL veritabanı SQL Server Management Studio ile bağlanma ve örnek T-SQL sorgusu gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="9bc23-139">Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="9bc23-140">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9bc23-140">Additional Resources</span></span>
* [<span data-ttu-id="9bc23-141">SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="9bc23-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="9bc23-142">Veritabanı Sınıfı</span><span class="sxs-lookup"><span data-stu-id="9bc23-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
