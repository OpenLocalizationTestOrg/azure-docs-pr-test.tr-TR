---
title: "Azure tanılama günlüklerinin aaaOverview | Microsoft Docs"
description: "Azure tanılama günlüklerini nedir ve nasıl bir Azure kaynağı içinde gerçekleşen toounderstand olayların kullanabilmek için öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Toplamak ve Azure kaynaklarınızdan günlük verilerini kullanma

## <a name="what-are-azure-resource-diagnostic-logs"></a>Azure kaynak tanılama günlüklerini nelerdir
**Azure kaynak düzeyi tanılama günlüklerini** olan bir kaynak tarafından gösterilen günlükleri, zengin, sık hello işlemi bu kaynağın hakkında veriler sağlar. Bu günlükler Merhaba içeriğine kaynak türüne göre değişir. Örneğin, ağ güvenlik grubu kural sayaçları ve anahtar kasası denetimleri kaynak günlükleri iki kategorisi vardır.

Kaynak düzeyi tanılama günlükleri farklı hello [etkinlik günlüğü](monitoring-overview-activity-logs.md). Merhaba etkinlik günlüğü kaynakları Kaynak Yöneticisi'ni kullanarak, örneğin, bir sanal makine oluşturma veya bir mantıksal uygulama silme gerçekleştirilen hello işlemleri hakkında bilgi sağlar. Merhaba etkinlik günlüğü bir abonelik düzeyi günlüğü bulunmaktadır. Kaynak düzeyi tanılama günlükleri, bu kaynak içinde kendisi, örneğin, gizli bir anahtar Kasası'nı alma gerçekleştirilen işlemler hakkında bilgi sağlar.

Kaynak düzeyi tanılama günlüklerini de konuk işletim sistemi düzeyinde tanılama günlükleri farklılık gösterir. Konuk işletim sistemi tanılama günlüklerini bu sanal makine içinde çalışan bir aracının tarafından toplanan veya diğer kaynak türü desteklenir. Konuk işletim sistemi düzeyinde tanılama günlüklerini hello işletim sistemi ve sanal makine üzerinde çalışan uygulamalardan veri yakalama işlemi sırasında kaynak düzeyi tanılama günlüklerini hello Azure platformu kendisini hiçbir aracı ve yakalama kaynak özgü veri gerektirir.

Tüm kaynakları kaynak tanılama günlüklerini burada açıklanan yeni tür hello desteklemez. Bu makale, hangi kaynak türlerinin hello yeni kaynak düzeyi tanılama günlüklerini destek bölümüne listesini içerir.

