---
title: "aaaAzure yönetilen uygulama UserNameTextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Compute.UserNameTextBox UI öğesi açıklar"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="6489c-103">Microsoft.Compute.UserNameTextBox UI öğesi</span><span class="sxs-lookup"><span data-stu-id="6489c-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="6489c-104">Bir metin kutusu denetiminin Windows ve Linux kullanıcı adları için yerleşik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="6489c-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="6489c-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6489c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6489c-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="6489c-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="6489c-108">Şema</span><span class="sxs-lookup"><span data-stu-id="6489c-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6489c-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="6489c-109">Remarks</span></span>
- <span data-ttu-id="6489c-110">Varsa `constraints.required` çok ayarlanır**doğru**, hello metin kutusuna bir değer toovalidate başarıyla içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6489c-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="6489c-111">Merhaba varsayılan değer **doğru**.</span><span class="sxs-lookup"><span data-stu-id="6489c-111">hello default value is **true**.</span></span>
- <span data-ttu-id="6489c-112">`osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="6489c-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="6489c-113">`constraints.regex`JavaScript normal ifade deseni olur.</span><span class="sxs-lookup"><span data-stu-id="6489c-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="6489c-114">Belirtilmişse, ardından hello metin kutusunun değerini hello düzeni toovalidate başarıyla eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6489c-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="6489c-115">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="6489c-115">The default value is **null**.</span></span>
- <span data-ttu-id="6489c-116">`constraints.validationMessage`bir dize toodisplay Hello metin kutusunun değeri tarafından belirtilen hello doğrulama başarısız olduğunda `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="6489c-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="6489c-117">Aksi takdirde belirtilen ardından metin kutusunun yerleşik doğrulama iletileri kullanılan hello.</span><span class="sxs-lookup"><span data-stu-id="6489c-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="6489c-118">Merhaba varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="6489c-118">hello default value is **null**.</span></span>
- <span data-ttu-id="6489c-119">Bu öğe için belirtilen başlangıç değeri temel alan yerleşik doğrulama sahip `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="6489c-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="6489c-120">Merhaba yerleşik doğrulama bir özel normal ifade ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6489c-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="6489c-121">İçin bir değer `constraints.regex` belirtilmişse hem yerleşik hello ve özel doğrulama tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="6489c-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6489c-122">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="6489c-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="6489c-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6489c-123">Next steps</span></span>
* <span data-ttu-id="6489c-124">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6489c-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6489c-125">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6489c-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6489c-126">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6489c-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
