---
title: "Azure yönetilen uygulama VirtualNetworkCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Network.VirtualNetworkCombo kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="5b471-103">Microsoft.Network.VirtualNetworkCombo UI öğesi</span><span class="sxs-lookup"><span data-stu-id="5b471-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="5b471-104">Yeni veya var olan bir sanal ağ seçme denetimlerini grubudur.</span><span class="sxs-lookup"><span data-stu-id="5b471-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="5b471-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5b471-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5b471-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="5b471-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="5b471-108">Kullanıcının her alt ağın ad ve adres öneki özelleştirebileceğiniz şekilde üst Tel Çerçeve içinde yeni bir sanal ağ kullanıcı çekilmiş.</span><span class="sxs-lookup"><span data-stu-id="5b471-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="5b471-109">Alt yapılandırma bu durumda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5b471-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="5b471-110">Kullanıcı dağıtım şablonu gerektiren her alt ağ için mevcut bir alt eşlemeniz gerekir böylece alt Tel Çerçeve mevcut bir sanal ağ, kullanıcı çekilmiş.</span><span class="sxs-lookup"><span data-stu-id="5b471-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="5b471-111">Alt yapılandırma bu durumda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5b471-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="5b471-112">Şema</span><span class="sxs-lookup"><span data-stu-id="5b471-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="5b471-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5b471-113">Remarks</span></span>
- <span data-ttu-id="5b471-114">Belirtilmişse, ilk çakışmayan adres öneki boyutunun `defaultValue.addressPrefixSize` kullanıcının abonelik varolan sanal ağlarda temel alınarak otomatik olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="5b471-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="5b471-115">İçin varsayılan değer `defaultValue.name` ve `defaultValue.addressPrefixSize` olan **null**.</span><span class="sxs-lookup"><span data-stu-id="5b471-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="5b471-116">`constraints.minAddressPrefixSize`belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5b471-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="5b471-117">Belirtilen değerden daha küçük bir adres alanı ile var olan tüm sanal ağları seçilemez.</span><span class="sxs-lookup"><span data-stu-id="5b471-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="5b471-118">`subnets`belirtilmesi gerekir ve `constraints.minAddressPrefixSize` her alt ağ için belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5b471-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="5b471-119">Yeni bir sanal ağ oluştururken, her alt ağın adres öneki göre otomatik olarak sanal ağın adres öneki ve ilgili hesaplanır `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="5b471-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="5b471-120">Sanal varolan kullanırken, ağ, hiçbir alt ağ ilgili küçük `constraints.minAddressPrefixSize` seçim için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5b471-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="5b471-121">Ayrıca, belirtilirse, en az içermeyen alt ağlar `minAddressCount` kullanılabilir adresler seçilemez.</span><span class="sxs-lookup"><span data-stu-id="5b471-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="5b471-122">Varsayılan değer **0**.</span><span class="sxs-lookup"><span data-stu-id="5b471-122">The default value is **0**.</span></span> <span data-ttu-id="5b471-123">Kullanılabilir adresler bitişik olduğundan emin olmak için belirtmek **true** için `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="5b471-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="5b471-124">Varsayılan değer **doğru**.</span><span class="sxs-lookup"><span data-stu-id="5b471-124">The default value is **true**.</span></span>
- <span data-ttu-id="5b471-125">Varolan bir sanal ağ alt ağları oluşturma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5b471-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="5b471-126">Varsa `options.hideExisting` olan **doğru**, kullanıcı varolan bir sanal ağı seçemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b471-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="5b471-127">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="5b471-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5b471-128">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="5b471-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="5b471-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b471-129">Next steps</span></span>
* <span data-ttu-id="5b471-130">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b471-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5b471-131">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b471-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5b471-132">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5b471-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
