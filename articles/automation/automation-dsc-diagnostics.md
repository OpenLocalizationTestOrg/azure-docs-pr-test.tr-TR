---
title: "Azure Otomasyonu DSC raporlama veri tooOMS günlük analizi aaaForward | Microsoft Docs"
description: "Bu makalede gösterilir nasıl toosend istenen durum raporlama veri tooMicrosoft Operations Management Suite günlük analizi toodeliver ek bilgiler ve yönetim Yapılandırma hizmeti (DSC)."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Azure Otomasyonu DSC veri tooOMS günlük analizi raporlama ilet

Automation DSC düğüm durumu veri tooyour Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı gönderebilirsiniz.  
Uyumluluk durumu hello Azure portal veya PowerShell ile tek tek DSC kaynakları düğüm yapılandırmaları ve düğümler için görülebilir. Günlük analizi ile şunları yapabilirsiniz:

* Yönetilen düğümler ve ayrı ayrı kaynaklar için uyumluluk bilgilerini alma
* Bir e-posta veya uyumluluk durumuna dayalı uyarı Tetikle
* Yönetilen düğümlere gelişmiş sorguları yazma
* Automation hesapları arasında uyumluluk durumu ilişkilendirmek
* Zaman içinde düğüm uyumluluk geçmişinizi Görselleştirme

## <a name="prerequisites"></a>Ön koşullar

Automation DSC gönderme toostart tooLog analizi raporları, gerekir:

