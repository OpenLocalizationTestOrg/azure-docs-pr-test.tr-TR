---
title: "Azure Power BI Embedded'de kümesinden yeni bir rapor aaaCreate | Microsoft Docs"
description: "Power BI Embedded raporları, kendi uygulamanızda kümesinden şimdi oluşturulabilir."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Power BI Embedded'de kümesinden yeni rapor oluşturma

Power BI Embedded raporları, kendi uygulamanızda kümesinden şimdi oluşturulabilir. 

Merhaba kimlik doğrulama yöntemini benzer toothat raporunun ekleme. Belirli tooa dataset olan erişim belirteçleri dayanır. Azure Active Directory (AAD tarafından) verilen belirteçler PowerBI.com için kullanılan ve Power BI Embedded belirteçleri kendi hizmeti tarafından verilir.

Yayınlanan belirteçleri createing katıştırılmış rapor hello için belirli bir veri kümesi olur. Belirteçleri ilişkili URL ile Merhaba katıştırmak hello üzerinde aynı öğesi tooensure her benzersiz belirtece sahip. İçinde katıştırılmış rapor toocreate sipariş *Dataset.Read ve Workspace.Report.Create* kapsamları hello erişim belirtecinde yer sağlanmalıdır.

## <a name="create-access-token-needed-toocreate-new-report"></a>Erişim belirteci gerekli toocreate yeni rapor oluşturma

Power BI Embedded kullanır ekleme belirteci, JSON Web belirteçlerini imzalı HMAC olduğu. Merhaba belirteçleri hello erişim anahtarıyla Azure Power BI Embedded çalışma alanı koleksiyonu imzalanmıştır. Varsayılan olarak belirteçleri, ekleme, olan okuma kullanılan tooprovide yalnızca erişim tooa rapor tooembed bir uygulamaya. Embed belirteçleri için belirli bir rapor verilir ve bir embed URL'si ile ilişkili olmalıdır.

Merhaba erişim tuşları kullanılan toosign/şifrelemek hello belirteçleri gibi erişim belirteçleri hello sunucusunda oluşturulmalıdır. Hakkında bilgi için bkz: toocreate bir erişim belirteci [Authenticating ve Power BI Embedded ile yetkilendirme](power-bi-embedded-app-token-flow.md). Merhaba gözden geçirebilirsiniz [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemi. Burada, ne için Power BI hello .NET SDK kullanarak gibi görünür bir örnek verilmiştir.

Bu örnekte, toocreat hello yeni rapor üzerinde istiyoruz bizim veri kümesi tanıtıcısı sahip. Ayrıca tooadd hello kapsamları için ihtiyacımız *Dataset.Read ve Workspace.Report.Create*.

Merhaba *PowerBIToken sınıfı* hello yüklemenizi gerektirir [Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**NuGet paketi yüklemesi**

```
Install-Package Microsoft.PowerBI.Core
```

**C# kodu**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Yeni boş bir rapor oluşturun

Sipariş toocreate yeni bir rapor, hello oluşturma yapılandırması sağlanmalıdır. Bu toocreate hello raporun, karşılarında istediğimiz hello erişim belirteci, hello embedURL ve hello Datasetıd içermelidir. Bu hello nuget yüklemenizi gerektirir [Power BI JavaScript paket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Merhaba embedUrl yalnızca https://embedded.powerbi.com/appTokenReportEmbed olacaktır.

> [!NOTE]
> Merhaba kullanabilirsiniz [JavaScript rapor katıştırmak örnek](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest işlevselliği. Aynı zamanda kullanılabilir hello farklı işlemler için kod örnekleri sağlar.

**NuGet paketi yüklemesi**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript kodu**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

Çağırma *powerbi.createReport()* hello içinde görünür boş bir tuval düzenleme modunda yapacak *div* öğesi.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Yeni raporlar Kaydet

Merhaba rapor gerçekte oluşturulmaz hello çağrısı tamamlanana kadar **Farklı Kaydet** işlemi. Bu dosya menüsünden veya JavaScript yapılabilir.

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
> Yeni bir rapor yalnızca sonra oluşturulan **Farklı Kaydet** olarak adlandırılır. Kaydettikten sonra hello tuvale hello dataset düzenleme modu ve değil hello raporda hala gösterir. Herhangi bir raporu gibi tooreload hello yeni rapor gerekir.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Yük hello yeni raporu

Merhaba yeni bir rapor ile sipariş toointeract'hello Merhaba uygulaması katıştırır normal bir raporu, anlamı, yeni bir belirteç aynı şekilde özellikle hello yeni rapor için verilmiş olması gerekir ve ardından arama hello içinde katıştırma yöntemi tooembed ihtiyacı vardır.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Kaydetme otomatikleştirmek ve "olay kaydedilmiş" Merhaba kullanarak yeni bir rapor yükleme

"Farklı Kaydet" sipariş tooautomate hello işlemi içinde ve yapabilirsiniz hello yeni rapor yüklenirken "Olay kaydedilmiş" hello kullanın. Bu olay hello kaydetme işlemi tamamlandığında ve (varsa) hello yeni reportId, rapor adı, hello eski reportId içeren bir Json nesnesi döndürür ve hello işlemi Farklı Kaydet olduysa veya kaydetme ateşlenir.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

"kaydedildi" Merhaba olayda dinleme, hello yeni reportId alabilir, hello yeni belirteç oluşturmak ve onunla hello yeni rapor ekleme tooAutomate hello işlemi.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a>Ayrıca bkz.

[Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Raporları kaydetme](power-bi-embedded-save-reports.md)  
[Rapor ekleme](power-bi-embedded-embed-report.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript paketi](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)
