---
title: aaaAzure kaynak sistem durumu ile ilgili SSS | Microsoft Docs
description: "Azure kaynak durumu genel bakış"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Azure kaynak durumu ile ilgili SSS
Merhaba toocommon ile Azure kaynak durumu ilgili sorular yanıtlanmaktadır öğrenin.

## <a name="what-is-azure-resource-health"></a>Azure kaynak durumu nedir?
Kaynak Durumu, bir Azure sorunu kaynaklarınızı etkilediğinde bunu tanılamanıza ve destek almanıza yardımcı olur. Merhaba geçerli ve geçmiş kaynaklarınızın sistem durumunu hakkında bilgilendirir ve sorunları azaltmaya yardımcı olur. Kaynak Durumu, Azure hizmet sorunları ile ilgili yardıma ihtiyacınız olduğunda teknik destek sağlar.  

## <a name="what-is-hello-resource-health-intended-for"></a>Kaynak durumu yönelik hello nedir?
Bir kaynağı ile ilgili bir sorun algıladı sonra kaynak durumu hello temel nedeni tanılamanıza yardımcı olabilir. Azure hizmet sorunları hakkında daha fazla yardıma ihtiyacınız olduğunda Yardım toomitigate hello sorun ve teknik destek sağlar.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Hangi sistem durumu denetler gerçekleştirilir kaynak durumu tarafından?
Kaynak durumu hello üzerinde göre çeşitli denetimleri gerçekleştirir [kaynak türü](resource-health-checks-resource-types.md). Bu denetimler tasarlanmış tooimplement üç sorunları türleri şunlardır: 
- Planlanmamış olayları, örneğin bir beklenmeyen ana bilgisayar yeniden başlatma
- Planlanan olayları ister zamanlanmış konak işletim sistemi güncelleştirmeleri
- Bir sanal makine yeniden başlatılıyor kullanıcı örneğin kullanıcı eylemleri tarafından tetiklenen olayları

## <a name="what-does-each-of-hello-health-status-mean"></a>Her hello sistem durumunu anlamı nedir?
Üç farklı sistem durum vardır:
- Kullanılabilir: Var olmayan herhangi bir bilinen sorun hello bu kaynak denetleyin.%nÇözüm Azure platformu
- Kullanılabilir: Kaynak durumu hello kaynak etkileyen sorunları algıladı.
- Bilinmeyen: hakkında bilgi alma durduğundan kaynak durumu bir kaynağın hello durumu belirlenemiyor. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>Ne bilinmeyen durum ortalama hello? My kaynakla yanlış bir şey mi?
Kaynak durumu belirli bir kaynak hakkında bilgi alma durduğunda hello sistem durumu toounknown ayarlanır. Bu durum burada sorunları yaşıyor durumlarda hello kaynak hello durumunun kesin bir gösterge olmamasına karşın Azure bir sorun olduğunu gösteriyor olabilir.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Kullanılabilir olmayan bir kaynak için nasıl Yardım alabilirim?
Merhaba kaynak durumu dikey penceresinden bir destek isteği gönderebilirsiniz. Merhaba kaynak kullanılamadığında Microsoft tooopen isteği ile bir destek sözleşmesi gerekli değildir çünkü platform olaylar.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Kaynak durumu platform sorunları şey yaptım karşı ortası kullanılamazlık birbirinden mu?
Evet, bir kaynak kullanılabilir olmadığında kaynak durumu hello kök nedeni bu kategorilerden birini içinde tanımlar: 
-   Kullanıcı tarafından başlatılan eylemi
-   Olay 
-   Planlanmamış olay

