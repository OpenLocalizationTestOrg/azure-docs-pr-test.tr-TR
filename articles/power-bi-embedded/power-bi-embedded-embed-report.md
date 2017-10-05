---
title: Bir rapor Azure Power BI Embedded ekleme | Microsoft Docs
description: "Power BI Embedded içinde olduğu uygulamanıza bir rapor ekleme hakkında bilgi edinin."
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Power BI Embedded içinde bir rapor ekleme

Power BI Embedded içinde olduğu uygulamanıza bir rapor ekleme hakkında bilgi edinin.

Gerçekte uygulamanıza bir rapor eklemek nasıl ele alacağız. Bu, mevcut bir rapor içinde bir çalışma alanı, çalışma alanı koleksiyonu zaten varsayılır. Bu adım henüz yapmadıysanız bkz [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).

Kolayca Power BI Embedded ile uygulamanızı .NET (C#) veya Node.js SDK, JavaScript ile birlikte kullanabilirsiniz. 

## <a name="using-the-access-keys-to-use-rest-apis"></a>REST API'lerini kullanma için erişim anahtarlarını kullanma

REST API çağrısı için belirtilen çalışma alanı koleksiyonu için Azure Portalı'ndan elde edebilirsiniz erişim anahtarı geçirebilirsiniz. Daha fazla bilgi için bkz: [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Bir rapor kimliği alma

Her erişim belirteci bir raporda temel alır. Eklemek istediğiniz rapor için belirli rapor kimliği alma gerekecektir. Bu temel alınarak çağrıları yapılabilir [raporları Al](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API. Bu rapor kimliği ve embed URL'sini döndürür. Bu Power BI .NET SDK kullanarak veya doğrudan REST API çağırma yapılabilir.

### <a name="using-the-power-bi-net-sdk"></a>Power BI .NET SDK kullanarak

.NET SDK'sı kullanırken, Azure portalından aldığınız erişim tuşu dayalı olan bir belirteç kimlik bilgisi oluşturmanız gerekir. Bu, yüklemenizi gerektirir [Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi).

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

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a>REST API doğrudan çağırma

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a>Bir erişim belirteci oluşturma

Power BI Embedded kullanır ekleme belirteci, JSON Web belirteçlerini imzalı HMAC olduğu. Belirteçler, Azure Power BI Embedded çalışma alanı koleksiyonu erişim anahtarla imzalanmıştır. Varsayılan olarak belirteçleri, ekleme, bir uygulamaya eklemek için bir rapor için salt okunur erişim sağlamak için kullanılır. Embed belirteçleri için belirli bir rapor verilir ve bir embed URL'si ile ilişkili olmalıdır.

Erişim tuşları belirteçleri oturum/şifrelemek için kullanılan erişim belirteçleri sunucuda oluşturulması gerekir. Bir erişim belirteci oluşturma hakkında daha fazla bilgi için bkz: [Authenticating ve Power BI Embedded ile yetkilendirme](power-bi-embedded-app-token-flow.md). Ayrıca gözden geçirebilirsiniz [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemi. Burada, ne için Power BI .NET SDK kullanarak gibi görünür bir örnek verilmiştir.

Daha önce aldığınız rapor kimliği kullanır. Ekleme belirteci oluşturulduktan sonra javascript açısından kullanabileceğiniz belirteci üretmek için erişim anahtarı kullanır. *PowerBIToken sınıfı* , yüklemenizi gerektirir [Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

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

### <a name="adding-permission-scopes-to-embed-tokens"></a>Belirteçleri katıştırmak için izin kapsamları ekleme

Embed belirteçleri kullanırken, erişim hakkı vermek kaynak kullanımını kısıtlamak istediğinizi düşünelim. Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz. Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>JavaScript kullanarak ekleme

Erişim belirteci ve rapor kimliği aldıktan sonra biz JavaScript kullanarak raporu eklenebilir. Bu, nuget yüklemenizi gerektirir [Power BI JavaScript paket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). EmbedUrl yalnızca https://embedded.powerbi.com/appTokenReportEmbed olacaktır.

> [!NOTE]
> Kullanabileceğiniz [JavaScript rapor katıştırmak örnek](https://microsoft.github.io/PowerBI-JavaScript/demo/) işlevselliğini test etmek için. Aynı zamanda kullanılabilir farklı işlemler için kod örnekleri sağlar.

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

### <a name="set-the-size-of-embedded-elements"></a>Katıştırılmış öğelerinin boyutunu ayarlama

Rapor kapsayıcısı boyutuna göre otomatik olarak katıştırılır. Varsayılan boyutu geçersiz kılmak için katıştırır genişliği ve yüksekliği için bir CSS sınıfı özniteliği veya satır içi stil eklemeniz yeterlidir.

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
Başka sorunuz mu var? [Power BI Topluluğu'nu deneyin](http://community.powerbi.com/)
