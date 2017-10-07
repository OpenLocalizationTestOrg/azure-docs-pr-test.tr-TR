---
title: "Azure SQL Data Warehouse veritabanlarında aaaManage | Microsoft Docs"
description: "SQL veri ambarı veritabanlarını yönetmeye genel bakış. Yönetim Araçları, Dwu ve sorgu performansı, iyi bir güvenlik ilkeleri oluşturma ve veri bozulması veya bölgesel bir kesintinin bir veritabanını geri yükleme sorunlarını giderme genişleme performans içerir."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse veritabanlarında yönetme
SQL veri ambarı veritabanlarınızı yönetme birçok nokta otomatikleştirir. Örneğin, yalnızca tooadjust gerekir ve Merhaba sağ düzeyini işlem kaynaklarını ödeme ve SQL Data Warehouse izin tooscale performans ölçeğini genişletme ve geri ölçeklendirme tüm hello işini yapın.

Performansınızı gereken yanı sıra uzun süre çalışan sorgularda sorun giderme, iş yükü tooidentify toomonitor kuşkusuz isteyeceksiniz. Kullanıcılar ve oturum açmalar için birkaç güvenlik görevlerini toomanage izinleri de tooperform gerekir.

Bu genel bakışta bu yönlerini SQL veri ambarı yönetimi ele alınmaktadır.

* Yönetim araçları
* Bilgi işlem
* Duraklatma ve sürdürme
* Performansı en iyi uygulamalar
* Sorgu izlemesi
* Güvenlik
* Yedekleme ve geri yükleme

## <a name="management-tools"></a>Yönetim araçları
SQL veri ambarı'nda çeşitli araçlar toomanage veritabanlarıyla kullanabilirsiniz. Veritabanları yönetirken, aracı Tercihler geliştireceksiniz görevinin her türü için tooperform gerekir.

### <a name="azure-portal"></a>Azure portalına
Merhaba [Azure portal] [ Azure portal] burada oluşturabilir, güncelleştirme ve veritabanlarını silin ve veritabanı kaynaklarını izleme web tabanlı portal değil. Bu harika bir araçtır, yalnızca veri ambarı veritabanlarını, az sayıda yönetme Azure ile çalışmaya Başlarken veya tooquickly bir şey yapmanız gerekmiyor.

