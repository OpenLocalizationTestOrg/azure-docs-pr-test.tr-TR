---
title: aaaAzure kaynak durumu ile ilgili SSS | Microsoft Docs
description: "Azure kaynak durumu genel bakış"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: 5c5cfa116340094ffb1d6d5b206a11d389a0305a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Azure kaynak durumu ile ilgili SSS
Merhaba toocommon ile Azure kaynak durumu ilgili sorular yanıtlanmaktadır öğrenin.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
* [Azure Kaynak Durumu nedir?](#what-is-azure-resource-health)
* [Ne hello kaynak durumu yöneliktir?](#what-is-the-resource-health-intended-for)
* [Hangi sistem durumu denetler gerçekleştirilir kaynak durumu tarafından?](#what-health-checks-are-performed-by-resource-health)
* [Her hello sistem durumunu anlamı nedir?](#what-does-each-of-the-health-status-mean)
* [Ne bilinmeyen durum ortalama hello? My kaynakla yanlış bir şey mi?](#what-does-the-unknown-status-mean-is-something-wrong-with-my-resource)
* [Kullanılabilir olmayan bir kaynak için nasıl Yardım alabilirim?](#how-can-i-get-help-for-a-resource-that-is-unavailable)
* [Kaynak durumu platform sorunları şey yaptım karşı ortası kullanılamazlık birbirinden mu?](#does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did)
* [Kaynak durumu my izleme araçları ile tümleştirebilir miyim?](#can-i-integrate-resource-health-with-my-monitoring-tools)
* [Kaynak durumu nereden bulabilirim?](#where-do-i-find-resource-health)
* [Kaynak durumu, tüm kaynak türleri için kullanılabilir mi?](#is-resource-health-available-for-all-resource-types)
* [Ne my kaynak kullanılabilir gösteren ancak ı değil düşünüyorsanız yapmalıyım?](#what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not)
* [Kaynak durumu için tüm Azure bölgeleri var mı?](#is-resource-health-available-for-all-azure-regions)
* [Kaynak durumu hello hizmet sağlığı panosunu veya hello Azure portal hizmeti bildirimleri farklı mı?](#how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications)
* [Her kaynak için tooactivate kaynak durumu gerekiyor mu?](#do-i-need-to-activate-resource-health-for-each-resource)
* [Tooenable kaynak durumu Kuruluşum için ihtiyacımız var?](#do-we-need-to-enable-resource-health-for-my-organization)
* [Kaynak durumu kullanılabilir ücretsiz?](#is-resource-health-available-free-of-charge)
* [Kaynak durumu sağlar hello önerileri nelerdir?](#what-are-the-recommendations-that-resource-health-provides)


## <a name="what-is-azure-resource-health"></a>Azure kaynak durumu nedir?
Kaynak Durumu, bir Azure sorunu kaynaklarınızı etkilediğinde bunu tanılamanıza ve destek almanıza yardımcı olur. Merhaba geçerli ve geçmiş kaynaklarınızın sistem durumunu hakkında bilgilendirir ve sorunları azaltmaya yardımcı olur. Kaynak Durumu, Azure hizmet sorunları ile ilgili yardıma ihtiyacınız olduğunda teknik destek sağlar.  

## <a name="what-is-hello-resource-health-intended-for"></a>Ne hello kaynak durumu yöneliktir?
Bir kaynağı ile ilgili bir sorun algıladı sonra kaynak durumu hello temel nedeni tanılamanıza yardımcı olabilir. Azure hizmet sorunları hakkında daha fazla yardıma ihtiyacınız olduğunda Yardım toomitigate hello sorun ve teknik destek sağlar.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Hangi sistem durumu denetler gerçekleştirilir kaynak durumu tarafından?
Kaynak durumu hello üzerinde göre çeşitli denetimleri gerçekleştirir [kaynak türü](resource-health-checks-resource-types.md). Bu denetimler tasarlanmış tooimplement üç sorunları türleri şunlardır: 
1. Planlanmamış olayları, örneğin bir beklenmeyen ana bilgisayar yeniden başlatma
2. Planlanan olayları ister zamanlanmış konak işletim sistemi güncelleştirmeleri
3. Bir sanal makine yeniden başlatılıyor kullanıcı örneğin kullanıcı eylemleri tarafından tetiklenen olayları

## <a name="what-does-each-of-hello-health-status-mean"></a>Her hello sistem durumunu anlamı nedir?
Üç farklı sistem durum vardır:
1. Kullanılabilir: Var olmayan herhangi bir bilinen sorun hello bu kaynak denetleyin.%nÇözüm Azure platformu
2. Kullanılabilir: Kaynak durumu hello kaynak etkileyen sorunları algıladı.
3. Bilinmeyen: hakkında bilgi alma durduğundan kaynak durumu bir kaynağın hello durumu belirlenemiyor. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>Ne bilinmeyen durum ortalama hello? My kaynakla yanlış bir şey mi?
Kaynak durumu belirli bir kaynak hakkında bilgi alma durduğunda hello sistem durumu toounknown ayarlanır. Bu durum burada sorunları yaşıyor durumlarda hello kaynak hello durumunun kesin bir gösterge olmamasına karşın Azure bir sorun olduğunu gösteriyor olabilir.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Kullanılabilir olmayan bir kaynak için nasıl Yardım alabilirim?
Merhaba kaynak sistem durumu dikey penceresinden bir destek isteği gönderebilirsiniz. Merhaba kaynak kullanılamadığında Microsoft tooopen isteği ile bir destek sözleşmesi gerekli değildir çünkü platform olaylar.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Kaynak durumu platform sorunları şey yaptım karşı ortası kullanılamazlık birbirinden mu?
Evet, bir kaynak kullanılabilir olmadığında kaynak durumu hello kök nedeni bu kategorilerden birini içinde tanımlar: 
1.  Kullanıcı tarafından başlatılan eylemi
2.  Olay 
3.  Planlanmamış olay

Merhaba Portalı'nda kullanıcı tarafından başlatılan Eylemler kırmızı bir uyarı simgesi kullanarak planlanmış ve planlanmamış olayları gösterilen sırada bir mavi bildirim simgesini kullanarak gösterilmektedir. Daha fazla ayrıntı hello sağlanan [kaynak sistem durumu genel bakış](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Kaynak durumu my izleme araçları ile tümleştirebilir miyim?
Kaynak durumu tanılamak ve kaynaklarınızı etkisi Azure hizmet sorunlarını gidermek tasarlanan hizmet toohelp ' dir. Kullanabilirsiniz ancak hello kaynak durumu API'si tooprogrammatically elde hello sistem durumu, kaynaklarınızın ölçümleri toomonitor kullanmanızı öneririz. Bir sorun algılandığında, kaynak durumu hello kök nedenini belirlemenize yardımcı olur ve Eylemler tooaddress rehberlik eder bunları. Ziyaret [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn ölçümleri toocheck kaynaklarınıza nasıl kullanabileceğiniz hakkında daha fazla bilgi.

## <a name="where-do-i-find-resource-health"></a>Kaynak durumu nereden bulabilirim?
Toohello Azure portalında oturum sonra kaynak durumu erişebilmeniz için birden çok yolu vardır:
1. Tooyour kaynak gidin. Merhaba sol gezinti bölmesinde tıklatın **kaynak durumu**.
2. Toohello Azure İzleyici dikey penceresine gidin.  Merhaba sol gezinti bölmesinde tıklatın **kaynak durumu**.
3. Açık hello **Yardım + Destek** hello sağ üst köşesindeki hello portal ve ardından seçerek hello soru işareti dikey **Yardım + Destek**. Merhaba dikey pencere açılır sonra tıklayın **kaynak durumu**

Merhaba kaynak durumu API'si tooobtain bilgilerini hello sistem kaynaklarınızın de kullanabilirsiniz.

## <a name="is-resource-health-available-for-all-resource-types"></a>Kaynak durumu, tüm kaynak türleri için kullanılabilir mi?
Merhaba sistem durumu denetimlerinin ve kaynak durumu desteklenen kaynak türleri listesi bulunabilir [burada](resource-health-checks-resource-types.md)

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>Ne my kaynak kullanılabilir gösteren ancak ı değil düşünüyorsanız yapmalıyım?"
Bir kaynağın Hello durumu denetlenirken tıklayabilirsiniz sağ hello sistem durumu altında **yanlış sistem durumu raporu**. Merhaba raporu göndermeden önce neden hello geçerli sistem durumu yanlış olduğunu düşündüğünüz hakkında ek ayrıntıları sağlayan hello seçeneğiniz vardır.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Kaynak durumu için tüm Azure bölgeleri var mı? 
Kaynak durumu bölgeleri aşağıdaki hello dışında tüm Azure geos üzerinden kullanılabilir:
* ABD Devleti Virginia
* ABD Devleti Iowa
* US DoD Doğu
* US DoD Orta
* Almanya Orta
* Almanya Kuzeydoğu
* Çin Doğu
* Çin Kuzey

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Kaynak durumu hello hizmet sağlığı panosunu veya hello Azure portal hizmeti bildirimleri farklı mı?
Kaynak durumu tarafından sağlanan hello Azure hizmet sağlığı panosunu hello tarafından sağlanan daha ayrıntılı bilgidir.

Oysa [Azure durum](https://status.azure.com) ve hello portal hizmet bildirimleri müşteriler (örneğin bir Azure bölgesi) geniş bir dizi etkileyen hizmeti sorunları hakkında bilgilendirmek, kaynak durumu yalnızca ilgili daha ayrıntılı olayları gösterir toohello belirli kaynak. Örneğin, bir ana bilgisayar beklenmedik şekilde yeniden başlatılırsa, kaynak durumu, sanal makineler Bu konakta çalışmakta olan müşteriler uyarır.

Önemli toonotice olan kaynaklarınızı etkileyen olayları görünürlüğünü tamamlamak bu tooprovide kaynak durumu aynı zamanda hizmet bildirimleri ve hello hizmet sağlığı panosunu yayımlanan olayları ortaya çıkarır.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>Her kaynak için tooactivate kaynak durumu gerekiyor mu?
Hayır, sistem durumu bilgisi, kaynak durumu kullanılabilir tüm kaynak türleri kullanılabilir. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Tooenable kaynak durumu Kuruluşum için ihtiyacımız var?
Hayır.  Azure kaynak durumu hello herhangi bir kurulum gereksinimi olmadan Azure portalı içinde erişilebilir.

## <a name="is-resource-health-available-free-of-charge"></a>Kaynak durumu kullanılabilir ücretsiz?
Evet.  Azure kaynak durumu ücretsizdir.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Kaynak durumu sağlar hello önerileri nelerdir?
Hello sistem durumuna bağlı olarak, kaynak durumu sorunlarını giderme harcanan hello süresini azaltarak hello amacı ile önerileri sağlar. Kullanılabilir kaynaklar için öneriler odaklanmayı nasıl toosolve hello en yaygın sorunları müşterilerin karşılaştığı hello. Merhaba kaynak nedeniyle kullanılamaz durumdaysa tooan Azure planlanmamış olay, hello odak olacaktır, sırasında ve sonrasında hello kurtarma işlemi yardımcı üzerinde. 

## <a name="next-steps"></a>Sonraki adımlar

Bu kaynaklar toolearn kaynak durumu hakkında daha fazla gözden geçirin:
-  [Azure kaynak sistem durumu genel bakış](Resource-health-overview.md)
-  [Azure Kaynak Durumu aracılığıyla kullanılabilen kaynak türleri ve durum denetimleri](resource-health-checks-resource-types.md)
