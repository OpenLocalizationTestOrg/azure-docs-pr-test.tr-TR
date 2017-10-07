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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>PowerShell toocreate bir Azure AD uygulama toouse hello Azure Media Services API ile kullanma

Nasıl toouse bir PowerShell komut dosyası toocreate bir Azure Active Directory (Azure AD) uygulama ve hizmet asıl tooaccess Azure Media Services kaynakları hakkında bilgi edinin.  

## <a name="prerequisites"></a>Ön koşullar

- Bir Azure hesabı. Bir hesabınız yoksa, başlayan bir [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/). 
- Bir Media Services hesabı. Daha fazla bilgi için bkz: [hello Azure portalında bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).
- Azure PowerShell sürümü 0.8.8 veya sonraki bir sürümü. Daha fazla bilgi için bkz: [nasıl toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Azure Resource Manager cmdlet'lerini.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>PowerShell kullanarak bir Azure AD uygulaması oluştur  

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

Daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Rol tabanlı erişim denetimini Azure PowerShell kullanarak yönetme](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Nasıl toomanually yapılandırmak arka plan programı uygulamaları sertifikaları kullanarak](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Sonraki adımlar

Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-portal-upload-files.md).
