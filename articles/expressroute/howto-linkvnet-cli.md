---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: CLI: Azure | Microsoft Docs"
description: "Bu belge hello Resource Manager dağıtım modeli ve CLI kullanarak (Vnet'ler) tooExpressRoute devreler nasıl toolink sanal ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>CLI kullanarak bir sanal ağ tooan expressroute bağlantı hattı Bağlan

Bu makale, CLI kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute devreleri bağlantı yardımcı olur. Azure CLI kullanarak toolink hello sanal ağlar hello Resource Manager dağıtım modeli kullanılarak oluşturulması gerekir. Hello ya da olabilir aynı abonelik ya da başka bir abonelik parçası. VNet tooan expressroute bağlantı hattı toouse farklı yöntem tooconnect istiyorsanız, bir makale listesi aşağıdaki hello seçebilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Yapılandırma önkoşulları

* Merhaba komut satırı arabirimi (CLI) en son sürümünü hello gerekir. Daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* Tooreview hello gereksinim [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. 
  * Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](howto-circuit-cli.md) ve bağlantı sağlayıcınız tarafından etkinleştirilmiş hello hattı sahip. 
  * Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun. Merhaba bkz [yönlendirmeyi yapılandırma](howto-routing-cli.md) yönlendirme yönergeleri için makalenin. 
  * Azure özel eşleme yapılandırıldığından emin olun. uçtan uca bağlantı etkinleştirebilmeniz için yukarı ağınız ve Microsoft arasında hello BGP eşliği olması gerekir.
  * Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olduğundan emin olun. Çok olarak Hello yönergeleri[ExpressRoute için bir sanal ağ geçidi yapılandırma](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Emin toouse olması `--gateway-type ExpressRoute`.

* Too10 sanal ağlar tooa standart expressroute bağlantı hattı bağlayabilirsiniz. Tüm sanal ağları hello olmalıdır standart bir expressroute bağlantı hattını kullanırken aynı coğrafi bölge. 

* Hello ExpressRoute premium eklentisi etkinleştirirseniz, bir sanal ağ dışında hello coğrafi bölge hello expressroute bağlantı hattı, bağlantı ya da çok sayıda sanal ağlar tooyour expressroute bağlantı hattı bağlanın. Merhaba hello premium eklentisi hakkında daha fazla bilgi için bkz: [SSS](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı

Merhaba örneği kullanarak bir sanal ağ geçidi tooan expressroute bağlantı hattı bağlanabilir. Bu hello sanal ağ geçidi oluşturulur ve hello komutunu çalıştırmadan önce bağlama için hazır olduğundan emin olun.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Farklı bir abonelik tooa hattı sanal bir ağa bağlan

Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz. Aşağıdaki Hello şekilde birden çok abonelik arasında basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterilmektedir.

Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir. Her hello kuruluşunuz içinde hello bölümlerin kendi aboneliği kullanabilirsiniz dağıtmak için kendi hizmetlerini--ancak tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşabilirsiniz. Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir. Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.

> [!NOTE]
> Bağlantı ve bant genişliği ücretleri ayrılmış hello hattı için uygulanan toohello ExpressRoute bağlantı hattı sahip olacaktır. Tüm sanal ağları hello paylaşmak aynı bant genişliği.
> 
> 

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Yönetim - hattı sahipleri ve hattı kullanıcılar

Merhaba 'Devre sahibinden' hello ExpressRoute bağlantı hattı kaynak yetkili bir güç kullanıcısıdır. Merhaba devre sahibinden 'hattı kullanıcılar tarafından kullanılan yetkilerini oluşturabilirsiniz. Bağlantı hattı kullanıcılardır sahipleri sanal ağ içinde olmayan ağ geçitleri, expressroute bağlantı hattı hello gibi aynı abonelik hello. Bağlantı hattı kullanıcıların yetkilerini (sanal ağ başına bir yetkilendirme) kullanmak.

Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir. Bir yetkilendirme iptal edildiğinde, tüm bağlantı erişimini iptal edildi hello abonelikten silinir.

### <a name="circuit-owner-operations"></a>Sahip işlem hattı

**toocreate bir yetkilendirme**

Merhaba devre sahibinden oluşturur olabilir bir yetkilendirme anahtarı oluşturur bir yetkilendirme kendi sanal ağ ağ geçitleri toohello expressroute bağlantı hattı kullanıcı tooconnect tarafından kullanılır. Bir yetkilendirme yalnızca bir bağlantı için geçerli değil.

örnekte gösterildiği nasıl aşağıdaki hello toocreate bir yetkilendirme:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

Merhaba yanıt hello yetkilendirme anahtar ve durum içerir:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview yetkilerini**

Merhaba devre sahibinden aşağıdaki örneğine hello çalıştırarak belirli bir bağlantı hattı üzerinde verilen tüm yetkilerini gözden geçirebilirsiniz:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd yetkilerini**

Merhaba devre sahibinden yetkilerini aşağıdaki örneğine hello kullanarak ekleyebilirsiniz:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete yetkilerini**

Merhaba devre sahibinden revoke/yetkilerini toohello kullanıcı aşağıdaki örneğine hello çalıştırarak silme:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Bağlantı hattı kullanıcı işlemleri

Merhaba hattı kullanıcı hello eş kimliği ve hello devre sahibinden yetkilendirme anahtarından gerekir. Merhaba yetkilendirme anahtarının bir GUID değeridir.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem Bağlantı Yetkilendirme**

Merhaba hattı kullanıcı örnek tooredeem aşağıdaki hello bağlantı yetkilendirme çalıştırabilirsiniz:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease Bağlantı Yetkilendirme**

Bir yetkilendirme hello ExpressRoute bağlantı hattı toohello sanal ağ bağlantıları hello bağlantı silerek serbest bırakabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
