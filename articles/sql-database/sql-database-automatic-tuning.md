---
title: "aaaSQL veritabanı - otomatik ayarlama | Microsoft Docs"
description: "SQL veritabanı SQL sorgusu analiz eder ve automaticaly toouser iş yüküne uyum sağlar."
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
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Otomatik ayarlama

Azure SQL veritabanı hello veritabanı üzerinde yürütülür ve otomatik olarak hello iş yükü performansını artırabilir hello sorguları izleyen bir tam olarak yönetilen veri hizmetidir. Azure SQL veritabanı otomatik olarak ayarlamak ve dinamik olarak hello veritabanı tooyour iş yükü uyarlama tarafından sorgularınızı performansını bir yerleşik zekaya mekanizması vardır. Azure SQL veritabanı'nda otomatik ayarlama, Azure SQL veritabanı toooptimize performansı sorgularınızı üzerinde etkinleştirebilirsiniz hello en önemli özelliklerden biri olabilir.

Merhaba adımları için bu makalenin çok bkz[otomatik ayarlamayı etkinleştirmek](sql-database-automatic-tuning-enable.md) hello Azure portal kullanarak.

## <a name="why-automatic-tuning"></a>Neden otomatik ayarlama?

Klasik veritabanı yönetim hello ana görevlerden birini hello iş yükü izleme kritik SQL tanımlayan sorgular, tooimprove performans eklenmelidir ve dizinler'nadiren kullanılan dizinleri. Azure SQL veritabanı toomonitor gerektiğini ayrıntılı bir anlayış hello sorgular ve dizinleri sağlar. Ancak özellikle birden fazla veritabanıyla ilgilenirken bir veritabanını sürekli izlemek zor ve yorucu bir görevdir. Veritabanları büyük sayıda yönetme bile tüm kullanılabilir araçları ve Azure SQL Database ve Azure portal sağlayan raporları verimli bir şekilde imkansız toodo olabilir. İzleme ve veritabanınızı el ile ayarlama yerine, izleme ve eylemleri tooAzure SQL veritabanı ayarlama hello bazıları için temsilci seçme düşünebilirsiniz otomatik ayarlama özelliğini kullanarak. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Nasıl yapılır otomatik ayarlama iş?

Azure SQL veritabanı sürekli hello hakkında iş yükünü özellik öğrenir ve olası sorunları ve geliştirmeleri belirlemek bir sürekli performans izleme ve çözümleme işlemi vardır.

![Otomatik ayarlama işlemi](./media/sql-database-automatic-tuning/tuning-process.png)

Azure SQL veritabanı toodynamically hangi dizinler ve planları, iş yüklerinin performansının artırılmasına ve hangi dizine bularak tooyour iş yükü uyum bu işlem etkinleştirir, iş yüklerini etkiler. Bu bulgularını üzerinde bağlı olarak, otomatik ayarlama, İş yükünüzün performansını ayarlama eylemlerine uygulanır. Ayrıca, Azure SQL Database, performans, İş yükünüzün performansını artırır otomatik ayarlama tooensure tarafından yapılan herhangi bir değişiklik sonra kesintisiz olarak izler. Performansı kaydetmedi herhangi bir eylem otomatik olarak geri döndürüldü. Bu doğrulama işlemi, otomatik ayarlama tarafından yapılan herhangi bir değişiklik, İş yükünüzün performansını hello azaltamazsınız sağlar anahtar bir özelliktir.

Azure SQL veritabanı'nda kullanılabilir olan iki otomatik ayarlama yönleri şunlardır:

 -  **Otomatik dizin yönetimi** veritabanınızda eklenmelidir dizinler ve kaldırılmalıdır dizinleri tanımlar.
 -  **Otomatik planı düzeltme** (, yakında zaten bulunan SQL Server 2017) sorunlu planları tanımlar ve düzeltmeleri SQL performans sorunlarını planlayın.

## <a name="automatic-index-management"></a>Otomatik dizin yönetimi

Azure SQL veritabanı'nda Azure SQL veritabanı yükünüzü hakkında öğrenir ve verilerinizin her zaman en uygun şekilde dizine sağlar çünkü dizin yönetimi kolaydır. Uygun dizin tasarımı, iş yükü en iyi performans için çok önemlidir ve otomatik dizin yönetimi dizinlerinizi en iyi hale getirmenize yardımcı olabilir. Otomatik dizin yönetimi ya da hatalı oluşturulmuş veritabanlarında, performans sorunlarını gidermek veya korumak ve hello varolan veritabanı şeması dizinlerinde artırmak. 

### <a name="why-do-you-need-index-management"></a>Dizin Yönetimi neden gerekiyor?

