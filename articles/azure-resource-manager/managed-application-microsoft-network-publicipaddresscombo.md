---
title: "Azure yönetilen uygulama PublicIpAddressCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Network.PublicIpAddressCombo kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="e44e9-103">Microsoft.Network.PublicIpAddressCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="e44e9-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="e44e9-104">Yeni veya var olan ortak IP adresi seçme denetimlerini grubudur.</span><span class="sxs-lookup"><span data-stu-id="e44e9-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="e44e9-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e44e9-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e44e9-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="e44e9-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="e44e9-108">Kullanıcının ortak IP adresi için ' None' seçerse, etki alanı adı etiketi metin kutusu gizlenir.</span><span class="sxs-lookup"><span data-stu-id="e44e9-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="e44e9-109">Kullanıcı var olan bir ortak IP adresi seçer, etki alanı adı etiketi metin kutusu devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="e44e9-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="e44e9-110">Seçili IP adresinin etki alanı adı etiketi değeri olduğu.</span><span class="sxs-lookup"><span data-stu-id="e44e9-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="e44e9-111">Otomatik olarak seçilen konum temelinde etki alanı adı soneki (örneğin, westus.cloudapp.azure.com) güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="e44e9-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="e44e9-112">Şema</span><span class="sxs-lookup"><span data-stu-id="e44e9-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="e44e9-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e44e9-113">Remarks</span></span>
- <span data-ttu-id="e44e9-114">Varsa `constraints.required.domainNameLabel` ayarlanır **doğru**, kullanıcı, yeni bir ortak IP adresi oluştururken, bir etki alanı adı etiketi sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e44e9-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="e44e9-115">Bir etiketi olmayan olmadan seçime uygun varolan ortak IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="e44e9-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="e44e9-116">Varsa `options.hideNone` ayarlanır **true**, ardından belirleme seçeneği **hiçbiri** için genel IP adresi gizlenir.</span><span class="sxs-lookup"><span data-stu-id="e44e9-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="e44e9-117">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="e44e9-117">The default value is **false**.</span></span>
- <span data-ttu-id="e44e9-118">Varsa `options.hideDomainNameLabel` ayarlanır **doğru**, etki alanı adı etiketi için metin kutusu gizli sonra.</span><span class="sxs-lookup"><span data-stu-id="e44e9-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="e44e9-119">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="e44e9-119">The default value is **false**.</span></span>
- <span data-ttu-id="e44e9-120">Varsa `options.hideExisting` kullanıcı mevcut bir ortak IP adresini seçebilir değil sonra true olur.</span><span class="sxs-lookup"><span data-stu-id="e44e9-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="e44e9-121">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="e44e9-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e44e9-122">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="e44e9-122">Sample output</span></span>
<span data-ttu-id="e44e9-123">Kullanıcının ortak IP adresi seçerse, aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="e44e9-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="e44e9-124">Kullanıcı yeni veya var olan bir IP adresi seçerse, aşağıdaki çıkış bekleniyor:</span><span class="sxs-lookup"><span data-stu-id="e44e9-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="e44e9-125">Zaman `options.hideNone` belirtilirse, `newOrExistingOrNone` her zaman döndürür **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="e44e9-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="e44e9-126">Zaman `options.hideDomainNameLabel` belirtilirse, `domainNameLabel` bildirilmedi.</span><span class="sxs-lookup"><span data-stu-id="e44e9-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e44e9-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e44e9-127">Next steps</span></span>
* <span data-ttu-id="e44e9-128">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e44e9-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e44e9-129">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e44e9-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e44e9-130">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="e44e9-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
