---
title: "Azure Hizmetleri - PowerShell aaaCreate uyarıları | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Ölçüm uyarılar Azure İzleyicisi'nde Azure Hizmetleri - PowerShell oluşturabilir.
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Genel Bakış
Bu makalede, Azure ölçüm yukarı tooset PowerShell kullanarak nasıl uyarıları gösterir.  

İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.

* **Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler. Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.    
* **Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur. Etkinlik günlüğü Uyarıları hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts.md)

Tetikler olduğunda bir uyarı ölçüm toodo hello aşağıdaki yapılandırabilirsiniz:

* e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder
* e-posta, belirttiğiniz tooadditional e-postalar gönderin.
* bir Web kancası çağırın
* bir Azure runbook'tan (yalnızca Azure portal hello) yürütülmesini Başlat

Yapılandırma ve uyarı kuralları kullanma hakkında bilgi edinin

* [Azure portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [komut satırı arabirimi (CLI)](insights-alerts-command-line-interface.md)
* [Azure monitör REST API'si](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Ek bilgi için her zaman yazabilirsiniz ```Get-Help``` ve PowerShell komutunu hakkında Yardım istediğiniz hello.

## <a name="create-alert-rules-in-powershell"></a>PowerShell'de uyarı kuralları oluşturma
1. TooAzure oturum açın.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Bir listesini almak hello abonelikleri sahip olduğunuz kullanılabilir. Merhaba doğru aboneliği çalıştığını doğrulayın. Aksi takdirde, toohello sağa bir ayarla hello çıktısını kullanarak `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. toolist var olan bir kaynak grubu kurallarında hello aşağıdaki komutu kullanın:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. bir kural toocreate toohave birkaç önemli bilgi parçasından önce gerekir.

  * Merhaba **kaynak kimliği** hello kaynak için bir uyarı tooset istiyor
  * Merhaba **ölçüm tanımlarını** kaynağı için kullanılabilir

     Tek yönlü tooget hello kaynak kimliği toouse hello Azure portal ' dir. Merhaba kaynak zaten oluşturulmuş olduğu varsayılarak, hello Portalı'nda seçin. Merhaba sonraki dikey penceresinde, ardından *özellikleri* hello altında *ayarları* bölümü. **Kaynak Kimliği** hello sonraki dikey penceresinde bir alandır. Başka bir yoldur toouse hello [Azure kaynak Gezgini](https://resources.azure.com/).

     Bir web uygulaması için bir örnek kaynak kimliği

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Kullanabileceğiniz `Get-AzureRmMetricDefinition` tooview hello belirli bir kaynak için tüm ölçüm açıklamalarının listesi.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Hello aşağıdaki örnek tablo hello ölçüm adı ile ve bu ölçümü için hello birim oluşturur.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Get-AzureRmMetricDefinition için kullanılabilir seçenekleri tam bir listesi, Get-MetricDefinitions çalıştırarak kullanılabilir.
5. bir web sitesi kaynakta bir uyarı örnek ayarlar aşağıdaki hello. 5 dakikada bir ve yeniden zaman 5 dakika boyunca hiçbir trafik aldığı için herhangi bir trafik tutarlı bir şekilde aldığı zaman hello uyarı tetikler.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. bir uyarıyı tetikleyen zaman toocreate Web kancası veya gönderme e-posta, hello e-posta ve/veya Web kancalarını önce oluşturun. Merhaba kural daha sonra hemen oluştururken hello - Eylemler etiketi ve hello aşağıdaki örnekte gösterildiği gibi. Web kancası veya e-posta zaten kuralları PowerShell aracılığıyla oluşturulan ilişkilendiremezsiniz.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. uyarılarınızı düzgün şekilde hello tek tek kurallarında bakarak oluşturulduğunu tooverify.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Uyarılarınızı silin. Bu komutlar, bu makalede daha önce oluşturduğunuz hello kuralları silin.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Sonraki adımlar
* [Azure izleme genel bir bakış elde](monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.
* Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).
* Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).
* Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).
* Alma bir [tanılama günlüklerinin toplanması genel bakış](monitoring-overview-of-diagnostic-logs.md) toocollect ayrıntılı hizmetinizi yüksek sıklıkta ölçümleri.
* Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
