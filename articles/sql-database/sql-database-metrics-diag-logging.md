---
title: "Azure SQL veritabanı ölçümleri & tanılama günlükleri | Microsoft Docs"
description: "Kaynak kullanımı, bağlantı ve sorgu yürütme istatistikleri depolamak için Azure SQL veritabanı kaynak yapılandırma hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Azure SQL Database ölçümleri ve tanılama günlükleri 
Azure SQL Database ölçümleri ve daha kolay izleme için tanılama günlükleri yayma. Kaynak kullanımı, çalışanlar ve oturumlar ve bu Azure kaynakları birine bağlantısını depolamak için Azure SQL veritabanı yapılandırabilirsiniz:
- **Azure Depolama**: Küçük maliyetlerle çok sayıda telemetri arşivleme için
- **Azure Event Hub**: Azure SQL veritabanı telemetri özel izleme çözümü veya etkin işlem hatları ile tümleştirmek için
- **Azure günlük analizi**: için raporlama, uyarı ve yetenekleri Azaltıcı çözüm izleme kutusunu dışında 

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Günlü kaydını etkinleştir

Ölçümleri ve Tanılama Günlüğü varsayılan olarak etkinleştirilmedi. Etkinleştirme ve ölçüm ve aşağıdaki yöntemlerden birini kullanarak oturum tanılama yönetebilirsiniz:
- Azure portalına
- PowerShell
- Azure CLI
- REST API 
- Resource Manager şablonu

Ölçümleri ve tanılama günlükleri etkinleştirdiğinizde, burada seçilen verileri toplanır Azure kaynak belirtmeniz gerekir. Seçenekleri kullanılabilir:
- Log Analytics
- Olay Hub'ı
- Azure Storage 

Yeni bir Azure kaynak sağlama veya var olan bir kaynak seçin. Depolama kaynağı seçtikten sonra hangi verileri toplamak için belirtmeniz gerekir. Kullanılabilir seçenekler şunlardır:

