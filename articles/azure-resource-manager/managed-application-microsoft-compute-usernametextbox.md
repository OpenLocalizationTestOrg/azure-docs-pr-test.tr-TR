---
title: "Azure yönetilen uygulama UserNameTextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Compute.UserNameTextBox kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="db60b-103">Microsoft.Compute.UserNameTextBox UI öğesi</span><span class="sxs-lookup"><span data-stu-id="db60b-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="db60b-104">Bir metin kutusu denetiminin Windows ve Linux kullanıcı adları için yerleşik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="db60b-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="db60b-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="db60b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="db60b-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="db60b-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="db60b-108">Şema</span><span class="sxs-lookup"><span data-stu-id="db60b-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="db60b-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="db60b-109">Remarks</span></span>
- <span data-ttu-id="db60b-110">Varsa `constraints.required` ayarlanır **doğru**, metin kutusunun başarıyla doğrulamak için bir değer içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="db60b-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="db60b-111">Varsayılan değer **doğru**.</span><span class="sxs-lookup"><span data-stu-id="db60b-111">The default value is **true**.</span></span>
- <span data-ttu-id="db60b-112">`osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="db60b-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="db60b-113">`constraints.regex`JavaScript normal ifade deseni olur.</span><span class="sxs-lookup"><span data-stu-id="db60b-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="db60b-114">Belirtilmişse, metin kutusunun değerini başarıyla doğrulamak için desen eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="db60b-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="db60b-115">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="db60b-115">The default value is **null**.</span></span>
- <span data-ttu-id="db60b-116">`constraints.validationMessage`metin kutusunun değeri tarafından belirtilen doğrulama başarısız olduğunda görüntülemek için bir dizedir `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="db60b-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="db60b-117">Belirtilmezse, metin kutusunun yerleşik doğrulama iletileri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="db60b-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="db60b-118">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="db60b-118">The default value is **null**.</span></span>
- <span data-ttu-id="db60b-119">Bu öğe için belirtilen değeri temel alan yerleşik doğrulama sahip `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="db60b-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="db60b-120">Yerleşik doğrulama bir özel normal ifade ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="db60b-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="db60b-121">İçin bir değer `constraints.regex` belirtildiğinden, yerleşik ve özel doğrulama tetiklenen sonra.</span><span class="sxs-lookup"><span data-stu-id="db60b-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="db60b-122">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="db60b-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="db60b-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db60b-123">Next steps</span></span>
* <span data-ttu-id="db60b-124">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db60b-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="db60b-125">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db60b-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="db60b-126">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="db60b-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
