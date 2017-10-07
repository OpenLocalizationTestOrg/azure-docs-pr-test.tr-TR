---
title: "aaaAdd Azure günlük analizi yönetim çözümleri | Microsoft Docs"
description: "Operations Management Suite (OMS) / Log Analytics yönetimi çözümleri belirli sorunu etrafına özetlenebilir ölçümleri sağlayan mantığı, Görselleştirme ve veri alım kurallar topluluğu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Azure günlük analizi yönetim çözümleri tooyour çalışma Ekle

Günlük analizi yönetim çözümleri koleksiyonu olan **mantığı**, **görselleştirme**, ve **veri alım kuralları** belirli bir özetlenebilir ölçümleri sağlar sorun alanı. Bu makalede, günlük analizi tarafından desteklenen yönetim çözümleri listeler ve nasıl tooadd ekleme ve kaldırma kullanarak bir çalışma alanı için Azure portal hello gösterir. Merhaba Çözümleri Galerisi kullanarak hello OMS portalında çözümleri de ekleyebilirsiniz.

Yönetim çözümleri için daha ayrıntılı Öngörüler izin ver:

* Araştırmak ve işletim sorunları daha hızlı çözülmesine yardımcı olur
* Toplamak ve makine verileri çeşitli türlerde ilişkilendirmek
* Merhaba çözüm sunan etkinlikleri ile öngörülü Yardım.

> [!NOTE]
> Günlük analizi tooinstall bir yönetim çözümü tooenable gerekmeyen şekilde günlük arama işlevini içerir. Ancak, veri görselleştirmeleri, önerilen arar ve Öngörüler yönetim çözümleri tooyour çalışma ekleyerek alırsınız.

Bu makalede'ı kullanarak yönetim çözümleri tooa hello Azure portal Market kullanarak çalışma alanı ekleyin. Bir çözüm ekledikten sonra veriler altyapınızı hello sunuculardan toplanacak ve toohello OMS hizmetine gönderilir. OMS hizmetine genellikle birkaç dakika tooan saat sürer hello tarafından işleniyor. Merhaba hizmet hello veri işledikten sonra OMS içinde görüntüleyebilirsiniz.

Artık gerekli olmadığında bir yönetim çözümü kolayca kaldırabilirsiniz. Bir yönetim çözümü kaldırdığınızda, kendi veri tooOMS gönderilmez. Ücretsiz fiyatlandırma katmanı hello üzerinde varsa, bir çözüm kaldırma kullanıldığında, veri veri günlük kotası altında olmanıza yardımcı hello miktarını azaltır.

## <a name="view-available-management-solutions"></a>Görünüm kullanılabilir yönetim çözümleri