![Kaynağın tanılama günlükleri diğer türleri vs günlükleri ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Kaynak düzeyi tanılama günlükleri ile yapabilecekleriniz
Kaynağın tanılama günlükleri ile yapabileceğiniz hello şeylerden bazıları şunlardır:

![Kaynağın tanılama günlüklerinin mantıksal yerleştirme](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Tooa kaydetmek [ **depolama hesabı** ](monitoring-archive-diagnostic-logs.md) denetim veya el ile İnceleme için. Merhaba bekletme süresi (gün) kullanarak belirtebilirsiniz **kaynak tanılama ayarlarını**.
* [Çok akış**Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) bir üçüncü taraf hizmeti veya Powerbı gibi özel analiz çözümü tarafından alımı için.
* Bunları ile analiz [OMS günlük analizi](../log-analytics/log-analytics-azure-storage.md)

Veya kullanımda olmayan olay hub'ları ad alanı hello aynı abonelik bir günlükleri yayma hello gibi bir depolama hesabı kullanabilirsiniz. Merhaba ayarı yapılandıran hello kullanıcının hello uygun RBAC erişim tooboth abonelikleri olması gerekir.

## <a name="resource-diagnostic-settings"></a>Kaynak tanılama ayarları
Kaynağın tanılama günlüklerini olmayan-kaynakları kaynak tanılama ayarları kullanılarak yapılandırılmış olan işlem. **Kaynak tanılama ayarlarını** kaynak denetimi için:

* Kaynağın tanılama günlüklerini ve ölçümleri (depolama hesabı, olay hub'ları ve/veya OMS günlük analizi) gönderildiği.
* Günlük kategorilerini gönderilir ve ölçüm verileri de gönderilip.
* Her günlük kategori bir depolama hesabında ne kadar süre tutulacağını
    - Sıfır gün bekletme günlükleri sonsuza kadar tutulur anlamına gelir. Aksi takdirde hello değer 1 ile 2147483647 arasındaki gün herhangi bir sayıda olabilir.
    - Bekletme ilkeleri ayarlanır, ancak yalnızca (örneğin, olay hub'ları veya OMS seçenekler seçilidir) günlükleri bir depolama hesabında depolama devre dışı bırakıldı, hello bekletme ilkeleri bir etkisi yoktur.
    - Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir. Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek.

Bu ayarlar hello hello Azure portalında bir kaynak için tanılama ayarları aracılığıyla, Azure PowerShell ve CLI komutları aracılığıyla veya hello aracılığıyla kolayca yapılandırılır [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Tanılama günlüklerini ve hello konuk işletim sistemi katmanından işlem kaynakları (örneğin, VM'ler veya Service Fabric) kullanım ölçümlerini [yapılandırması ve çıkışları seçimi için ayrı bir mekanizma](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Nasıl kaynak tanılama günlüklerini tooenable koleksiyonu
Kaynağın tanılama günlüklerini koleksiyonunu etkinleştirilebilir [bir Resource Manager şablonunda kaynak oluştururken bir parçası olarak](./monitoring-enable-diagnostic-logs-using-template.md) veya bir kaynak hello Portalı'nda bu kaynağın sayfasından oluşturulduktan sonra. Azure PowerShell veya CLI komutları veya hello Azure İzleyici REST API'sini kullanarak herhangi bir noktada koleksiyonu de etkinleştirebilirsiniz.

> [!TIP]
> Bu yönergeleri tooevery kaynak doğrudan geçerli olmayabilir. Toocertain kaynak türleri uygulayabilir bu sayfa toounderstand özel adımlar hello sonundaki Hello şema bağlantılara bakın.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Merhaba Portal'daki kaynak tanılama günlükleri toplamayı etkinleştir
Tanılama günlükleri hello Azure kaynak koleksiyonunu etkinleştirebilirsiniz kaynak giderek tooa belirli bir kaynak tarafından ya da tooAzure İzleyici gezinme oluşturulduktan sonra portal. tooenable Azure İzleyicisi aracılığıyla:

1. Merhaba, [Azure portal](http://portal.azure.com)tooAzure İzleyici gidin ve tıklayın **tanılama ayarları**

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. İsteğe bağlı olarak kaynak grubu veya kaynak türü tarafından hello listesini filtrelemek ve tooset tanılama ayarını istediğiniz hello kaynakta'i tıklatın.

3. Hiçbir ayar seçmiş olduğunuz hello kaynakta mevcut, istendiğinde toocreate bir ayar demektir. "Tanılamayı açın."'i tıklatın

   ![Tanılama ayarını - ayar Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Merhaba kaynakta mevcut ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz. "Tanılama ayarını Ekle" yi tıklatın.

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Ayar bir adı verin, her hedef toowhich toosend veri gibi ve hangi kaynak yapılandırmak her hedefi için kullanılan hello kutularını kontrol edin. İsteğe bağlı olarak, bu günlükler ayarlamak hello kullanarak birkaç gün tooretain **bekletme (gün)** kaydırıcılar (yalnızca geçerli toohello depolama hesabı hedef). Sıfır gün bekletme hello günlükleri süresiz olarak depolar.
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. **Kaydet** düğmesine tıklayın.

Yeni olay verilerini oluşturulan hemen birkaç dakika sonra hello ayarı bu kaynak için ayarları listesi görüntülenir ve tanılama günlüklerini toohello gönderilen yeni hedefleri belirtilmiş.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>PowerShell aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir
kaynağın tanılama günlüklerini Azure PowerShell, aşağıdaki komutları kullanın hello aracılığıyla tooenable koleksiyonu:

bir depolama hesabında tanılama günlüklerinin tooenable depolama bu komutu kullanın:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

Merhaba depolama hesabı kimliği hello depolama hesabı toowhich toosend hello istediğiniz günlükleri oluşturmak için kaynak kimliği hello.

Tanılama günlüklerini tooan event hub ' tooenable akış bu komutu kullanın:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

Merhaba hizmet veri yolu kural kimliği: Bu biçim bir dizeyle: `{Service Bus resource ID}/authorizationrules/{key name}`.

Tanılama günlüklerini tooa günlük analizi çalışma alanının tooenable gönderme bu komutu kullanın:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Merhaba kaynak kimliği komutu aşağıdaki hello kullanarak günlük analizi çalışma alanınızın elde edebilirsiniz:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Bu parametreleri tooenable birden çok çıktı seçenekleri birleştirebilirsiniz.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>CLI aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir
Kaynak tanılama günlüklerini hello Azure CLI aracılığıyla tooenable koleksiyonu hello aşağıdaki komutları kullanın:

bir depolama hesabında tanılama günlüklerinin tooenable depolama bu komutu kullanın:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

Merhaba depolama hesabı kimliği hello depolama hesabı toowhich toosend hello istediğiniz günlükleri oluşturmak için kaynak kimliği hello.

Tanılama günlüklerini tooan event hub ' tooenable akış bu komutu kullanın:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

Merhaba hizmet veri yolu kural kimliği: Bu biçim bir dizeyle: `{Service Bus resource ID}/authorizationrules/{key name}`.

Tanılama günlüklerini tooa günlük analizi çalışma alanının tooenable gönderme bu komutu kullanın:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Bu parametreleri tooenable birden çok çıktı seçenekleri birleştirebilirsiniz.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>REST API aracılığıyla kaynak tanılama günlükleri toplamayı etkinleştir
Hello Azure İzleyici REST API'sini kullanarak toochange tanılama ayarlarını bkz [bu belgeyi](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Merhaba Portal'daki kaynak tanılama ayarlarını yönet
Tüm kaynaklarınız tanılama ayarları ile ayarlandığından emin olun. Çok gidin**İzleyici** hello portal ve açık olarak **tanılama ayarlarını**.

![Tanılama günlüklerini dikey penceresinde hello portalı](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

"Daha fazla Hizmetleri" toofind hello İzleyici bölümüne tooclick olabilir.

Burada görebilirsiniz ve tanılama ayarlarını toosee tanılaması etkin varsa destekleyen tüm kaynakları filtreleyin. Ayrıca, birden çok ayarları bir kaynakta ayarlandıysa toosee incelemek ve hangi depolama hesabı, olay hub'ları ad ve/veya veri akışının günlük analizi çalışma alanı denetleyin.

![Tanılama günlüklerini sonuçları portalında](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Merhaba burada etkinleştir, devre dışı bırakmak veya hello için tanılama ayarlarınızı değiştirmek için tanılama ayarları görünümü, Yukarı tanılama ayarını getirir ekleme kaynak seçtiniz.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Desteklenen hizmetler, kategoriler ve kaynak tanılama günlükleri için şemaları
[Bu makaleye bakın](monitoring-diagnostic-logs-schema.md) desteklenen hizmetlerin ve hello günlük kategorileri ve bu hizmetler tarafından kullanılan şemalar tam bir listesi.

## <a name="next-steps"></a>Sonraki adımlar

* [Kaynağın tanılama günlükleri çok akış**olay hub'ları**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Hello Azure İzleyici REST API'sini kullanarak kaynak tanılama ayarlarını değiştirme](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin](../log-analytics/log-analytics-azure-storage.md)
