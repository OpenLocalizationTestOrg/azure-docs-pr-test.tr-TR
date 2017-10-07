---
title: Azure Power BI Embedded aaaSave raporlarda | Microsoft Docs
description: "Power BI içinde toosave raporları nasıl katıştırılmış öğrenin. Bu sipariş toowork uygun izinleri başarıyla gerektirir."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>Raporlar Power BI Embedded Kaydet

Power BI içinde toosave raporları nasıl katıştırılmış öğrenin. Bu sipariş toowork uygun izinleri başarıyla gerektirir.

Power BI Embedded içinde varolan raporları düzenleyebilir ve kaydedebilirsiniz. Ayrıca, yeni bir rapor oluşturmak ve bir yeni raporu toocreate bir kaydedin.

Sipariş toosave bir rapor önce toocreate bir belirteç hello sağ kapsamlarla hello belirli rapor için gerekir:

* tooenable Report.ReadWrite kapsam kaydetme gereklidir
* olarak tooenable kaydetme Report.Read ve Workspace.Report.Copy kapsamları gereklidir
* tooenable kaydedin ve kaydetme, Report.ReadWrite ve Workspace.Report.Copy gerekli

Embed rapor hello zaman sırasıyla sipariş tooenable hello kaydetme/Kaydet doğru dosya menüsünden düğmeleri gibi tooprovide hello hello Embed yapılandırma izni hemen:

* modeller. Permissions.ReadWrite
* modeller. Permissions.Copy
* modeller. Permissions.All

> [!NOTE]
> Erişim belirteci hello uygun kapsamları da gerekir. Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Rapor düzenleme modunda ekleme

Şimdi tooEmbed bir rapor düzenleme modunda uygulamanızı içinde deyin istediğiniz, toodo böylece yalnızca Embed yapılandırmasında hello hakkı özellikleri geçirmek ve powerbi.embed() çağırın. Düğmeleri düzenleme modunda olarak toosupply izinleri ve viewMode sipariş toosee hello kaydetmek ve kaydetme de gerekir. Daha fazla bilgi için bkz: [yapılandırma ayrıntılarını katıştırmak](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

JavaScript'te örneğin:

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

Şimdi bir rapor düzenleme modunda, uygulamanızda katıştırılır.

## <a name="save-report"></a>Raporu kaydetme

Embbeding hello raporda düzenledikten sonra hello sağ belirteci ve izinleri moduyla hello Dosya menüsünden veya javascript hello rapor kaydedebilirsiniz:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Farklı kaydet

```
// Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> Yalnızca sonra *Farklı Kaydet* oluşturulan yeni bir rapor. Merhaba kaydettikten sonra hello tuvale hala hello eski rapor düzenleme modu ve değil hello yeni raporu gösteriliyor. Oluşturulan tooembed hello yeni rapor gerekir. Bu, rapor oluşturuldukça yeni bir erişim belirteci gerektirir.

Ardından tooload hello sonra yeni bir rapor gerekir bir *Farklı Kaydet*. Bu benzer tooembedding bir rapordur.

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a>Ayrıca bkz.

[Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Rapor ekleme](power-bi-embedded-embed-report.md)  
[Veri kümesinden yeni rapor oluşturma](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)

