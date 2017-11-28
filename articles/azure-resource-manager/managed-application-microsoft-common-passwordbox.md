---
title: "aaaAzure yönetilen uygulama PasswordBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.PasswordBox UI öğesi açıklar"
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="e09ea-103">Microsoft.Common.PasswordBox UI öğesi</span><span class="sxs-lookup"><span data-stu-id="e09ea-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="e09ea-104">Kullanılan tooprovide ve bir parolayı onaylayın denetim.</span><span class="sxs-lookup"><span data-stu-id="e09ea-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="e09ea-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e09ea-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e09ea-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="e09ea-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="e09ea-108">Şema</span><span class="sxs-lookup"><span data-stu-id="e09ea-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="e09ea-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e09ea-109">Remarks</span></span>
- <span data-ttu-id="e09ea-110">Bu öğe hello desteklemiyor `defaultValue` özelliği.</span><span class="sxs-lookup"><span data-stu-id="e09ea-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="e09ea-111">Uygulama ayrıntıları için `constraints`, bkz: [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="e09ea-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="e09ea-112">Varsa `options.hideConfirmation` çok ayarlanır**doğru**, hello kullanıcının parolasını onayladığınız için hello ikinci metin kutusu gizlenir.</span><span class="sxs-lookup"><span data-stu-id="e09ea-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="e09ea-113">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="e09ea-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e09ea-114">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="e09ea-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="e09ea-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e09ea-115">Next steps</span></span>
* <span data-ttu-id="e09ea-116">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e09ea-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e09ea-117">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e09ea-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e09ea-118">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="e09ea-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
