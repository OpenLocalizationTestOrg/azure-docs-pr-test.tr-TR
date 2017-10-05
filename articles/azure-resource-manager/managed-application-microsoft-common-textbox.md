---
title: "Azure yönetilen uygulama TextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.TextBox kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="4886d-103">Microsoft.Common.TextBox UI öğesi</span><span class="sxs-lookup"><span data-stu-id="4886d-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="4886d-104">Biçimlendirilmemiş metin düzenlemek için kullanılan bir denetimi.</span><span class="sxs-lookup"><span data-stu-id="4886d-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="4886d-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4886d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4886d-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="4886d-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="4886d-108">Şema</span><span class="sxs-lookup"><span data-stu-id="4886d-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="4886d-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="4886d-109">Remarks</span></span>
- <span data-ttu-id="4886d-110">Varsa `constraints.required` ayarlanır **doğru**, metin kutusunun başarıyla doğrulamak için bir değer içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4886d-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="4886d-111">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="4886d-111">The default value is **false**.</span></span>
- <span data-ttu-id="4886d-112">`constraints.regex`JavaScript normal ifade deseni olur.</span><span class="sxs-lookup"><span data-stu-id="4886d-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="4886d-113">Belirtilmişse, metin kutusunun değerini başarıyla doğrulamak için desen eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4886d-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="4886d-114">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="4886d-114">The default value is **null**.</span></span>
- <span data-ttu-id="4886d-115">`constraints.validationMessage`metin kutusunun değerini doğrulanamadığında görüntülenecek bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="4886d-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="4886d-116">Belirtilmezse, metin kutusunun yerleşik doğrulama iletileri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4886d-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="4886d-117">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="4886d-117">The default value is **null**.</span></span>
- <span data-ttu-id="4886d-118">İçin bir değer belirtin mümkündür `constraints.regex` zaman `constraints.required` ayarlanır **false**.</span><span class="sxs-lookup"><span data-stu-id="4886d-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="4886d-119">Bu senaryoda, bir değer başarıyla doğrulamak metin kutusu için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="4886d-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="4886d-120">Belirtilmişse, normal ifade deseni eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4886d-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4886d-121">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="4886d-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="4886d-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4886d-122">Next steps</span></span>
* <span data-ttu-id="4886d-123">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4886d-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4886d-124">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4886d-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4886d-125">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4886d-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
