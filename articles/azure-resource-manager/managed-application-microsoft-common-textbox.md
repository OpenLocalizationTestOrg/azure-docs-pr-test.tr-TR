---
title: "aaaAzure yönetilen uygulama TextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.TextBox UI öğesi açıklar"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="6def6-103">Microsoft.Common.TextBox UI öğesi</span><span class="sxs-lookup"><span data-stu-id="6def6-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="6def6-104">Kullanılan tooedit olabilir bir denetim biçimlendirilmemiş metin.</span><span class="sxs-lookup"><span data-stu-id="6def6-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="6def6-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6def6-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6def6-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="6def6-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="6def6-108">Şema</span><span class="sxs-lookup"><span data-stu-id="6def6-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6def6-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="6def6-109">Remarks</span></span>
- <span data-ttu-id="6def6-110">Varsa `constraints.required` çok ayarlanır**doğru**, hello metin kutusuna bir değer toovalidate başarıyla içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6def6-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="6def6-111">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="6def6-111">hello default value is **false**.</span></span>
- <span data-ttu-id="6def6-112">`constraints.regex`JavaScript normal ifade deseni olur.</span><span class="sxs-lookup"><span data-stu-id="6def6-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="6def6-113">Belirtilmişse, ardından hello metin kutusunun değerini hello düzeni toovalidate başarıyla eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6def6-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="6def6-114">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="6def6-114">The default value is **null**.</span></span>
- <span data-ttu-id="6def6-115">`constraints.validationMessage`bir dize toodisplay Hello metin kutusunun değerini doğrulama başarısız olduğunda.</span><span class="sxs-lookup"><span data-stu-id="6def6-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="6def6-116">Aksi takdirde belirtilen ardından metin kutusunun yerleşik doğrulama iletileri kullanılan hello.</span><span class="sxs-lookup"><span data-stu-id="6def6-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="6def6-117">Merhaba varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="6def6-117">hello default value is **null**.</span></span>
- <span data-ttu-id="6def6-118">Olası toospecify için bir değer `constraints.regex` zaman `constraints.required` çok ayarlanır**false**.</span><span class="sxs-lookup"><span data-stu-id="6def6-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="6def6-119">Bu senaryoda, bir değer başarıyla hello metin kutusu toovalidate için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="6def6-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="6def6-120">Belirtilmişse, bu hello normal ifade deseni eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="6def6-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6def6-121">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="6def6-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="6def6-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6def6-122">Next steps</span></span>
* <span data-ttu-id="6def6-123">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6def6-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6def6-124">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6def6-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6def6-125">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6def6-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