Dizinleri, bazı hello tablolarından veri okuma sorgularınızı hızlandırmak; Ancak, verileri güncelleştiren hello sorguları yavaşlatabilir. Toocarefully gerek toocreate dizin ve hangi sütunların içinde tooinclude gereken dizin hello çözümlemek. Bazı dizinleri bir süre sonra gerekli değildir. Bu nedenle tooperiodically gerekir tanımlamak ve tüm avantajları Getir değil hello dizinleri bırakın. Yoksayarsanız kullanılmayan dizinleri Merhaba, verileri güncelleştirmek hello sorguların performansını veri okuma hello sorgularını bir fayda olmaksızın düşürülmesini. Ek güncelleştirmeler gereksiz günlük gerektirdiğinden kullanılmayan dizinler de hello sistemin genel performansı etkiler.

Merhaba, tablolarından veri okumak ve düşük etkili güncelleştirmeleri hello sorguların performansını artırmaya dizinleri en iyi kümesi bulma sürekli ve karmaşık analiz gerektirebilir.

Azure SQL veritabanı yerleşik zekaya ve sorgularınızı çözümlemek, geçerli iş yükleri için en uygun olacak dizinleri tanımlamak Gelişmiş kurallar kullanır ve hello dizinleri kaldırılabilir. Azure SQL veritabanı veri okuma hello sorguları en iyi duruma getirme dizinleri gerekli en az sayıda sahip olmasını sağlar, üzerindeki etkiyi en aza hello ile diğer sorgular hello.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Nasıl tooidentify veritabanınızda değiştirilen bu gereksinimi toobe dizinler?

Azure SQL veritabanı dizin yönetimi işlemini kolaylaştırır. Azure SQL veritabanı yükünüzü çözümler hello can sıkıcı işlemi el ile iş yükü analiz ve dizin izleme yerine yeni bir dizin ile daha hızlı yürütülebilir hello sorguları tanımlar ve kullanılmayan veya yinelenen dizinleri tanımlar. Konumundaki değiştirilmelidir dizinleri tanımlaması hakkında daha fazla bilgi bulmak [dizin önerileri Azure Portalı'nda bulmak](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Otomatik dizin yönetimi konuları

Merhaba yerleşik kurallar veritabanınızı hello performansının artırılmasına bulursanız, Azure SQL veritabanını otomatik olarak dizinlerinizi Yönet sağlayabilir.

Azure SQL veritabanlarında toocreate gerekli dizinler kaynaklarını tüketebilir ve geçici olarak iş yükü performansını etkileyen eylemler gereklidir. Dizin oluşturma iş yükü performansı, Azure SQL veritabanı toominimize hello etkisini hello uygun zaman penceresi için herhangi bir dizin yönetimi işlem bulur. Eylem ayarlama hello veritabanının yükünüzü kaynakları tooexecute gerekiyorsa Ertelenen ve hello veritabanı yeterli olduğunda başlatılan hello bakım görevini kullanılabilmesi için kullanılmayan kaynaklar. Otomatik Dizin Yönetimi'nde bir önemli özellik hello eylemlerin bir onaydır. Azure SQL veritabanı oluşturur veya dizin bırakır, izleme işlemi hello eylemin hello performans geliştirilmiş, iş yükü tooverify performansını analiz eder. Önemli iyileştirme – Getir alamadık, hello eylem hemen geri döndürüldü. Bu şekilde, otomatik Eylemler, İş yükünüzün performansını olumsuz etkilemez Azure SQL veritabanı sağlar. Otomatik ayarlama tarafından oluşturulan dizinleri hello temel şeması hello bakım işlemi için saydamdır. Şema değişiklikleri bırakmayı veya sütunları yeniden adlandırma gibi otomatik olarak oluşturulan dizinleri hello varlığını tarafından engellenmez. Azure SQL veritabanı tarafından otomatik olarak oluşturulan dizinleri hemen bırakılır ne zaman ilgili tablo veya sütun bırakıldı.

## <a name="automatic-plan-choice-correction"></a>Otomatik planı seçim düzeltme

Otomatik planı düzeltme SQL Server 2017 CTP2.0 içinde işlemiyorsa SQL planları tanımlayan eklenen yeni bir otomatik ayarlama özelliğidir. Bu otomatik ayarlama seçeneğini, Azure SQL veritabanı yakında çıkıyor. Daha fazla bilgi bulmak [otomatik SQL Server 2017 ayarlama](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Sonraki adımlar

- tooenable ayarlama Azure SQL veritabanı ve let otomatik otomatik ayarı özelliğini tam olarak İş yükünüzün yönetmek için bkz: [otomatik ayarlamayı etkinleştirmek](sql-database-automatic-tuning-enable.md).
- toouse el ile ayarlama, gözden geçirebilirsiniz [önerileri Azure portalında ayarlama](sql-database-advisor-portal.md) ve el ile Merhaba sorgularınızı performansını olanları uygulayın.
