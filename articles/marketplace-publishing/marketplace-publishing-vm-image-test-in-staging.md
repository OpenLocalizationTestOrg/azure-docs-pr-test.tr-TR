---
title: VM Merhaba Market teklifi aaaTest | Microsoft Docs
description: "Nasıl tootest VM görüntü hello Azure Marketi anlayın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>VM teklifiniz hello Azure Marketi için hazırlamada test etme
Hazırlama, SKU özel ", test ve toohello Market dağıtmadan önce işlevselliğini doğrulamak sandbox" dağıtma anlamına gelir. Merhaba SKU dağıtmış olan tooa müşteri gibi hazırlama görüntülenir. VM görüntüsü gönderilen sertifikalı toobe toostaging olması gerekir.

## <a name="step-1-push-your-offer-toostaging"></a>1. adım: Teklif toostaging bildirme
1. Merhaba üzerinde **Yayımla** sekmesini tıklatın, **anında tooStaging**.
   
    ![Çizim](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Merhaba yayımlama portalında size herhangi bir hata bildirirse, bunları düzeltin.
3. Merhaba, **kimin hazırlanmış teklifiniz erişebilir?** iletişim kutusunda, Azure abonelikleri toopreview hello teklifiniz kullanacağı hello listesini girin [Azure Önizleme portalı](https://portal.azure.com).
   
   > [!NOTE]
   > Sanal makineler durumunda ve çözüm şablonları, lütfen **sağlamadığı** beyaz liste abonelikleri CSP, DreamSpark veya Open ile Azure türü.
   > 
   > 

    > Merhaba düğmesini tıklattığınızda, sanal makineleri durumunda **İTME tooSTAGING**, aşağıdaki adımları hello hello Sahne gerçekleştirilir. Her bir adımın hello yayımlama hello sekmede altında mümkün tooview hello ilerleme olacaktır portalını yayımlama. (Hazırlanmış hello durumu gösterilir) kadar bu sayfayı düzenli aralıklarla, uçtan düzeltmesi gereken tüm hata bilgileri için işaretlemeniz gerekir.

    > - İlk bakışta hazırlama isteğiniz hello vhd doğrulamak toohello sertifika takımın gider. İsteğiniz değişiklik yalnızca pazarlama aldı, ancak ardından hello sertifika adım atlanır.
    > - Merhaba sertifika tamamlandıktan sonra tüm hello Teklif başlangıç çoğaltmasını Azure veri merkezleri hello. Genellikle, 24-48hours hello çoğaltma toocomplete için alır ancak tooa hafta hello vhd hello boyutuna bağlı olarak yukarı sürebilir. İsteğiniz değişiklik yalnızca pazarlama aldı, ancak ardından hello çoğaltma daha hızlıdır.
    > - Hello çoğaltma işlemi tamamlandıktan sonra hello teklif hello kullanılabilecek [Azure portal](http:/portal.azure.com). O zaman hello durum hale HAZIRLANAN hello portalını yayımlama. Aşamalı bir teklif hello görülebilir [Azure portal](http:/portal.azure.com) yalnızca teklif ile hangi hello hazırlanan hello abonelikle ilişkili hello e-posta Kimlikleri'ni kullanarak.

1. İçinde toohello oturum [Azure Önizleme portalını](https://portal.azure.com) hello birini kullanarak Azure abonelikleri listelenen hello önceki adımda.
2. Teklifiniz bulun ve VM görüntü noktaları doğrula:
   
   * İçerik pazarlama doğru hello Market gösterildiğini doğrulayın.
   * Merhaba VM görüntüsü uçtan uca dağıtımı.
     
      ![img harita portalı](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Teklifiniz hello Yayımlama Portalı Microsoft'a bildirmeyi kadar hazırlama kalacak [**Yayımla** sekmesini > merhaba düğmesine tıklayın **"onay tooPush tooProduction istek"**] hazır toopush olduğunu tooproduction. Her şeyi listelenen giderek teklifiniz için hazırlık üzerinden tüm ekibinizin üyeleri denetleyin ideal zaman toohave budur.
> 
> Platform hazırlama hello hello yayımcı tarafından önizleme modunda test hello teklif için tasarlanmıştır. Bu platofrm commerical amaçlı kullanan önleyin.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Teklifiniz "hazırlanan" ve işlevselliği ve içeriği pazarlama test göre toohello son yayımlama geçebilmeniz aşaması, **4. adım**: [, teklif toohello Market dağıtma](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Başlarken: nasıl toopublish bir teklif toohello Azure Market](marketplace-publishing-getting-started.md)

