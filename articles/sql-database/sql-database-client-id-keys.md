---
title: "Uygulama kimlik doğrulama - Azure SQL veritabanı için aaaGet değerleri | Microsoft Docs"
description: "SQL veritabanı koddan erişmek için bir hizmet sorumlusu oluşturun."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a><span data-ttu-id="5301b-103">Koddan uygulama tooaccess SQL veritabanı kimlik doğrulaması için gerekli hello değerlerini alma</span><span class="sxs-lookup"><span data-stu-id="5301b-103">Get hello required values for authenticating an application tooaccess SQL Database from code</span></span>
<span data-ttu-id="5301b-104">toocreate ve burada Azure kaynaklarınızı oluşturulmuş hello Azure Active Directory (AAD) etki alanında hello Abonelikteki uygulamanızı kaydetmeniz gerekir kodundan SQL veritabanını yönetme.</span><span class="sxs-lookup"><span data-stu-id="5301b-104">toocreate and manage SQL Database from code you must register your app in hello Azure Active Directory (AAD) domain  in hello subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a><span data-ttu-id="5301b-105">Bir hizmet asıl tooaccess kaynakları bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5301b-105">Create a service principal tooaccess resources from an application</span></span>
<span data-ttu-id="5301b-106">Toohave hello son gereksinim [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) yüklü ve çalışır.</span><span class="sxs-lookup"><span data-stu-id="5301b-106">You need toohave hello latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="5301b-107">Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="5301b-107">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="5301b-108">Merhaba aşağıdaki PowerShell betiğini hello Active Directory (AD) uygulama ve hello hizmet asıl tooauthenticate C# uygulamamıza ihtiyacımız olmadığını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5301b-108">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="5301b-109">Merhaba betik Merhaba önceki C# örnek değerleri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="5301b-109">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="5301b-110">Ayrıntılı bilgi için bkz: [kullanım Azure PowerShell toocreate bir hizmet sorumlusu tooaccess kaynakları](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5301b-110">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

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




## <a name="see-also"></a><span data-ttu-id="5301b-111">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="5301b-111">See also</span></span>
* [<span data-ttu-id="5301b-112">SQL veritabanı C# ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="5301b-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="5301b-113">Bağlantı tooSQL veritabanı tarafından kullanarak Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5301b-113">Connecting tooSQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

