---
title: "Veri Yönetimi ağ geçidi için aaaRelease notları | Microsoft Docs"
description: "Veri Yönetimi ağ geçidi yazı sürüm notları"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Veri Yönetimi Ağ Geçidi için sürüm notları
Merhaba zorluklar modern veri tümleştirme için şirket içi toocloud gelen toomove veri tooand biridir. Data Factory veri yönetimi, şirket içi tooenable karma veri taşıma yükleyebilmek için bir aracı olan ağ geçidi ile tümleştirme sağlar.

Makaleler veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için aşağıdaki hello bakın ve nasıl toouse onu:

*  [Veri Yönetimi Ağ Geçidi](data-factory-data-management-gateway.md)
*  [Şirket içi arasında veri taşıyabilir ve Azure Data Factory kullanarak bulut](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>GEÇERLİ SÜRÜM (2.10.6347.7)

### <a name="enhancements-"></a>Geliştirmeler-
- Uygulamaları güvenilir listeye almayı yerine DNS girişlerini toowhitelist hizmet veri yolu tüm Azure IP adresleri, Güvenlik Duvarı (gerekirse) ekleyebilirsiniz. Azure Portal'da ilgili DNS girişi bulabilirsiniz (Data Factory -> 'Geliştir ve Dağıt' -> 'Ağ geçidi' -> (JSON içinde) "serviceUrls"
- HDFS bağlayıcı kendinden imzalı bir ortak sertifika SSL Doğrulamayı atla izin vererek olarak destekler.
- Sabit: Ağ geçidi çevrimdışı (son tooclock eğriltme) güncelleştirme sorun



## <a name="earlier-versions"></a>Önceki sürümleri

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Geliştirmeler-
-   Uygulamaları güvenilir listeye almayı yerine DNS girişlerini toowhitelist Service Bus tüm Azure IP adresleri, Güvenlik Duvarı (gerekirse) ekleyebilirsiniz. Daha fazla ayrıntı burada.
-   Şimdi tek blok blobu too4.75 blok blobu hello desteklenen en büyük boyutu TB yukarı/gruptan veri kopyalayabilirsiniz. (önceki sınırı 195 GB'den okunurdu).
-   Sabit: Kopyalama etkinliği sırasında birkaç küçük dosyalar unzipping çalışırken bellek sorununu dışı.
-   Sabit: Dizin belge DB tooan kopyalama sırasında aralığı sorunu dışında SQL Server benzersizlik özelliği ile şirket içi.
-   Sabit: SQL temizleme betiğini Kopyalama Sihirbazı'ndan şirket içi SQL Server ile çalışmaz.
-   Sabit: Hello sonunda boşluk sütun adıyla kopyalama etkinliği çalışmaz.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Geliştirmeler-
- Sabit: ağ geçidi makinenin yeniden başlatılmasını kimlik bilgileri eksik olan sorun.
- Sabit: Kayıt sırasında ağ geçidi ile ilgili sorun geri yedekleme dosyası kullanarak.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Geliştirmeler-
- Sabit: Kaynak olarak Oracle arasında ondalık null değer yanlış okuyun.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>Yenilikler
- Müşteri geri bildirim deneyimi kaydetme ağ geçidinde sağlayabilir.
- Yeni bir sıkıştırma biçimi destekler: ZIP (Deflate)

### <a name="enhancements-"></a>Geliştirmeler-
- Oracle havuz, HDFS kaynak için performans geliştirmesi.
- Ağ geçidi işleme kapasitesi paralel hata düzeltmesi için ağ geçidi otomatik güncelleştirme.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Geliştirmeleri
- Daha güçlü ve geliştirilmiş ağ geçidi kayıt deneyimi hello kayıt deneyimi daha iyi yanıt kılan hello ağ geçidi kayıt işlemi sırasında ilerleme durumunu izleyebilirsiniz artık-.
- Bu güncelleştirme ile Merhaba ağ geçidi yedekleme dosyası yoksa bile gelişme ağ geçidi geri yükleme işlem, ağ geçidi kurtarmaya devam edebilirsiniz. Bu, Portal tooreset bağlantılı hizmet kimlik bilgileri gerektirir.
- Hata düzeltmesi.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>Yenilikler

- Şimdi veri kaynağı kimlik bilgileri yerel olarak depolayabilirsiniz. Merhaba kimlik bilgileri şifrelenir. Merhaba veri kaynağı kimlik bilgileri kurtarılabilir ve ağ geçidi, tüm şirket içi varolan hello aktarılabilir hello yedekleme dosyasını kullanarak geri.

### <a name="enhancements-"></a>Geliştirmeler-

- Geliştirilmiş ve daha sağlam ağ geçidi kayıt deneyimi.
- Otomatik algılama quotechar özelliğine yapılandırmasının Kopyalama Sihirbazı'nı metin biçiminde destek ve hello geliştirmek genel, algılama doğruluğu biçimlendirin.

## <a name="2361002"></a>2.3.6100.2

- Metin dosyaları kopyalama Sihirbazı'nda firstRowAsHeader ve SkipLineCount otomatik algılama şirket içi dosya sistemi ve HDFS'i destekler.
- Ağ geçidi ile Service Bus arasındaki ağ bağlantısının Hello kararlılığını geliştirmek
- Birkaç hata düzeltmeleri


## <a name="2260721"></a>2.2.6072.1

*  Merhaba ağ geçidi Yapılandırma Yöneticisi'ni kullanarak hello ağ geçidi için HTTP proxy ayarını destekler. Yapılandırılmışsa, Azure Blob, Azure Table, Azure Data Lake ve belge DB HTTP proxy üzerinden erişilir.
*  TextFormat için veri kopyalama işlemi sırasında işleme destekler üstbilgi / tooAzure Blob, Azure Data Lake Store, şirket içi dosya sistemi ve şirket içi HDFS.
*  Veri ekleme Blob ve sayfa blobu hello birlikte zaten kopyalama destekler blok blobu desteklenir.
*  Yeni bir ağ geçidi durumu tanıtır **çevrimiçi (sınırlı)**, o hello ana işlevlerini hello ağ geçidi belirten çalışır hello etkileşimli işlemi Kopyalama Sihirbazı'nı desteği dışında.
*  Kayıt anahtarı kullanarak ağ geçidi kaydı Hello sağlamlık geliştirir.

## <a name="216040"></a>2.1.6040.

*  DB2 sürücüsü hello ağ geçidi yükleme paketini artık dahil edilmiştir. Tooinstall gerekmez, ayrı olarak.
*  DB2 sürücüsü artık destekliyor z/OS ve DB2 için t (AS / 400) zaten desteklenen hello platformlar (Linux, Unix ve Windows) ile birlikte.
*  Azure Cosmos DB şirket içi veri depoları için bir kaynak veya hedef olarak kullanılmasını destekler
*  Merhaba birlikte veri öğesinden/toocold/hot blob depolama zaten kopyalama destekler, genel amaçlı depolama hesabı desteklenmiyor.
*  Tooconnect tooon içi sağlayan uzak oturum açma ayrıcalıklarına sahip ağ geçidi üzerinden SQL Server'a.  

## <a name="2060131"></a>2.0.6013.1

*  El ile yükleme sırasında bir ağ geçidi tarafından kullanılan hello dil/kültür toobe seçebilirsiniz.

*  Ağ geçidi beklendiği gibi çalışmaz, son yedi gün tooMicrosoft toofacilitate hello sorun giderme toosend gateway günlükleri seçebilirsiniz. Ağ geçidi değilse bağlı toohello bulut hizmeti, toosave seçin ve ağ geçidi günlüklerini arşivleyin.  

*  Ağ geçidi Yapılandırma Yöneticisi için kullanıcı arabirimi iyileştirmeleri:

    *  Ağ geçidi durumu daha görünür hello Giriş sekmesinde yapın.

    *  Yeniden düzenlenen ve Basitleştirilmiş denetler.

    *  Hello kullanarak bir depolama biriminden veri kopyalayabilirsiniz [Kodsuz kopya önizleme aracını](data-factory-copy-data-wizard-tutorial.md). Bkz: [hazırlanan kopyalama](data-factory-copy-activity-performance.md#staged-copy) bu hakkındaki ayrıntılar için özelliklere genel.
*  Veri Yönetimi ağ geçidi tooingress verileri doğrudan bir şirket içi SQL Server veritabanını Azure Machine Learning kullanabilirsiniz.

*  Performans iyileştirmeleri

    * Şema/Önizleme SQL sunucusuna karşı Kodsuz kopyalama Önizleme aracında görüntüleme performansı.

## <a name="11259531"></a>1.12.5953.1

*  Hata düzeltmeleri

## <a name="11159181"></a>1.11.5918.1

*  Merhaba ağ geçidi olay günlüğünün en büyük boyutu 1 MB too40 MB'den çıkarılmıştır.

*  Ağ geçidi otomatik güncelleştirme sırasında yeniden başlatma gerektiğinde bir uyarı iletişim kutusu görüntülenir. Sonra ya da daha sonra toorestart sağ seçebilirsiniz.

*  Otomatik güncelleştirme başarısız olursa, otomatik güncelleştirme en fazla üç kez konumundaki ağ geçidi yükleyicisi yeniden dener.

*  Performans iyileştirmeleri

    * Şirket içi sunucudan Kodsuz kopyalama senaryosu büyük tabloları yüklenmesi için performansı.

*  Hata düzeltmeleri

## <a name="11058921"></a>1.10.5892.1

*  Performans iyileştirmeleri

*  Hata düzeltmeleri

## <a name="1958652"></a>1.9.5865.2

*  Sıfır dokunma otomatik güncelleştirme özelliği
*  Ağ geçidi Durum göstergeleri ile yeni Tepsi simgesi
*  Özelliği çok "güncelleştir şimdi" Merhaba istemciden
*  Özelliği tooset güncelleştirme zamanlama süresi
*  Otomatik güncelleştirmeyi Aç/Kapat geçiş için PowerShell Betiği
*  JSON biçimi desteği  
*  Performans iyileştirmeleri
*  Hata düzeltmeleri

## <a name="1858221"></a>1.8.5822.1

*  Sorun giderme deneyimini geliştirmeye
*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1757951"></a>1.7.5795.1

*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1757641"></a>1.7.5764.1

*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1657351"></a>1.6.5735.1

*  Şirket içi HDFS kaynak/havuz desteği
*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1656961"></a>1.6.5696.1

*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1656761"></a>1.6.5676.1

*  Configuration Manager Destek Tanılama araçları
*  Tablo sütunları tablo veri kaynakları için Azure Data Factory için destek.
*  Azure Data Factory SQL DW desteği
*  Azure veri fabrikası için BlobSource ve FileSource Reclusive desteği
*  Destek CopyBehavior – MergeFiles, PreserveHierarchy ve BlobSink ve Azure veri fabrikası için ikili kopyayla FileSink FlattenHierarchy
*  Kopya etkinliği Azure Data Factory için ilerleme durumu raporlama desteği
*  Azure veri fabrikası için destek veri kaynağı bağlantısı doğrulama
*  Hata düzeltmeleri

### <a name="1656721"></a>1.6.5672.1

*  ODBC veri kaynağı için tablo adı için Azure Data Factory destek
*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1656581"></a>1.6.5658.1

*  Destek dosyası havuz için Azure veri fabrikası
*  Hiyerarşi için Azure Data Factory ikili kopyasında koruma desteği
*  Azure veri fabrikası için kopyalama etkinliği benzersizlik desteği
*  Hata düzeltmeleri

### <a name="1656401"></a>1.6.5640.1

*  3 daha fazla veri kaynakları (ODBC, OData, HDFS) Azure Data Factory için destek
*  Azure Data Factory için csv ayrıştırıcısını tırnak işareti karakteri desteği
*  Sıkıştırma desteği (Bzıp2)
*  Hata düzeltmeleri

### <a name="1556121"></a>1.5.5612.1

*  Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata ve Sybase) için beş ilişkisel veritabanlarını destekler
*  Sıkıştırma desteği (Gzip ve Deflate)
*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1455491"></a>1.4.5549.1

*  Azure Data Factory için Oracle veri kaynağı destek ekleme
*  Performans iyileştirmeleri
*  Hata düzeltmeleri

### <a name="1454921"></a>1.4.5492.1

*  Microsoft Azure veri fabrikası ve Office 365 Power BI hizmetlerini destekleyen birleşik ikili
*  Merhaba yapılandırma kullanıcı Arabirimi ve kayıt işlemini daraltın
*  Azure Data Factory – Azure giriş ve çıkış desteklemek için SQL Server veri kaynağı

### <a name="1253031"></a>1.2.5303.1

*  Zaman aşımı sorunu toosupport daha uzun süren veri kaynağı bağlantılarını düzeltin.

### <a name="1155268"></a>1.1.5526.8

*  .NET Framework 4.5.1 Kurulum sırasında bir önkoşul olarak gereklidir.

### <a name="1051442"></a>1.0.5144.2

*  Azure Data Factory senaryoları etkileyen değişiklik yok.
