---
title: "Application Insights'te aaaUse Powershell tooset uyarıları | Microsoft Docs"
description: "Application Insights tooget e-postaların ölçüm değişiklikler hakkında yapılandırma otomatikleştirin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Application Insights'ta PowerShell tooset uyarıları kullanın
Merhaba yapılandırmasını otomatik hale getirebilirsiniz [uyarıları](app-insights-alerts.md) içinde [Application Insights](app-insights-overview.md).

Buna ek olarak, şunları yapabilirsiniz [kancalarını tooautomate yanıt tooan Uyarınız ayarlamak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Toocreate kaynakları ve uyarılara istiyorsanız aynı hello saat, göz önünde bulundurun [bir Azure Resource Manager şablonu kullanarak](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Tek seferlik Kurulumu
Önce Azure aboneliğinizle PowerShell kullanmadıysanız:

Hello Azure Powershell modülü toorun hello betikleri istediğiniz hello makineye yükleyin.

* Yükleme [Microsoft Web Platformu Yükleyicisi (v5 veya üzeri)](http://www.microsoft.com/web/downloads/platform.aspx).
* Microsoft Azure Powershell tooinstall kullanın

## <a name="connect-tooazure"></a>TooAzure Bağlan
Azure PowerShell'i başlatın ve [tooyour abonelik bağlanmak](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Uyarıları alma
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Uyarı ekleme
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Örnek 1
Merhaba sunucunun yanıt tooHTTP isteği, üzerinde 5 dakika ortalaması 1 saniyeden daha yavaş ise bana e-posta. My Application Insights kaynağı IceCreamWebApp denir ve Fabrikam kaynak grubunda bulunuyor. Hello Azure aboneliği hello sahibi ben.

Merhaba GUID hello abonelik kimliği (değil hello izleme anahtarını hello uygulamasının) olur.

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Örnek 2
Bir uygulama içinde kullanmam sahip [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport "salesPerHour." adlı bir ölçüm "SalesPerHour" üzerinde 24 saat ortalaması 100 düşerse toomy iş arkadaşlarınızı bir e-posta gönderin.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

aynı kural hello ölçüm için kullanılabilir hello bildirilen hello kullanarak [ölçüm parametresi](app-insights-api-custom-events-metrics.md#properties) TrackEvent veya trackPageView gibi başka bir izleme çağrısı.

## <a name="metric-names"></a>Ölçüm adları
| Ölçüm adı | Ekran adı | Açıklama |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Tarayıcı özel durumları |Merhaba tarayıcıda oluşturulan Yakalanmayan Özel durumların sayısı. |
| `basicExceptionServer.count` |Sunucu özel durumları |Merhaba uygulama tarafından oluşturulan işlenmemiş özel durum sayısı |
| `clientPerformance.clientProcess.value` |İstemci işlem süresi |Merhaba DOM yüklenene kadar belgeyi son baytını hello alma arasındaki süre. Zaman uyumsuz isteği hala işliyor olabilir. |
| `clientPerformance.networkConnection.value` |Sayfa yükleme ağ bağlantı süresi |Zaman hello tarayıcı tooconnect toohello ağ alır. Önbelleğe alınmış 0 olabilir. |
| `clientPerformance.receiveRequest.value` |Alıcı yanıt süresi |İstek toostarting tooreceive yanıtı göndermeyi tarayıcı arasındaki süre. |
| `clientPerformance.sendRequest.value` |İstek süresi Gönder |Tarayıcı toosend isteği tarafından harcanan süre. |
| `clientPerformance.total.value` |Tarayıcı sayfa yükleme süresi |DOM, stil sayfaları, betikler ve görüntüleri yüklenene kadar kullanıcı isteği süresi. |
| `performanceCounter.available_bytes.value` |Kullanılabilir bellek |Bir işlem veya sistem kullanımı için hemen kullanılabilir fiziksel bellek. |
| `performanceCounter.io_data_bytes_per_sec.value` |İşlemin g/ç hızı |İkinci okuma ve yazılı toofiles, ağ ve aygıt başına toplam bayt sayısı. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |özel durum oranı |Saniye başına oluşturulan özel durumları. |
| `performanceCounter.percentage_processor_time.value` |İşlem CPU |Merhaba işlemci tooexecution yönergeleri ile Merhaba uygulamaları işlemi için kullanılan tüm işlem iş parçacıklarının geçen sürenin yüzdesini Hello. |
| `performanceCounter.percentage_processor_total.value` |İşlemci zamanı |Merhaba hello işlemci zamanı yüzdesi, boş olmayan iş parçacıklarında harcadığı. |
| `performanceCounter.process_private_bytes.value` |İşlem özel bayt sayısı |Özel olarak toohello atanan bellek uygulamanın işlemleri izlenen. |
| `performanceCounter.request_execution_time.value` |ASP.NET isteği yürütme süresi |Merhaba en son isteği yürütme süresi. |
| `performanceCounter.requests_in_application_queue.value` |ASP.NET isteklerini yürütme kuyruğundaki |Merhaba uygulama istek sırası uzunluğu. |
| `performanceCounter.requests_per_sec.value` |ASP.NET isteği hızı |ASP.NET tarafından saniye başına toohello uygulama isteklerinin tüm hızı. |
| `remoteDependencyFailed.durationMetric.count` |Bağımlılık hataları |Merhaba sunucu uygulama tooexternal kaynakları tarafından yapılan başarısız çağrı sayısı. |
| `request.duration` |Sunucu yanıt süresi |Bir HTTP isteği alma ve hello yanıtı göndermeyi bitirmeden arasındaki süre. |
| `request.rate` |İstek oranı |Saniye başına tüm istekleri toohello uygulamasının oranı. |
| `requestFailed.count` |Başarısız istekler |Bir yanıt kodu ile sonuçlandı sayısı, HTTP isteklerini > = 400 |
| `view.count` |Sayfa görünümleri |Bir web sayfası için istemci kullanıcı isteklerini sayısı. Yapay trafiği filtrelenmelidir. |
| {, özel ölçüm adı} |{Ölçüm adı} |Ölçüm değeri tarafından bildirilen [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) veya hello [izleme çağrı ölçümleri parametresinin](app-insights-api-custom-events-metrics.md#properties). |

Merhaba ölçümleri farklı telemetri modülleri tarafından gönderilir:

| Ölçüm grubu | Toplayıcı Modülü |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>görünüm |[Tarayıcı JavaScript](app-insights-javascript.md) |
| performanceCounter |[Performans](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Bağımlılık](app-insights-configuration-with-applicationinsights-config.md) |
| isteği<br/>requestFailed |[Sunucu isteği](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Web kancaları
Yapabilecekleriniz [yanıt tooan Uyarınız otomatikleştirmek](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Bir uyarı ortaya çıktığında azure tercih ettiğiniz bir web adresini çağırır.

## <a name="see-also"></a>Ayrıca bkz.
* [Komut dosyası tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Application Insights ve web test kaynakları Şablondan Oluştur](app-insights-powershell.md)
* [Microsoft Azure tanılama tooApplication Öngörüler Kuplaj otomatikleştirme](app-insights-powershell-azure-diagnostics.md)
* [Yanıt tooan Uyarınız otomatikleştirme](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
