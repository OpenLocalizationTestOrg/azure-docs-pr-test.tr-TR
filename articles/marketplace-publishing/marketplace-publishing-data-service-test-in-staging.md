---
title: Veri Hizmeti Merhaba Market teklifi aaaTesting | Microsoft Docs
description: "Nasıl tootest, veri hizmeti sunan hello Azure Marketi anlayın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Veri Hizmeti teklifiniz hazırlamada test etme
> [!IMPORTANT]
> **Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.** Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners). Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Merhaba ilk iki adımları tamamladıktan sonra [, Microsoft Developer hesabı oluşturma](marketplace-publishing-accounts-creation-registration.md) ve [yayımlama portalında oluşturma, veri hizmeti sunan](marketplace-publishing-data-service-creation.md) teklifiniz hello kullanılabilir yapmak için hazır Azure Market. Bu konuda hello ilk adım, Orta, çağrılan "Hazırlama" adım

Hazırlama teklifiniz özel ", test ve tooproduction göndermeden önce işlevselliğini doğrulayın sandbox" dağıtma anlamına gelir. Merhaba teklif hazırlama dağıtmış olan tooa müşteri gibi görünür.

## <a name="step-1-pushing-your-offer-toostaging"></a>1. Adım Teklif toostaging iletme
Teklif toostaging Ftp'den kullanılabilir toofuture aboneleri duruma gelmesi tootest hello teklif da sağlar.  Teklifiniz nasıl görüntülenir ve tooyour veri abone olanlar için işlev görebilirsiniz.  

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Merhaba oturum [Yayımlama Portalı](https://publish.windowsazure.com)
2. Seçin **Veri Hizmetleri** hello sol gezinti penceresinde
3. Teklifiniz toopush toostaging istediğinizi seçin. Başlangıç ekranı üzerinde görürsünüz.
4. Tıklatın **anında tooStaging** düğmesi.  
5. Bir sorun varsa ile Merhaba önceki toopushing toostaging toobe gerekli teklif tamamlandı, görüntülenen bir listesini görürsünüz.  Bu öğeler hello listedeki her öğeye tıklayarak düzeltin. Yapılan, tüm düzeltmeler tıklattığınızda **anında tooStaging** yeniden düğmesine tıklayın.

Teklifiniz hiçbir sorun varsa hello açılır pencere görürsünüz.  

Siz değilseniz, planlama değil onaylanan toosurface teklifiniz Azure Portalı'nda (şu anda sınırlı kapasite), sonra yalnızca Kapat hello açılır penceresi.

tootest, verilerinizi Azure Portalı'nda (toplama toohello DataMarket Portalı'nda) hizmet ile bir Azure abonelik kimliği tootest gerekir.  Bu abonelik kimliği olacak hello hesabını tanımlayacak tootest teklifiniz izin verilir.  

Kesme ve abonelik Kimliğinizi yapıştırın ve hello onay işareti toocontinue'ı tıklatın.

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Bu Azure abonelik kimlikleri yalnızca olan test etme ve hello hazırlama için gereken [Azure Yönetim Portalı](https://manage.windowsazure.com). Bunlar Azure markette gerekli tootest değildir.
> 
> 

Merhaba görüntülenen sonraki ekranında yayımlama hello "Sürüyor" görüntüleyerek yer aldığını gösterir simgesi sarı aşağıdaki vurgulanır. Toostaging Ftp'den arasında 10 too15 dakika sürer.  İlk uzun sürüyorsa, tarayıcınızı (IE içinde F5 tuşuna basın) yenileyin.  Burada teklifiniz hala toostaging bir saat sonra Ftp'den olduğu hello nadir durumlarda, bize bir sorun olduğunu bize toolet bağlantı hello kişiyi tıklatın.

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Merhaba itme tooStaging hello tamamlandığında "Sürüyor" taşıma simgesi durdurur ve çok "hazırlanmış" Merhaba durumu güncelleştirilir.  Artık hazır tootest teklifiniz şunlardır.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>2. Adım DataMarket içinde hazırlanmış teklifiniz test
Merhaba metin aşağıdaki hello bağlantısına tıklayın **"adresindeki teklif hizmetinizi bkz..."** Abone hello toodisplay Merhaba ekranında teklifiniz tooproduction gittiğinde görürsünüz ve DataMarket içinde görüntülenir.

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Test veya hello 12 öğelerin her birini tooensure olarak işaretlenmiş tüm logolar, Fiyatlar/işlemleri, metin, görüntüler, belgeleri ve bağlantıları düzgün doğru ve çalışıyor olduğunu doğrulayın.  Teklifiniz oluştururken girdiğiniz tüm test değerleri gerçek değerlerle değiştirilmiştir iyi zaman tooensure budur.

1. Teklif logosu
2. Teklif adı
3. Yayımcı adı/bağlantı tooyour şirketinizin Web sitesi
4. Teklifiniz için arama kategorileri
5. Teklifiniz 's destek bağlantı tooassist aboneleri
6. Teklifiniz için bağlamsal açıklaması
7. Fatura Ayrıntıları gösteren teklif planı
8. Bağlantı tooimplementation kodu
9. Teklif verilerini gösteren örnek görüntüleri kullanın
10. Merhaba teklif içinde her hizmet için giriş/çıkış meta verileri
11. Teklif'ın kullanım koşulları
12. Merhaba teklif'ın veri önizlemesi

Son olarak, onay hello hizmeti, "Keşfedin bu veri KÜMESİ" Merhaba bağlantıyı tıklatarak Datamarket hello çalışır.  Yeni bir pencerede açılır hizmetinize karşı hello bir sorgunun sonuçlarını önizlemek için hello aracında "Hizmet Gezgini" diyoruz.  Bu pencerede, parametreleri gerektiği ve hizmetinizi sorgusundan görüntülenen hello sonuçları görmek hello girebilirsiniz.   Ayrıca, görüntülenen hello URL sorgunuz için geçerlidir.  

> [!NOTE]
> Hello üstünde görüntülenen hello hizmetinin emin tooreview hello metinsel açıklaması olabilir.  Teklifiniz birden fazla hizmeti oluşur, çağrı, hello alt tooswitch toohello sonraki hizmet tooreview hello sekmeleri tıklatın ve test.
> 
> 

## <a name="next-step"></a>Sonraki adım
Sorunu yaşıyor ve Yardım ihtiyacınız varsa bunları çözme Lütfen kişi [Azure yayımcı desteğine](http://go.microsoft.com/fwlink/?LinkId=272975).

Memnun ve hazır toopublish teklifiniz okuyun hello [isteği onayı tooPush tooProduction](marketplace-publishing-push-to-production.md) belgeleri.

## <a name="see-also"></a>Ayrıca Bkz.
* [Başlarken: Nasıl toopublish bir teklif toohello Azure Market](marketplace-publishing-getting-started.md)

