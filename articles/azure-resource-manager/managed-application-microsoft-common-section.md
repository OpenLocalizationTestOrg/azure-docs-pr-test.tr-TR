---
title: "aaaAzure yönetilen uygulama bölümü UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.Section UI öğesi açıklar"
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="e22f8-103">Microsoft.Common.Section UI öğesi</span><span class="sxs-lookup"><span data-stu-id="e22f8-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="e22f8-104">Bir veya daha fazla öğe bir başlık altında grupları denetim.</span><span class="sxs-lookup"><span data-stu-id="e22f8-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="e22f8-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e22f8-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e22f8-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="e22f8-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="e22f8-108">Şema</span><span class="sxs-lookup"><span data-stu-id="e22f8-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="e22f8-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e22f8-109">Remarks</span></span>
- <span data-ttu-id="e22f8-110">`elements`en az bir öğe içermelidir ve dışındaki tüm öğe türleri içerebilir `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="e22f8-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="e22f8-111">Bu öğe hello desteklemiyor `toolTip` özelliği.</span><span class="sxs-lookup"><span data-stu-id="e22f8-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e22f8-112">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="e22f8-112">Sample output</span></span>
<span data-ttu-id="e22f8-113">tooaccess hello çıktı öğeleri değerlerini `elements`, hello kullan [basics()](managed-application-createuidefinition-functions.md#basics) veya [steps()](managed-application-createuidefinition-functions.md#steps) işlevler ve noktalı gösterim:</span><span class="sxs-lookup"><span data-stu-id="e22f8-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="e22f8-114">Türündeki öğeler `Microsoft.Common.Section` hiçbir çıktı değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="e22f8-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e22f8-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e22f8-115">Next steps</span></span>
* <span data-ttu-id="e22f8-116">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e22f8-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e22f8-117">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e22f8-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e22f8-118">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="e22f8-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
