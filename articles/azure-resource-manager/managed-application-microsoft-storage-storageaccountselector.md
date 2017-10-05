---
title: "Azure yönetilen uygulama StorageAccountSelector UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Storage.StorageAccountSelector kullanıcı Arabirimi öğesi açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="9b725-103">Microsoft.Storage.StorageAccountSelector UI öğesi</span><span class="sxs-lookup"><span data-stu-id="9b725-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="9b725-104">Yeni veya var olan depolama hesabını seçmek için bir denetim.</span><span class="sxs-lookup"><span data-stu-id="9b725-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="9b725-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9b725-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9b725-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="9b725-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="9b725-108">Şema</span><span class="sxs-lookup"><span data-stu-id="9b725-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="9b725-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="9b725-109">Remarks</span></span>
- <span data-ttu-id="9b725-110">Belirtilmişse, `defaultValue.name` benzersizlik için otomatik olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="9b725-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="9b725-111">Depolama hesabı adı benzersiz değilse, kullanıcının farklı bir ad belirtin veya mevcut bir depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="9b725-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="9b725-112">İçin varsayılan değer `defaultValue.type` olan **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="9b725-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="9b725-113">Belirtilen olmayan herhangi bir türü `constraints.allowedTypes` gizlenir ve belirtilen olmayan herhangi bir türü `constraints.excludedTypes` gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9b725-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="9b725-114">`constraints.allowedTypes`ve `constraints.excludedTypes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9b725-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="9b725-115">Varsa `options.hideExisting` olan **doğru**, kullanıcının mevcut bir depolama hesabını seçemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b725-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="9b725-116">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="9b725-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="9b725-117">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="9b725-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="9b725-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9b725-118">Next steps</span></span>
* <span data-ttu-id="9b725-119">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b725-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9b725-120">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b725-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9b725-121">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9b725-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
