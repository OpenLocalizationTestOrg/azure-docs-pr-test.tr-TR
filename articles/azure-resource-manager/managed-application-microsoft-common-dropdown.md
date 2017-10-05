---
title: "Azure yönetilen uygulama açılır UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.DropDown kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="1eccf-103">Microsoft.Common.DropDown UI öğesi</span><span class="sxs-lookup"><span data-stu-id="1eccf-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="1eccf-104">Seçim denetim bir açılır liste.</span><span class="sxs-lookup"><span data-stu-id="1eccf-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="1eccf-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1eccf-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1eccf-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="1eccf-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="1eccf-108">Şema</span><span class="sxs-lookup"><span data-stu-id="1eccf-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="1eccf-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1eccf-109">Remarks</span></span>
- <span data-ttu-id="1eccf-110">Etiketi `constraints.allowedValues` öğenin görünen metindir ve değerini öğesi seçildiğinde çıktı değeri.</span><span class="sxs-lookup"><span data-stu-id="1eccf-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="1eccf-111">Belirtilmişse, varsayılan değer mevcut bir etiketi olmalıdır `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="1eccf-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="1eccf-112">Belirtilmezse, listedeki ilk öğe `constraints.allowedValues` seçilir.</span><span class="sxs-lookup"><span data-stu-id="1eccf-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="1eccf-113">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="1eccf-113">The default value is **null**.</span></span>
- <span data-ttu-id="1eccf-114">`constraints.allowedValues`en az bir öğe içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1eccf-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="1eccf-115">Bu öğe desteklemiyor `constraints.required` özelliği.</span><span class="sxs-lookup"><span data-stu-id="1eccf-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="1eccf-116">Bu davranış benzetmek için bir etiket ve değerine sahip bir öğe eklemek `""` (boş dize) için `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="1eccf-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1eccf-117">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="1eccf-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="1eccf-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1eccf-118">Next steps</span></span>
* <span data-ttu-id="1eccf-119">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1eccf-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1eccf-120">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1eccf-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1eccf-121">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="1eccf-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
