---
title: "aaaMonitor Azure İzleyicisi ile API Management | Microsoft Docs"
description: "Nasıl toomonitor Azure API Management hizmet Azure İzleyicisi'ni kullanma hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Azure İzleyicisi ile İzleyici API Yönetimi
Azure İzleyicisi tüm Azure kaynakları izlemek için tek bir kaynak sağlayan bir Azure hizmetidir. Azure izleme ile görselleştirme, sorgulama yapabilir, yönlendirmek, arşiv ve hello ölçümleri ve API Management gibi Azure kaynakları'ten gelen günlükleri eylemleri gerçekleştirin. 

Video gösterileri nasıl aşağıdaki hello toomonitor API Azure İzleyicisi'ni kullanarak yönetim. Azure İzleyicisi hakkında daha fazla bilgi için bkz: [Azure İzleyicisi ile çalışmaya başlama]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Ölçümler
API Management anda beş ölçümleri yayar ve biz tooadd hello gelecekte daha fazla planlayın. Bu ölçümleri her dakika hello durumu ve Apı'lerinizi durumunu gerçek zamanlı görünürlük yakın vermiş gösterilen. Merhaba ölçümleri bir özeti aşağıda verilmiştir:
* : Toplam ağ geçidi API hello sayısı hello dönemde istekleri. 
* Başarılı ağ geçidi istekleri: 304, 307 ve 301 (örneğin, 200) daha küçük bir şey de dahil olmak üzere başarılı HTTP yanıt kodları alınan API istek hello sayısı. 
* Ağ geçidi isteği başarısız oldu: hello hatalı HTTP yanıt kodu 400 ve 500'den büyük herhangi bir şey de dahil olmak üzere alınan API istek sayısı.
* Yetkisiz ağ geçidi istekleri: HTTP yanıt kodları 401, 403 ve 429 dahil alınan API istek hello sayısı. 
* Diğer ağ geçidi istekleri: Kategoriler (örneğin, 418) önceki hello tooany ait değil HTTP yanıt kodları alınan API istek hello sayısı.

API Management hizmetiniz ölçümlerini ya da Azure İzleyicisi'nde tüm Azure kaynaklarına erişim ölçümlerini erişebilir. API Management hizmetiniz tooview ölçümlerini:
1. Açık hello Azure portalı.
2. Tooyour API Management hizmeti gidin.
3. Tıklatın **ölçümleri**.

![Ölçüm dikey penceresi][metrics-blade]

Hakkında daha fazla bilgi için toouse ölçümler görmek [genel bakış, ölçümleri].

## <a name="activity-logs"></a>Etkinlik Günlükleri
Etkinlik günlükleri, API Management services üzerinde gerçekleştirilen hello işlemlerinin bir anlayış sağlar. Daha önce "denetim günlüklerini" veya "işletimsel logs" olarak bilinirdi. Etkinlik Günlükleri'ni kullanarak hello belirleyebilirsiniz "ne, kimin, ne zaman ve" herhangi bir yazma, API Management hizmetlerde yapılan işlemleri (PUT, POST, DELETE) için. 

> [!NOTE]
> Etkinlik günlükleri okuma (GET) işlemleri veya başlığında gerçekleştirilen işlemleri dahil değil Klasik yayımcı portalı hello veya hello özgün yönetim API'leri kullanılarak.

API Management hizmetiniz etkinlik günlükleri erişmek veya günlükleri, Azure kaynaklarınızın Azure İzleyicisi'nde erişim. API Management hizmetiniz tooview etkinliğini kaydeder:
1. Açık hello Azure portalı.
2. Tooyour API Management hizmeti gidin.
3. Tıklatın **etkinlik günlüğü**.

![Etkinlik günlükleri dikey penceresi][activity-logs-blade]

Hakkında daha fazla bilgi için toouse ölçümler görmek [etkinlik günlükleri genel bakış].

## <a name="alerts"></a>Uyarılar
Ölçümleri ve etkinlik açtığında temelinde tooreceive uyarılar yapılandırabilirsiniz. Azure İzleyici tetikler olduğunda bir uyarı toodo hello aşağıdaki tooconfigure sağlar:

* Bir e-posta bildirimi gönder
* bir Web kancası çağırın
* Bir Azure mantıksal uygulamayı çağırmak

API Management hizmetiniz veya Azure İzleyicisi uyarı kuralları yapılandırabilirsiniz. tooconfigure API Management bunları: 
1. Açık hello Azure portalı.
2. Tooyour API Management hizmeti gidin.
3. Tıklatın **uyarı kuralları**.

![Uyarı kuralları dikey penceresi][alert-rules-blade]

Uyarıları kullanma hakkında daha fazla bilgi için bkz: [genel bakış, uyarıları].

## <a name="diagnostic-logs"></a>Tanılama Günlükleri
Tanılama günlüklerini işlemleri ve denetim yanı sıra sorun giderme amacıyla önemli hataları hakkında zengin bilgi sağlar. Tanılama günlükleri, etkinlik günlükleri farklılık gösterir. Etkinlik günlükleri Azure kaynaklarınızı üzerinde gerçekleştirilen hello işlemlerinin fikir sağlar. Tanılama günlükleri işlemleri kaynağınız kendisini gerçekleştirilen bir anlayış sağlar.

API Management anda tanılama sağlar (saatlik toplu hale) günlükleri ayrı API'si hakkında isteği yapı izlenerek hello sahip her girişi:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

API Management hizmetiniz tanılama günlüklerine erişmek veya günlükleri, Azure kaynaklarınızın Azure İzleyicisi'nde erişim. API Management hizmetiniz tanılama günlüklerine tooview:
1. Açık hello Azure portalı.
2. Tooyour API Management hizmeti gidin.
3. Tıklatın **tanılama günlük**.

![Tanılama günlükleri dikey penceresi][diagnostic-logs-blade]

Hakkında daha fazla bilgi için toouse ölçümler görmek [tanılama günlükleri'ne genel bakış].

## <a name="next-step"></a>Sonraki adım

* [Azure İzleyicisi ile çalışmaya başlama]
* [genel bakış, ölçümleri]
* [etkinlik günlükleri genel bakış]
* [tanılama günlükleri'ne genel bakış]
* [genel bakış, uyarıları]

[Azure İzleyicisi ile çalışmaya başlama]: ../monitoring-and-diagnostics/monitoring-get-started.md
[genel bakış, ölçümleri]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[etkinlik günlükleri genel bakış]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[tanılama günlükleri'ne genel bakış]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[genel bakış, uyarıları]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
