---
title: "Nasıl tooconfigure (eşleme) bir expressroute bağlantı hattı için yönlendirmeyi: Resource Manager: Azure | Microsoft Docs"
description: "Bu makalede, oluşturma ve sağlama hello özel, genel ve Microsoft bir expressroute bağlantı hattı eşlemesi hello adım adım anlatılmaktadır. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Oluşturma ve bir ExpressRoute bağlantı hattı için eşlemesini değiştirme

Bu makalede, bir expressroute bağlantı hattı hello Azure portal kullanarak hello Resource Manager dağıtım modelinde için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur. Ayrıca, hello durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın. Bağlantı hattınız ile toouse farklı yöntem toowork istiyorsanız, bir makale listesi aşağıdaki hello seçin:


## <a name="configuration-prerequisites"></a>Yapılandırma önkoşulları

* Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) hello sayfasında [yönlendirme gereksinimleri](expressroute-routing.md) sayfası ve hello [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfasında.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Merhaba expressroute bağlantı hattı, toobe mümkün toorun hello cmdlet'leri hello sonraki bölümlerde için sağlanmış ve etkin durumda olması gerekir.
* Paylaşılan bir anahtar/MD5 karma değeri toouse düşünüyorsanız emin toouse bu hello sayısı tünel ve sınırı hello karakter tooa en fazla 25 her iki tarafında olması.

Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yönlendirmeyi sizin için yönetir ve yapılandırır. 

> [!IMPORTANT]
> Biz hello Hizmet Yönetimi Portalı aracılığıyla hizmet sağlayıcılar tarafından yapılandırılan eşlemeleri şu anda tanıtmıyoruz. Bu özelliği yakında etkinleştirmek için çalışıyoruz. BGP eşlemelerini yapılandırmadan önce hizmet sağlayıcınıza başvurun.
> 
> 

Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz. Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz. Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.

## <a name="azure-private-peering"></a>Azure özel eşlemesi

Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.

### <a name="toocreate-azure-private-peering"></a>Azure özel eşleme toocreate

1. Merhaba expressroute bağlantı hattını yapılandırın. Merhaba hattı tam olarak hello bağlantı sağlayıcı tarafından devam etmeden önce sağlandığından emin olun.

  ![Liste](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın. Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:

  * Bir/30 alt ağı hello birincil bağlantı için. Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz. Bu eşleme için özel bir AS numarası kullanabilirsiniz. 65515’i kullanmadığınızdan emin olun.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.
3. Hello aşağıdaki örnekte gösterildiği gibi Hello Azure özel eşleme satırını seçin:

  ![Özel](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Özel eşleme oluşturun. Görüntü aşağıdaki hello bir yapılandırma örneği gösterilir:

  ![Özel eşleme oluşturun](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Tüm parametreleri belirledikten sonra hello yapılandırmayı kaydedin. Merhaba yapılandırma başarıyla kabul edildikten sonra aşağıdaki örneğine benzeri toohello bakın:

  ![Özel eşleme Kaydet](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview Azure özel eşleme ayrıntıları

Merhaba eşlemeyi seçerek Azure özel eşleme özelliklerini hello görüntüleyebilirsiniz.

![Özel eşleme görüntüleyin](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>Azure özel eşleme yapılandırmasını tooupdate

Eşleme için başlangıç satırı seçin ve hello eşleme özelliklerini değiştirebilirsiniz.

![Özel eşleme güncelleştir](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>Azure özel eşleme toodelete

Görüntü aşağıdaki hello gösterildiği gibi hello Sil simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:

![Özel eşleme Sil](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Azure ortak eşleme

Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.

### <a name="toocreate-azure-public-peering"></a>Azure ortak eşleme toocreate

1. ExpressRoute bağlantı hattını yapılandırın. Merhaba hattı tam olarak hello bağlantı sağlayıcı tarafından daha fazla devam etmeden önce sağlandığından emin olun.

  ![Ortak eşleme listesi](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın. Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:

  * Bir/30 alt ağı hello birincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.
3. Görüntü aşağıdaki hello gösterildiği gibi Hello Azure ortak eşleme satırını seçin:

  ![Ortak eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Ortak eşlemeyi yapılandırın. Görüntü aşağıdaki hello bir yapılandırma örneği gösterilir:

  ![Ortak eşlemeyi yapılandırın](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Tüm parametreleri belirledikten sonra hello yapılandırmayı kaydedin. Merhaba yapılandırma başarıyla kabul edildikten sonra aşağıdaki örneğine benzeri toohello bakın:

  ![Ortak eşleme yapılandırmasını kaydedin](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview Azure genel eşliği ayrıntıları

Merhaba eşlemeyi seçerek Azure ortak eşleme özelliklerini hello görüntüleyebilirsiniz.

![Ortak eşleme özelliklerini görüntüle](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>Azure ortak eşleme yapılandırmasını tooupdate

Eşleme için başlangıç satırı seçin ve hello eşleme özelliklerini değiştirebilirsiniz.

![Ortak eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>Azure ortak eşleme toodelete

Hello aşağıdaki örnekte gösterildiği gibi hello Sil simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:

![Ortak eşleme Sil](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Microsoft eşlemesi

Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme yardımcı olur.

> [!IMPORTANT]
> Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 hello Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur. Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı. Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft eşlemesi

1. ExpressRoute bağlantı hattını yapılandırın. Merhaba hattı tam olarak hello bağlantı sağlayıcı tarafından daha fazla devam etmeden önce sağlandığından emin olun.

  ![Microsoft eşlemesi listesi](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Microsoft Hello bağlantı hattı için eşlemesini yapılandırın. Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.

  * Bir/30 alt ağı hello birincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
  * Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın. Yalnızca ortak IP adresi ön ekleri kabul edilir. Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz. Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.
  * **İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekler Tanıtıyorsanız, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.
  * Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.
3. Merhaba tooconfigure, istediğiniz hello aşağıdaki gösterildiği gibi eşliği seçebilirsiniz örnek. Merhaba Microsoft eşleme satırını seçin.

  ![Microsoft eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Microsoft eşlemesini yapılandırın. Görüntü aşağıdaki hello bir yapılandırma örneği gösterilir:

  ![Microsoft eşlemesini yapılandırın](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Tüm parametreleri belirledikten sonra hello yapılandırmayı kaydedin.

  Bağlantı hattınız 'doğrulama gerekli' tooa alırsa (Merhaba görüntüde gösterildiği gibi) durumunda, bir destek bileti tooshow hello öneklerini tooour destek ekibi sahipliğini kanıtını açmanız gerekir.

  ![Microsoft eşleme yapılandırmasını kaydedin](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  Hello aşağıdaki örnekte gösterildiği gibi bir destek bileti doğrudan hello portalından açabilirsiniz:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Merhaba yapılandırma başarıyla kabul edildikten sonra görüntü aşağıdaki benzeri toohello bakın:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>tooview Microsoft eşleme ayrıntıları

Merhaba eşlemeyi seçerek Azure ortak eşleme özelliklerini hello görüntüleyebilirsiniz.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft eşleme yapılandırması

Eşleme için başlangıç satırı seçin ve hello eşleme özelliklerini değiştirebilirsiniz.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft eşlemesi

Görüntü aşağıdaki hello gösterildiği gibi hello Sil simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Sonraki adımlar

Sonraki adım, [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-portal-resource-manager.md)
* ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).
* Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).
* Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).
