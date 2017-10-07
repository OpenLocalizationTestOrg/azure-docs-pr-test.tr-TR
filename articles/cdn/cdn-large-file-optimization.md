---
title: "hello Azure içerik teslim ağı aracılığıyla aaaLarge dosya indirme iyileştirme"
description: "En iyi duruma getirme derinliği açıklandığı büyük dosya indirme"
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
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Hello Azure içerik teslim ağı aracılığıyla büyük dosya indirme iyileştirme

Dosya boyutları hello Internet teslim içeriğinin son tooenhanced işlevselliği, geliştirilmiş grafik ve zengin medya içeriği toogrow devam edin. Bu büyüme birçok faktöre tarafından yönetilir: geniş bant sızma, büyük uygun maliyetli depolama aygıtları, yüksek tanımlı video ve Internet'e bağlı cihazlar (IOT) yaygın arttıkça. Bir hızlı ve verimli teslim büyük dosyalar için kritik tooensure kesintisiz ve eğlenceli Müşteri Deneyimi mekanizmadır.

Büyük dosyaları teslimini çeşitli zorluklar sahiptir. İlk olarak, uygulamaların tüm verileri sıralı olarak indirmesini değil çünkü hello ortalama süre toodownload büyük bir dosya önemli olabilir. Bazı durumlarda, uygulamaların hello ilk bölümü önce dosyayı son parçası hello indirmesini. Az miktarda bir dosya istenen veya bir kullanıcı bir indirme duraklatır, hello yükleme başarısız olabilir. Merhaba sonra içerik teslim ağı (CDN) hello tüm dosya hello kaynak sunucudan kadar hello indirme de gecikebilir. 

İkinci olarak, bir kullanıcının makine ve hello dosyası arasındaki hello gecikme süresi içerik aktarılma görüntüleyebilirler hello hızını belirler. Ayrıca, Ağ Tıkanıklığı ve kapasite sorunları verimliliği de etkiler. Sunucular ve kullanıcılar arasında büyük uzaklıklar kalite azaltan paket kaybı toooccur ek fırsatı oluşturun. sınırlı üretilen işi tarafından kalite Hello azalmasına neden ve artan paket kaybı dosya indirme toofinish için hello bekleme süresini artırabilir. 

Üçüncü birçok büyük dosyayı kendi bütün teslim edilmedi. Kullanıcılar aracılığıyla yarısı bir yüklemeyi iptal edin veya ilk birkaç dakikalık video uzun bir MP4 yalnızca hello izleyin. Bu nedenle, yazılım ve medya teslim şirketler toodeliver yalnızca hello istenen dosyanın bölümünü istiyor. Hello etkili bir dağıtım bölümleri hello kaynak sunucudan hello çıkış trafiği azaltan istedi. Etkili bir dağıtım hello bellek ve g/ç baskısı hello kaynak sunucu üzerinde de azaltır. 

Merhaba akamai'den Azure içerik teslim ağı şimdi büyük dosyalar toousers verimli bir şekilde ölçekli Merhaba dünya genelinde sunan bir özellik sunar. hello yük hello kaynak sunucularda azalttığı hello özelliği gecikmelerini azaltır. Bu özellik hello standart Akamai fiyatlandırma katmanı ile kullanılabilir.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Büyük dosyaları CDN uç noktası toooptimize teslimini yapılandırın

CDN uç noktası toooptimize teslimi hello Azure portal aracılığıyla büyük dosyalar için yapılandırabilirsiniz. Herhangi bir istemci SDK'ları toodo bu hello veya bizim REST API de kullanabilirsiniz. Merhaba aşağıdaki adımlar hello işlem hello Azure portal aracılığıyla gösterir.

