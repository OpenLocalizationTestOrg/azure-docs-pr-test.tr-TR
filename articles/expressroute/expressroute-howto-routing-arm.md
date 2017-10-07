---
title: "Nasıl tooconfigure (eşleme) bir expressroute bağlantı hattı için yönlendirmeyi: Resource Manager: PowerShell: Azure | Microsoft Docs"
description: "Bu makalede, oluşturma ve sağlama hello özel, genel ve Microsoft bir expressroute bağlantı hattı eşlemesi hello adım adım anlatılmaktadır. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Oluşturma ve PowerShell kullanarak bir ExpressRoute bağlantı hattı için eşlemesini değiştirme

Bu makalede, PowerShell kullanarak hello Resource Manager dağıtım modelinde bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur. Ayrıca, hello durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın. Bağlantı hattınız ile toouse farklı yöntem toowork istiyorsanız, bir makale listesi aşağıdaki hello seçin:

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [Video - özel eşliği](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - ortak eşleme](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft eşlemesi](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Yapılandırma önkoşulları

* Hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü hello gerekir. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). 
* Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) hello sayfasında [yönlendirme gereksinimleri](expressroute-routing.md) sayfası ve hello [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfasında.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Merhaba expressroute bağlantı hattı, bu makaledeki toobe mümkün toorun hello cmdlet'leri için sağlanmış ve etkin durumda olması gerekir.

Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.

> [!IMPORTANT]
> Biz hello Hizmet Yönetimi Portalı aracılığıyla hizmet sağlayıcılar tarafından yapılandırılan eşlemeleri şu anda tanıtmıyoruz. Bu özelliği yakında etkinleştirmek için çalışıyoruz. BGP eşlemelerini yapılandırmadan önce hizmet sağlayıcınıza başvurun.
> 
> 

Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz. Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz. Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir. 

## <a name="azure-private-peering"></a>Azure özel eşlemesi

Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.

### <a name="toocreate-azure-private-peering"></a>Azure özel eşleme toocreate

1. ExpressRoute için Hello PowerShell modülünü içeri aktarın.

  Merhaba son PowerShell'i Yükleyiciden yüklemelisiniz [PowerShell Galerisi](http://www.powershellgallery.com/) ve hello ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure Resource Manager modüllerini aktarın. Yönetici olarak toorun PowerShell gerekir.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Tüm hello bilinen semantik sürüm aralığı içinde hello AzureRM.* modüllerini içeri aktarın.

  ```powershell
  Import-AzureRM
  ```

  Ayrıca hello bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Tooyour hesabında oturum açın.

  ```powershell
  Login-AzureRmAccount
  ```

  Toocreate expressroute bağlantı hattı hello aboneliği seçin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. ExpressRoute bağlantı hattı oluşturun.

  Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-arm.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.

  Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.
3. Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun. Aşağıdaki örnek hello kullan:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın. Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:

  * Bir/30 alt ağı hello birincil bağlantı için. Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz. Bu eşleme için özel bir AS numarası kullanabilirsiniz. 65515’i kullanmadığınızdan emin olun.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.

  Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini özel hello kullan:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview Azure özel eşleme ayrıntıları

Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>Azure özel eşleme yapılandırmasını tooupdate

Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz. Bu örnekte, hello hello hattının VLAN kimliği 100 too500 güncelleştiriliyor.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>Azure özel eşleme toodelete

Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:

> [!WARNING]
> Bu örneği çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı hello bağlantısız olduğundan emin olmalısınız. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Azure ortak eşleme

Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.

### <a name="toocreate-azure-public-peering"></a>Azure ortak eşleme toocreate

1. ExpressRoute için Hello PowerShell modülünü içeri aktarın.

  Merhaba son PowerShell'i Yükleyiciden yüklemelisiniz [PowerShell Galerisi](http://www.powershellgallery.com/) ve hello ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure Resource Manager modüllerini aktarın. Yönetici olarak toorun PowerShell gerekir.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Tüm hello bilinen semantik sürüm aralığı içinde hello AzureRM.* modüllerini içeri aktarın.

  ```powershell
  Import-AzureRM
  ```

  Ayrıca hello bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.

  ```powershell
  Import-Module AzureRM.Network
```

  Tooyour hesabında oturum açın.

  ```powershell
  Login-AzureRmAccount
  ```

  Toocreate expressroute bağlantı hattı hello aboneliği seçin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. ExpressRoute bağlantı hattı oluşturun.

  Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-arm.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.

  Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.
3. Sağlanan ve ayrıca etkin hello ExpressRoute bağlantı hattı tooensure denetleyin. Aşağıdaki örnek hello kullan:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın. Devam etmeden önce aşağıdaki bilgilerle hello sahip olduğunuzdan emin olun.

  * Bir/30 alt ağı hello birincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.

  Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini genel hello çalıştırın

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview Azure genel eşliği ayrıntıları

Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>Azure ortak eşleme yapılandırmasını tooupdate

Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz. Bu örnekte, hello hello hattının VLAN kimliği 200 too600 güncelleştiriliyor.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>Azure ortak eşleme toodelete

Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Microsoft eşlemesi

Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme yardımcı olur.

> [!IMPORTANT]
> Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 hello Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur. Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı. Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft eşlemesi

1. ExpressRoute için Hello PowerShell modülünü içeri aktarın.

  Merhaba son PowerShell'i Yükleyiciden yüklemelisiniz [PowerShell Galerisi](http://www.powershellgallery.com/) ve hello ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure Resource Manager modüllerini aktarın. Yönetici olarak toorun PowerShell gerekir.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Tüm hello bilinen semantik sürüm aralığı içinde hello AzureRM.* modüllerini içeri aktarın.

  ```powershell
  Import-AzureRM
  ```

  Ayrıca hello bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Tooyour hesabında oturum açın.

  ```powershell
  Login-AzureRmAccount
  ```

  Toocreate expressroute bağlantı hattı hello aboneliği seçin.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. ExpressRoute bağlantı hattı oluşturun.

  Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-arm.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.

  Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.
3. Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun. Aşağıdaki örnek hello kullan:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Microsoft Hello bağlantı hattı için eşlemesini yapılandırın. Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.

  * Bir/30 alt ağı hello birincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
  * Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın. Yalnızca ortak IP adresi ön ekleri kabul edilir. Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz. Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.
  * **İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekler Tanıtıyorsanız, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.
  * Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.

   Aşağıdaki örnek tooconfigure hattınız için Microsoft eşlemesini hello kullan:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget Microsoft eşleme ayrıntıları

Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft eşleme yapılandırması

Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz:

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft eşlemesi

Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Sonraki adımlar

Sonraki adım, [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md).

* ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).
* Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).
* Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).
