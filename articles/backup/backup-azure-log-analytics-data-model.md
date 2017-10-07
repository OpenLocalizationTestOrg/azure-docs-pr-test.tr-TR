---
title: Azure Backup aaaLog Analytics veri modeli
description: "Bu makalede, Azure yedekleme verileri için günlük analizi veri modeli ayrıntılarına hakkında alınmaktadır."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Azure yedekleme verileri için günlük analizi veri modeli
Bu makalede, raporlama veri tooLog Analytics gönderilmesi için kullanılan hello veri modeli açıklanır. Bu veri modelini kullanarak özel sorgular, panolar, oluşturma ve OMS içinde kullanma. 

## <a name="using-azure-backup-data-model"></a>Azure Backup veri modelini kullanma
Merhaba veri modeli toocreate görselleri, özel sorgular ve Pano gereksinimlerinizi bir parçası olarak sağlanan alanları izleyen hello kullanabilirsiniz.

### <a name="alert"></a>Uyarı
Bu tablo uyarı ilgili alanları hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| AlertUniqueId_s |Metin |Merhaba benzersiz kimliğini uyarıyı üreten |
| AlertType_s |Metin |Uyarı, örneğin, yedekleme hello türünü oluşturulan |
| AlertStatus_s |Metin |Merhaba uyarı, örneğin, etkin durumu |
| AlertOccurenceDateTime_s |Tarih/saat |Tarih ve uyarının oluşturulduğu saat |
| AlertSeverity_s |Metin |Merhaba uyarının, örneğin, kritik önem derecesini |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| BackupItemUniqueId_s |Metin |Bu uyarı çok ait hello yedekleme öğesi toowhich benzersiz kimliği|
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Merhaba uyarı nesnenin, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu uyarı çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - uyarı adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| ProtectedServerUniqueId_s |Metin |Bu uyarı çok ait toowhich hello benzersiz kimliğini korumalı|
| VaultUniqueId_s |Metin |Bu uyarı çok ait toowhich hello benzersiz kimliğini korumalı|
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="backupitem"></a>BackupItem
Bu tablo yedekleme öğesi ilişkili alanlar hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |  
| BackupItemUniqueId_s |Metin |Merhaba yedekleme öğesinin benzersiz kimliği |
| BackupItemId_s |Metin |Yedekleme öğesinin kimliği |
| BackupItemName_s |Metin |Yedekleme öğesinin adı |
| BackupItemFriendlyName_s |Metin |Yedekleme öğesinin kolay adı |
| BackupItemType_s |Metin |Yedekleme öğesi, örneğin, VM, FileFolder türü |
| ProtectedServerName_s |Metin |Korumalı sunucu toowhich yedekleme öğesinin adını çok ait|
| ProtectionState_s |Metin |Merhaba yedekleme öğesi, örneğin, korumalı, ProtectionStopped geçerli koruma durumu |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Merhaba yedekleme öğesi nesnenin, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu yedekleme öğesi çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - BackupItem adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="backupitemassociation"></a>BackupItemAssociation
Bu tabloda, çeşitli varlıkları yedekleme öğesi ilişkilerini hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |  
| BackupItemUniqueId_s |Metin |Merhaba yedekleme öğesinin benzersiz kimliği |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Merhaba yedekleme öğesi ilişkilendirme nesnenin, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu yedekleme öğesi çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - BackupItemAssociation adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| PolicyUniqueId_g |Metin |Hangi yedekleme öğesi çok ilişkilendirilen benzersiz kimliği tooidentify hello İlkesi|
| ProtectedServerUniqueId_s |Metin |Bu yedekleme öğesi çok ait sunucu toowhich hello benzersiz kimliğini korumalı|
| VaultUniqueId_s |Metin |Bu yedekleme öğesi çok ait hello kasa toowhich benzersiz kimliği|
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="job"></a>İş
Bu tabloyu işle ilgili alanları hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| BackupItemUniqueId_s |Metin |Bu iş çok ait hello yedekleme öğesi toowhich benzersiz kimliği|
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Merhaba iş nesnesi, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu iş çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan iş hello geçerli işlem - adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| ProtectedServerUniqueId_s |Metin |Bu iş çok ait toowhich hello benzersiz kimliğini korumalı|
| VaultUniqueId_s |Metin |Bu iş çok ait toowhich hello benzersiz kimliğini korumalı|
| JobOperation_s |Metin |İçin proje Örneğin, yedekleme, geri yükleme, yapılandırma yedekleme çalıştığı işlemi |
| JobStatus_s |Metin |İş, örneğin, tamamlandı, başarısız hello durumunu tamamlandı |
| JobFailureCode_s |Metin |Hata kodu dize hangi nedeniyle iş başarısız oldu |
| JobStartDateTime_s |Tarih/saat |Tarih ve saat başlatılan çalışan iş yapılırken |
| BackupStorageDestination_s |Metin |Yedekleme depolama, örneğin, bulut, Disk hedefi  |
| JobDurationInSecs_s | Sayı |Saniye cinsinden toplam iş yürütme süresi |
| DataTransferredInMB_s | Sayı |Bu proje için MB cinsinden aktarılan veriler|
| JobUniqueId_g |Metin |Benzersiz kimliği tooidentify hello işi |
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="policy"></a>İlke
Bu tablo ilkesiyle ilgili alanları hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Hello İlkesi nesnesini, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu ilkenin çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - ilke adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| PolicyUniqueId_g |Metin |Benzersiz kimliği tooidentify hello İlkesi |
| PolicyName_s |Metin |Tanımlanan hello ilke adı |
| BackupFrequency_s |Metin |Hangi yedeklemeler çalıştırılır, örneğin, günlük, haftalık sıklığı |
| BackupTimes_s |Metin |Yedeklemelerin ne zaman zamanlanmış tarih ve saat |
| BackupDaysOfTheWeek_s |Metin |Yedeklemelerin ne zaman zamanlandı hello haftanın günleri |
| RetentionDuration_s |Tam sayı |Yapılandırılmış yedeklemeler için elde tutma süresi |
| DailyRetentionDuration_s |Tam sayı |Yapılandırılan yedekleme için gün cinsinden toplam tutma süresi |
| DailyRetentionTimes_s |Metin |Tarih ve saat günlük bekletme zaman yapılandırıldı |
| WeeklyRetentionDuration_s |Ondalık sayı |Yapılandırılmış yedeklemeler için hafta cinsinden toplam haftalık tutma süresi |
| WeeklyRetentionTimes_s |Metin |Tarih ve saat haftalık bekletme zaman yapılandırılır |
| WeeklyRetentionDaysOfTheWeek_s |Metin |Merhaba haftanın günlerini haftalık bekletme için seçili |
| MonthlyRetentionDuration_s |Ondalık sayı |Yapılandırılmış yedeklemeler için ay cinsinden toplam tutma süresi |
| MonthlyRetentionTimes_s |Metin |Tarih ve saat aylık bekletme zaman yapılandırılır |
| MonthlyRetentionFormat_s |Metin |Aylık bekletme, örneğin, günlük tabanlı, haftalık dayalı haftanın günü için yapılandırma türü |
| MonthlyRetentionDaysOfTheWeek_s |Metin |Aylık bekletme için hello haftanın günlerini seçili |
| MonthlyRetentionWeeksOfTheMonth_s |Metin |Örneğin, ilk, son vb. hafta aylık bekletme yapılandırıldığında, hello ayın. |
| YearlyRetentionDuration_s |Ondalık sayı |Yapılandırılmış yedeklemeleri yıldır cinsinden toplam tutma süresi |
| YearlyRetentionTimes_s |Metin |Tarih ve saat yıllık bekletme zaman yapılandırılır |
| YearlyRetentionMonthsOfTheYear_s |Metin |Merhaba yılın ay yıllık bekletme için seçili |
| YearlyRetentionFormat_s |Metin |Tür yıllık bekletme, örneğin, günlük tabanlı, haftalık dayalı haftanın günü için yapılandırma |
| YearlyRetentionDaysOfTheMonth_s |Metin |Yıllık bekletme için seçili hello ayın tarihleri |
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="policyassociation"></a>PolicyAssociation
Bu tablo ilke ilişkilendirmelerini çeşitli varlıkları ile ilgili ayrıntıları sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Hello İlkesi nesnesini, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu ilkenin çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - PolicyAssociation adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| PolicyUniqueId_g |Metin |Benzersiz kimliği tooidentify hello İlkesi |
| VaultUniqueId_s |Metin |Bu ilke çok ait hello kasa toowhich benzersiz kimliği|
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="protectedserver"></a>ProtectedServer
Bu tablo korumalı sunucu ilgili alanlar hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| ProtectedServerName_s |Metin |Korumalı sunucunun adı |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Sunucu nesnesi, örneğin, etkin, silinen hello geçerli durumunu korumalı |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu korumalı sunucunun çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - ProtectedServer adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| ProtectedServerUniqueId_s |Metin |Merhaba benzersiz kimliğini korumalı sunucusu |
| RegisteredContainerId_s |Metin |Yedekleme için kayıtlı kapsayıcı kimliği |
| ProtectedServerType_s |Metin |Örneğin, Windows Kurulumu türü korumalı sunucunun yedeği |
| ProtectedServerFriendlyName_s |Metin |Korumalı sunucusunun kolay adı |
| AzureBackupAgentVersion_s |Metin |Aracı yedekleme sürümünün sürüm numarası |
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Bu tablo korumalı sunucu ilişkilendirmeleri diğer varlıklarla ilgili ayrıntıları sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Sunucusu ilişki nesnesi, örneğin, etkin, silinen hello geçerli durumunu korumalı |
| BackupManagementType_s |Metin |Yedekleme, örneğin, IaaSVM, bu korumalı sunucunun çok ait FileFolder toowhich gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - ProtectedServerAssociation adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| ProtectedServerUniqueId_s |Metin |Merhaba benzersiz kimliğini korumalı sunucusu |
| VaultUniqueId_s |Metin |Bu korumalı sunucunun çok ait hello kasa toowhich benzersiz kimliği|
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

