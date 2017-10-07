---
title: aaaUse PowerShell toocreate bir Azure AD uygulama tooaccess hello Azure Media Services API | Microsoft Docs
description: "Bilgi nasıl toouse PowerShell toocreate bir Azure Active Directory (Azure AD) uygulama ve Azure Media Services API tooaccess hello ayarlayın."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="740ec-103">PowerShell toocreate bir Azure AD uygulama toouse hello Azure Media Services API ile kullanma</span><span class="sxs-lookup"><span data-stu-id="740ec-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="740ec-104">Nasıl toouse bir PowerShell komut dosyası toocreate bir Azure Active Directory (Azure AD) uygulama ve hizmet asıl tooaccess Azure Media Services kaynakları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="740ec-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="740ec-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="740ec-105">Prerequisites</span></span>

- <span data-ttu-id="740ec-106">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="740ec-106">An Azure account.</span></span> <span data-ttu-id="740ec-107">Bir hesabınız yoksa, başlayan bir [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="740ec-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="740ec-108">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="740ec-108">A Media Services account.</span></span> <span data-ttu-id="740ec-109">Daha fazla bilgi için bkz: [hello Azure portalında bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="740ec-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="740ec-110">Azure PowerShell sürümü 0.8.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="740ec-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="740ec-111">Daha fazla bilgi için bkz: [nasıl toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="740ec-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="740ec-112">Azure Resource Manager cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="740ec-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="740ec-113">PowerShell kullanarak bir Azure AD uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="740ec-113">Create an Azure AD app by using PowerShell</span></span>  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

<span data-ttu-id="740ec-114">Daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="740ec-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="740ec-115">Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="740ec-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="740ec-116">Rol tabanlı erişim denetimini Azure PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="740ec-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="740ec-117">Nasıl toomanually yapılandırmak arka plan programı uygulamaları sertifikaları kullanarak</span><span class="sxs-lookup"><span data-stu-id="740ec-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="740ec-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="740ec-118">Next steps</span></span>

<span data-ttu-id="740ec-119">Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="740ec-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
