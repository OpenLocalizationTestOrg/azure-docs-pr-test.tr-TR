---
title: "Bir Azure sanal ağı tooanother VNet bağlanın: portalı | Microsoft Docs"
description: "Kaynak Yöneticisi'ni kullanarak sanal ağlar arasında bir VPN ağ geçidi bağlantısı oluşturun ve Azure portal hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Hello Azure portalını kullanarak VNet-VNet VPN ağ geçidi bağlantısı yapılandırma

Bu makale size nasıl gösterir toocreate sanal ağlar arasında bir VPN ağ geçidi bağlantısı. Merhaba sanal ağları olabilir hello aynı ya da farklı bölgelerde ve gelen aynı hello ya da farklı Aboneliklerde. Bağlanan sanal ağlar farklı aboneliklerden hello abonelikleri ile ilişkili toobe gerekmediğinde aynı Active Directory Kiracı hello. 

Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulanır ve hello Azure portalını kullanın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Farklı dağıtım modellerini bağlama - Azure portalı](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Farklı dağıtım modellerini bağlama - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

Sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın. Sanal ağlar hello varsa aynı bölgede VNet eşlemesi kullanarak bunları bağlanma tooconsider isteyebilir. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).

Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir. Hello Aşağıdaki diyagramda gösterildiği gibi arası sanal ağ bağlantısı ile şirket içi bağlantılar birleştiren ağ topolojileri kurabilmenize olanak sağlar:

