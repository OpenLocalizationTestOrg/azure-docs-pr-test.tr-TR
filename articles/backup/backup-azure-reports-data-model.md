---
title: "Azure Backup için aaaData modeli"
description: "Bu makalede, Azure Backup raporları için Power BI veri modeli ayrıntılarına hakkında alınmaktadır."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Azure Backup raporları için veri modeli
Bu makalede, Azure Backup raporlar oluşturmak için kullanılan hello Power BI veri modeli açıklanır. Bu veri modeli kullanarak, varolan raporlarla ilgili alanlara göre filtreleyebilirsiniz ve daha fazla tabloları ve alanları hello modelinde kullanarak da önemlisi, kendi raporlarınızı oluşturun. 

## <a name="creating-new-reports-in-power-bi"></a>Power BI'da yeni raporları oluşturma
Power BI yapabilecekleriniz kullandığı özelleştirme özellikleri sağlar [hello veri modelini kullanarak raporları oluşturma](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).

## <a name="using-azure-backup-data-model"></a>Azure Backup veri modelini kullanma
Merhaba verilerin bir kısmını toocreate raporları model ve mevcut raporları özelleştirme gibi sağlanan alanları izleyen hello kullanabilirsiniz.

### <a name="alert"></a>Uyarı
Bu tablo üzerinde çeşitli uyarı ilgili alanları temel alan ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #AlertsCreatedInPeriod |Tam sayı |Seçilen bir zaman diliminde oluşturulan uyarıların sayısı |
| % ActiveAlertsCreatedInPeriod |Yüzdesi |Seçilen zaman aralığı içindeki etkin uyarılar yüzdesi |
| % CriticalAlertsCreatedInPeriod |Yüzdesi |Seçilen zaman aralığı içinde kritik uyarılar yüzdesi |
| AlertOccurenceDate |Tarih |Uyarının oluşturulduğu tarih |
| AlertSeverity |Metin |Örneğin, kritik hello uyarının önem derecesini |
| AlertStatus |Metin |Örneğin, etkin hello uyarı durumu |
| AlertType |Metin |Örneğin, yedekleme hello oluşturulan uyarı türü |
| AlertUniqueId |Metin |Merhaba benzersiz kimliğini uyarıyı üreten |
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |Ondalık sayı |Seçilen zaman aralığı için ortalama süre (dakika cinsinden) tooresolve Uyarısı |
| EntityState |Metin |Örneğin, etkin, silinen hello uyarı nesnenin geçerli durumu |

### <a name="backup-item"></a>Yedekleme öğesi
Bu tablo üzerinde çeşitli yedekleme öğesi ilişkili alanlar temel alanlar ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #BackupItems |Tam sayı |Yedekleme öğelerin sayısı |
| #UnprotectedBackupItems |Tam sayı |Koruma için durduruldu veya yedeklemeleri ancak başlatılmamış yedeklemeler için yapılandırılan yedekleme öğelerinin sayısı|
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| BackupItemFriendlyName |Metin |Yedekleme öğesinin kolay adı |
| BackupItemId |Metin |Yedekleme öğesinin kimliği |
| BackupItemName |Metin |Yedekleme öğesinin adı |
| BackupItemType |Metin |Yedekleme öğesi Örneğin, VM, FileFolder türü |
| EntityState |Metin |Örneğin, etkin, silinen hello yedekleme öğesi nesnenin geçerli durumu |
| LastBackupDateTime |Tarih/saat |Yedekleme seçili öğe için son yedekleme zamanı |
| LastBackupState |Metin |Örneğin, başarılı, başarısız yedekleme seçili öğe için son yedekleme durumu |
| LastSuccessfulBackupDateTime |Tarih/saat |Seçili yedekleme öğesi için son başarılı yedekleme saati |
| ProtectionState |Metin |Örneğin, korumalı, ProtectionStopped hello yedekleme öğesinin geçerli koruma durumu |

### <a name="calendar"></a>Takvim
Bu tablo takvim ilişkili alanlar hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| Tarih |Tarih |Verileri filtreleme için seçilen tarihi |
| DateKey |Metin |Her bir tarih öğesi için benzersiz anahtar |
| DayDiff |Ondalık sayı |Filtreleme veriler için gün içinde örneğin fark, 0, geçerli günün verileri gösterir, bir önceki günün veri -1 gösterir, 0 ile -1 geçerli ve önceki gün için veri gösterir  |
| Ay |Metin |Ay ay verileri filtreleme için seçili hello yılın ilk günü başlayan ve biten 31 gün |
| MonthDate | Tarih |Tarih hello ay ay sona erdiğinde, veri filtreleme için seçili |
| MonthDiff |Ondalık sayı |Filtreleme veriler için aydaki örneğin fark, 0, geçerli ayın verilerini gösterir, önceki ayın veri -1 gösterir, 0 ile -1, geçerli ve önceki ay için verileri belirtmek |
| Hafta |Metin |Verileri filtreleme için seçilen hafta hafta Pazar günü başlar ve biter Cumartesi günleri |
| WeekDate |Tarih |Tarihi hello hafta hafta sona erdiğinde, veri filtreleme için seçili |
| WeekDiff |Ondalık sayı |Hafta filtreleme veriler için örneğin fark, 0, geçerli haftanın verilerini gösterir, önceki haftanın veri -1 gösterir, 0 ile -1 için geçerli ve önceki hafta verileri belirtmek |
| Yıl |Metin |Verileri filtreleme için seçili takvim yılı |
| YearDate |Tarih |Tarih hello yılın yıl sona erdiğinde, veri filtreleme için seçili |

