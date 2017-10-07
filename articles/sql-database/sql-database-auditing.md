---
title: "aaaGet başlatılan Azure SQL veritabanı denetimi ile | Microsoft Docs"
description: "Azure SQL veritabanı denetimi ile çalışmaya başlama"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>SQL veritabanı denetimini kullanmaya başlayın
Azure SQL veritabanı denetimi veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar. Ayrıca denetleme:

* Yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve iş endişeleri veya güvenlik ihlalleri hakkında daha fazla bilgi kavramanıza yardımcı olur.

* Etkinleştirir ve uyumluluk garanti etmez ancak bağlılığı toocompliance standartları kolaylaştırır. Bu destek standartları uyumluluğu Azure hakkında daha fazla bilgi programları hello bakın [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Genel Bakış denetim azure SQL veritabanı
SQL veritabanı için denetimi kullanabilirsiniz:


* **Korumak** seçili olayların bir denetim izi. Denetlenecek veritabanı Eylemler toobe kategorilerini tanımlayabilirsiniz.
* **Rapor** veritabanı etkinlik. Önceden yapılandırılmış raporları ve etkinlik ve olay Raporlama ile hızlı şekilde kullanmaya bir Pano tooget kullanabilirsiniz.
* **Analiz** raporlar. Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.

Farklı türlerde olay kategorisi için Denetim hello açıklandığı gibi yapılandırabileceğiniz [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.

Denetim günlüklerini tooAzure Blob storage, Azure aboneliğinizde yazılır.


## <a id="subheading-8"></a>Sunucu düzeyinde ve veritabanı düzeyi denetim ilkesi tanımlayın

Bir denetim ilkesi, belirli bir veritabanı veya varsayılan sunucu ilkesi olarak tanımlanabilir:

* Bir sunucu ilkesi tooall mevcut ve yeni oluşturulan veritabanları hello sunucu üzerinde uygulanır.

* Varsa *sunucu blob denetimi etkin*, onu *toohello veritabanı her zaman geçerli* (diğer bir deyişle, hello veritabanı denetlenmez), bağımsız olarak hello veritabanı denetim ayarları.

* Merhaba veritabanında toplama tooenabling üzerinde hello sunucuda denetim blob etkinleştirme olacak *değil* geçersiz kılabilir veya hello sunucu blob denetleme hello ayarlardan herhangi birini değiştirmek. Her iki denetimleri yan yana yer alır. Diğer bir deyişle, hello veritabanı (kez hello sunucu İlkesi ve bir kez tarafından hello veritabanı İlkesi) iki kez paralel olarak denetlenecektir.

   > [!NOTE]
   > Sunucu blob denetlenmesi ve veritabanı blob birlikte denetimi sürece etkinleştirme kaçınmanız gerekir:
    > * Farklı bir toouse istediğiniz *depolama hesabı* veya *saklama dönemi* belirli bir veritabanı için.
    > * Olay türlerinden farklı belirli bir veritabanı veya hello sunucudaki hello veritabanları hello geri kalanı için denetlenen kategorileri için tooaudit olay türleri veya kategoriler istiyorsunuz. Örneğin, yalnızca belirli bir veritabanı için denetlenen toobe gereken tablo ekler olabilir.
   > 
   > Aksi takdirde, yalnızca sunucu düzeyinde blob denetimi ve veritabanı düzeyinde hello tüm veritabanları için devre dışı bırak denetimi etkinleştirmeniz önerilir.


## <a id="subheading-2"></a>Veritabanınız için denetimi ayarlamanız
Merhaba aşağıdaki bölümde hello Azure portal kullanarak denetim hello yapılandırmasını açıklar.

1. Toohello Git [Azure portal](https://portal.azure.com).
2. Toohello Git **ayarları** hello tooaudit istediğiniz SQL veritabanı/SQL server dikey. Merhaba, **ayarları** dikey penceresinde, select **denetim ve tehdit algılama**.

    <a id="auditing-screenshot"></a>![Gezinti Bölmesi][1]
3. (Bu sunucuda tooall mevcut ve yeni oluşturulan veritabanları uygulanır) olan bir sunucu denetim ilkesi yukarı tooset tercih ederseniz, hello seçebilirsiniz **sunucu ayarlarını görüntüleyin** hello veritabanı denetim dikey penceresinde bağlantı. Daha sonra görüntülemek veya hello sunucu denetim ayarlarını değiştirin.

    ![Gezinti Bölmesi][2]
4. Tooenable hello veritabanı düzeyi (toplama tooor) sunucu düzeyinde denetimi yerine, blob denetimi için tercih ederseniz **denetim**seçin **ON**ve **türü denetimi** , seçin **Blob**.

    Sunucu blob denetimi etkinse hello veritabanı yapılandırılmış denetim hello sunucu blob denetim yan yana yer alır.  

    ![Gezinti Bölmesi][3]
5. tooopen hello **denetim günlüklerini depolama** dikey penceresinde, select **depolama ayrıntıları**. Burada günlükleri kaydedilecek ve hangi hello sonra eski günlükleri silinecek hello saklama dönemi ardından hello Azure depolama hesabı seçin. Daha sonra, **Tamam**'a tıklayın. 
   >[!TIP] 
   >Merhaba Denetim raporları şablonları, kullanım dışı en tooget hello hello denetlenen tüm veritabanları için aynı depolama hesabı. 

    <a id="storage-screenshot"></a>![Gezinti Bölmesi][4]
6. Toocustomize denetlenen hello olayları istiyorsanız, bunu PowerShell ile yapmak veya REST API hello. Daha fazla ayrıntı için bkz: Merhaba [Otomasyon (PowerShell/REST API'si)](#subheading-7) bölümü.
7. Denetim ayarlarını yapılandırdıktan sonra yeni tehdit algılama özelliğini hello açın ve e-postaları tooreceive güvenlik uyarılarını yapılandırın. Tehdit algılama kullandığınızda, olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini öngörülü uyarılar alırsınız. Daha fazla ayrıntı için bkz: [tehdit algılama ile çalışmaya başlama](sql-database-threat-detection-get-started.md).
8. **Kaydet** düğmesine tıklayın.





## <a id="subheading-3"></a>Denetim günlüklerini ve raporları analiz eder.
Denetim günlüklerini hello Kurulum sırasında seçtiğiniz Azure depolama hesabında toplanır. Gibi bir araç kullanarak denetim günlüklerini keşfedebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/).

BLOB denetim günlüklerini adlı bir kapsayıcı içindeki blob dosya koleksiyonu olarak kaydedilir **sqldbauditlogs**.

Merhaba hello hiyerarşisini başlangıç blob denetim günlüklerini depolama klasörü, blob adlandırma kuralları ve günlük biçimi hakkında daha fazla ayrıntı için bkz: [Blob denetim günlük biçimi başvurusu (.docx dosya indirme)](https://go.microsoft.com/fwlink/?linkid=829599).

Günlükleri denetlemeyi tooview blob kullanabileceğiniz birkaç yöntem vardır:

* Kullanım hello [Azure portal](https://portal.azure.com).  Açık hello ilgili veritabanı. Merhaba veritabanının AT hello üst **denetim ve tehdit algılama** dikey penceresinde tıklatın **denetim günlüklerini görüntüle**.

    ![Gezinti Bölmesi][7]

    Bir **denetim kayıtları** içinden olmanız mümkün tooview hello günlükler dikey penceresi açılır.

    - Belirli tarihleri tıklatarak görüntüleyebileceğiniz **filtre** hello hello üstündeki **denetim kayıtları** dikey.
    - Bir sunucu İlkesi veya veritabanı ilke denetimi tarafından oluşturulan denetim kayıtları arasında geçiş yapabilirsiniz.

       ![Gezinti Bölmesi][8]

* Merhaba sistem işlevi kullanın **sys.fn_get_audit_file** (T-SQL) tooreturn hello denetim günlüğü verilerini tablo biçiminde. Bu işlev kullanma hakkında daha fazla bilgi için bkz: Merhaba [sys.fn_get_audit_file belgelerine](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Kullanım **denetim dosyaları birleştirme** SQL Server Management Studio'da (SSMS 17 ile başlayarak):  
    1. Merhaba SSMS menüsünden seçin **dosya** > **açık** > **denetim dosyaları birleştirme**.

        ![Gezinti Bölmesi][9]
    2. Merhaba **denetim dosyaları Ekle** iletişim kutusu açılır. Merhaba birini seçin **Ekle** toomerge denetim bir yerel dosyaları olup olmadığını seçmek için seçenekler disk veya bunları Azure depolama alanından içeri aktarın (, gerekli tooprovide Azure Storage ayrıntılarını ve hesap anahtarı olacaktır).

    3. Tüm dosyaları toomerge eklendikten sonra tıklatın **Tamam** toocomplete hello birleştirme işlemi.

    4. Merhaba birleştirilmiş dosya burada görüntüleyebilir ve, isteğe bağlı olarak verme tooan XEL'e veya CSV dosyası veya tooa tablo hem analiz SSMS açılır.

* Kullanım hello [eşitleme uygulama](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , oluşturduk. Azure üzerinde çalışır ve Operations Management Suite (OMS) günlük analizi Genel API toopush SQL denetim günlüklerini OMS kullanır. Merhaba eşitleme uygulaması hello OMS günlük analizi Pano tüketimi için OMS günlük analizi SQL denetim günlüklerini iter. 

* Power BI kullanın. Görüntülemek ve denetim günlüğü verilerini Power bı'da analiz edin. Daha fazla bilgi edinmek [Power BI ve erişim indirilebilir bir şablon](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Günlük dosyaları gibi bir araç kullanarak veya hello Portalı aracılığıyla Azure depolama blob kapsayıcısını indirin [Azure Storage Gezgini](http://storageexplorer.com/).
    * Bir günlük dosyası yerel olarak indirdikten sonra hello dosya tooopen çift tıklayarak görüntülemek ve SSMS içinde hello günlüklerini analiz edin.
    * Ayrıca, Azure Storage Gezgini ile aynı anda birden çok dosya indirebilirsiniz. Özel bir alt klasör (örneğin, belirli bir tarihteki tüm günlük dosyalarını içeren bir alt) sağ tıklayın ve **Farklı Kaydet** yerel bir klasörde toosave.

* Ek yöntemleri:
   * Pek çok dosya (veya hello önceki öğesi bu listede açıklandığı gibi tüm bir gün için günlük dosyalarını içeren bir alt klasörü) indirdikten sonra bunları yerel olarak daha önce açıklanan hello SSMS birleştirme Denetim dosyalarını yönergelerde açıklandığı gibi birleştirebilirsiniz.

   * Görünüm blob denetimi programlı olarak günlüğe kaydeder:

     * Kullanım hello [genişletilmiş olaylar okuyucu](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# Kitaplığı.
     * [Sorgu genişletilmiş olaylar dosyaları](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) PowerShell kullanarak.




## <a id="subheading-5"></a>Üretim uygulamaları
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Coğrafi olarak çoğaltılmış veritabanları denetleme</a>
Coğrafi olarak çoğaltılmış veritabanları kullanırken hello birincil veritabanı, hello ikincil veritabanı ya da her ikisini de hello denetim türüne bağlı olarak denetim yukarı olası tooset olur.

(Blob denetimi açmak veya kapatmak denetim ayarları yalnızca hello birincil veritabanından açılabilir olduğunu unutmayın) bu yönergeleri izleyin:

* **Birincil veritabanı**. BLOB, hello sunucusunda veya hello veritabanının kendisi, Denetim hello açıklandığı gibi açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.
* **İkincil veritabanı**. Hello açıklandığı gibi hello birincil veritabanında BLOB denetim açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü. 
   * BLOB denetimi üzerinde hello etkinleştirilmelidir *birincil veritabanının kendisi*, hello sunucusu değil.
   * BLOB denetimi hello birincil veritabanında etkinleştirildikten sonra aynı zamanda hello ikincil veritabanı üzerinde etkin hale.

     >[!IMPORTANT]
     >Varsayılan olarak, hello ikincil veritabanının hello depolama ayarlarını hello birincil veritabanının aynı toothose çapraz bölge trafiği neden olur. Bu blob hello ikincil sunucuda denetim ve yerel depolama hello ikincil sunucu depolama ayarlarında yapılandırma etkinleştirerek önleyebilirsiniz. Bu hello ikincil veritabanı ve denetim günlüklerini toolocal depolama alanı kaydetme her veritabanı sonucunda hello depolama konumu geçersiz kılar.  
<br>

### <a id="subheading-6">Depolama anahtarını yeniden üretme</a>
Üretimde, depolama alanınızın düzenli aralıklarla anahtarları büyük olasılıkla toorefresh demektir. Anahtarlarınızı yenilerken tooresave hello Denetim İlkesi gerekir. Merhaba işlem aşağıdaki gibidir:

1. Açık hello **depolama ayrıntıları** dikey. Merhaba, **depolama erişim tuşu** kutusunda **ikincil**, tıklatıp **Tamam**. Ardından **kaydetmek** yapılandırma dikey penceresi denetim hello hello üstünde.

    ![Gezinti Bölmesi][5]
2. Toohello depolama yapılandırma dikey gidin ve hello birincil erişim anahtarını yeniden oluşturma.

    ![Gezinti Bölmesi][6]
3. Yapılandırma dikey penceresi denetim toohello geri dönün, geçiş hello depolama erişim ikincil tooprimary anahtarından ve ardından **Tamam**. Ardından **kaydetmek** yapılandırma dikey penceresi denetim hello hello üstünde.
4. Toohello depolama yapılandırma dikey ve üretme hello ikincil erişim tuşu (Merhaba sonraki anahtarın yenileme döngüsü için hazırlık) geri dönün.

## <a id="subheading-7"></a>Otomasyon (PowerShell/REST API)
Otomasyon araçları aşağıdaki hello kullanarak Azure SQL veritabanı'nda denetim da yapılandırabilirsiniz:

* **PowerShell cmdlet'leri**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Kullanım AzureRMSqlServerAuditingPolicy][107]

   Bir komut dosyası örneği için bkz: [denetim ve tehdit algılama PowerShell kullanarak yapılandırmanız](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **REST API - Blob denetimi**:

   * [Denetim İlkesi veritabanı Blob güncelle](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [Oluşturma veya güncelleştirme sunucusu Blob Denetim İlkesi](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [Denetim İlkesi veritabanı Blob alma](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [Denetim İlkesi Sunucu Blob alma](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [İşlem sonucu denetim sunucu Blob alma](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
