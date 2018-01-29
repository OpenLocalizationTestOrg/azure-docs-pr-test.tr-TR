---
title: "Performans önerileri - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanı geçerli sorgu performansını artırmak, SQL veritabanları için öneriler sağlar."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: On Demand
ms.date: 09/20/2017
ms.author: sstein
ms.openlocfilehash: ea1069d4ec29ad66562a6798a8b13998d0d2ef89
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="performance-recommendations"></a>Performans önerileri

Azure SQL veritabanı öğrenir ve uygulamanız ile uyum ve SQL veritabanlarının performansını en üst düzeye çıkarmak için özelleştirilmiş önerileri olanak sağlar. Performansınızı SQL veritabanı kullanım geçmişiniz çözümleyerek sürekli olarak değerlendirildiği. Sağlanan öneriler, bir veritabanı benzersiz iş yükü deseni temel alınarak ve kendi performansını iyileştirmeye yardımcı olmak.

> [!TIP]
> [Otomatik ayarlama](sql-database-automatic-tuning.md) performans ayarlama, önerilen yoludur. [Akıllı Öngörüler](sql-database-intelligent-insights.md) performans izleme önerilen yoludur. 
>

## <a name="create-index-recommendations"></a>Dizin önerileri oluşturma
Azure SQL veritabanı sürekli olarak yürütülmekte olan sorguları izler ve performansının artırılmasına dizinleri tanımlar. Yeterli güvenirlik derlendikten sonra belirli bir dizin eksik, yeni bir **Create Index** öneri oluşturulur. Azure SQL veritabanı performans kazancı dizini tamamlanışında sunacağı tahminlerle güven oluşturur. Tahmini performans kazancını bağlı olarak öneriler yüksek, Orta veya düşük kategorilere ayrılır. 

Önerileri kullanarak oluşturulan dizinleri her zaman auto_created dizinler işaretlenir. Hangi dizinleri auto_created sys.indexes Sergi bakarak görebilirsiniz. Otomatik olarak oluşturulan dizinleri ALTER/yeniden adlandırma komutları engelleme. Bir otomatik olarak dizin üzerinde oluşturulan sahip sütun bırakma çalışırsanız, komut gönderir ve otomatik olarak dizini oluşturulan komutuyla bırakılır. Normal dizin dizini sütunlar üzerinde ALTER/RENAME komutu engellenebilir.

Create Index öneri uygulandıktan sonra Azure SQL Database sorguları performans taban çizgisi performansı ile karşılaştırın. Yeni dizin performans geliştirmeleri geldiyseniz öneri başarılı olarak işaretlenir ve etkisi raporu kullanılabilir olacaktır. Dizini avantajları getirmek kaydetmedi durumda otomatik olarak döndürülecek. Önerileri kullanarak yalnızca veritabanı performansını artırır, böylece Azure SQL veritabanı sağlar.

Tüm **Create Index** önerisi bir geri alma havuzu veya veritabanı kaynak kullanımı yüksekse, öneri uygulama izin vermiyor İlkesi yok. Geri alma İlkesi, hesap CPU, veri g/ç, günlük GÇ ve kullanılabilir depolama alanı alır. CPU, veri g/ç veya günlük GÇ son 30 dakika içinde % 80 oluşturmak yerine daha yüksek olduğunda dizin ertelendi. Dizin oluşturulduktan sonra kullanılabilir depolama alanı % 10 olacaksa öneri hata durumuna geçer. İşlem, birkaç gün sonra otomatik hala ayarlama o dizini yararlı olacaktır inanırsa yeniden başlatılacak. Bu işlem, dizin oluşturmak için yeterli kullanılabilir depolama alanı veya dizin olarak yararlı artık görülmez kadar yinelenir.

## <a name="drop-index-recommendations"></a>Dizin kaldırma önerileri
Eksik bir dizin algılama yanı sıra, Azure SQL veritabanı sürekli varolan dizinleri performansını analiz eder. Dizin kullanılmazsa, Azure SQL veritabanı bırakmadan öneririz. Bir dizini bırakmadan iki durumda da önerilir:
* Dizin (aynı dizine ve sütun, bölüm şeması ve filtreleri dahil) başka bir dizin yinelemesi
* Dizin uzun süren bir süre (93 gün) için kullanılmaz

Dizin kaldırma önerileri de uygulama sonra doğrulama geçer. Performans artarsa etkisi raporu kullanılabilir. Bir performans düşüşü algılanırsa durumda öneri geri alınacak.


## <a name="parameterize-queries-recommendations"></a>Sorguları önerileri Parametreleştirme
**Sorguları Parametreleştirme** önerileri sürekli son yukarı ile aynı sorgu yürütme planı derlenir bir veya daha fazla sorgular varsa görünür. Bu durum, önbelleğe alınmış ve gelecekteki performansı artırma ve kaynak kullanımını azaltarak yeniden sorgu planlarını sağlayacak zorlanmış parametrelemeyi uygulamak için bir fırsat yukarı açar. 

SQL Server karşı başlangıçta verilen her sorgu yürütme planı oluşturmak için derlenmesi gerekiyor. Oluşturulan her plan planı önbelleğe eklenir ve ek derleme gereksinimini önbelleğinden Bu planın aynı sorgu sonraki yürütmelerde yeniden kullanabilirsiniz. 

