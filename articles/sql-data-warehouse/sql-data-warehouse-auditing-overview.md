---
title: Azure SQL Data warehouse'da aaaAuditing | Microsoft Docs
description: "Azure SQL Data Warehouse'da denetimi ile çalışmaya başlama"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Azure SQL veri ambarı'nda denetleme
> [!div class="op_single_selector"]
> * [Denetim](sql-data-warehouse-auditing-overview.md)
> * [Tehdit algılama](sql-data-warehouse-security-threat-detection.md)
> 
> 

SQL veri ambarı denetim toorecord olayları, veritabanı tooan Denetim günlüğüne Azure depolama hesabınızdaki sağlar. Denetim, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve iş endişeleri veya güvenlik ihlalleri hakkında daha fazla bilgi kavramanıza yardımcı olabilir. Ayrıca SQL Data Warehouse denetim Microsoft Power BI ile ayrıntıya raporlama ve analiz için ile tümleştirir.

Denetleme Araçları etkinleştirmek ve bağlılığı toocompliance standartları kolaylaştırmak ancak Uyumluluk garanti etmez. Bu destek standartları uyumluluğu Azure hakkında daha fazla bilgi programları hello bakın <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Güven Merkezi</a>.

* [Veritabanı denetim temelleri]
* [Veritabanınız için denetimi ayarlamanız]
* [Denetim günlüklerini ve raporları analiz eder.]

## <a id="subheading-1"></a>Azure SQL veri ambarı veritabanı denetimi temelleri
SQL veri ambarı veritabanı denetimi yapmanıza olanak sağlar:

* **Korumak** seçili olayların bir denetim izi. Denetlenecek veritabanı Eylemler toobe kategorilerini tanımlayabilirsiniz.
* **Rapor** veritabanı etkinlik. Önceden yapılandırılmış raporları ve etkinlik ve olay Raporlama ile hızlı şekilde kullanmaya bir Pano tooget kullanabilirsiniz.
* **Analiz** raporlar. Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.

Olay kategorileri aşağıdaki Merhaba denetimini yapılandırabilirsiniz:

**Düz SQL** ve **parametreli SQL** olarak sınıflandırılan hangi hello için toplanan denetim günlükleri  

* **Erişim toodata**
* **Şema değişiklikleri (DDL)**
* **Veri değişiklikleri (DML)**
* **Hesapları, rolleri ve izinleri (DCL)**
* **Saklı yordam**, **oturum açma** ve **işlem yönetimi**.

Her bir olay kategorisi için Denetim, **başarı** ve **hatası** işlemleri ayrı olarak yapılandırılır.

Merhaba hello etkinlikleri ve denetlenen olayları hakkında daha fazla bilgi için bkz: <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">denetim günlük biçimi başvurusu (doc dosya indirme)</a>.

Denetim günlükleri, Azure depolama hesabında depolanır. Bir denetim günlük Bekletme dönemi tanımlayabilirsiniz.

Bir denetim ilkesi, belirli bir veritabanı veya varsayılan sunucu ilkesi olarak tanımlanabilir. Varsayılan sunucu denetim ilkesi tooall veritabanları tanımlanmış bir özel geçersiz kılma veritabanı denetim ilkesi olmayan bir sunucu üzerinde uygulanır.

Denetimi kullanıyorsanız onay denetim ayarlamadan önce bir ["Alt düzey istemci."](sql-data-warehouse-auditing-downlevel-clients.md)

## <a id="subheading-2"></a>Veritabanınız için denetimi ayarlamanız
1. Merhaba başlatma <a href="https://portal.azure.com" target="_blank">Azure portal</a>.
2. Toohello Git **ayarları** hello tooaudit istediğiniz SQL Data Warehouse dikey. Merhaba, **ayarları** dikey penceresinde, select **denetim ve tehdit algılama**.
   
    ![][1]
3. Ardından, hello tıklayarak denetimi etkinleştirmek **ON** düğmesi.
   
    ![][3]
4. Yapılandırma dikey penceresi denetim hello seçin **depolama ayrıntıları** tooopen hello denetim günlüklerini depolama dikey. Merhaba burada günlükleri kaydedileceği Azure depolama hesabı, hello seçip saklama süresi. 
>[!TIP]
>Aynı depolama hesabı en hello dışında tüm denetlenen veritabanları tooget hello için önceden yapılandırılmış kullanım hello şablonları bildirir.
   
    ![][4]
5. Merhaba tıklatın **Tamam** düğme toosave hello depolama ayrıntıları yapılandırması.
6. Altında **tarafından olay günlüğü**, tıklatın **başarı** ve **hatası** toolog tüm olayları veya tek tek olay kategorilerini seçin.
7. Bir veritabanı için Denetim yapılandırıyorsanız, tooalter hello bağlantı dizesi verileri denetleme doğru yakalanır, istemci tooensure gerekebilir. Merhaba denetleyin [hello bağlantı dizesinde değişiklik sunucu FDQN](sql-data-warehouse-auditing-downlevel-clients.md) alt düzey istemci bağlantıları için konu.
8. **Tamam** düğmesine tıklayın.

## <a id="subheading-3"></a>Denetim günlüklerini ve raporları analiz eder.
Denetim günlüklerini toplanan deposu tablolarla koleksiyonunda bir **SQLDBAuditLogs** hello Kurulum sırasında seçtiğiniz Azure depolama hesabı önek. Bir aracı gibi kullanarak günlük dosyalarını görüntüleyebilirsiniz <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Gezgini</a>.

Önceden yapılandırılmış Pano rapor şablonu olarak kullanılabilir bir <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">indirilebilir Excel elektronik tablosu</a> toohelp günlük verileri hızlı bir şekilde çözümleyin. Denetim günlüklerini toouse hello şablonunda, gereksinim duyduğunuz Excel 2013 veya üstü ve indirebilirsiniz Power Query <a href="http://www.microsoft.com/download/details.aspx?id=39379">burada</a>.

Merhaba şablon kurgusal örnek veriler olan ve doğrudan Azure storage hesabınızdan, Denetim günlüğü Power Query tooimport ayarlayabilirsiniz.

## <a id="subheading-4"></a>Depolama anahtarını yeniden üretme
Üretimde, depolama alanınızın düzenli aralıklarla anahtarları büyük olasılıkla toorefresh demektir. Anahtarlarınızı yenilerken toosave hello İlkesi gerekir. Merhaba işlem aşağıdaki gibidir:

1. (Bölüm denetimi hello kurulumunda yukarıda) yapılandırma dikey penceresi denetim hello hello anahtarının **depolama erişim tuşu** gelen *birincil* çok*ikincil* ve  **Kaydet**.

   ![][4]
2. Git toohello depolama yapılandırma dikey ve **yeniden** hello *birincil erişim anahtarını*.
3. Yapılandırma dikey penceresinde, anahtar hello denetim toohello dönün **depolama erişim tuşu** gelen *ikincil* çok*birincil* ve basın **KAYDETMEK**.
4. Toohello depolama UI geri dönün ve **yeniden** hello *ikincil erişim anahtarını* (hello için hazırlık olarak sonraki anahtarları döngüsü yenileyin.

## <a id="subheading-5"></a>Otomasyon (PowerShell/REST API)
Otomasyon araçları aşağıdaki hello kullanarak Azure SQL Data Warehouse'da denetim da yapılandırabilirsiniz:

* **PowerShell cmdlet'leri**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Kullanım AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Veritabanı denetim temelleri]: #subheading-1
[Veritabanınız için denetimi ayarlamanız]: #subheading-2
[Denetim günlüklerini ve raporları analiz eder.]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy