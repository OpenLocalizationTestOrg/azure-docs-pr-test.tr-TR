---
title: "Azure CDN kullanım desenlerini çözümleme | Microsoft Docs"
description: "Aşağıdaki raporlar kullanarak, CDN için kullanım desenlerini görüntüleyebilirsiniz: bant genişliği, aktarılan verileri, isabet, önbellek durumları, önbellek isabet oranı, IPv4/IPv6 aktarılan veriler."
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
ms.openlocfilehash: aadbe872dd3384c8d337b432fb3be69422ca322b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Azure CDN kullanım desenlerini Çözümle

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Kılavuzu Verizon profilleri Yönet Portalı aracılığıyla çekirdek raporları görüntülemek için adımları geçer. Ayrıca depolama, olay hub'ı temel analiz verileri dışarı aktarma veya Verizon ve Akamai profilleri için günlük analizi (oms) [azure portalı üzerinden](cdn-log-analysis.md).

Aşağıdaki raporlar kullanarak, CDN için kullanım desenlerini görüntüleyebilirsiniz:

* Bant Genişliği
* Aktarılan veriler
* İsabet sayısı
* Önbellek durumları
* İsabetli Önbellek okuması oranı
* IPv4/IPv6 veri aktarma

## <a name="accessing-core-reports"></a>Çekirdek raporları erişme
1. CDN profili dikey penceresinden tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-reports/cdn-manage-btn.png)
   
    CDN Yönetim Portalı'nı açar.
