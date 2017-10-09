---
title: "aaaConfigure bir sanal ağ ve ağ geçidi için de ExpressRoute hello Klasik portalı | Microsoft Docs"
description: "Bu makalede hello Klasik dağıtım modeli ve hello Klasik portalı kullanarak ExpressRoute için bir sanal ağ ayarı aracılığıyla anlatılmaktadır."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Merhaba Klasik Portalı'nda ExpressRoute için bir sanal ağ oluşturma
Bu makaledeki adımları Hello hello Klasik dağıtım modeli ve hello Klasik portalı kullanarak ExpressRoute ile bir sanal ağ ve sanal ağ geçidi kullanmak için yapılandırırken size yol gösterir.

Merhaba Resource Manager dağıtım modeli için yönergeler arıyorsanız, aşağıdaki makaleler hello kullanabilirsiniz: [PowerShell kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-ps.md) ve [bir VPN ağ geçidi tooa Resource Manager Vnet'i eklemek için ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Bir Klasik VNet ve ağ geçidi oluşturun
Merhaba aşağıdaki adımları Klasik VNet ve bir sanal ağ geçidi oluşturun. Klasik bir VNet zaten varsa hello bkz [olan bir Klasik VNet yapılandırma](#config) bu makalenin bölümünde.

1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com).
2. Merhaba sol alt köşedeki hello ekranının, tıklatın **yeni**. Merhaba Gezinti bölmesinde **Ağ Hizmetleri**ve ardından **sanal ağ**. Tıklatın **özel Oluştur** toobegin hello Yapılandırma Sihirbazı'nı.
3. Merhaba üzerinde **sanal ağ ayrıntıları** sayfasında, hello aşağıdakileri girin:
   
   * **Ad** – sanal ağınızı adlandırın. Çok karmaşık toomake hello adı isteyebilirsiniz, Vm'leri ve PaaS örnekleri dağıtırken bu sanal ağ adı kullanacaksınız.
   * **Konum** – hello konumdur kaynaklar (VM'ler) tooreside istediğiniz doğrudan ilgili toohello fiziksel konum (bölge). Örneğin, fiziksel olarak Doğu ABD'de bulunan toothis sanal ağ toobe dağıttığınız hello VM'ler istiyorsanız, o konumu seçin. Oluşturduktan sonra sanal ağınızla ilişkili hello bölgeyi değiştiremezsiniz.
4. Merhaba üzerinde **DNS sunucuları ve VPN bağlantısı** sayfasında, aşağıdaki bilgilerle hello girin ve ardından hello hello alt köşedeki İleri okuna tıklayın. 
   
   * **DNS sunucuları** - hello DNS sunucusu adı ve IP adresini girin ya da daha önce kaydedilmiş bir DNS sunucusu hello kısayol menüsünden seçin. Bu ayarla bir DNS sunucusu oluşturulmaz. Bu sanal ağ için ad çözümlemesi için toouse istediğiniz toospecify hello DNS sunucuları sağlar.
   * **Siteden siteye bağlantı** - seçin onay kutusunu hello **siteden siteye VPN bağlantısını yapılandırma**.
   * **ExpressRoute** – seç onay kutusu hello **kullanım ExpressRoute**. Seçtiyseniz bu seçeneği yalnızca görünür **siteden siteye VPN bağlantısını yapılandırma**.
   * **Yerel ağ** -gerekli toohave ExpressRoute için bir yerel ağ sitesi olan. Ancak, bir ExpressRoute bağlantı hello durumda ağ site yok sayılacak hello adres öneklerini hello yerel belirtilmiş. Bunun yerine, hello adres öneklerini tooMicrosoft hello expressroute bağlantı hattı üzerinden yönlendirme amacıyla kullanılacak tanıtılan.<BR>ExpressRoute bağlantınızı için oluşturulan bir yerel ağ zaten varsa, hello aşağı açılır listeden seçebilirsiniz. Aksi takdirde, seçin **yeni bir yerel ağ belirtmek**.
5. Merhaba **siteden siteye bağlantı** hello önceki adımda toospecify yeni bir yerel ağ seçtiyseniz sayfası görüntülenir. tooconfigure, yerel ağınızda bilgisinden hello girin ve ardından hello İleri okuna tıklayın. 
   
   * **Ad** -yerel toocall istediğiniz hello adını (şirket içi) ağ alanı.
   * **Adres alanı** - dahil olmak üzere başlangıç IP'si ve CIDR'si (adres sayısı). Sanal ağınız için hello adres aralığıyla örtüşmeyecek sürece herhangi bir adres aralığı belirtebilirsiniz. Genellikle, bunun şirket içi ağlarınız hello adres aralıklarını belirtebilirsiniz, ancak ExpressRoute hello durumda bu ayarları kullanılmaz. Ancak, bu ayar hello Klasik portal kullanırken sipariş toocreate hello yerel ağ gereklidir.
   * **Adres Alanı Ekle** -Bu ayar için ExpressRoute ilgili değildir.
6. Merhaba üzerinde **sanal ağ adres alanları** sayfasında, aşağıdaki bilgilerle hello girin ve ağınızı hello alt sağ tooconfigure hello onay işaretine'ye tıklayın. 
   
   * **Adres alanı** - başlangıç IP dahil olmak üzere ve adres sayısı. Belirttiğiniz hello adres alanlarından herhangi biri yerel ağınızda sahip hello adres alanları çakışmadığını doğrulayın.
   * **Alt ağ Ekle** - dahil olmak üzere başlangıç IP'si ve adres sayısı. Ek alt ağlar gerekli değildir.
   * **Ağ geçidi alt ağı eklemek** -tooadd hello ağ geçidi alt ağı'ı tıklatın. Merhaba ağ geçidi alt ağı yalnızca hello sanal ağ geçidi için kullanılır ve bu yapılandırma için gereklidir.<BR>ağ geçidi alt ağı CIDR (adres sayısı) ExpressRoute /28 olmalıdır hello veya daha büyük (/ 27, / 26 vb..). Bu, alt ağ tooallow hello yapılandırma toowork yeterli IP adresi sağlar. Hello onay kutusunu toouse ExpressRoute seçtiyseniz hello Klasik Portalı'nda, bir ağ geçidi alt ağı hello portalı ile /28 belirtir.  Merhaba CIDR adres sayısı hello Klasik Portalı'nda ayarlayamazsınız. Merhaba ağ geçidi alt ağı olarak görünür **ağ geçidi** hello Klasik portalında hello oluşturulan hello ağ geçidi alt ağı gerçek adını gerçekten olsa **GatewaySubnet**. Bu ad hello Azure portal veya PowerShell kullanarak görüntüleyebilirsiniz.
7. Tıklatın hello sayfasının hello altındaki onay işaretine hello ve sanal ağınız toocreate başlar. Tamamlandığında, görürsünüz **oluşturulan** altında listelenen **durum** hello üzerinde **ağlar** hello Klasik portalında sayfası.

## <a name="gw"></a>Merhaba ağ geçidi oluşturma
1. Merhaba üzerinde **ağlar** sayfasında, yeni sanal ağ hello oluşturulan tıklayın ve ardından **Pano** hello sayfanın üst kısmındaki hello.
2. Merhaba, hello altta **Pano** sayfasında, **ağ geçidi Oluştur** seçip **dinamik yönlendirme**. Tıklatın **Evet** tooconfirm toocreate bir ağ geçidi istiyor.
3. Merhaba ağ geçidi oluşturma başlatıldığında, bu hello ağ geçidi başlatıldı bildiğiniz bir ileti veren görürsünüz. Merhaba ağ geçidi toocreate too45 dakika yukarı sürebilir.
4. Ağ tooa hattınız bağlayın. Merhaba hello makalesindeki yönergeleri izleyin [nasıl toolink sanal ağlar tooExpressRoute devreler](expressroute-howto-linkvnet-classic.md).

## <a name="config"></a>Varolan Klasik VNet ExpressRoute için yapılandırma
Klasik bir VNet zaten varsa, hello Klasik Portalı'nda tooconnect tooExpressRoute yapılandırabilirsiniz. Hello ayarları olan hello aynı hello bölümlerde yukarıdaki okuyun, bu bölümler toobecome ile Merhaba tanıdık ayarlarını gereken şekilde. Toocreate ExpressRoute /-siteye eşzamanlı bağlantı istiyorsanız, bkz: [bu makalede](expressroute-howto-coexist-classic.md) hello adımlar için. Bunlar hello bu makaledeki adımları farklı.

1. Sanal ağ ayarlarınızı hello rest güncelleştirmeden önce toocreate hello yerel ağ gerekir. ExpressRoute hello Klasik portal aracılığıyla yapılandırırken gerekli olan yeni bir yerel ağ toocreate tıklatın **yeni**  **>**  **Ağ Hizmetleri**  **>**  **Sanal ağ**  **>**  **Ekle yerel ağ**. Merhaba Sihirbazı adımları toocreate hello yerel ağ uygulayın.
2. Kullanım **yapılandırma** sayfasında tooupdate hello rest hello ayarlarının VNet ve tooassociate hello VNet toohello yerel ağınız için.
3. Hello ayarlarını yapılandırdıktan sonra toohello Git [oluşturma hello ağ geçidi](#gw) Bu makale toocreate hello ağ geçidi bölümü.

## <a name="next-steps"></a>Sonraki adımlar
* Tooadd sanal makineleri tooyour sanal ağ istiyorsanız, bkz: [sanal makine öğrenme yolları](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Merhaba toolearn ExpressRoute hakkında daha fazla bilgi istiyorsanız bkz [ExpressRoute genel bakış](expressroute-introduction.md).

