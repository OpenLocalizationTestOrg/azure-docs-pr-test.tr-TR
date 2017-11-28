---
title: "aaaAzure yönetilen uygulama MultiStorageAccountCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Storage.MultiStorageAccountCombo UI öğesi açıklar"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="641d5-103">Microsoft.Storage.MultiStorageAccountCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="641d5-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="641d5-104">Ortak bir önek ile başlayan adlarla, birden çok depolama hesabı oluşturmak için denetimleri grubudur.</span><span class="sxs-lookup"><span data-stu-id="641d5-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="641d5-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="641d5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="641d5-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="641d5-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="641d5-108">Şema</span><span class="sxs-lookup"><span data-stu-id="641d5-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="641d5-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="641d5-109">Remarks</span></span>
- <span data-ttu-id="641d5-110">Merhaba değeri `defaultValue.prefix` bir veya daha fazla tamsayılar toogenerate hello dizisi depolama hesabı adları ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="641d5-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="641d5-111">Örneğin, varsa `defaultValue.prefix` olan **foobar** ve `count` olan **2**, ardından depolama hesabı adları **foobar1** ve **foobar2** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="641d5-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="641d5-112">Oluşturulan depolama hesabı adları için benzersizlik otomatik olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="641d5-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="641d5-113">Merhaba depolama hesabı adları lexicographically temel alınarak oluşturulur `count`.</span><span class="sxs-lookup"><span data-stu-id="641d5-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="641d5-114">Örneğin, varsa `count` 10'dur ve ardından hello depolama hesabı adları ile 2 basamaklı tamsayılar bitiş (01, 02, 03, vs.).</span><span class="sxs-lookup"><span data-stu-id="641d5-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="641d5-115">Merhaba için varsayılan değer `defaultValue.prefix` olan **null**ve `defaultValue.type` olan **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="641d5-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="641d5-116">Belirtilen olmayan herhangi bir türü `constraints.allowedTypes` gizlenir ve belirtilen olmayan herhangi bir türü `constraints.excludedTypes` gösterilir.</span><span class="sxs-lookup"><span data-stu-id="641d5-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="641d5-117">`constraints.allowedTypes`ve `constraints.excludedTypes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="641d5-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="641d5-118">Toplama toogenerating depolama hesabı adları `count` kullanılan tooset hello öğesi için uygun çarpanı olan.</span><span class="sxs-lookup"><span data-stu-id="641d5-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="641d5-119">Statik bir değer gibi destekleyen **2**, veya gibi başka bir öğeden dinamik bir değer `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="641d5-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="641d5-120">Merhaba varsayılan değer **1**.</span><span class="sxs-lookup"><span data-stu-id="641d5-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="641d5-121">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="641d5-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="641d5-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="641d5-122">Next steps</span></span>
* <span data-ttu-id="641d5-123">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="641d5-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="641d5-124">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="641d5-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="641d5-125">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="641d5-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
