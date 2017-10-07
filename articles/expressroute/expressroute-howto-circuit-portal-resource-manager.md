---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: Azure portal | Microsoft Docs"
description: "Bu makalede nasıl toocreate, sağlama, doğrulayın, güncelleştirme, silme ve bir expressroute bağlantı hattı yetkisini kaldırma açıklanmaktadır."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Oluşturma ve bir expressroute bağlantı hattı değiştirme
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-circuit-classic.md)
>

Bu makalede nasıl toocreate kullanarak bir Azure expressroute bağlantı hattı hello Azure portal ve hello Azure Resource Manager dağıtım modeli açıklanır. Ayrıca aşağıdaki adımları hello nasıl toocheck hello hello devrenin durumunu, güncelleştirin veya silin ve onu yetkisini kaldırma gösterir.


## <a name="before-you-begin"></a>Başlamadan önce
* Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
* Erişim toohello sahip olduğundan emin olun [Azure portal](https://portal.azure.com).
* İzinleri toocreate yeni ağ kaynaklarını olduğundan emin olun. Merhaba doğru izinler yoksa, hesap yöneticinize başvurun.
* Yapabilecekleriniz [bir video izlemek](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) toobetter sırayla başlamadan önce hello adımları anlayın.

## <a name="create-and-provision-an-expressroute-circuit"></a>Oluşturma ve bir expressroute bağlantı hattı sağlama
### <a name="1-sign-in-toohello-azure-portal"></a>1. Toohello Azure portalında oturum açın
Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve Azure hesabınızla oturum açın.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Yeni bir expressroute bağlantı hattı oluşturma
> [!IMPORTANT]
> ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren Fatura edilecek. Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirmek emin olun.
> 
> 

1. Yeni bir kaynak hello seçeneği toocreate seçerek bir expressroute bağlantı hattı oluşturabilirsiniz. Tıklatın **yeni** > **ağ** > **ExpressRoute**hello görüntü aşağıdaki gösterildiği gibi:
   
    ![ExpressRoute bağlantı hattı oluşturma](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Tıklattıktan sonra **ExpressRoute**, hello görürsünüz **oluşturma expressroute bağlantı hattı** dikey. Bu dikey penceresinde hello değerleri doldurma sırasında hello doğru SKU katmanı ve ölçüm verilerini belirttiğinizden emin olun.
   
   * **Katman** bir expressroute bağlantı standart ExpressRoute premium Eklentisi etkin olup olmadığını belirler. Belirleyebileceğiniz **standart** tooget hello standart SKU veya **Premium** hello premium eklenti için.
   * **Ölçüm verilerini** hello faturalama türü belirler. Belirleyebileceğiniz **Metered** ölçülen veri planı için ve **sınırsız** sınırsız veri planı için. Merhaba fatura türünden değiştirebileceğinizi unutmayın **Metered** çok**sınırsız**, ancak hello türünden değiştiremezsiniz **sınırsız** çok**Metered**.
     
     ![Merhaba SKU katmanı ve ölçüm verilerini Yapılandır](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Lütfen bu hello eşleme konumu gösterir hello unutmayın [fiziksel konumu](expressroute-locations.md) Burada sizin eşlemeyi Microsoft ile. Bu **değil** çok bağlantılı hello Azure ağ kaynak sağlayıcısı bulunduğu toohello Coğrafya başvuruyor "Konum" özelliği. Bunlar ilişkili olsa da, iyi bir uygulama toochoose ağ kaynak sağlayıcısı coğrafi olarak Kapat toohello hello hattı eşlemesi konumunu durumdur. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Görünüm hello devreler ve özellikleri
**Tüm hello devreler görüntüleyin**

Seçerek oluşturulan tüm hello devreler görüntüleyebilirsiniz **tüm kaynakları** hello sol taraftaki menüsünde.

![Görünüm bağlantı hatları](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Merhaba özellikleri görüntüle**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Özellikleri görüntüle](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder
Bu dikey penceredeki **sağlayıcı durumu** hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar. **Hattı durum** Microsoft yan hello üzerinde hello durumunu sağlar. Merhaba hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.

Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello hattı durumu aşağıdaki hello olacaktır:

Sağlayıcı Durumu: sağlanmadı<BR>
Devre, durum: etkin

![Sağlama işlemini başlatın](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello değişir:

Sağlayıcı Durumu: sağlama<BR>
Devre, durum: etkin

Toobe mümkün toouse için bir expressroute bağlantı hattı, durumu aşağıdaki hello olmalıdır:

Sağlayıcı Durumu: sağlanan<BR>
Devre, durum: etkin

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin
Merhaba, içinde seçerek ilgileniyor hello hattı özelliklerini görüntüleyebilirsiniz. Merhaba denetleyin **sağlayıcı durumu** ve çok taşımadığından emin olun**hazırlandı** devam etmeden önce.

![Bağlantı hattı ve sağlayıcı durumu](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Yönlendirme yapılandırması oluşturma
Adım adım yönergeler için toohello bakın [expressroute bağlantı hattı yönlendirme yapılandırması](expressroute-howto-routing-portal-resource-manager.md) makale toocreate ve hattı eşlemeler değiştirin.

> [!IMPORTANT]
> Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Sanal ağ tooan expressroute bağlantı hattı bağlantı
Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın. Kullanım hello [sanal bağlama ağları tooExpressRoute devreler](expressroute-howto-linkvnet-arm.md) hello Resource Manager dağıtım modeliyle çalışırken makalesi.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı Hello durumunu alma
Bir bağlantı hattı hello durumunu seçerek görüntüleyebilirsiniz. 

![Bir expressroute bağlantı hattı durumu](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı değiştirme
Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.

Yapabileceğiniz kapalı kalma süresi ile aşağıdaki hello:

* Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.
* Artış hello bant genişliği, expressroute bağlantı hattı var. kapasite kullanılabilir hello bağlantı noktasında sağlanır. Önceki sürüme indirme bir bağlantı hattının bant genişliği hello Not desteklenmiyor. 
* Ölçülen veri tooUnlimited veri planından ölçümü hello değiştirin. Bu değişen hello ölçüm planından veri desteklenmiyor sınırsız veri tooMetered unutmayın.
* Etkinleştirme ve devre dışı *izin Klasik işlemleri*.

Toohello sınırlar ve sınırlamalar hakkında daha fazla bilgi için bkz [ExpressRoute SSS](expressroute-faqs.md).

toomodify bir expressroute bağlantı hattı üzerinde hello tıklatın **yapılandırma** hello aşağıdaki çizimde gösterildiği gibi.

![Bağlantı hattı değiştirme](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Merhaba bant genişliği, SKU, fatura modelini değiştirin ve klasik işlemleri hello yapılandırma dikey izin verebilirsiniz.

> [!IMPORTANT]
> Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir. Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.
>
> Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz. Bant genişliği eski sürüme düşürmeyi toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.
> 
> Premium eklentisi devre dışı bırakma işlemi hello standart bağlantı hattı için izin daha büyük olan kaynakları kullanıyorsanız başarısız olabilir.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme
Expressroute bağlantı hattı hello seçerek silebilirsiniz **silmek** simgesi. Merhaba aşağıdakileri göz önünde bulundurun:

* Tüm sanal ağlardan hello expressroute bağlantı hattı bağlantısını gerekir. Bu işlem başarısız olursa, herhangi bir sanal ağa bağlı olup olmadığını denetleyin toohello hattı.
* Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı** kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir. Biz tooreserve kaynakları devam edecek ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.
* Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması değilse (Merhaba Hizmet Sağlayıcısı sağlama durumu çok ayarlamak**sağlanmadı**) hello hattı sonra silebilirsiniz. Bu hello hattı için fatura durdurur

## <a name="next-steps"></a>Sonraki adımlar
Bağlantı hattınız oluşturduktan sonra aşağıdaki hello emin olun:

* [Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme](expressroute-howto-routing-portal-resource-manager.md)
* [Sanal ağ tooyour expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md)

