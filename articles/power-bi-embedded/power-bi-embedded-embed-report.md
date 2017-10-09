---
title: bir rapor Azure Power BI Embedded aaaEmbed | Microsoft Docs
description: "Bilgi nasıl tooembed olan Power BI Embedded uygulamanıza bir rapor."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Power BI Embedded içinde bir rapor ekleme

Bilgi nasıl tooembed olan Power BI Embedded uygulamanıza bir rapor.

Nasıl tooactually katıştırmak bir raporu uygulamanıza ele alacağız. Bu, mevcut bir rapor içinde bir çalışma alanı, çalışma alanı koleksiyonu zaten varsayılır. Bu adım henüz yapmadıysanız bkz [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).

Tooeasily Power BI Embedded ile uygulamanızı oluşturma, hello .NET (C#) veya Node.js SDK, JavaScript ile birlikte kullanabilirsiniz. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Merhaba erişim anahtarları toouse REST API'lerini kullanma

Sipariş toocall hello REST API, hello belirli çalışma alanı koleksiyonu için Azure Portalı'ndan elde edebilirsiniz hello erişim tuşu geçirebilirsiniz. Daha fazla bilgi için bkz: [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Bir rapor kimliği alma

Her erişim belirteci bir raporda temel alır. Tooembed istediğiniz hello rapor için rapor kimliği belirtilen tooget hello gerekir. Bu çağrı toohello göre yapılabilir [raporları Al](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API. Bu kimliği ve hello url katıştırmak hello rapor döndürür. Bu yapılabilir hello Power BI .NET SDK kullanarak veya doğrudan hello REST API çağırma.

### <a name="using-hello-power-bi-net-sdk"></a>Merhaba Power BI .NET SDK kullanarak

Merhaba .NET SDK'sı kullanırken toocreate hello Azure portal ' aldığınız hello erişim tuşu dayalı olan bir belirteç kimlik bilgisi gerekir. Bu hello yüklemenizi gerektirir [Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi).

**NuGet paketi yüklemesi**

```
Install-Package Microsoft.PowerBI.Api
```

**C# kodu**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Doğrudan çağırma hello REST API'si

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>Bir erişim belirteci oluşturma

Power BI Embedded kullanır ekleme belirteci, JSON Web belirteçlerini imzalı HMAC olduğu. Merhaba belirteçleri hello erişim anahtarıyla Azure Power BI Embedded çalışma alanı koleksiyonu imzalanmıştır. Varsayılan olarak belirteçleri, ekleme, olan okuma kullanılan tooprovide yalnızca erişim tooa rapor tooembed bir uygulamaya. Embed belirteçleri için belirli bir rapor verilir ve bir embed URL'si ile ilişkili olmalıdır.

Merhaba erişim tuşları kullanılan toosign/şifrelemek hello belirteçleri gibi erişim belirteçleri hello sunucusunda oluşturulmalıdır. Hakkında bilgi için bkz: toocreate bir erişim belirteci [Authenticating ve Power BI Embedded ile yetkilendirme](power-bi-embedded-app-token-flow.md). Merhaba gözden geçirebilirsiniz [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemi. Burada, ne için Power BI hello .NET SDK kullanarak gibi görünür bir örnek verilmiştir.

Daha önce aldığınız hello rapor kimliği kullanır. Hello katıştırmak sonra belirteç oluşturulur, ardından hello javascript açısından kullanabileceğiniz hello erişim anahtar toogenerate hello belirteci kullanacaktır. Merhaba *PowerBIToken sınıfı* hello yüklemenizi gerektirir [Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**NuGet paketi yüklemesi**

```
Install-Package Microsoft.PowerBI.Core
```

**C# kodu**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>İzin kapsamları tooembed belirteçleri ekleme

Embed belirteçleri kullanırken toorestrict kullanım hello kaynakların erişim hakkı vermek isteyebilirsiniz. Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz. Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>JavaScript kullanarak ekleme

Merhaba erişim belirtecini ve hello rapor kimliğini oluşturduktan sonra biz JavaScript kullanarak hello rapor eklenebilir. Bu hello nuget yüklemenizi gerektirir [Power BI JavaScript paket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Merhaba embedUrl yalnızca https://embedded.powerbi.com/appTokenReportEmbed olacaktır.

> [!NOTE]
> Merhaba kullanabilirsiniz [JavaScript rapor katıştırmak örnek](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest işlevselliği. Aynı zamanda kullanılabilir hello farklı işlemler için kod örnekleri sağlar.

**NuGet paketi yüklemesi**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript kodu**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>Katıştırılmış öğeleri Hello boyutunu ayarlama

Merhaba rapor kapsayıcısı hello boyutuna göre otomatik olarak katıştırılır. Merhaba toooverride hello varsayılan boyutu katıştırır yalnızca genişliği ve yüksekliği için bir CSS sınıfı özniteliği veya satır içi stil ekleyin.

## <a name="see-also"></a>Ayrıca bkz.

[Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI JavaScript paketi](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi)
[Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Powerbı CSharp Git deposu](https://github.com/Microsoft/PowerBI-CSharp)  
[Powerbı düğümlü Git deposu](https://github.com/Microsoft/PowerBI-Node)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)
