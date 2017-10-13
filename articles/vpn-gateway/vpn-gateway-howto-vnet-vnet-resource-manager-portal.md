---
title: "Bir Azure sanal ağını başka bir sanal ağa bağlama: Portal | Microsoft Docs"
description: "Resource Manager ve Azure portalı kullanarak sanal ağlar arasında VPN ağ geçidi bağlantısı oluşturun."
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
ms.openlocfilehash: cbbae06d4e5774d5fdf7bcce65dc7efddaa5f280
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-the-azure-portal"></a>Azure portalı kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma

Bu makalede, sanal ağlar arasında VPN ağ geçidi bağlantısının nasıl oluşturulduğu gösterilir. Sanal ağlar aynı ya da farklı bölgelerde ve aynı ya da farklı aboneliklerde bulunuyor olabilirler. Farklı aboneliklerden sanal ağları bağlarken aboneliklerin aynı Active Directory kiracısıyla ilişkilendirilmiş olması gerekmez. 

Bu makaledeki adımlar Resource Manager dağıtım modeli için geçerlidir ve Azure portalını kullanır. Ayrıca aşağıdaki listeden farklı bir seçenek belirtip farklı bir dağıtım aracı veya dağıtım modeli kullanarak da bu yapılandırmayı oluşturabilirsiniz:

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

Bir sanal ağı başka bir sanal ağa bağlamak (VNet'ten VNet'e), bir VNet'i şirket içi site konumuna bağlamakla aynıdır. Her iki bağlantı türü de IPsec/IKE kullanarak güvenli bir tünel sunmak üzere bir VPN ağ geçidi kullanır. VNet’leriniz aynı bölgedeyse VNet Eşlemesi kullanarak bağlamayı düşünebilirsiniz. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).

Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir. Bunun yapılması aşağıdaki diyagramda da görüldüğü gibi şirket içi ve şirket dışı bağlantıyla sanal ağ içi bağlantıyı birleştiren ağ topolojileri kurabilmenize olanak sağlar:

