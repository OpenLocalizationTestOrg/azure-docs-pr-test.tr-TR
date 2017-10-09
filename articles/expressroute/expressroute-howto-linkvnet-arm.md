---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: PowerShell: Azure | Microsoft Docs"
description: "Bu belge nasıl hello Resource Manager dağıtım modeli ve PowerShell kullanarak sanal toolink (Vnet'ler) tooExpressRoute devreler ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Sanal ağ tooan expressroute bağlantı hattı Bağlan
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-linkvnet-classic.md)
>

Bu makalede, hello Resource Manager dağıtım modeli ve PowerShell kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute bağlantı hatları bağlama yardımcı olur. Sanal ağlar hello olabilir ya da aynı abonelik veya başka bir abonelik parçası. Bu makalede ayrıca nasıl tooupdate bir sanal ağ bağlantı gösterilmektedir. 

## <a name="before-you-begin"></a>Başlamadan önce
* Merhaba hello Azure PowerShell modüllerinin en son sürümünü yükleyin. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. 
  * Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve bağlantı sağlayıcınız tarafından etkinleştirilmiş hello hattı sahip. 
  * Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun. Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md) yönlendirme yönergeleri için makalenin. 
  * Azure özel eşleme yapılandırılır ve uçtan uca bağlantı etkinleştirebilmeniz için ağınız ve Microsoft arasında hello BGP eşliği yukarı olduğundan emin olun.
  * Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olduğundan emin olun. Çok olarak Hello yönergeleri[ExpressRoute için bir sanal ağ geçidi oluşturmak](expressroute-howto-add-gateway-resource-manager.md). ExpressRoute için bir sanal ağ geçidi hello GatewayType 'ExpressRoute' değil VPN kullanır.

* Too10 sanal ağlar tooa standart expressroute bağlantı hattı bağlayabilirsiniz. Tüm sanal ağları hello olmalıdır standart bir expressroute bağlantı hattını kullanırken aynı coğrafi bölge. 

* Merhaba expressroute bağlantı hattı hello jeopolitik bölge dışında sanal ağlara bağlantı veya çok sayıda sanal ağlar tooyour expressroute bağlantı hattı hello ExpressRoute premium eklentisi etkinse bağlanabilirsiniz. Merhaba denetleyin [SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı
Bir sanal ağ geçidi tooan expressroute bağlantı hattı cmdlet'i aşağıdaki hello kullanarak bağlanabilir. Bu hello sanal ağ geçidi oluşturulur ve hello cmdlet'i çalıştırmadan önce bağlama için hazır olduğundan emin olun:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Farklı bir abonelik tooa hattı sanal bir ağa bağlan
Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz. Aşağıdaki şekilde hello arasında birden çok abonelik basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterir.

Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir. Her hello kuruluşunuz içinde hello bölümlerin kendi aboneliği kullanabilirsiniz dağıtmak için kendi hizmetlerini--ancak tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşabilirsiniz. Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir. Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.

> [!NOTE]
> Bağlantı ve bant genişliği ücretleri hello expressroute bağlantı hattı için uygulanan toohello abonelik sahibi olur. Tüm sanal ağları hello paylaşmak aynı bant genişliği.
> 
> 

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Yönetim - hattı sahipleri ve hattı kullanıcılar

Merhaba 'devre sahibinden' hello ExpressRoute bağlantı hattı kaynak yetkili bir güç kullanıcısıdır. Merhaba devre sahibinden 'hattı kullanıcılar tarafından kullanılan yetkilerini oluşturabilirsiniz. Bağlantı hattı kullanıcılardır sahipleri sanal ağ içinde olmayan ağ geçitleri, expressroute bağlantı hattı hello gibi aynı abonelik hello. Bağlantı hattı kullanıcıların yetkilerini (sanal ağ başına bir yetkilendirme) kullanmak.

Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir. Bir yetkilendirme sonuçlarına tüm bağlantı erişimini iptal edildi hello abonelikten silinmesini iptal ediliyor.

### <a name="circuit-owner-operations"></a>Bağlantı hattı sahibi işlemleri

**toocreate bir yetkilendirme**

Merhaba devre sahibinden bir yetkilendirme oluşturur. Bu olabilir bir yetkilendirme anahtarı hello oluşturulmasında sonuçları kendi sanal ağ ağ geçitleri toohello expressroute bağlantı hattı kullanıcı tooconnect tarafından kullanılır. Bir yetkilendirme yalnızca bir bağlantı için geçerli değil.

cmdlet kod parçacığında gösterildiği nasıl aşağıdaki hello toocreate bir yetkilendirme:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Merhaba yanıt toothis hello yetkilendirme anahtar ve durum içerir:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview yetkilerini**

Merhaba devre sahibinden hello aşağıdaki cmdlet'i çalıştırarak belirli bir bağlantı hattı üzerinde verilen tüm yetkilerini gözden geçirebilirsiniz:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd yetkilerini**

Merhaba devre sahibinden yetkilerini cmdlet'i aşağıdaki hello kullanarak ekleyebilirsiniz:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete yetkilerini**

Merhaba devre sahibinden revoke/yetkilerini toohello kullanıcı hello aşağıdaki cmdlet'i çalıştırarak silme:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Bağlantı hattı kullanıcı işlemleri

Merhaba hattı kullanıcı hello eş kimliği ve hello devre sahibinden yetkilendirme anahtarı gerekir. Merhaba yetkilendirme anahtarının bir GUID değeridir.

Eş Kimliği komutu aşağıdaki hello denetlenebilir:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem Bağlantı Yetkilendirme**

Merhaba hattı kullanıcı cmdlet tooredeem aşağıdaki hello bağlantı yetkilendirme çalıştırabilirsiniz:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease Bağlantı Yetkilendirme**

Bir yetkilendirme hello ExpressRoute bağlantı hattı toohello sanal ağ bağlantıları hello bağlantı silerek serbest bırakabilirsiniz.

## <a name="modify-a-virtual-network-connection"></a>Sanal ağ bağlantısı değiştirme
Belirli bir sanal ağ bağlantısı özellikleri güncelleştirebilirsiniz. 

**tooupdate hello bağlantı ağırlığı**

Sanal ağınıza bağlı toomultiple ExpressRoute bağlantı hatları olabilir. Birden fazla expressroute bağlantı hattı aynı önek hello alabilirsiniz. hangi bağlantı toosend trafiği için bu önek hedefleyen toochoose değiştirebilir *RoutingWeight* bağlantısı. Trafik, yüksek hello ile Merhaba bağlantıda gönderilecek *RoutingWeight*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Merhaba aralığını *RoutingWeight* 0 too32000 değil. Merhaba varsayılan değer 0'dır.

## <a name="next-steps"></a>Sonraki adımlar
ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
