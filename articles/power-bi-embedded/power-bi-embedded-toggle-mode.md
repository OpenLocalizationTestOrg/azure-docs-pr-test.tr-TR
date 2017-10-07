---
title: "Azure Power BI Embedded raporlarda görüntüleme ve düzenleme modu arasında aaaToggle | Microsoft Docs"
description: "Bilgi nasıl tootoggle raporlarınızı Power BI Embedded içinde için görüntüleme ve düzenleme modu arasında."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>Görünüm arasında geçiş yapmak ve Power BI Embedded raporlarda modunu düzenleyin

Bilgi nasıl tootoggle raporlarınızı Power BI Embedded içinde için görüntüleme ve düzenleme modu arasında.

## <a name="creating-an-access-token"></a>Bir erişim belirteci oluşturma

Toocreate hello özelliği tooboth görüntüleme ve düzenleme bir rapor veren bir erişim belirteci gerekir. tooedit ve bir raporu hello gerekir **Report.ReadWrite** belirteci izni. Daha fazla bilgi için bkz: [Authenticating ve Power BI Embedded yetkilendirme](power-bi-embedded-app-token-flow.md).

> [!NOTE]
> Bu tooedit izin ver ve tooan varolan rapor değişiklikleri kaydedin. Ayrıca destekleme hello işlevi isterseniz **Kaydet**, toosupply ek izinler gerekir. Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes).

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>Yapılandırma katıştırma

Toosupply izinleri ve viewMode sipariş toosee hello Kaydet düğmesine düzenleme modunda de gerekir. Daha fazla bilgi için bkz: [yapılandırma ayrıntılarını katıştırmak](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

Bu temel görünüm modunda tooembed hello rapor gösterecektir **viewMode** çok ayarlanan**modeller. ViewMode.View**.

## <a name="view-mode"></a>Görünüm modu

Düzenleme modunda olduğunda, görünüm moduna JavaScript tooswitch aşağıdaki hello kullanabilirsiniz.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>Düzenleme modu

Görünüm modu değilseniz JavaScript tooswitch düzenleme moduna aşağıdaki hello kullanabilirsiniz.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>Ayrıca bkz.

[Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Rapor ekleme](power-bi-embedded-embed-report.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Powerbı CSharp Git deposu](https://github.com/Microsoft/PowerBI-CSharp)  
[Powerbı düğümlü Git deposu](https://github.com/Microsoft/PowerBI-Node)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)
