---
title: "Azure yönetilen uygulama SizeSelector UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Compute.SizeSelector kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="c2d8d-103">Microsoft.Compute.SizeSelector UI öğesi</span><span class="sxs-lookup"><span data-stu-id="c2d8d-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="c2d8d-104">Bir veya daha fazla sanal makine örnekleri için bir boyut seçmek için bir denetim.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="c2d8d-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c2d8d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="c2d8d-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="c2d8d-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="c2d8d-108">Şema</span><span class="sxs-lookup"><span data-stu-id="c2d8d-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="c2d8d-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="c2d8d-109">Remarks</span></span>
- <span data-ttu-id="c2d8d-110">`recommendedSizes`en az bir boyut içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="c2d8d-111">İlk önerilen boyut, varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="c2d8d-112">Önerilen boyut Seçilen konumda kullanılabilir durumda değilse, boyutu otomatik olarak atlandı.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="c2d8d-113">Bunun yerine, önerilen bir sonraki boyuta kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="c2d8d-114">Belirtilen olmayan herhangi bir boyutta `constraints.allowedSizes` gizlenir ve belirtilen olmayan herhangi bir boyutta `constraints.excludedSizes` gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="c2d8d-115">`constraints.allowedSizes`ve `constraints.excludedSizes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="c2d8d-116">Kullanılabilir boyutların listesi çağırarak belirlenebilir [listesinden bir abonelik için kullanılabilir sanal makine boyutlarını](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="c2d8d-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="c2d8d-117">`osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="c2d8d-118">Sanal makinelerin donanım maliyetlerini belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="c2d8d-119">`imageReference`üçüncü taraf görüntüleri için sağlanan ancak birinci taraf görüntüleri için atlandı.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="c2d8d-120">Sanal makinelerin yazılım maliyetleri belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="c2d8d-121">`count`öğesi için uygun çarpanı ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="c2d8d-122">Statik bir değer gibi destekleyen **2**, veya gibi başka bir öğeden dinamik bir değer `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="c2d8d-123">Varsayılan değer **1**.</span><span class="sxs-lookup"><span data-stu-id="c2d8d-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="c2d8d-124">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="c2d8d-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="c2d8d-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2d8d-125">Next steps</span></span>
* <span data-ttu-id="c2d8d-126">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2d8d-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c2d8d-127">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2d8d-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="c2d8d-128">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="c2d8d-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
