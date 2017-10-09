---
title: "Klasik sanal ağlar tooAzure Resource Manager sanal ağlara bağlanma: PowerShell | Microsoft Docs"
description: "Bilgi nasıl toocreate Klasik sanal ağlar ve Resource Manager VPN ağ geçidi ve PowerShell kullanarak sanal ağlar arasında bir VPN bağlantısı"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>PowerShell kullanarak farklı dağıtım modellerindeki sanal ağları birbirine bağlama



Bu makale size nasıl tooconnect Klasik sanal ağlar tooResource Yöneticisi sanal ağlar tooallow hello hello ayrı dağıtım modelleri toocommunicate birbirleriyle bulunan kaynakları gösterir. Hello adımları bu makalede PowerShell kullanın ancak bu listeden hello makale seçerek hello Azure portal kullanarak bu yapılandırmayı da oluşturabilirsiniz.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Resource Manager Vnet'i klasik bir VNet tooa bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın. Farklı Aboneliklerde ve farklı bölgelerdeki sanal ağlar arasında bir bağlantı oluşturabilirsiniz. Dinamik ya da rota tabanlı ile yapılandırıldığını hello ağ geçidi olduğu sürece bağlantıları tooon içi ağlar, zaten sanal ağlar da bağlanabilirsiniz. VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda. 

Sanal ağlar hello varsa aynı bölgede isteyebilir tooinstead VNet eşlemesi kullanarak bunları bağlanma göz önünde bulundurun. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Başlamadan önce

Merhaba aşağıdaki adımları hello ayarları gerekli tooconfigure, dinamik ya da rota tabanlı ağ geçidi her sanal ağ için yol ve hello ağ geçitleri arasında bir VPN bağlantısı oluşturun. Bu yapılandırma, statik veya ilke tabanlı ağ geçitleri desteklemez.

### <a name="prerequisites"></a>Ön koşullar

* Her iki Vnet'in zaten oluşturulmuş.
* hello ağ geçitleri bağlı olabilir diğer bağlantılar için hello aralıklardan herhangi biriyle başlangıç adresi aralığı sanal ağlar değil birbirleri ile üst üste veya üst üste hello için.
* Merhaba son PowerShell cmdlet'leri yüklediniz. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için. Merhaba Hizmet Yönetimi (SM) ve Kaynak Yöneticisi (RM) cmdlet'leri hello yüklediğinizden emin olun. 

### <a name="exampleref"></a>Örnek ayarlar

Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.

**Klasik VNet ayarları**

Sanal ağ adı ClassicVNet = <br>
Konum Batı ABD = <br>
Sanal ağ adres alanları 10.0.0.0/24 = <br>
Alt ağ 1 10.0.0.0/27 = <br>
GatewaySubnet 10.0.0.32/29 = <br>
Yerel ağ adı RMVNetLocal = <br>
GatewayType DynamicRouting =

**Resource Manager Vnet'i ayarları**

Sanal ağ adı RMVNet = <br>
Kaynak grubu RG1 = <br>
Sanal ağ IP adresi alanları 192.168.0.0/16 = <br>
Alt ağ 1 192.168.1.0/24 = <br>
GatewaySubnet 192.168.0.0/26 = <br>
Konum Doğu ABD = <br>
Ağ geçidi genel IP adı gwpip = <br>
Yerel ağ geçidi ClassicVNetLocal = <br>
Sanal ağ geçidi adı RMGateway = <br>
Ağ geçidi IP adresleme yapılandırmasını gwipconfig =

## <a name="createsmgw"></a>1. bölüm - yapılandırma Klasik VNet hello
### <a name="part-1---download-your-network-configuration-file"></a>Bölüm 1 - ağ yapılandırma dosyası indirme
1. İçinde tooyour yükseltilmiş haklara sahip Azure hesabı hello PowerShell konsolunda oturum açın. Merhaba aşağıdaki cmdlet'i, hello oturum açma kimlik bilgilerini Azure hesabınız için ister. Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirir. Merhaba SM PowerShell cmdlet'leri toocomplete hello yapılandırmasının bu bölümü kullanın.

  ```powershell
  Add-AzureAccount
  ```
