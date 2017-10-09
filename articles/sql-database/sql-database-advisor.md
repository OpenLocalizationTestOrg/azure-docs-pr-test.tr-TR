---
title: "aaaPerformance önerileri - Azure SQL veritabanı | Microsoft Docs"
description: "Hello Azure SQL veritabanı geçerli sorgu performansını artırmak, SQL veritabanları için öneriler sağlar."
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
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Performans önerileri

Azure SQL veritabanı öğrenir ve uygulamanız ile uyum ve toomaximize hello performans SQL veritabanlarınızın etkinleştirme özelleştirilmiş öneriler sağlar. Performansınızı SQL veritabanı kullanım geçmişiniz çözümleyerek sürekli olarak değerlendirildiği. sağlanan hello öneriler, bir veritabanı benzersiz iş yükü deseni temel alınarak ve performansını artırmaya yardımcı.

> [!NOTE]
> Önerileri kullanarak önerilen veritabanınızda 'Otomatik ayarı' seçeneğini etkinleştirerek yoludur. Ayrıntılar için bkz [otomatik ayarlama](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Dizin önerileri oluşturma
Azure SQL veritabanı sürekli olarak yürütülen hello sorguları izler ve hello performansını artırmak hello dizinleri tanımlar. Yeterli güvenirlik derlendikten sonra belirli bir dizin eksik, yeni bir **Create Index** öneri oluşturulur. Azure SQL veritabanı derlemeleri güvenirlik performans kazancı hello dizin hesaplaması tamamlanışında sunacağı. Tahmini hello performans kazancı bağlı olarak öneriler yüksek, Orta veya düşük kategorilere ayrılır. 

Önerileri kullanarak oluşturulan dizinleri her zaman auto_created dizinler işaretlenir. Hangi dizinleri auto_created sys.indexes Sergi bakarak görebilirsiniz. Otomatik olarak oluşturulan dizinleri ALTER/yeniden adlandırma komutları engelleme. Bir otomatik olarak dizin üzerinde oluşturulan sahip toodrop hello sütun çalışırsanız, hello komutu gönderir ve hello otomatik olarak dizini oluşturulan de hello komutuyla bırakılır. Normal dizin hello ALTER/RENAME komutu dizini sütunlarda engellenebilir.

Merhaba oluşturduktan sonra dizin önerisi uygulanır, Azure SQL veritabanı hello sorguların performansını hello taban çizgisi performansı ile karşılaştırır. Yeni dizin hello performans geliştirmeleri geldiyseniz öneri başarılı olarak işaretlenir ve etkisi raporu kullanılabilir olacaktır. Merhaba dizini hello avantajları getirmek kaydetmedi durumda otomatik olarak döndürülecek. Önerileri kullanarak yalnızca hello veritabanı performansını artırır, böylece Azure SQL veritabanı sağlar.

Tüm **Create Index** önerisi bir geri alma hello veritabanı veya havuz DTU kullanımı son 20 dakika veya hello depolama kullanımı % 90 olup olmadığını % 80 ise hello öneri uygulama izin vermiyor İlkesi yok. Bu durumda, hello öneri Ertelenen.

## <a name="drop-index-recommendations"></a>Dizin kaldırma önerileri
Ayrıca toodetecting eksik bir dizin, Azure SQL veritabanı sürekli varolan dizinleri hello performansını analiz eder. Dizin kullanılmazsa, Azure SQL veritabanı bırakmadan öneririz. Bir dizini bırakmadan iki durumda da önerilir:
* Dizin (aynı dizine ve sütun, bölüm şeması ve filtreleri dahil) başka bir dizin yinelemesi
* Dizin uzun süren bir süre (93 gün) için kullanılmaz

Dizin kaldırma önerileri de hello doğrulamadan sonra uygulama geçer. Merhaba performans artarsa hello etkisi raporu kullanılabilir. Bir performans düşüşü algılanırsa durumda öneri geri alınacak.


## <a name="parameterize-queries-recommendations"></a>Sorguları önerileri Parametreleştirme
**Sorguları Parametreleştirme** önerileri varsa veya sürekli olarak derlenir ancak şunun daha fazla sorguları hello aynı sorgu yürütme planı yaptığınızda görünmez. Bu durum toobe önbelleğe alınmış ve performansı artırır ve kaynak kullanımını azaltarak gelecekteki hello yeniden sorgu planlarını sağlayacak parameterızatıon forced bir fırsat tooapply yukarı açar. 

SQL Server karşı başlangıçta verilen her sorgu yürütme planı derlenmiş toobe toogenerate gerekir. Oluşturulan her plan toohello plan önbelleğinin ve sonraki yürütmelerde eklenir hello ek derleme hello gereksinimini hello önbelleğinden Bu planın aynı sorgu yeniden kullanabilirsiniz. 

Parametreli olmayan değerler, sorguları göndermek uygulamalar, burada her tür sorguda farklı parametre değerleri ile Merhaba yürütme planı yeniden derlenir tooa performansa neden olabilir. Birçok durumda hello farklı parametre değerlerini oluşturmak aynı sorgularıyla aynı yürütme planları Merhaba, ancak bu planlarını toohello plan önbelleğinin hala ayrı olarak eklenir. Yeniden derlenmesi yürütme planları veritabanı kaynaklarını kullanmak için önbellek neden hello önbellekten çıkarılmasına toobe planları hello sorgu süresi saat ve taşma hello planı artırın. SQL Server'ın bu davranış parametrelemeyi seçeneği hello veritabanında zorunlu hello ayarlayarak değiştirilebilir. 

(Merhaba öneri gibi uygulandıysa) hello gerçek CPU arasında bir karşılaştırma ile kullanım ve hello CPU kullanımı öngörülen toohelp, bu öneri hello etkisini tahmin, sağlanır. Ayrıca tooCPU tasarruf derlemede hello zamanın için sorgu süresini azaltır. Ayrıca olacaktır daha az ek yükü plan önbelleğinin, hello çoğunluğu vererek toostay önbelleğinde planları ve yeniden kullanılabilir. Merhaba üzerinde tıklatarak hızlı ve kolay bir şekilde Bu öneri uygulayabilirsiniz **Uygula** komutu. 

Bu öneriyi uyguladığınızda, yaklaşık 24 saat boyunca sürer işlem izleme hello başlatır ve veritabanı yükünüzü dakika içinde zorlanmış parametrelemeyi olanağı sağlar. Bu süre, 24 saat önce veritabanınızı CPU kullanımını gösteren mümkün toosee hello doğrulama raporunu olması ve hello öneri uygulandıktan sonra olur. SQL veritabanı Danışmanı performans regresyon algılandı, otomatik olarak uygulanan hello öneri döner bir güvenlik mekanizması vardır.

## <a name="fix-schema-issues-recommendations"></a>Şema sorunları önerileri Düzelt
**Şema sorunları giderin** önerileri hello tıklattığınızda görünür SQL veritabanı hizmetinin bildirimler bir anomali şema ile ilgili SQL hataları Azure SQL veritabanınızda gerçekleştiği hello sayısı. Bu öneri, genellikle veritabanınızı bir saat içinde birden çok şema ile ilgili hataları (geçersiz sütun adı, geçersiz nesne adı, vb.) karşılaştığında görüntülenir.

"Şema" Merhaba tanımı hello SQL sorgusunun ve hello tanımının hello veritabanı şemasının hizalanmadıysa zaman meydana söz dizimi hataları SQL Server'daki sınıfının sorunlardır. Örneğin, hello sorgu tarafından beklenen hello sütunlardan biri eksik olabilir hello hedef tabloda veya tersi. 

Azure SQL veritabanı hizmetinin Azure SQL veritabanınızda gerçekleştiği şema ile ilgili SQL hataları hello sayısı cinsinden bir anomali bildirimler "şema sorunu düzeltin" öneri görünür. Merhaba, aşağıdaki ilgili tooschema sorunlardır tablo gösterir hello hatalar:

| SQL hata kodu | İleti |
| --- | --- |
| 201 |Yordamı veya işlevi '*'parametresini beklemektedir'*', hangi değil sağlandı. |
| 207 |Geçersiz sütun adı ' *'. |
| 208 |Geçersiz nesne adı ' *'. |
| 213 |Sütun adı veya numarası sağlanan değerlerin tablo tanımı eşleşmiyor. |
| 2812 |Saklı yordamı bulunamadı. ' *'. |
| 8144 |Yordam veya işlev * belirtilen çok fazla bağımsız değişkenlere sahiptir. |

## <a name="next-steps"></a>Sonraki adımlar
Önerilerinizi izlemek ve tooapply devam bunları toorefine performans. Veritabanı iş yüklerini, dinamik ve sürekli olarak değiştirin. SQL veritabanı Danışmanı'nı toomonitor devam eder ve veritabanınızın performansı artırmak öneriler sağlar. 

* Bkz: [hello Azure portal performans önerileri](sql-database-advisor-portal.md) nasıl toouse performans önerileri Azure portal hello adımlar için.
* Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) toolearn hakkında ve görünüm hello üst sorgularınızı performans etkisini.

## <a name="additional-resources"></a>Ek kaynaklar
* [Sorgu deposu](https://msdn.microsoft.com/library/dn817826.aspx)
* [DİZİN OLUŞTURMA](https://msdn.microsoft.com/library/ms188783.aspx)
* [Rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md)