- **[1 dakikalık ölçümleri](sql-database-metrics-diag-logging.md#1-minute-metrics)**  -içeren DTU yüzdesi, DTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, başarılı/başarısız/engellenen Güvenlik Duvarı bağlantılarını, oturumlar yüzdesi, çalışanların yüzdesi Depolama, depolama yüzdesi, XTP depolama yüzdesi

Olay hub'ı veya bir AzureStorage hesabı belirtirseniz, seçilen zaman aralığı silinmiş daha eski bu verileri belirtmek için bir bekletme ilkesi belirtebilirsiniz. Günlük analizi belirtirseniz, bekletme ilkesi seçilen fiyatlandırma katmanını bağlıdır. Daha fazla bilgi edinin [günlük analizi fiyatlandırma](https://azure.microsoft.com/pricing/details/log-analytics/). 

Her ikisi de okumanızı öneririz [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md) ve [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) günlük ancak ölçümleri etkinleştirmek yalnızca nasıl anlamak için makaleleri ve çeşitli Azure Hizmetleri tarafından desteklenen kategorileri oturum açın.

### <a name="azure-portal"></a>Azure portalına

Ölçümleri ve tanılama günlüklerini toplama Azure portalında etkinleştirmek için Azure SQL veritabanı veya esnek havuz sayfasına gidin ve ardından **tanılama ayarlarını**.

   ![Azure portalında etkinleştir](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

Ölçümleri ve PowerShell kullanarak tanılama günlük kaydını etkinleştirmek için aşağıdaki komutları kullanın:

- Tanılama günlüklerinin bir depolama hesabındaki depolama etkinleştirmek için bu komutu kullanın:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   Depolama hesabı kimliği günlükleri göndermek istediğiniz depolama hesabını kaynak kimliğidir.

- Bir olay Hub'ına tanılama günlüklerini akışını etkinleştirmek için bu komutu kullanın:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Hizmet veri yolu kuralı kimliği, bu biçiminde bir dizedir:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- Günlük analizi çalışma alanı için tanılama günlüklerini gönderilmesine izin vermek için bu komutu kullanın:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- Aşağıdaki komutu kullanarak, günlük analizi çalışma alanı kaynak kimliğini elde edebilirsiniz:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

Birden çok çıktı seçenekleri etkinleştirmek için bu parametreler birleştirebilirsiniz.

### <a name="cli"></a>CLI

Ölçümleri ve Azure CLI kullanarak tanılama günlük kaydını etkinleştirmek için aşağıdaki komutları kullanın:

- Tanılama günlüklerinin bir depolama hesabındaki depolama etkinleştirmek için bu komutu kullanın:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   Depolama hesabı kimliği günlükleri göndermek istediğiniz depolama hesabını kaynak kimliğidir.

- Bir olay Hub'ına tanılama günlüklerini akışını etkinleştirmek için bu komutu kullanın:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Hizmet veri yolu kuralı kimliği, bu biçiminde bir dizedir:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- Günlük analizi çalışma alanı için tanılama günlüklerini gönderilmesine izin vermek için bu komutu kullanın:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

Birden çok çıktı seçenekleri etkinleştirmek için bu parametreler birleştirebilirsiniz.

### <a name="rest-api"></a>REST API

Konusunu okuyun [Azure İzleyici REST API'sini kullanarak tanılama ayarlarını değiştirme](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Resource Manager şablonu

Konusunu okuyun [Resource Manager şablonu kullanarak kaynak oluşturmada tanılama ayarlarını etkinleştirin](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Günlük analizi akışa 
Azure SQL Database ölçümleri ve tanılama günlükleri, günlük analizi portalında veya Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyici REST API'si aracılığıyla tanılama ayarında günlük analizi etkinleştirerek yerleşik "Göndermek için günlük analizi" seçeneğini kullanarak içine gönderilebilen.

### <a name="installation-overview"></a>Yüklemeye genel bakış

Azure SQL veritabanı Donanma izleme günlük analizi ile basit bir işlemdir. Üç adım gerekli değildir:

1.  Günlük analizi kaynağı oluşturma
2.  Ölçümleri ve tanılama günlüklerini oluşturulan günlük analizi kaydetmek için veritabanlarını yapılandırın
3.  Yükleme **Azure SQL analizi** günlük analizi Galerisi'nde çözüm

### <a name="create-log-analytics-resource"></a>Günlük analizi kaynağı oluşturma

1. Tıklatın **yeni** sol menüde.
2. Tıklatın **izleme + Yönetimi**
3. Tıklatın **günlük analizi**
4. Gerekli ek bilgiler içeren günlük analizi formu doldurun: çalışma alanı adı, abonelik, kaynak grubu, konum ve fiyatlandırma katmanı.

   ![günlük analizi](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a>Kayıt ölçümleri ve tanılama günlüklerini veritabanlarını yapılandırın

Azure portalı üzerinden nerede veritabanları kendi ölçümleri kaydı yapılandırmak için en kolay yoludur. Azure portalında Azure SQL veritabanı kaynağınızın gidin ve tıklayın **tanılama ayarları**. 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a>Azure SQL analiz çözümü Galerisi'nden yükleyin  

1. Günlük analizi kaynağı oluşturulur ve verilerinizi içine akan sonra Azure SQL analiz çözümü yükleyin. Bu aracılığıyla yapılabilir **Çözümleri Galerisi** , OMS giriş sayfası ve yan menüde bulabilirsiniz. Galeride bulun ve tıklatın **Azure SQL analizi** çözümü ve tıklatın **Ekle**.

   ![İzleme çözümü](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. OMS sayfanız üzerinde yeni bir kutucuk olarak adlandırılan **Azure SQL analizi** görüntülenir. Bu kutucuğu seçerek Azure SQL analizi panosu açılır.

### <a name="using-azure-sql-analytics-solution"></a>Azure SQL analiz çözümü kullanma

Azure SQL analizi Azure SQL veritabanı kaynak hiyerarşisi aracılığıyla gitmeye izin veren hiyerarşik bir Pano ' dir. Bu özellik, üst düzey izleme yapmanıza olanak sağlar, ancak yalnızca sağ kümesine kaynakların izleme kapsamını belirlemek de sağlar.
Pano seçili kaynağın farklı kaynaklarınıza listesini içerir. Örneğin, seçili abonelik için tüm sunucular, esnek havuzlar ve seçilen aboneliğe ait veritabanları görebilirsiniz. Ayrıca, esnek havuzlar ve veritabanları için bu kaynağın kaynak kullanım ölçümleri görebilirsiniz. Bu grafik DTU, CPU, g/ç, günlük, oturumlar, çalışanlar, bağlantıları ve GB depolama içerir.

## <a name="stream-into-azure-event-hub"></a>Azure Event hub'ı akışa

Azure SQL Database ölçümleri ve tanılama günlükleri, olay hub'ı portalında veya Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyici REST API'si aracılığıyla tanılama ayarında Service Bus kural kimliği etkinleştirerek yerleşik "Bir olay hub'ına akış" seçeneğini kullanarak içine gönderilebilen. 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a>Yapılacaklar ölçümleri ve Event Hub'ındaki tanılama günlükleri ile?
Seçili verileri olay Hub'ına akışı verdikten sonra etkinleştirme için bir adım daha yaklaşarak artık izleme senaryoları Gelişmiş demektir. Event Hubs bir olay komut zincirinin "ön kapısı" olarak görev yapar ve veriler bir Event Hub'ına toplandıktan sonra herhangi bir gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak dönüştürülebilir ve depolanabilir. Event Hubs olay akışı üretimlerini bu olayların tüketilmesinden ayırır, böylece olay tüketicileri olaylara kendi zamanlamalarında erişebilir. Olay hub'ı hakkında daha fazla bilgi için bkz:

- [Azure Event Hubs nedir](../event-hubs/event-hubs-what-is-event-hubs.md)?
- [Event Hubs kullanmaya başlayın](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Akış özelliği kullanabilir birkaç yollar şunlardır:

-   Hizmet durumunu görüntülemek için Powerbı - olay hub'ı kullanarak, akış analizi ve Powerbı, "sıcak yolu" veri akış tarafından kolayca ölçümleri ve tanılama verilerinizi yakın gerçek zamanlı Öngörüler Azure hizmetlerinizi dönüştürebilirsiniz. Bir Event Hubs, akış analizi ve bir çıkış olarak kullanmak üzere Powerbı ile verileri işlemek ayarlama hakkında genel bakış için bkz: [akış analizi ve Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Akış günlükleri akışlara üçüncü taraf günlüğe kaydetme ve telemetri – kullanarak Event Hubs, akış ölçümlerinizi alabilir ve tanılama farklı üçüncü taraf izleme ve günlük analizi çözümleri günlükleri. 
-   Bir özel telemetri ve günlüğe kaydetme platformu yapı – zaten bir özel olarak geliştirilmiş telemetri platform varsa veya olan yalnızca biri, yüksek düzeyde ölçeklenebilir yapı hakkında olay hub'ları yapısını yayımlama-abone düşünüyorum esnek tanılama günlüklerini alma olanak tanır. Bkz: [bir küresel ölçekteki telemetri platform olay hub'ları kullanarak Dan Rosanova'nın kılavuzuna](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Azure depolama alanına akış

Azure SQL veritabanı ölçümleri ve tanılama günlükleri, Azure portalında veya Azure Storage Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyicisi aracılığıyla tanılama ayarı etkinleştirerek yerleşik "Depolama hesabı arşivi" seçeneğini kullanarak Azure depolama alanına depolanabilir REST API.

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a>Şema ölçümleri ve depolama hesabındaki tanılama günlükleri

Ölçümleri ve tanılama günlüklerini toplama ayarladıktan sonra bir depolama kapsayıcısı ilk veri satırı kullanılamadığında, seçtiğiniz depolama hesabı oluşturulur. Bu BLOB'ları yapıdır:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
Veya daha basit bir şekilde:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Örneğin, bir blob adı 1 dakikalık ölçümünün olabilir:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

Esnek havuz verileri kaydetmek istediğiniz durumunda, blob adı biraz farklıdır:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>İndirme ölçümleri ve Azure depolama günlükleri

Bkz: [Azure depolama biriminden ölçümleri ve tanılama günlüklerini indirin](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)

## <a name="1-minute-metrics"></a>1 dakikalık ölçümleri

| |  |
|---|---|
|**Kaynak**|**Ölçümler**|
|Database|DTU yüzdesi DTU kullanıldığında, DTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, başarılı/başarısız/engellenen Güvenlik Duvarı bağlantılarını, oturumlar yüzdesi, çalışanları yüzdesi, depolama, depolama yüzdesi, XTP depolama yüzdesi kilitlenmeleri |
|Esnek havuz|eDTU yüzde eDTU kullanıldığında, eDTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, oturumlar yüzdesi, çalışanları yüzdesi, depolama, depolama yüzdesi, depolama sınırı, XTP depolama yüzdesi |
|||

## <a name="next-steps"></a>Sonraki adımlar

- Hem de okuma [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md) ve [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) günlüğe kaydetme, ancak ölçümleri ve günlük kategorileri etkinleştirmek yalnızca nasıl anlamak için makaleleri çeşitli Azure Hizmetleri tarafından desteklenmiyor.
- Olay hub'ları hakkında bilgi edinmek için bu makaleler okuyun:
   - [Azure Event Hubs nedir](../event-hubs/event-hubs-what-is-event-hubs.md)?
   - [Event Hubs kullanmaya başlayın](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Bkz: [Azure depolama biriminden ölçümleri ve tanılama günlüklerini indirin](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