### <a name="storage"></a>Depolama
Bu tablo depolama ilişkili alanlar hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| CloudStorageInBytes_s |Ondalık sayı |Bulut yedekleme depolama hesaplanan yedekleri tarafından kullanılan son değere göre |
| ProtectedInstances_s |Ondalık sayı |Ön uç depolama faturalama, hesaplanan dayalı olarak en son değeri hesaplamak için kullanılan korumalı örneği sayısı |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Merhaba depolama nesnesi, örneğin, etkin, silinen geçerli durumu |
| BackupManagementType_s |Metin |Örneğin, IaaSVM, bu depolama çok ait FileFolder toowhich Yedekleme gerçekleştirmek için sağlayıcı türü|
| OperationName |Metin |Bu alan hello geçerli işlem - depolama adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| ProtectedServerUniqueId_s |Metin |Merhaba benzersiz kimliğini korumalı depolama hesaplandığı sunucusu |
| VaultUniqueId_s |Metin |Merhaba kasası depolama için benzersiz kimliğini hesaplanır |
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan representse kendisi için veri toplanırken - hello kaynak kasalarını yazın |

### <a name="vault"></a>Kasa
Bu tablo, kasa ile ilgili alanları hakkında ayrıntılar sağlar.

| Alan | Veri türü | Açıklama |
| --- | --- | --- |
| EventName_s |Metin |Bu alan bu olay adını temsil eder, her zaman AzureBackupCentralReport. |
| SchemaVersion_s |Metin |Bu alan geçerli hello şema sürümü gösterir, **V1** |
| State_s |Metin |Merhaba kasası nesnenin, örneğin, etkin, silinen geçerli durumu |
| OperationName |Metin |Bu alan hello geçerli işlem - kasa adını temsil eder |
| Kategori |Metin |Bu alan tooLog Analytics gönderilen tanılama verilerini kategorisini temsil eder, AzureBackupReport. |
| Kaynak |Metin |Bu veri toplanmakta hello kaynak, Kurtarma Hizmetleri kasa adı gösterir |
| VaultUniqueId_s |Metin |Merhaba kasasının benzersiz kimliği |
| VaultName_s |Metin |Merhaba kasasının adını |
| AzureDataCenter_s |Metin |Kasa bulunduğu veri merkezi |
| StorageReplicationType_s |Metin |Merhaba kasası, örneğin, GeoRedundant için depolama çoğaltma türü |
| SourceSystem |Metin |Kaynak sistemi hello geçerli verilerin - Azure |
| ResourceId |Metin |İsteğe bağlı olarak veri toplanmakta Bu alan temsil kaynak kimliği kurtarma Hizmetleri kasası kaynak kimliği gösterir |
| SubscriptionId |Metin |Bu alan, abonelik kimliği için veri toplanırken hello kaynağın (RS kasa) temsil eder |
| ResourceGroup |Metin |Bu alan için veri toplanırken hello kaynak (RS kasa) kaynak grubunu temsil eder |
| ResourceProvider |Metin |Bu alan için veri toplanırken - hello kaynak sağlayıcısı Microsoft.RecoveryServices temsil eder |
| ResourceType |Metin |Bu alan için veri toplanırken - hello kaynak kasalarını türünü temsil eder |

## <a name="next-steps"></a>Sonraki adımlar
Azure Backup raporları oluşturmak için hello veri modeli gözden sonra başlatabilirsiniz [Pano oluşturma](../log-analytics/log-analytics-dashboards.md) günlük analizi ve OMS.
