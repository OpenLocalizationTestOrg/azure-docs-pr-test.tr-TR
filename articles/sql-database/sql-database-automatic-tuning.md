---
title: "SQL veritabanı - otomatik ayarlama | Microsoft Docs"
description: "SQL veritabanı SQL sorgusu analiz eder ve automaticaly kullanıcı iş yüküne uyum sağlar."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: f5552793db2d89542782b7d9e8f996314f62e429
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automatic-tuning"></a>Otomatik ayarlama

Azure SQL veritabanı veritabanı üzerinde yürütülür ve otomatik olarak iş yükü performansını artırabilir sorguları izleyen bir tam olarak yönetilen veri hizmetidir. Azure SQL veritabanı otomatik olarak ayarlamak ve dinamik olarak İş yükünüzün veritabanına uyarlama tarafından sorgularınızı performansını bir yerleşik zekaya mekanizması vardır. Azure SQL veritabanı'nda otomatik ayarlama, Azure SQL veritabanındaki sorgu performansını iyileştirmek için etkinleştirebilirsiniz en önemli özelliklerden biri olabilir.

Bu makalede adımları için bkz: [otomatik ayarlamayı etkinleştirmek](sql-database-automatic-tuning-enable.md) Azure portalını kullanarak.

## <a name="why-automatic-tuning"></a>Neden otomatik ayarlama?

Klasik veritabanı yönetim'deki ana görevlerden birini kritik SQL sorguları, performansı artırmak için eklenmelidir dizinler ve nadiren kullanılan dizinleri tanımlayan iş yükü izlemektedir. Azure SQL veritabanı sorguları ve izlemek için gereken dizinleri ayrıntılı bir anlayış sağlar. Ancak özellikle birden fazla veritabanıyla ilgilenirken bir veritabanını sürekli izlemek zor ve yorucu bir görevdir. Veritabanları büyük sayıda yönetme verimli bir şekilde bile tüm kullanılabilir araçları ve Azure SQL Database ve Azure portal sağlayan raporları yapmak mümkün olabilir. İzleme ve veritabanınızı el ile ayarlama yerine otomatik ayarlama özelliğini kullanarak, Azure SQL veritabanına izleme ve ayarlama eylemlerin bazıları için temsilci seçme düşünebilirsiniz. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Nasıl yapılır otomatik ayarlama iş?

Azure SQL veritabanı sürekli yükünüzü karakteristiğini hakkında öğrenir ve olası sorunları ve geliştirmeleri belirlemek bir sürekli performans izleme ve çözümleme işlemi vardır.

![Otomatik ayarlama işlemi](./media/sql-database-automatic-tuning/tuning-process.png)

Bu işlem, iş yükü için hangi dizinler ve planları, iş yüklerinin performansının artırılmasına ve iş yüklerinizi hangi dizinleri etkileyen bulma tarafından dinamik olarak uyarlamak Azure SQL veritabanı sağlar. Bu bulgularını üzerinde bağlı olarak, otomatik ayarlama, İş yükünüzün performansını ayarlama eylemlerine uygulanır. Ayrıca, Azure SQL Database, performans, İş yükünüzün performansını artırır emin olmak için otomatik ayarlama tarafından yapılan herhangi bir değişiklik sonra kesintisiz olarak izler. Performansı kaydetmedi herhangi bir eylem otomatik olarak geri döndürüldü. Bu doğrulama işlemi, otomatik ayarlama tarafından yapılan herhangi bir değişiklik, İş yükünüzün performansını azaltamazsınız sağlar anahtar bir özelliktir.

Azure SQL veritabanı'nda kullanılabilir olan iki otomatik ayarlama yönleri şunlardır:

 -  **Otomatik dizin yönetimi** veritabanınızda eklenmelidir dizinler ve kaldırılmalıdır dizinleri tanımlar.
 -  **Otomatik planı düzeltme** (, yakında zaten bulunan SQL Server 2017) sorunlu planları tanımlar ve düzeltmeleri SQL performans sorunlarını planlayın.

## <a name="automatic-index-management"></a>Otomatik dizin yönetimi

Azure SQL veritabanı'nda Azure SQL veritabanı yükünüzü hakkında öğrenir ve verilerinizin her zaman en uygun şekilde dizine sağlar çünkü dizin yönetimi kolaydır. Uygun dizin tasarımı, iş yükü en iyi performans için çok önemlidir ve otomatik dizin yönetimi dizinlerinizi en iyi hale getirmenize yardımcı olabilir. Otomatik dizin yönetimi ya da hatalı oluşturulmuş veritabanlarında, performans sorunlarını çözün veya korumak ve var olan veritabanı şeması dizinlerinde artırmak. 

### <a name="why-do-you-need-index-management"></a>Dizin Yönetimi neden gerekiyor?

