---
title: "aaaAzure yönetilen uygulama VirtualNetworkCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Network.VirtualNetworkCombo UI öğesi açıklar"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="95871-103">Microsoft.Network.VirtualNetworkCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="95871-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="95871-104">Yeni veya var olan bir sanal ağ seçme denetimlerini grubudur.</span><span class="sxs-lookup"><span data-stu-id="95871-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="95871-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="95871-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="95871-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="95871-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="95871-108">Merhaba kullanıcı her alt ağın ad ve adres öneki özelleştirebileceğiniz şekilde hello üst Tel Çerçeve içinde yeni bir sanal ağ hello kullanıcı çekilmiş.</span><span class="sxs-lookup"><span data-stu-id="95871-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="95871-109">Alt yapılandırma bu durumda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="95871-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="95871-110">Merhaba alt Tel Çerçeve, hello kullanıcı varolan bir sanal ağı seçmiş olan, hello kullanıcı eşlemeniz gerekir böylece her alt ağ hello dağıtım şablonu tooan mevcut alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="95871-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="95871-111">Alt yapılandırma bu durumda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="95871-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="95871-112">Şema</span><span class="sxs-lookup"><span data-stu-id="95871-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="95871-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="95871-113">Remarks</span></span>
- <span data-ttu-id="95871-114">Belirtilmişse, ilk çakışmayan adres ön eki boyutu hello `defaultValue.addressPrefixSize` hello kullanıcının abonelik varolan sanal ağlarda temel alınarak otomatik olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="95871-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="95871-115">Merhaba için varsayılan değer `defaultValue.name` ve `defaultValue.addressPrefixSize` olan **null**.</span><span class="sxs-lookup"><span data-stu-id="95871-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="95871-116">`constraints.minAddressPrefixSize`belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="95871-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="95871-117">Mevcut hiçbir sanal ağ hello belirtilen değeri seçilemez küçük bir adres alanı ile.</span><span class="sxs-lookup"><span data-stu-id="95871-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="95871-118">`subnets`belirtilmesi gerekir ve `constraints.minAddressPrefixSize` her alt ağ için belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="95871-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="95871-119">Yeni bir sanal ağ oluştururken, her alt ağın adres öneki göre otomatik olarak hello sanal ağın adres öneki ve ilgili hesaplanır `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="95871-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="95871-120">Sanal varolan kullanırken, ağ, hiçbir alt ağ ilgili küçük `constraints.minAddressPrefixSize` seçim için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="95871-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="95871-121">Ayrıca, belirtilirse, en az içermeyen alt ağlar `minAddressCount` kullanılabilir adresler seçilemez.</span><span class="sxs-lookup"><span data-stu-id="95871-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="95871-122">Merhaba varsayılan değer **0**.</span><span class="sxs-lookup"><span data-stu-id="95871-122">hello default value is **0**.</span></span> <span data-ttu-id="95871-123">kullanılabilir adreslerin hello tooensure bitişik, belirtin **true** için `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="95871-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="95871-124">Merhaba varsayılan değer **doğru**.</span><span class="sxs-lookup"><span data-stu-id="95871-124">hello default value is **true**.</span></span>
- <span data-ttu-id="95871-125">Varolan bir sanal ağ alt ağları oluşturma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="95871-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="95871-126">Varsa `options.hideExisting` olan **doğru**, hello kullanıcı varolan bir sanal ağı seçilemez.</span><span class="sxs-lookup"><span data-stu-id="95871-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="95871-127">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="95871-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="95871-128">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="95871-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="95871-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95871-129">Next steps</span></span>
* <span data-ttu-id="95871-130">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95871-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="95871-131">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95871-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="95871-132">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="95871-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
