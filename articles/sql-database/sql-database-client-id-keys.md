---
title: "Uygulama kimlik doğrulama - Azure SQL veritabanı değerlerini alma | Microsoft Docs"
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
ms.openlocfilehash: ec6256e9c5bb0d9c8d15d0f673cea70b3915eb34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-required-values-for-authenticating-an-application-to-access-sql-database-from-code"></a><span data-ttu-id="9effa-103">Bir uygulama kodundan SQL veritabanına erişmek için kimlik doğrulaması için gereken değerleri alma</span><span class="sxs-lookup"><span data-stu-id="9effa-103">Get the required values for authenticating an application to access SQL Database from code</span></span>
<span data-ttu-id="9effa-104">Oluşturup koddan SQL veritabanını yönetmek için burada Azure kaynaklarınızı oluşturulan Azure Active Directory (AAD) etki alanında Abonelikteki uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9effa-104">To create and manage SQL Database from code you must register your app in the Azure Active Directory (AAD) domain  in the subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-to-access-resources-from-an-application"></a><span data-ttu-id="9effa-105">Bir hizmet asıl kaynaklarına erişmek için bir uygulama oluşturun</span><span class="sxs-lookup"><span data-stu-id="9effa-105">Create a service principal to access resources from an application</span></span>
<span data-ttu-id="9effa-106">En son gerek [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) yüklü ve çalışır.</span><span class="sxs-lookup"><span data-stu-id="9effa-106">You need to have the latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="9effa-107">Ayrıntılı bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="9effa-107">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="9effa-108">Aşağıdaki PowerShell betiği Active Directory (AD) uygulamasını ve C# uygulamamızda kimlik doğrulamak için gereken hizmet sorumlusunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9effa-108">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="9effa-109">Betik önceki C# örneği için gereken değerleri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="9effa-109">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="9effa-110">Ayrıntılı bilgi için bkz. [Kaynaklara erişmek üzere hizmet sorumlusu oluşturmak için Azure PowerShell kullanma](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="9effa-110">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a><span data-ttu-id="9effa-111">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9effa-111">See also</span></span>
* [<span data-ttu-id="9effa-112">SQL veritabanı C# ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="9effa-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="9effa-113">Azure Active Directory kimlik doğrulamasını kullanarak SQL veritabanına bağlanma</span><span class="sxs-lookup"><span data-stu-id="9effa-113">Connecting to SQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

