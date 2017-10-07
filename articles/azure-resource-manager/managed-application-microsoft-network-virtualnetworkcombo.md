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
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Microsoft.Network.VirtualNetworkCombo UI öğesi
Yeni veya var olan bir sanal ağ seçme denetimlerini grubudur. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- Merhaba kullanıcı her alt ağın ad ve adres öneki özelleştirebileceğiniz şekilde hello üst Tel Çerçeve içinde yeni bir sanal ağ hello kullanıcı çekilmiş. Alt yapılandırma bu durumda isteğe bağlıdır.
- Merhaba alt Tel Çerçeve, hello kullanıcı varolan bir sanal ağı seçmiş olan, hello kullanıcı eşlemeniz gerekir böylece her alt ağ hello dağıtım şablonu tooan mevcut alt gerektirir. Alt yapılandırma bu durumda gereklidir.

## <a name="schema"></a>Şema
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

## <a name="remarks"></a>Açıklamalar
- Belirtilmişse, ilk çakışmayan adres ön eki boyutu hello `defaultValue.addressPrefixSize` hello kullanıcının abonelik varolan sanal ağlarda temel alınarak otomatik olarak belirlenir.
- Merhaba için varsayılan değer `defaultValue.name` ve `defaultValue.addressPrefixSize` olan **null**.
- `constraints.minAddressPrefixSize`belirtilmelidir. Mevcut hiçbir sanal ağ hello belirtilen değeri seçilemez küçük bir adres alanı ile.
- `subnets`belirtilmesi gerekir ve `constraints.minAddressPrefixSize` her alt ağ için belirtilmelidir.
- Yeni bir sanal ağ oluştururken, her alt ağın adres öneki göre otomatik olarak hello sanal ağın adres öneki ve ilgili hesaplanır `addressPrefixSize`.
- Sanal varolan kullanırken, ağ, hiçbir alt ağ ilgili küçük `constraints.minAddressPrefixSize` seçim için kullanılamaz. Ayrıca, belirtilirse, en az içermeyen alt ağlar `minAddressCount` kullanılabilir adresler seçilemez.
Merhaba varsayılan değer **0**. kullanılabilir adreslerin hello tooensure bitişik, belirtin **true** için `requireContiguousAddresses`. Merhaba varsayılan değer **doğru**.
- Varolan bir sanal ağ alt ağları oluşturma desteklenmiyor.
- Varsa `options.hideExisting` olan **doğru**, hello kullanıcı varolan bir sanal ağı seçilemez. Merhaba varsayılan değer **false**.

## <a name="sample-output"></a>Örnek çıktı
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

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
