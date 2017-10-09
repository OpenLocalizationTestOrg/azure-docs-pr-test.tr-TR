---
title: "aaaAzure RemoteApp, ağ bant genişliği kullanımını bazı yaygın senaryolar ile test etme - | Microsoft Docs"
description: "Ağ bant genişliği ihtiyaçlarınız için Azure RemoteApp hakkında ne yardımcı olabilecek genel kullanım senaryoları tahmin öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp - bazı yaygın senaryolar ile ağ bant genişliği kullanımını test etme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Biz anlatıldığı gibi [tahmin Azure RemoteApp ağ bant genişliği kullanımını](remoteapp-bandwidth.md), hangi hello Azure RemoteApp tooyour ağ toorun etkisidir çıkışı en iyi şekilde toofigure bazı kullanım testleri hello. Her senaryo için gereken bir kümesi zaman dönemi ve ölçü hello bant genişliği için bu testleri çalıştırın. Merhaba yeteneği varsa, belirli ortamınızda oluşturulacak hello ağ paket kaybı ve ağ değişimi toounderstand hello ağ desenleri de ölçebilirsiniz.

Merhaba bant genişliği kullanımını değerlendirirken, kullanım, şirketinizdeki farklı kullanıcılar arasında değişir unutmayın. Örneğin, metin okuyucuları ve yazıcıları genellikle video ile çalışan kullanıcılar daha az bant genişliği tüketebilir. En iyi sonuçlar için kendi kullanıcı gereksinimlerini araştırmak ve en iyi şirketinizin hello kullanıcıları temsil eden senaryoları aşağıdaki hello bir karışımını oluşturun. Çok unutmayın[bant genişliği kullanımı ve kullanıcı etkisi gözden geçirme hello Etkenler deneyimi](remoteapp-bandwidthexperience.md) -yardımcı olacak hello ideal testleri tanımlayın.

İlk okuma hello testleri hakkında karışımı seçin ve ardından bunları çalıştırın. Toohelp izleme performans hello tabloda kullanabilirsiniz.

> [!NOTE]
> Kendi ağ testi yapamayacağı veya hello zaman toodo böylece yok, kullanıma bizim [temel ağ bant genişliğini tahmin/önerileri](remoteapp-bandwidthguidelines.md). Mesafe, ancak bunu varsa değişebilir, *için* , kendi testlerinizi yapmanız gerekir.
> 
> 

## <a name="hello-usage-tests"></a>Merhaba kullanım testleri
Bu testler, her zaman farklı miktarlarda ve farklı işlevler/ağ bant genişliği özellikleri test çalıştırabilirsiniz. Toochoose hello tek tek şirket kullanıcılarınız en iyi şekilde eşleşen test karışımı unutmayın.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>Executive/karmaşık PowerPoint - 900-1000 saniye çalıştırın
Tam ekran modunda Microsoft Office PowerPoint kullanarak 45-50 yüksek doğruluk slayta bir kullanıcıyı gösterir. Merhaba slayt görüntüleri, geçişleri (ile animasyonları) ve şirketiniz için tipik olan arka plan rengi gradyan ile içermelidir. Merhaba kullanıcı en az 20 saniye her slayta kullanması.

Bu senaryo bir slayt toohello sonraki slayt hello sunusunda geçişleri bursty trafiği oluşturur.

