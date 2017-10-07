---
title: "aaaAzure yönetilen uygulama CredentialsCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Compute.CredentialsCombo UI öğesi açıklar"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="3edf5-103">Microsoft.Compute.CredentialsCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="3edf5-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="3edf5-104">Windows ve Linux parolalar ve SSH ortak anahtarları için yerleşik doğrulama denetimleriyle grubudur.</span><span class="sxs-lookup"><span data-stu-id="3edf5-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="3edf5-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3edf5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="3edf5-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="3edf5-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="3edf5-108">Şema</span><span class="sxs-lookup"><span data-stu-id="3edf5-108">Schema</span></span>
<span data-ttu-id="3edf5-109">Varsa `osPlatform` olan **Windows**, hello aşağıdaki şema kullanılır:</span><span class="sxs-lookup"><span data-stu-id="3edf5-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="3edf5-110">Varsa `osPlatform` olan **Linux**, hello aşağıdaki şema kullanılır:</span><span class="sxs-lookup"><span data-stu-id="3edf5-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="3edf5-111">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="3edf5-111">Remarks</span></span>
- <span data-ttu-id="3edf5-112">`osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="3edf5-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="3edf5-113">Varsa `constraints.required` çok ayarlanır**doğru**, parola hello veya SSH ortak anahtarı metin kutuları içermelidir değerleri toovalidate başarıyla.</span><span class="sxs-lookup"><span data-stu-id="3edf5-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="3edf5-114">Merhaba varsayılan değer **doğru**.</span><span class="sxs-lookup"><span data-stu-id="3edf5-114">hello default value is **true**.</span></span>
- <span data-ttu-id="3edf5-115">Varsa `options.hideConfirmation` çok ayarlanır**doğru**, hello kullanıcının parolasını onayladığınız için hello ikinci metin kutusu gizli sonra.</span><span class="sxs-lookup"><span data-stu-id="3edf5-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="3edf5-116">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="3edf5-116">hello default value is **false**.</span></span>
- <span data-ttu-id="3edf5-117">Varsa `options.hidePassword` çok ayarlanır**doğru**, hello seçeneği toouse parola kimlik doğrulaması gizli sonra.</span><span class="sxs-lookup"><span data-stu-id="3edf5-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="3edf5-118">Kullanılabilmesi için yalnızca `osPlatform` olan **Linux**.</span><span class="sxs-lookup"><span data-stu-id="3edf5-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="3edf5-119">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="3edf5-119">The default value is **false**.</span></span>
- <span data-ttu-id="3edf5-120">Merhaba ek kısıtlamalar izin hello kullanarak parolaları uygulanabilir `customPasswordRegex` özelliği.</span><span class="sxs-lookup"><span data-stu-id="3edf5-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="3edf5-121">Merhaba dizesinde `customValidationMessage` parola özel doğrulama başarısız olduğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3edf5-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="3edf5-122">Merhaba her iki özellik için varsayılan değer olan **null**.</span><span class="sxs-lookup"><span data-stu-id="3edf5-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="3edf5-123">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="3edf5-123">Sample output</span></span>
<span data-ttu-id="3edf5-124">Varsa `osPlatform` olan **Windows**, veya hello kullanıcı sağlanan parola yerine bir SSH ortak anahtarı ardından hello aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="3edf5-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="3edf5-125">Merhaba kullanıcı SSH ortak anahtarı sağladıysanız, ardından hello aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="3edf5-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="3edf5-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3edf5-126">Next steps</span></span>
* <span data-ttu-id="3edf5-127">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3edf5-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3edf5-128">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3edf5-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="3edf5-129">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="3edf5-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
