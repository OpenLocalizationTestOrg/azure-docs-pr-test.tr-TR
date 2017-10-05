---
title: "Power BI Embedded ile kimlik doğrulama ve yetkilendirme"
description: "Power BI Embedded ile kimlik doğrulama ve yetkilendirme"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Power BI Embedded ile kimlik doğrulama ve yetkilendirme

Power BI Embedded hizmet kullandığı **anahtarları** ve **uygulama belirteçleri** kimlik doğrulaması ve yetkilendirme açık son kullanıcı kimlik doğrulaması yerine. Bu modelde, kimlik doğrulama ve yetkilendirme kullanıcılarınızın uygulamanızın yönetir. Gerekli olduğunda, uygulamanızın oluşturur ve istenen rapor oluşturmak üzere hizmete bildirir uygulama belirteçleri gönderir. Hala; ancak bu tasarımı uygulamanız Azure Active Directory kullanıcı kimlik doğrulaması ve yetkilendirme için kullanılacak gerektirmez.

## <a name="two-ways-to-authenticate"></a>Kimlik doğrulaması için iki yol

**Anahtar** -tüm Power BI Embedded REST API çağrıları için tuşlarını kullanabilirsiniz. Anahtarları bulunabilir **Azure portal** tıklayarak **tüm ayarları** ve ardından **erişim anahtarları**. Her zaman bir parola değilmiş gibi anahtarınızı kabul eder. Bu anahtarlar üzerinde belirli çalışma alanı koleksiyonu çağrı herhangi bir REST API'nin yapma izinlerine sahiptir.

Bir anahtar REST çağrısı kullanmak için aşağıdaki authorization üstbilgisi ekleyin:            

    Authorization: AppKey {your key}

**Uygulama belirteci** -uygulama belirteçleri katıştırma tüm istekler için kullanılır. Tek bir rapor sınırlı ve bir sona erme süresini ayarlamak için en iyi bir uygulamadır için istemci tarafı çalıştırılmak üzere tasarlanmışlardır.

Uygulama belirteçleri anahtarlarınızı biri tarafından imzalanan JWT (JSON Web belirteci) var.

Uygulama belirteci aşağıdaki talep içerebilir:

| İste | Açıklama |
| --- | --- |
| **ver** |Uygulama belirteci sürümü. 0.2.0 geçerli sürümdür. |
| **aud** |Belirtecin hedeflenen alıcı. Power BI Embedded kullanılacak: "https://analysis.windows.net/powerbi/api". |
| **ISS** |Belirtecin uygulama gösteren bir dize. |
| **türü** |Oluşturulan uygulama Belirtecin türü. Geçerli tek desteklenen türüdür **katıştırmak**. |
| **WCN** |Çalışma alanı koleksiyonu adı belirteci için yayımlanmaktadır. |
| **WID** |Çalışma alanı kimliği belirteci için yayımlanmaktadır. |
| **RID** |Rapor Kimliği belirteci için yayımlanmaktadır. |
| **Kullanıcı adı** (isteğe bağlı) |RLS ile kullanıldığında, bu kullanıcının RLS kuralları uygularken belirlemenize yardımcı olabilecek bir dize değeridir. |
| **rolleri** (isteğe bağlı) |Satır düzeyi güvenlik kuralları uygularken seçmek için rolleri içeren bir dize. Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır. |
| **SCP** (isteğe bağlı) |İzinleri kapsamları içeren bir dize. Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır. |
| **exp** (isteğe bağlı) |Belirteç sona erecek süresini gösterir. Bu UNIX zaman damgaları geçirilmesi. |
| **NBF** (isteğe bağlı) |İçinde belirtecin geçerli olan başladığı saati belirtir. Bu UNIX zaman damgaları geçirilmesi. |

Örnek bir uygulama belirtecini şuna benzeyecektir:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Kodunu çözdü, şunun gibi görünür:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Apptokens oluşturulmasını kolaylaştırmak SDK içinde kullanılabilir yöntem vardır. Örneğin, .NET için bakabilirsiniz [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) sınıfı ve [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemleri.

.NET SDK için başvurabilirsiniz [kapsamları](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Kapsamları

Embed belirteçleri kullanırken, erişim hakkı vermek kaynak kullanımını kısıtlamak istediğinizi düşünelim. Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz.

Power BI Embedded kullanılabilir kapsamlarının verilmiştir.

|Kapsam|Açıklama|
|---|---|
|Dataset.Read|Belirtilen veri okuma izni sağlar.|
|Dataset.Write|Belirtilen veri kümesi için yazma izni sağlar.|
|Dataset.ReadWrite|Belirtilen veri kümesine okumasına ve yazmasına izin sağlar.|
|Report.Read|Belirtilen rapor görüntüleme izni sağlar.|
|Report.ReadWrite|Görüntülemek ve belirtilen rapor düzenleme izni sağlar.|
|Workspace.Report.Create|Belirtilen çalışma alanı içinde yeni bir rapor oluşturma izni sağlar.|
|Workspace.Report.Copy|Var olan bir raporu belirtilen çalışma alanı içindeki kopyalamaya izin sağlar.|

Aşağıdaki gibi kapsamları arasında bir boşluk kullanarak birden çok kapsam sağlayabilir.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Gerekli talep - kapsamları**

SCP: {scopesClaim} scopesClaim bir dize veya bir çalışma alanı kaynaklarına (rapor, veri kümesi, vb.) izin verilen izinleri belirterek bir dizeler dizisi olabilir

Kodu çözülmüş bir belirteç tanımlanan kapsamlarla aşağıdakine benzer görünecektir.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>İşlemler ve kapsamlar

|İşlem|Hedef kaynak|Belirteç izinleri|
|---|---|---|
|(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun.|Veri kümesi|Dataset.Read|
|(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun ve raporu kaydedin.|Veri kümesi|* Dataset.Read<br>* Workspace.Report.Create|
|Görüntüleyin ve (bellek içi) var olan bir raporu keşfedin/düzenleyin. Report.Read Dataset.Read anlamına gelir. Bu düzenlemeleri kaydetmek için izinlere izin vermez.|Rapor|Report.Read|
|Düzenle ve var olan bir raporu kaydedin.|Rapor|Report.ReadWrite|
|(Farklı Kaydet) bir raporun bir kopyasını kaydedin.|Rapor|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-the-flow-works"></a>İşte akışı nasıl çalışır?
1. API anahtarları uygulamanıza kopyalayın. Anahtarları alabileceğiniz **Azure Portal**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Belirteç talep onaylar ve sona erme süresi vardır.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Belirteci bir API erişim anahtarlarla imzalanması.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Bir raporu görüntülemek için kullanıcı istekleri.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Belirteç API'si erişim tuşları ile doğrulanır.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded, kullanıcıya bir rapor gönderir.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Sonra **Power BI Embedded** rapor kullanıcı, kullanıcı için bir özel uygulamanızda raporunu görüntüleyebilirsiniz. Örneğin, içeri aktardığınız [çözümleme satış verileri PBIX örnek](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), örnek web uygulaması şuna benzer:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Ayrıca Bkz.

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Microsoft Power BI Embedded örneği kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Microsoft Power BI Embedded senaryoları](power-bi-embedded-scenarios.md)  
[Microsoft Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md)  
[Powerbı CSharp Git deposu](https://github.com/Microsoft/PowerBI-CSharp)  
Başka sorunuz mu var? [Power BI Topluluğu'nu deneyin](http://community.powerbi.com/)

