---
title: "en iyi duruma getirme hello Azure içerik teslim ağı aracılığıyla akış aaaMedia"
description: "Akış medya dosyaları kesintisiz teslim için en iyi duruma getirme"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>En iyi duruma getirme hello Azure içerik teslim ağı üzerinden akış medyası 
 
Yüksek tanımlı video kullanımını hello büyük dosyaların verimli bir şekilde teslim sorunlar oluşturur Internet üzerinde artmaktadır. Müşteriler, isteğe bağlı video kesintisiz çalınmasını beklediğiniz veya ağları ve istemcilerin çeşitli video varlıklar Merhaba Dünya çapında canlı. Medya dosyaları için hızlı ve verimli teslim mekanizması kritik tooensure kesintisiz ve eğlenceli Müşteri Deneyimi ' dir.  

Canlı akış medya özellikle zor toodeliver hello büyük boyutları ve eşzamanlı görüntüleyiciler sayısı nedeniyle var. Kullanıcıların tooleave uzun gecikmelere neden. Canlı akışlar önceden önbelleğe alınamaz ve büyük gecikme kabul edilebilir tooviewers değil çünkü video parçaları zamanında teslim edilmelidir. 

Akış hello istek desenlerini yeni zorluklar ortaya de sağlar. Popüler bir canlı akışı veya yeni bir seri serbest bırakıldığında için isteğe bağlı video olarak binlerce görüntüleyiciler toomillions hello hello akış isteği aynı anda. Bu durumda, birleştirme önemli toonot olan akıllı isteği doldurmaya hello kaynak sunucuları hello varlıklar henüz önbelleğe olmayan alındığında.
 
Merhaba akamai'den Azure içerik teslim ağı şimdi akış medya varlıklar toousers verimli bir şekilde ölçekli Merhaba dünya genelinde sunan bir özellik sunar. hello yük hello kaynak sunucularda azalttığı hello özelliği gecikmelerini azaltır. Bu özellik hello standart Akamai fiyatlandırma katmanı ile kullanılabilir. 

Merhaba verizon'dan Azure içerik teslim ağı akış medya doğrudan hello genel web teslim en iyi duruma getirme türü sunar.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Bir uç nokta toooptimize medya hello Azure içerik teslim ağı akamai'den akışı yapılandırma
 
İçerik teslim ağı (CDN) uç noktası toooptimize teslim hello Azure portal aracılığıyla büyük dosyalar için yapılandırabilirsiniz. Herhangi bir istemci SDK'ları toodo bu hello veya bizim REST API de kullanabilirsiniz. Merhaba aşağıdaki adımlarda hello Azure portal aracılığıyla hello işlemi gösterilmektedir:

1. tooadd hello üzerinde yeni bir uç noktası **CDN profili** sayfasında, **Endpoint**.
  
    ![Yeni uç noktası](./media/cdn-media-streaming-optimization/01_Adding.png)