### <a name="job"></a>İş
Bu tablo üzerinde çeşitli iş ile ilgili alanları temel alan ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #JobsCreatedInPeriod |Tam sayı |Zaman aralığı seçili hello oluşturulan iş sayısı |
| % FailuresForJobsCreatedInPeriod |Yüzdesi |Yüzde genel, süre seçili hello hatalarına işi |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |Ondalık sayı |Veri 80. yüzde birlik değerini aktarılan MB için **yedekleme** süre seçili hello oluşturulan işler |
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |Ondalık sayı |Ortalama zaman dakika cinsinden **tamamlanmış yedeği** seçilen bir zaman diliminde oluşturulan işler |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |Ondalık sayı |Ortalama zaman dakika cinsinden **geri yükleme tamamlandı** seçilen bir zaman diliminde oluşturulan işler |
| BackupStorageDestination |Metin |Yedekleme depolama Örneğin, bulut, Disk hedefi  |
| EntityState |Metin |Örneğin, etkin, silinen hello iş nesnenin geçerli durumu |
| JobFailureCode |Metin |Hata kodu dize hangi nedeniyle iş başarısız oldu |
| JobOperation |Metin |İçin proje Örneğin, yedekleme, geri yükleme, yapılandırma yedekleme çalıştığı işlemi |
| JobStartDate |Tarih |İş çalışmaya başladığı tarih |
| JobStartTime |Zaman |Çalışan işin başladığı zaman zaman |
| JobStatus |Metin |Merhaba durumunu iş Örneğin, tamamlandı tamamlandı, başarısız oldu |
| JobUniqueId |Metin |Benzersiz kimliği tooidentify hello işi |

### <a name="policy"></a>İlke
Bu tablo üzerinde çeşitli ilkesiyle ilgili alanları temel alan ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #Policies |Tam sayı |Merhaba sistemde mevcut yedekleme ilkeleri sayısı |
| #PoliciesInUse |Tam sayı |Şu anda yedeklemeleri yapılandırma için kullanılan ilkeleri sayısı |
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| BackupDaysOfTheWeek |Metin |Yedeklemelerin ne zaman zamanlandı hello haftanın günleri |
| BackupFrequency |Metin |Yedeklemeler, çalıştığı Örneğin, günlük, haftalık sıklığı |
| BackupTimes |Metin |Yedeklemelerin ne zaman zamanlanmış tarih ve saat |
| DailyRetentionDuration |Tam sayı |Yapılandırılan yedekleme için gün cinsinden toplam tutma süresi |
| DailyRetentionTimes |Metin |Tarih ve saat günlük bekletme zaman yapılandırıldı |
| EntityState |Metin |Örneğin, etkin, silinen hello İlkesi nesnenin geçerli durumu |
| MonthlyRetentionDaysOfTheMonth |Metin |Aylık bekletme için seçili hello ayın tarihleri |
| MonthlyRetentionDaysOfTheWeek |Metin |Aylık bekletme için hello haftanın günlerini seçili |
| MonthlyRetentionDuration |Ondalık sayı |Yapılandırılmış yedeklemeler için ay cinsinden toplam tutma süresi |
| MonthlyRetentionFormat |Metin |Aylık bekletme yapılandırmasının Örneğin, günlük tabanlı, haftalık dayalı haftanın günü için yazın |
| MonthlyRetentionTimes |Metin |Tarih ve saat aylık bekletme zaman yapılandırılır |
| MonthlyRetentionWeeksOfTheMonth |Metin |Aylık bekletme olduğunda hello ayın haftasını, örneğin, ilk, son vb. yapılandırılmış. |
| PolicyName |Metin |Tanımlanan hello ilke adı |
| PolicyUniqueId |Metin |Benzersiz kimliği tooidentify hello İlkesi |
| RetentionType |Metin |Örneğin, günlük, haftalık, aylık, yıllık bekletme ilkesi, yazın |
| WeeklyRetentionDaysOfTheWeek |Metin |Merhaba haftanın günlerini haftalık bekletme için seçili |
| WeeklyRetentionDuration |Ondalık sayı |Yapılandırılmış yedeklemeler için hafta cinsinden toplam haftalık tutma süresi |
| WeeklyRetentionTimes |Metin |Tarih ve saat haftalık bekletme zaman yapılandırılır |
| YearlyRetentionDaysOfTheMonth |Metin |Yıllık bekletme için seçili hello ayın tarihleri |
| YearlyRetentionDaysOfTheWeek |Metin |Merhaba haftanın günlerini yıllık bekletme için seçili |
| YearlyRetentionDuration |Ondalık sayı |Yapılandırılmış yedeklemeleri yıldır cinsinden toplam tutma süresi |
| YearlyRetentionFormat |Metin |Yıllık bekletme yapılandırmasının Örneğin, günlük tabanlı, haftalık dayalı haftanın günü için yazın |
| YearlyRetentionMonthsOfTheYear |Metin |Merhaba yılın ay yıllık bekletme için seçili |
| YearlyRetentionTimes |Metin |Tarih ve saat yıllık bekletme zaman yapılandırılır |
| YearlyRetentionWeeksOfTheMonth |Metin |Yıllık bekletme olduğunda hello ayın haftasını, örneğin, ilk, son vb. yapılandırılmış. |

