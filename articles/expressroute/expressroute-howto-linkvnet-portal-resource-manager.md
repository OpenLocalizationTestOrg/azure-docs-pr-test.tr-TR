---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: Azure portal | Microsoft Docs"
description: "Bu belge nasıl (Vnet'ler) tooExpressRoute devreler toolink sanal ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
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

Bu makalede hello Resource Manager dağıtım modeli kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute bağlantı hatları bağlama ve Azure portal hello yardımcı olur. Sanal ağlar olabilir ya da hello aynı abonelik veya başka bir abonelik parçası olabilir.

## <a name="before-you-begin"></a>Başlamadan önce
* Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.
  
  * Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve bağlantı sağlayıcınız tarafından etkinleştirilmiş hello hattı sahip.
  * Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun. Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-portal-resource-manager.md) yönlendirme yönergeleri için makalenin.
  * Azure özel eşleme yapılandırılır ve uçtan uca bağlantı etkinleştirebilmeniz için ağınız ve Microsoft arasında hello BGP eşliği yukarı olduğundan emin olun.
  * Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olduğundan emin olun. Çok olarak Hello yönergeleri[ExpressRoute için bir sanal ağ geçidi oluşturmak](expressroute-howto-add-gateway-resource-manager.md). ExpressRoute için bir sanal ağ geçidi hello GatewayType 'ExpressRoute' değil VPN kullanır.

* Too10 sanal ağlar tooa standart expressroute bağlantı hattı bağlayabilirsiniz. Tüm sanal ağları hello olmalıdır standart bir expressroute bağlantı hattını kullanırken aynı coğrafi bölge. 
* Bir sanal ağ dışında hello coğrafi bölge hello expressroute bağlantı hattı, bağlantı veya çok sayıda sanal ağlar tooyour expressroute bağlantı hattı hello ExpressRoute premium eklentisi etkinse bağlanabilirsiniz. Merhaba denetleyin [SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.
* Yapabilecekleriniz [bir video izlemek](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) başına toobetter anlamak önce hello adımları.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı

### <a name="toocreate-a-connection"></a>toocreate bağlantı

> [!NOTE]
> BGP yapılandırma bilgilerini hello Katman 3 sağlayıcısı, eşlemeler yapılandırılıp yapılandırılmadığını gösterilmez. Bağlantı hattınız sağlanan durumdaysa mümkün toocreate bağlantıları olması gerekir.
>

1. Expressroute bağlantı hattı ve Azure özel eşleme başarılı bir şekilde yapılandırıldığından emin olun. Merhaba yönergeleri izleyin [bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md). Expressroute bağlantı hattı hello görüntü aşağıdaki gibi görünmelidir:

    ![ExpressRoute bağlantı hattı ekran görüntüsü](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. Sanal ağ geçidi tooyour expressroute bağlantı hattı bağlantı toolink sağlama şimdi başlayabilirsiniz. Tıklatın **bağlantı** > **Ekle** tooopen hello **Bağlantı Ekle** dikey penceresinde ve başlangıç değerleri yapılandırın.

    ![Bağlantı ekran Ekle](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Bağlantınızı başarıyla yapılandırıldıktan sonra bağlantı nesnesi hello bağlantısı için hello bilgileri gösterir.

     ![Bağlantı nesnesi ekran görüntüsü](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete bağlantı
Bir bağlantı hello seçerek silebilirsiniz **silmek** hello dikey bağlantınız için simge.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Farklı bir abonelik tooa hattı sanal bir ağa bağlan
Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz. Aşağıdaki Hello şekilde birden çok abonelik arasında basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterilmektedir.

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir.
- Hizmetlerini dağıtmak için her hello kuruluşunuz içinde hello bölümlerin kendi abonelik kullanabilirsiniz, ancak tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşabilirsiniz.
- Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir. Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.

    > [!NOTE]
    > Bağlantı ve bant genişliği ücretleri ayrılmış hello hattı için uygulanan toohello ExpressRoute bağlantı hattı sahip olacaktır. Tüm sanal ağları hello paylaşmak aynı bant genişliği.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Yönetim - hattı sahipleri ve hattı kullanıcılar

Merhaba 'devre sahibinden' hello ExpressRoute bağlantı hattı kaynak yetkili bir güç kullanıcısıdır. Merhaba devre sahibinden 'hattı kullanıcılar tarafından kullanılan yetkilerini oluşturabilirsiniz. Bağlantı hattı kullanıcılardır sahipleri sanal ağ içinde olmayan ağ geçitleri, expressroute bağlantı hattı hello gibi aynı abonelik hello. Bağlantı hattı kullanıcıların yetkilerini (sanal ağ başına bir yetkilendirme) kullanmak.

Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir. Bir yetkilendirme sonuçlarına tüm bağlantı erişimini iptal edildi hello abonelikten silinmesini iptal ediliyor.

### <a name="circuit-owner-operations"></a>Bağlantı hattı sahibi işlemleri

**toocreate Bağlantı Yetkilendirme**

Merhaba devre sahibinden bir yetkilendirme oluşturur. Bu olabilir bir yetkilendirme anahtarı hello oluşturulmasında sonuçları kendi sanal ağ ağ geçitleri toohello expressroute bağlantı hattı kullanıcı tooconnect tarafından kullanılır. Bir yetkilendirme yalnızca bir bağlantı için geçerli değil.

1. Merhaba ExpressRoute dikey penceresinde tıklayın **yetkilerini** ve ardından bir **adı** hello yetkilendirme ve tıklatın **kaydetmek**.

    ![Yetkileri değiştirme](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Merhaba Hello yapılandırma kaydedildikten sonra kopyalama **kaynak kimliği** ve hello **yetkilendirme anahtarının**.

    ![Yetkilendirme anahtarı](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete Bağlantı Yetkilendirme**

Bir bağlantı hello seçerek silebilirsiniz **silmek** hello dikey bağlantınız için simge.

### <a name="circuit-user-operations"></a>Bağlantı hattı kullanıcı işlemleri

Merhaba hattı kullanıcı hello kaynak kimliği ile Merhaba devre sahibinden yetkilendirme anahtarından gerekir. 

**tooredeem Bağlantı Yetkilendirme**

1.  Merhaba tıklatın **+ yeni** düğmesi.

    ![Yeni'yi tıklatın](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Arama **"Bağlantı"** hello Market, seçin ve tıklatın **oluşturma**.

    ![Bağlantı için arama](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Merhaba emin olun **bağlantı türü** çok Ayarla "ExpressRoute".


4.  Merhaba ayrıntıları doldurun ve ardından **Tamam** hello temel bilgileri dikey penceresinde.

    ![Temel Bilgiler dikey penceresi](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  Merhaba, **ayarları** dikey penceresinde, Select hello **sanal ağ geçidi** ve hello denetleyin **yetkilendirme kullanmak** onay kutusu.

6.  Merhaba girin **yetkilendirme anahtar** ve hello **hattı URI eş** ve hello bağlantı bir ad verin. **Tamam** düğmesine tıklayın.

    ![Ayarlar dikey penceresi](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Merhaba hello bilgileri gözden **Özet** tıklayın ve dikey **Tamam**.


**toorelease Bağlantı Yetkilendirme**

Bir yetkilendirme hello ExpressRoute bağlantı hattı toohello sanal ağ bağlantıları hello bağlantı silerek serbest bırakabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
