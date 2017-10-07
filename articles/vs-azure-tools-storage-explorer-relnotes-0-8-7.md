---
title: "Azure Storage Gezgini (Önizleme) 0.8.7 aaaMicrosoft | Microsoft Docs"
description: "Microsoft Azure Storage Gezgini (Önizleme) 0.8.7 için sürüm notları"
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Microsoft Azure Storage Gezgini 0.8.7 (Önizleme)
## <a name="overview"></a>Genel Bakış
Bu makale, Azure Storage Gezgini 0.8.7 Önizleme sürümü için sürüm notları hello içerir.

[Microsoft Azure Storage Gezgini (Önizleme)](./vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan bir tek başına uygulamadır.

## <a name="azure-storage-explorer-087-preview"></a>Azure Storage Gezgini 0.8.7 (Önizleme)
### <a name="download-azure-storage-explorer-087-preview"></a>Azure Depolama Gezgini (Önizleme) 0.8.7 indirin
- [Windows için Azure Storage Gezgini 0.8.7 Önizleme](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Mac için Azure Storage Gezgini 0.8.7 Önizleme](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Linux için Azure Storage Gezgini 0.8.7 Önizleme](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Yeni güncelleştirmeler
* Nasıl bir güncelleştirme hello başında tooresolve çakışmaları indirin veya kopyalama oturum hello seçebilirsiniz **etkinlikleri** penceresi.
* Sekmesinde toosee hello tam bir yol hello depolama kaynağı gelin.
* Sekme tıklattığınızda hello sol taraftaki gezinti bölmesindeki konumuyla eşitler.

### <a name="fixes"></a>Düzeltmeler
* Sabit: Depolama Gezgini güvenilen uygulama macOS üzerinde sunulmuştur.
* Sabit: Ubuntu 14.04 yeniden desteklenir.
* Sabit: Bazen hello eklemek hesap UI abonelikler yüklenirken yanıp sönen.
* Sabit: Bazen tüm depolama kaynaklarını hello sol taraftaki Gezinti Bölmesi'nde listelenen.
* Sabit: hello eylem bölmesinde, bazen boş eylemler görüntülenir.
* Sabit: hello pencere boyutu son kapatılan hello oturumundan şimdi korunur.
* Sabit: Hello için birden çok sekme açabilirsiniz hello bağlam menüsünü kullanarak aynı kaynak.

### <a name="known-issues"></a>Bilinen sorunlar
* Hızlı erişim yalnızca abonelik tabanlı öğeleri ile çalışır. Yerel kaynaklar veya anahtar veya SAS belirteci üzerinden bağlı kaynakları bu sürümde desteklenmez.
* Hızlı erişim birkaç saniye toonavigate toohello hedef kaynak, sahip olduğunuz kaç kaynak bağlı olarak devam edebilir.
* BLOB'ları veya aynı hello yüklenen dosyalar üçten fazla gruba sahip zaman hatalara neden olabilir.
* Bundan sonra kabaca 50.000 düğümlere - arama arama tanıtıcıları performansı etkilenebilir veya işlenmeyen özel durumlara neden olabilir.
* Merhaba macOS üzerinde hello Depolama Gezgini'ni kullanarak ilk kez isteyen kullanıcının izni tooaccess hello Anahtarlık için birden çok komut istemlerini görebilirsiniz. Seçtiğiniz önerdiğimiz **her zaman izin ver** hello istemi yeniden görüntülenmeyecek şekilde

## <a name="previous-releases"></a>Önceki sürümler
### <a name="features"></a>Özellikler
#### <a name="main-features"></a>Önemli özellikleri
* macOS, Linux ve Windows sürümleri
* İçinde tooview abonelik tarafından gruplandırılmış depolama hesaplarınızı imzalayın:
    * Kurumsal hesap, Microsoft, 2FA, Account kullanın.
    * Yapılandırma ve proxy ayarlarını yönetme
    * Oturumunuzu hesaplarını kaldırın
* TooStorage hesaplarını kullanarak bağlanın:
    * Anahtar ve hesap adı
    * Özel uç noktaları (Azure Çin'de dahil)
    * SAS URI'sini depolama hesapları
* Azure Resource Manager ve klasik depolama desteği
* BLOB'ları, blob kapsayıcılar, kuyruklar, tablolar veya dosya paylaşımları için SAS anahtarları oluştur
* Paylaşılan erişim imzaları (SAS) anahtarıyla tooblob kapsayıcıları, kuyruklar, tablolar veya dosya paylaşımlarına bağlanmak
* Blob kapsayıcıları, kuyruklar, tablolar veya dosya paylaşımları için depolanan erişim ilkelerini yönetme
* Depolama öykünücüsü (yalnızca Windows) ile yerel geliştirme depolama
* Oluşturma ve blob kapsayıcılar, kuyruk veya tablo silme
* Görünüm $logs blob kapsayıcıları ve $metrics tabloları
* Belirli BLOB, kuyruklar, tablolar veya dosya paylaşımları için arama
* Doğrudan bağlantılar toostorage hesapları veya kapsayıcıları, kuyruklar, tablolar veya dosya paylaşımı ve kolayca kaynaklarınıza erişmek için paylaşır
* Blob kapsayıcılar, tablolar, dosya paylaşımları yeniden adlandırma
* Özelliği toomanage CORS kuralları yapılandırın
* Birincil ve ikincil anahtar depolama hesapları için kolayca kopyalayın
* Karşıya yükleme ve indirme veri bütünlüğü ve tutarlılık için MD5 denetler
* Blob kapsayıcılar, tablolar, kuyruklar, dosya paylaşımları veya hello arama kutusuna depolama hesaplarından arayın
* Artık PIN Hizmetleri toohello hızlı erişim için kolay gezinme en sık kullanılan yapabilecekleriniz
* Artık farklı sekmelerde birden çok düzenleyicileri açabilirsiniz. Tek tooopen geçici sekmesini tıklatın. tooopen kalıcı bir sekme çift tıklayın. Merhaba geçici sekmesini toomake tıklatabilirsiniz, kalıcı bir sekmesi
* Ve hızlı makinelerde büyük dosyalar için özellikle indirmelere için belirgin performans ve kararlılık geliştirmeleri
* Merhaba Gelişmiş kapsamlı arama ve kapsamı eklenen hello kavramı biz yeniden eklenmesiyle. Sağ tıklatma -> "Arama gelen buraya", veya el ile tooscope bu düğüm, Hello yolu tooa düğümü hello vurgulu simgesi girin. Kapsamlı sonra hello toodeep arama yolu o düğümünden başlayan bir arama terimi toohello sonuna ekleyebilirsiniz
* Çeşitli temalar ekledik: açık (varsayılan), koyu, yüksek karşıtlık siyah ve yüksek karşıtlık beyaz.
* Git tooEdit tema tercihinizi Temalar toochange ->
* Linux üzerinde bir 64-bit işletim sistemi sunulmuştur gerekli
* Biz bizim logosu güncelleştirilmiş!
#### <a name="blobs"></a>Bloblar
* BLOB'ları görüntülemek ve dizinleri gidin
* Karşıya yükleyin, indirin, silme ve BLOB'ları ve klasörleri kopyalama
* Metin ve resim içeriği BLOB'ları hello açabilirsiniz
* Blob özellikleri ve meta verileri görüntüleyin ve düzenleyin
* Ön eke göre BLOB Ara
* Oluşturun ve blobları ve blob kapsayıcıları için kira sürelerini bölün
* Sürükleme 'n dosyaları tooupload bırak
* BLOB'ları ve klasörleri yeniden adlandırma
* Boş "sanal" klasörler şimdi blob kapsayıcı oluşturulabilir
* Merhaba Blob ve dosya özelliklerini değiştirebilirsiniz
#### <a name="tables"></a>Tablolar
* Görüntüleyin ve ODATA varlık sorgu veya Sorgu Oluşturucu toocreate karmaşık sorgular kullanın
* Ekleme, düzenleme, varlıklarını silme
* İçeri ve dışarı aktarma İçindekiler CSV biçiminde (sorgu sonuçlarını dışarı aktarma dahil)
* Sütun sırasını özelleştirme
* Özelliği toosave sorguları
#### <a name="queues"></a>Kuyruklar
* Son 32 iletiye göz atın
* Eklemek için dequeue, iletilerini görüntüleme
* Kuyruğu temizleyin
* Sıra iletilerinizi tooencode ve çözmek istediğiniz olup olmadığını biz, toodecide olası yapılan
#### <a name="file-shares"></a>Dosya Paylaşımları
* Dosyaları görüntülemek ve dizinleri gidin
* Dosya ve dizinleri karşıya yükleyin, indirin, silin, kopyalayın
* Dosya özellikleri görüntüle
* Dosyaları ve dizinleri yeniden adlandırma

### <a name="bug-fixes"></a>Hata düzeltmeleri
* Sabit: ekran dondurma sorunları
* Sabit: Gelişmiş Güvenlik

### <a name="known-issues"></a>Bilinen sorunlar
* Bundan sonra kabaca 50.000 düğümlere - arama tanıtıcıları performans etkilenen macOS yükleme olabilir arama yükseltilmiş izinler gerektirebilir
* Hesap Ayarları panelini tooreenter kimlik bilgileri toofilter abonelikleri gerektiğini gösterebilir
* BLOB'lar (ayrı ayrı veya yeniden adlandırılmış blob kapsayıcısı içinde) yeniden adlandırma anlık görüntüleri korumaz. Diğer tüm özellikleri ve meta veri BLOB'lar, dosyalar ve varlıklar için bir yeniden adlandırma sırasında korunur
* Azure yığın şu anda desteklemiyor dosyaları, bu nedenle tooexpand hello çalışırken **dosyaları** düğümü hatayla sonuçlanır
* Linux 14.04 yükleme güncelleştirilmiş veya yükseltilmiş gcc sürüm olması gerekir. Merhaba aşağıdaki adımları göstermek nasıl tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Önceki sürümler
#### <a name="october-2016-release-version-085"></a>Ekim 2016 sürüm (sürüm 0.8.5)
* [Windows için indirin](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Mac için indirme](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Linux için indirme](https://go.microsoft.com/fwlink/?LinkId=809308)