1. tooadd hello üzerinde yeni bir uç noktası **CDN profili** sayfasında, **Endpoint**.

    ![Yeni uç noktası](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. Merhaba, **için en iyi duruma getirilmiş** aşağı açılan listesinden, **büyük dosya indirme**.

    ![Seçili büyük dosya en iyi duruma getirme](./media/cdn-large-file-optimization/02_Creating.png)


Merhaba CDN uç noktası oluşturduktan sonra hello büyük dosya iyileştirmeler belirli ölçütlere uyan tüm dosyaları için geçerlidir. bölümden hello bu işlemi açıklanmaktadır.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Akamai'den teslimi hello Azure içerik teslim ağı ile büyük dosyalar için en iyi duruma getirme

Merhaba büyük dosya en iyi duruma getirme türü özelliği ağ iyileştirmeleri ve yapılandırmaları toodeliver büyük dosyaları üzerinde daha hızlı ve daha responsively etkinleştirir. Genel web teslimat Akamai ile dosyaları yalnızca 1,8 GB aşağıda önbelleğe alır ve tünel (değil önbellek) için dosyaları too150 GB. Büyük dosya iyileştirme too150 GB dosyaları önbelleğe alınır.

Belirli koşullar karşılandığında büyük dosya iyileştirmesi etkili olur. Koşullar hello kaynak sunucuyu nasıl çalıştığı ve hello boyutları ve istenen hello dosya türlerini içerir. Biz bu konular hakkında ayrıntılar almak önce hello iyileştirme nasıl çalıştığını anlamanız gerekir. 

### <a name="object-chunking"></a>Öbekleme nesnesi 

Hello Azure içerik teslim ağı akamai'den nesne Öbekleme adında bir teknik kullanır. Büyük bir dosya istendiğinde hello CDN hello dosyasının küçük parça hello kaynaktan alır. Merhaba CDN uç/POP sunucu tam veya bayt aralığı dosya isteği aldıktan sonra bu en iyi duruma getirme desteklenen hello dosya türü olup olmadığını denetler. Ayrıca, hello dosya türü hello dosya boyutu gereksinimleri karşılayıp karşılamadığını denetler. Merhaba dosya boyutu 10 MB'den büyük ise hello CDN uç sunucusunu hello dosya 2 MB'lık parçalar hello kaynaktan ister. 

CDN uç hello Hello öbek ulaştıktan sonra bu önbelleğe alınmış ve hemen toohello kullanıcı sunulan. Merhaba CDN sonra prefetches hello sonraki öbek paralel. Bu önceden getirme hello içerik gecikmesini azaltır hello kullanıcı öncesinde bir öbek kalmasını sağlar. Bu işlem, dosya (isteniyorsa) indirilir hello tüm kadar devam eder, tüm bayt aralığı (isteniyorsa) kullanılabilir, veya hello istemci hello bağlantıyı sonlandırır. 

Merhaba bayt aralığı isteği hakkında daha fazla bilgi için bkz: [RFC 7233](https://tools.ietf.org/html/rfc7233).

alındığında gibi hello CDN herhangi öbekleri önbelleğe alır. dosyanın tamamı Hello hello CDN önbelleği önbelleğe toobe sahip değil. CDN önbellek hello sonraki istekleri hello dosya ya da bayt aralıkları için sunulur. CDN hello tüm hello öbekleri önbelleğe alınan, hazırlık kullanılan toorequest öbekleri hello kaynaktan olur. Bu iyileştirme hello kaynak sunucu toosupport bayt aralığı isteklerini hello yeteneklerini kullanır. _Merhaba kaynak sunucu bayt aralığı isteklerini desteklemiyorsa, bu en iyi duruma getirme etkin değil._ 

### <a name="caching"></a>Önbelleğe alma
Büyük dosya en iyi duruma getirme, genel web teslim farklı varsayılan önbelleğe alma sona erme sürelerinden kullanır. Pozitif hem HTTP yanıt kodlarına dayalı negatif önbelleğini arasında ayırır. Merhaba kaynak sunucusu önbellek denetim aracılığıyla bir sona erme saati belirtir veya sona erme hello yanıt üstbilgisi, bu değeri hello CDN geliştirir. Merhaba kaynak belirtmiyor ve hello dosya bu en iyi duruma getirme türü için hello türü ve boyutunu koşullara uyan hello CDN büyük dosya iyileştirme için hello varsayılan değerleri kullanır. Aksi durumda, hello CDN genel web teslimat için varsayılanları kullanır.


|    | Genel web | Büyük dosya en iyi duruma getirme 
--- | --- | --- 
Önbelleğe alma: pozitif <br> HTTP 200, 203, 300, <br> 301, 302 ve 410 | 7 gün |1 gün  
Önbelleğe alma: negatif <br> HTTP 204, 305, 404, <br> ve 405 | None | 1 saniye 

### <a name="deal-with-origin-failure"></a>Kaynak hata ile Dağıt

Genel web teslim tootwo dakika hello büyük dosya en iyi duruma getirme türü için iki saniye gelen Hello kaynak okuma zaman aşımı süresi artırır. Bu artış hello büyük dosya boyutlarına tooavoid için erken zaman aşımı bağlantısı hesapları.

Bağlantı zaman aşımına uğradığında hello CDN "504 - ağ geçidi zaman aşımı" hata toohello istemci göndermeden önce sayısı yeniden dener. 

### <a name="conditions-for-large-file-optimization"></a>Büyük dosya iyileştirme için koşullar

Aşağıdaki tablonun hello ölçütleri toobe büyük dosya iyileştirme için memnun hello kümesini listeler:

Koşul | Değerler 
--- | --- 
Desteklenen dosya türleri | 3g 2, 3gp, asf, AVI, bz2, dmg, exe, f4v, flv, <br> GZ hdp, ISO, jxr, m4v, mkv, mov, mp4, <br> MPEG, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, ZIP  
Küçük dosya boyutu | 10 MB 
En büyük dosya boyutu | 150 GB 
Kaynak sunucu özellikleri | Bayt aralığı isteklerini desteklemesi gerekir 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Verizon'dan teslimi hello Azure içerik teslim ağı ile büyük dosyalar için en iyi duruma getirme

Hello Azure içerik teslim ağı verizon'dan dosya boyutu bir büyük harf olmayan büyük dosyaları sunar. Ek özellikleri daha hızlı varsayılan toomake teslimini büyük dosyalar tarafından etkinleştirilir.

### <a name="complete-cache-fill"></a>Tam önbellek doldurma

ilk istek terk kaybolur veya hello varsayılan tam önbellek dolgu özellik hello CDN toopull bir dosya hello önbelleğine sağlar. 

Tam önbellek dolgu büyük varlıkları için kullanışlıdır. Genellikle, kullanıcıların onları başlangıç toofinish yüklemeyin. Aşamalı indirme kullanırlar. Merhaba varsayılan davranışı hello kenar sunucu tooinitiate hello varlık hello kaynak sunucusundan bir arka plan almaya zorlar. Daha sonra hello kenar sunucunun yerel önbellekteki hello varlıktır. Hello Önbelleği'nde Hello tam nesne olduktan sonra hello uç sunucusunu hello önbelleğe alınmış nesnenin için bayt aralığı isteklerini toohello CDN yerine getirir.

Merhaba Verizon Premium katmanı hello kurallar altyapısı aracılığıyla Hello varsayılan davranışı devre dışı bırakılabilir.

### <a name="peer-cache-fill-hot-filing"></a>Eş önbelleği hot dosyalama doldurun

Merhaba varsayılan eş önbellek dolgu hot dosyalama özelliği bir karmaşık özel algoritması kullanır. Bant genişliğine bağlı sunucuları önbelleğe alma ek kenar kullanır ve toplama ölçümleri toofulfill istemci büyük, yüksek oranda popüler nesneler için istekleri. Bu özellik, çok sayıda ek isteği tooa kullanıcının kaynak sunucuya gönderilen bir durum önler. 

### <a name="conditions-for-large-file-optimization"></a>Büyük dosya iyileştirme için koşullar

Merhaba iyileştirme özelliklerini Verizon için varsayılan olarak açıktır. En büyük dosya boyutu üzerinde hiçbir sınır vardır. 

## <a name="additional-considerations"></a>Diğer konular

Ek bir yönü bu en iyi duruma getirme türü için aşağıdaki hello göz önünde bulundurun.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Akamai'den Azure içerik teslim ağı

- işlem Öbekleme hello ek istekler toohello kaynak sunucu oluşturur. Ancak, hello genel hello kaynaktan teslim verilerin hacmi çok daha küçüktür. Kümeleme sonuçlarında hello CDN konumundaki önbelleğe alma özelliklerini daha iyi.

- Merhaba dosyasının küçük parça teslim edildiğinden bellek ve g/ç baskısı hello kaynak azaltılır.

- CDN Hello önbelleğe alınmış öbekleri için vardır hiçbir ek istekler toohello kaynak hello içeriğin süresi dolar veya hello önbellekten çıkarılmasına kadar.

- Kullanıcılar, aralık yapabilir toohello CDN ister ve normal bir dosya gibi ele. En iyi duruma getirme, yalnızca geçerli bir dosya türü ise ve hello bayt aralığı 10 MB ve 150 GB arasında ise geçerlidir. İstenen hello ortalama dosya boyutu 10 MB'den küçük ise toouse genel web teslim isteyebilirsiniz.

### <a name="azure-content-delivery-network-from-verizon"></a>Verizon'dan Azure içerik teslim ağı

Merhaba genel web teslim en iyi duruma getirme türü büyük dosyalar sunabilir.
