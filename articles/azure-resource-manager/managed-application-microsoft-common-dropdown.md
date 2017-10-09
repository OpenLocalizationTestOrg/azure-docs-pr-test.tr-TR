---
title: "aaaAzure yönetilen uygulama açılır UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.DropDown UI öğesi açıklar"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="71905-103">Microsoft.Common.DropDown UI öğesi</span><span class="sxs-lookup"><span data-stu-id="71905-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="71905-104">Seçim denetim bir açılır liste.</span><span class="sxs-lookup"><span data-stu-id="71905-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="71905-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="71905-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="71905-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="71905-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="71905-108">Şema</span><span class="sxs-lookup"><span data-stu-id="71905-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="71905-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="71905-109">Remarks</span></span>
- <span data-ttu-id="71905-110">Merhaba etiketi `constraints.allowedValues` öğenin hello görüntüleme metni ve değeri seçildiğinde hello öğesinin hello çıktı değeri.</span><span class="sxs-lookup"><span data-stu-id="71905-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="71905-111">Belirtilmişse, hello varsayılan değer mevcut bir etiketi olmalıdır `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="71905-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="71905-112">Belirtilmezse, ilk öğe olarak hello `constraints.allowedValues` seçilir.</span><span class="sxs-lookup"><span data-stu-id="71905-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="71905-113">Merhaba varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="71905-113">hello default value is **null**.</span></span>
- <span data-ttu-id="71905-114">`constraints.allowedValues`en az bir öğe içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="71905-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="71905-115">Bu öğe hello desteklemiyor `constraints.required` özelliği.</span><span class="sxs-lookup"><span data-stu-id="71905-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="71905-116">tooemulate Bu davranış bir etiket ve değerine sahip bir öğe eklemek `""` (çok dize boş)`constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="71905-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="71905-117">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="71905-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="71905-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="71905-118">Next steps</span></span>
* <span data-ttu-id="71905-119">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71905-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="71905-120">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71905-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="71905-121">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="71905-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
