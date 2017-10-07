---
title: "aaaAzure yönetilen uygulama StorageAccountSelector UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Storage.StorageAccountSelector UI öğesi açıklar"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="38b41-103">Microsoft.Storage.StorageAccountSelector UI öğesi</span><span class="sxs-lookup"><span data-stu-id="38b41-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="38b41-104">Yeni veya var olan depolama hesabını seçmek için bir denetim.</span><span class="sxs-lookup"><span data-stu-id="38b41-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="38b41-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="38b41-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="38b41-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="38b41-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="38b41-108">Şema</span><span class="sxs-lookup"><span data-stu-id="38b41-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="38b41-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="38b41-109">Remarks</span></span>
- <span data-ttu-id="38b41-110">Belirtilmişse, `defaultValue.name` benzersizlik için otomatik olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="38b41-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="38b41-111">Merhaba depolama hesabı adı benzersiz değilse, hello kullanıcı farklı bir ad belirtin veya mevcut bir depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="38b41-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="38b41-112">Merhaba için varsayılan değer `defaultValue.type` olan **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="38b41-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="38b41-113">Belirtilen olmayan herhangi bir türü `constraints.allowedTypes` gizlenir ve belirtilen olmayan herhangi bir türü `constraints.excludedTypes` gösterilir.</span><span class="sxs-lookup"><span data-stu-id="38b41-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="38b41-114">`constraints.allowedTypes`ve `constraints.excludedTypes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="38b41-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="38b41-115">Varsa `options.hideExisting` olan **doğru**, hello kullanıcı, mevcut bir depolama hesabını seçilemez.</span><span class="sxs-lookup"><span data-stu-id="38b41-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="38b41-116">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="38b41-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="38b41-117">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="38b41-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="38b41-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38b41-118">Next steps</span></span>
* <span data-ttu-id="38b41-119">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38b41-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="38b41-120">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38b41-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="38b41-121">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="38b41-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
