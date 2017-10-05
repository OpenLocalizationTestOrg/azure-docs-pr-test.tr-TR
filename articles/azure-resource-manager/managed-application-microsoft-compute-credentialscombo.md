---
title: "Azure yönetilen uygulama CredentialsCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Compute.CredentialsCombo kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="09aef-103">Microsoft.Compute.CredentialsCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="09aef-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="09aef-104">Windows ve Linux parolalar ve SSH ortak anahtarları için yerleşik doğrulama denetimleriyle grubudur.</span><span class="sxs-lookup"><span data-stu-id="09aef-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="09aef-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="09aef-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="09aef-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="09aef-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="09aef-108">Şema</span><span class="sxs-lookup"><span data-stu-id="09aef-108">Schema</span></span>
<span data-ttu-id="09aef-109">Varsa `osPlatform` olan **Windows**, aşağıdaki şema kullanılır:</span><span class="sxs-lookup"><span data-stu-id="09aef-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="09aef-110">Varsa `osPlatform` olan **Linux**, aşağıdaki şema kullanılır:</span><span class="sxs-lookup"><span data-stu-id="09aef-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="09aef-111">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="09aef-111">Remarks</span></span>
- <span data-ttu-id="09aef-112">`osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="09aef-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="09aef-113">Varsa `constraints.required` ayarlanır **doğru**, parola veya SSH ortak anahtarı metin kutuları başarıyla doğrulamak için değerleri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09aef-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="09aef-114">Varsayılan değer **doğru**.</span><span class="sxs-lookup"><span data-stu-id="09aef-114">The default value is **true**.</span></span>
- <span data-ttu-id="09aef-115">Varsa `options.hideConfirmation` ayarlanır **doğru**, sonra da kullanıcının parolasını onayladığınız için ikinci metin kutusu gizli.</span><span class="sxs-lookup"><span data-stu-id="09aef-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="09aef-116">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="09aef-116">The default value is **false**.</span></span>
- <span data-ttu-id="09aef-117">Varsa `options.hidePassword` ayarlanır **doğru**, parola kimlik doğrulaması kullanma seçeneğini gizli sonra.</span><span class="sxs-lookup"><span data-stu-id="09aef-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="09aef-118">Kullanılabilmesi için yalnızca `osPlatform` olan **Linux**.</span><span class="sxs-lookup"><span data-stu-id="09aef-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="09aef-119">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="09aef-119">The default value is **false**.</span></span>
- <span data-ttu-id="09aef-120">İzin verilen parolalar ek kısıtlamalar kullanarak uygulanabilir `customPasswordRegex` özelliği.</span><span class="sxs-lookup"><span data-stu-id="09aef-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="09aef-121">Dizede `customValidationMessage` parola özel doğrulama başarısız olduğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="09aef-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="09aef-122">Her iki özellik için varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="09aef-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="09aef-123">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="09aef-123">Sample output</span></span>
<span data-ttu-id="09aef-124">Varsa `osPlatform` olan **Windows**, veya kullanıcı parola yerine bir SSH ortak anahtarı sağlanan sonra aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="09aef-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="09aef-125">Kullanıcı SSH ortak anahtarı sağladıysanız, aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="09aef-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="09aef-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09aef-126">Next steps</span></span>
* <span data-ttu-id="09aef-127">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09aef-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="09aef-128">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09aef-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="09aef-129">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="09aef-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