### <a name="simple-powerpoint---run-for-620-seconds"></a>Basit PowerPoint - ~ 620 saniye çalıştırın
Bir kullanıcı yaklaşık olarak 30 slayt ile tam ekran modunda Microsoft Office PowerPoint kullanarak basit bir PowerPoint dosyası sayısını gösterir. Merhaba slayt daha metin hello Executive/karmaşık PowerPoint senaryoda yoğun'den ve daha basit arka planları ve görüntüleri (siyah diyagramları) sahiptir. 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - ~ 250 saniye çalıştırın
Bir kullanıcı, Internet Explorer kullanarak hello web gözatar. Merhaba kullanıcı gözatar ve bir karışımını metin, doğal görüntüler ve bazı şematik diyagramları ile birlikte kayar. Merhaba hello yerel disk sürücüsünde hello Uzak Masaüstü oturumu ana bilgisayarı (RD Oturumu Ana bilgisayarı) sunucusu olarak depolanan web sayfalarını bir. MHT dosyası. Page Up, Page Down, yukarı ve aşağı anahtarları, her anahtar/türünü kaydırma için değişen aralıkları kullanarak Hello kullanıcı kayar:

    - Aşağı - 250 tuş vuruşları çok 500 ms
    - Page Up - 36 tuş vuruşları her 1000 ms
    - Aşağı - 75 her 100 ms tuş vuruşları
    - Page Down - 20 tuş vuruşları her 500 ms
    - Yukarı - 120 her 300 ms tuş vuruşları

### <a name="pdf-document---simple---run-for-610-seconds"></a>PDF belgesini - basit - ~ 610 saniye çalıştırın
Bir kullanıcı okur ve PDF belgesini Adobe Acrobat Reader'ı kullanarak çeşitli şekillerde arar. Merhaba belge tabloları, basit grafikleri ve birden çok metin yazı tipi oluşmalıdır. Merhaba, 35-40 sayfaları uzun belgedir. Merhaba kullanıcı kayar geriye doğru iki farklı hızlarda aracılığıyla ve, dört farklı yakınlaştırma boyutlarda iletir (uygun toopage, uygun toowidth % 100 ve seçtiğiniz başka bir). Yakınlaştırma hello hello metin (yazı tipi) farklı boyutlarda işler sağlar. Kaydırma hello Page Up, Page Down, yukarı ve aşağı anahtarları, her kaydırma için değişen aralıkları ile aşağı kullanmaktır.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>PDF belge ~ 320 saniye - karma - Çalıştır
Bir kullanıcı okur ve PDF belgesini Adobe Acrobat Reader'ı kullanarak çeşitli şekillerde arar. Merhaba belgeyi yüksek kaliteli görüntüleri (fotoğraf dahil), tablolar, basit grafikleri ve birden çok metin yazı tipi oluşur. Merhaba kullanıcı kayar geriye doğru iki farklı hızlarda aracılığıyla ve, dört farklı yakınlaştırma boyutlarda iletir (uygun toopage, uygun toowidth % 100 ve seçtiğiniz başka bir). Yakınlaştırma hello hello metin (yazı tipi) farklı boyutlarda işler sağlar. Kaydırma hello Page Up, Page Down, yukarı ve aşağı anahtarları, her kaydırma için değişen aralıkları ile aşağı kullanmaktır.

### <a name="flash-video-playback---run-for-180-seconds"></a>Flash video oynatmayı - ~ 180 saniye çalıştırın
Bir kullanıcının bir web sayfasındaki katıştırılmış bir Adobe Flash kodlu video görüntüler. Merhaba web sayfası hello yerel sabit diskine hello RD Oturumu Ana bilgisayarı sunucu depolanır. Merhaba video Internet Explorer içinden eklenti katıştırılmış player tarafından oynatılır.

Bu senaryo multimedya içeren zengin içerik web sayfalarını görüntüleme kullanıcılar öykünür. Merhaba verilerin çoğu VOBR aracılığıyla bo gerekir.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Uzak yazarak word - ~ 1800 saniye çalıştırın
Bir kullanıcı bir belge türleri bir RDP oturumu üzerinden'ü tıklatın. Tuş vuruşları hello uzak oturumda çalışan hello istemci tarafı hello RDP oturumu tooa Microsoft Word belgesinde üzerinden gönderilir. Merhaba oranı yazarak bir her 250 ms (toplam 7050 karakter) karakterdir. 

Bu, bir bilgi çalışanı için hello en sık karşılaşılan senaryolardan biri. Bu senaryo, modern iş işlemci yazarak bir kullanıcının hello yanıtlama sınar. Bant genişliği kullanımını hassas tooeven küçük değişikliklere senaryodur.

