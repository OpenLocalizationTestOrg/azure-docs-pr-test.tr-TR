---
title: "aaaAzure yönetilen uygulama PublicIpAddressCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Network.PublicIpAddressCombo UI öğesi açıklar"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="134f6-103">Microsoft.Network.PublicIpAddressCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="134f6-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="134f6-104">Yeni veya var olan ortak IP adresi seçme denetimlerini grubudur.</span><span class="sxs-lookup"><span data-stu-id="134f6-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="134f6-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="134f6-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="134f6-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="134f6-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="134f6-108">Genel IP adresi için ' None' Hello kullanıcı seçerse, hello etki alanı adı etiketi metin kutusu gizlenir.</span><span class="sxs-lookup"><span data-stu-id="134f6-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="134f6-109">Mevcut bir ortak IP adresini Hello kullanıcının seçtiği hello etki alanı adı etiketi metin kutusu devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="134f6-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="134f6-110">Değerini hello etki alanı adı etiketi hello seçili IP adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="134f6-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="134f6-111">etki alanı adı soneki (örneğin, westus.cloudapp.azure.com) güncelleştirmeleri otomatik olarak seçilen hello konum temelinde hello.</span><span class="sxs-lookup"><span data-stu-id="134f6-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="134f6-112">Şema</span><span class="sxs-lookup"><span data-stu-id="134f6-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="134f6-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="134f6-113">Remarks</span></span>
- <span data-ttu-id="134f6-114">Varsa `constraints.required.domainNameLabel` çok ayarlanır**doğru**, yeni bir ortak IP adresi oluştururken hello kullanıcı bir etki alanı adı etiketi sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="134f6-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="134f6-115">Bir etiketi olmayan olmadan seçime uygun varolan ortak IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="134f6-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="134f6-116">Varsa `options.hideNone` çok ayarlanır**true**, seçeneği tooselect hello **hiçbiri** hello için genel IP adresi gizlenir.</span><span class="sxs-lookup"><span data-stu-id="134f6-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="134f6-117">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="134f6-117">hello default value is **false**.</span></span>
- <span data-ttu-id="134f6-118">Varsa `options.hideDomainNameLabel` çok ayarlanır**doğru**, etki alanı adı etiketi hello metin kutusu gizli sonra.</span><span class="sxs-lookup"><span data-stu-id="134f6-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="134f6-119">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="134f6-119">hello default value is **false**.</span></span>
- <span data-ttu-id="134f6-120">Varsa `options.hideExisting` hello kullanıcı mümkün toochoose mevcut bir ortak IP adresini değil sonra true olur.</span><span class="sxs-lookup"><span data-stu-id="134f6-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="134f6-121">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="134f6-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="134f6-122">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="134f6-122">Sample output</span></span>
<span data-ttu-id="134f6-123">Merhaba kullanıcı ortak IP adresi seçerse, hello aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="134f6-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="134f6-124">Merhaba kullanıcı yeni veya var olan bir IP adresi seçer, hello aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="134f6-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="134f6-125">Zaman `options.hideNone` belirtilirse, `newOrExistingOrNone` her zaman döndürür **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="134f6-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="134f6-126">Zaman `options.hideDomainNameLabel` belirtilirse, `domainNameLabel` bildirilmedi.</span><span class="sxs-lookup"><span data-stu-id="134f6-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="134f6-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="134f6-127">Next steps</span></span>
* <span data-ttu-id="134f6-128">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="134f6-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="134f6-129">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="134f6-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="134f6-130">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="134f6-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
