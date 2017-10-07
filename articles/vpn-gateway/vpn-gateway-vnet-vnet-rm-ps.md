---
title: "Bir Azure sanal ağı tooanother VNet bağlanın: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak sanal ağları birbirine bağlama konusu incelenmektedir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>PowerShell kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma

Bu makale size nasıl gösterir toocreate sanal ağlar arasında bir VPN ağ geçidi bağlantısı. Merhaba sanal ağları olabilir hello aynı ya da farklı bölgelerde ve gelen aynı hello ya da farklı Aboneliklerde. Bağlanan sanal ağlar farklı aboneliklerden hello abonelikleri ile ilişkili toobe gerekmediğinde aynı Active Directory Kiracı hello. 

Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulanır ve PowerShell kullanın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Farklı dağıtım modellerini bağlama - Azure portalı](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Farklı dağıtım modellerini bağlama - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın. Sanal ağlar hello varsa aynı bölgede VNet eşlemesi kullanarak bunları bağlanma tooconsider isteyebilir. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).

Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir. Hello Aşağıdaki diyagramda gösterildiği gibi arası sanal ağ bağlantısı ile şirket içi bağlantılar birleştiren ağ topolojileri kurabilmenize olanak sağlar:

![Bağlantılar hakkında](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Sanal ağları neden bağlamalıyız?

Aşağıdaki nedenlerden Merhaba tooconnect sanal ağlar isteyebilirsiniz:

* **Çapraz bölge coğrafi artıklığı ve coğrafi-durum**

  * Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.
  * Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz. Bir önemli SQL Always On kullanılabilirlik grupları: birden fazla Azure bölgesine yayılan ile yukarı tooset örnektir.
* **Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**

  * İçinde hello aynı bölge tooisolation ya da yönetim gereksinimleri birbirlerine bağlı birden çok sanal ağ ile çok katmanlı uygulamalar ayarlayabilirsiniz.

VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda.

## <a name="which-set-of-steps-should-i-use"></a>Hangi adımları tamamlamalıyım? 

Bu makalede iki farklı adım kümesi görürsünüz. Adımlar için bir dizi [içinde bulunan sanal ağlar aynı abonelik hello](#samesub), diğeri [farklı Aboneliklerde bulunan sanal ağlar](#difsub). Merhaba anahtar hello kümeleri arasında olup olmadığını oluşturabilir ve hello içindeki tüm sanal ağ ve ağ geçidi kaynaklarını yapılandırma farktır aynı PowerShell oturumunda.

Merhaba bu makaledeki adımları hello her bölümün başında bildirilen değişkenlerini kullanın. Varolan sanal ağlar ile çalışıyorsanız, kendi ortamınızdaki hello değişkenleri tooreflect hello ayarlarını değiştirin. Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>Nasıl tooconnect sanal ağlar olan hello aynı abonelik

![v2v diyagramı](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Başlamadan önce

Başlamadan önce tooinstall hello en son sürümünü hello Azure Resource Manager PowerShell cmdlet'leri, en az 4.0 veya sonraki sürümü gerekir. Merhaba PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

### <a name="Step1"></a>1. adım -, IP adres aralıklarını planlama

Aşağıdaki adımları hello, kullanıcıların kendi ağ geçidi alt ağları ve yapılandırmalarıyla birlikte iki sanal ağ oluşturun. Ardından hello arasında bir VPN bağlantısı iki Vnet oluşturuyoruz. Önemli tooplan başlangıç IP adresi aralıklarını ağ yapılandırmanızı olur. Sanal ağ aralıklarınızın ya da yerel ağ aralıklarınızın hiçbir şekilde çakışmadığından emin olmalısınız. Bu örneklerde bir DNS sunucusu eklemiyoruz. Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Merhaba örnekleri değerleri aşağıdaki hello kullanırız:

**Değerler TestVNet1 için:**

* VNet Name: TestVNet1
* Resource Group: TestRG1
* Location: East US
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Public IP: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Değerler TestVNet4 için:**

* VNet Name: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Resource Group: TestRG4
* Location: West US
* GatewayName: VNet4GW
* Public IP: VNet4GWIP
* VPNType: RouteBased
* Connection: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Adım 2 - oluşturma ve TestVNet1 yapılandırma

1. Değişkenlerinizi bildirin. Bu örnekte bu alıştırmada hello değerleri kullanarak hello değişkenler bildirilmektedir. Çoğu durumda, hello değerleri kendinizinkilerle değiştirmeniz gerekir. Ancak, hello adımları toobecome yapılandırma bu tür tanıdık aracılığıyla çalıştırıyorsanız, bu değişkenleri kullanabilirsiniz. Gerekirse, hello değişkenleri değiştirin, sonra kopyalayın ve PowerShell konsolunuza yapıştırın.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Tooyour hesabı bağlayın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

  ```powershell
  Login-AzureRmAccount
  ```

  Merhaba hesabının Hello abonelikleri kontrol edin.

  ```powershell
  Get-AzureRmSubscription
  ```

  Merhaba abonelik toouse istediğinizi belirtin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Yeni bir kaynak grubu oluşturun.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. TestVNet1 için alt ağ yapılandırmaları Hello oluşturun. Bu örnekte TestVNet1 adlı bir sanal ağ ve üç alt ağ oluşturulmaktadır. Biri GatewaySubnet, biri FrontEnd, diğeri BackEnd’dir. Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır. Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.

  Merhaba aşağıdaki örnek daha önce belirlediğiniz hello değişkenleri kullanır. Bu örnekte, hello ağ geçidi alt ağı/27 kullanmaktadır. Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, en az/28 veya /27 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz. Bu, gelecekteki hello isteyebileceğiniz yeterli adresleri tooaccommodate olası ek yapılandırmalar için izin verir.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. TestVNet1’i oluşturun.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Ağınız için oluşturacağınız bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği. Bu hello AllocationMethod dinamik olduğuna dikkat edin. Başlangıç IP adresi toouse istediğiniz belirtemezsiniz. Dinamik olarak ayrılan tooyour geçididir. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Merhaba ağ geçidi yapılandırmasını oluşturun. Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar. Merhaba örnek toocreate, ağ geçidi yapılandırmasını kullanın.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. TestVNet1 için Hello ağ geçidi oluşturun. Bu adımda TestVNet1'iniz için hello sanal ağ geçidi oluşturun. Sanal Ağdan Sanal Ağa yapılandırmaları, RouteBased bir VPNType gerektirir. Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello seçilen ağ geçidi SKU'su bağlı olarak genellikle alabilir.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>3. Adım - TestVNet4’ü oluşturma ve yapılandırma

TestVNet1 yapılandırıldıktan sonra TestVNet4’ü oluşturun. Aşağıda, hello değerleri gerektiğinde kendi dosyanızı değiştirerek hello adımları izleyin. Bu adım hello içinde aynı yapılabilir PowerShell oturumu olduğundan hello aynı abonelik.

1. Değişkenlerinizi bildirin. Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Yeni bir kaynak grubu oluşturun.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Merhaba TestVNet4 için alt ağ yapılandırmaları oluşturun.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. TestVNet4’ü oluşturun.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Genel bir IP adresi isteyin.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Merhaba ağ geçidi yapılandırmasını oluşturun.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Merhaba TestVNet4 ağ geçidi oluşturun. Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello seçilen ağ geçidi SKU'su bağlı olarak genellikle alabilir.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>4. adım - hello bağlantıları oluşturma

1. Her iki sanal ağ geçidini de alın. Merhaba ağ geçitleri her ikisi de hello olduğunda aynı abonelik hello örnekte olduğu gibi hello Bu adımda tamamlayabilirsiniz aynı PowerShell oturumunda.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun. Bu adımda TestVNet1 tooTestVNet4 hello bağlantı oluşturun. Merhaba örneklerde paylaşılan bir anahtar göreceksiniz. Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz. Merhaba hello paylaşılan anahtara şeydir önemli hem bağlantılarında eşleşmesi gerekir. Bağlantı oluşturma toocomplete sırasında kısa sürebilir.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun. TestVNet4 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır. Merhaba paylaşılan anahtarların eşleştiğinden emin olun. birkaç dakika sonra Hello bağlantı kurulur.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Bağlantınızı doğrulayın. Merhaba bölümüne bakın [nasıl tooverify bağlantınızı](#verify).

## <a name="difsub"></a>Nasıl farklı Aboneliklerde bulunuyor tooconnect sanal ağlar

![v2v diyagramı](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

Bu senaryoda TestVNet1 ve TestVNet5 bağlanır. TestVNet1 ve TestVNet5 farklı bir abonelikte bulunur. Merhaba abonelikleri hello ile ilişkili toobe gerek yoktur aynı Active Directory kiracısı. Merhaba bu adımları hello önceki kümesi arasındaki bazı hello yapılandırma adımlarını hello hello ikinci abonelik bağlamında ayrı bir PowerShell oturumunda gerçekleştirilen toobe gerektiğini farktır. Özellikle zaman hello iki abonelikleri toodifferent kuruluşların ait.

### <a name="step-5---create-and-configure-testvnet1"></a>5. Adım - TestVNet1'i oluşturma ve yapılandırma

Tamamlamanız gereken [1. adım](#Step1) ve [2. adım](#Step2) hello önceki gelen bölüm toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi için TestVNet1 hello. Oluşturursanız, bu adımlara devam çakışmamasını rağmen bu yapılandırma için gerekli toocreate TestVNet4 hello önceki bölümden değildir. Adım 1 ve 2. adım tamamlandığında, adım 6 toocreate TestVNet5 devam edin. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>6. adım - başlangıç IP adresi aralıklarını doğrulama

Önemli toomake hello IP adres alanı hello yeni sanal ağın TestVNet5 hiçbirini aralıklarınız veya yerel ağ geçidi aralıkları ile çakışmaması emin olur. Bu örnekte, hello sanal ağlar toodifferent kuruluşlara ait olabilir. Bu alıştırmada, hello TestVNet5 için değerler aşağıdaki hello kullanabilirsiniz:

**Değerler TestVNet5 için:**

* VNet Name: TestVNet5
* Resource Group: TestRG5
* Location: Japan East
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Public IP: VNet5GWIP
* VPNType: RouteBased
* Connection: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>7. Adım - TestVNet5'i oluşturma ve yapılandırma

Bu adım hello hello yeni abonelik bağlamında yapılmalıdır. Bu bölümü hello aboneliğin sahibi olan farklı bir kuruluşta hello Yöneticisi tarafından gerçekleştirilebilir.

1. Değişkenlerinizi bildirin. Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Toosubscription 5 bağlayın. PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

  ```powershell
  Login-AzureRmAccount
  ```

  Merhaba hesabının Hello abonelikleri kontrol edin.

  ```powershell
  Get-AzureRmSubscription
  ```

  Merhaba abonelik toouse istediğinizi belirtin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Yeni bir kaynak grubu oluşturun.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Merhaba TestVNet5 için alt ağ yapılandırmaları oluşturun.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. TestVNet5’i oluşturun.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Genel bir IP adresi isteyin.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Merhaba ağ geçidi yapılandırmasını oluşturun.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Merhaba TestVNet5 ağ geçidi oluşturun.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>8. adım - hello bağlantıları oluşturma

Merhaba ağ geçitleri hello farklı Aboneliklerde olduğundan bu örnekte, biz bu adımı iki PowerShell oturumuna [abonelik 1] ve [5. abonelik] bölme.

1. **[1. abonelik]**  Get hello sanal ağ geçidi için abonelik 1. Oturum açın ve aşağıdaki örneğine hello çalıştırmadan önce tooSubscription 1 bağlanın:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Öğeleri aşağıdaki hello Hello çıktısını kopyalayın ve 5. abonelik bu toohello yönetici e-posta veya başka bir yöntemle gönderin.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Bu iki öğenin değerleri benzer toohello örnek çıktı şu olacaktır:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[5. abonelik]**  Get hello sanal ağ geçidi 5. abonelik için. Oturum açın ve aşağıdaki örneğine hello çalıştırmadan önce tooSubscription 5 bağlanın:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Öğeleri aşağıdaki hello Hello çıktısını kopyalayın ve bu abonelik 1 toohello yönetici e-posta veya başka bir yöntem gönderin.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Bu iki öğenin değerleri benzer toohello örnek çıktı şu olacaktır:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[1. abonelik]**  Hello TestVNet1 tooTestVNet5 bağlantı oluşturun. Bu adımda TestVNet1 tooTestVNet5 hello bağlantı oluşturun. Burada Hello fark, farklı bir abonelikte olduğundan bu $ vnet5gw'un doğrudan alınamıyor olmasıdır. 1. abonelikten hello Yukarıdaki adımlarda iletilen hello değerlerle yeni bir PowerShell nesnesi toocreate gerekir. Aşağıdaki Hello örneği kullanın. Merhaba adı, kimliği ve paylaşılan anahtar kendi değerlerinizle değiştirin. Merhaba hello paylaşılan anahtara şeydir önemli hem bağlantılarında eşleşmesi gerekir. Bağlantı oluşturma toocomplete sırasında kısa sürebilir.

  Aşağıdaki örnek hello çalıştırmadan önce tooSubscription 1 Bağlan:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[5. abonelik]**  Hello TestVNet5 tooTestVNet1 bağlantı oluşturun. Bu adım, TestVNet5 tooTestVNet1 hello bağlantı oluşturma dışında benzer toohello biri yukarıdaki aynıdır. Merhaba, 1. abonelikten elde hello değerlere göre bir PowerShell nesnesi oluşturma aynı işlemi burada da geçerlidir. Bu adımda, hello paylaşılan anahtarların eşleştiğinden emin olun.

  Aşağıdaki örnek hello çalıştırmadan önce tooSubscription 5 Bağlan:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Nasıl tooverify bağlantı

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

* Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Merhaba bkz [Virtual Machines belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) daha fazla bilgi için.
* BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