* Kasım 2016 hello veya sonraki sürümünün [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Azure Otomasyonu hesabı. Daha fazla bilgi için bkz: [Azure Automation ile çalışmaya başlama](automation-offering-get-started.md)
* Günlük analizi çalışma alanı ile bir **otomasyon ve Denetim** hizmet teklifi. Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](../log-analytics/log-analytics-get-started.md).
* En az bir Azure Otomasyonu DSC düğümü. Daha fazla bilgi için bkz: [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Günlük analizi ile tümleştirmeyi ayarlamak

verileri Azure Automation DSC'den günlük analizi, şu adımları tam hello alma toobegin:

1. İçinde tooyour PowerShell Azure hesabında oturum açın. Bkz: [oturum oturum Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. Merhaba almak _ResourceId_ hello aşağıdaki PowerShell komutunu çalıştırarak Otomasyon hesabınızın: (birden fazla Otomasyon hesabı varsa, hello seçin _ResourceId_ istediğiniz hello hesabı tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Merhaba alma _ResourceId_ hello aşağıdaki PowerShell komutunu çalıştırarak günlük analizi çalışma alanınızın: (birden çok çalışma alanı varsa, hello seçin _ResourceId_ istediğiniz hello çalışma alanı için tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Aşağıdaki PowerShell komutunu, değiştirme çalıştırma hello `<AutomationResourceId>` ve `<WorkspaceResourceId>` hello ile _ResourceId_ değerleri hello önceki adımların her biri:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Azure Automation DSC'den günlük analizi veri alma toostop istiyorsanız, hello aşağıdaki PowerShell komutunu çalıştırın.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Merhaba DSC günlüklerini görüntüle

Automation DSC verileriniz için günlük analizi ile tümleştirme ayarladıktan sonra bir **günlük arama** düğmesi üzerinde hello görünecektir **DSC düğümleri** dikey Otomasyon hesabınızın. Merhaba tıklatın **günlük arama** düğmesini tooview hello günlükleri DSC düğümü veriler için.

![Günlük Ara düğmesi](media/automation-dsc-diagnostics/log-search-button.png)

Merhaba **günlük arama** dikey penceresi açılır ve gördüğünüz bir **DscNodeStatusData** her DSC düğümü için işlemi ve **DscResourceStatusData** işlemi her [DSC Kaynak](https://msdn.microsoft.com/powershell/dsc/resources) hello düğüm yapılandırması uygulanan toothat düğüm olarak adlandırılır.

Merhaba **DscResourceStatusData** işlemi başarısız DSC kaynakları için hata bilgilerini içerir.

Merhaba liste toosee hello verilerini her bir işlemde bu işlem için tıklatın.

[Günlük analizi arayarak. hello günlüklerini görüntüleyebilirsiniz Bkz: [Bul günlük aramaları kullanarak verileri](../log-analytics/log-analytics-log-searches.md).
Türü hello aşağıdaki sorgu toofind, DSC günlükleri:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Ayrıca, hello sorgu hello işlemi adıyla da daraltabilirsiniz. Örneğin: ' türü AzureDiagnostics ResourceProvider = = "MICROSOFT. OTOMASYON"kategorisi"DscNodeStatus"OperationName ="DscNodeStatusData"=

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>DSC uyumluluk denetimi başarısız olduğunda bir e-posta Gönder

Bir şeyler bir DSC yapılandırması yanlış gittiğinde bizim üst müşteri isteklerini hello özelliği toosend için bir e-posta veya bir metin biridir.   

toocreate bir uyarı kuralı, bir günlük arama hello uyarı çağıracağı hello DSC rapor kayıtlar için oluşturarak başlayın.  Merhaba tıklatın **uyarı** düğmesini toocreate ve hello uyarı kuralı yapılandırın.

1. Merhaba günlük analizi genel bakış sayfasında, **günlük arama**.
1. Arama hello sorgu alanına aşağıdaki hello yazarak, uyarı için bir günlük arama sorgusu oluşturun:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Birden fazla Otomasyon hesabı veya abonelik tooyour çalışma günlüklerinden ayarladıysanız uyarılarınızı aboneliği ve Automation hesabı göre gruplandırabilirsiniz.  
  Automation hesabı adını DscNodeStatusData hello arama hello kaynak alanından elde edilebilir.  
1. tooopen hello **uyarı kuralı Ekle** ekranında **uyarı** hello sayfanın üst kısmındaki hello. Başlangıç seçenekleri tooconfigure hello uyarı hakkında daha fazla bilgi için bkz: [günlük analizi uyarılarını](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Tüm düğümleri arasında başarısız DSC kaynakları bulun

Günlük analizi kullanmanın bir avantajı, düğümlere başarısız olup olmadığını denetler arayabilirsiniz ' dir.
toofind başarısız DSC kaynakları tüm örneklerini.

1. Merhaba günlük analizi genel bakış sayfasında, **günlük arama**.
1. Arama hello sorgu alanına aşağıdaki hello yazarak, uyarı için bir günlük arama sorgusu oluşturun:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Geçmiş DSC düğüm durumu görüntüle

Son olarak, zaman içinde DSC düğüm durumu geçmişi toovisualize isteyebilirsiniz.  
Bu sorgu toosearch zamanla DSC düğümü durumunuzu hello durumunun kullanabilirsiniz.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Bu grafik hello düğüm durumu zaman içinde görüntüler.

## <a name="log-analytics-records"></a>Log Analytics kayıtları

Azure Otomasyonu tanılama günlük analizi kayıtları iki kategorisi oluşturur.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Özellik | Açıklama |
| --- | --- |
| TimeGenerated |Tarih ve saat hello uyumluluk denetimi ne zaman çalıştırıldığı. |
| OperationName |DscNodeStatusData |
| ResultType |Merhaba düğümü uyumlu olup olmadığı. |
| NodeName_s |Merhaba yönetilen düğümünün Hello adı. |
| NodeComplianceStatus_s |Merhaba düğümü uyumlu olup olmadığı. |
| DscReportStatus |Olup hello uyumluluk denetimi başarıyla çalıştırıldı. |
| ConfigurationMode | Nasıl hello yapılandırma uygulanan toohello düğümdür. Olası değerler şunlardır: __"ApplyOnly"__,__"ApplyandMonitior"__, ve __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC hello yapılandırmasını uygular ve yeni bir yapılandırma toohello hedef düğüm veya bir sunucudan yeni bir yapılandırma ne zaman çekilir itildiği sürece başka hiçbir şey yapmaz. Yeni yapılandırma ilk uygulamadan sonra DSC önceden yapılandırılmış bir durumdan kayması kontrol etmez. DSC çalışır tooapply hello yapılandırma önce başarılı olana kadar __ApplyOnly__ etkisi alır. </li><li> __ApplyAndMonitor__: hello varsayılan değer budur. LCM'yi Hello yeni tüm yapılandırmaları geçerlidir. İstenen hello durumundan Hello hedef düğüm drifts yeni yapılandırma ilk uygulamadan sonra günlükleri hello tutarsızlık DSC bildirir. DSC çalışır tooapply hello yapılandırma önce başarılı olana kadar __ApplyAndMonitor__ etkisi alır.</li><li>__ApplyAndAutoCorrect__: DSC tüm yeni yapılandırmaları uygular. DSC hello hedef düğüm istenen hello durumundan drifts, yeni yapılandırma ilk uygulamadan sonra günlükleri hello tutarsızlık raporları ve hello geçerli yapılandırmasını yeniden uygular.</li></ul> |
| HostName_s | Merhaba yönetilen düğümünün Hello adı. |
| IP adresi | Merhaba Hello IPv4 adresini düğümü yönetilen. |
| Kategori | DscNodeStatus |
| Kaynak | hello Azure Automation hesabını Hello adı. |
| Tenant_g | Merhaba çağıran hello Kiracı tanımlayan GUID. |
| NodeId_g |Merhaba yönetilen düğümü tanıtan GUID. |
| DscReportId_g |Merhaba rapor tanımlar GUID. |
| LastSeenTime_t |Tarih ve saat hello rapor en son ne zaman görüntülenebilir. |
| ReportStartTime_t |Tarih ve saat hello rapor başlatıldığı. |
| ReportEndTime_t |Tarih ve saat zaman hello rapor tamamlandı. |
| NumberOfResources_d |DSC kaynakları Hello sayısı hello uygulanan yapılandırma toohello düğümünde çağrılır. |
| SourceSystem | Günlük analizi nasıl hello veri toplanmadı. Her zaman *Azure* Azure tanılama için. |
| ResourceId |Hello Azure Otomasyonu hesabını belirtir. |
| ResultDescription | Bu işlem için Hello açıklaması. |
| SubscriptionId | Merhaba hello Otomasyon hesabı için Azure aboneliği kimlik (GUID). |
| ResourceGroup | Merhaba Otomasyon hesabı hello kaynak grubunun adı. |
| ResourceProvider | MICROSOFT. OTOMASYON |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |Merhaba hello uyumluluk raporu bağıntı kimliği olan GUID. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Özellik | Açıklama |
| --- | --- |
| TimeGenerated |Tarih ve saat hello uyumluluk denetimi ne zaman çalıştırıldığı. |
| OperationName |DscResourceStatusData|
| ResultType |Merhaba kaynak uyumlu olup olmadığı. |
| NodeName_s |Merhaba yönetilen düğümünün Hello adı. |
| Kategori | DscNodeStatus |
| Kaynak | hello Azure Automation hesabını Hello adı. |
| Tenant_g | Merhaba çağıran hello Kiracı tanımlayan GUID. |
| NodeId_g |Merhaba yönetilen düğümü tanıtan GUID. |
| DscReportId_g |Merhaba rapor tanımlar GUID. |
| DscResourceId_s |Merhaba DSC kaynağı örneği Hello adı. |
| DscResourceName_s |Merhaba DSC kaynağı Hello adı. |
| DscResourceStatus_s |Merhaba DSC kaynağı uyumlu olup olmadığı. |
| DscModuleName_s |Merhaba DSC kaynağı içeren hello PowerShell modülü Hello adı. |
| DscModuleVersion_s |Merhaba DSC kaynağı içeren hello PowerShell modülü sürümü Hello. |
| DscConfigurationName_s |Merhaba yapılandırmasının Hello adı toohello düğümü uygulanır. |
| ErrorCode_s | Merhaba kaynak başarısız olursa hello hata kodu. |
| ErrorMessage_s |Merhaba kaynak başarısız olursa hello hata iletisi. |
| DscResourceDuration_d |DSC kaynağı hello saniye cinsinden Hello saat kaldı. |
| SourceSystem | Günlük analizi nasıl hello veri toplanmadı. Her zaman *Azure* Azure tanılama için. |
| ResourceId |Hello Azure Otomasyonu hesabını belirtir. |
| ResultDescription | Bu işlem için Hello açıklaması. |
| SubscriptionId | Merhaba hello Otomasyon hesabı için Azure aboneliği kimlik (GUID). |
| ResourceGroup | Merhaba Otomasyon hesabı hello kaynak grubunun adı. |
| ResourceProvider | MICROSOFT. OTOMASYON |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |Merhaba hello uyumluluk raporu bağıntı kimliği olan GUID. |

## <a name="summary"></a>Özet

Automation DSC veri tooLog Analytics göndererek hello durumunu, Automation DSC düğümleri göre daha iyi bir anlayış alabilirsiniz:

* Bir sorun olduğunda uyarıları toonotify ayarlama
* Özel görünümleri ve arama sorguları toovisualize kullanarak, runbook sonuçları, runbook iş durumu ve diğer anahtar göstergeleri veya ölçümleri ilgili.  

Günlük analizi büyük işletimsel görünürlük tooyour Automation DSC verileri sağlar ve adres olaylar daha hızlı yardımcı olabilir.  

## <a name="next-steps"></a>Sonraki adımlar

* Günlük analizi ile nasıl tooconstruct farklı arama sorguları ve gözden geçirme Automation DSC hello hakkında daha fazla oturum toolearn bakın [oturum aramaları günlük analizi](../log-analytics/log-analytics-log-searches.md)
* Azure Otomasyonu DSC kullanma hakkında daha fazla toolearn bakın [Azure Otomasyonu DSC ile çalışmaya başlama](automation-dsc-getting-started.md)
* OMS günlük analizi ve veri toplama kaynakları hakkında daha fazla toolearn bakın [toplama Azure storage veri günlük analizi genel bakış](../log-analytics/log-analytics-azure-storage.md)

