---
title: "aaaAnalyze Azure CDN kullanım desenlerini | Microsoft Docs"
description: "Raporlar aşağıdaki hello kullanarak, CDN için kullanım desenlerini görüntüleyebilirsiniz: bant genişliği, aktarılan verileri, isabet, önbellek durumları, önbellek isabet oranı, IPv4/IPv6 aktarılan veriler."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Azure CDN kullanım desenlerini Çözümle

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Merhaba kılavuzu aşağıdaki hello adımları tooview hello çekirdek raporlarda Verizon profilleri için hello Yönet portalı üzerinden gider. Çekirdek analytics veri toostorage, olay hub'ı veya Verizon ve Akamai profilleri için günlük analizi (oms) da verebilirsiniz [hello azure portalı üzerinden](cdn-log-analysis.md).

Raporlar aşağıdaki hello kullanarak, CDN için kullanım desenlerini görüntüleyebilirsiniz:

* Bant Genişliği
* Aktarılan veriler
* İsabet sayısı
* Önbellek durumları
* İsabetli Önbellek okuması oranı
* IPv4/IPv6 veri aktarma

## <a name="accessing-core-reports"></a>Çekirdek raporları erişme
1. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-reports/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **çekirdek raporları** çıkma.  Merhaba menü hello istenen rapora tıklayın.
   
    ![CDN Yönetim Portalı - çekirdek Raporlar menüsü](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Bant Genişliği
HTTP ve HTTPS için belirli bir süre boyunca hello bant genişliği kullanımını gösteren bir grafik ve veri tablosu Hello bant genişliği rapor oluşur. Tüm CDN POP veya belirli bir POP üzerinden hello bant genişliği kullanımını görüntüleyebilirsiniz. Bu, tooview hello trafiği ani ve dağıtım CDN POP MB/sn cinsinden arasında sağlar.

* Tüm kenar düğümleri toosee trafiği tüm düğümlerdeki veya belirli bir bölge/düğüm hello açılır listeden seçin.
* Tarih aralığı tooview verileri bugün/bu hafta için/bu ay, vb. veya özel tarihleri girin, seçip toomake seçiminizi güncelleştirildiğinden emin "Git"'i tıklatın.
* Dışarı aktarabilir ve Başlangıç'ı tıklatarak yükleme hello veri excel sonraki sayfa simgesini "gidin" çok.

Merhaba rapor her 5 dakikada bir güncelleştirilir.

![Bant genişliği raporu](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Aktarılan veriler
Bu rapor hello trafiği kullanım HTTP ve HTTPS için belirli bir süre boyunca gösteren bir grafik ve veri tablosu oluşur. Tüm CDN POP veya belirli bir POP üzerinden hello trafiği kullanım görüntüleyebilirsiniz. Bu, tooview hello trafiği ani ve dağıtım CDN POP GB arasında sağlar.

* Tüm kenar düğümleri toosee trafiği tüm notlarını veya belirli bir bölge/düğüm hello açılır listeden seçin.
* Tarih aralığı tooview verileri bugün/bu hafta için/bu ay, vb. veya özel tarihleri girin, seçip toomake seçiminizi güncelleştirildiğinden emin "Git"'i tıklatın.
* Dışarı aktarabilir ve Başlangıç'ı tıklatarak yükleme hello veri excel sonraki sayfa simgesini "gidin" çok.

Merhaba rapor her 5 dakikada bir güncelleştirilir.

![Rapor aktarılan veriler](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>İsabet (durum kodu)
Bu rapor içeriğiniz için isteği durum kodları hello dağıtımını açıklar. İçerik için her istek HTTP durum kodu oluşturur. Merhaba durum kodu kenar POP hello isteğin nasıl işleneceğini açıklar. Örneğin, bir 4xx durum kodu bir hata oluştu göstergesidir bu hello isteği başarıyla tooa istemci sunulduğu 2xx durum kodları belirtin. HTTP durum kodu hakkında daha fazla ayrıntı için bkz: [durum kodları](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Tarih aralığı tooview verileri bugün/bu hafta için/bu ay, vb. veya özel tarihleri girin, seçip toomake seçiminizi güncelleştirildiğinden emin "Git"'i tıklatın.
* Dışarı aktarabilir ve hello tıklayarak indirme hello veri excel sonraki bulunan sayfası "gidin" çok.

![İsabet raporu](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Önbellek durumları
Bu rapor İsabetli Önbellek okuma sayısı ve istemci isteği için İsabetsiz Önbellek okuma sayısı hello dağıtımını açıklar. Hello hızlı performans Önbelleği İsabetli Okuma gelen olduğundan, veri teslim hızlarını en aza İsabetsiz Önbellek okuma sayısı ve süresi dolan Önbelleği İsabetli Okuma göre en iyi duruma getirebilirsiniz. İsabetsiz önbellek okuma sayısı "no-cache" yanıt üstbilgilerini atama, kaynak sunucu tooavoid yapılandırma, kesinlikle gerekli olduğunda sorgu dizesi önbelleğe önleme ve alınabilir olmayan yanıt kodları önleme azaltılabilir. Önbelleği isabetli okuma isteklerinin toohello kaynak sunucu sayısını olası toominimize hello sürece, bir varlığın max-age yaparak önlenebilir süresi doldu.

![Önbellek durumları raporu](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Ana önbellek durumlar şunlardır:
* TCP_HIT: Kenarından sundu. Hello Nesne Önbelleği'nde olduğu ve onun Maksimum yaş aşmıştı değil.
* TCP_MISS: Kaynaktan sundu. Merhaba nesne önbellekte değil ve hello yanıt geri tooorigin olmuştur.
* TCP_EXPIRED _MISS: kaynağına sahip COLLECTION sonra kaynaktan alınan hizmet. Merhaba Nesne önbelleğinde oldu, ancak kendi max-age aşmıştı. Yeniden doğrulanması kaynağına sahip yeni bir yanıt kaynaktan tarafından değiştirilen hello önbellek nesnesi ile sonuçlandı.
* TCP_EXPIRED _HIT: kaynağına sahip COLLECTION sonra kenarından hizmet. Merhaba Nesne önbelleğinde oldu, ancak kendi max-age aşmıştı. Değiştirilmemiş hello önbellek nesnesinde COLLECTION hello kaynak sunucu ile sonuçlandı.
* Tarih aralığı tooview verileri bugün/bu hafta için/bu ay, vb. veya özel tarihleri girin, seçip toomake seçiminizi güncelleştirildiğinden emin "Git"'i tıklatın.
* Dışarı aktarabilir ve Başlangıç'ı tıklatarak yükleme hello veri excel sonraki sayfa simgesini "gidin" çok.

### <a name="full-list-of-cache-statuses"></a>Önbellek durumları tam listesi
* TCP_HIT - bir istek doğrudan hello POP toohello istemciden sunulduğunda bu durum bildirilir. Bir varlık hemen bir hello POP en yakın toohello istemcide önbelleğe alınır ve geçerli bir yaşam süresi bulunduğunda POP veya TTL sunulur. TTL yanıt üstbilgilerini aşağıdaki hello tarafından belirlenir:
  
  * Cache-Control: s-maxage
  * Cache-Control:, max-age
  * Süre sonu
* TCP_MISS - bu durum, önbelleğe alınan bir hello istenen varlık sürümü hello POP en yakın toohello istemcide bulunamadı gösterir. Merhaba varlık, kaynak sunucu veya bir kaynak kalkan sunucu istenecektir. Merhaba kaynak sunucu veya hello kaynak kalkan sunucu bir varlık döndürürse, toohello istemci sunulan ve hem hello istemci hem de hello edge sunucusunda önbelleğe alınır. Aksi takdirde, 200 durum kodu (örn., 403 Yasak, 404 bulunamadı, vb.) döndürülür.
* TCP_EXPIRED _HIT - doğrudan hello POP toohello istemciden bir varlığı zaman hello varlığın max-age süresi doldu gibi bir süresi dolan TTL hedeflenen bir isteğin sunulduğu, bu durum bildirilir.
  
    Süresi dolmuş istek genellikle bir yeniden doğrulanması isteği toohello kaynak sunucu sonuçlanır. TCP_EXPIRED _HIT toooccur için sırayla hello varlık daha yeni bir sürümü mevcut değil hello kaynak sunucuyu belirtmeniz gerekir. Böyle bir durum, genellikle bu varlığın Cache-Control ve Expires üstbilgileri güncelleştirir.
* TCP_EXPIRED _MISS - süresi dolmuş bir önbelleğe alınan varlık daha yeni bir sürümü hello POP toohello istemciden sunulduğunda bu durum bildirilir. Önbelleğe alınmış bir varlık için Hello TTL süresi doldu bu durum oluşur (örn., max-age süresi) ve hello kaynak sunucu, varlık, yeni bir sürümünü döndürür. Merhaba varlık bu yeni sürümü toohello istemci hello önbelleğe alınmış sürümü yerine sunulacak. Ayrıca, bu hello uç sunucusu ve hello istemci önbelleğe alınır.
* CONFIG_NOCACHE - bu durum, bizim kenar POP müşteriye özgü yapılandırmasına önbelleğe alınması hello varlık engelledi gösterir.
* HİÇBİRİ - bu durum, bir önbellek içerik yenilik denetimi gerçekleştirilmemiş gösterir.
* TCP_ CLIENT_REFRESH _MISS - bir HTTP istemcisi (örn., tarayıcı) kenar POP tooretrieve eski varlık yeni bir sürümü hello kaynak sunucudan zorlar, bu durum bildirilir.
  
    Varsayılan olarak, hello kaynak sunucudan bizim kenar sunucuları tooretrieve hello varlık yeni bir sürümü zorlama sunucularımızda bir HTTP istemcisi engeller.
* TCP_ PARTIAL_HIT - vuruş kısmen önbelleğe alınmış bir varlık için bir bayt aralığı isteği sonuçlanır olduğunda bu durum bildirilir. Merhaba bayt aralığı hemen hello POP toohello istemciden sunulan istedi.
* UNCACHEABLE -, POP veya hello HTTP istemci tarafından önbelleğe alınması gereken değil, bir varlığın Cache-Control ve Expires üstbilgileri belirtmek, bu durum bildirilir. Bu tür istekleri hello kaynak sunucudan hizmet alır

## <a name="cache-hit-ratio"></a>İsabetli Önbellek okuması oranı
Bu rapor, doğrudan önbelleğinden sunulduğunu önbelleğe alınan istek sayısı hello yüzdesini gösterir.

Merhaba rapor aşağıdaki ayrıntılara hello sağlar:

* Merhaba, içerik hello POP en yakın toohello isteyenin üzerinde önbelleğe istedi.
* Merhaba isteğin doğrudan hello kenarından ağımız sunulduğu.
* Merhaba istek COLLECTION hello kaynak sunucu ile gerekli değil.

Merhaba rapor içermez:

* Toocountry filtreleme seçenekleri reddedilen istek sayısı.
* Bunlar değil konumlandırılmalıdır başlıklarını belirtmek varlıklar için istek sayısı. Örneğin, Cache-Control: özel, Cache-Control: no-cache veya Pragma: no-cache üstbilgileri, bir varlık önbelleğe alınmasını engeller.
* Kısmen önbelleğe alınmış içeriği için bayt aralığı isteklerini.

Merhaba formül: (TCP_ İSABET / (TCP_ İSABET + TCP_MISS)) * 100

* Tarih aralığı tooview verileri bugün/bu hafta için/bu ay, vb. veya özel tarihleri girin, seçip toomake seçiminizi güncelleştirildiğinden emin "Git"'i tıklatın.
* Dışarı aktarabilir ve Başlangıç'ı tıklatarak yükleme hello veri excel sonraki sayfa simgesini "gidin" çok.

![İsabetli Önbellek okuması oranı raporu](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>IPv4/IPv6 aktarılan veriler
Bu rapor, IPv4 vs IPv6 hello trafiği kullanım dağılımını gösterir.

![IPv4/IPv6 aktarılan veriler](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Tarih aralığı tooview verileri bugün/bu hafta için/bu ay, vb. seçin veya özel tarihleri girin.
* Toomake seçiminizi güncelleştirildiğinden emin "Git"'ye tıklayın.

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Raporları yalnızca son 18 ay içinde hello oluşturulabilir.

