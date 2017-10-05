---
title: "Raporları Azure Power BI Embedded kaydetmek | Microsoft Docs"
description: "Power BI embedded içinde raporları kaydetmek öğrenin. Bu, başarılı bir şekilde çalışması için uygun izinleri gerektirir."
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
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>Raporlar Power BI Embedded Kaydet

Power BI embedded içinde raporları kaydetmek öğrenin. Bu, başarılı bir şekilde çalışması için uygun izinleri gerektirir.

Power BI Embedded içinde varolan raporları düzenleyebilir ve kaydedebilirsiniz. Ayrıca, yeni bir rapor oluşturmak ve oluşturmak için yeni bir rapor olarak kaydedin.

Bir raporu kaydetmek için önce belirli bir rapor için bir belirteç sağ kapsamlarla oluşturmanız gerekir:

* Report.ReadWrite etkinleştirmek için kapsam gereklidir
* Kaydetme etkinleştirmek için Report.Read ve Workspace.Report.Copy kapsamları gereklidir
* Report.ReadWrite ve Workspace.Report.Copy gerekli olduğu gibi kaydetme ve kaydetme etkinleştirmek için

Sırasıyla sağ etkinleştirmek için raporun katıştırma Embed yapılandırmasında doğru iznin sağlamanız gereken dosya menüsü düğmeleri farklı kaydet/Kaydet:

* modeller. Permissions.ReadWrite
* modeller. Permissions.Copy
* modeller. Permissions.All

> [!NOTE]
> Erişim belirteci uygun kapsamları da gerekir. Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Rapor düzenleme modunda ekleme

Bu nedenle yalnızca Embed yapılandırmasında hakkı özellikleri geçirmek ve powerbi.embed() çağırmak için uygulamanızın içinde düzenleme modunda bir rapor eklemek istediğiniz varsayalım. İzinler ve bir viewMode kaydetme görmeniz için sağlamanız gerekir ve gibi durumlarda düğmeleri Kaydet düzenleme modunda. Daha fazla bilgi için bkz: [yapılandırma ayrıntılarını katıştırmak](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

JavaScript'te örneğin:

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
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

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

Şimdi bir rapor düzenleme modunda, uygulamanızda katıştırılır.

## <a name="save-report"></a>Raporu kaydetme

Raporda Embbeding sonra Dosya menüsünden veya javascript rapor kaydedebilirsiniz izinleri ve doğru belirteci moduyla düzenleyin:

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Farklı kaydet

```
// Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> Yalnızca sonra *Farklı Kaydet* oluşturulan yeni bir rapor. Kaydetme sonra tuvale hala eski rapor düzenleme modunu ve yeni rapor göstermez. Oluşturulan yeni rapor eklemek gerekir. Bu, rapor oluşturuldukça yeni bir erişim belirteci gerektirir.

Ardından yeni raporun sonra Yük gerekir bir *Farklı Kaydet*. Bu, herhangi bir raporu katıştırmak için benzer.

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
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
Başka sorunuz mu var? [Power BI Topluluğu'nu deneyin](http://community.powerbi.com/)

