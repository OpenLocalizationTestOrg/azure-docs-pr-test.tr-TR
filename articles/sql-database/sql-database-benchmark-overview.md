---
title: "aaaAzure SQL veritabanı Kıyaslama genel bakış"
description: "Bu konuda hello Azure SQL veritabanı hello Azure SQL veritabanı performansını ölçmek kullanılan Kıyaslama açıklanmaktadır."
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Azure SQL veritabanı Kıyaslama genel bakış
## <a name="overview"></a>Genel Bakış
Microsoft Azure SQL veritabanı sunar üç [hizmet katmanları](sql-database-service-tiers.md) birden çok performans düzeyine sahip. Her performans düzeyi artan bir tasarlanmış kümesi kaynakları veya 'power' toodeliver giderek daha yüksek verimlilik sağlar.

Önemli toobe mümkün tooquantify hello artan her performans düzeyi gücünü artan veritabanı performansını nasıl çevirir olur. Bu Microsoft geliştirmiştir toodo hello Azure SQL veritabanı Kıyaslama (ASDB). Merhaba Kıyaslama temel işlemleri tüm OLTP iş yüklerini bulunan bir karışımını uygular. Biz her performans düzeyi çalışan veritabanları için elde hello iş hacmini ölçmek.

Merhaba kaynakları ve her hizmet katmanını ve performans düzeyi gücünü cinsinden ifade edilir [veritabanı işlem birimleri (Dtu'lar)](sql-database-what-is-a-dtu.md). Dtu'lar toodescribe hello performans düzeyinin göreli kapasitesini CPU, bellek, karışık bir ölçüyü temel ve okur ve her performans düzeyi tarafından sunulan oranları yazma bir yol sağlar. Bir veritabanı Hello DTU derecesi Katlama toodoubling hello veritabanı güç karşılık gelir. Merhaba Kıyaslama bize tooassess hello etkisi her performans düzeyine göre gerçek veritabanı işlemleri, veritabanı boyutu, kullanıcı ve işlem hızları sayısını oranda ölçekleme sırasında kullanan tarafından sunulan güç artırma hello veritabanı performansını sağlar. toohello sağlanan kaynakları toohello veritabanı.

Merhaba verimlilik hello temel hizmet katmanının her saat için işlemleri kullanarak ifade tarafından hello standart hizmet katmanında işlemleri dakika başına ve işlemleri daha kolay tooquickly yapar saniyede, kullanma hello Premium Hizmet katmanını kullanarak ilişkili hello Her bir uygulamanın hizmet katmanı toohello gereksinimlerini performans olasılığı.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Bağıntı kıyaslama sonuçları tooreal world veritabanı performansı
Bu önemli toounderstand tüm değerlendirmeleri gibi bu ASDB, yalnızca temsili ve göstergesi. Merhaba Kıyaslama uygulamayla elde oranları değil olması hello diğer uygulamalarla elde o aynı işlem hello. Merhaba Kıyaslama farklı bir işlem türleri bir dizi tablolar ve veri türlerini içeren bir şemaya karşı çalıştırmak koleksiyonunu içerir. Ortak tooall OLTP iş yüklerinin aynı temel işlemleri Hello Kıyaslama alıştırmaları hello olsa da, veritabanı veya uygulamanın belirli herhangi bir sınıf temsil etmiyor. Merhaba hello Kıyaslama tooprovide bir makul Kılavuzu toohello göreli yukarı veya aşağı Ölçeklendirmesi, performans düzeyleri arasında beklenen veritabanının performansını hedefidir. Gerçekte, veritabanları farklı boyutlarda ve karmaşıklık olan, iş yüklerini farklı bileşimleri karşılaştığınız ve farklı şekilde yanıt verir. Örneğin, bir g/ç yoğunluklu uygulama GÇ eşikleri er isabet veya bir CPU-yoğun uygulama CPU sınırları er isabet. Belirli bir veritabanını aynı şekilde artan altında hello Kıyaslama olarak yük hello ölçeklenir garanti yoktur.

Merhaba Kıyaslama ve metodolojisi aşağıdaki daha ayrıntılı olarak açıklanmıştır.

## <a name="benchmark-summary"></a>Kıyaslama özeti
ASDB çevrimiçi işlem işleme (OLTP) iş yükleri en sık karşılaşılan temel veritabanı işlemleri bir karışımını hello performansını ölçer. Merhaba Kıyaslama göz önünde bulut tasarlanmıştır ancak hello veritabanı şeması, veri doldurma ve işlemleri tasarlanmış toobe OLTP iş yüklerini en yaygın olarak kullanılan hello temel öğelerinin kapsamlı temsilcisi olmuştur.

## <a name="schema"></a>Şema
Merhaba şema tasarlanmış toohave yeterli çeşitli ve karmaşıklık toosupport çok çeşitli işlemleri olduğu. Merhaba Kıyaslama altı tabloları oluşan bir veritabanına karşı çalışır. Merhaba tabloları üç kategoriye ayrılır: sabit ölçekleme ve büyüyen boyutlu,. İki sabit boyutlu tablo vardır; üç ölçeklendirme tablolar; ve artan bir tablo. Sabit boyutlu tabloları sabit sayıda satıra sahip. Ölçeklendirme tabloları orantılı toodatabase performans olan ancak hello Kıyaslama sırasında değişmez kardinalitesi var. İlk yükleme ölçeklendirme bir tablo gibi tablo büyüyen hello boyuta sahip olmadığından, ancak sonra hello nicelik satır eklenen ve Silinen gibi hello Kıyaslama çalıştıran biri hello indirmelere içinde değişir.

Merhaba şeması içerir, tamsayı dahil olmak üzere veri türlerinin bir karışımını sayısal karakter ve tarih/saat. birincil ve ikincil anahtarlar, ancak hiçbir yabancı anahtarlar Hello şeması içerir - diğer bir deyişle, vardır hiçbir başvuru bütünlüğü kısıtlamalarını tablolar arasında.

Bir veri oluşturma programı hello ilk veritabanı için hello veriler üretir. Tamsayı ve sayısal veriler çeşitli stratejiler kullanılarak oluşturulur. Bazı durumlarda değerler rastgele bir aralığı içinde dağıtılır. Diğer durumlarda, belirli bir dağıtım korunur rastgele derlenemiyor tooensure değerler kümesidir. Metin alanları sözcükleri tooproduce gerçekçi görünümlü veri ağırlıklı listesinden üretilir.

bir "ölçek faktörü üzerinde." temel Hello veritabanı boyutu Merhaba ölçek çarpanı (BT kısaltılır) ölçekleme ve tabloları büyütme hello hello önemi belirler. Aşağıda açıklandığı gibi hello veritabanı boyutu, kullanıcılar ve tüm oranı tooeach diğer ölçek maksimum performans sayısı Bölüm kullanıcıları ve ilerleme, hello.

## <a name="transactions"></a>İşlemler
Hello iş yükü hello aşağıdaki tabloda gösterildiği gibi dokuz işlem türlerini oluşur. Her işlem tasarlanmış toohighlight sistem özelliklerine hello veritabanı motoru ve sistem donanımı belirli bir dizi, yüksek karşıtlık diğer işlemleri hello. Bu yaklaşım, farklı bileşenler toooverall performans daha kolay tooassess hello etkisini kolaylaştırır. Örneğin, "Okuma ağır" Merhaba işlem çok sayıda diskten okuma işlemleri üretir.

| İşlem türü | Açıklama |
| --- | --- |
| Lite okuma |SEÇİN; bellek içi; salt okunur |
| Okuma Orta |SEÇİN; çoğunlukla bellek içi; salt okunur |
| Okuma ağır |SEÇİN; çoğunlukla olmayan bellek içi; salt okunur |
| Lite güncelleştirme |GÜNCELLEŞTİRME; bellek içi; okuma-yazma |
| Ağır güncelleştir |GÜNCELLEŞTİRME; çoğunlukla olmayan bellek içi; okuma-yazma |
| Lite Ekle |INSERT; bellek içi; okuma-yazma |
| Ağır Ekle |INSERT; çoğunlukla olmayan bellek içi; okuma-yazma |
| Sil |DELETE; bellek içi ve değil bellek karışımı; okuma-yazma |
| CPU ağır |SEÇİN; bellek içi; görece yoğun CPU yükünü; salt okunur |

## <a name="workload-mix"></a>İş yükü karışımı
İşlemler, genel karışımı aşağıdaki hello ile ağırlıklı bir dağıtım noktasından rastgele seçilir. Merhaba genel karışımı yaklaşık 2:1 okuma/yazma oranını sahiptir.

| İşlem türü | Karışımı yüzdesi |
| --- | --- |
| Lite okuma |35 |
| Okuma Orta |20 |
| Okuma ağır |5 |
| Lite güncelleştirme |20 |
| Ağır güncelleştir |3 |
| Lite Ekle |3 |
| Ağır Ekle |2 |
| Sil |2 |
| CPU ağır |10 |

## <a name="users-and-pacing"></a>Kullanıcılar ve Adımlama
eş zamanlı kullanıcı sayısı, bağlantıları toosimulate hello davranışını kümesi boyunca işlemleri gönderir bir aracından Hello Kıyaslama iş yükü yönlendirilir. Tüm hello bağlantıları ve işlemleri oluşturulan makine olsa da, kolaylık sağlamak için biz toothese bağlantıları "kullanıcılar" olarak bakın Diğer tüm kullanıcıları bağımsız olarak her kullanıcı çalışır ancak tüm kullanıcılar hello gerçekleştirme adımları aşağıda gösterilen aynı döngüsü:

1. Bir veritabanı bağlantısı kurun.
2. İş tooexit kadar yineleyin:
   * Bir işlem rastgele (dağıtımdan bir ağırlıklı) seçin.
   * Seçili hello hareket ve ölçü hello yanıt süresi gerçekleştirin.
   * İlerleme Gecikmesini bekleyin.
3. Merhaba veritabanı bağlantısı kapatın.
4. Çıkış.

(2 c adımında) gecikmesine hello rastgele seçilir, ancak bir dağıtım 1.0 ikinci ortalama sahip. Bu nedenle her kullanıcı ortalama, saniye başına en fazla bir işlem oluşturabilir.

## <a name="scaling-rules"></a>Ölçeklendirme kuralları
Merhaba sayısı, kullanıcı hello veritabanı boyutu (Ölçek çarpanı birimleri) tarafından belirlenir. Her beş ölçek çarpanı birimler için bir kullanıcı yoktur. Gecikmesine hello nedeniyle, bir kullanıcı en fazla bir işlem saniye başına ortalama oluşturabilir.

Örneğin, bir ölçek faktörü 500 (BT = 500) veritabanı 100 kullanıcıların gerekir ve en çok saniyede 100 TP'leri elde edebilirsiniz. toodrive daha yüksek bir TP'leri hızı, daha fazla kullanıcı ve daha büyük bir veritabanı gerektirir.

Merhaba tabloda hello gerçekte her hizmet katmanını ve performans düzeyini Sürdürülen kullanıcı sayısını gösterir.

| Hizmet Katmanı (performans düzeyi) | Kullanıcılar | Veritabanı Boyutu |
| --- | --- | --- |
| Temel |5 |720 MB |
| Standart (S0) |10 |1 GB |
| Standart (S1) |20 |2.1 GB |
| Standart (S2) |50 |7.1 GB |
| Premium (P1) |100 |14 GB |
| Premium (P2) |200 |28 GB |
| Premium (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>Ölçüm süresi
Geçerli bir Kıyaslama en az bir saat kararlı durum ölçüm süresi gerektirir.

## <a name="metrics"></a>Ölçümler
Merhaba anahtar hello Kıyaslama, üretilen iş ve yanıt süresi ölçümleridir.

* Üretilen iş hello temel performans ölçüsü hello Kıyaslama içinde ' dir. İşleme birim--tüm işlem türleri sayım zaman, başına işlemlerde bildirilir.
* Yanıt süresi, performans öngörülebilirlik ölçüsüdür. Merhaba yanıt süresi kısıtlaması hizmetiyle aşağıda gösterildiği gibi daha sıkı bir yanıt süresi gereksinimi olan hizmet yüksek sınıfları sınıfının göre değişir.

| Hizmet sınıfı | Üretilen iş ölçü | Yanıt süresi gereksinimi |
| --- | --- | --- |
| Premium |Saniye başına işlem |0,5 saniye adresindeki 95. yüzdebirlik |
| Standart |Dakika başına işlem |1.0 saniye adresindeki 90 yüzdebirlik |
| Temel |Saat başına işlem |2.0 saniye adresindeki 80. yüzdebirlik |

## <a name="conclusion"></a>Sonuç
Hello Azure SQL veritabanı Kıyaslama hello göreli hello aralığını kullanılabilir hizmet katmanları ve performans düzeyleri arasında çalışan Azure SQL veritabanı performansını ölçer. Merhaba Kıyaslama çevrimiçi işlem işleme (OLTP) iş yükleri en sık karşılaşılan temel veritabanı işlemleri bir karışımını uygular. Gerçek performans ölçerek hello Kıyaslama hello etkisi daha anlamlı bir değerlendirme CPU hızı, bellek boyutu ve IOPS gibi her düzey tarafından sağlanan hello kaynakları listeleyerek mümkün olandan hello performans düzeyinin değiştirilmesi, verimlilik sağlar . Hello gelecekteki, biz tooevolve hello Kıyaslama toobroaden kapsamı devam et ve sağlanan hello verileri genişletin.

## <a name="resources"></a>Kaynaklar
[Giriş tooSQL veritabanı](sql-database-technical-overview.md)

[Hizmet katmanları ve performans düzeyleri](sql-database-service-tiers.md)

[Tek veritabanları için performans rehberi](sql-database-performance-guidance.md)