Hello Azure Market hello listesini içeren [yönetim çözümleri için günlük analizi](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Merhaba tıklayarak yönetim çözümleri Azure Marketi'nden yükleyebilirsiniz **Şimdi Al** her çözüm hello sonundaki bağlantı.

## <a name="add-a-management-solution"></a>Bir yönetim çözümü ekleyin
1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com) Azure aboneliğinizi kullanarak.
2. Merhaba, **yeni** altında dikey **Market**seçin **izleme + Yönetim**.
3. Merhaba, **izleme + Yönetim** dikey penceresinde tıklatın **tümünü görmek**.  
    ![İzleme + yönetim dikey penceresi](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. sağ toohello **yönetim çözümleri**, tıklatın **daha fazla**.
5. Merhaba, **yönetim çözümleri** dikey penceresinde tooadd tooa çalışma istediğiniz bir yönetim çözümü seçin.  
    ![İzleme + yönetim dikey penceresi](./media/log-analytics-add-solutions/management-solutions.png)  
6. Merhaba yönetim çözümü dikey penceresinde hello yönetim çözümü hakkındaki bilgileri gözden geçirin ve ardından **oluşturma**.
7. Merhaba, *yönetim çözümü adı* dikey penceresinde hello yönetim çözümüyle tooassociate istediğiniz çalışma alanı seçin.
8. İsteğe bağlı olarak, çalışma alanı ayarları hello Azure abonelik, kaynak grubunu ve konumu için değiştirin. Ayrıca seçebilirsiniz **Otomasyon seçenekleri**. **Oluştur**'a tıklayın.  
    ![çözüm çalışma alanı](./media/log-analytics-add-solutions/solution-workspace.png)  
9. tooyour çalışma alanında, eklediğiniz hello yönetim çözümünü kullanarak toostart çok gidin**günlük analizi** > **abonelikleri** > ***çalışma alanı adı ***  >  **Genel bakış**. Yeni bir kutucuk Yönetimi çözümünüz için görüntülenir. Hello döşeme tooopen ve hello çözüm için veriler toplandıktan sonra hello çözümünü kullanarak Başlat'ı tıklatın.

## <a name="remove-a-management-solution"></a>Bir yönetim çözümünü Kaldır

1. Merhaba, [Azure portal](https://portal.azure.com), çok gidin**günlük analizi** > **abonelikleri** > ***çalışma alanı adı*** ve ardından hello ***çalışma alanı adı*** dikey penceresinde tıklatın **çözümleri**.
2. Yönetim çözümleri Hello listesinde hello çözüm tooremove istediğinizi seçin.
3. Çalışma alanınız için Hello çözüm dikey penceresinde tıklayın **silmek**.  
    ![Çözüm silme](./media/log-analytics-add-solutions/solution-delete.png)  
4. Merhaba onay iletişim kutusunda tıklatın **Evet**.

## <a name="offers-and-pricing-tiers"></a>Teklifler ve fiyatlandırma katmanları

Aşağıdaki tablonun hello hangi yönetim çözümleri tooeach Operations Management Suite teklif ait tanımlar.
Merhaba tablo aynı zamanda her yönetim çözümü için kullanılabilir katmanları fiyatlandırma hello tanımlar.
Aşağıdaki tablonun hello tüm çözümlerinde hello hello günlük analizi portalında Azure portal ve hello Çözümleri Galerisi içinde kullanılabilir.

| Yönetim çözümü                                                                       | Sunduğu                                                                     | Fiyatlandırma katmanlarına<sup>1</sup>                                                 | Notlar |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | 90 günlük veri kullanılabilir ücretsiz<br>Veri toohello ücretsiz katmanı cap edilmez |
| [AD Değerlendirmesi](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [AD Çoğaltma Durumu](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Mevcut değil tooadd Marketi'nden Azure portal /. |
| [Aracı Durumu](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Veri toohello ücretsiz katmanı cap edilmez<br> Mevcut değil tooadd Marketi'nden Azure portal /. |
| [Uyarı Yönetimi](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Mevcut değil tooadd Marketi'nden Azure portal /. |
| [Uygulama Öngörüler Bağlayıcısı (Önizleme)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Otomasyon karma çalışanı](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Otomasyon ve Denetim</li></ul>                                  | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | Günlük analizi çalışma alanı bağlı toobe tooan Otomasyon hesabı gerektirir |
| [Azure uygulama ağ geçidi analizi](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Azure ağ güvenlik grubu analizi](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Azure SQL analizi (Önizleme)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br>Başına&nbsp;düğümü&nbsp;(OMS)                                                                          | Günlük analizi çalışma alanı bağlı toobe tooan Otomasyon hesabı gerektirir|
| [Azure Web Apps Analytics](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
|[Backup](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                       | Klasik bir yedekleme kasası gerektirir.<br> Mevcut değil tooadd Marketi'nden Azure portal /. |
| [Kapasite ve performans (Önizleme)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Değişiklik İzleme](log-analytics-change-tracking.md)                                       | <ul><li>Otomasyon ve Denetim</li></ul>                                  | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | Günlük analizi çalışma alanı bağlı toobe tooan Otomasyon hesabı gerektirir |
| [Kapsayıcılar](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [BT Hizmet Yönetimi Bağlayıcısı (Önizleme)](log-analytics-itsmc-overview.md)                                              | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)     | |
| Hdınsight HBase izleme <br>(Önizleme)                                                  | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Anahtar Kasası Analizi](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Mevcut değil tooadd Marketi'nden Azure portal /. |
| [Kötü Amaçlı Yazılım Değerlendirmesi](log-analytics-malware.md)                                            | <ul><li>Güvenlik ve Uyumluluk</li></ul>                                 | Ücretsiz<br> Tek Başına<br>Başına&nbsp;düğümü&nbsp;(OMS)                                                                           | 19 Haziran 2017 sonra hello güvenlik ve uyumluluk çözümleri eklerseniz [faturalama olan düğüm başına](https://azure.microsoft.com/pricing/details/security-compliance/)ne olursa olsun, fiyatlandırma katmanı hello çalışma. Merhaba ilk 60 gün ücretsizdir.  |
| [Ağ Performansı İzleyicisi](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight and Analytics</li></ul>                                   | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | |
| [Office 365 Analytics (Önizleme)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Güvenlik ve Denetim](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Güvenlik&nbsp;ve&nbsp;uyumluluk</li></ul>                       | Ücretsiz<br> Tek Başına<br>Başına&nbsp;düğümü&nbsp;(OMS)                                                                           | Bu çözüm güvenlik olay günlüklerini toplama gerektirir<br>19 Haziran 2017 sonra hello güvenlik ve uyumluluk çözümleri eklerseniz [faturalama olan düğüm başına](https://azure.microsoft.com/pricing/details/security-compliance/)ne olursa olsun, fiyatlandırma katmanı hello çalışma. Merhaba ilk 60 gün ücretsizdir. |
| [Service Fabric Analytics (Önizleme)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Hizmet eşlemesi (Önizleme)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight and Analytics</li></ul>                      | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | Doğu ABD, Batı Avrupa ve Batı Orta ABD kullanılabilir    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight and Analytics</li></ul>                                   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                       | Klasik Site Recovery kasası gerektirir.<br> Mevcut değil tooadd Marketi'nden Azure portal /. |
| [SQL Değerlendirmesi](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| Hizmetin kapalı olduğu saatlerde Sanal Makineleri Başlatma/Durdurma<br>(Önizleme)                                              | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | Günlük analizi çalışma alanı bağlı toobe tooan Otomasyon hesabı gerektirir |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Mevcut değil tooadd Marketi'nden Azure portal /. |
| [System Center Operations Manager değerlendirmesi (Önizleme)](log-analytics-scom-assessment.md)  | <ul><li>Insight and Analytics</li><li>Log Analytics</li></ul>        | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Güncelleştirme yönetimi](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Otomasyon ve Denetim</li></ul>                                  | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | Günlük analizi çalışma alanı bağlı toobe tooan Otomasyon hesabı gerektirir |
| [Güncelleştirme uyumluluğu (Önizleme)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Ücret ödemeden verilerin veya düğümler<br>Veri toohello ücretsiz katmanı cap edilmez.<br> Mevcut değil tooadd Marketi'nden Azure portal /. |
| [Yükseltme Hazırlığı](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | Ücret ödemeden verilerin veya düğümler<br>Veri toohello ücretsiz katmanı cap edilmez.<br> Mevcut değil tooadd Marketi'nden Azure portal /. |
| [VMware izleme (Önizleme)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Standart<br> Premium&nbsp;(OMS)<br> Başına&nbsp;GB&nbsp;(tek başına)<br> Başına&nbsp;düğümü&nbsp;(OMS)   | |
| [Kablo verileri 2.0 (Önizleme)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)                                                                         | Doğu ABD, Batı Avrupa ve Batı Orta ABD kullanılabilir |

<sup>1</sup> hello *standart* ve *Premium (OMS)* fiyatlandırma katmanlarına bulunan ve yalnızca kendi günlük analizi çalışma alanı önceki tooSeptember 21, 2016 oluşturan müşteriler için.

### <a name="community-provided-management-solutions"></a>Yönetim çözümleri sağlanan topluluk

Sağlanan topluluk çözümleri hello kullanılabilir [Azure Şablon Galerisi](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) ve hello yazarın doğrudan.

| Yönetim çözümü               | Sunduğu                                                                     | Fiyatlandırma katmanları                         | Notlar |
| ---                               | ---                                                                       | ---                                   | ---   |
| Tüm sağlanan topluluk çözümleri  | <ul><li>Insight&nbsp;ve&nbsp;analizi</li><li>Log Analytics</li></ul>   | Ücretsiz<br> Başına&nbsp;düğümü&nbsp;(OMS)     |   Günlük analizi çalışma alanı bağlı toobe tooan Otomasyon hesabı gerektirir |




## <a name="data-collection-details"></a>Veri toplama ayrıntıları
Merhaba aşağıdaki tablolarda veri toplama yöntemleri ve diğer ayrıntılar için günlük analizi yönetim çözümleri ve veri kaynakları verileri nasıl toplanır hakkında gösterilmektedir. Merhaba tabloları çok eşitlemek çözümü teklifleri tarafından ayrılır[fiyatlandırma katmanlarına abonelik](https://go.microsoft.com/fwlink/?linkid=827926). Merhaba etkinlik günlüğü analiz çözümü fiyatlandırma katmanlarına ücretsiz kullanılabilir tooall ' dir.

Günlük analizi Windows Aracısı hello ve System Center Operations Manager aracısı olan temelde aynı hello. Merhaba Windows aracısı içeren ek işlevsellik tooallow bu tooconnect toohello OMS çalışma ve bir proxy üzerinden rota. Bir Operations Manager Aracısı kullanırsanız, bir OMS Aracısı toocommunicate OMS ile olarak hedeflenen gerekir. Bu tabloda Operations Manager aracıları bağlı tooOperations Yöneticisi OMS aracıları olan. Bkz: [Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md) , var olan Operations Manager ortamı tooOMS bağlanma hakkında bilgi için.

> [!NOTE]
> Merhaba türü kullandığınız Aracısı'nın nasıl veri tooOMS, aşağıdaki koşullar hello ile gönderilen belirler:
> - Ya da hello Windows aracısı veya Operations Manager bağlı OMS Aracısı kullanın.
> - Operations Manager gerekli olduğunda, Operations Manager aracısı veri hello çözüm için her zaman hello Operations Manager yönetim grubunu kullanarak tooOMS gönderilir. Ayrıca, Operations Manager gerekli olduğunda, yalnızca hello Operations Manager Aracısı hello çözüm tarafından kullanılıyor.
> - Her zaman zaman Operations Manager gerekli değildir ve Operations Manager aracısı veri hello yönetim grubu ve Operations Manager Aracısı verileri kullanarak tooOMS gönderilir hello tablo gösterir Yönetim gruplarını kullanarak tooOMS gönderilir. Windows aracılarının hello yönetim grubu atlamak ve kendi veri gönderme doğrudan tooOMS.
> - Bir yönetim grubu kullanarak Operations Manager aracısı veri gönderilmez, hello verileri doğrudan tooOMS gönderilir. — hello yönetim grubu atlama.

### <a name="insight--analytics--log-analytics"></a>Insight & Analytics / Log Analytics

| Yönetim çözümü | Platform | Microsoft İzleme Aracısı | Operations Manager Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Etkinlik Günlüğü Analizi | Azure |   |   |   |   |   | bildirim |
| AD Değerlendirmesi |Windows |&#8226; |&#8226; |  |  |&#8226; |7 gün |
| AD Çoğaltma Durumu |Windows |&#8226; |&#8226; |  |  |&#8226; |5 gün |
| Aracı Durumu | Windows ve Linux | &#8226; | &#8226; |   |   | &#8226; | 1 dakika |
| Uyarı Yönetimi (Nagios) |Linux |&#8226; |  |  |  |  |geldiğinde |
| Uyarı Yönetimi (Zabbix) |Linux |&#8226; |  |  |  |  |1 dakika |
| Uyarı Yönetimi (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 dakika |
| Uygulama Öngörüler Bağlayıcısı (Önizleme) | Azure |   |   |   |   |   | bildirim |
| Azure uygulama ağ geçidi analizi | Azure |   |   |   |   |   | bildirim |
| Azure ağ güvenlik grubu analizi | Azure |   |   |   |   |   | bildirim |
| Azure SQL analizi (Önizleme) |Windows |  |  |  |  |  | 10 dakika |
| Kapasite Yönetimi |Windows |&#8226; |&#8226; |  |  |&#8226; |geldiğinde |
| Kapsayıcılar | Windows ve Linux | &#8226; | &#8226; |   |   |   | 3 dakika |
| Anahtar kasası analizi |Windows |  |  |  |  |  |bildirim |
| Ağ Performansı İzleyicisi | Windows | &#8226; | &#8226; |   |   |   | TCP el sıkışmaları veri her 5 saniye boyunca 3 dakikada gönderilen |
| Office 365 Analytics (Önizleme) |Windows |  |  |  |  |  |bildirim |
| Service Fabric analizi |Windows |  |  |&#8226; |  |  |5 dakika |
| Hizmet Eşlemesi | Windows ve Linux | &#8226; | &#8226; |   |   |   | 15 saniye |
| SQL Değerlendirmesi |Windows |&#8226; |&#8226; |  |  |&#8226; |7 gün |
| SurfaceHub |Windows |&#8226; |  |  |  |  |geldiğinde |
| System Center Operations Manager değerlendirmesi (Önizleme) | Windows | &#8226; | &#8226; |   |   | &#8226; | yedi gün |
| Yükseltme Analytics (Önizleme) | Windows | &#8226; |   |   |   |   | 2 gün |
| VMware izleme (Önizleme) | Linux | &#8226; |   |   |   |   | 3 dakika |
| Kablo Verileri |Windows (2012 R2 / 8.1 veya üzeri) |&#8226; |&#8226; |  |  |  | 1 dakika |


### <a name="automation--control"></a>Otomasyon ve Denetim

| Yönetim çözümü | Platform | Microsoft İzleme Aracısı | Operations Manager Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Otomasyon karma çalışanı | Windows | &#8226; | &#8226; |   |   |   | yok |
| Değişiklik İzleme |Windows |&#8226; |&#8226; |  |  |&#8226; |saatlik |
| Değişiklik İzleme |Linux |&#8226; |  |  |  |  |saatlik |
| Güncelleştirme Yönetimi | Windows |&#8226; |&#8226; |  |  |&#8226; |en az 2 kez gün ve bir güncelleştirme yüklendikten sonra 15 dakika |

### <a name="security--compliance"></a>Güvenlik ve Uyumluluk

| Yönetim çözümü | Platform | Microsoft İzleme Aracısı | Operations Manager Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Kötü amaçlı yazılımdan koruma değerlendirme |Windows |&#8226; |&#8226; |  |  |&#8226; |saatlik |
| Güvenlik ve Denetim<sup>1</sup> | Windows ve Linux | Kısmi | Kısmi | Kısmi |   | Kısmi | çeşitli |

<sup>1</sup> güvenlik hello ve denetim çözüm, Windows, Operations Manager ve Linux aracılarını günlüklerini toplayabilir. Bkz: [veri kaynakları](#data-sources) veri toplama hakkında bilgi edinmek için:

- Syslog
- Windows Güvenlik olay günlükleri
- Windows Güvenlik duvarı günlükleri
- Windows olay günlükleri



### <a name="protection--recovery"></a>Koruma ve Kurtarma

| Yönetim çözümü | Platform | Microsoft İzleme Aracısı | Operations Manager Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Backup | Azure |   |   |   |   |   | yok |
| Azure Site Recovery | Azure |   |   |   |   |   | yok |


### <a name="data-sources"></a>Veri kaynakları


| Veri kaynağı | Platform | Microsoft İzleme Aracısı | Operations Manager Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Azure etkinlik günlükleri |Windows |  |  |  |  |  |bildirim |
| Azure tanılama günlükleri |Windows |  |  |  |  |  |bildirim |
| Azure tanılama ölçümleri |Windows |  |  |  |  |  |bildirim |
| ETW |Windows |  |  |&#8226; |  |  |5 dakika |
| IIS günlükleri |Windows |&#8226; |&#8226; |&#8226; |  |  |5 dakika |
| Performans Sayaçları |Windows |&#8226; |&#8226; |  |  |  |Zamanlandığı gibi en az 10 saniye |
| Performans Sayaçları |Linux |&#8226; |  |  |  |  |Zamanlandığı gibi en az 10 saniye |
| Syslog |Linux |&#8226; |  |  |  |  |Azure depolama biriminden: 10 dakika; aracısından: işle |
| Windows Güvenlik olay günlükleri |Windows |&#8226; |&#8226; |&#8226; |  |  |Azure Depolama: 10 min; Merhaba aracısı: işle |
| Windows Güvenlik duvarı günlükleri |Windows |&#8226; |&#8226; |  |  |  |geldiğinde |
| Windows olay günlükleri |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |Azure Depolama: 10 min; Merhaba aracısı: işle |



## <a name="preview-management-solutions-and-features"></a>Önizleme yönetim çözümleri ve özellikleri
Bir hizmeti çalıştıran ve devops yöntemler aşağıdaki müşteriler toodevelop özelliklerin ve çözümlerin ile mümkün toopartner duyuyoruz.

Özel önizleme sırasında küçük bir grup ile müşteriler erişim tooan erken uyarlamasını hello özelliği ya da çözüm toogain geri bildirim verin ve iyileştirmeler sağlar. Bu erken uygulaması en az özellikleri ve işletimsel yetenekleri sahiptir.

Biz neler çalışır ve ne işe yaramazsa bulabilmesi Amacımız tootry şeyler hızla ' dir. Merhaba hello özel Önizleme müşterilerin görüşleri bize biz genel önizlemesi için hazır olduğunu bildirir. kadar size bu süreçte yineleme.

Merhaba genel Önizleme sırasında hello özelliği ya da çözüm daha fazla geribildirim tüm kullanıcıların tooget için kullanılabilir hale getirmek ve bizim ölçekleme ve verimlilik doğrulayın. Bu aşamada:

* Önizleme özellikleri hello ayarları sekmesinde görüntülenir ve herhangi bir kullanıcı tarafından etkinleştirilebilir.
* Önizleme çözümler eklenir üzerinden hello galeri veya bir komut dosyası kullanarak.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Ne ı Önizleme özellikleri ve çözümleri hakkında bilmeniz gereken?
Şu yeni özellikler ve yönetim çözümleri hakkında Çoğalması ve bunları, toodevelop ile çalışma memnuniyet.

Önizleme özelliklerin ve çözümlerin herkes için doğru değil. Özel önizleme toojoin sormak veya genel Önizleme etkinleştirmeden önce Tamam geliştirilmekte olan bir şey çalıştığınız emin olun.

Bir önizleme özelliği hello portal üzerinden etkinleştirme geçirdiğinizde özelliği Merhaba, önizlemededir anımsatma bir uyarı görürsünüz.

#### <a name="for-both-private-and-public-preview"></a>Her ikisi için de *özel* ve *ortak* Önizleme
Merhaba aşağıdaki bilgiler tooboth ortak ve özel önizlemeleri geçerlidir:

* Şeyler düzgün her zaman çalışmayabilir.
  * İkincil bir sıkıntı getirir hiç çalışmıyor toosomething aracılığıyla engeller aralığı verir.
* Yoktur hello Önizleme toohave sistemleriniz üzerinde olumsuz bir etkisi için olası / ortamı.
  * Biz OMS ancak bazen beklenmeyen şeyler ile kullandığınız oluşmasını toohello sistemleri ortaya tooavoid negatif şeyleri deneyin.
* Veri kaybı / Bozulması meydana gelebilir.
* Biz, toocollect tanılama günlükleri veya diğer veri toohelp sorun giderme sorunlarını isteyebilir.
* Merhaba özelliği ya da çözüm (geçici veya kalıcı olarak) kaldırılmış olabilir.
  * Bizim learnings üzerinde hello Önizleme sırasında dayalı biz toonot yayın hello özelliği ya da çözüm karar verebilirsiniz.
* Önizlemeler çalışmayabilir veya tüm yapılandırmaları test edilmemiştir ve biz sınırlayabilir:
  * Merhaba kullanılabilir işletim sistemleri (örneğin, bir özelliği yalnızca önizlemesinde tooLinux geçerli olabilir).
  * Merhaba kullanılabilir aracısının (MMA, Operations Manager) türünü (örneğin, bir özellik önizlemesinde Operations Manager'da çalışmayabilir).  
* Önizleme çözümleri ve özellikleri hello tarafından hizmet düzeyi sözleşmesi kapsamında değildir.
* Önizleme özelliklerinin kullanımını kullanım ücretleri doğurur.
* Özellikleri veya yetenekleri hello özelliği için gereksinim duyduğunuz / çözüm toobe yararlı eksik veya tamamlanmamış olabilir.
* Özellikler / çözümleri kullanılabilir olmayabilir tüm bölgelerde.
* Özellikler / çözümleri yerelleştirilmemiş.
* Özellikler / çözümleri, müşterilerinin ya da kullanılabilmesi için cihazların Merhaba sayısına bir sınır olabilir.
* Toouse betikleri tooperform yapılandırması ve tooenable hello çözüm/özellik gerekebilir.
* Merhaba kullanıcı arabirimi (UI) eksik ve gün tooday değişebilir.
* Üretim için uygun / kritik ortak önizlemeleri olmayabilir sistemler.

#### <a name="for-private-preview"></a>İçin *özel* Önizleme
Toplama toohello öğelerde yukarıdaki bilgisinden hello belirli tooprivate önizlemeleri şöyledir:

* Böylece biz yapabilirsiniz deneyiminizi geribildirim bizimle özelliği/çözümü aşağıdaki daha iyi hello tooprovide bekliyoruz.
* Sizinle anketler, telefon aramaları veya e-posta kullanarak geri bildirim için iletişim.
* Öğeleri her zaman doğru çalışmaz.
* Biz olmayan açığa Sözleşmesi (NDA) için katılımını gerektirebilir veya gizli içeriğin içerebilir.
  * Blog, TWİTLEME veya aksi halde üçüncü taraflarla iletişim önce lütfen hello hello Önizleme toounderstand için sorumlu Program Yöneticisi ile açığa üzerinde herhangi bir kısıtlamanın denetleyin.
* Çalıştırmayın üretim / kritik sistemler.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Erişim tooprivate Önizleme özelliklerin ve çözümlerin nasıl sağlarım?
Müşteriler tooprivate önizlemeleri hello Önizleme bağlı olarak birkaç farklı şekilde aracılığıyla davet ediyoruz.

* Merhaba aylık müşteri anket yanıtlama ve bize izni toofollow sizinle vazgeçmeden davet edilen tooa özel Önizleme olma şansınız artırır.
* Microsoft hesap ekibi, belirleyebilirsiniz.
* Twitter'da gönderilen Ayrıntılar temel kaydolabilirsiniz [msopsmgmt](https://twitter.com/msopsmgmt).
* Ayrıntılar paylaşılan topluluk olaylara göre – kaydolabilirsiniz bize karşılamak Ara ups, konferans ve çevrimiçi topluluklar.

## <a name="next-steps"></a>Sonraki adımlar
* [Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı yönetim çözümleri tarafından toplanan bilgiler.
