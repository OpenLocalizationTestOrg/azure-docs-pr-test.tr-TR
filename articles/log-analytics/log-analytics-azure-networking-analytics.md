---
title: "Günlük analizi ağ Analytics çözümde aaaAzure | Microsoft Docs"
description: "Hello Azure ağ analizi çözümde günlük analizi tooreview Azure ağ güvenlik grubu ve Azure uygulama ağ geçidi günlükleri kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Günlük analizi çözümlerinde izleme azure ağ iletişimi

Günlük analizi çözümleri, ağları izleme için aşağıdaki hello sunar:
* Ağ Performans İzleyicisi'ne (NPM)
 * Ağ İzleyicisi Merhaba sistem durumu
* Azure uygulama ağ geçidi analytics tooreview
 * Azure uygulama ağ geçidi günlükleri
 * Azure uygulama ağ geçidi ölçümleri
* Azure ağ güvenlik grubu analytics tooreview
 * Azure ağ güvenlik grubu günlükleri

## <a name="network-performance-monitor-npm"></a>Ağ Performans İzleyicisi'ni (NPM)

Merhaba [Ağ Performansı İzleyicisi](log-analytics-network-performance-monitor.md) yönetimi çözümüdür izleme hello sistem durumu, kullanılabilirliği ve ulaşılabilirliği ağların izler çözümü, bir ağ.  Arasında kullanılan toomonitor bağlantısı şöyledir:

* Genel Bulut ve şirket içi
* veri merkezleri ve kullanıcı konumları (şubelere)
* çok katmanlı bir uygulama çeşitli katmanlarını barındırma alt ağlar.