### <a name="protected-server"></a>Korumalı sunucu
Bu tablo üzerinde çeşitli korumalı sunucu ilgili alanlar temel alanlar ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #ProtectedServers |Tam sayı |Korumalı sunucu sayısı |
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| AzureBackupAgentOSType |Metin |Azure yedekleme Aracısı'nın işletim sistemi türü |
| AzureBackupAgentOSVersion |Metin |Azure yedekleme Aracısı'nın işletim sistemi sürümü |
| AzureBackupAgentUpdateDate |Metin |Aracı Backup Aracısı güncelleştirildiği tarihi |
| AzureBackupAgentVersion |Metin |Aracı yedekleme sürümünün sürüm numarası |
| BackupManagementType |Metin |Örneğin, IaaSVM FileFolder yedeklemenin için sağlayıcı türü |
| EntityState |Metin |Örneğin, etkin, silinen hello korumalı sunucu nesnenin geçerli durumu |
| ProtectedServerFriendlyName |Metin |Korumalı sunucusunun kolay adı |
| ProtectedServerName |Metin |Korumalı sunucunun adı |
| ProtectedServerType |Metin |Örneğin, IaaSVMContainer korumalı sunucu türünü yedeklenen |
| ProtectedServerName |Metin |Korumalı sunucu toowhich yedekleme öğesinin adını ait |
| RegisteredContainerId |Metin |Yedekleme için kayıtlı kapsayıcı kimliği |

### <a name="storage"></a>Depolama
Bu tablo üzerinde çeşitli depolama ilişkili alanlar temel alanlar ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #ProtectedInstances |Ondalık sayı |Seçilen zaman içinde ön uç depolama faturalama, hesaplanan dayalı olarak en son değeri hesaplamak için kullanılan korumalı örneği sayısı |
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| CloudStorageInMB |Ondalık sayı |Hesaplanan yedekleri tarafından kullanılan bulut yedekleme depolama alanı en son değeri seçili zaman dayanır. |
| EntityState |Metin |Örneğin, etkin, silinen hello nesnenin geçerli durumu |
| LastUpdatedDate |Tarih |Seçilen satırın en son güncelleştirildiği tarihi |

### <a name="time"></a>Zaman
Bu tablo saati ile ilgili alanları hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| Saat |Zaman |Örneğin, 1:00:00 PM hello günün saati |
| HourNumber |Ondalık sayı |Merhaba gün örneğin 13,00 saat sayısı |
| Dakika |Ondalık sayı |Merhaba saat, dakika |
| PeriodOfTheDay |Metin |Merhaba gün Örneğin, 12-3 AM dönem yuvada zaman |
| Zaman |Zaman |Örneğin, 00:00:01: 00 hello günün saati |
| TimeKey |Metin |Anahtar değeri toorepresent saat |

### <a name="vault"></a>Kasa
Bu tablo üzerinde çeşitli kasası ilişkili alanlar temel alanlar ve toplamalar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| #Vaults |Tam sayı |Kasa sayısı |
| AsOnDateTime |Tarih/saat |Son yenileme zamanının hello seçili satır için |
| AzureDataCenter |Metin |Kasa bulunduğu veri merkezi |
| EntityState |Metin |Örneğin, etkin, silinen hello kasası nesnenin geçerli durumu |
| StorageReplicationType |Metin |Örneğin, GeoRedundant hello kasası için depolama çoğaltma türü |
| SubscriptionId |Metin |Rapor oluşturmak için seçilen hello müşterinin abonelik kimliği |
| VaultName |Metin |Merhaba kasasının adını |
| VaultTags |Metin |Etiketler ilişkili toohello kasası |

## <a name="next-steps"></a>Sonraki adımlar
Azure Backup raporları oluşturmak için hello veri modeli gözden sonra makaleleri oluşturma ve Power BI raporları görüntüleme hakkında daha fazla ayrıntı için aşağıdaki hello başvurun.

* [Power BI raporları oluşturma](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [Power BI raporları filtreleme](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
