---
title: "Azure RemoteApp, ağ bant genişliği kullanımını bazı yaygın senaryolar ile test etme - | Microsoft Docs"
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
ms.openlocfilehash: 8ad172a06e34cd0647079d787097cb2696cf116e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp - bazı yaygın senaryolar ile ağ bant genişliği kullanımını test etme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Biz anlatıldığı gibi [tahmin Azure RemoteApp ağ bant genişliği kullanımını](remoteapp-bandwidth.md), hangi Azure RemoteApp etkisini ağınıza bazı kullanım testleri çalıştırmak için olduğunu anlamalarını en iyi yolu. Ayarlanmış bir süre boyunca bu testleri çalıştırmak ve her senaryo için gereken bant genişliği ölçebilirsiniz. Özellik varsa, belirli ortamınızda oluşturulacak ağ desenleri anlamak için ağ paket kaybı ve ağ gecikmeyi ayrıca ölçebilirsiniz.

Bant genişliği kullanımını değerlendirirken, kullanım, şirketinizdeki farklı kullanıcılar arasında değişir unutmayın. Örneğin, metin okuyucuları ve yazıcıları genellikle video ile çalışan kullanıcılar daha az bant genişliği tüketebilir. En iyi sonuçlar için kendi kullanıcı gereksinimlerini araştırmak ve en iyi, şirketinizdeki kullanıcılar temsil eden bir karışımını aşağıdaki senaryolarda oluşturun. Unutmayın [bant genişliği kullanımı ve kullanıcı etkisi Etkenler deneyimi gözden](remoteapp-bandwidthexperience.md) -yardımcı olacak ideal testleri tanımlayın.

İlk okuma testleri hakkında karışımı seçin ve ardından bunları çalıştırın. Performans izlemenize yardımcı olması için aşağıdaki tabloyu kullanın.

> [!NOTE]
> Kendi ağ testi yapamayacağı veya bunu yapmak için zamanınız yok, kullanıma bizim [temel ağ bant genişliğini tahmin/önerileri](remoteapp-bandwidthguidelines.md). Mesafe, ancak bunu varsa değişebilir, *için* , kendi testlerinizi yapmanız gerekir.
> 
> 

## <a name="the-usage-tests"></a>Kullanım testleri
Bu testler, her zaman farklı miktarlarda ve farklı işlevler/ağ bant genişliği özellikleri test çalıştırabilirsiniz. Tek şirket kullanıcılarınız en iyi eşleşeni test karışımı seçmek unutmayın.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>Executive/karmaşık PowerPoint - 900-1000 saniye çalıştırın
Tam ekran modunda Microsoft Office PowerPoint kullanarak 45-50 yüksek doğruluk slayta bir kullanıcıyı gösterir. Slayt görüntüleri, geçişleri (ile animasyonları) ve şirketiniz için tipik olan arka plan rengi gradyan ile içermelidir. Kullanıcı en az 20 saniye her slayta kullanması.

Bu senaryo sunuya sonraki slayta bir slayt geçişleri bursty trafiği oluşturur.

### <a name="simple-powerpoint---run-for-620-seconds"></a>Basit PowerPoint - ~ 620 saniye çalıştırın
Bir kullanıcı yaklaşık olarak 30 slayt ile tam ekran modunda Microsoft Office PowerPoint kullanarak basit bir PowerPoint dosyası sayısını gösterir. Slayt daha metin Executive/karmaşık PowerPoint senaryoda yoğun'den ve daha basit arka planları ve görüntüleri (siyah diyagramları) sahiptir. 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - ~ 250 saniye çalıştırın
Bir kullanıcı, Internet Explorer kullanarak web gözatar. Kullanıcı gözatar ve bir karışımını metin, doğal görüntüler ve bazı şematik diyagramları ile birlikte kayar. Uzak Masaüstü oturumu ana bilgisayarı (RD Oturumu Ana bilgisayarı) sunucusu olarak yerel disk sürücüsünde depolanan web sayfalarını bir. MHT dosyası. Page Up, Page Down, yukarı ve aşağı anahtarları, her anahtar/türünü kaydırma için değişen aralıkları kullanarak kullanıcı kayarken:

    - Aşağı - 250 tuş vuruşları çok 500 ms
    - Page Up - 36 tuş vuruşları her 1000 ms
    - Aşağı - 75 her 100 ms tuş vuruşları
    - Page Down - 20 tuş vuruşları her 500 ms
    - Yukarı - 120 her 300 ms tuş vuruşları

### <a name="pdf-document---simple---run-for-610-seconds"></a>PDF belgesini - basit - ~ 610 saniye çalıştırın
Bir kullanıcı okur ve PDF belgesini Adobe Acrobat Reader'ı kullanarak çeşitli şekillerde arar. Belge tabloları, basit grafikleri ve birden çok metin yazı tipi oluşmalıdır. Belge 35-40 sayfaları uzun değil. Kullanıcı ile iki farklı hızlarda geriye doğru birlikte kayar ve, dört farklı yakınlaştırma boyutlarda iletir (sayfasında uygun genişliğe, Sığdır % 100 ve seçtiğiniz başka bir). Yakınlaştırma (yazı tipi) metin farklı boyutlarda işler sağlar. Kaydırma Page Up veya Page Down, yukarı ve aşağı anahtarları, her kaydırma için değişen aralıkları ile aşağı kullanmaktır.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>PDF belge ~ 320 saniye - karma - Çalıştır
Bir kullanıcı okur ve PDF belgesini Adobe Acrobat Reader'ı kullanarak çeşitli şekillerde arar. Belgeyi yüksek kaliteli görüntüleri (fotoğraf dahil), tablolar, basit grafikleri ve birden çok metin yazı tipi oluşur. Kullanıcı ile iki farklı hızlarda geriye doğru birlikte kayar ve, dört farklı yakınlaştırma boyutlarda iletir (sayfasında uygun genişliğe, Sığdır % 100 ve seçtiğiniz başka bir). Yakınlaştırma (yazı tipi) metin farklı boyutlarda işler sağlar. Kaydırma Page Up veya Page Down, yukarı ve aşağı anahtarları, her kaydırma için değişen aralıkları ile aşağı kullanmaktır.