2. Azure ağı yapılandırma dosyanızı hello aşağıdaki komutu çalıştırarak dışa aktarın. Merhaba dosya tooexport tooa farklı konumu gerekirse hello konumunu değiştirebilirsiniz.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Açık hello .xml dosyası tooedit indirilen bu. Merhaba hello ağ yapılandırma dosyası örneği için bkz: [ağ yapılandırma şeması](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Bölüm 2 - hello ağ geçidi alt ağını doğrulayın
Merhaba, **VirtualNetworkSites** öğesi değil zaten oluşturulmuş bir ağ geçidi alt ağı tooyour VNet ekleyin. Merhaba ağ yapılandırma dosyası ile çalışırken, "GatewaySubnet" Merhaba ağ geçidi alt ağı adlı gerekir veya Azure algılar ve bir ağ geçidi alt ağı kullanın.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Örnek:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Bölüm 3 - hello yerel ağ sitesi ekleme
eklediğiniz hello yerel ağ sitesine hello tooconnect istediğiniz RM VNet toowhich temsil eder. Ekleme bir **LocalNetworkSites** zaten yoksa öğe toohello dosyası. Bu noktada hello ağ geçidi hello Resource Manager Vnet'i için oluşturduğumuz henüz yapmadıysanız için hello yapılandırmasında hello VPNGatewayAddress herhangi bir geçerli ortak IP adresi olabilir. Biz hello ağ geçidi oluşturduktan sonra Biz bu yer tutucu IP adresi toohello RM ağ geçidi atanmış hello doğru ortak IP adresiyle değiştirin.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Bölüm 4 - hello yerel ağ sitesi ile ilişkilendirme hello VNet
Bu bölümde, tooconnect istediğiniz hello yerel ağ sitesine belirttiğimiz Vnet'e hello. Bu durumda, hello daha önce başvurulan Resource Manager Vnet'i olur. Eşleşen emin hello adlar kolaylaştırır. Bu adım, bir ağ geçidi oluşturmaz. Ağ geçidi hello hello yerel ağ bağlanacağı belirtir.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>5 Kısım - hello dosyasını kaydedin ve karşıya yükleme
Merhaba dosyasını kaydedin ve ardından hello aşağıdaki komutu çalıştırarak tooAzure alma. Ortamınız için gerektiği gibi hello dosya yolu değiştirdiğinizden emin olun.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Merhaba içeri aktarma başarılı olduğunu gösteren benzer bir sonuç görürsünüz.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Bölüm 6 - hello ağ geçidi oluşturma

Bu örneği çalıştırmadan önce toohello başvurmak bu Azure hello tam adları için yüklediğiniz ağ yapılandırma dosyası toosee bekliyor. Hello ağ yapılandırma dosyası, Klasik sanal ağlar için hello değerler içeriyor. Bazen hello adları Klasik sanal ağlar hello ağ yapılandırma dosyasında Klasik VNet ayarlarında oluştururken değişmesi için Azure portal hello dağıtım modellerini toohello farklılıkları nedeniyle hello. Örneğin, hello Klasik VNet 'Klasik VNet' adlı ve 'ClassicRG' adlı bir kaynak grubunda oluşturduğunuz Azure portal toocreate kullandıysanız, dönüştürülmüş too'Group ClassicRG Klasik VNet hello ağ yapılandırma dosyasında yer alan hello adı. '. Boşluk içeren bir VNet Hello adı belirtirken, hello değeri tırnak işaretleri kullanın.


Aşağıdaki örnek toocreate dinamik yönlendirme ağ geçidi hello kullan:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Hello kullanarak hello hello ağ geçidi durumunu kontrol edebilirsiniz **Get-AzureVNetGateway** cmdlet'i.

## <a name="creatermgw"></a>2. Bölüm: Merhaba RM VNet ağ geçidini yapılandırma
toocreate hello RM VNet için VPN ağ geçidi hello yönergeleri izleyin. Merhaba Klasik sanal ağınızın ağ geçidi için genel IP adresi hello aldıktan sonra hello adımları kadar başlatmayın. 

1. İçinde tooyour Azure hesabı hello PowerShell konsolunda oturum açın. Merhaba aşağıdaki cmdlet'i, hello oturum açma kimlik bilgilerini Azure hesabınız için ister. Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirilir.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Birden fazla aboneliğiniz varsa, Azure aboneliklerinize listesini alın.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Merhaba abonelik toouse istediğinizi belirtin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Bir yerel ağ geçidi oluşturun. Bir sanal ağ hello yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir. Bu durumda, hello yerel ağ geçidi tooyour Klasik VNet anlamına gelir. Olarak Azure tooit başvurun ve ayrıca hello adres alanı ön ekini belirtin bir ad verin. Azure başlangıç IP adresi ön eki hangi trafik toosend tooyour içi konumu tooidentify belirttiğiniz kullanır. Tooadjust hello buradaki bilgiler daha sonra ağ geçidiniz, oluşturmadan önce gerekirse hello değerleri ve çalışma hello örnek yeniden değiştirebilirsiniz.
   
   **-Ad** tooassign toorefer toohello yerel ağ geçidi istediğiniz hello adıdır.<br>
   **-AddressPrefix** hello Klasik VNet adres alanı değil.<br>
   **-Gatewayıpaddress** hello hello Klasik sanal ağınızın ağ geçidinin genel IP adresidir. Tooreflect hello doğru IP adresi toochange hello aşağıdaki örnek emin olun.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Bir ortak IP adresi toobe ayrılmış toohello sanal ağ geçidi hello Resource Manager Vnet'i için istek. Başlangıç IP adresi toouse istediğiniz belirtemezsiniz. Başlangıç IP adresi toohello sanal ağ geçidi dinamik olarak ayrılır. Ancak, bu başlangıç IP adresi değişiklikleri gelmez. ağ geçidi Hello sanal ağ geçidi IP adresi değişiklikleri hello zaman hello yalnızca zaman silindiğinde ve yeniden. Yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında hello ağ geçidi değiştirmez.

  Bu adımda, biz de bir sonraki adımda kullanılan bir değişken ayarlayın.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Sanal ağınızın ağ geçidi alt ağı olduğunu doğrulayın. Hiçbir ağ geçidi alt ağı varsa ekleyin. Merhaba ağ geçidi alt ağı adlandırılan emin olun *GatewaySubnet*.
5. Merhaba aşağıdaki komutu çalıştırarak Hello ağ geçidi için kullanılan hello alt alın. Bu adımda, biz de hello sonraki adımda kullanılan bir değişken toobe ayarlayın.
   
   **-Name** Resource Manager Vnet'i hello adıdır.<br>
   **-ResourceGroupName** hello kaynak grubudur VNet ile ilişkili o hello. Merhaba ağ geçidi alt ağı için bu sanal ağ zaten mevcut olmalıdır ve adlandırılmalıdır *GatewaySubnet* toowork düzgün.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Merhaba ağ geçidi IP adresleme yapılandırmasını oluşturun. Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar. Aşağıdaki örnek toocreate hello ağ geçidi yapılandırmanızı kullanın.

  Bu adımda, hello **- SubnetId** ve **- PublicIpAddressId** parametreleri gerekir bayraklarıdır hello ID özelliği hello alt ağ ve IP adresi nesneleri, sırasıyla. Basit bir dize kullanamazsınız. Bu değişkenler hello adım toorequest bir ortak IP ayarlanır ve adım tooretrieve hello alt hello.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Merhaba aşağıdaki komutu çalıştırarak Hello Resource Manager sanal ağ geçidi oluşturun. Merhaba `-VpnType` olmalıdır *RouteBased*. 45 dakika veya daha fazla hello ağ geçidi toocreate alabilir.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Merhaba VPN ağ geçidi oluşturulduktan sonra hello genel IP adresi kopyalayın. Klasik sanal ağınızı hello yerel ağ ayarlarını yapılandırırken kullanın. Cmdlet tooretrieve hello genel IP adresi aşağıdaki hello kullanabilirsiniz. Merhaba genel IP adresi hello dönüş olarak listelenen *IPADDRESS*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>3. Bölüm: Merhaba Klasik VNet yerel site ayarlarını değiştirme

Bu bölümde, hello ile iş Klasik VNet. Kullanılan tooconnect toohello Resource Manager Vnet'i ağ geçidi olacaktır hello yerel site ayarlarını belirtmek için kullanılan hello yer tutucu IP adresini değiştirin. 

1. Merhaba ağ yapılandırma dosyasını dışarı aktarın.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Bir metin düzenleyicisi kullanarak VPNGatewayAddress için başlangıç değerini değiştirin. Hello ortak IP adresini hello Resource Manager ağ geçidi ile Merhaba yer tutucu IP adresini değiştirin ve ardından hello değişiklikleri kaydedin.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. İçeri aktarma hello ağ yapılandırma dosyası tooAzure değiştirdi.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>4. Bölüm: Merhaba ağ geçitleri arasında bağlantı oluşturma
Merhaba ağ geçitleri arasında bir bağlantı oluşturmak için PowerShell gerekir. Azure hesabı toouse hello Klasik sürümünüz hello PowerShell cmdlet'leri tooadd gerekebilir. Bu nedenle, toodo kullanmak **Add-AzureAccount**.

1. Merhaba PowerShell konsolunda paylaşılan anahtarınız ayarlayın. Toohello başvurmak Hello cmdlet'leri çalıştırmadan önce bu Azure hello tam adları için yüklediğiniz ağ yapılandırma dosyası toosee bekliyor. Boşluk içeren bir VNet Hello adı belirtirken, hello değeri tek tırnak işareti kullanın.<br><br>Aşağıdaki örnekte, **- vnetname adlı** hello hello adıdır Klasik VNet ve **- LocalNetworkSiteName** hello yerel ağ sitesi için belirtilen hello adı. Merhaba **- SharedKey** oluşturmak ve belirten bir değer. Merhaba örnekte 'abc123' kullandık ancak oluşturabilir ve daha karmaşık bir şey kullanın. Burada belirttiğiniz başlangıç değeri şeydir önemli Hello hello aynı bağlantınızı oluştururken hello sonraki adımda belirttiğiniz değeri olmalıdır. Hello dönüş Göster **durumu: başarılı**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Merhaba aşağıdaki komutları çalıştırarak Hello VPN bağlantısı oluşturun:
   
  Merhaba değişkenleri ayarlayın.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Merhaba bağlantı oluşturun. Bu hello fark **- ConnectionType** IPSec, Vnet2Vnet değil.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Bölüm 5: bağlantılarınızı doğrulayın

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>Klasik VNet tooyour Resource Manager Vnet'i tooverify hello bağlantısından

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Azure portalına

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>Resource Manager Vnet'i tooyour tooverify hello bağlantısından Klasik VNet

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Azure portalına

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

