---
title: "aaaUse Azure portal toocreate SQL veritabanı uyarıları | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında hangi bildirimleri ya da Otomasyon tetikleyebilir hello Azure portal toocreate SQL veritabanı uyarıları kullanın."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Azure SQL veritabanı ve veri ambarı için Azure portal toocreate uyarıları kullanın

## <a name="overview"></a>Genel Bakış
Bu makalede nasıl tooset kullanarak Azure SQL veritabanı ve veri ambarı uyarıları hello Azure portal gösterilmektedir. Bu makalede ayrıca uyarı dönemleri ayarlamak için en iyi yöntemler sağlar.    

İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.

* **Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler. Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.    
* **Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir sayıda olayları oluşur.

Tetikler olduğunda bir uyarı toodo hello aşağıdaki yapılandırabilirsiniz:

* e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder
* e-posta, belirttiğiniz tooadditional e-postalar gönderin.
* bir Web kancası çağırın

Yapılandırma ve uyarı kuralları kullanma hakkında bilgi edinin

* [Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [komut satırı arabirimi (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [Azure monitör REST API'si](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Ölçüm hello Azure portal ile bir uyarı kuralı oluşturma
1. Merhaba, [portal](https://portal.azure.com/), izleme ilgilenen hello kaynak bulup seçin.
2. Bu adım, SQL DB ve SQL DW esnek havuzları için farklıdır: 

   - **SQL DB yalnız & CA esnek havuzları**: seçin **uyarıları** veya **uyarı kuralları** hello izleme bölümü altında. Merhaba metin ve simge farklı kaynaklar için biraz değişebilir.  
   
     ![İzleme](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **YALNIZCA SQL DW**: seçin **izleme** hello ortak görevler bölümü altında. Merhaba tıklatın **DWU kullanım** grafik.

     ![ORTAK GÖREVLER](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Select hello **uyarı Ekle** komut ve hello alanları doldurun.
   
    ![Uyarı ekleme](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. **Ad** , uyarı kuralı ve seçin bir **açıklama**, bildirim e-postalarda da gösterir.
5. Select hello **ölçüm** toomonitor istediğiniz sonra seçin bir **koşulu** ve **eşik** hello ölçüm için değer. Ayrıca hello Seçtiğiniz **süresi** ölçüm hello süresini kural hello uyarı Tetikleyicileri önce yerine getirilmesi gereken. Dolayısıyla örneğin Hello CPU % 80 5 dakika boyunca sürekli olarak yukarıdaki kaldığında hello süresi "PT5M" kullanıyorsanız ve uyarıyı % 80 CPU arar hello uyarı tetikler. Merhaba ilk tetikleyici oluşur sonra hello CPU 5 dakika boyunca % 80'altında kaldığında oluşan yeniden tetikler. Merhaba CPU ölçüm, 1 dakikada oluşur.   
6. Denetleme **e-posta sahipleri...**  e-posta ile yöneticileri ve ortak Yöneticiler toobe istiyorsanız, ne zaman uyarı ateşlenir hello.
7. Ek e-postaları tooreceive hello olduğunda bir bildirim istiyorsanız uyarı ateşlenir, hello eklemek **ek yönetici email(s)** alan. Birden çok e-postaları - noktalı virgülle ayırın  *email@contoso.com;email2@contoso.com*
8. Merhaba geçerli bir URI koymak **Web kancası** alan adlı istiyorsanız, ne zaman hello uyarı etkinleşir.
9. Seçin **Tamam** zaman Bitti'yi toocreate hello uyarı.   

Birkaç dakika içinde hello uyarı etkin ve daha önce açıklandığı şekilde tetikler.

## <a name="managing-your-alerts"></a>Uyarılarınızı yönetme
Bir uyarı oluşturduktan sonra bunu seçebilirsiniz ve:

* Önceki gün Hello ölçüm eşiği ve hello hello gerçek değerleri gösteren bir grafik görüntüleyin.
* Düzenleyin veya silin.
* **Devre dışı** veya **etkinleştirmek** onu, tootemporarily durdurma veya bu uyarı için bildirimleri almaya devam etmek istiyorsanız.


## <a name="sql-database-alert-values"></a>SQL veritabanı uyarı değerleri

| Kaynak Türü | Ölçüm adı | Kolay ad | Toplama türü | En az uyarı zaman penceresi|
| --- | --- | --- | --- | --- |
| SQL veritabanı | cpu_percent | CPU yüzdesi | Ortalama | 5 dakika |
| SQL veritabanı | physical_data_read_percent | Veri G/Ç yüzdesi | Ortalama | 5 dakika |
| SQL veritabanı | log_write_percent | Günlük g/ç yüzdesi | Ortalama | 5 dakika |
| SQL veritabanı | dtu_consumption_percent | DTU yüzdesi | Ortalama | 5 dakika |
| SQL veritabanı | Depolama | Toplam veritabanı boyutu | Maksimum | 30 dakika |
| SQL veritabanı | connection_successful | Başarılı bağlantıları | Toplam | 10 dakika |
| SQL veritabanı | connection_failed | Başarısız bağlantı sayısı | Toplam | 10 dakika |
| SQL veritabanı | blocked_by_firewall | Güvenlik Duvarı tarafından engellendi | Toplam | 10 dakika |
| SQL veritabanı | Kilitlenme | Kilitlenmeleri | Toplam | 10 dakika |
| SQL veritabanı | storage_percent | Veri boyutu yüzdesi | Maksimum | 30 dakika |
| SQL veritabanı | xtp_storage_percent | Bellek içi OLTP depolama percent(Preview) | Ortalama | 5 dakika |
| SQL veritabanı | workers_percent | Çalışanlar yüzdesi | Ortalama | 5 dakika |
| SQL veritabanı | sessions_percent | Oturumları yüzde | Ortalama | 5 dakika |
| SQL veritabanı | dtu_limit | DTU sınırı | Ortalama | 5 dakika |
| SQL veritabanı | dtu_used | Kullanılan DTU | Ortalama | 5 dakika |
||||||
| Esnek havuz | cpu_percent | CPU yüzdesi | Ortalama | 10 dakika |
| Esnek havuz | physical_data_read_percent | Veri G/Ç yüzdesi | Ortalama | 10 dakika |
| Esnek havuz | log_write_percent | Günlük g/ç yüzdesi | Ortalama | 10 dakika |
| Esnek havuz | dtu_consumption_percent | DTU yüzdesi | Ortalama | 10 dakika |
| Esnek havuz | storage_percent | Depolama yüzdesi | Ortalama | 10 dakika |
| Esnek havuz | workers_percent | Çalışanlar yüzdesi | Ortalama | 10 dakika |
| Esnek havuz | eDTU_limit | eDTU sınırı | Ortalama | 10 dakika |
| Esnek havuz | storage_limit | Depolama sınırı | Ortalama | 10 dakika |
| Esnek havuz | eDTU_used | kullanılan eDTU | Ortalama | 10 dakika |
| Esnek havuz | storage_used | Kullanılan depolama | Ortalama | 10 dakika |
||||||               
| SQL veri ambarı | cpu_percent | CPU yüzdesi | Ortalama | 10 dakika |
| SQL veri ambarı | physical_data_read_percent | Veri G/Ç yüzdesi | Ortalama | 10 dakika |
| SQL veri ambarı | Depolama | Toplam veritabanı boyutu | Maksimum | 10 dakika |
| SQL veri ambarı | connection_successful | Başarılı bağlantıları | Toplam | 10 dakika |
| SQL veri ambarı | connection_failed | Başarısız bağlantı sayısı | Toplam | 10 dakika |
| SQL veri ambarı | blocked_by_firewall | Güvenlik Duvarı tarafından engellendi | Toplam | 10 dakika |
| SQL veri ambarı | service_level_objective | Hizmet düzeyi hedefi hello veritabanı | Toplam | 10 dakika |
| SQL veri ambarı | dwu_limit | dwu sınırı | Maksimum | 10 dakika |
| SQL veri ambarı | dwu_consumption_percent | DWU yüzdesi | Ortalama | 10 dakika |
| SQL veri ambarı | dwu_used | Kullanılan DWU | Ortalama | 10 dakika |
||||||


## <a name="next-steps"></a>Sonraki adımlar
* [Azure izleme genel bir bakış elde](../monitoring-and-diagnostics/monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.
* Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Alma bir [tanılama günlükleri'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) hizmetinizde ayrıntılı yüksek sıklıkta ölçümleri toplamak ve.
* Alma bir [ölçümleri toplama genel bakış](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
