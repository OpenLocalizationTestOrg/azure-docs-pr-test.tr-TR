---
title: "SQL veri ambarı aaaConcurrency ve iş yükü yönetimi | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse eşzamanlılık ve iş yükü yönetimi anlayın."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>SQL veri ambarı eşzamanlılık ve iş yükü yönetimi
ölçekli olarak Microsoft Azure SQL Data Warehouse toodeliver tahmin edilebilir performans yardımcı olan denetim eşzamanlılık düzeyleri ve bellek ve CPU önceliği gibi kaynak ayırma. Bu makalede nasıl her iki özellik uygulanan ve nasıl veri ambarında denetlenebilecek açıklayan eşzamanlılık ve iş yükü yönetimi toohello kavramları tanıtır. SQL veri ambarı iş yükü çok kullanıcılı ortamlar destek hedeflenen toohelp yönetimidir. Çoklu kiracı iş yükleri için tasarlanmamıştır.

## <a name="concurrency-limits"></a>Eşzamanlılık sınırları
SQL veri ambarı too1, 024 eşzamanlı bağlantı sağlar. Tüm 1.024 bağlantıları sorguları eşzamanlı olarak gönderebilirsiniz. Ancak, SQL Data Warehouse toooptimize üretilen işi her sorgu en az bellek ataması aldığını bazı sorgular tooensure sırası. Queuing sorgu yürütme sırasında oluşur. Eşzamanlılık sınırları ulaşıldığında, SQL Data Warehouse artırabilirsiniz olduğunda queuing sorgular tarafından bellek kaynaklarının etkin sorgular erişim toocritically elde etmenizi sağlayarak toplam verimlilik gereklidir.  

Eşzamanlılık sınırları iki kavramları tarafından yönetilir: *eş zamanlı sorguları* ve *eşzamanlılık yuvaları*. Bir sorgu tooexecute için hello sorgu eşzamanlılık sınırı ve hello eşzamanlılık yuvası ayırma içinde yürütülmelidir.