Merhaba Portalı'nda kullanıcı tarafından başlatılan Eylemler kırmızı bir uyarı simgesi kullanarak planlanmış ve planlanmamış olayları gösterilen sırada bir mavi bildirim simgesini kullanarak gösterilmektedir. Daha fazla ayrıntı hello sağlanan [kaynak durumu genel bakış](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Kaynak durumu my izleme araçları ile tümleştirebilir miyim?
Kaynak durumu tanılamak ve kaynaklarınızı etkisi Azure hizmet sorunlarını gidermek tasarlanan hizmet toohelp ' dir. Kullanabilirsiniz ancak hello kaynak durumu API'si tooprogrammatically elde hello sistem durumu, kaynaklarınızın ölçümleri toomonitor kullanmanızı öneririz. Bir sorun algılandığında, kaynak durumu hello kök nedenini belirlemenize yardımcı olur ve Eylemler tooaddress rehberlik eder bunları. Ziyaret [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn ölçümleri toocheck kaynaklarınıza nasıl kullanabileceğiniz hakkında daha fazla bilgi.

## <a name="where-do-i-find-resource-health"></a>Kaynak durumu nereden bulabilirim?
Toohello Azure portalında oturum sonra kaynak durumu erişebilmeniz için birden çok yolu vardır:
- Tooyour kaynak gidin. Merhaba sol gezinti bölmesinde seçin **kaynak durumu**
- Toohello Azure İzleyici dikey penceresine gidin.  Merhaba sol gezinti bölmesinde seçin **kaynak durumu**.
- Açık hello **Yardım + Destek** hello sağ üst köşedeki hello portal ve ardından seçerek hello soru işareti seçerek dikey **Yardım + Destek**. Merhaba dikey pencere açılır sonra seçeneğini **kaynak durumu**

Itanium tabanlı sistemler için hello kaynak durumu API'si tooobtain bilgileri hello sistem durumu hakkında kaynaklarınızın de kullanabilirsiniz.

## <a name="is-resource-health-available-for-all-resource-types"></a>Kaynak durumu, tüm kaynak türleri için kullanılabilir mi?
Merhaba sistem durumu denetimlerinin ve kaynak durumu desteklenen kaynak türleri listesi bulunabilir [burada](resource-health-checks-resource-types.md).

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>Ne my kaynak kullanılabilir gösteren ancak ı değil düşünüyorsanız yapmalıyım?"
Bir kaynağın Hello durumu denetlenirken tıklayabilirsiniz sağ hello sistem durumu altında **yanlış sistem durumu raporu**. Merhaba raporu göndermeden önce neden hello geçerli sistem durumu yanlış olduğunu düşündüğünüz hakkında ek ayrıntıları sağlayan hello seçeneğiniz vardır.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Kaynak durumu için tüm Azure bölgeleri var mı? 
Kaynak durumu bölgeleri aşağıdaki hello dışında tüm Azure geos üzerinden kullanılabilir:
- ABD Devleti Virginia
- ABD Devleti Iowa
- US DoD Doğu
- US DoD Orta
- Almanya Orta
- Almanya Kuzeydoğu
- Çin Doğu
- Çin Kuzey

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Kaynak durumu hello hizmet sağlığı panosunu veya hello Azure portal hizmeti bildirimleri farklı mı?
Kaynak durumu tarafından sağlanan hello Azure hizmet sağlığı panosunu hello tarafından sağlanan daha ayrıntılı bilgidir.

Oysa [Azure durum](https://status.azure.com) ve hello portal hizmet bildirimleri müşteriler (örneğin bir Azure bölgesi) geniş bir dizi etkileyen hizmeti sorunları hakkında bilgilendirmek, kaynak durumu yalnızca ilgili daha ayrıntılı olayları gösterir toohello belirli kaynak. Örneğin, bir ana bilgisayar beklenmedik şekilde yeniden başlatılırsa, kaynak durumu, sanal makineler Bu konakta çalışmakta olan müşteriler uyarır.

Bu önemli toonotice kaynak yüzeyleri olayları hizmet bildirimlerini de yayımlanan durumu kaynaklarınızı etkileyen olayları görünürlüğünü tamamlamak bu tooprovide ve hizmet sağlığı panosunu hello.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>Her kaynak için tooactivate kaynak durumu gerekiyor mu?
Hayır, sistem durumu bilgisi, kaynak durumu kullanılabilir tüm kaynak türleri kullanılabilir. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Kaynak durumu tooenable Kuruluşum için ihtiyacımız var?
Hayır.  Azure kaynak durumu hello herhangi bir kurulum gereksinimi olmadan Azure portalı içinde erişilebilir.

## <a name="is-resource-health-available-free-of-charge"></a>Kaynak durumu kullanılabilir ücretsiz?
Evet.  Azure kaynak durumu ücretsizdir.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Kaynak durumu sağlar hello önerileri nelerdir?
Hello sistem durumuna bağlı olarak, kaynak durumu sorunlarını giderme harcanan hello süresini azaltarak hello amacı ile önerileri sağlar. Kullanılabilir kaynaklar için öneriler odaklanmayı nasıl toosolve hello en yaygın sorunları müşterilerin karşılaştığı hello. Merhaba kaynak nedeniyle kullanılamaz durumdaysa tooan Azure planlanmamış olay, hello odak olacaktır, sırasında ve sonrasında hello kurtarma işlemi yardımcı üzerinde. 

## <a name="next-steps"></a>Sonraki adımlar

Kaynak durumu hakkında daha fazla bilgi edinin:
-  [Azure kaynak durumu genel bakış](Resource-health-overview.md)
-  [Azure Kaynak Durumu aracılığıyla kullanılabilen kaynak türleri ve durum denetimleri](resource-health-checks-resource-types.md)