![Bağlantılar hakkında](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")

### <a name="why-connect-virtual-networks"></a>Sanal ağları neden bağlamalıyız?

Aşağıdaki nedenlerden Merhaba tooconnect sanal ağlar isteyebilirsiniz:

* **Çapraz bölge coğrafi artıklığı ve coğrafi-durum**
  
  * Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.
  * Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz. Bir önemli SQL Always On kullanılabilirlik grupları: birden fazla Azure bölgesine yayılan ile yukarı tooset örnektir.
* **Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**
  
  * İçinde hello aynı bölge tooisolation ya da yönetim gereksinimleri birbirlerine bağlı birden çok sanal ağ ile çok katmanlı uygulamalar ayarlayabilirsiniz.

VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda. Sanal ağlar farklı Aboneliklerde varsa, hello bağlantı hello Portalı'nda oluşturamazsınız unutmayın. [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) veya [CLI](vpn-gateway-howto-vnet-vnet-cli.md) kullanabilirsiniz.

### <a name="values"></a>Örnek ayarlar

Bu adımları bir alıştırma olarak kullanırken, hello örnek ayarlarının değerleri kullanabilirsiniz. Örneklerde her sanal ağ için birden fazla adres alanı kullanılmaktadır. Ancak sanal ağlar arası bağlantı yapılandırmaları için birden fazla adres alanı gerekli değildir.

**Değerler TestVNet1 için:**

* VNet Name: TestVNet1
* Adres alanı: 10.11.0.0/16
  * Alt ağ adı: FrontEnd
  * Alt ağ adres aralığı: 10.11.0.0/24
* Resource Group: TestRG1
* Location: East US
* Adres Alanı: 10.12.0.0/16
  * Alt ağ adı: BackEnd
  * Alt ağ adres aralığı: 10.12.0.0/24
* Ağ geçidi alt ağ adı: GatewaySubnet (Bu işlem otomatik olarak doldurulması hello Portalı'nda)
  * Ağ Geçidi Alt Ağ adres aralığı: 10.11.255.0/27
* DNS sunucusu: DNS sunucunuzun hello IP adresini kullanın
* Sanal Ağ Geçidi Adı: TestVNet1GW
* Gateway Type: VPN
* VPN türü: Rota tabanlı
* SKU: Merhaba toouse istediğiniz ağ geçidi SKU'su seçin
* Genel IP adresi adı: TestVNet1GWIP
* Bağlantı değerleri:
  * Ad: TestVNet1toTestVNet4
  * Paylaşılan anahtar: hello paylaşılan anahtarı kendiniz oluşturabilirsiniz. Bu örnekte abc123 kullanacağız. Merhaba önemli hello sanal ağlar arasında hello bağlantı oluşturduğunuzda, hello değeriyle eşleşmelidir şeydir.

**Değerler TestVNet4 için:**

* VNet Name: TestVNet4
* Adres alanı: 10.41.0.0/16
  * Alt ağ adı: FrontEnd
  * Alt ağ adres aralığı: 10.41.0.0/24
* Resource Group: TestRG1
* Location: West US
* Adres Alanı: 10.42.0.0/16
  * Alt ağ adı: BackEnd
  * Alt ağ adres aralığı: 10.42.0.0/24
* GatewaySubnet ad: GatewaySubnet (Bu işlem otomatik olarak doldurulması hello Portalı'nda)
  * Ağ Geçidi Alt Ağ adres aralığı: 10.41.255.0/27
* DNS sunucusu: DNS sunucunuzun hello IP adresini kullanın
* Sanal Ağ Geçidi Adı: TestVNet4GW
* Gateway Type: VPN
* VPN türü: Rota tabanlı
* SKU: Merhaba toouse istediğiniz ağ geçidi SKU'su seçin
* Genel IP adresi adı: TestVNet4GWIP
* Bağlantı değerleri:
  * Ad: TestVNet4toTestVNet1
  * Paylaşılan anahtar: hello paylaşılan anahtarı kendiniz oluşturabilirsiniz. Bu örnekte abc123 kullanacağız. Merhaba önemli hello sanal ağlar arasında hello bağlantı oluşturduğunuzda, hello değeriyle eşleşmelidir şeydir.

## <a name="CreatVNet"></a>1. TestVNet1’i oluşturma ve yapılandırma
Bir VNet zaten varsa, hello ayarlarının VPN ağ geçidi tasarımınız ile uyumlu olduğunu doğrulayın. Diğer ağlar ile çakışabilen tooany alt ağlar belirli dikkat edin. Çakışan alt ağlarınız varsa bağlantınız düzgün şekilde gerçekleşmeyebilir. Sanal ağınızı hello doğru ayarlarla yapılandırdıysanız, hello hello adımda başlayabilirsiniz [DNS sunucusu belirleme](#dns) bölümü.

### <a name="toocreate-a-virtual-network"></a>toocreate bir sanal ağ
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Ek adres alanı ekleme ve alt ağ oluşturma
Sanal ağınız oluşturulduktan sonra ek adres alanı ekleyebilir ve alt ağ oluşturabilirsiniz.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Ağ geçidi alt ağı oluşturma
Sanal ağ tooa geçidiniz bağlanmadan önce öncelikle toocreate hello ağ geçidi alt ağı gerekir hello sanal ağ toowhich için tooconnect istiyor. Mümkünse, / 28 veya /27 CIDR bloğu sipariş tooprovide kullanarak bir ağ geçidi alt ağı tooaccommodate gelecekteki ek yapılandırma gereksinimlerini yeterli IP adresleri en iyi toocreate olur.

Bu yapılandırmayı bir alıştırma olarak oluşturuyorsanız, toothese başvuran [örnek ayarlar](#values) ağ geçidi alt ağınızı oluştururken.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate bir ağ geçidi alt ağı
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. DNS sunucusu belirtme (isteğe bağlı)
Sanal Ağdan Sanal Ağa bağlantılar için DNS gerekli değildir. Ancak, dağıtılan tooyour sanal ağ için kaynaklar toohave ad çözümlemesi istiyorsanız, bir DNS sunucusunu belirtmeniz gerekir. Bu ayar hello DNS sunucusu, bu sanal ağ için ad çözümlemesi için toouse istediğinizi belirtmenize olanak sağlar. Bir DNS sunucusu oluşturmaz.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Sanal ağ geçidi oluşturma
Bu adımda, ağınız için hello sanal ağ geçidi oluşturun. Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello seçilen ağ geçidi SKU'su bağlı olarak genellikle alabilir. Bu yapılandırmayı bir alıştırma olarak oluşturuyorsanız, toohello başvurabilir [örnek ayarlar](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate bir sanal ağ geçidi
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. TestVNet4’ü oluşturma ve yapılandırma
TestVNet1 yapılandırdıktan sonra TestVNet4 TestVNet4 olanlar hello değerleri değiştirerek hello önceki adımları yineleyerek oluşturun. TestVNet1 için Hello sanal ağ geçidi TestVNet4 yapılandırmadan önce oluşturma tamamlanana kadar toowait gerek yoktur. Kendi değerlerinizi kullanıyorsanız, hello adres alanlarından herhangi biriyle hello tooconnect için istediğiniz sanal ağlar çakışmadığından emin olun.

## <a name="TestVNet1Connection"></a>7. Merhaba TestVNet1 bağlantısını yapılandırın
Merhaba sanal ağ geçitleri için TestVNet1 ve TestVNet4 tamamladıktan sonra sanal ağınızın ağ geçidi bağlantıları oluşturabilirsiniz. Bu bölümde, VNet1 tooVNet4 bir bağlantı oluşturur. Bu adımları yalnızca hello Vnet'lerde aynı işe abonelik. Sanal ağlar farklı Aboneliklerde varsa, PowerShell toomake hello bağlantı kullanmanız gerekir. Merhaba bkz [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) makalesi.

1. İçinde **tüm kaynakları**, ağınız için toohello sanal ağ geçidi gidin. Örnek: **TestVNet1GW**. Tıklatın **TestVNet1GW** tooopen hello sanal ağ geçidi dikey.
   
    ![Bağlantılar dikey penceresi](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")
2. Tıklatın **+ Ekle** tooopen hello **Bağlantı Ekle** dikey.
3. Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde hello ad alanına bağlantınız için bir ad yazın. Örnek: **TestVNet1toTestVNet4**.
   
    ![Bağlantı adı](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")
4. **Bağlantı türü** için. seçin **VNet-VNet** gelen hello açılır.
5. Merhaba **ilk sanal ağ geçidi** alan değeri otomatik olarak doldurulur çünkü bu bağlantının hello belirtilen sanal ağ geçidinden oluşturuluyor.
6. Merhaba **ikinci sanal ağ geçidi** alandır hello VNet hello sanal ağ ağ geçidi bağlantı toocreate istiyor. Tıklatın **başka bir sanal ağ geçidi seçin** tooopen hello **Seç sanal ağ geçidi** dikey.
   
    ![Bağlantı ekleme](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")
7. Bu dikey pencerede listelenen hello sanal ağ geçitlerini görünümü. Yalnızca aboneliğinizdeki sanal ağ geçitleri listelenir. Aboneliğinizde değil tooconnect tooa sanal ağ geçidi istiyorsanız, lütfen hello kullanın [PowerShell makale](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Tooconnect için istediğiniz hello sanal ağ geçidi'ı tıklatın.
9. Merhaba, **paylaşılan anahtarı** alan, bağlantınız için bir paylaşılan anahtar girin. Bu anahtarı kendiniz üretebilir veya oluşturabilirsiniz. Bir siteden siteye bağlantı kullandığınız hello anahtar olması tam olarak Merhaba, şirket içi cihaz ve sanal ağ geçidi bağlantısı için aynı. Merhaba kavram benzer burada; tek fark bağlanan tooa VPN cihazı yerine tooanother sanal ağ geçidi bağlanan.
   
    ![Paylaşılan anahtar](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")
10. Tıklatın **Tamam** sırasında değişikliklerinizi hello dikey toosave alt hello.

## <a name="TestVNet4Connection"></a>8. Merhaba TestVNet4 bağlantısını yapılandırın
Ardından, TestVNet4 tooTestVNet1 bir bağlantı oluşturun. Kullanım hello aynı TestVNet1 tooTestVNet4 toocreate hello bağlantısından kullanılan yöntem. Merhaba kullandığınızdan emin olun aynı paylaşılan anahtar.

## <a name="VerifyConnection"></a>9. Bağlantınızı doğrulama
Merhaba bağlantısı doğrulayın. Her sanal ağ geçidi için aşağıdaki hello:

1. Merhaba dikey penceresinde hello sanal ağ geçidi için bulun. Örnek: **TestVNet4GW**. 
2. Merhaba sanal ağ geçidi dikey penceresinde **bağlantıları** tooview hello bağlantıları dikey hello sanal ağ geçidi için.

Merhaba bağlantılarını görüntülemek ve hello durumunu doğrulayın. Merhaba bağlantısı oluşturulduktan sonra göreceğiniz **başarılı** ve **bağlı** durum değerleri hello gibi.

![Başarılı](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")

Her bağlantı ayrı ayrı çift tıklayarak tooview hello bağlantı hakkında daha fazla bilgi.

![Temel Parçalar](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS
VNet-VNet bağlantıları hakkında ek bilgi için SSS Hello ayrıntılarını görüntüleyin.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Merhaba bkz [Virtual Machines belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) daha fazla bilgi için.
