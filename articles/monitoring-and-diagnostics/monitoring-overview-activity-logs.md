---
title: "hello Azure etkinlik günlüğü aaaOverview | Microsoft Docs"
description: "Azure etkinlik günlüğü hangi hello ve nasıl Azure aboneliğinizi içinde gerçekleşen toounderstand olayların kullanabileceğinizi öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Azure etkinlik günlüğü hello ile abonelik etkinliğini izleme
Merhaba **Azure etkinlik günlüğü** , Azure'da oluşan abonelik düzeyinde olaylar hakkında bilgi sağlayan bir abonelik günlüktür. Bu verileri, Azure Resource Manager işlemsel veri tooupdates hizmet sistem durumu olayları üzerinde bir dizi içerir. Hello etkinlik günlüğü önceden hello yönetim kategorisi raporları denetim düzlemi olaylarını aboneliklerinizi itibaren "Denetim günlüklerini" veya "İşlem günlükleri," olarak bilinirdi. Merhaba etkinlik günlüğü kullanarak hello belirleyebilirsiniz ' ne, kimin, ne zaman ve ' herhangi yazma işlemleri (PUT, POST, DELETE) aboneliğinizde hello kaynaklar üzerinde gerçekleştirilecek için. Merhaba hello işleminin durumunu ve ilgili diğer özellikleri de anlayabilirsiniz. Merhaba etkinlik günlüğü okuma (GET) işlemleri veya hello Klasik kullanan kaynakları işlemlerinde içermez / "RDFE" modeli.