* Eş zamanlı sorgular olan hello sorguları aynı hello yürütme süresi. SQL veri ambarı too32 eşzamanlı hello daha büyük DWU boyutları sorgulamaları yukarı destekler.
* Eşzamanlılık yuvaları üzerinde DWU göre ayrılır. Her 100 DWU 4 eşzamanlılık yuvası sağlar. Örneğin, bir DW100 4 eşzamanlılık yuvası ayırır ve 40 DW1000 ayırır. Bir veya daha fazla eşzamanlılık yuvaları, üzerinde hello bağımlı her sorgu tüketir [kaynak sınıfı](#resource-classes) hello sorgu. Merhaba smallrc kaynak sınıfında çalışan sorguları bir eşzamanlılık yuvası kullanabilir. Sorguları daha yüksek bir kaynak sınıfında çalıştırma başka eşzamanlılık yuva kullanabilir.

Merhaba aşağıdaki tabloda hello sınırları eş zamanlı sorgular ve hello adresindeki eşzamanlılık yuvaları için çeşitli DWU boyutları açıklanmaktadır.

### <a name="concurrency-limits"></a>Eşzamanlılık sınırları
| DWU | En fazla eş zamanlı sorgular | Ayrılmış eşzamanlılık yuvaları |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Bu eşikler biri karşılandığında yeni sorgular sıraya ve bir ilk giren ilk çıkar özelliğine sahip temelinde yürütülür.  Sıraya alınan sorguları bir sorguları tamamlandıktan ve hello sınırları hello sayısı sorgular ve yuvaları denk olarak yayımlanmıştır. 

> [!NOTE]  
> *Seçin* sorguları özel olarak üzerinde yürütme (Dmv'leri) dinamik yönetim görünümleri veya Katalog görünümleri değil yönetilir hello eşzamanlılık sınırları biriyle. Merhaba sistem hello sorguları üzerinde yürütme sayısı bağımsız olarak izleyebilirsiniz.
> 
> 

## <a name="resource-classes"></a>Kaynak sınıfları
Kaynak bellek ayırma ve CPU döngülerini tooa sorgu verilen denetlemenize yardımcı olur sınıfları. İki tür kaynak sınıfları tooa kullanıcı veritabanı rolleri hello biçiminde atayabilirsiniz. iki tür kaynak sınıfı Hello aşağıdaki gibidir:
1. Dinamik kaynak sınıflar (**smallrc, mediumrc, largerc, xlargerc**) bir değişken hello bağlı olarak bellek miktarını tahsis geçerli DWU. Bunun anlamı tooa ölçeklendirdiğinizde büyük DWU sorgularınızı otomatik olarak daha fazla bellek alın. 
2. Statik kaynak sınıflar (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) hello tahsis bellek bakılmaksızın aynı miktarda hello geçerli DWU (koşuluyla DWU kendisini hello yeterli bellek olduğundan). Bu büyük Dwu üzerinde size daha fazla sorguları her kaynak sınıfında eşzamanlı olarak çalıştırabileceği anlamına gelir.

Kullanıcılar **smallrc** ve **staticrc10** daha az miktarda belleğe verilir ve daha yüksek eşzamanlılık avantajından yararlanabilirsiniz. Kullanıcılar buna karşılık, atanan çok**xlargerc** veya **staticrc80** büyük miktarlarda bellek, verilir ve bu nedenle daha az sorgularını çalışabilir.

Varsayılan olarak, her kullanıcı hello küçük bir kaynak sınıfı üyesidir **smallrc**. Merhaba yordamı `sp_addrolemember` olan tooincrease hello kaynak sınıfı, kullanılan ve `sp_droprolemember` olan toodecrease hello kaynak sınıfı kullanılır. Örneğin, bu komut loaduser hello kaynak sınıfının çok artırır**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Kaynak sınıfları getirmiyor sorguları

Birkaç daha büyük bir bellek ayırma faydalanmaz sorgu türleri vardır. Merhaba sistem kendi kaynak sınıfı ayırma yoksayar ve her zaman bu sorgular hello küçük kaynak sınıfında yerine çalıştırın. Bu sorguları her zaman hello küçük kaynak sınıfında çalıştırırsanız, olduğunda eşzamanlılık yuvaları baskısı altında ve gerekli olandan daha fazla yuvaları tüketmemesidir çalıştırabilirsiniz. Bkz: [kaynak sınıf özel durumları](#query-exceptions-to-concurrency-limits) daha fazla bilgi için.

## <a name="details-on-resource-class-assignment"></a>Kaynak sınıf ataması ilgili ayrıntılar


Kaynak sınıfı birkaç daha fazla bilgi:

* *Rol alter* izni gereklidir, bir kullanıcının toochange hello kaynak sınıfı.
* Bir kullanıcı tooone veya daha fazla hello daha yüksek kaynak sınıfları ekleyebilirsiniz, ancak dinamik kaynak sınıfları statik kaynak sınıfları önceliklidir. Diğer bir deyişle, bir kullanıcı tooboth atanmışsa **mediumrc**(dinamik) ve **staticrc80**(statik) **mediumrc** uygulanır hello kaynak sınıfı.
 * Bir kullanıcı belirli bir kaynak sınıfı türü (birden fazla dinamik kaynak sınıfı veya birden çok statik kaynak sınıfı) bir kaynak sınıfında daha toomore atandığında, hello en yüksek kaynak sınıfı uygulanır. Diğer bir deyişle, bir kullanıcı tooboth mediumrc ve largerc atanmışsa hello daha yüksek kaynak sınıfı (largerc) uygulanır. Ve bir kullanıcı tooboth atanmışsa **staticrc20** ve **statirc80**, **staticrc80** ayardaki değil.
* Merhaba sistem yönetici kullanıcı Hello kaynak sınıfının değiştirilemez.

Ayrıntılı bir örnek için bkz: [değiştirme kullanıcı kaynak sınıfı örneği](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Bellek ayırma
Bir kullanıcının kaynak sınıfı Artıları ve eksileri tooincreasing vardır. Bir kullanıcı için bir kaynak sınıfı artırılması, sorgularını daha hızlı sorgu yürütebilir olduğu anlamına gelebilir erişim toomore belleği sağlar.  Ancak, daha yüksek kaynak sınıfları ayrıca çalıştırabilirsiniz eş zamanlı sorguları hello sayısını azaltın. Büyük miktarlarda bellek tooa tek sorgu ayırma veya bellek ayırmaları, aynı anda toorun da gereken diğer sorgular vererek arasında hello dengelemeyi budur. Bir kullanıcı bir sorgu için bellek yüksek ayırmaları verilirse, diğer kullanıcıların erişim toothat sahip olmaz aynı bellek toorun bir sorgu.

Aşağıdaki tablonun hello hello bellek tooeach dağıtım DWU ve kaynak sınıfı tarafından eşler.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Dinamik kaynak sınıfları (MB) için dağıtım başına bellek ayırma
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1,600 |
| DW500 |100 |400 |800 |1,600 |
| DW600 |100 |400 |800 |1,600 |
| DW1000 |100 |800 |1,600 |3,200 |
| DW1200 |100 |800 |1,600 |3,200 |
| DW1500 |100 |800 |1,600 |3,200 |
| DW2000 |100 |1,600 |3,200 |6,400 |
| DW3000 |100 |1,600 |3,200 |6,400 |
| DW6000 |100 |3,200 |6,400 |12,800 |

Aşağıdaki tablonun hello tooeach dağıtım DWU ve statik kaynak sınıfı tarafından ayrılmış hello bellek eşler. Hello daha yüksek kaynak sınıfları kendi belleğe sahip Not toohonor hello genel DWU sınırları azalır.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Statik kaynak sınıfları (MB) için dağıtım başına bellek ayırma
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW500 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW600 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW1000 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1200 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1500 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW2000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW3000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW6000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |12,800 |

Tablo önceki hello DW2000 hello içinde çalışan bir sorgu görebilirsiniz **xlargerc** kaynak sınıfı erişim too6, 400 MB bellek her bir hello 60 dağıtılmış veritabanı içinde sahip olabilir.  SQL veri ambarı'nda 60 dağıtımları vardır. Bu nedenle, bir sorguda belirtilen kaynak sınıfı, değerleri yukarıda hello için toocalculate hello toplam bellek ayırma 60 çarpılan.

### <a name="memory-allocations-system-wide-gb"></a>Bellek ayırma sistem genelinde (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

Bu sistem genelinde bellek ayırmaları tablodan hello xlargerc kaynak sınıfında DW2000 üzerinde çalışan bir sorgu 375 GB bellek toplam ayrılır görebilirsiniz (6.400 MB * 60 dağıtımları / 1.024 tooconvert tooGB) SQL veri ambarı hello tamamen üzerinden.

Merhaba aynı hesaplama toostatic kaynak sınıfları geçerlidir.
 
## <a name="concurrency-slot-consumption"></a>Eşzamanlılık yuvası tüketim  
SQL veri ambarını daha yüksek kaynak sınıflarda çalıştıran daha fazla bellek tooqueries verir. Bellek sabit bir kaynaktır.  Bu nedenle, daha az sayıda eşzamanlı sorgu yürütebilir hello sorgu daha fazla bellek tahsis hello. Merhaba aşağıdaki tabloda tüm DWU tarafından kullanılabilir eşzamanlılık yuvaları ve her kaynak sınıfı tarafından tüketilen hello yuvaları hello sayısını gösterir tek bir görünümde hello önceki kavramlarını reiterates.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Ayırma ve dinamik kaynak sınıfları için eşzamanlılık yuva tüketim  
| DWU | En fazla eş zamanlı sorgular | Ayrılmış eşzamanlılık yuvaları | Smallrc tarafından kullanılan yuvaları | Mediumrc tarafından kullanılan yuvaları | Largerc tarafından kullanılan yuvaları | Xlargerc tarafından kullanılan yuvaları |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Ayırma ve statik kaynak sınıfları için eşzamanlılık yuva tüketim  
| DWU | En fazla eş zamanlı sorgular | Ayrılmış eşzamanlılık yuvaları |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

Bu tablodan en fazla 32 eş zamanlı sorgular ve 40 eşzamanlılık yuvaları toplam DW1000 ayırır gibi SQL veri ambarı çalıştıran görebilirsiniz. Tüm kullanıcılar smallrc çalıştırıyorsanız, her sorgu 1 eşzamanlılık yuva kullanılmasına neden olur olduğundan 32 eş zamanlı sorguları izin. Tüm kullanıcılar bir DW1000 mediumrc içinde çalışmakta olan, her sorgu 47 GB sorgu başına bir toplam bellek ayırma için dağıtım başına 800 MB ayrılması ve eşzamanlılık sınırlı too5 kullanıcılar olacaktır (40 eşzamanlılık yuvaları / 8 yuvası mediumrc kullanıcı başına).

## <a name="selecting-proper-resource-class"></a>Doğru kaynak sınıfını seçme  
İyi bir uygulama, kendi kaynak sınıflarını değiştirmek yerine toopermanently Ata kullanıcıları tooa kaynak sınıfının olur. Örneğin, yükleri tooclustered columnstore tabloları daha fazla bellek tahsis zaman daha yüksek kaliteli dizinler oluşturun. yükleri erişim toohigher belleğe sahip, özellikle verileri yüklemek için bir kullanıcı oluşturun ve kalıcı olarak bu kullanıcı tooa daha yüksek kaynak sınıfı atamanız tooensure.
En iyi yöntemler toofollow burada birkaç vardır. Yukarıda belirtildiği gibi SQL DW iki tür kaynak sınıfı türlerini destekler: statik kaynak sınıfları ve dinamik kaynak sınıfları.
### <a name="loading-best-practices"></a>En iyi uygulamaları yükleme
1.  Merhaba beklentilerini normal veri miktarı ile yükleri varsa, statik kaynak sınıfı iyi bir seçimdir. Daha sonra tooget ölçeklendirme daha fazla hesaplama gücüne, hello veri ambarı okuyamayacak zaman toorun daha fazla eşzamanlı out-of--box, hello yük kullanıcı daha fazla bellek tüketmesine değil olarak sorgular.
2.  Merhaba beklentilerini bazı durumlar büyük yükleri varsa, dinamik kaynak sınıfı iyi bir seçimdir. Daha sonra daha fazla hesaplama gücüne tooget ölçekleme sırasında hello yük kullanıcı daha fazla bellek out-of--box, bu nedenle hello yük tooperform daha hızlı izin alır.

Merhaba ihtiyaç duyulan bellek tooprocess yüklerini verimli bir şekilde bağlıdır hello tablo yüklenen ve işlenen veri miktarı hello üzerinde hello yapısı. Örneğin, CCI tablolara veri yükleniyor bazı bellek toolet CCI rowgroups en iyi hale getirme ulaşmak gerektirir. Daha fazla ayrıntı için hello Columnstore dizinleri - veri kılavuzu yükleme bakın.

En iyi uygulama, biz toouse tutumunuzu en az 200MB bellek yükler için.

### <a name="querying-best-practices"></a>En iyi yöntemler sorgulama
Sorguları kendi karmaşıklığına bağlı olarak farklı gereksinimleri vardır. Sorgu başına bellek artırma veya hello eşzamanlılık artırmayı olan hem de geçerli yolları tooaugment hello sorgu gereksinimlerine bağlı olarak genel üretilen işi.
1.  Merhaba beklentilerini normal, karmaşık sorgular varsa (örneğin, toogenerate günlük ve haftalık raporları) ve gerek kalmaz eşzamanlılık tootake avantajı, dinamik kaynak sınıfı iyi bir seçimdir. Merhaba sistemi daha fazla veri tooprocess varsa, hello veri ambarını ölçeklendirme bu nedenle otomatik olarak hello sorgusu çalıştırarak daha fazla bellek toohello kullanıcı sağlar.
2.  Hello beklentilerini değişkeni ya da diurnal eşzamanlılık desenleri varsa (örneği için hello veritabanı web UI kapsamlı erişilebilir sorgulanan varsa), bir statik kaynak sınıf iyi bir seçimdir. Daha sonra toodata ambarı ölçeklendirme sonra hello statik kaynak sınıfıyla ilişkili hello kullanıcı otomatik olarak gerçekleşecek daha fazla eşzamanlı sorguları mümkün toorun olabilir.

Sorgunuzu hello ihtiyacına bağlı olarak seçilmesi uygun bellek ataması Önemsiz olmayan, aynıdır hello sorgulanan, veri miktarı gibi birçok faktöre hello tablo şemalarını ve çeşitli birleştirme, seçim ve Grup koşulları hello yapısına bağlıdır. Genel açısından daha fazla bellek ayırma sorguları toocomplete daha hızlı izin verir, ancak azaltmak Genel eşzamanlılık hello. Eşzamanlılık sorunu değilse, aşırı bellek ayırma zarar değil. toofine ayarlama verimlilik, kaynak sınıflarının çeşitli özellikleri çalışırken gerekli olabilir.

Depolanan hello aşağıdakileri kullanabilirsiniz yordamı toofigure verilen SLO ve hello en yakın iyi kaynak için bir sınıf bellek yoğun CCI tablosu üzerinde işlem bölümlenmemiş CCI belirtilen kaynak sınıfı, kaynak sınıfı başına eşzamanlılık ve bellek verme çıkışı:

#### <a name="description"></a>Açıklama:  
Bu saklı yordam hello amacı şöyledir:  
1. toohelp kullanıcı şekil verilen SLO kaynak sınıfı başına eşzamanlılık ve bellek verme çıkışı. Kullanıcının tooprovide NULL hem şema hem de tablename için bu hello aşağıdaki örnekte gösterildiği gibi olması gerekir.  
2. toohelp kullanıcı anlayıp hello en yakın iyi kaynak sınıfı hello bellek intensed için belirtilen kaynak sınıfı olmayan bölümlenmiş CCI tablosunda CCI işlemleri (yük, kopyalama tablo yeniden dizin, vb.). depolanan hello proc tablo şemasını toofind hello gerekli bellek ataması çıkışı bu için kullanır.

#### <a name="dependencies--restrictions"></a>Bağımlılıklar ve sınırlamalar:
- Bu saklı yordam bölümlenmiş cci tablosu için tasarlanmış toocalculate bellek gereksinimi değil.    
- Bu saklı yordam hello SELECT Ekle/CTAS-seçin kısmı için bellek gereksinimi dikkate almaz ve toobe basit bir SELECT varsayar.
- Bu saklı yordam hello oturumunda bu kullanılabilir Bu saklı yordam oluşturulduğu geçici bir tablo kullanır.    
- Bu değişiklikler, ardından bu saklı yordam düzgün çalışmayan ve bu saklı yordam hello geçerli tekliflerini (örn. donanım yapılandırması, DMS config) bağlıdır.  
- Değişiklikler, ardından bu saklı yordam düzgün çalışmayan ve bu saklı yordam varolan sunulan eşzamanlılık sınırı bağlıdır.  
- Bu saklı yordam mevcut kaynak sınıfı tekliflerini bağlıdır ve, ardından bu değişip değişmediğini proc wuold çalışmaz doğru bir şekilde depolanır.  

>  [!NOTE]  
>  Saklı yordam olabilir sonra iki durumda sağlanan parametrelerle yürüttükten sonra çıktı almıyorsanız. <br />1. Her iki DW parametresi geçersiz SLO değeri içeriyor <br />2. VEYA yoksa hiçbir eşleşen kaynak sınıfı CCI işlemi için tablo adı sağlandı. <br />Örneğin, DW100, en yüksek bellek ataması 400 MB'dir ve tablo şemasını genişse yeterli toocross 400 MB gereksinimi hello.
      
#### <a name="usage-example"></a>Kullanım örneği:
Sözdizimi:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Ya da NULL parametresi tooextract sağlamak hello DW DB gelen geçerli DWU hello veya desteklenen herhangi bir DWU 'DW100' hello biçiminde sağlayın
2. @SCHEMA_NAME:Merhaba tablonun şema adını sağlayın
3. @TABLE_NAME:Merhaba ilgi bir tablo adı sağlayın

Bu saklı yordam yürütme örnekler:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Merhaba örnekleri yukarıda kullanılan tablo1 aşağıdaki gibi oluşturulabilir:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Merhaba saklı yordamı tanımı aşağıda verilmiştir:
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Sorgu önem derecesi
SQL veri ambarı iş yükü gruplarını kullanarak kaynak sınıfları uygular. Merhaba arasında çeşitli DWU boyutları hello kaynak sınıfları hello davranışını denetleyen sekiz iş yükü grupları toplam vardır. SQL veri ambarı tüm DWU için yalnızca dört hello sekiz iş yükü gruplarını kullanır. Her iş yükü grubu tooone dört kaynak sınıfların atanmış olduğundan bu mantıklı: smallrc, mediumrc, largerc, veya xlargerc. Merhaba hello iş yükü grupları anlama önemini iş yükü gruplarının bazıları toohigher ayarlanır olan *önem*. Önem derecesi CPU için kullanılan planlama. Yüksek öncelikli olarak çalıştırılan sorguların olandan Orta önem düzeyine sahip üç kat daha fazla CPU döngülerini alırsınız. Bu nedenle, eşzamanlılık yuvası eşlemeleri CPU Öncelik belirler. Bir sorgu 16 veya daha fazla yuvaları tüketir yüksek önem olarak çalışır.

Merhaba aşağıdaki tabloda her iş yükü grubu için hello önem eşlemeler gösterilmektedir.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>İş yükü grubu eşlemeleri tooconcurrency yuvaları ve önem derecesi
| İş yükü grupları | Eşzamanlılık yuvası eşleme | MB / dağıtım | Önem derecesi eşleme |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Orta |
| SloDWGroupC01 |2 |200 |Orta |
| SloDWGroupC02 |4 |400 |Orta |
| SloDWGroupC03 |8 |800 |Orta |
| SloDWGroupC04 |16 |1,600 |Yüksek |
| SloDWGroupC05 |32 |3,200 |Yüksek |
| SloDWGroupC06 |64 |6,400 |Yüksek |
| SloDWGroupC07 |128 |12,800 |Yüksek |

Merhaba gelen **ayırma ve kullanımını eşzamanlılık yuva** grafiği, bir DW500 1, 4, 8 ya da 16 eşzamanlılık yuvası smallrc, mediumrc, largerc ve xlargerc, sırasıyla kullandığını görebilirsiniz. Bu değerleri grafik toofind hello önem her kaynak sınıfı için önceki hello bakabilirsiniz.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Kaynak sınıfları tooimportance DW500 eşleme
| Kaynak sınıfı | İş yükü grubu | Kullanılan eşzamanlılık yuvaları | MB / dağıtım | Önem derecesi |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Orta |
| mediumrc |SloDWGroupC02 |4 |400 |Orta |
| largerc |SloDWGroupC03 |8 |800 |Orta |
| xlargerc |SloDWGroupC04 |16 |1,600 |Yüksek |
| staticrc10 |SloDWGroupC00 |1 |100 |Orta |
| staticrc20 |SloDWGroupC01 |2 |200 |Orta |
| staticrc30 |SloDWGroupC02 |4 |400 |Orta |
| staticrc40 |SloDWGroupC03 |8 |800 |Orta |
| staticrc50 |SloDWGroupC03 |16 |1,600 |Yüksek |
| staticrc60 |SloDWGroupC03 |16 |1,600 |Yüksek |
| staticrc70 |SloDWGroupC03 |16 |1,600 |Yüksek |
| staticrc80 |SloDWGroupC03 |16 |1,600 |Yüksek |

DMV sorgusu toolook bellek kaynağı ayırma ayrıntılı hello farklılıkları hello kaynak İdarecisi hello açısından veya hello iş yükü grupları tooanalyze etkin ve geçmiş kullanımı sırasında sorunlarını giderirken aşağıdaki hello kullanabilirsiniz.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Eşzamanlılık sınırları dikkate sorguları
Sorguların çoğu kaynak sınıfları tarafından yönetilir. Bu sorguları hello eşzamanlı sorgu ve eşzamanlılık yuvası eşikleri sığması gerekir. Bir kullanıcı, bir sorgu hello eşzamanlılık yuvası modelden tooexclude seçemezsiniz.

tooreiterate, deyimleri Uy kaynak sınıfları aşağıdaki hello:

* INSERT SEÇİN
* GÜNCELLEŞTİRME
* SİL
* (Kullanıcı tablosu sorgulanırken) seçin
* ALTER INDEX YENİDEN OLUŞTURMA
* ALTER INDEX REORGANIZE KOMUTUNU
* ALTER TABLE YENİDEN OLUŞTURMA
* DİZİN OLUŞTURMA
* KÜMELENMİŞ COLUMNSTORE DİZİNİ OLUŞTURMA
* TABLE AS SELECT (CTAS) OLUŞTURMA
* Veri yükleme
* Veri Taşıma hizmeti (DMS) Hello tarafından gerçekleştirilen veri taşıma işlemleri

## <a name="query-exceptions-tooconcurrency-limits"></a>Sorgu özel durumları tooconcurrency sınırları
Bazı sorgular hello kaynak getirmiyor sınıfı toowhich hello kullanıcı atanır. Belirli bir komut için gereken hello bellek kaynakları genellikle Hello komutu meta veri işlemi olduğundan düşük olduğunda bu özel durumlar toohello eşzamanlılık sınırları yapılır. Merhaba bu özel durumları tooavoid büyük bellek ayırmaları hiçbir zaman bunları gerekir sorgular için hedefidir. Bu durumlarda, küçük bir kaynak sınıfı (smallrc) hello gerçek kaynak sınıfı bağımsız olarak her zaman kullanılır hello varsayılan toohello kullanıcı atanır. Örneğin, `CREATE LOGIN` smallrc içinde her zaman çalışır. Merhaba gerekli kaynakları toofulfill bu işlem çok düşük algılama tooinclude hello sorgu hello eşzamanlılık yuvası modelinde yapmaz şekilde.  Bu sorguları da hello 32 kullanıcı eşzamanlılık sınırı tarafından sınırlı değildir, bu sorguları sınırsız sayıda 1.024 oturumlarının toohello oturum sınırı çalıştırabilirsiniz.

deyimlerini aşağıdaki hello kaynak sınıfları getirmiyor:

* DROP TABLE veya oluşturma
* ALTER TABLE... ANAHTAR, bölme veya bölüm birleştirme
* ALTER INDEX DEVRE DIŞI BIRAK
* DROP INDEX
* OLUŞTURMA, güncelleştirme ya da DROP STATISTICS
* TRUNCATE TABLE
* ALTER YETKİLENDİRME
* OTURUM AÇMA OLUŞTURUN
* CREATE, ALTER veya DROP USER
* OLUŞTURMA, değiştirme veya bırakma yordamı
* OLUŞTURMA veya DROP VIEW
* DEĞER EKLEME
* Sistem görünümleri ve Dmv'leri seçin
* AÇIKLANMAKTADIR
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a>Bir kullanıcı kaynak sınıfı örneği değiştirme
1. **Oturum açma oluşturun:** bağlantı tooyour açmak **ana** veritabanı hello SQL Server'da, SQL veri ambarı veritabanını barındıran ve hello aşağıdaki komutları yürütün.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Merhaba ana veritabanını Azure SQL Data Warehouse kullanıcılar için iyi bir fikir toocreate bir kullanıcı olarak. Master kullanıcı oluşturma, bir veritabanı adı belirtmeden SSMS gibi araçları kullanarak bir kullanıcı toologin sağlar.  Ayrıca bunları toouse hello Nesne Gezgini tooview tüm veritabanları SQL server üzerinde sağlar.  Oluşturma ve kullanıcıları yönetme hakkında daha fazla ayrıntı için bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **SQL veri ambarı kullanıcı oluşturun:** bağlantı toohello açmak **SQL Data Warehouse** veritabanı ve hello aşağıdaki komutu yürütün.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **İzinleri verin:** hello örnek verir `CONTROL` hello üzerinde **SQL Data Warehouse** veritabanı. `CONTROL`Merhaba veritabanı düzeyi olduğu hello SQL Server'daki db_owner eşdeğeridir.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Kaynak sınıfı artırmak:** kullanım hello aşağıdaki sorgu tooadd kullanıcı tooa daha yüksek iş yükü yönetim rolü.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Kaynak sınıfı azaltın:** kullanım hello aşağıdaki sorgu tooremove bir kullanıcıdan bir iş yükü yönetim rolü.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Olası tooremove smallrc bir kullanıcı değil.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Sıraya alınan sorgu algılama ve diğer Dmv'leri
Merhaba kullanabilirsiniz `sys.dm_pdw_exec_requests` bir eşzamanlılık sırada bekleyen DMV tooidentify sorgular. Sorgular bir eşzamanlılık yuva durumu için bekleyen **askıya**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

İş yükü yönetim rolleri ile görüntülenebilir `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

Sorgu aşağıdaki hello her kullanıcının atandığı rolü gösterir.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL veri ambarı türleri bekleyin hello aşağıdakileri içerir:

* **LocalQueriesConcurrencyResourceType**: hello eşzamanlılık yuvası framework dışında sit sorgular. DMV sorgular ve sistem işlevleri gibi `SELECT @@VERSION` yerel sorgular gösterilebilir.
* **UserConcurrencyResourceType**: hello eşzamanlılık yuvası framework içinde sit sorgular. Son kullanıcı tabloları sorguları bu kaynak türü kullanırsınız örnekleri temsil eder.
* **DmsConcurrencyResourceType**: veri taşıma işlemleri kaynaklanan bekler.
* **BackupConcurrencyResourceType**: Bu bekleme bir veritabanı yedekleniyor olduğunu gösterir. Bu kaynak türü için Hello en büyük değer 1'dir. Birden çok yedekleme sırasında hello istenmiş, aynı zamanda, diğerleri sıraya hello.

Merhaba `sys.dm_pdw_waits` DMV kullanılan toosee hangi kaynakların bir isteği bekliyor olabilir.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Merhaba `sys.dm_pdw_resource_waits` DMV belirli bir sorgu tarafından tüketilen hello kaynak bekler gösterir. Kaynak bekleme süresi yalnızca sağlanan kaynakları toobe için bekleyen hello süreyi ölçer. Bu, karşılıklı toosignal bekleyin gibi hello zamanı zaman SQL sunucuları tooschedule hello hello CPU üzerine sorguyla hello için alır.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Merhaba `sys.dm_pdw_wait_stats` DMV bekler geçmiş eğilim analizi için kullanılabilir.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Sonraki adımlar
Veritabanı kullanıcıları yönetme ve güvenlik hakkında daha fazla bilgi için bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse]. Ne kadar büyük kaynak sınıfları hakkında daha fazla bilgi kümelenmiş columnstore dizini kalitesini artırmak, bkz [dizinleri tooimprove segment kalite yeniden].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[dizinleri tooimprove segment kalite yeniden]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
