---
title: "ExpressRoute için bir sanal ağ geçidi tooa VNet ekleyin: Portal: Azure | Microsoft Docs"
description: "Bu makalede Resource Manager Vnet'i ExpressRoute için önceden oluşturulmuş bir sanal ağ geçidi tooan eklerken size yol gösterilir."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Bir sanal ağ geçidi hello Azure portalını kullanarak ExpressRoute için yapılandırma
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portalı](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Klasik - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Bu makalede önceden var olan bir VNet için hello adımları tooadd bir sanal ağ geçidi anlatılmaktadır. Bu makalede hello adımları tooadd anlatılmaktadır, yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidi kaldırın. Merhaba bu yapılandırma için özellikle bir expressroute bağlantı yapılandırmasında kullanılacak hello Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için adımlardır. Sanal ağ geçitleri ve ExpressRoute ağ geçidi yapılandırma ayarları hakkında daha fazla bilgi için bkz: [ExpressRoute için sanal ağ geçitleri hakkında](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Başlamadan önce

Bu görev kullanılacak bir VNet Hello adımları yapılandırma başvuru listesi aşağıdaki hello başlangıç değerleri temel. Biz bizim örnek adımlarda bu listeyi kullanın. Merhaba değerleri kendi değerlerinizle değiştirerek bir başvuru olarak hello listesi toouse kopyalayabilirsiniz.

**Yapılandırma başvuru listesi**

* Sanal ağ adı "TestVNet" =
* Sanal ağ adres alanı 192.168.0.0/16 =
* Alt ağ adı "Ön uç" = 
    * Alt ağ adres alanının "192.168.1.0/24" =
* Kaynak grubu "TestRG" =
* Konum, "Doğu ABD" =
* Ağ geçidi alt ağ adı: "GatewaySubnet gerekir her zaman adını bir ağ geçidi alt ağı" *GatewaySubnet*.
    * Ağ geçidi alt ağ adres alanının "192.168.200.0/26" =
* Ağ geçidi adı "ERGW" =
* Ağ geçidi IP adı "MyERGWVIP" =
* Ağ geçidi türü = "ExpressRoute" Bu tür bir ExpressRoute yapılandırma için gereklidir.
* Ağ geçidi genel IP adı "MyERGWVIP" =

Görüntüleyebileceğiniz bir [Video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) yapılandırmanıza başlamadan önce bu adımları.

## <a name="create-hello-gateway-subnet"></a>Merhaba ağ geçidi alt ağı oluşturun

1. Merhaba, [portal](http://portal.azure.com), toohello Resource Manager sanal ağ toocreate bir sanal ağ geçidi istediğiniz gidin.
2. Merhaba, **ayarları** bölümü, VNet dikey tıklayın **alt ağlar** tooexpand hello alt ağlar dikey penceresini.
3. Merhaba üzerinde **alt ağlar** dikey penceresinde tıklatın **+ ağ geçidi alt ağı** tooopen hello **alt ağ Ekle** dikey. 
   
    ![Merhaba ağ geçidi alt ağı eklemek](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "hello ağ geçidi alt ağı Ekle")


4. Merhaba **adı** alt ağınızı hello oturum otomatik olarak doldurulur 'GatewaySubnet' değeri. Bu değer varsayılan olarak, hello ağ geçidi alt ağı sırada Azure toorecognize hello alt ağ için gereklidir. Merhaba otomatik doldurulmuş ayarlamak **adres aralığı** yapılandırma gereksinimlerinizi toomatch değerleri. / 27 veya daha büyük bir ağ geçidi alt ağı oluşturmanızı öneririz (/ 26, / 25 vb..). Ardından **Tamam** toosave hello değerleri ve hello ağ geçidi alt ağı oluşturun.

    ![Merhaba alt ekleme](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "hello alt ağ ekleme")

## <a name="create-hello-virtual-network-gateway"></a>Merhaba sanal ağ geçidi oluşturma

1. Merhaba sol tarafında hello portal'ı tıklatın ** + ** ve Ara 'Sanal ağ geçidi' yazın. Bulun **sanal ağ geçidi** hello arama dönün ve hello girdiyi tıklatın. Merhaba üzerinde **sanal ağ geçidi** dikey penceresinde tıklatın **oluşturma** hello dikey penceresinde hello sonundaki. Merhaba açılır **sanal ağ geçidi Oluştur** dikey.
2. Merhaba üzerinde **sanal ağ geçidi Oluştur** dikey penceresinde, sanal ağ geçidinizin hello değerlerini doldurun.

    ![Sanal ağ geçidi oluştur dikey penceresinin alanları](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Sanal ağ geçidi oluştur dikey penceresinin alanları")
3. **Ad**: Ağ geçidinizi adlandırın. Bu olduğu değil hello bir ağ geçidi alt ağını adlandırmayla aynı. Oluşturmakta olduğunuz hello ağ geçidi nesnesinin hello adı kullanıcının.
4. **Ağ geçidi türü**: seçin **ExpressRoute**.
5. **SKU**: Select hello ağ geçidinden SKU hello açılır.
6. **Konum**: hello ayarlamak **konumu** alan sanal ağınızı bulunduğu toopoint toohello konumu. Başlangıç konumu, sanal ağınızda bulunduğu toohello bölge işaret etmiyor hello sanal ağ hello 'Seç bir sanal ağ' açılır listede görünmüyor.
7. Merhaba sanal ağ toowhich seçin bu ağ geçidi tooadd istiyor. Tıklatın **sanal ağ** tooopen hello **sanal ağ seçin** dikey. Merhaba VNet seçin. Sanal ağınızı görmüyorsanız, emin hello olun **konumu** toohello bölgesi, sanal ağınızda bulunduğu alan işaret eden.
9. Genel bir IP adresi seçin. Tıklatın **genel IP adresi** tooopen hello **genel IP adresi seçin** dikey. Tıklatın **+ Yeni Oluştur** tooopen hello **oluşturma ortak IP adresi dikey**. Genel IP adresiniz için bir ad girin. Bu dikey bir ortak IP adresi dinamik olarak atanmış bir ortak IP adresi nesne toowhich oluşturur. Tıklatın **Tamam** toosave değişiklikleri toothis dikey.
10. **Abonelik**: Abonelik seçili doğru bu hello doğrulayın.
11. **Kaynak grubu**: Bu ayar hello Seçtiğiniz sanal ağ tarafından belirlenir.
12. Merhaba ayarlama **konumu** hello önceki ayarları belirttikten sonra.
13. Hello ayarlarını doğrulayın. Ağ geçidi tooappear hello Panoda istiyorsanız, seçebileceğiniz **PIN toodashboard** hello dikey penceresinde hello sonundaki.
14. Tıklatın **oluşturma** toobegin hello ağ geçidi oluşturma. Hello ayarları doğrulanır ve hello ağ geçidi dağıtır. Sanal ağ geçidi oluşturma too45 dakika toocomplete alabilir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba VNet ağ geçidini oluşturduktan sonra VNet tooan expressroute bağlantı hattı bağlayabilirsiniz. Bkz: [sanal ağ tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-portal-resource-manager.md).
