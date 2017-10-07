---
title: "Zorlamalı tünel Azure siteden siteye bağlantıları için yapılandırın: Klasik | Microsoft Docs"
description: "Nasıl tooredirect veya 'force' tüm Internet'e bağlı trafik geri tooyour konumu şirket içi."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Zorlamalı tünel kullanarak yapılandırma hello Klasik dağıtım modeli

Yeniden yönlendirme veya "tüm Internet'e bağlı trafik geri tooyour şirket içi konumu denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla zorla" sağlar tünel zorlandı. Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri. Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden azure'da her zaman toohello Internet hello seçeneği tooallow olmadan çıkışı doğrudan Azure ağ altyapısından, tooinspect ya da Denetim hello trafik dizinlere. Yetkisiz Internet erişimine olası tooinformation açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Bu makalede zorlamalı tünel hello Klasik dağıtım modeli kullanılarak oluşturulmuş sanal ağlar için nasıl yapılandıracağınız anlatılmaktadır. Zorlamalı tünel, değil hello Portalı aracılığıyla PowerShell kullanarak yapılandırılabilir. Zorlanan hello Resource Manager dağıtım modeli için tünel tooconfigure istiyorsanız, Klasik makale açılır listeden aşağıdaki hello seçin:

> [!div class="op_single_selector"]
> * [PowerShell - Klasik](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Gereksinimleri ve konular
Zorlamalı tünel Azure'da sanal ağ kullanıcı tanımlı yolları (UDR) yapılandırılır. Yeniden yönlendirme trafiği tooan site varsayılan yol toohello Azure VPN ağ geçidi olarak ifade edilir şirket içi. Merhaba aşağıdaki bölümde bir Azure sanal ağı hello yönlendirme tablosuna ve yollar sınırlama geçerli hello listelenmektedir:

* Her sanal ağ alt yerleşik sistem yönlendirme tablosu vardır. Merhaba sistem yönlendirme tablosu aşağıdaki üç grup yolların hello sahiptir:

  * **Yerel VNet yollar:** doğrudan toohello hedef VM'ler hello aynı sanal ağ.
  * **Şirket içi yollar:** toohello Azure VPN ağ geçidi.
  * **Varsayılan yol:** doğrudan toohello Internet. Merhaba önceki iki yolları tarafından kapsanmayan hedefleyen paketler toohello özel IP adresleri bırakılır.
* Kullanıcı tanımlı yolların Hello sürümle birlikte, varsayılan yol yönlendirme tablosu tooadd oluşturun ve bu alt ağlardaki tünel zorunlu hello yönlendirme tablosu tooyour sanal ağ alt ağı tooenable ilişkilendirin.
* Tooset "varsayılan site" Merhaba şirket içi yerel siteleri bağlı toohello sanal ağ arasında gerekir.
* Zorlamalı tünel dinamik yönlendirme VPN ağ geçidi (olmayan bir statik ağ geçidi) sahip bir sanal ağ ile ilişkilendirilmiş olması gerekir.
* Zorlanan tünel ExpressRoute bu düzenek yapılandırılmamış, ancak bunun yerine, varsayılan rota hello ExpressRoute BGP üzerinden reklam tarafından etkinleştirilmiş eşliği oturumlarını. Lütfen hello bakın [ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/) daha fazla bilgi için.

## <a name="configuration-overview"></a>Yapılandırmasına genel bakış
Aşağıdaki örneğine hello hello ön uç alt ağı değil zorlamalı tünel. Merhaba ön uç alt Hello iş yüklerini tooaccept devam et ve toocustomer isteklerini doğrudan Internet hello yanıt. Merhaba Orta katmanda ve arka uç alt zorlanır tünel. Bu iki alt toohello Internet tüm giden bağlantılar zorlanmış ya da yeniden yönlendirilen geri tooan şirket içi site S2S VPN tünelleri hello biri aracılığıyla olacaktır.

Bu toorestrict sağlar ve Internet erişimi, sanal makinelerden inceleme veya çok katmanlı bir hizmet Mimarinizi gerekli tooenable devam ederken, azure'daki hizmetlere bulut. Sanal ağlarınıza hiçbir Internet'e iş yükleri varsa zorlamalı tünel toohello tüm sanal ağların de uygulayabilirsiniz.

![Zorlamalı Tünel Oluşturma](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Başlamadan önce
Aşağıdaki başlangıç yapılandırması önce öğelerindeki hello sahip olduğunuzu doğrulayın.

* Azure aboneliği. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Yapılandırılmış bir sanal ağ. 
* en son sürümünü hello Azure PowerShell cmdlet'lerini Hello. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.

## <a name="configure-forced-tunneling"></a>Zorlamalı tünel yapılandırma
Aşağıdaki yordamı hello için bir sanal ağ zorlamalı tünel belirtmenize yardımcı olur. Merhaba yapılandırma adımları toohello VNet ağ yapılandırma dosyası karşılık gelir.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

Bu örnekte, hello sanal ağ 'MultiTier-VNet' üç alt ağa sahip değil: 'Ön uç', 'Midtier' ve 'Backend' alt ağlar, dört şirket içi ve dışı bağlantılar: 'DefaultSiteHQ' ve üç dalları. 

Merhaba adımları hello 'DefaultSiteHQ' hello varsayılan site bağlantısı zorlamalı tünel olarak ayarlayın ve zorlanan tünel hello Midtier ve arka uç alt ağlar toouse yapılandırın.

1. Bir yönlendirme tablosu oluşturun. Cmdlet toocreate aşağıdaki hello yol tablosu kullanın.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Varsayılan rota toohello yönlendirme tablosu ekleyin. 

  Merhaba aşağıdaki örnek 1. adımda oluşturduğunuz bir varsayılan rota toohello yönlendirme tablosuna ekler. Yalnızca desteklenen rota hello Not "0.0.0.0/0" toohello "VPNGateway" NextHop hello hedef öneki ' dir.

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Merhaba yönlendirme tablosu toohello alt ağları ilişkilendirin. 

  Bir yönlendirme tablosu oluşturulur ve bir yol eklenir sonra örnek tooadd aşağıdaki hello kullanın veya hello rota tablosu tooa sanal ağ alt ağını ilişkilendirin. Merhaba örnek hello rota tablosu "MyRouteTable" toohello Midtier ve arka uç alt ağlar VNet MultiTier-VNet ekler.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Varsayılan site zorlanan tünel için atayın. 

  Adım önceki hello hello örnek cmdlet komutlar yönlendirme tablosunu hello oluşturulan ve hello rota tablosu tootwo hello sanal ağların ilişkili. Merhaba kalan tooselect bir yerel site hello çok siteli bağlantıları hello varsayılan siteyle veya tünel hello sanal ağ arasında bir adımdır.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Ek PowerShell cmdlet'leri
### <a name="toodelete-a-route-table"></a>toodelete bir yol tablosu

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist bir yol tablosu

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete giden bir yol tablosu bir yolu

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove bir alt ağdaki bir yol

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>bir alt ağla ilişkili toolist hello yol tablosu

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>bir sanal ağ VPN ağ geçidi varsayılan sitesinden tooremove

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```