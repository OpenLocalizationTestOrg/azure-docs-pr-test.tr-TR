---
title: "Azure yönetilen uygulama PasswordBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.PasswordBox kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="fbdc8-103">Microsoft.Common.PasswordBox UI öğesi</span><span class="sxs-lookup"><span data-stu-id="fbdc8-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="fbdc8-104">Bir parolayı onaylayın ve sağlamak için kullanılan bir denetimi.</span><span class="sxs-lookup"><span data-stu-id="fbdc8-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="fbdc8-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fbdc8-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fbdc8-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="fbdc8-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="fbdc8-108">Şema</span><span class="sxs-lookup"><span data-stu-id="fbdc8-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="fbdc8-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="fbdc8-109">Remarks</span></span>
- <span data-ttu-id="fbdc8-110">Bu öğe desteklemiyor `defaultValue` özelliği.</span><span class="sxs-lookup"><span data-stu-id="fbdc8-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="fbdc8-111">Uygulama ayrıntıları için `constraints`, bkz: [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="fbdc8-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="fbdc8-112">Varsa `options.hideConfirmation` ayarlanır **doğru**, kullanıcının parolasını onayladığınız için ikinci metin kutusu gizlenir.</span><span class="sxs-lookup"><span data-stu-id="fbdc8-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="fbdc8-113">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="fbdc8-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fbdc8-114">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="fbdc8-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="fbdc8-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fbdc8-115">Next steps</span></span>
* <span data-ttu-id="fbdc8-116">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbdc8-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="fbdc8-117">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbdc8-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="fbdc8-118">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fbdc8-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
