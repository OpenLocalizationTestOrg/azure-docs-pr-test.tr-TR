---
title: "aaaHow tooUse rol tabanlı erişim denetimini Azure API Management | Microsoft Docs"
description: "Nasıl toouse yerleşik roller hello ve Azure API Management'te özel roller oluşturmanızı öğrenin"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Nasıl tooUse rol tabanlı erişim kontrol Azure API Management'te
Azure API Management Azure rol tabanlı erişim denetimi (RBAC) tooenable ayrıntılı erişim yönetimi API Management hizmet ve varlıkları (örn., API, ilkeleri) kullanır. Bu makalede, API Yönetimi'nde hello yerleşik ve özel roller genel bir bakış sağlar. Hello Azure portalına erişim yönetimi hakkında daha ayrıntılı bilgi isterseniz bkz [hello Azure portalına erişim yönetimi kullanmaya başlama](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Yerleşik roller
API Management şu anda 3 yerleşik roller sağlar ve hello yakın zaman içinde 2 diğer rolleri ekler. Bu rolleri abonelik, kaynak grubu ve tek tek API Management örneği dahil farklı kapsamların atanabilir. Hello kaynak grubu düzeyinde tooan kullanıcı Hello "Azure API Management hizmeti okuyucu" rolüne atanırsa, örneğin, sonra hello kullanıcı okuma erişimi tooall API Management örnekleri hello kaynak grubu içinde sahip olur. 

Merhaba aşağıdaki tabloda hello kısa açıklamaları yerleşik roller sağlar. Hello Azure Portal veya Azure dahil olmak üzere diğer araçları kullanarak bu roller atayabilirsiniz [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [komut satırı arabirimi](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), ve [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Hakkında ayrıntılar için bkz: tooassign yerleşik rolleri, [rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Rol          | Okuma erişimi<sup>[1]</sup> | Yazma erişimi<sup>[2]</sup> | Hizmet oluşturma, silme, ölçeklendirme, VPN ve özel etki alanı yapılandırması | Erişim toolegacy Publsiher portalı | Açıklama
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Azure API Management hizmeti katkıda bulunan | ✓ | ✓ | ✓ | ✓ | Süper kullanıcı. Tam CRUD erişim tooAPI Yönetim Hizmetleri ve varlıkları (örn., API'leri, ilkeleri) sahiptir. Erişim toohello eski yayımcı portalı vardır. |
| Azure API Management hizmeti okuyucusu | ✓ | | || Salt okunur erişim tooAPI Yönetim Hizmetleri ve varlıkları vardır. |
| Azure API Management hizmeti işleci | ✓ | | ✓ | | API Management services ancak olmayan varlıklar yönetebilirsiniz.|
| Azure API Management hizmeti Düzenleyicisi<sup>*</sup> | ✓ | ✓ | |  | API Management varlıklar ancak değil hizmetleri yönetebilirsiniz.|
| Azure API Management İçerik Yöneticisi<sup>*</sup> | ✓ | | | ✓ | Geliştirici Portalı yönetebilirsiniz. Salt okunur erişim tooservices ve varlıklar.|

<sup>[1] okuma erişimi tooAPI Yönetim Hizmetleri ve varlıkları (örn., API, ilkeleri)</sup>

<sup>[2] yazma erişimi tooAPI Yönetim Hizmetleri ve varlıkları aşağıdaki opeartions dışında: 1) örneği oluşturma, silme ve 2) VPN yapılandırması 3) özel etki alanı adı Kurulumu ölçeklendirme</sup>

<sup>\*Biz tüm yönetici UI hello varolan yayımcı portalı toohello Azure portal geçirdikten sonra hello Hizmet Düzenleyicisi rolü kullanılabilir. Merhaba içerik yöneticisi rolü kullanılabilecek tooonly hello yayımcı portalına bulunanad sonra İşlevler ilgili toomanaging hello Geliştirici Portalı içerir.</sup>  


## <a name="custom-roles"></a>Özel roller
Merhaba yerleşik roller hiçbiri belirli ihtiyaçlarınızı karşılamıyorsa, özel roller tooprovide daha ayrıntılı olarak oluşturulabilir erişim yönetimi API Management varlıklar için. Örneğin, salt okunur erişim tooan API Management hizmeti ancak yalnızca belirli tooone API, yazma erişimine sahip bir özel rolü oluşturabilirsiniz. toolearn özel rolleri hakkında daha fazla ayrıntı görmek [Azure rbac'de özel roller](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Özel bir rol oluşturduğunuzda, daha kolay toostart hello yerleşik roller birine sahip olur. Merhaba öznitelikleri tooadd hello Eylemler, NotActions veya AssignableScopes düzenleyin, sonra hello değişiklikleri yeni bir rolü olarak kaydedebilirsiniz. Merhaba aşağıdaki örnek hello "Azure API Yönetimi Hizmeti okuyucu" rolüyle başlar ve "Hesaplayıcı API'si Düzenleyicisi" adlı özel bir rol oluşturur. belirli API bu nedenle yalnızca olacak tooa erişim toothat API'si olduğunda yalnızca hello özel rol atanabilir. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Video genel izleyin

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar

* Azure rol tabanlı erişim denetimi hakkında daha fazla bilgi edinin
  * [Hello Azure portalına erişim yönetimi kullanmaya başlama](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Rol atamaları toomanage erişim tooyour Azure aboneliği kaynakları kullanın](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Azure RBAC özel rolleri](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