Parametreli olmayan değerler, sorguları göndermek uygulamalar, nerede farklı parametre değerleri ile gibi her bir sorgu için yürütme planı yeniden derlenir performans yükü için yol açabilir. Çoğu durumda aynı sorguları farklı parametresiyle aynı yürütme planları değerlerini oluşturmak, ancak bu planlar plan önbelleğinin hala ayrı olarak eklenir. Yeniden derlenmesi yürütme planları veritabanı kaynaklarını kullanmak için sorgu süresini artırmak ve planları önbellekten çıkarılmasına neden plan önbelleğinin taşması. Bu davranış, SQL Server veritabanı zorlanmış parametrelemeyi seçeneğini ayarlayarak değiştirilebilir. 

(Öneri gibi uygulandıysa) Bu öneri etkisini tahmin etmenize yardımcı olmak için gerçek CPU kullanımı ve tahmini CPU kullanımı arasında bir karşılaştırma sağlanır. CPU tasarrufu ek olarak, sorgu süresi derlemede harcanan süre için azaltır. Ayrıca olacaktır daha az ek yükü plan önbelleğinde önbelleğinde kalır ve yeniden kullanılabilir planları çoğunluğu izin verme. Tıklayarak hızla ve kolayca Bu öneri uygulayabilirsiniz **Uygula** komutu. 

Bu öneriyi uyguladığınızda, yaklaşık 24 saat boyunca sürer izleme işlemi başlatır ve veritabanı yükünüzü dakika içinde zorlanmış parametrelemeyi olanağı sağlar. Bu süre, 24 saat önce ve öneri uygulandıktan sonra veritabanınız CPU kullanımını gösteren doğrulama raporunu görmeye olacaktır. SQL veritabanı Danışmanı performans regresyon algılandı, otomatik olarak uygulanan öneri döner bir güvenlik mekanizması vardır.

## <a name="fix-schema-issues-recommendations-preview"></a>Şema sorunları önerileri (Önizleme) Düzelt

> [!IMPORTANT]
> Microsoft, "şema sorunu düzeltin" önerileri onaysız kılınmadan sürecinde ' dir. Kullanarak başlamalıdır [akıllı Öngörüler](sql-database-intelligent-insights.md) otomatik, veritabanı performans sorunları izlemek için aşağıdakileri içeren daha önce "şema sorunu düzeltin" öneriler ele şema sorunları.
> 

**Şema sorunları giderin** önerileri SQL veritabanı hizmetinin Azure SQL veritabanınızda gerçekleştiği şema ile ilgili SQL hataları sayısındaki bir anomali bildirimler olduğunda görüntülenir. Bu öneri, genellikle veritabanınızı bir saat içinde birden çok şema ile ilgili hataları (geçersiz sütun adı, geçersiz nesne adı, vb.) karşılaştığında görüntülenir.

"Şema" SQL Sorgu tanımını ve veritabanı şeması tanımı hizalanmadıysa zaman meydana söz dizimi hataları SQL Server'daki sınıfının sorunlardır. Örneğin, bir sorgu tarafından beklenen sütun eksik olabilir hedef tablodaki veya tersi. 

Azure SQL veritabanı hizmetinin Azure SQL veritabanınızda gerçekleştiği şema ile ilgili SQL hataları sayısındaki bir anomali bildirimler "şema sorunu düzeltin" öneri görünür. Aşağıdaki tabloda şema sorunlarıyla ilgili hataları gösterilmektedir:

| SQL hata kodu | İleti |
| --- | --- |
| 201 |Yordamı veya işlevi '*'parametresini beklemektedir'*', hangi değil sağlandı. |
| 207 |Geçersiz sütun adı ' *'. |
| 208 |Geçersiz nesne adı ' *'. |
| 213 |Sütun adı veya numarası sağlanan değerlerin tablo tanımı eşleşmiyor. |
| 2812 |Saklı yordamı bulunamadı. ' *'. |
| 8144 |Yordam veya işlev * belirtilen çok fazla bağımsız değişkenlere sahiptir. |

## <a name="next-steps"></a>Sonraki adımlar
Önerilerinizi izleyebilir ve bunları performansı iyileştirmek için uygulanmaya devam eder. Veritabanı iş yüklerini, dinamik ve sürekli olarak değiştirin. SQL veritabanı Danışmanı izlemek ve veritabanınızın performansı artırmak öneriler sunmak devam eder. 

* Bkz: [Azure SQL veritabanı otomatik ayarlama](sql-database-automatic-tuning.md) veritabanı dizinleri ve sorgu yürütme planları otomatik ayarlama.
* Bkz: [Azure SQL akıllı Öngörüler](sql-database-intelligent-insights.md) otomatik olarak otomatik tanılama ve kök ile veritabanı performansını izleme için performans sorunlarını analizini neden.
* Bkz: [performans önerileri Azure portalında](sql-database-advisor-portal.md) performans önerileri Azure portalında kullanma adımları için.
* Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) hakkında bilgi edinin ve üst sorgularınızı performans etkisini görüntülemek için.