Daha fazla bilgi için bkz: [Ağ Performansı İzleyicisi](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure uygulama ağ geçidi ve ağ güvenlik grubu analizi
toouse hello çözümleri:
1. Merhaba yönetim çözümü tooLog Analytics, Ekle ve
2. Tanılama toodirect hello tanılama tooa günlük analizi çalışma alanı etkinleştirin. Gerekli toowrite hello günlükleri tooAzure Blob Depolama olmadığı.

Tanılama ve hello karşılık gelen çözümü birini veya her ikisini de uygulama ağ geçidi ve ağ güvenlik grupları için etkinleştirebilirsiniz.

Belirli bir kaynak türü için tanılama günlük kaydını etkinleştirmeyin, ancak hello çözümü yüklemek, hello Pano Kanatlar bu kaynak için boş ve bir hata iletisi görüntülenir.

> [!NOTE]
> Ocak 2017 ' Analytics değiştirilen uygulama ağ geçitleri ve ağ güvenlik grupları tooLog günlükleri gönderme şekilde hello desteklenir. Hello görürseniz **Azure ağ analizi (kullanım dışı)** çözüm, çok başvurmak[hello eski ağ Analytics çözüm'den geçiş](#migrating-from-the-old-networking-analytics-solution) adımları toofollow gerekir.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Veri toplama ayrıntıları ağ Azure gözden geçirin
Hello Azure uygulama ağ geçidi analytics ve hello ağ güvenlik grubu analytics Yönetimi çözümlerini doğrudan Azure uygulama ağ geçitleri ve ağ güvenlik grupları tanılama günlüklerini toplayın. Gerekli toowrite hello günlükleri tooAzure Blob Depolama değil ve aracı için veri toplama gereklidir.

Merhaba aşağıdaki tabloda veri toplama yöntemleri ve Azure uygulama ağ geçidi analizi ve hello ağ güvenlik grubu analiz için verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Platform | Doğrudan Aracısı | Systems Center Operations Manager Aracısı | Azure | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |oturum açıldığında |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Azure uygulama ağ geçidi analytics çözümüne günlük analizi

![Azure uygulama ağ geçidi Analytics simgesi](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Uygulama ağ geçitleri için günlükleri aşağıdaki hello desteklenir:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Ölçümleri aşağıdaki hello uygulama ağ geçitleri için desteklenir:

* 5 dakikalık işleme

### <a name="install-and-configure-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Aşağıdaki yönergeler tooinstall hello kullanın ve hello Azure uygulama ağ geçidi analiz çözümü yapılandırın:

1. Hello Azure uygulama ağ geçidi analytics çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Hello için tanılama günlüğünü etkinleştirme [uygulama ağ geçitleri](../application-gateway/application-gateway-diagnostics.md) toomonitor istiyor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Azure uygulama ağ geçidi tanılama hello portalında etkinleştir

1. Toohello uygulama ağ geçidi kaynak toomonitor Hello Azure portalına gidin
2. Seçin *tanılama günlükleri* sayfası aşağıdaki tooopen hello

   ![Azure uygulama ağ geçidi kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Tıklatın *tanılamayı açın* sayfası aşağıdaki tooopen hello

   ![Azure uygulama ağ geçidi kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. Tanılama üzerinde tooturn tıklatın *üzerinde* altında *durumu*
5. Merhaba onay kutusunu tıklatın *tooLog Analytics Gönder*
6. Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma
7. Altında Hello onay kutusuna tıklayın **günlük** her hello günlük türleri toocollect
8. Tıklatın *kaydetmek* tooenable hello günlüğe tanılama tooLog analizi

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>PowerShell kullanarak Azure Ağ Tanılama'yı etkinleştir

PowerShell Betiği aşağıdaki hello nasıl bir örnek sağlar tooenable uygulama ağ geçitleri için günlüğü tanılama.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Azure uygulama ağ geçidi analytics kullanın
![Azure uygulama ağ geçidi analytics döşeme görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Merhaba tıklattıktan sonra **Azure uygulama ağ geçidi analytics** döşeme hello genel bakış, günlüklerinizi özetlerini görüntüleyin ve kategorileri aşağıdaki hello toodetails içinde ayrıntıya gidin:

* Uygulama ağ geçidi erişimi günlükleri
  * Uygulama ağ geçidi erişim günlükleri için istemci ve sunucu hataları
  * Her uygulama ağ geçidi için saat başına istek sayısı
  * Saat başına istekleri her uygulama ağ geçidi için başarısız oldu
  * Uygulama ağ geçitleri için kullanıcı aracısı tarafından hataları
* Uygulama ağ geçidi performansı
  * Uygulama ağ geçidi ana bilgisayar durumu
  * Uygulama ağ geçidi için en yüksek ve 95 yüzdebirlik başarısız istekleri

![Azure uygulama ağ geçidi analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure uygulama ağ geçidi analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

Merhaba üzerinde **Azure uygulama ağ geçidi analytics** panoyu hello Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview ayrıntılı hello günlük arama sayfası hakkında bilgi.

Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz. Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Günlük analizi analytics çözümde Azure ağ güvenlik grubu

![Azure ağ güvenlik grubu Analytics simgesi](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Ağ güvenlik grupları için günlükleri aşağıdaki hello desteklenir:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Aşağıdaki yönergeler tooinstall hello kullanın ve hello Azure ağ analiz çözümü yapılandırın:

1. Hello Azure ağ güvenlik grubu analytics çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Hello için tanılama günlüğünü etkinleştirme [ağ güvenlik grubu](../virtual-network/virtual-network-nsg-manage-log.md) toomonitor istediğiniz kaynakları.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Azure ağ güvenlik grubu tanılama hello portalında etkinleştir

1. Toohello ağ güvenlik grubu kaynak toomonitor Hello Azure portalına gidin
2. Seçin *tanılama günlükleri* sayfası aşağıdaki tooopen hello

   ![Azure ağ güvenlik grubu kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Tıklatın *tanılamayı açın* sayfası aşağıdaki tooopen hello

   ![Azure ağ güvenlik grubu kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. Tanılama üzerinde tooturn tıklatın *üzerinde* altında *durumu*
5. Merhaba onay kutusunu tıklatın *tooLog Analytics Gönder*
6. Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma
7. Altında Hello onay kutusuna tıklayın **günlük** her hello günlük türleri toocollect
8. Tıklatın *kaydetmek* tooenable hello günlüğe tanılama tooLog analizi

### <a name="enable-azure-network-diagnostics-using-powershell"></a>PowerShell kullanarak Azure Ağ Tanılama'yı etkinleştir

PowerShell Betiği aşağıdaki hello nasıl bir örnek sağlar tooenable ağ güvenlik grupları için günlük kaydı tanılama
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Azure ağ güvenlik grubu kullanın analizi
Merhaba tıklattıktan sonra **Azure ağ güvenlik grubu analytics** döşeme hello genel bakış, günlüklerinizi özetlerini görüntüleyin ve kategorileri aşağıdaki hello toodetails içinde ayrıntıya gidin:

* Ağ güvenlik grubu akışları engellendi
  * Ağ güvenlik grubu kural engellenen akışlarıyla
  * Engellenen akışlarıyla MAC adresleri
* Ağ güvenlik grubu akışları izin
  * İzin verilen akışları ile ağ güvenlik grubu kuralları
  * İzin verilen akışlarıyla MAC adresleri

![Azure ağ güvenlik grubu analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure ağ güvenlik grubu analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

Merhaba üzerinde **Azure ağ güvenlik grubu analytics** panoyu hello Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview ayrıntılı hello günlük arama sayfası hakkında bilgi.

Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz. Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Merhaba eski ağ Analytics çözüm'den geçiş
Ocak 2017 ' Analytics değiştirilen Azure uygulama ağ geçitleri ve Azure ağ güvenlik grupları tooLog günlükleri gönderme şekilde hello desteklenir. Bu değişiklikler hello aşağıdaki avantajları sağlar:
+ TooLog Analytics hello olmadan gereken doğrudan toouse bir depolama hesabı günlüklerine yazılır
+ Günlük analizi kullanılabilir olmasını durduracak toothem günlükleri olduğunda hello zamandan daha az gecikme oluşturulan
+ Daha az yapılandırma adımları
+ Azure tanılama tüm türleri için ortak bir biçimi

toouse hello çözümleri güncelleştirildi:

1. [Azure uygulama Gateway bileşenlerinden tooLog Analytics doğrudan gönderilen tanılama toobe yapılandırın](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Doğrudan Azure ağ güvenlik gruplarındaki tooLog Analytics gönderilen tanılama toobe yapılandırın](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Merhaba etkinleştirmek *Azure uygulama ağ geçidi Analytics* ve hello *Azure ağ güvenlik grubu Analytics* hello işlemi kullanarak çözüm açıklanan [eklemek günlük analizi çözümleri Merhaba Çözümleri Galerisi](log-analytics-add-solutions.md)
3. Tüm kayıtlı sorgu, panolar veya uyarıları toouse hello yeni veri türü güncelleştirme
  + TooAzureDiagnostics türüdür. Merhaba ResourceType toofilter tooAzure ağ günlüklerini kullanabilir.

    | Onun yerine: | Kullanım: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Sonekine sahip herhangi bir alan için \_s, \_d veya \_g hello adı hello ilk karakter toolower harf durumunu değiştir
   + Sonekine sahip herhangi bir alan için \_adında, hello veri o iç içe geçmiş hello alan adlarını temel alarak tek tek alanlara bölünür.
4. Merhaba kaldırmak *Azure ağ analizi (kullanım dışı)* çözümü.
  + PowerShell kullanıyorsanız, kullanın`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Merhaba değişiklik hello yeni çözümde görünür değil önce veri toplanmadı. Bu verileri kullanarak hello için eski türü ve alan adları tooquery devam edebilirsiniz.

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Azure Tanılama verileri.
