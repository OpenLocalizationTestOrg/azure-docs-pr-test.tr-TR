---
title: "Azure SQL veritabanı denetimi ile çalışmaya başlama | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a>SQL veritabanı denetimini kullanmaya başlayın
Azure SQL veritabanı denetimi veritabanı olaylarını ve Azure depolama hesabınızdaki bunları Denetim günlüğüne yazar izler. Ayrıca denetleme:

* Yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve iş endişeleri veya güvenlik ihlalleri hakkında daha fazla bilgi kavramanıza yardımcı olur.

* Etkinleştirir ve uyumluluk garanti etmez ancak Uyumluluk standartlara uyulması kolaylaştırır. Bu destek standartları uyumluluğu Azure hakkında daha fazla bilgi programlar için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Genel Bakış denetim azure SQL veritabanı
SQL veritabanı için denetimi kullanabilirsiniz:


* **Korumak** seçili olayların bir denetim izi. Denetlenecek veritabanı eylemleri kategorilerini tanımlayabilirsiniz.
* **Rapor** veritabanı etkinlik. Etkinlik ve olay Raporlama ile hızlı bir şekilde başlamak için önceden yapılandırılmış raporları ve panoyu kullanabilirsiniz.
* **Analiz** raporlar. Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.

Farklı türlerde olay kategorisi için Denetim açıklandığı şekilde yapılandırabilirsiniz [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.

Denetim günlükleri, Azure aboneliğinizde Azure Blob depolama alanına yazılır.


## <a id="subheading-8"></a>Sunucu düzeyinde ve veritabanı düzeyi denetim ilkesi tanımlayın

Bir denetim ilkesi, belirli bir veritabanı veya varsayılan sunucu ilkesi olarak tanımlanabilir:

* Sunucudaki tüm mevcut ve yeni oluşturulan veritabanları için bir sunucu ilkesi uygulanır.

* Varsa *sunucu blob denetimi etkin*, onu *veritabanı için her zaman geçerli* (diğer bir deyişle, veritabanı denetlenmez), bağımsız olarak veritabanı denetim ayarları.

* Veritabanı üzerinde BLOB denetiminin etkinleştirilmesi, sunucu üzerinde etkinleştirmenin yanı sıra olur *değil* geçersiz kılabilir veya sunucu blob denetimi ayarlarından herhangi birini değiştirin. Her iki denetimleri yan yana yer alır. Diğer bir deyişle, veritabanı (kez sunucu İlkesi ve bir kez tarafından veritabanı İlkesi) iki kez paralel olarak denetlenecektir.

   > [!NOTE]
   > Sunucu blob denetlenmesi ve veritabanı blob birlikte denetimi sürece etkinleştirme kaçınmanız gerekir:
    > * Farklı bir kullanmak istediğiniz *depolama hesabı* veya *saklama dönemi* belirli bir veritabanı için.
    > * Olay türlerini veya belirli bir veritabanı için olay türlerinden farklı kategorileri veya veritabanlarını sunucuda geri kalanı için denetlenen kategorileri denetlemek istediğiniz. Örneğin, yalnızca belirli bir veritabanı için denetlenmesi gereken tablo ekler olabilir.
   > 
   > Aksi takdirde, yalnızca sunucu düzeyinde blob denetlemeyi etkinleştirme ve devre dışı tüm veritabanları için veritabanı düzeyinde denetimi bırakın önerilir.


## <a id="subheading-2"></a>Veritabanınız için denetimi ayarlamanız
Aşağıdaki bölümde denetim Azure Portalı'nı kullanarak yapılandırmayı açıklar.

1. [Azure Portal](https://portal.azure.com) gidin.
2. Git **ayarları** denetlemek istediğiniz SQL veritabanı/SQL server'ın dikey. İçinde **ayarları** dikey penceresinde, select **denetim ve tehdit algılama**.

    <a id="auditing-screenshot"></a>![Gezinti Bölmesi][1]
3. (Bu sunucudaki tüm mevcut ve yeni oluşturulan veritabanları için uygulanır) bir sunucu denetim ilkesini ayarlamak tercih ederseniz, seçebileceğiniz **sunucu ayarlarını görüntüleyin** veritabanı denetim dikey penceresinde bağlantı. Daha sonra görüntülemek veya sunucunun denetim ayarları değiştirin.

    ![Gezinti Bölmesi][2]
4. İçin veritabanı düzeyinde (ek olarak veya sunucu düzeyinde denetimi yerine), blob denetimi etkinleştirmeyi tercih ediyorsanız **denetim**seçin **ON**ve **türü denetimi**, seçin **Blob**.

    Sunucu blob denetimi etkinse, veritabanı yapılandırılmış denetim yan yana sunucu blob denetim yer alır.  

    ![Gezinti Bölmesi][3]
5. Açmak için **denetim günlüklerini depolama** dikey penceresinde, select **depolama ayrıntıları**. Burada günlükleri kaydedilecek ve sonra eski günlükleri silinecek saklama dönemi, ardından Azure depolama hesabı seçin. Daha sonra, **Tamam**'a tıklayın. 
   >[!TIP] 
   >En iyi denetim raporları şablonları almak için denetlenen tüm veritabanları için aynı depolama hesabı kullanın. 

    <a id="storage-screenshot"></a>![Gezinti Bölmesi][4]
6. Denetlenen olayları özelleştirmek istiyorsanız, PowerShell veya REST API bunu yapabilirsiniz. Daha fazla ayrıntı için bkz: [Otomasyon (PowerShell/REST API'si)](#subheading-7) bölümü.
7. Denetim ayarlarını yapılandırdıktan sonra yeni tehdit algılama özelliğini açmak ve güvenlik uyarıları almak için e-postaları yapılandırın. Tehdit algılama kullandığınızda, olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini öngörülü uyarılar alırsınız. Daha fazla ayrıntı için bkz: [tehdit algılama ile çalışmaya başlama](sql-database-threat-detection-get-started.md).
8. **Kaydet** düğmesine tıklayın.





## <a id="subheading-3"></a>Denetim günlüklerini ve raporları analiz eder.
Denetim günlükleri, Kurulum sırasında seçtiğiniz Azure depolama hesabında toplanır. Gibi bir araç kullanarak denetim günlüklerini keşfedebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/).

BLOB denetim günlüklerini adlı bir kapsayıcı içindeki blob dosya koleksiyonu olarak kaydedilir **sqldbauditlogs**.

Hiyerarşi blob denetim günlüklerini depolama klasörü, blob adlandırma kuralları ve günlük biçimi hakkında daha fazla ayrıntı için bkz: [Blob denetim günlük biçimi başvurusu (.docx dosya indirme)](https://go.microsoft.com/fwlink/?linkid=829599).

Blob denetim günlüklerini görüntülemek için kullanabileceğiniz birkaç yöntem vardır:

* Kullanım [Azure portal](https://portal.azure.com).  İlgili veritabanını açın. Veritabanının üstündeki **denetim ve tehdit algılama** dikey penceresinde tıklatın **denetim günlüklerini görüntüle**.

    ![Gezinti Bölmesi][7]

    Bir **denetim kayıtları** dikey penceresi açılır ve kendisinden, günlükleri görüntüleyebilirsiniz.

    - Belirli tarihleri tıklatarak görüntüleyebileceğiniz **filtre** en üstündeki **denetim kayıtları** dikey.
    - Bir sunucu İlkesi veya veritabanı ilke denetimi tarafından oluşturulan denetim kayıtları arasında geçiş yapabilirsiniz.

       ![Gezinti Bölmesi][8]

* Bir sistem işlevi kullanın **sys.fn_get_audit_file** (Denetim günlüğü verilerini tablo biçiminde döndürmek için T-SQL). Bu işlev kullanma hakkında daha fazla bilgi için bkz: [sys.fn_get_audit_file belgelerine](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Kullanım **denetim dosyaları birleştirme** SQL Server Management Studio'da (SSMS 17 ile başlayarak):  
    1. SSMS menüsünden seçin **dosya** > **açık** > **denetim dosyaları birleştirme**.

        ![Gezinti Bölmesi][9]
    2. **Denetim dosyaları Ekle** iletişim kutusu açılır. Aşağıdakilerden birini seçin **Ekle** Seçenekleri denetim dosyalarını yerel bir sürücüden birleştirme ya da Azure (size gerekecek Azure Storage ayrıntıları ve hesap anahtarı sağlamak) depolama biriminden almak isteyip istemediğinizi seçin.

    3. Birleştirme için tüm dosyaları ekledikten sonra tıklatın **Tamam** birleştirme işlemini tamamlamak için.

    4. Burada, görüntülemek ve analiz edin, yanı sıra bir XEL'e ya da CSV dosyası veya tablo dışa SSMS birleştirilmiş dosya açılır.

* Kullanım [eşitleme uygulama](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , oluşturduk. Azure üzerinde çalışır ve Operations Management Suite (OMS) SQL denetim günlüklerini OMS göndermek için günlük analizi genel API'leri kullanır. Eşitleme uygulamanın OMS günlük analizi Pano tüketimi için OMS günlük analizi SQL denetim günlüklerini iter. 

* Power BI kullanın. Görüntülemek ve denetim günlüğü verilerini Power bı'da analiz edin. Daha fazla bilgi edinmek [Power BI ve erişim indirilebilir bir şablon](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Günlük dosyaları gibi bir araç kullanarak veya Portalı aracılığıyla Azure depolama blob kapsayıcısını indirin [Azure Storage Gezgini](http://storageexplorer.com/).
    * Bir günlük dosyası yerel olarak indirdikten sonra açın, görüntülemek ve SSMS'ndeki günlükleri çözümlemek için dosyayı çift tıklayabilirsiniz.
    * Ayrıca, Azure Storage Gezgini ile aynı anda birden çok dosya indirebilirsiniz. Özel bir alt klasör (örneğin, belirli bir tarihteki tüm günlük dosyalarını içeren bir alt) sağ tıklayın ve **Farklı Kaydet** içinde yerel bir klasöre kaydeder.

* Ek yöntemleri:
   * Pek çok dosya (veya önceki öğeyi bu listede açıklandığı gibi tüm bir gün için günlük dosyalarını içeren bir alt klasörü) indirdikten sonra bunları yerel olarak daha önce açıklanan SSMS birleştirme Denetim dosyalarını yönergelerde açıklandığı gibi birleştirebilirsiniz.

   * Görünüm blob denetimi programlı olarak günlüğe kaydeder:

     * Kullanım [genişletilmiş olaylar okuyucu](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# Kitaplığı.
     * [Sorgu genişletilmiş olaylar dosyaları](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) PowerShell kullanarak.




## <a id="subheading-5"></a>Üretim uygulamaları
<!--The description in this section refers to preceding screen captures.-->

### <a id="subheading-6">Coğrafi olarak çoğaltılmış veritabanları denetleme</a>
Coğrafi olarak çoğaltılmış veritabanları kullandığınızda, birincil veritabanı, ikincil veritabanı ya da her ikisini de denetim türüne bağlı olarak denetimini ayarlamak mümkündür.

(Blob denetimi açmak veya kapatmak denetim ayarları yalnızca birincil veritabanından açılabilir olduğunu unutmayın) bu yönergeleri izleyin:

* **Birincil veritabanı**. BLOB, sunucuda veya veritabanının kendisi, Denetim açıklandığı gibi açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü.
* **İkincil veritabanı**. Bölümünde açıklandığı gibi birincil veritabanında BLOB denetim açıldıktan [veritabanınız için denetimi ayarlamanız](#subheading-2) bölümü. 
   * Üzerinde BLOB denetimi etkinleştirilmelidir *birincil veritabanının kendisi*, sunucu değil.
   * BLOB denetimi birincil veritabanında etkinleştirildikten sonra aynı zamanda ikincil veritabanı etkin hale.

     >[!IMPORTANT]
     >Varsayılan olarak, ikincil veritabanı için depolama ayarlarını çapraz bölge trafiği neden bu birincil veritabanının aynı olacaktır. Bu ikincil sunucuda blob denetimi ve yerel depolama için ikincil sunucu depolama ayarlarında yapılandırma etkinleştirerek önleyebilirsiniz. Bu ikincil veritabanı ve denetim günlüklerinin yerel depolama alanına kaydediliyor her veritabanı sonucunda için depolama konumu geçersiz kılar.  
<br>

### <a id="subheading-6">Depolama anahtarını yeniden üretme</a>
Üretimde büyük bir olasılıkla depolama anahtarlarınızı düzenli aralıklarla yenileyin. Anahtarlarınızı yenilerken denetim ilkesi yeniden kaydetmeniz gerekir. İşlem aşağıdaki gibidir:

1. Açık **depolama ayrıntıları** dikey. İçinde **depolama erişim tuşu** kutusunda **ikincil**, tıklatıp **Tamam**. Ardından **kaydetmek** denetim yapılandırma dikey pencerenin üstündeki.

    ![Gezinti Bölmesi][5]
2. Depolama yapılandırma dikey penceresine gidin ve birincil erişim anahtarını yeniden oluşturma.

    ![Gezinti Bölmesi][6]
3. Birincil ikincil depolama erişim anahtarı yeniden denetim yapılandırma dikey penceresine, anahtar ve ardından Git **Tamam**. Ardından **kaydetmek** denetim yapılandırma dikey pencerenin üstündeki.
4. Depolama yapılandırma dikey penceresine geri dönün ve (için Hazırlanmakta sonraki anahtarın yenileme döngüsü) ikincil erişim anahtarını yeniden oluşturma.

## <a id="subheading-7"></a>Otomasyon (PowerShell/REST API)
Azure SQL veritabanı'nda aşağıdaki Otomasyon araçları kullanarak denetim da yapılandırabilirsiniz:

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