Dizinleri, bazı tablolarından veri okuma sorgularınızı hızlandırmak; Ancak, verileri güncelleştiren sorguları yavaşlatabilir. Dizin oluşturmak ne zaman ve hangi sütunların dikkatle analiz etmeniz dizinde eklemeniz gerekir. Bazı dizinleri bir süre sonra gerekli değildir. Bu nedenle, düzenli aralıklarla tanımlamak ve tüm avantajları Getir değil dizinleri bırak gerekir. Kullanılmayan dizinleri yoksayarsanız, verileri güncelleştirmek sorguların performansını veri okuma sorgularını bir fayda olmaksızın azaltılabilir. Ek güncelleştirmeler gereksiz günlük gerektirdiğinden kullanılmayan dizinleri da sistemin genel performansı etkiler.

En iyi kümesini, tablolarından veri okumak ve güncelleştirmeleri en az etkisi olan sorguları performansını dizinleri bulma sürekli ve karmaşık analiz gerektirebilir.

Azure SQL veritabanı yerleşik zekaya ve sorgularınızı çözümlemek, geçerli iş yükleri için en uygun olacak dizinleri tanımlamak Gelişmiş kurallar kullanır ve dizinler kaldırılabilir. Azure SQL veritabanı verileriyle diğer sorgular simge durumuna küçültülmüş etkisini okuma sorguları en iyi duruma getirme dizinleri gerekli en az sayıda sahip olmasını sağlar.

### <a name="how-to-identify-indexes-that-need-to-be-changed-in-your-database"></a>Veritabanınızda değiştirilmesi gereken dizinleri tanımlamak nasıl?

Azure SQL veritabanı dizin yönetimi işlemini kolaylaştırır. Azure SQL veritabanı yükünüzü çözümler can sıkıcı işlemi el ile iş yükü analiz ve dizin izleme yerine yeni bir dizin ile daha hızlı yürütülebilir sorguları tanımlar ve kullanılmayan veya yinelenen dizinleri tanımlar. Konumundaki değiştirilmelidir dizinleri tanımlaması hakkında daha fazla bilgi bulmak [dizin önerileri Azure Portalı'nda bulmak](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Otomatik dizin yönetimi konuları

Yerleşik kurallar veritabanınızın performansını artırmak bulursanız, Azure SQL veritabanını otomatik olarak dizinlerinizi Yönet sağlayabilir.

Azure SQL veritabanlarında gerekli dizinler oluşturmak için gerekli eylemleri kaynaklarını tüketebilir ve geçici olarak iş yükü performansını etkiler. Dizin oluşturma iş yükü performansı üzerindeki etkisini en aza indirmek için Azure SQL veritabanı için herhangi bir dizin yönetimi işlem uygun zaman penceresini bulur. Eylem ayarlama veritabanının yükünüzü yürütmek için kaynakları gerekiyorsa Ertelenen ve veritabanının yeterli olduğunda başlatılan bakım görevini kullanılabilmesi için kullanılmayan kaynaklar. Otomatik Dizin Yönetimi'nde bir önemli özellik eylemlerin bir onaydır. Azure SQL veritabanı oluşturur veya dizin bırakır, izleme işlemi eylemi performansı geliştirildi doğrulamak için İş yükünüzün performansını analiz eder. Önemli iyileştirme – Getir alamadık, eylem hemen geri döndürüldü. Bu şekilde, otomatik Eylemler, İş yükünüzün performansını olumsuz etkilemez Azure SQL veritabanı sağlar. Otomatik ayarlama tarafından oluşturulan dizinleri, temel alınan şema bakım işlemi için saydamdır. Şema değişiklikleri bırakmayı veya sütunları yeniden adlandırma gibi otomatik olarak oluşturulan dizinleri varlığını tarafından engellenmez. Azure SQL veritabanı tarafından otomatik olarak oluşturulan dizinleri hemen bırakılır ne zaman ilgili tablo veya sütun bırakıldı.

## <a name="automatic-plan-choice-correction"></a>Otomatik planı seçim düzeltme

Otomatik planı düzeltme SQL Server 2017 CTP2.0 içinde işlemiyorsa SQL planları tanımlayan eklenen yeni bir otomatik ayarlama özelliğidir. Bu otomatik ayarlama seçeneğini, Azure SQL veritabanı yakında çıkıyor. Daha fazla bilgi bulmak [otomatik SQL Server 2017 ayarlama](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Sonraki adımlar

- Azure SQL veritabanı'nda otomatik olarak ayarlamayı etkinleştirmek ve işleminizi iş yükü tam olarak yönetmek otomatik ayarlama özelliği sağlar için bkz: [otomatik ayarlamayı etkinleştirmek](sql-database-automatic-tuning-enable.md).
- El ile ayarlamayı kullanacak şekilde gözden geçirebilirsiniz [önerileri Azure portalında ayarlama](sql-database-advisor-portal.md) ve el ile sorgularınızı performansını olanları uygulayın.