![Bağlantılar hakkında](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")

### <a name="why-connect-virtual-networks"></a>Sanal ağları neden bağlamalıyız?

Sanal ağları aşağıdaki sebeplerden dolayı bağlamak isteyebilirsiniz:

* **Çapraz bölge coğrafi artıklığı ve coğrafi-durum**
  
  * Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.
  * Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz. Buna önemli bir örnek olarak SQL Always On ile birden fazla Azure bölgesine yayılan Kullanılabilirlik Grupları’nı birlikte kurmak verilebilir.
* **Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**
  
  * Yalıtım ve yönetim gereksinimlerinden dolayı aynı bölge içinde birbirlerine bağlı birden fazla sanal ağ ile çok katmanlı uygulamalar kurabilirsiniz.

Sanal ağlar arası bağlantılar hakkında daha fazla bilgi için bu makalenin sonunda yer alan [Sanal ağlar arası bağlantılar hakkında SSS](#faq) bölümünü inceleyin. Sanal ağlarınız farklı aboneliklerdeyse, portalda bağlantı oluşturamazsınız. [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) veya [CLI](vpn-gateway-howto-vnet-vnet-cli.md) kullanabilirsiniz.

### <a name="values"></a>Örnek ayarlar

Bu adımları bir alıştırma olarak kullanırken, örnek ayar değerlerini kullanabilirsiniz. Örneklerde her sanal ağ için birden fazla adres alanı kullanılmaktadır. Ancak sanal ağlar arası bağlantı yapılandırmaları için birden fazla adres alanı gerekli değildir.

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
* Ağ Geçidi Alt Ağ adı: GatewaySubnet (bu alan portalda otomatik doldurulacaktır)
  * Ağ Geçidi Alt Ağ adres aralığı: 10.11.255.0/27
* DNS Sunucusu: DNS sunucunuzun IP adresini kullanın
* Sanal Ağ Geçidi Adı: TestVNet1GW
* Gateway Type: VPN
* VPN türü: Rota tabanlı
* SKU: Kullanmak istediğiniz Ağ Geçidi SKU’sunu seçin
* Genel IP adresi adı: TestVNet1GWIP
* Bağlantı değerleri:
  * Ad: TestVNet1toTestVNet4
  * Paylaşılan anahtar: Paylaşılan anahtarı kendiniz oluşturabilirsiniz. Bu örnekte abc123 kullanacağız. Sanal ağlar arası bağlantı oluştururken önemli olan, iki ağda da aynı değerin kullanılmasıdır.

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
* Ağ Geçidi Alt Ağ adı: GatewaySubnet (bu alan portalda otomatik doldurulacaktır)
  * Ağ Geçidi Alt Ağ adres aralığı: 10.41.255.0/27
* DNS Sunucusu: DNS sunucunuzun IP adresini kullanın
* Sanal Ağ Geçidi Adı: TestVNet4GW
* Gateway Type: VPN
* VPN türü: Rota tabanlı
* SKU: Kullanmak istediğiniz Ağ Geçidi SKU’sunu seçin
* Genel IP adresi adı: TestVNet4GWIP
* Bağlantı değerleri:
  * Ad: TestVNet4toTestVNet1
  * Paylaşılan anahtar: Paylaşılan anahtarı kendiniz oluşturabilirsiniz. Bu örnekte abc123 kullanacağız. Sanal ağlar arası bağlantı oluştururken önemli olan, iki ağda da aynı değerin kullanılmasıdır.

## <a name="CreatVNet"></a>1. TestVNet1’i oluşturma ve yapılandırma
Zaten bir VNet'iniz varsa ayarların VPN ağ geçidi tasarımınızla uyumlu olduğunu doğrulayın. Diğer ağlarla çakışabilecek herhangi bir alt ağ olup olmadığına özellikle dikkat edin. Çakışan alt ağlarınız varsa bağlantınız düzgün şekilde gerçekleşmeyebilir. VNet'iniz doğru ayarlarla yapılandırıldıysa [DNS sunucusu belirtme](#dns) bölümündeki adımları uygulamaya başlayabilirsiniz.

### <a name="to-create-a-virtual-network"></a>Sanal ağ oluşturmak için
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Ek adres alanı ekleme ve alt ağ oluşturma
Sanal ağınız oluşturulduktan sonra ek adres alanı ekleyebilir ve alt ağ oluşturabilirsiniz.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Ağ geçidi alt ağı oluşturma
Sanal ağınızı bir ağ geçidine bağlamadan önce, bağlamak istediğiniz sanal ağ için ağ geçidi alt ağını oluşturmanız gerekir. Mümkünse, gelecekteki ek yapılandırma gereksinimlerini karşılamaya yetecek sayıda IP adresi sağlamak için /28 veya /27 CIDR bloğu kullanılarak ağ geçidi alt ağı oluşturulması idealdir.

Bu yapılandırmayı bir alıştırma olarak oluşturuyorsanız ağ geçidi alt ağınızı oluştururken bu [Örnek ayarlara](#values) başvurun.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="to-create-a-gateway-subnet"></a>Bir ağ geçidi alt ağı oluşturmak için
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. DNS sunucusu belirtme (isteğe bağlı)
Sanal Ağdan Sanal Ağa bağlantılar için DNS gerekli değildir. Ancak, sanal ağınıza dağıtılmış olan kaynaklarınız için ad çözümleme istiyorsanız bir DNS sunucusu belirtmeniz gerekir. Bu ayar, bu sanal ağ için ad çözümlemede kullanmak istediğiniz DNS sunucusunu belirtmenizi sağlar. Bir DNS sunucusu oluşturmaz.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Sanal ağ geçidi oluşturma
Bu adımda sanal ağınız için sanal ağ geçidi oluşturacaksınız. Bir ağ geçidinin oluşturulması, seçili ağ geçidi SKU’suna bağlı olarak 45 dakika veya daha uzun sürebilir. Bu yapılandırmayı bir alıştırma olarak oluşturuyorsanız [Örnek ayarlara](#values) başvurabilirsiniz.

### <a name="to-create-a-virtual-network-gateway"></a>Bir sanal ağ geçidi oluşturmak için
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. TestVNet4’ü oluşturma ve yapılandırma
TestVNet1’i oluşturduktan sonra önceki adımlarda verilen değerleri TestVNet4’ün değerleriyle değiştirip tekrar uygulayarak TestVNet4’ü oluşturun. TestVNet4’ü yapılandırmak için TestVNet1’in sanal ağ geçidi oluşturma işlemlerinin tamamlanmasını beklemenize gerek yoktur. Değerleri kendiniz belirliyorsanız adres alanlarının bağlanmak istediğiniz sanal ağlarınkilerle çakışmadığından emin olun.

## <a name="TestVNet1Connection"></a>7. TestVNet1 bağlantısını yapılandırma
TestVNet1 ve TestVNet4 için sanal ağ geçidi oluşturma işlemleri tamamlandıktan sonra sanal ağ geçidi bağlantılarınızı oluşturabilirsiniz. Bu bölümde VNet1 ile VNet4 arasında bir bağlantı oluşturacaksınız. Bu adımlar yalnızca aynı abonelikteki sanal ağlar için geçerlidir. Sanal ağlar farklı aboneliklerdeyse, bağlantıyı kurmak için PowerShell kullanmanız gerekir. [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) makalesine bakın.

1. **Tüm kaynaklar** bölümünde sanal ağınıza ait sanal ağ geçidini bulun. Örnek: **TestVNet1GW**. Sanal ağ geçidi dikey penceresini açmak için **TestVNet1GW** öğesine tıklayın.
   
    ![Bağlantılar dikey penceresi](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")
2. **+Ekle**’ye tıklayarak **Bağlantı ekle** dikey penceresini açın.
3. **Bağlantı ekle** dikey penceresinin ad alanına bağlantınıza vermek istediğiniz adı yazın. Örnek: **TestVNet1toTestVNet4**.
   
    ![Bağlantı adı](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")
4. **Bağlantı türü** için. Açılır listeden **VNet-VNet**’i seçin.
5. Bu bağlantıyı belirtilen bir sanal ağ geçidinden oluşturduğunuz için **Birinci sanal ağ geçidi** alanı otomatik olarak doldurulur.
6. **İkinci sanal ağ geçidi** alanı, bağlantı oluşturmak istediğiniz hedef sanal ağın sanal ağ geçididir. **Başka bir sanal ağ geçidi seç**’e tıklayarak **Sanal ağ geçidi seç** dikey penceresini açın.
   
    ![Bağlantı ekleme](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")
7. Bu dikey pencerede listelenen sanal ağ geçitlerini görüntüleyin. Yalnızca aboneliğinizdeki sanal ağ geçitleri listelenir. Kendi aboneliğinizde olmayan bir sanal ağ geçidine bağlanmak istiyorsanız lütfen [PowerShell makalesini](vpn-gateway-vnet-vnet-rm-ps.md) kullanın. 
8. Bağlanmak istediğiniz sanal ağ geçidine tıklayın.
9. **Paylaşılan anahtar** alanına bağlantınız için bir paylaşılan anahtar girin. Bu anahtarı kendiniz üretebilir veya oluşturabilirsiniz. Siteler arası bağlantılarda kullanacağınız anahtarın hem şirket içi cihazlarınız hem de sanal ağ geçidi bağlantınız için aynı olması gerekir. Buradaki kavram benzerdir ancak bir VPN cihazına bağlanmak yerine başka bir sanal ağ geçidine bağlanmış olursunuz.
   
    ![Paylaşılan anahtar](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")
10. Değişikliklerinizi kaydetmek için dikey pencerenin en altında yer alan **Tamam**’a tıklayın.

## <a name="TestVNet4Connection"></a>8. TestVNet4 bağlantısını yapılandırma
Bu adımda TestVNet4 ile TestVNet1 arasında bir bağlantı oluşturun. TestVNet1 ile TestVNet4 arasında bağlantı oluşturmak için kullandığınız yöntemi kullanın. Aynı paylaşılan anahtarı kullandığınızdan emin olun.

## <a name="VerifyConnection"></a>9. Bağlantınızı doğrulama
Bağlantınızı doğrulayın. Her sanal ağ geçidi için aşağıdakileri yapın:

1. Sanal ağ geçidine ait dikey pencereyi bulun. Örnek: **TestVNet4GW**. 
2. Sanal ağ geçidi dikey penceresinde **Bağlantılar**’a tıklayarak sanal ağ geçidine ait bağlantılar dikey penceresini görüntüleyin.

Bağlantıları görüntüleyin ve durumlarını doğrulayın. Bağlantı oluşturulduğunda **Başarılı oldu** ve **Bağlandı** Durum değerleri görüntülenir.

![Başarılı](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")

Her bir bağlantıya çift tıklayarak daha fazla bilgi görüntüleyebilirsiniz.

![Temel Parçalar](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS
Sanal ağlar arası bağlantılar hakkında ek bilgi için SSS sayfasını görüntüleyin.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-faq-vnet-vnet-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal ağlarınıza sanal makineler ekleyebilirsiniz. Daha fazla bilgi için bkz. [Virtual Machines belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
