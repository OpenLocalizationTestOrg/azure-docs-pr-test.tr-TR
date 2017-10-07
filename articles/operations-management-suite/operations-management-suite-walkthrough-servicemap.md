---
title: "aaaService Haritası çözümü kendi kendini demo hızını belirleyebileceği | Microsoft Docs"
description: "Hizmet eşlemesi bir çözüm Operations Management Suite (OMS) Windows uygulama bileşenleri otomatik olarak bulur ve Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello.  Hizmet eşlemesi tooidentify kullanarak kılavuzluk ve bir web uygulaması sanal bir sorunu tanılamak kendini uygulanan demo budur."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Operations Management Suite (OMS) adımlı tanıtımı - Hizmet Eşlemesi
Merhaba kullanılarak üzerinden anlatan kendi kendine uygulanan demo budur [hizmet Haritası çözüm](operations-management-suite-service-map.md) Operations Management Suite (OMS) tooidentify içinde ve bir web uygulaması sanal bir sorunu tanılamak.  Hizmet eşlemesi sistemlerde, Windows ve Linux uygulama bileşenleri otomatik olarak bulur ve Hizmetleri arasındaki iletişimi eşlemeleri hello.  Ayrıca diğer OMS Hizmetleri tooassist tarafından toplanan verileri birleştirir, performans çözümleme ve sorunları tanımlar.  Ayrıca kullanacağınız [günlük analizi aramaları oturum](../log-analytics/log-analytics-log-searches.md) aşağı toodrill sırası tooidentify hello kök sorunu toplanan veriler üzerinde.


## <a name="scenario-description"></a>Senaryo açıklaması
Merhaba ACME müşteri portalı uygulaması performans sorunları yaşıyor bildirim yalnızca aldık.  sahip olduğunuz hello yalnızca bu sorunları yaklaşık 4:00:00 PST bugün başladığını bilgilerdir.  Merhaba bileşenlerinin tümünü tamamen emin değilseniz bu hello portal web sunucuları bir dizi dışında bağımlıdır.  