2. Merhaba, **için en iyi duruma getirilmiş** aşağı açılan listesinden, **isteğe bağlı medya akış Video** isteğe bağlı video varlıklar. Bir birleşimi canlı ve isteğe bağlı video akış bunu yaparsanız, seçin **genel akış**.

    ![Akış seçili](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Merhaba endpoint oluşturduktan sonra hello iyileştirme belirli ölçütlere uyan tüm dosyaları için geçerlidir. bölümden hello bu işlemi açıklanmaktadır. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Medya hello akamai'den Azure içerik teslim ağı için en iyi duruma getirme
 
Akamai'den akış iyileştirme Canlı için etkin değil veya bağımsız medya kullanan isteğe bağlı video akış ortamlardan teslim edilmek üzere parça. Bu işlem, aşamalı indirme aracılığıyla veya bayt aralığı isteklerini kullanarak aktarılan tek bir büyük varlık farklıdır. Medya teslimi bu stili hakkında daha fazla bilgi için bkz [büyük dosya iyileştirme](cdn-large-file-optimization.md).


Merhaba genel medya teslim veya isteğe bağlı video medya teslim en iyi duruma getirme türü bir CDN uç iyileştirmeler toodeliver ortam varlıkları ile daha hızlı kullanın. Bunlar ayrıca yapılandırmaları zamanla öğrenilen en iyi uygulamaları temel ortam varlıkları için kullanın.

### <a name="caching"></a>Önbelleğe alma

Merhaba akamai'den Azure içerik teslim ağı akış bildirimini veya parça o hello varlığı olduğunu algılarsa, genel web teslim farklı önbelleğe alma sona erme sürelerinden kullanır. (Aşağıdaki tablonun hello hello tam listeye bakın.) Cache-control veya Expires üstbilgileri hello kaynaktan gönderilen her zaman, dikkate gibi. Merhaba varlık medya varlık değilse, genel web teslimi için zaman aşımı değeri hello kullanarak önbelleğe alır.

çok sayıda kullanıcı henüz mevcut olmayan bir parça istediğinde hello kısa negatif önbelleğe alma saat kaynak boşaltması için yararlıdır. Burada Karşılama paketleri, ikinci hello kaynaktan kullanılamaz bir canlı akış örneğidir. Merhaba artık önbelleğe alma aralığı video içeriği genellikle değiştirdiğinden değil hello kaynak gelen istekleri boşaltma yardımcı olur.
 

|    | Genel<br> Web<br>etkinleştirme | Genel<br> medya<br> Akış | İsteğe bağlı video <br>medya<br> Akış  
--- | --- | --- | ---
Önbelleğe alma: pozitif <br> HTTP 200, 203, 300, <br> 301, 302 ve 410 | 7 gün |365 gün | 365 gün   
Önbelleğe alma: negatif <br> HTTP 204, 305, 404, <br> ve 405 | None | 1 saniye | 1 saniye
 
### <a name="deal-with-origin-failure"></a>Kaynak hata ile Dağıt  

Genel ortam teslim ve isteğe bağlı video medya teslim kaynak zaman aşımı ve tipik istek modelleri için en iyi yöntemler dayalı bir yeniden deneme günlük da vardır. Örneğin, genel medya teslim için canlı ve isteğe bağlı video medya teslim daha kısa bir bağlantı zaman aşımı nedeniyle toohello zamana duyarlı yapısını kullanır olduğundan canlı akış.

Bağlantı zaman aşımına uğradığında hello CDN "504 - ağ geçidi zaman aşımı" hata toohello istemci göndermeden önce sayısı yeniden dener. 

Bir dosya hello dosya türü ve boyutunu koşullar listesi eşleştiğinde hello CDN hello davranışı akış medya için kullanır. Aksi takdirde, genel web teslim kullanır.
   
### <a name="conditions-for-media-streaming-optimization"></a>En iyi duruma getirme medya için koşullar 

Aşağıdaki tablonun hello ölçütleri toobe medya için en iyi duruma getirme memnun hello kümesini listeler: 
 
Desteklenen akış türleri | Dosya uzantıları  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, anahtarı, ts, aac
Adobe HDS | f4m, f4x, drmmeta, önyükleme, f4f,<br>Seg parça URL yapısı <br> (regex eşleşen: ^(/.*)Seq(\d+)-Frag(\d+)
TİRE | mpd, tire, dıvx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, ISMA
Kesintisiz akış | / bildirimi /, / QualityLevels/parçaları /
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Medya hello verizon'dan Azure içerik teslim ağı için en iyi duruma getirme

Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü kullanılarak doğrudan akış medya varlıklar sunar. Merhaba CDN birkaç özellikleri doğrudan varsayılan medya varlıklar dağıtımına yardımcı.

### <a name="partial-cache-sharing"></a>Kısmi önbellek paylaşımı

Kısmi önbellek paylaşımı, hello CDN tooserve kısmen önbelleğe alınmış içerik toonew isteklere izin verir. Örneğin, Hello ilk istek toohello CDN bir önbellek isabetsizliği sonuçlanırsa hello isteği toohello kaynak gönderilir. Bu içeriği eksik CDN önbellek hello yüklenmiş olsa da, bu veri alma diğer istekleri toohello CDN başlatabilirsiniz. 

### <a name="cache-fill-wait-time"></a>Önbellek dolgu bekleme süresi

 Merhaba önbellek dolgu bekleme süresi özelliğinin tüm istekler için üstbilgileri hello kaynak sunucudan gelen HTTP yanıtı kadar aynı kaynak hello hello kenar sunucu toohold zorlar. Hello Zamanlayıcı süresi dolmadan önce hello kaynaktan HTTP yanıt üstbilgilerini ulaşırsa, askıya tüm istekleri önbelleğe büyüyen hello dışında sunulur. Merhaba aynı zaman hello önbellek hello kaynaktan verileri tarafından doldurulur. Varsayılan olarak, hello önbellek dolgu bekleme süresi too3, 000 milisaniye olarak ayarlanır. 