Hello Azure portal ile çalışmaya tooget bkz [SQL veri ambarı (Azure portalı) oluşturma][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server veri araçları Visual Studio
[SQL Server veri Araçları] [ SQL Server Data Tools] (SSDT) Visual Studio'da, yönetmek ve veritabanlarınızı geliştirmek tooconnect sağlar. Bir uygulama geliştiricisi Visual Studio'ya veya diğer tümleşik geliştirme ortamlarını (IDE) hakkında bilgi sahibi değilseniz, Visual Studio'da SSDT kullanmayı deneyin.

SSDT hello toovisualize sağlayan SQL Server Nesne Gezgini içerir, bağlanmak ve SQL Data Warehouse veritabanlarında komut dosyalarını çalıştır. tooquickly tooSQL veri ambarına bağlanmak, hello tıklamanız yeterlidir **Visual Studio'da Aç** hello veritabanı ayrıntıları hello Klasik Azure portalı görüntülerken hello komut çubuğu düğmesini.  

Visual Studio'da SSDT kullanmaya tooget bkz [sorgu Azure SQL Data Warehouse Visual Studio ile][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Komut satırı araçları
Komut satırı araçlarını, iş yüklerini otomatikleştirmek için idealdir.  PowerShell ve sqlcmd olan iki yolları tooautomate işlemlerinizi.  Çok sayıda mantıksal sunucuları yönetme ve gerekli hello görevleri komut dosyası ve daha sonra otomatik olarak kaynak değişiklikleri bir üretim ortamında dağıtmak için bu araçları öneririz.

### <a name="dynamic-management-views"></a>Dinamik Yönetim görünümlerini
Dmv'leri SQL veri ambarını yönetme hello ekmek ve ezmesi ' dir. Merhaba Portalı'nda ortaya çıkarır neredeyse tüm bilgi üzerinde Dmv'leri kullanır. toosee SQL veri ambarı Dmv'leri listesini görmek [SQL veri ambarı sistem görünümleri][SQL Data Warehouse system views].

başlatıldı, tooget bkz [bağlanma ve sorgu sqlcmd ile][Connect and query with sqlcmd], ve [veritabanı (PowerShell) oluşturma][Create a database (PowerShell)].

## <a name="scale-compute"></a>Bilgi işlem
SQL veri ambarı'nda performans out veya geri artırarak veya azaltarak işlem kaynakları CPU, bellek ve g/ç bant genişliği tarafından hızlı bir şekilde ölçeklendirebilirsiniz. tooscale performans tek toodo ihtiyacınız olan SQL Data Warehouse tooyour veritabanı ayırır veri ambarı birimi (Dwu) hello sayısını ayarlayın. SQL veri ambarı hızlı bir şekilde değiştirmek hello yapar ve tüm hello temel değişiklikleri toohardware veya yazılım işler.

Dwu, ölçeklendirme hakkında daha fazla toolearn bkz [ölçeklendirme performans].

## <a name="pause-and-resume"></a>Duraklatma ve sürdürme
toosave maliyetleri'nın, duraklatma ve sürdürme işlem kaynakları isteğe bağlı. Örneğin, hello veritabanı hello gece sırasında ve hafta sonları kullandığınız olmaz, bu saatlerde duraklatma ve hello günde sürdürün. Merhaba veritabanı duraklatıldığında Dwu için sizden ücret olmaz.

Daha fazla bilgi için bkz: [duraklatma işlem][Pause compute], ve [sürdürme işlem][Resume compute].

## <a name="performance-best-practices"></a>Performansı en iyi uygulamalar
Merhaba ipuçları ve en iyi sağ hello başından iş püf noktaları bulma ile yeni bir teknoloji Başlarken, çok fazla kaydedebilirsiniz.  Bizim konuları çoğunu tamamında en iyi yöntemler bulacaksınız.

toosee, iş yükü geliştirilirken en önemli noktalar hello birçok özetini görmek [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Sorgu izlemesi
Bazen bir sorgu uzun çalışıyor, ancak hello sorunlu hangi biri olduğundan emin değil. SQL veri ambarı, sorgu çok uzun sürüyor dinamik yönetim görünümlerini (Dmv'leri toofigure kullanabilirsiniz) sahiptir.

toofind uzun süre çalışan sorgular, bkz: [Dmv'leri kullanarak, iş yükünü izlemek][Monitor your workload using DMVs].

## <a name="security"></a>Güvenlik
toomaintain güvenli bir sistemde, her tür yetkisiz erişime karşı koruma ve hello uyarıdaki olması gerekir. Bir güvenlik sistemi toomake güvenlik duvarı kuralları yalnızca yetkili IP adreslerini bağlanabilir karşılandığından emin gerekir. Kullanıcı kimlik bilgilerinin düzgün bir kimlik doğrulaması gerekir. Bir kullanıcı toohello veritabanı bağlandı sonra hello kullanıcı yalnızca izinleri tooperform Eylemler en az sayıda sahip olmalıdır. toosecure veri şifreleme kullanabilirsiniz. Ayrıca, Denetim ve tüm şüpheli etkinlikleri ise olayları yeniden izlemesine şekilde izleme önemli toohave unutulmamalıdır.

Güvenlik, head toohello üzerinden yönetmeyle ilgili toolearn [güvenliğine genel bakış][Security overview].

## <a name="backup-and-restore"></a>Yedekleme ve geri yükleme
Verilerinizin güvenilir backps sahip, herhangi bir üretim veritabanını önemli bir parçasıdır. SQL veri ambarı otomatik olarak düzenli aralıklarla, etkin veritabanlarını yedekleyerek, verilerinizi güvenli tutar. Bu yedeklemeler buradan verilerinizi bozulmuş veya yanlışlıkla veri veya veritabanı bırakılan senaryolardan toorecover izin verin.  Merhaba veri yedekleme zamanlamasını, bekletme ilkesi için ve nasıl toorestore bir veritabanı bkz [anlık görüntüden geri][Restore from snapshot].

## <a name="next-steps"></a>Sonraki adımlar
İyi veritabanı tasarım ilkeleri kullanarak hale getirir, daha kolay toomanage SQL Data Warehouse veritabanınızda. toolearn daha toohello üzerinden head [geliştirmeye genel bakış][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[ölçeklendirme performans]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