## <a name="tracking-hello-test-results"></a>İzleme hello test sonuçları
Tablo tooevaluate hello senaryolar, ortamınızdaki hello kullanabilirsiniz. Aşağıda sağlanan hello verileri yalnızca gösterim amacıyla -, gözlemlemek gelen çok farklı olabilir. 

Kolaylık olması için tüm senaryoları hello aynı 1920 x 1080 piksel ekran çözünürlüğü kullanarak test edilmiş ve hello 120 ms + işaretine yaklaşık % 1'in altındaki 200 ms ve ağ gecikme süresi (gecikme) olan bir ağda TCP taşımaları değişimi varsayıyoruz.

Merhaba tablo hakkında:

* **Ortalama deneyimi** burada kullanıcı üretkenliğini önemli ölçüde etkilenmez ancak bazen ses veya video hatalardan hariç değil hello ağ bant genişliği içerir. Merhaba mümkün toorecover hızlı bir şekilde hello dinamik mantığı yararlanarak sistemidir. Merhaba ağ bant genişliğini tahmin girişimi tooguarantee hello kalitesi hello kullanıcı deneyimi.
  * **Belirgin sorunları (kesme noktası)** burada kullanıcıları deneyimlerini önemli sorunları fark ve üretkenliklerini ölçülebilir zaman aralıkları için etkilenen hello ağ bant genişliği içerir. Bu noktada hello RDP algoritmaları zorlanıyor olan ve hello kullanıcının kalitesinden yeterli ağ bant genişliği nedeniyle garanti edemez.
  * **Önerilen** hello ağ bant genişliği iyi veya mükemmel deneyimi için önerilen içerir. Genellikle tek bir adımda hello karşılık gelen içinde hello değerden daha yüksek olan **ortalama deneyimi** sütun.
  * **Notlar** gözlemleri ve açıklamaları içerir.

| Test etme | Ortalama deneyimi | Belirgin sorunları (kesme noktası) | Önerilen ağ bant genişliği | Notlar |
| --- | --- | --- | --- | --- |
| Executive/karmaşık PPT |10 MB/sn |1 MB/sn |> 10 MB/s, tercih edilen 100 MB/sn |1 MB/sn'ye birçok animasyonları kaybolur |
| Basit PPT |5 MB/sn |256 KB/sn |10 MB/sn |256 KB/sn'ye hello slayt belirgin gecikmeyle yükleyin. |
| Internet Explorer |10 MB/sn |1 MB/sn |> 10 MB/s, tercih edilen 100 MB/sn |1 MB/sn, web videoları bulanık ve dalgalı, hızlı kaydırma sorunları var. |
| Basit PDF |1 MB/sn |256 KB/sn |5 MB/sn |256 KB/sn'ye biraz sürdüğünü tooload başlangıç sayfası |
| Karma PDF |1 MB/sn |256 KB/sn |5 MB/sn |256 KB/sn'ye hello sayfa önemli miktarda zaman tooload alır. |
| Flash video kayıttan yürütme |10 MB/sn |1 MB/sn |> 10 MB/s, tercih edilen 100 MB/sn |1 MB/sn'ye hello video karlı olduğuna ve bazı çerçeveler bırakıldı |
| Uzak yazarak word |256 KB/sn |128 KB/sn |1 MB/sn |256 KB/sn'ye kullanıcı hello zaman tuş vuruşları arasındaki fark edebilirsiniz |

Kullanıcı başına tooevaluate hello ağ bant genişliği hello senaryoları yukarıda bir karışımını ve karşılık gelen bir oranı hello gerekli ağ bant genişliği oluşturun. Senaryolarınız için gereken en yüksek sayı hello seçin. Kullanıcıların neredeyse hiçbir zaman tek başına hello sistem kullandığından, aynı ağ üzerinde eşzamanlı olarak çalışan kullanıcılar hello için bazı ayırma göz önünde bulundurun.

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Azure RemoteApp ağ bant genişliği kullanımını tahmin etme](remoteapp-bandwidth.md)
* [Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri](remoteapp-bandwidthguidelines.md)

