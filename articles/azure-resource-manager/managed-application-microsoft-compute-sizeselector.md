---
title: "aaaAzure yönetilen uygulama SizeSelector UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Compute.SizeSelector UI öğesi açıklar"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="93bef-103">Microsoft.Compute.SizeSelector UI öğesi</span><span class="sxs-lookup"><span data-stu-id="93bef-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="93bef-104">Bir veya daha fazla sanal makine örnekleri için bir boyut seçmek için bir denetim.</span><span class="sxs-lookup"><span data-stu-id="93bef-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="93bef-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="93bef-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="93bef-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="93bef-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="93bef-108">Şema</span><span class="sxs-lookup"><span data-stu-id="93bef-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="93bef-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="93bef-109">Remarks</span></span>
- <span data-ttu-id="93bef-110">`recommendedSizes`en az bir boyut içermelidir.</span><span class="sxs-lookup"><span data-stu-id="93bef-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="93bef-111">Merhaba, ilk boyutu hello varsayılan olarak kullanılır önerilir.</span><span class="sxs-lookup"><span data-stu-id="93bef-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="93bef-112">Önerilen boyut hello seçili konumda kullanılabilir durumda değilse, hello boyutu otomatik olarak atlandı.</span><span class="sxs-lookup"><span data-stu-id="93bef-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="93bef-113">Bunun yerine, hello sonraki önerilen boyut kullanılır.</span><span class="sxs-lookup"><span data-stu-id="93bef-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="93bef-114">Hello belirtilmemiş herhangi bir boyutta `constraints.allowedSizes` gizlenir ve belirtilen olmayan herhangi bir boyutta `constraints.excludedSizes` gösterilir.</span><span class="sxs-lookup"><span data-stu-id="93bef-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="93bef-115">`constraints.allowedSizes`ve `constraints.excludedSizes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="93bef-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="93bef-116">Merhaba kullanılabilir boyutların listesi çağırarak belirlenebilir [listesinden bir abonelik için kullanılabilir sanal makine boyutlarını](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="93bef-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="93bef-117">`osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="93bef-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="93bef-118">Toodetermine hello donanım maliyetlerini hello sanal makinelerin kullandı.</span><span class="sxs-lookup"><span data-stu-id="93bef-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="93bef-119">`imageReference`üçüncü taraf görüntüleri için sağlanan ancak birinci taraf görüntüleri için atlandı.</span><span class="sxs-lookup"><span data-stu-id="93bef-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="93bef-120">Toodetermine hello yazılım maliyetleri hello sanal makinelerin kullandı.</span><span class="sxs-lookup"><span data-stu-id="93bef-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="93bef-121">`count`kullanılan tooset hello uygun çarpanı hello öğesi var.</span><span class="sxs-lookup"><span data-stu-id="93bef-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="93bef-122">Statik bir değer gibi destekleyen **2**, veya gibi başka bir öğeden dinamik bir değer `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="93bef-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="93bef-123">Merhaba varsayılan değer **1**.</span><span class="sxs-lookup"><span data-stu-id="93bef-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="93bef-124">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="93bef-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="93bef-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93bef-125">Next steps</span></span>
* <span data-ttu-id="93bef-126">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93bef-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="93bef-127">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93bef-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="93bef-128">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="93bef-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