2. Üzerine gelerek **Analytics** sekmesini ve ardından üzerine gelerek **çekirdek raporları** çıkma.  İstenen rapor menüde tıklayın.
   
    ![CDN Yönetim Portalı - çekirdek Raporlar menüsü](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Bant Genişliği
Bant genişliği raporun belirli bir süre boyunca HTTP ve HTTPS için bant genişliği kullanımını gösteren bir grafik ve veri tablosu oluşur. Tüm CDN POP veya belirli bir POP arasında bant genişliği kullanımını görüntüleyebilirsiniz. Bu, CDN POP MB/sn cinsinden arasında trafiği ani ve dağıtım görüntülemenize olanak sağlar.

* Belirli bir bölge/düğüm açılır listeden seçin veya tüm düğümlerde gelen trafiği görmek için tüm kenar düğümleri seçin.
* Veri bugün/bu hafta için/bu ay, vb. görüntülemek veya özel tarihleri girin, ardından "seçiminizi güncelleştirildiğinden emin olmak için Git"'i tıklatın tarih aralığını seçin.
* Dışarı aktarma ve veri "Git" yanında bulunan excel sayfası simgesini tıklatarak yükleyin.

Rapor her 5 dakikada bir güncelleştirilir.

![Bant genişliği raporu](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Aktarılan veriler
Bu rapor belirli bir süre boyunca HTTP ve HTTPS trafiği kullanım gösteren bir grafik ve veri tablo oluşur. Tüm CDN POP veya belirli bir POP üzerinden trafik kullanım görüntüleyebilirsiniz. Bu, CDN POP GB arasında trafiği ani ve dağıtım görüntülemenize olanak sağlar.

* Belirli bir bölge/düğüm açılır listeden seçin veya tüm notları gelen trafiği görmek için tüm kenar düğümleri seçin.
* Veri bugün/bu hafta için/bu ay, vb. görüntülemek veya özel tarihleri girin, ardından "seçiminizi güncelleştirildiğinden emin olmak için Git"'i tıklatın tarih aralığını seçin.
* Dışarı aktarma ve veri "Git" yanında bulunan excel sayfası simgesini tıklatarak yükleyin.

Rapor her 5 dakikada bir güncelleştirilir.

![Rapor aktarılan veriler](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>İsabet (durum kodu)
Bu rapor içeriğiniz için isteği durum kodları dağıtımını açıklar. İçerik için her istek HTTP durum kodu oluşturur. Durum kodu kenar POP isteğin nasıl işleneceğini açıklar. Örneğin, bir 4xx durum kodu bir hata oluştu göstergesidir isteğin başarılı bir şekilde bir istemciye sunulduğu 2xx durum kodları belirtin. HTTP durum kodu hakkında daha fazla ayrıntı için bkz: [durum kodları](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Veri bugün/bu hafta için/bu ay, vb. görüntülemek veya özel tarihleri girin, ardından "seçiminizi güncelleştirildiğinden emin olmak için Git"'i tıklatın tarih aralığını seçin.
* Dışarı aktarma ve "Git" yanında bulunan excel sayfası tıklayarak veri indirin.

![İsabet raporu](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Önbellek durumları
Bu rapor İsabetli Önbellek okuma sayısı ve istemci isteği için İsabetsiz Önbellek okuma sayısı dağıtımını açıklar. Hızlı performans Önbelleği İsabetli Okuma gelen olduğundan, veri teslim hızlarını en aza İsabetsiz Önbellek okuma sayısı ve süresi dolan önbelleği isabetli okuma en iyi duruma getirebilirsiniz. İsabetsiz önbellek okuma sayısı "no-cache" yanıt üstbilgilerini atama önlemek için kaynak sunucunuzu yapılandırma, kesinlikle gerekli olduğunda sorgu dizesi önbelleğe önleme ve alınabilir olmayan yanıt kodları önleme azaltılabilir. Bir varlık yaparak isabet önlenebilir önbellek süresi dolan istekleri kaynak sunucuya sayısını en aza indirmek için mümkün olan en kısa sürece, max-age.

![Önbellek durumları raporu](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Ana önbellek durumlar şunlardır:
* TCP_HIT: Kenarından sundu. Nesne Önbelleği'nde olduğu ve onun Maksimum yaş aşmıştı değil.
* TCP_MISS: Kaynaktan sundu. Nesne önbellekte değil ve yanıt geri kaynağa olmuştur.
* TCP_EXPIRED _MISS: kaynağına sahip COLLECTION sonra kaynaktan alınan hizmet. Nesne önbelleğinde oldu, ancak kendi max-age aşmıştı. Yeniden doğrulanması kaynağına sahip yeni bir yanıt kaynaktan tarafından değiştirilen önbellek nesnesi ile sonuçlandı.
* TCP_EXPIRED _HIT: kaynağına sahip COLLECTION sonra kenarından hizmet. Nesne önbelleğinde oldu, ancak kendi max-age aşmıştı. Kaynak sunucu ile yeniden doğrulanması değiştirilmemiş önbellek nesnesinde sonuçlandı.
* Veri bugün/bu hafta için/bu ay, vb. görüntülemek veya özel tarihleri girin, ardından "seçiminizi güncelleştirildiğinden emin olmak için Git"'i tıklatın tarih aralığını seçin.
* Dışarı aktarma ve veri "Git" yanında bulunan excel sayfası simgesini tıklatarak yükleyin.

### <a name="full-list-of-cache-statuses"></a>Önbellek durumları tam listesi
* TCP_HIT - bir istek istemciye doğrudan POP sunulduğunda bu durum bildirilir. Bir varlık, bir istemcinin en yakın POP önbelleğe alınır ve geçerli bir yaşam süresi bulunduğunda POP veya TTL hemen sunulur. TTL aşağıdaki yanıt üstbilgileri tarafından belirlenir:
  
  * Cache-Control: s-maxage
  * Cache-Control:, max-age
  * Süre sonu
* TCP_MISS - bu durum, istenen varlık önbelleğe alınmış bir sürümü, istemcinin en yakın POP üzerinde bulunamadı gösterir. Varlık, kaynak sunucu veya bir kaynak kalkan sunucu istenecektir. Kaynak sunucu veya kaynak kalkan sunucu bir varlık döndürürse, istemciye hizmet ve hem istemci hem de edge sunucusunda önbelleğe alınır. Aksi takdirde, 200 durum kodu (örn., 403 Yasak, 404 bulunamadı, vb.) döndürülür.
* TCP_EXPIRED _HIT - bir varlığı zaman varlığın max-age süresi doldu gibi bir süresi dolan TTL hedeflenen bir isteğin doğrudan POP istemciye sunulduğu, bu durum bildirilir.
  
    Süresi dolmuş bir isteği yeniden doğrulanması istekte kaynak sunucuya genellikle sonuçlanır. Sırayla gerçekleşmesi TCP_EXPIRED _HIT için kaynak sunucuyu varlık daha yeni bir sürümü mevcut değil belirtmeniz gerekir. Böyle bir durum, genellikle bu varlığın Cache-Control ve Expires üstbilgileri güncelleştirir.
* TCP_EXPIRED _MISS - süresi dolmuş bir önbelleğe alınan varlık daha yeni bir sürümü istemciye POP sunulduğunda bu durum bildirilir. Önbelleğe alınan bir varlık için TTL'nin süresi doldu bu durum oluşur (örn., max-age süresi) ve kaynak sunucu, varlık, yeni bir sürümünü döndürür. Varlık bu yeni sürümü, önbelleğe alınan sürümü yerine istemciye sunulacak. Ayrıca, bu uç sunucusunu ve istemcide önbelleğe alınır.
* CONFIG_NOCACHE - bu durum, bizim kenar POP müşteriye özgü yapılandırmasına önbelleğe alınması varlık engelledi gösterir.
* HİÇBİRİ - bu durum, bir önbellek içerik yenilik denetimi gerçekleştirilmemiş gösterir.
* TCP_ CLIENT_REFRESH _MISS - bir HTTP istemcisi (örn., tarayıcı) eski varlık yeni bir sürümü kaynak sunucudan almak üzere POP kenar zorlar, bu durum bildirilir.
  
    Varsayılan olarak, kaynak sunucudan veri varlığı yeni bir sürümünü almak için kenar sunucularımızda zorlama sunucularımızda bir HTTP istemci engeller.
* TCP_ PARTIAL_HIT - vuruş kısmen önbelleğe alınmış bir varlık için bir bayt aralığı isteği sonuçlanır olduğunda bu durum bildirilir. İstenen bayt aralığı, istemciye POP hemen sunulur.
* UNCACHEABLE - bir varlığın Cache-Control ve Expires üstbilgileri belirttiğinizde, POP veya HTTP istemci tarafından önbelleğe alınması gereken değil, bu durum bildirilir. Bu tür istekleri kaynak sunucudan hizmet alır

## <a name="cache-hit-ratio"></a>İsabetli Önbellek okuması oranı
Bu rapor, doğrudan önbelleğinden sunulduğunu önbelleğe alınan istek sayısı yüzdesini gösterir.

Bu rapor, aşağıdaki ayrıntıları sağlar:

* İstenen içerik istemciye en yakın POP önbelleğe alınmadı.
* İsteğin doğrudan sunduğumuz ağ kenarından sunulduğu.
* İstek yeniden doğrulanması kaynak sunucu ile gerekli değil.

Raporun içermez:

* Ülke filtreleme seçeneklerini nedeniyle reddedildi istek sayısı.
* Bunlar değil konumlandırılmalıdır başlıklarını belirtmek varlıklar için istek sayısı. Örneğin, Cache-Control: özel, Cache-Control: no-cache veya Pragma: no-cache üstbilgileri, bir varlık önbelleğe alınmasını engeller.
* Kısmen önbelleğe alınmış içeriği için bayt aralığı isteklerini.

Formül: (TCP_ İSABET / (TCP_ İSABET + TCP_MISS)) * 100

* Veri bugün/bu hafta için/bu ay, vb. görüntülemek veya özel tarihleri girin, ardından "seçiminizi güncelleştirildiğinden emin olmak için Git"'i tıklatın tarih aralığını seçin.
* Dışarı aktarma ve veri "Git" yanında bulunan excel sayfası simgesini tıklatarak yükleyin.

![İsabetli Önbellek okuması oranı raporu](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>IPv4/IPv6 aktarılan veriler
Bu rapor, IPv4 vs IPv6 trafiği kullanım dağılımını gösterir.

![IPv4/IPv6 aktarılan veriler](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Özel tarih girmek veya veri bugün/bu hafta için/bu ay, vb. görüntülemek için tarih aralığını seçin.
* Sonra seçiminizi güncelleştirildiğinden emin olmak için "Git"'i tıklatın.

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Raporları yalnızca son 18 ay içinde oluşturulabilir.

