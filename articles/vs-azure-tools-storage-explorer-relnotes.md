---
title: "aaaMicrosoft Azure Storage Gezgini (Önizleme) sürüm notları | Microsoft Docs"
description: "Microsoft Azure Storage Gezgini (Önizleme) için sürüm notları"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Microsoft Azure Storage Gezgini (Önizleme) sürüm notları

Bu makalede Azure Storage Gezgini 0.8.16 için (Önizleme), önceki sürümler için sürüm notları yanı sıra sürüm notları hello sürüm içerir.

[Microsoft Azure Storage Gezgini (Önizleme)](./vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan bir tek başına uygulamadır.

## <a name="version-0816-preview"></a>Sürüm 0.8.16 (Önizleme)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Azure Depolama Gezgini (Önizleme) 0.8.16 indirin
- [Windows için Azure Storage Gezgini 0.8.16 (Önizleme)](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Mac için Azure Storage Gezgini 0.8.16 (Önizleme)](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Linux için Azure Storage Gezgini 0.8.16 (Önizleme)](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Yeni
* Bir blob açtığınızda, bir değişiklik algılandığında, Depolama Gezgini tooupload hello indirilen dosya ister
* Gelişmiş Azure yığın oturum açma deneyimi
* Çok sayıda küçük karşıya/indirilmesi geliştirilmiş hello performans dosyaları hello aynı saat


### <a name="fixes"></a>Düzeltmeler
* Bazı blob türleri için çok bir karşıya yükleme çakışması sırasında "replace" seçme bazen hello karşıya yükleme yeniden başlatılıyor neden olur. 
* 0.8.15 sürümünde yüklemeleri bazen %99 kabin.
* Henüz mevcut tooupload tooa dizin seçerseniz dosyaları tooa dosya paylaşımı, karşıya yüklenirken, yükleme başarısız olur.
* Depolama Gezgini hatalı zaman damgaları paylaşılan erişim imzaları ve tablo sorguları oluşturma.


Bilinen sorunlar
* Bir ad ve anahtar bağlantı dizesi kullanarak şu an çalışmıyor. Merhaba sonraki sürümde düzeltilecektir. O zamana kadar kullandığınız adı ve anahtar ekleyebilirsiniz.
* Merhaba indirme tooopen geçersiz bir Windows dosya adına sahip bir dosya çalışırsanız, bir dosya bulunamadı hatası neden olur.
* "İptal" görevde tıkladıktan sonra bu görev toocancel bir süre devam edebilir. Hello Azure Depolama düğümü kitaplığı kısıtlamasıdır.
* Bir blob karşıya yükleme işlemini tamamladıktan sonra hello karşıya yükleme başlatılan hello sekmesini yenilenir. Bu önceki davranış farklıdır ve ayrıca geri toohello kök olduğunuz hello kapsayıcısının gerçekleştirilecek toobe neden olur.
* Yanlış PIN/akıllı kart sertifika hello sonra sipariş toohave toorestart gerekir seçerseniz Depolama Gezgini kararı unutmayın.
* Merhaba Hesap Ayarları panelini tooreenter kimlik bilgileri toofilter abonelikleri gerektiğini gösterebilir.
* BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz. Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.
* Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder.
* Ubuntu 14.04 kullanıcıları, GCC olan toodate tooensure gerekir - bu hello çalıştırarak yapılabilir komutları izleyerek ve, makinenin yeniden başlatılması:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Ubuntu 17.04 kullanıcıları, tooinstall GConf gerekir - bu komutları aşağıdaki ve, makinenin yeniden başlatılması hello çalıştıran yapılabilir:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Sürüm 0.8.14 (Önizleme)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Azure Depolama Gezgini (Önizleme) 0.8.14 indirin
* [Windows Azure Depolama Gezgini (Önizleme) 0.8.14 indirin](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Mac için Azure Storage Gezgini (Önizleme) 0.8.14 indirin](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Linux için Azure Storage Gezgini (Önizleme) 0.8.14 indirin](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Yeni

* Sipariş tootake avantajlarından birkaç kritik güvenlik güncelleştirmeleri, güncelleştirilmiş Elektron sürüm too1.7.2
* Artık hızlı bir şekilde hello çevrimiçi sorun giderme kılavuzu hello Yardım menüsünden erişebilirsiniz
* Depolama Gezgini sorun giderme [Kılavuzu][2]
* [Yönergeler] [ 3] tooan Azure yığın abonelik bağlanma

### <a name="known-issues"></a>Bilinen sorunlar

* Merhaba Sil klasör onay iletişim düğmeleri hello fare tıklamaları Linux'ta kaydetme yok. Geçici çözüm toouse hello Enter anahtarı.
* Yanlış PIN/akıllı kart sertifika hello sonra sipariş toohave Depolama Gezgini toorestart gerekir seçerseniz hello karar unuttunuz
* BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir
* Merhaba Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir
* BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz. Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.
* Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder. 
* Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Ubuntu 14.04 yükleme gereksinimleri aşağıda verilmiştir:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Önceki sürümler

* [Sürüm 0.8.13](#version-0813)
* [Sürüm 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Sürüm 0.8.9 / 0.8.8](#version-089--088)
* [Sürüm 0.8.7](#version-087)
* [Sürüm 0.8.6](#version-086)
* [Sürüm 0.8.5](#version-085)
* [Sürüm 0.8.4](#version-084)
* [Sürüm 0.8.3](#version-083)
* [Sürüm 0.8.2](#version-082)
* [Sürüm 0.8.0](#version-080)
* [Sürüm 0.7.20160509.0](#version-07201605090)
* [Sürüm 0.7.20160325.0](#version-07201603250)
* [Sürüm 0.7.20160129.1](#version-07201601291)
* [Sürüm 0.7.20160105.0](#version-07201601050)
* [Sürüm 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Sürüm 0.8.13
12.05.2017

#### <a name="new"></a>Yeni

* Depolama Gezgini sorun giderme [Kılavuzu][2]
* [Yönergeler] [ 3] tooan Azure yığın abonelik bağlanma

#### <a name="fixes"></a>Düzeltmeler

* Sabit: Karşıya dosya yükleme yetersiz bellek hatası neden, yüksek şansınız
* Sabit: Artık PIN/akıllı kart ile oturum
* Sabit: Portalda şimdi works Azure Çin, Azure Almanya, Azure ABD devlet kurumları ve Azure yığın açın
* Sabit: klasör tooa blob kapsayıcısı karşıya yüklenirken "Geçersiz işlemi" hata bazen oluşacak
* Sabit: Tümünü Seç anlık görüntüleri yönetirken devre dışı bırakıldı
* Sabit: hello temel blob hello meta verileri, anlık görüntüleri hello özelliklerini görüntüledikten sonra üzerine

#### <a name="known-issues"></a>Bilinen sorunlar

* Yanlış PIN/akıllı kart sertifika hello sonra sipariş toohave Depolama Gezgini toorestart gerekir seçerseniz hello karar unuttunuz
* Merhaba yakınlaştırma düzeyini veya uzaklaştırılacağını olsa da, kısa bir süre içinde toohello varsayılan düzeyini sıfırlayabilir
* BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir
* Merhaba Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir
* BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz. Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.
* Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder. 
* Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Ubuntu 14.04 yükleme gereksinimleri aşağıda verilmiştir:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Sürüm 0.8.12 / 0.8.11 / 0.8.10
04/07/2017

#### <a name="new"></a>Yeni

* Merhaba güncelleştirme bildirimden bir güncelleştirmeyi yüklediğinizde Depolama Gezgini otomatik olarak kapatılacak
* Sık erişilen kaynaklarla çalışmak için Gelişmiş bir deneyim yerinde hızlı erişim sağlar
* Merhaba Blob kapsayıcısına düzenleyicisinde kiralık blob ait sanal makine artık görebilirsiniz
* Merhaba sol tarafındaki paneli şimdi daraltabilirsiniz
* Bulma şimdi hello'de çalışır aynı saat indirme
* İstatistikleri hello Blob kapsayıcısı, dosya paylaşımı ve tablo düzenleyicileri toosee hello boyutunu kaynak ya da seçimi kullanın
* Oturum açma Active Directory (AAD) tooAzure Azure yığın hesapları dayalı artık kullanabilirsiniz. 
* Karşıya yükleme arşiv üzerinde 32 MB tooPremium depolama hesapları dosyaları artık şunları yapabilirsiniz
* Geliştirilmiş erişilebilirlik desteği
* Artık güvenilir Base-64 ekleyebilirsiniz kodlanmış X.509 SSL sertifikalarını giderek tooEdit tarafından -&gt; SSL sertifikalarını -&gt; alma sertifikaları

#### <a name="fixes"></a>Düzeltmeler

* Sabit: bir hesabın kimlik yenilendikten sonra hello ağaç görünümü bazen otomatik olarak yeniler değil
* Sabit: öykünücüsü kuyruklar ve tablolar için bir SAS oluşturma geçersiz bir URL neden olur
* Sabit: proxy etkinken premium depolama hesapları artık Genişletilebilir
* Sabit: hello Uygula düğmesini seçili 1 veya 0 hesapları varsa Yönetim sayfasında çalışmayan hello hesaplarında
* Sabit: çakışma çözümü gerektiren BLOB karşıya yükleme - 0.8.11 içinde sabit başarısız olabilir 
* Sabit: geri bildirim gönderme 0.8.12 içinde sabit 0.8.11 içinde-hatalı olan 

#### <a name="known-issues"></a>Bilinen sorunlar

* Too0.8.10 yükselttikten sonra toorefresh gerekir tüm kimlik bilgilerinizi.
* Giriş veya çıkış uzaklaştırılacağını olsa da, hello yakınlaştırma düzeyini kısa bir süre içinde toohello varsayılan düzeyini sıfırlayabilir.
* BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir.
* Merhaba Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir.
* BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz. Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur.
* Azure yığın şu anda dosya paylaşımlarını desteklemez ancak dosya paylaşımlarına düğümü ekli bir Azure yığın depolama hesabı altında görünmeye devam eder. 
* Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Ubuntu 14.04 yükleme gereksinimleri aşağıda verilmiştir:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Sürüm 0.8.9 / 0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Yeni

* Depolama Gezgini 0.8.9 hello güncelleştirmeleri için en son sürümünü otomatik olarak indirir.
* Düzeltme: bir portal kullanarak bir depolama hesabı hatayla sonuçlandı SAS URI'sini tooattach oluşturulur.
* Şimdi oluşturmak, yönetmek ve blob anlık görüntüleri yükseltin.
* Şimdi tooAzure Çin, Azure Almanya ve Azure ABD devlet kurumları hesaplarında oturum açabilir.
* Şimdi hello yakınlaştırma düzeyini değiştirebilirsiniz. Uzaklaştır, ve yakınlaştırma sıfırlama hello Görünüm menüsünde tooZoom Hello seçenekleri kullanın.
* Unicode karakterler, BLOB'lar ve dosyalar için kullanıcı meta verilerde artık desteklenmektedir.
* Erişilebilirlik geliştirmeleri.
* Merhaba sonraki sürüme ait sürüm notları hello güncelleştirme bildirimden görüntülenebilir. Merhaba geçerli sürüm notları hello Yardım menüsünden de görüntüleyebilirsiniz.

#### <a name="fixes"></a>Düzeltmeler

* Sabit: hello sürüm numarası artık doğru şekilde Windows Denetim Masası'nda görüntülenir
* Sabit: arama artık sınırlı too50, 000 düğümleri değil
* Sabit: hello hedef dizin zaten mevcut değilse karşıya yükleme tooa dosya paylaşımı sürekli başlar
* Sabit: kararlılığı uzun ve indirmelere için

#### <a name="known-issues"></a>Bilinen sorunlar

* Giriş veya çıkış uzaklaştırılacağını olsa da, hello yakınlaştırma düzeyini kısa bir süre içinde toohello varsayılan düzeyini sıfırlayabilir.
* Hızlı erişim yalnızca abonelik temel öğeleri ile çalışır. Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.
* Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak devam edebilir.
* BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir.

12/16/2016
### <a name="version-087"></a>Sürüm 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Yeni

* Nasıl bir güncelleştirme hello başında tooresolve çakışmaları indirin veya oturum hello etkinlikleri penceresindeki kopyalamak seçebilirsiniz
* Sekme toosee hello tam bir yol hello depolama kaynağı getirin
* Bir sekmede tıklattığınızda hello sol taraftaki gezinti bölmesindeki konumuyla eşitler

#### <a name="fixes"></a>Düzeltmeler

* Sabit: Depolama Gezgini güvenilen uygulama Mac üzerinde sunulmuştur
* Sabit: Ubuntu 14.04 yeniden desteklenir
* Sabit: Bazen hello eklemek UI abonelikler yüklenirken yanıp sönen hesabı
* Sabit: Bazen tüm depolama kaynaklarını hello sol taraftaki Gezinti Bölmesi'nde listelenen
* Sabit: hello eylem bölmesinde bazen boş eylemler görüntülenir
* Sabit: hello pencere boyutu son kapatılan hello oturumundan şimdi korunur
* Sabit: Hello için birden çok sekme açabilirsiniz hello bağlam menüsünü kullanarak aynı kaynak

#### <a name="known-issues"></a>Bilinen sorunlar

* Hızlı erişim yalnızca abonelik temel öğeleri ile çalışır. Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.
* Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak alabilir
* BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir
* Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performansı etkilenebilir veya işlenmeyen bir özel duruma neden olabilir
* Merhaba macOS üzerinde hello Depolama Gezgini'ni kullanarak ilk kez isteyen kullanıcının izni tooaccess Anahtarlık için birden çok komut istemlerini görebilirsiniz. Merhaba istemi yeniden göstermeyecektir şekilde her zaman izin ver seçeneğini öneririz

11/18/2016
### <a name="version-086"></a>Sürüm 0.8.6

#### <a name="new"></a>Yeni

* Artık PIN Hizmetleri toohello hızlı erişim için kolay gezinme en sık kullanılan yapabilecekleriniz
* Artık farklı sekmelerde birden çok düzenleyicileri açabilirsiniz. Tek tooopen geçici sekmesini tıklatın. çift tooopen kalıcı sekmesini tıklatın. Ayrıca hello geçici sekmesini toomake üzerinde kalıcı sekmesini tıklatabilirsiniz
* Fark edilebilir performans yapmış olduğunuz ve kararlılık geliştirmeleri için hızlı makinelerde büyük dosyalar için özellikle indirir ve yükler
* Boş "sanal" klasörler şimdi blob kapsayıcı oluşturulabilir
* Şimdi arama yapmak için iki seçeneğiniz vardır böylece biz bizim yeni Gelişmiş substring arama ile kapsamlı arama yeniden sunulmuştur: 
    * Genel arama - yalnızca hello arama metin kutusuna bir arama terimi girin
    * Kapsamlı arama - hello Büyüteç simgesini sonraki tooa düğümü, ardından hello yolu, bir arama terimi toohello sonuna ekleyin veya sağ tıklatın ve "Arama gelen burada" seçin
* Çeşitli temalar ekledik: açık (varsayılan), koyu, yüksek karşıtlık siyah ve yüksek karşıtlık beyaz. TooEdit - Git&gt; Temalar toochange tema tercihinizi
* Blob ve dosya özelliklerini değiştirebilirsiniz
* Kodlanmış (base64) ve kodlanmamış iletileri artık desteklenmektedir
* Linux üzerinde bir 64-bit işletim sistemi sunulmuştur gerekli. Bu sürüm için yalnızca 64-bit Ubuntu 16.04.1 destekliyoruz LTS
* Biz bizim logosu güncelleştirilmiş!

#### <a name="fixes"></a>Düzeltmeler

* Sabit: ekran dondurma sorunları
* Sabit: Gelişmiş Güvenlik
* Sabit: Bazen yinelenen ekli hesapları görünmez
* Sabit: Blob tanımlanmamış bir içerik türüne sahip bir özel durum da oluşturabilir
* Sabit: Boş bir tablo üzerinde açılış hello sorgu paneli mümkün değildi
* Sabit: arama hatalarda değişir
* Sabit: "Daha yük" tıklatıldığında 50 too100 yüklenen kaynak hello sayısı artar
* Sabit: bir hesap olarak imzalı değilse ilk çalıştırılmasında biz şimdi bu hesap için tüm abonelikleri varsayılan olarak seçin 

#### <a name="known-issues"></a>Bilinen sorunlar

* Bu sürümü hello Depolama Gezgini, Ubuntu 14.04 üzerinde çalışmaz
* tooopen aynı kaynak değil sürekli tıklayın hello için birden fazla sekme hello aynı kaynak. Üzerinde başka bir kaynak'ı tıklatın ve geri dönün ve hello özgün kaynak tooopen yeniden başka bir sekmede tıklatın 
* Hızlı erişim yalnızca abonelik temel öğeleri ile çalışır. Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.
* Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak alabilir
* BLOB'ları veya aynı hello yüklenen dosyalar 3'ten fazla gruba sahip zaman hatalara neden olabilir
* Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performansı etkilenebilir veya işlenmeyen bir özel duruma neden olabilir

10/03/2016
### <a name="version-085"></a>Sürüm 0.8.5

#### <a name="new"></a>Yeni

* Tooattach tooStorage kullanım Portal tarafından oluşturulan SAS anahtarları artık açabilir hesapları ve kaynakları

#### <a name="fixes"></a>Düzeltmeler

* Sabit: bazen arama sırasında yarış durumu Genişletilebilir olmayan düğümler toobecome neden
* Sabit: "HTTP kullan" tooStorage hesapları hesap adı ve anahtar ile bağlanırken çalışmıyor
* Sabit: SAS anahtarları (olanlar için özel Portal tarafından oluşturulan) "sondaki eğik çizgi" bir hata döndürür
* Sabit: tablo alma sorunları
    * Bölüm anahtarı ve satır anahtarını bazen tersine
    * "Bölüm anahtarlarını null" oluşturulamıyor tooread

#### <a name="known-issues"></a>Bilinen sorunlar

* Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performans etkilenmiş olabilir.
* Tooexpand dosyaları çalışılırken bir hata gösterir şekilde azure yığın dosyaları, şu anda desteklemiyor

09/12/2016
### <a name="version-084"></a>Sürüm 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Yeni

* Doğrudan bağlantılar toostorage hesapları, kapsayıcıları, kuyruklar, tablolar oluşturmak veya dosya paylaşımları paylaşım ve kolay tooyour - Windows kaynaklara ve Mac OS destek
* Blob kapsayıcılar, tablolar, kuyruklar, dosya paylaşımları veya hello arama kutusuna depolama hesaplarından arayın
* Merhaba Tablo Sorgu Oluşturucusu sorgu yan tümcelerinde şimdi gruplandırabilirsiniz
* Yeniden adlandırın ve blob kapsayıcıları, dosya paylaşımları, tablolar, BLOB'lar, blob klasörleri, dosyaları ve dizinlerden SAS bağlı hesapları ve kapsayıcılar içinde kopyala/yapıştır
* Yeniden adlandırma ve kopyalama kapsayıcıları blob ve dosya paylaşımları artık özellikleri ve meta verileri koru

#### <a name="fixes"></a>Düzeltmeler

* Sabit: boolean veya ikili özellikleri içermiyorsa tablo varlıkları düzenlenemez.

#### <a name="known-issues"></a>Bilinen sorunlar

* Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performans etkilenmiş olabilir.

08/03/2016
### <a name="version-083"></a>Sürüm 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Yeni

* Kapsayıcılar, tablolar, dosya paylaşımları yeniden adlandırma
* Gelişmiş Sorgu Oluşturucu deneyim
* Özelliği toosave ve yük sorguları
* Doğrudan bağlantılarını toostorage hesapları veya kapsayıcıları, kuyruklar, tablolar veya dosya paylaşımı ve kolayca kaynaklarınıza erişmek için paylaşımları (yalnızca Windows - macOS desteği yakında!)
* Özelliği toomanage CORS kuralları yapılandırın

#### <a name="fixes"></a>Düzeltmeler

* Sabit: Microsoft Accounts yeniden kimlik doğrulaması 8-12 saatte gerektirir

#### <a name="known-issues"></a>Bilinen sorunlar

* Bazen hello UI dondurulmuş görünebilir - hello penceresinin ekranı kaplamasını bu sorunu çözmenize yardımcı olur
* macOS yükleme yükseltilmiş izinler gerektirebilir
* Hesap Ayarları panelini sipariş toofilter abonelikleri tooreenter kimlik bilgilerine ihtiyacınız gösterebilir
* Yeniden adlandırma dosya paylaşımları, blob kapsayıcıları ve tablolar değil korumak meta verileri veya dosya paylaşım kotası, ortak erişim düzeyi veya erişim ilkeleri gibi hello kapsayıcısı üzerinde diğer özellikleri
* BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz. Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur
* Kopyalama veya kaynakları yeniden adlandırma SAS bağlı hesapları içinde çalışmıyor

07/07/2016
### <a name="version-082"></a>Sürüm 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Yeni

* Depolama hesapları abonelikler tarafından gruplandırılır; Geliştirme depolama ve anahtar veya SAS aracılığıyla bağlı kaynakları (yerel ve iliştirildiği) düğümünde gösterilir
* "Azure hesap ayarları" panelinde hesaplarından Oturumu Kapat
* Proxy ayarları tooenable yapılandırma ve oturum açma yönetme
* Oluşturma ve blob kira bölün
* Açık blob kapsayıcılar, kuyruklar, tablolar ve tek bir tıklatmayla dosyaları

#### <a name="fixes"></a>Düzeltmeler

* Sabit: .NET veya Java kitaplıklarıyla eklenen iletileri kuyruğa düzgün base64 kodlaması çözülür değil
* Sabit: $metrics tablolar için Blob Storage hesapları gösterilmez
* Sabit: tablolar düğümünü yerel (Geliştirme) depolama için çalışmıyor

#### <a name="known-issues"></a>Bilinen sorunlar

* macOS yükleme yükseltilmiş izinler gerektirebilir

06/15/2016
### <a name="version-080"></a>Sürüm 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Yeni

* Dosya Paylaşımı desteği: görüntüleme, karşıya yükleme, indirme, dosyaları ve dizinleri, SAS URI'ler kopyalama (oluşturma ve bağlanma)
* SAS URI'ler veya hesap anahtarlarla tooStorage bağlanmak için kullanıcı deneyimi geliştirildi
* Tablo sorgusu sonuçlarını dışarı aktarma
* Tablo sütun yeniden sıralamayı ve özelleştirme
* $Logs blob kapsayıcıları ve $metrics tabloları depolama hesapları için etkin Ölçümleriyle görüntüleme
* Geliştirilmiş dışarı aktarma ve davranış alma, artık özellik değeri türü içerir

#### <a name="fixes"></a>Düzeltmeler

* Sabit: karşıya yükleme veya büyük BLOB'ları indirme tamamlanmamış yüklemeleri/yüklemeler neden olabilir
* Sabit: düzenleme, ekleme ya da bir sayısal dize değeri ("1") sahip bir varlık alma toodouble dönüştürür
* Sabit: Oluşturulamıyor tooexpand hello tablo düğümünde hello yerel geliştirme ortamı

#### <a name="known-issues"></a>Bilinen sorunlar

* $metrics tabloları Blob Depolama hesapları için görünür değildir
* Merhaba iletileri Base64 kodlama kullanılarak kodlanır, program aracılığıyla eklenen iletileri kuyruğa düzgün görüntülenmeyebilir

05/17/2016
### <a name="version-07201605090"></a>Sürüm 0.7.20160509.0

#### <a name="new"></a>Yeni

* Daha iyi hata uygulaması için işleme kilitleniyor

#### <a name="fixes"></a>Düzeltmeler

* Oturum açma kimlik bilgileri gerekli olduğunda burada bilgi çubuğu iletileri bazen görünmüyor sabit hata

#### <a name="known-issues"></a>Bilinen sorunlar

* Tablolar: Ekleme, düzenleme, veya "1" veya "1.0" gibi muğlak sayısal bir değere sahip bir özelliği olan bir varlık alma ve kullanıcı çalıştığında toosend hello gibi bir `Edm.String`, hello değeri gelen geri hello istemcisi bir Edm.Double olarak API aracılığıyla

03/31/2016

### <a name="version-07201603250"></a>Sürüm 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Yeni

* Tablo desteği: görüntüleme, sorgulanırken, dışa aktarma, içeri aktarma ve varlıklar için CRUD işlemleri
* Sıra desteği: görüntüleme, ekleme, dequeueing iletileri
* Depolama hesapları için SAS URI oluşturma
* SAS URI'ler bağlanan tooStorage hesaplarıyla
* Gelecekteki güncelleştirmeleri tooStorage Explorer ilişkin güncelleştirme bildirimlerini
* Güncelleştirilmiş Görünüm

#### <a name="fixes"></a>Düzeltmeler

* Performans ve güvenilirlik geliştirmeleri

### <a name="known-issues-amp-mitigations"></a>Bilinen sorunlar &amp; Azaltıcı Etkenler

* İndirme büyük blob dosyaların düzgün çalışmıyor - AzCopy kullanırken, biz bu soruna öneririz 
* Hesap kimlik bilgilerini değil alınan ya da hello giriş klasörü bulunamıyor veya yazılamaz önbelleğe
* Biz ekleme, düzenleme veya "1" veya "1.0" gibi muğlak sayısal bir değere sahip bir özelliği olan bir varlık alma ve hello kullanıcı çalışırsa toosend olarak bir `Edm.String`, hello değeri gelen geri hello istemcisi bir Edm.Double olarak API aracılığıyla
* Çok satırlı kayıtları içeren CSV dosyalarını içeri aktarırken hello veri kesilmiş Tasarımlı karıştırılmış veya

02/03/2016

### <a name="version-07201601291"></a>Sürüm 0.7.20160129.1

#### <a name="fixes"></a>Düzeltmeler

* Karşıya yükleme, indirme ve BLOB kopyalama genel performansı

01/14/2016

### <a name="version-07201601050"></a>Sürüm 0.7.20160105.0

#### <a name="new"></a>Yeni

* Linux desteği (eşlik özellikleri tooOSX)
* BLOB kapsayıcıları ile paylaşılan erişim imzaları (SAS) anahtar Ekle
* Azure Çin için depolama hesapları ekleme
* Özel uç noktaları ile depolama hesapları ekleme
* Metin ve resim içeriği BLOB'ları hello açabilirsiniz
* Blob özellikleri ve meta verileri görüntüleyin ve düzenleyin

#### <a name="fixes"></a>Düzeltmeler

* Sabit: karşıya yükleme veya indirme çok sayıda BLOB (500 +) bazen hello uygulama toohave beyaz bir ekran neden olabilir 
* Sabit: hello kapsayıcı hello odaklanmak yeniden ayarlayana kadar blob kapsayıcısı genel erişim düzeyi ayarlanırken hello yeni değer güncelleştirilmez. Ayrıca, hello iletişim her zaman çok varsayılan olarak "hiçbir ortak erişim" ve hello gerçek geçerli değer değil.
* Daha iyi genel klavye/erişilebilirlik ve kullanıcı Arabirimi desteği
* Boşluk ile uzun olduğunda içerik haritalarında geçmiş metin sarmalar
* Giriş doğrulaması SAS iletişim destekler
* Kullanıcı kimlik bilgilerinin süresi dolmuş olsa bile yerel depolama toobe kullanılabilir devam eder
* Merhaba blob explorer hello sağ tarafında açılan blob kapsayıcısı silindiğinde, kapalı

#### <a name="known-issues"></a>Bilinen sorunlar

* Gcc sürüm güncelleştirilmiş veya yükseltilmiş – adımları tooupgrade Linux yükleme gereksinimleri aşağıda verilmiştir: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>Sürüm 0.7.20151116.0

#### <a name="new"></a>Yeni

* macOS ve Windows sürümleri
* Depolama hesaplarınızı tooview içinde oturum – Kurumsal hesap, Microsoft, 2FA, Account kullanın.
* Yerel geliştirme depolama (depolama öykünücüsünü kullanma yalnızca Windows)
* Azure Resource Manager ve klasik kaynak desteği
* Oluşturma ve BLOB, kuyruk veya tablo silme
* Belirli BLOB, kuyruk veya tablo Ara
* Blob kapsayıcıları Merhaba içeriğine keşfedin
* Görüntülemek ve dizinleri gidin
* Karşıya yükleyin, indirin ve BLOB'ları ve klasörleri silme
* Blob özellikleri ve meta verileri görüntüleyin ve düzenleyin
* SAS anahtarları oluştur
* Yönetmek ve depolanan erişim ilkeleri (SAP) oluşturun
* Ön eke göre BLOB Ara
* Sürükleme 'n açılan dosyaları tooupload veya indirme

#### <a name="known-issues"></a>Bilinen sorunlar

* Merhaba kapsayıcı hello odaklanmak yeniden ayarlayana kadar blob kapsayıcısı genel erişim düzeyi ayarlanırken hello yeni değer güncelleştirilmez
* Hello iletişim tooset hello genel erişim düzeyi açtığınızda, bu her zaman "Public erişim yok" hello varsayılan ve hello gerçek geçerli değer değil gösterir
* İndirilen BLOB'ları yeniden adlandırılamıyor
* Etkinlik günlüğü girişleri bazen "bir sürüyor takılıyor" ne zaman bir hata oluşur ve hello hata görüntülenmiyor belirtin.
* Bazen kilitleniyor kapatır tamamen tooupload çalışırken beyaz veya çok sayıda BLOB indirin
* Bazen bir kopyalama işlemi iptal ediliyor çalışmıyor
* Geçersiz bir ad girin ve toocreate devam (sırası/blob/tablosu) kapsayıcı oluşturma sırasında başka farklı kapsayıcı türü altında odak hello yeni tür ayarlanamaz
* Yeni bir klasör oluşturulamaz veya klasörünü yeniden adlandırın




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md