### <a name="flash-video-playback---run-for-180-seconds"></a>Flash video oynatmayı - ~ 180 saniye çalıştırın
Bir kullanıcının bir web sayfasındaki katıştırılmış bir Adobe Flash kodlu video görüntüler. Web sayfası RD Oturumu Ana Bilgisayarı sunucusu yerel sabit sürücüde depolanır. Video Internet Explorer içinden eklenti katıştırılmış player tarafından oynatılır.

Bu senaryo multimedya içeren zengin içerik web sayfalarını görüntüleme kullanıcılar öykünür. Verilerin çoğu VOBR aracılığıyla bo gerekir.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Uzak yazarak word - ~ 1800 saniye çalıştırın
Bir kullanıcı bir belge türleri bir RDP oturumu üzerinden'ü tıklatın. Tuş vuruşları RDP oturumu aracılığıyla istemci tarafı bir Microsoft Word belgesine uzak oturumda çalışan gönderilir. Bir karakter her 250 ms (toplam 7050 karakter) yazma hızıdır. 

Bu, bir bilgi çalışanı için en sık karşılaşılan senaryolardan biri. Bu senaryo, modern iş işlemci yazarak bir kullanıcının yanıtlama sınar. Bu senaryo, bant genişliği kullanımını bile küçük değişikliklere duyarlıdır.

## <a name="tracking-the-test-results"></a>Test sonuçlarını izleme
Ortamınızda senaryoları değerlendirmek için aşağıdaki tabloyu kullanın. Aşağıda sağlanan verileri yalnızca gösterim amacıyla -, gözlemlemek gelen çok farklı olabilir. 

Kolaylık olması için tüm senaryoları aynı 1920 x 1080 piksel ekran çözünürlüğü kullanarak test edilmiş ve 120 ms + işaretine yaklaşık % 1'in altındaki 200 ms ve ağ gecikme süresi (gecikme) olan bir ağda TCP taşımaları değişimi varsayıyoruz.

Tablo hakkında:

* **Ortalama deneyimi** burada kullanıcı üretkenliğini önemli ölçüde etkilenmez ancak bazen ses veya video hatalardan hariç değil ağ bant genişliğini içerir. Sistem dinamik mantığı yararlanarak hızla kurtarabilirsiniz. Kullanıcı deneyimini kalite güvence altına almak için ağ bant genişliğini tahmin girişimi.
  * **Belirgin sorunları (kesme noktası)** burada kullanıcıları deneyimlerini önemli sorunları fark ve üretkenliklerini ölçülebilir zaman aralıkları için etkilenen ağ bant genişliğini içerir. Bu noktada RDP algoritmaları zorlanıyor olan ve kullanıcının kalitesinden yeterli ağ bant genişliği nedeniyle garanti edemez.
  * **Önerilen** iyi veya mükemmel deneyimi için önerilen ağ bant genişliği içerir. Genellikle tek bir adımda karşılık gelen değerden daha yüksek olan **ortalama deneyimi** sütun.
  * **Notlar** gözlemleri ve açıklamaları içerir.

| Test etme | Ortalama deneyimi | Belirgin sorunları (kesme noktası) | Önerilen ağ bant genişliği | Notlar |
| --- | --- | --- | --- | --- |
| Executive/karmaşık PPT |10 MB/sn |1 MB/sn |> 10 MB/s, tercih edilen 100 MB/sn |1 MB/sn'ye birçok animasyonları kaybolur |
| Basit PPT |5 MB/sn |256 KB/sn |10 MB/sn |256 KB/sn'ye slayt belirgin gecikmeyle yükleyin. |
| Internet Explorer |10 MB/sn |1 MB/sn |> 10 MB/s, tercih edilen 100 MB/sn |1 MB/sn, web videoları bulanık ve dalgalı, hızlı kaydırma sorunları var. |
| Basit PDF |1 MB/sn |256 KB/sn |5 MB/sn |Sayfa yükleme biraz sürdüğünü 256 KB/s |
| Karma PDF |1 MB/sn |256 KB/sn |5 MB/sn |256 KB/sn'ye sayfa bir önemli yüklemek için gereken süre |
| Flash video kayıttan yürütme |10 MB/sn |1 MB/sn |> 10 MB/s, tercih edilen 100 MB/sn |1 MB/sn'ye video karlı olduğuna ve bazı çerçeveler bırakıldı |
| Uzak yazarak word |256 KB/sn |128 KB/sn |1 MB/sn |256 KB/sn'ye tuş vuruşları arasındaki süre kullanıcı karşılaşabilirsiniz |

Kullanıcı başına ağ bant genişliği değerlendirmek için yukarıdaki senaryoların bir karışımını ve gerekli ağ bant genişliği karşılık gelen bir oranı oluşturun. Senaryolarınız için gereken en yüksek sayı seçin. Kullanıcıların neredeyse hiçbir zaman tek başına sistem kullandığından, aynı ağ üzerinde eşzamanlı olarak çalışan kullanıcılar için bazı ayrılmış göz önünde bulundurun.

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Azure RemoteApp ağ bant genişliği kullanımını tahmin etme](remoteapp-bandwidth.md)
* [Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri](remoteapp-bandwidthguidelines.md)