![Etkinlik günlükleri vs günlükleri diğer türleri ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Şekil 1: Etkinlik günlükleri vs günlükleri diğer türleri

Merhaba etkinlik günlüğü farklıdır [tanılama günlükleri](monitoring-overview-of-diagnostic-logs.md). Etkinlik günlükleri hello (Merhaba "Denetim düzlemi") dışında bir kaynaktan hello işlemleri hakkında veriler sağlar. Tanılama günlüklerini bir kaynak tarafından gösterilen ve bu kaynağın (Merhaba "veri düzlemi") hello işlemiyle ilgili bilgi sağlayın.

Olaylar, etkinlik hello Azure portal, CLI, PowerShell cmdlet'lerini kullanarak günlük alabilir ve Azure İzleyici REST API'si.


> [!WARNING]
> öncelikle Azure Kaynak Yöneticisi'nde ortaya etkinlikleri Hello Azure etkinlik günlüğü içindir. Merhaba Klasik/RDFE modeli kullanarak kaynakları izlemez. Bazı Klasik kaynak türleri proxy kaynak sağlayıcısı Azure Resource Manager (örneğin, Microsoft.ClassicCompute) sahiptir. Bir Klasik kaynak türü üzerinden Azure kaynak bu proxy kaynak sağlayıcılarını kullanarak Yöneticisi ile etkileşim hello işlemleri hello etkinlik günlüğü görünür. İle etkileşim Klasik kaynak türü hello Klasik Portalı'nda veya aksi halde hello Azure Resource Manager proxy'leri dışında eylemlerinizi yalnızca hello işlem günlüğüne kaydedilir. Merhaba işlem günlüğünün yalnızca hello Klasik portalda erişilebilir.
>
>

Video ile tanışın hello etkinlik günlüğü aşağıdaki görünümü hello.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Merhaba etkinlik günlüğü kategorileri
Merhaba etkinlik günlüğü verileri çeşitli kategorileri içerir. Bu kategoride hello şemalara ilgili tam Ayrıntılar için [bu makaleye bakın](monitoring-activity-log-schema.md). Bunlar:
* **Yönetim** -bu kategorideki tüm hello kayıt içeren oluşturma, güncelleştirme, silme ve eylem işlemlerine Resource Manager aracılığıyla gerçekleştirilir. Bu kategorideki görür olay türleri dahil hello örnekleri "sanal makine oluşturma" ve "ağ güvenlik grubu bir kullanıcı tarafından gerçekleştirilen her eylem delete" veya Kaynak Yöneticisi'ni kullanarak uygulama belirli bir kaynak türü üzerinde bir işlemi olarak modellenir. Merhaba işlem türü ise yazma, silme veya eylem hello kayıtlarını hello başlangıç ve başarı veya işlemi hello yönetim kategorisinde kaydedilir başarısız. Merhaba yönetim kategorisi, ayrıca bir abonelikte herhangi bir değişiklik toorole tabanlı erişim denetimi içerir.
* **Hizmet durumu** -bu kategoriyi Azure'da oluşan herhangi bir hizmet durumu olay hello kaydını içerir. Bu kategorideki görür olay hello türü "SQL Azure Doğu ABD kesinti yaşanıyor." örneğidir Hizmet sistem durumu olayları beş çeşit olarak gelir: eylem gerekli, Destekli kurtarma, olay, bakım, bilgi veya güvenlik ve hello olay tarafından etkilenen hello Abonelikteki bir kaynağınız varsa yalnızca görünür.
* **Uyarı** -bu kategorideki tüm etkinleştirmeleri Azure uyarıların hello kaydını içerir. Bu kategorideki görür olay hello türü "myVM CPU % son 5 dakika boyunca hello 80 bırakıldı." örneğidir Azure sistemleri çeşitli sahip bir uyarı verme kavramı--bir kural çeşit tanımlayabilir ve bu kural için koşullara uyan bir bildirim alıyorsunuz. Her bir desteklenen Azure uyarı türü 'etkinleştirir,' veya hello koşullar sağlanmadığı toogenerate bir bildirim, hello etkinleştirme kaydını da hello etkinlik günlüğü toothis kategorisini gönderilir.
* **Otomatik ölçeklendirme** -bu kategori, aboneliğinizde tanımladığınız herhangi bir otomatik ölçeklendirme ayarı göre hello otomatik ölçeklendirme altyapısının herhangi bir olayları ilgili toohello işlem hello kaydını içerir. Bu kategorideki görür olay hello türü "Otomatik ölçeklendirme ölçek büyütme eylemi başarısız oldu." örneğidir Otomatik ölçeklendirme'ni kullanarak, otomatik olarak ölçeğini veya ölçeklendirmek hello desteklenen kaynak türü örneği sayısı dayalı bir otomatik ölçeklendirme ayarı kullanarak gün ve/veya yük (ölçüm) verileri zamanında. Merhaba koşullar karşılandığında tooscale yukarı veya aşağı, hello başlangıç ve başarılı veya başarısız olayları bu kategorideki kaydedilir.
* **Öneri** -öneri olaylarından web siteleri ve SQL sunucuları gibi bazı kaynak türleri bu kategorisi içerir. Bu olaylar nasıl toobetter kullanan kaynaklarınız için öneriler sunar. Öneriler yayma kaynaklarınız varsa, yalnızca bu tür olayları alırsınız.
* **İlke, güvenlik ve kaynak durumu** -Bu kategorilerden tüm olaylar içermez; gelecekte kullanılmak üzere ayrılmıştır.

## <a name="event-schema-per-category"></a>Her kategori şeması
[Bu makale toounderstand hello etkinlik günlüğü olay şema her kategori bakın.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>Etkinlik günlüğü hello ile yapabilecekleriniz
Etkinlik günlüğü hello ile yapabileceğiniz hello şeylerden bazıları şunlardır:

![Azure etkinlik günlüğü](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Sorgulamak ve hello görüntülemek **Azure portal**.
* [Bir uyarı etkinlik günlüğü olay olarak oluşturun.](monitoring-activity-log-alerts.md)
* [Tooan akış **olay hub'ı** ](monitoring-stream-activity-logs-event-hubs.md) bir üçüncü taraf hizmeti veya Powerbı gibi özel analiz çözümü tarafından alımı için.
* Hello kullanarak Powerbı içinde analiz [ **Power BI içerik paketi**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Tooa kaydetmek **depolama hesabı** arşivleme veya el ile İnceleme için](monitoring-archive-activity-log.md). Hello kullanarak hello bekletme süresi (gün) belirtebilirsiniz **günlük profili**.
* PowerShell Cmdlet, CLI veya REST API sorgu.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Sorgu hello etkinlik günlüğü hello Azure portalı
Azure portal Hello içinde çeşitli yerlerde, etkinlik günlüğü görüntüleyebilirsiniz:
* Merhaba **etkinlik günlüğü dikey**, hangi hello Sol Gezinti Bölmesi'nde hello "Daha Hizmetleri" altında etkinlik günlüğü için arama yaparak erişebilirsiniz.
* Merhaba **İzleyici dikey**, varsayılan hello sol gezinti bölmesinde görüntülenir. Merhaba etkinlik günlüğü bu Azure İzleyici dikey bölümüdür.
* Herhangi bir kaynağa ait **kaynak dikey**, örneğin, bir sanal makine için hello yapılandırma dikey. Merhaba etkinlik günlüğü bu kaynak dikey çoğunu hello bölümleri biri olması olduğundan ve otomatik olarak üzerine tıklayarak hello olayları filtreler toothose ilgili toothat belirli kaynak.

Hello Azure portalı, bu alanlara göre etkinlik günlüğü filtreleyebilirsiniz:
* TimeSpan - hello başlangıç ve bitiş zamanı olayları.
* Kategori - yukarıda açıklandığı gibi hello olay kategorisi.
* Abonelik - bir veya daha fazla Azure aboneliği adları.
* Kaynak grubu - bu abonelikleri içinde bir veya daha fazla kaynak gruplar.
* Kaynak (ad) - belirli bir kaynak hello adı.
* Kaynak türü - kaynak, örneğin, Microsoft.Compute/virtualmachines hello türü.
* İşlem adı - Merhaba, örneğin, Microsoft.SQL/servers/Write bir Azure Resource Manager işlem.
* Önem derecesi - hello önem derecesi hello olayı (uyarı, bilgilendirici, hata, kritik).
* 'Arayan' Hello veya hello işlemi gerçekleştiren kullanıcı tarafından - başlatılan olay.
* Arama Aç - tüm olayları tüm alanları genelinde için bu dizeyi arar bir açık metin arama kutusu budur.

Bir filtre kümesi tanımladıktan sonra tooperform erişiminizi gerekirse oturumlarında kalıcı bir sorgu kaydedebilirsiniz hello aynı sorgu bu filtreler yeniden hello gelecekteki uygulanmış. Ayrıca, bir sorgu tooyour Azure Pano tooalways Koru bir göz belirli olayları sabitleyebilirsiniz.

"Uygulama" tıklatarak sorgunuzu çalıştırır ve tüm eşleşen olayları gösterir. Gösterir bu olay Özet hello yanı sıra bu olayın tam ham JSON hello hello listesindeki herhangi bir etkinliğe tıklayarak.

Daha fazla güç için hello tıklatabilirsiniz **günlük arama** hello etkinlik günlüğü verilerinizi görüntüler simgesi [günlük analizi etkinlik günlüğü analizi çözüm](../log-analytics/log-analytics-activity.md). Merhaba etkinlik günlüğü dikey günlükleri, ancak siz toopivot sorgu ve daha güçlü şekilde görselleştirmek günlük analizi sağlar temel filtre/Gözat deneyimi sağlar.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Merhaba günlük profille etkinlik günlüğü dışarı aktarma
A **günlük profili** nasıl etkinlik günlüğü dışarı denetler. Bir günlük profili kullanarak, aşağıdakileri yapılandırabilirsiniz:

* Merhaba etkinlik günlüğü (depolama hesabı veya olay hub'ları) burada gönderilmesi gereken
* Hangi olay kategorileri (yazma, silme, eylem) gönderilmelidir. *Günlük profillerinde ve etkinlik günlüğü olaylarını "kategorisi" Merhaba anlamını farklıdır. Hello günlük profili, "Kategorisi" Merhaba işlem türü (yazma, silme, eylem) temsil eder. Bir etkinlik günlüğü olay hello "kategorisi" özelliğini hello kaynak ya da (örneğin, yönetim, ServiceHealth, uyarı ve daha fazla) olay türünü temsil eder.*
* Hangi bölgelerde (konumlara) aktarılması. Merhaba etkinlik günlüğü birçok olayları genel olayları olduğundan emin tooinclude "Genel" yapın.
* Ne kadar süreyle etkinlik günlüğü hello bir depolama hesabında tutulmalıdır.
    - Sıfır gün bekletme günlükleri sonsuza kadar tutulur anlamına gelir. Aksi takdirde hello değer 1 ile 2147483647 arasındaki gün herhangi bir sayıda olabilir.
    - Bekletme ilkeleri ayarlanır, ancak yalnızca (örneğin, olay hub'ları veya OMS seçenekler seçilidir) günlükleri bir depolama hesabında depolama devre dışı bırakıldı, hello bekletme ilkeleri bir etkisi yoktur.
    - Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir. Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek.

Veya kullanımda olmayan olay hub'ad alanı hello aynı abonelik bir günlükleri yayma hello gibi bir depolama hesabı kullanabilirsiniz. Merhaba ayarı yapılandıran hello kullanıcının hello uygun RBAC erişim tooboth abonelikleri olması gerekir.

Bu ayarlar, hello "Verme" seçeneğinin hello etkinlik günlüğü dikey penceresinde hello portal aracılığıyla yapılandırılabilir. Bunlar ayrıca program aracılığıyla yapılandırılabilir [hello Azure İzleyici REST API'sini kullanarak](https://msdn.microsoft.com/library/azure/dn931927.aspx), PowerShell cmdlet'leri veya CLI. Bir abonelik yalnızca bir günlük profil olabilir.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Hello Azure portal kullanarak günlük profillerini yapılandırma
Merhaba etkinlik günlüğü tooan olay hub'ı akışla aktarmak veya bunları hello Azure portal hello "Verme" seçeneğini kullanarak bir depolama hesabında depolamak.

1. Toohello gidin **etkinlik günlüğü** yan hello portalının sol hello üzerinde hello menüsünü kullanarak dikey.

    ![TooActivity günlük portalında gidin](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Merhaba tıklatın **dışarı** hello dikey penceresinde hello üstündeki düğmesi.

    ![Portalında Dışarı Aktar](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Görüntülenen hello dikey penceresinde şunları seçebilirsiniz:  
  * tooexport olayları istediğiniz bölgeleri
  * Depolama hesabı toowhich toosave olayları istediğiniz hello
  * Bu olaylar depolama tooretain istediğiniz gün sayısını Hello. 0 gün ayarı hello günlükleri sonsuza kadar saklar.
  * Merhaba hizmet veri yolu Namespace bu olayları akış için oluşturulan bir olay hub'ı toobe istersiniz.

     ![Etkinlik günlüğü dikey dışarı aktarma](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Tıklatın **kaydetmek** toosave bu ayarlar. Hello ayarları hemen uygulanan tooyour abonelik olabilir.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Hello Azure PowerShell cmdlet'lerini kullanarak günlük profillerini yapılandırma
#### <a name="get-existing-log-profile"></a>Var olan günlük profilini Al
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Bir günlük profili ekleyin
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| Ad |Evet |Günlük profilinin adı. |
| StorageAccountId |Hayır |Kaynak Kimliğini hello depolama hesabı toowhich hello etkinlik günlüğü kaydedilmesi gerekir. |
| serviceBusRuleId |Hayır |Hizmet veri yolu kural kimliği hello hizmet veri yolu ad alanı için oluşturduğunuz toohave olay hub'ları ister. Bu biçimde bir dize: `{service bus resource ID}/authorizationrules/{key name}`. |
| Konumlar |Evet |Toocollect etkinlik günlüğü olaylarını istediğiniz bölgeler virgülle ayrılmış listesi. |
| retentionInDays |Evet |Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı. Sıfır değeri hello günlükleri süresiz olarak depolar (sürekli). |
| Kategoriler |Hayır |Toplanması gereken olay kategorileri virgülle ayrılmış listesi. Olası değerler şunlardır: yazma, silme ve eylem. |

#### <a name="remove-a-log-profile"></a>Günlük profilini Kaldır
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Günlük profillerini yapılandırma kullanma hello Azure platformlar arası CLI
#### <a name="get-existing-log-profile"></a>Var olan günlük profilini Al
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Merhaba `name` özelliği, günlük profilinizin hello adı olmalıdır.

#### <a name="add-a-log-profile"></a>Bir günlük profili ekleyin
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| ad |Evet |Günlük profilinin adı. |
| storageId |Hayır |Kaynak Kimliğini hello depolama hesabı toowhich hello etkinlik günlüğü kaydedilmesi gerekir. |
| serviceBusRuleId |Hayır |Hizmet veri yolu kural kimliği hello hizmet veri yolu ad alanı için oluşturduğunuz toohave olay hub'ları ister. Bu biçimde bir dize: `{service bus resource ID}/authorizationrules/{key name}`. |
| Konumları |Evet |Toocollect etkinlik günlüğü olaylarını istediğiniz bölgeler virgülle ayrılmış listesi. |
| retentionInDays |Evet |Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı. Sıfır değeri hello günlükleri süresiz olarak depolar (sürekli). |
| kategorileri |Hayır |Toplanması gereken olay kategorileri virgülle ayrılmış listesi. Olası değerler şunlardır: yazma, silme ve eylem. |

#### <a name="remove-a-log-profile"></a>Günlük profilini Kaldır
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Sonraki Adımlar
* [Merhaba etkinlik günlüğü (önceki adıyla denetim günlüklerini) hakkında daha fazla bilgi edinin](../azure-resource-manager/resource-group-audit.md)
* [Hello Azure etkinlik günlüğü tooEvent hub akışı](monitoring-stream-activity-logs-event-hubs.md)