## <a name="components-and-features-used"></a>Kullanılan bileşenler ve özellikler
- [Hizmet Eşlemesi çözümü](operations-management-suite-service-map.md)
- [Log Analytics günlük aramaları](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>İzlenecek yol

### <a name="1-connect-toohello-oms-experience-center"></a>1. Toohello OMS deneyimi Center'a Bağlan
Bu ilerlemesi aracılığıyla hello kullanan [Operations Management Suite deneyimi Center](https://experience.mms.microsoft.com/) örnek verilerle eksiksiz bir OMS ortamı sağlar. Başlat bu bağlantıyı izleyerek, bilgilerinizi sağlayın ve ardından hello seçin **Insight and Analytics** senaryo.


### <a name="2-start-service-map"></a>2. Hizmet Eşlemesi’ni başlatma
Merhaba hizmet Haritası çözüm üzerinde hello tıklayarak Başlat **hizmet Haritası** döşeme.

![Hizmet Eşlemesi Kutucuğu](media/operations-management-suite-walkthrough-servicemap/tile.png)

Merhaba hizmet Haritası konsolunda görüntülenir.  Hello sol bölmesinde, ortamınızdaki hello hizmet Haritası aracısının yüklü olduğu bilgisayarlar listesidir.  Bu listeden tooview istediğiniz hello bilgisayarın seçersiniz.

![Bilgisayar listesi](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Bilgisayarı görüntüleme
Bu makul yer toostart gibi görünüyor şekilde hello web sunucuları AcmeWFE001 ve AcmeWFE002, adlandırılır biliyoruz.  **AcmeWFE001**’e tıklayın.  Bu, AcmeWFE001 hello harita ve tüm bağımlılıkları görüntüler.  Hangi işlemlerin hello seçili bilgisayar ve hangi çalıştıran görebilirsiniz dış Hizmetler iletişim kurar.

![Web sunucusu](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Biz web hizmetlerimizi hello performansı hakkında endişe uygulamayı şekilde hello üzerinde tıklatın **AcmeAppPool (IIS uygulama havuzu)** işlemi.  Bu, bu işlem için hello ayrıntılarını görüntüler ve bağımlılıklarını vurgular.  

![Uygulama Havuzu](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Zaman penceresini değiştirme

Biz neler o anda bir göz sahip 4: 00'da sağlandığından başlatıldı bu hello sorunu duymuş. Tıklayın **zaman aralığı** ve hello zaman too4 değiştirin: 00 AM PST (Merhaba geçerli güncel tutar ve ayarlamak için yerel saat dilimi) 20 dakika süreli.

![Saat Seçici](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Uyarı görüntüleme

Biz şimdi bu hello bkz **acmetomcat** bağımlılık bizim olası bir sorun olması için bir uyarı içeriyor.  Merhaba uyarı simgesine tıklayın **acmetomcat** tooshow hello hello uyarı ayrıntılarını.  Kritik CPU kullanımına sahip olduğumuzu görebiliriz ve daha fazla ayrıntı için uyarıyı genişletebiliriz.  Performansın yavaşlamasına neden olan sorun büyük olasılıkla budur. 

![Uyarı](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Performansı görüntüleme

Şimdi **acmetomcat**’e daha yakından bakalım.  Hello'ı tıklatın sağ üst **acmetomcat** seçip **yük Server haritasını** tooshow hello ayrıntı ve bu makine için bağımlılıkları. Biz sonra biraz daha bu performans sayaçlarını tooverify bizim şüpheyle bakabilirsiniz.  Select hello **performans** sekmesini toodisplay hello [günlük analizi tarafından toplanan performans sayaçlarını](../log-analytics/log-analytics-data-sources-performance-counters.md) hello zaman aralığı içinde.  Merhaba işlemci ve bellek düzenli ani almanızı görebiliriz.

![Performans](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Değişiklik izlemeyi görüntüleme
Bu yüksek kullanıma neyin neden olabileceğini bulabilecek miyiz, görelim.  Tıklatın hello üzerinde **Özet** sekmesi.  Bu OMS hello bilgisayardan gibi topladı bilgiler bağlantıları, kritik uyarılar ve yazılım değişikliği başarısız oldu sağlar.  Bölümler ilginç en son bilgilerle zaten genişletilmesini ve içerdikleri diğer bölümleri tooinspect bilgileri genişletebilirsiniz.


**Değişiklik İzleme** henüz açık değilse genişletin.  Bu hello tarafından toplanan bilgiler gösterir [değişiklik izleme çözümü](../log-analytics/log-analytics-change-tracking.md).  Bu zaman penceresinde bir yazılım değişikliği yapılmış gibi görünüyor.  Tıklayın **yazılım** tooget ayrıntıları.  Bu toobe hello sorunlu tüketilen hello aşırı kaynaklar için görünmesi bir yedekleme işlemi yalnızca 4: 00'da sonra toohello makine eklendi.

![Değişiklik izleme](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Günlük Araması’nda ayrıntıları görüntüleme
Size daha fazla bu hello bakarak doğrulayabilirsiniz ayrıntılı hello günlük analizi deposunda toplanan performans bilgileri.  Üzerinde hello'ı tıklatın **uyarıları** yeniden sekmesini ve ardından hello birini **yüksek CPU** uyarıları.  **Günlük Aramasında Göster**’e tıklayın.  Burada gerçekleştirebilirsiniz hello günlük arama penceresi açılır [oturum aramaları](../log-analytics/log-analytics-log-searches.md) hello deposunda depolanan tüm verileri karşı.  Hizmet bir queriy bize doldurulmuş Haritası tooretrieve hello uyarı ilginizi çalışıyoruz.  

![Günlük araması](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Kayıtlı aramayı açma
Biz bu uyarıyı üreten hello performans toplama üzerinde biraz daha fazla ayrıntı almak ve bu yedekleme işlemi tarafından hello sorunlara neden bizim şüpheyle doğrulayın görelim.  Merhaba zaman aralığı çok değiştirme**6 saat**.  Tıklayın **Sık Kullanılanlar** ve toohello Kaydedilmiş aramaları için aşağı kaydırın **hizmet Haritası**.  Bunlar özellikle bu analiz için oluşturduğumuz sorgulardır.  **Acmetomcat için CPU’ya Göre İlk 5 İşlem**’e tıklayın.

![Kayıtlı arama](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


İlk 5 işlemleri üzerindeki işlemci tüketen hello listesini bu sorgunun döndürdüğü **acmetomcat**.  Merhaba sorgu tooget günlük aramalar için kullanılan bir giriş toohello sorgu dili inceleyebilirsiniz.  Diğer bilgisayarlarda hello işlemlerini ilginizi olsaydı, bu bilgileri hello sorgu tooretrieve değiştirebilir.

Bu durumda, biz hello yedekleme işlemi tutarlı bir şekilde hello uygulama sunucusunun CPU % 60'hakkında tüketen görebilirsiniz.  Performans sorunumuzdan bu yeni işlemin sorumlu olduğu son derece açıktır.  Çözümümüzdür açıkça tooremove bu yeni olacaktır yedekleme yazılımını hello uygulama sunucusu kapalı.  İstenen durum yapılandırması (DSC) bu işlemi hiçbir zaman bu kritik sistemlerinde çalıştırılan olun Azure Otomasyonu toodefine ilkelerine göre yönetilen gerçekte nden.


## <a name="summary-points"></a>Özet maddeleri
- [Hizmet Eşlemesi](operations-management-suite-service-map.md), tüm sunucu ve bağımlılıklarını bilmeseniz bile tüm uygulamanızın görünümünü sağlar.
- Hizmet eşlemesi ortaya çıkarır veri diğer OMS çözümleri toohelp tarafından toplanan sorunlar uygulamanız ve onun altyapının tanımlarsınız.
- [Oturum aramaları](../log-analytics/log-analytics-log-searches.md) toodrill aşağı hello günlük analizi deposunda toplanan belirli veri sağlar.    

## <a name="next-steps"></a>Sonraki adımlar
- [Hizmet Eşlemesi](operations-management-suite-service-map.md) hakkında daha fazla bilgi edinin.
- Hizmet Eşlemesini [dağıtın ve yapılandırın](operations-management-suite-service-map-configure.md).
- Hizmet Eşlemesi için gereken ve aracılar tarafından depolanan işlem verilerini kaydeden [Log Analytics](../log-analytics/log-analytics-overview.md) hakkında bilgi edinin.