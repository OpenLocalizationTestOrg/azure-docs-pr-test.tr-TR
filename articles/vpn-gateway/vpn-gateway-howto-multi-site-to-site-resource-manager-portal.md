---
title: "Birden çok VPN ağ geçidi siteden siteye bağlantıları tooa VNet ekleyin: Azure Portal: Resource Manager | Microsoft Docs"
description: "Varolan bir bağlantıyı sahip çok siteli S2S bağlantıları tooa VPN ağ geçidi Ekle"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Mevcut bir VPN ağ geçidi bağlantısı olan bir siteden siteye bağlantı tooa VNet ekleme

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klasik)](vpn-gateway-multi-site.md)
>
> 

Bu makalede, varolan bir bağlantıyı sahip hello Azure portal tooadd siteden siteye (S2S) bağlantıları tooa VPN ağ geçidi kullanılarak üzerinden açıklanmaktadır. Bu tür bir bağlantı başvurulan tooas "çok siteli" yapılandırma görülür. S2S bağlantısı tooa S2S bağlantısı, noktadan siteye bağlantı veya VNet-VNet bağlantısı zaten VNet ekleyebilirsiniz. Bağlantıları eklerken, bazı sınırlamalar vardır. Merhaba denetleyin [başlamadan önce](#before) yapılandırmanıza başlamadan önce bu makale tooverify bölümünde. 

Bu makale RouteBased VPN ağ geçidine sahip hello Resource Manager dağıtım modeli kullanılarak oluşturulan tooVNets geçerlidir. Bu adımları tooExpressRoute /-siteye eşzamanlı bağlantı yapılandırmaları geçerli değildir. Bkz: [ExpressRoute/S2S arada var olabilen bağlantılar](../expressroute/expressroute-howto-coexist-resource-manager.md) arada var olabilen bağlantılar hakkında bilgi için.

### <a name="deployment-models-and-methods"></a>Dağıtım modelleri ve yöntemleri
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Bu tabloda yeni makaleler olarak güncelleştiriyoruz ve ek araçlar bu yapılandırma için kullanılabilir hale gelir. Bir makale kullanılabilir olduğunda sizi doğrudan bu tablodan tooit bağlayın.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Başlamadan önce
Aşağıdaki öğelerindeki hello doğrulayın:

* Bir ExpressRoute/S2S eşzamanlı bağlantı oluşturma değil.
* Varolan bir bağlantı hello Resource Manager dağıtım modeli kullanılarak oluşturulmuş bir sanal ağ var.
* Merhaba sanal ağ geçidi Vnet'inizi için RouteBased ' dir. PolicyBased VPN ağ geçidi varsa, hello sanal ağ geçidini silin ve yeni bir VPN ağ geçidi RouteBased olarak oluşturun.
* Herhangi bir hello bu VNet bağlandığı sanal ağlar için hello adres aralıklarını hiçbiri çakışıyor.
* Uyumlu VPN cihazı ve mümkün tooconfigure olan birisi sahip onu. Bkz. [VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md). VPN Cihazınızı yapılandırmak konusunda veya şirket içi ağ yapılandırmanızda bulunan hello IP adresi aralıklarıyla ilgili bilginiz varsa, bu detayları sizin için sağlayabilecek biriyle toocoordinate gerekir.
* VPN cihazınız için dışarıya dönük bir genel IP adresine sahip. Bu IP adresi bir NAT’nin arkasında olamaz.

## <a name="part1"></a>Bölüm 1 - bir bağlantı yapılandırma
1. Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve gerekiyorsa Azure hesabınızla oturum açın.
2. Tıklatın **tüm kaynakları** ve bulun, **sanal ağ geçidi** kaynakları hello listesinden ve tıklatın.
3. Merhaba üzerinde **sanal ağ geçidi** dikey penceresinde tıklatın **bağlantıları**.
   
    ![Bağlantılar dikey penceresi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")<br>
4. Merhaba üzerinde **bağlantıları** dikey penceresinde tıklatın **+ Ekle**.
   
    ![Add bağlantı düğmesini](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Ekle bağlantı düğmesi")<br>
5. Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde, aşağıdaki alanları hello doldururken:
   
   * **Ad:** toogive toohello site hello bağlantı oluşturmakta istediğiniz hello adı.
   * **Bağlantı türü:** seçin **siteden siteye (IPSec)**.
     
     ![Ekle bağlantı dikey](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Ekle bağlantı dikey")<br>

## <a name="part2"></a>Bölüm 2 - bir yerel ağ geçidi ekleme
1. Tıklatın **yerel ağ geçidi** ***bir yerel ağ geçidi seçin***. Bu hello açar **Seç yerel ağ geçidi** dikey.
   
    ![Seç yerel ağ geçidi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Seç yerel ağ geçidi")<br>
2. Tıklatın **Yeni Oluştur** tooopen hello **oluşturma yerel ağ geçidi** dikey.
   
    ![Create yerel ağ geçidi dikey](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "oluşturma yerel ağ geçidi")<br>
3. Merhaba üzerinde **oluşturma yerel ağ geçidi** dikey penceresinde, aşağıdaki alanları hello doldururken:
   
   * **Ad:** toogive toohello yerel ağ geçidi kaynağı istediğiniz hello adı.
   * **IP adresi:** hello tooconnect için istediğiniz hello sitesinde hello VPN cihazının genel IP adresi.
   * **Adres alanı:** toobe istediğiniz hello adres alanı toohello yeni yerel ağ sitesi yönlendirilir.
4. Tıklatın **Tamam** hello üzerinde **oluşturma yerel ağ geçidi** dikey toosave hello değişiklikleri.

## <a name="part3"></a>3 Kısım - hello paylaşılan anahtar ekleme ve hello bağlantı oluşturma
1. Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde hello paylaşılan anahtar bağlantınızı toouse toocreate istediğiniz ekleyin. Ya da VPN aygıtınızdan hello paylaşılan anahtar alın veya bir burada yapabilir ve VPN cihaz toouse hello yapılandırmak aynı paylaşılan anahtar. Merhaba hello anahtarlarının tam olarak olduğunu şeydir önemli hello aynı.
   
    ![Paylaşılan anahtar](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")<br>
2. Merhaba dikey penceresinde Hello altındaki tıklatın **Tamam** toocreate hello bağlantı.

## <a name="part4"></a>4 Kısım - hello VPN bağlantısını doğrulama


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Merhaba sanal makineleri görmek [öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) daha fazla bilgi için.
