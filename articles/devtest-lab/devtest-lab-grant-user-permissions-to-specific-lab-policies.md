---
title: "aaaGrant kullanıcı izinleri toospecific Laboratuvar ilkeleri | Microsoft Docs"
description: "Nasıl toogrant kullanıcı izinleri toospecific Laboratuvar ilkeleri DevTest Labs her kullanıcının ihtiyaçlarına göre bilgi edinin"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Kullanıcı izinleri toospecific Laboratuvar ilkeleri
## <a name="overview"></a>Genel Bakış
Bu makalede gösterilmektedir nasıl toouse PowerShell toogrant kullanıcıların izinleri tooa belirli Laboratuvar ilkesi. Bu şekilde izinleri her kullanıcının gereksinimlerinize göre uygulanabilir. Örneğin, bir belirli kullanıcı hello özelliği toochange hello VM ilke ayarları toogrant isteyebilirsiniz, ancak değil hello ilkeleri maliyeti.

## <a name="policies-as-resources"></a>İlke kaynakları olarak
Hello anlatıldığı gibi [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md) makale, RBAC Azure kaynaklarının ayrıntılı erişim yönetimini sağlar. RBAC kullanarak, DevOps ekibiniz içinde görevleri kurabilmeleri ve tooperform işlerini gereken erişim toousers yalnızca hello miktarını verebilirsiniz.

DevTest Labs'de hello RBAC eylem sağlayan bir kaynak türü ilkedir **Microsoft.DevTestLab/labs/policySets/policies/**. Her Laboratuvar ilke hello İlkesi kaynak türü, bir kaynak değildir ve bir kapsam tooan RBAC rolü olarak atanabilir.

Örneğin, sipariş toogrant kullanıcıların okuma/yazma izni toohello içinde **izin VM boyutları** İlkesi, hello ile çalışır, özel bir rol oluşturmak **Microsoft.DevTestLab/labs/policySets/policies/** * Eylem ve ata hello uygun kullanıcıları toothis özel rol hello kapsamındaki **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn RBAC, özel rolleri hakkında daha fazla bilgi görmek hello [özel roller erişim denetimi](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>PowerShell kullanarak bir lab özel rol oluşturma
Başlatılan sipariş tooget içinde anlatılmıştır makale aşağıdaki tooread hello gerekir nasıl tooinstall ve hello Azure PowerShell cmdlet'leri yapılandırma: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Azure PowerShell cmdlet'lerini hello ayarladıktan sonra hello aşağıdaki görevleri gerçekleştirebilirsiniz:

* Bir kaynak sağlayıcısı için tüm hello operations/eylemler listesi
* Belirli bir rol eylemler listesi:
* Özel bir rol oluşturun

PowerShell Betiği aşağıdaki hello örnekleri gösterilmektedir tooperform bu görevler:

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>İzinleri tooa kullanıcı için özel roller kullanarak belirli bir ilke atama
Özel rollerinizi tanımladığınız sonra bunları toousers atayabilirsiniz. Sipariş tooassign özel rol tooa kullanıcı, ilk hello edinmelidir **objectID** bu kullanıcıyı temsil eden. Merhaba kullanın, toodo **Get-AzureRmADUser** cmdlet'i.

Aşağıdaki örneğine hello hello **objectID** Merhaba, *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 kullanıcıdır.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Merhaba olduktan sonra **objectID** hello kullanıcı ve özel rol adı için bu rolü toohello kullanıcı hello ile atayabilirsiniz **New-AzureRmRoleAssignment** cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

Merhaba önceki örnekte hello **AllowedVmSizesInLab** İlkesi kullanılır. Aşağıdaki ilkeler hello birini kullanabilirsiniz:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bir kez bazı sonraki adımları tooconsider İşte kullanıcı izinleri toospecific Laboratuvar ilkeleri, verilen:

* [Güvenli erişim tooa Laboratuvar](devtest-lab-add-devtest-user.md).
* [Laboratuvar ilkeleri belirleme](devtest-lab-set-lab-policy.md).
* [Laboratuvar şablonu oluşturma](devtest-lab-create-template.md).
* [VM'leriniz için özel yapılar oluşturma](devtest-lab-artifact-author.md).
* [Yapıları tooa Laboratuvar'yle bir VM'yi eklemek](devtest-lab-add-vm-with-artifacts.md).

