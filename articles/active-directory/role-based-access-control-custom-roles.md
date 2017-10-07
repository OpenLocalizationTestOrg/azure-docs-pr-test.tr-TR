---
title: "Azure RBAC için özel roller aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toodefine Azure aboneliğinizde daha kesin kimlik yönetimi için Azure rol tabanlı erişim denetimi ile özel roller."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Azure rol tabanlı erişim denetimi için özel roller oluşturma
Merhaba yerleşik roller hiçbiri belirli erişim gereksinimlerinizi karşılıyorsa özel bir rol Azure rol tabanlı erişim denetimi (RBAC) oluşturun. Özel roller kullanılarak oluşturulabilir [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure komut satırı arabirimi](role-based-access-control-manage-access-azure-cli.md) (CLI) ve hello [REST API](role-based-access-control-manage-access-rest.md). Yalnızca yerleşik roller gibi özel roller toousers, grupları ve uygulamaları abonelik, kaynak grubu ve kaynak kapsamları atayabilirsiniz. Özel roller Azure AD kiracısı içinde depolanır ve abonelikler arasında paylaşılabilir.

Her bir kiracı too2000 özel rolleri oluşturabilirsiniz. 

Merhaba aşağıdaki örnek izleme ve sanal makineleri yeniden başlatmayı için özel bir rol gösterir:

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>Eylemler
Merhaba **Eylemler** özel bir rol özelliği belirtir hello Azure işlemleri toowhich hello rol erişim verir. Azure kaynak sağlayıcıları güvenliği sağlanabilir işlemlerini tanımlayan işlemi dizelerin koleksiyonudur. İşlemi dizeleri izleyin hello biçimi `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Joker karakterler içeren işlemi dizeleri (\*) hello işlemi dizeyi eşleştir tooall işlemleri erişim verin. Örneğin:

* `*/read`verir tooread işlemleri tüm Azure kaynak sağlayıcıları tüm kaynak türleri için erişim.
* `Microsoft.Compute/*`verir tooall işlemleri hello Microsoft.Compute kaynak sağlayıcısındaki tüm kaynak türleri için erişim.
* `Microsoft.Network/*/read`verir tooread işlemleri Azure hello Microsoft.Network kaynak Sağlayıcısı'nda tüm kaynak türleri için erişim.
* `Microsoft.Compute/virtualMachines/*`sanal makineler ve onun alt kaynak türleri tooall işlemleri verir erişin.
* `Microsoft.Web/sites/restart/Action`verir toorestart Web sitelerine erişim.

Kullanım `Get-AzureRmProviderOperation` (PowerShell'de) veya `azure provider operations show` (içinde Azure CLI) toolist işlemleri Azure kaynak sağlayıcıları. Bu komutlar tooverify işlemi dizisi geçerli olduğunu ve tooexpand joker işlemi dizeleri de kullanabilirsiniz.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell ekran görüntüsü - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Azure CLI ekran görüntüsü - azure sağlayıcısı işlemleri göster "Microsoft.Compute/virtualMachines/ \* /eylem" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Kullanım hello **NotActions** tooallow istediğiniz işlem hello kümesi daha kolay kısıtlı işlemleri hariç tutarak tanımlanmışsa özelliği. Merhaba özel bir rol tarafından verilen erişim hello çıkarılmasıyla hesaplanır **NotActions** hello işlemlerinden **Eylemler** işlemleri.

> [!NOTE]
> Bir kullanıcı bir işlemde dışlar bir rolü atanıp atanmadığını **NotActions**ve erişim veren ikinci bir rolü atanmış aynı işlemi, hello kullanıcı toohello izin tooperform bu işlemi. **NotActions** reddetme değil kural – belirli işlemleri dışarıda toobe gerektiğinde bir yöntemdir toocreate izin verilen işlem kümesi yalnızca olduğu.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Merhaba **AssignableScopes** hello özel rol özelliği içinde hangi hello özel rol atama için uygun hello kapsamları (abonelik, kaynak grupları veya kaynakları) belirtir. Merhaba özel rol ataması için kullanılabilir yalnızca hello Aboneliklerde yapabileceğiniz veya ve değil dağınıklığı kullanıcının gerektiren kaynak grupları hello kalanı hello abonelik veya kaynak grupları için karşılaşabilirsiniz.

Geçerli atanabilir kapsamların örnekleri şunlardır:

* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - hello rol ataması için iki Aboneliklerde kullanılabilmesini sağlar.
* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - kullanılabilir hale getirir hello rol ataması tek bir abonelik.
* "/ abonelikleri/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/ağ" - hello rol atamasını yalnızca hello ağ kaynak grubu için kullanılabilir hale getirir.

> [!NOTE]
> En az bir kullanmalısınız abonelik, kaynak grubu veya kaynak kimliği
>
>

## <a name="custom-roles-access-control"></a>Özel roller erişim denetimi
Merhaba **AssignableScopes** hello özel rolünün özelliği de denetimleri kimin görüntüleyin, değiştirin ve hello rolünü silin.

* Kimin özel bir rol oluşturabilir miyim?
    Sahiplerinin (ve kullanıcı erişim Yöneticileri) Abonelikleri, kaynak grupları ve kaynakları kullanmak için özel roller bu kapsamları oluşturabilirsiniz.
    Merhaba hello rol oluşturma kullanıcının ihtiyacı toobe mümkün tooperform `Microsoft.Authorization/roleDefinition/write` tüm hello işlemi **AssignableScopes** hello rolünün.
* Özel bir rol değiştirebilecekleri?
    Sahiplerinin (ve kullanıcı erişim Yöneticileri) Abonelikleri, kaynak grupları ve kaynakları bu kapsamları özel rollerinde değiştirebilirsiniz. Kullanıcıların gereksinim toobe mümkün tooperform hello `Microsoft.Authorization/roleDefinition/write` tüm hello işlemi **AssignableScopes** özel bir rol.
* Kimin özel roller görebilir?
    Azure RBAC yerleşik rolleri tüm rollerin atama için uygun olmayan görüntüleme izin verin. Merhaba gerçekleştirebilirsiniz kullanıcılar `Microsoft.Authorization/roleDefinition/read` bir kapsamda işlemi bu kapsamda atama için kullanılabilir olan hello RBAC rolü görüntüleyebilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.
* [Rol tabanlı erişim denetimi](role-based-access-control-configure.md): hello Azure portalında RBAC ile çalışmaya başlama.
* Toomanage nasıl erişim ile bilgi edinin:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
  * [REST API](role-based-access-control-manage-access-rest.md)
* [Yerleşik roller](role-based-access-built-in-roles.md): Get RBAC standart gelen hello rolleri hakkında ayrıntılar.
