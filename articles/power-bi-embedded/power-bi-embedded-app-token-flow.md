---
title: aaaAuthenticating ve Power BI Embedded ile yetkisi verme
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
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Power BI Embedded ile kimlik doğrulama ve yetkilendirme

Merhaba Power BI Embedded hizmeti kullanan **anahtarları** ve **uygulama belirteçleri** kimlik doğrulaması ve yetkilendirme açık son kullanıcı kimlik doğrulaması yerine. Bu modelde, kimlik doğrulama ve yetkilendirme kullanıcılarınızın uygulamanızın yönetir. Gerekli olduğunda, uygulamanızın oluşturur ve istenen rapor bizim hizmet toorender söyler hello uygulama belirteçleri hello gönderir. Hala; ancak bu tasarım, uygulama toouse Azure Active Directory kullanıcı kimlik doğrulaması ve yetkilendirme için gerektirmez.

## <a name="two-ways-tooauthenticate"></a>İki yolla tooauthenticate

**Anahtar** -tüm Power BI Embedded REST API çağrıları için tuşlarını kullanabilirsiniz. Merhaba anahtarları hello bulunabilir **Azure portal** tıklayarak **tüm ayarları** ve ardından **erişim anahtarları**. Her zaman bir parola değilmiş gibi anahtarınızı kabul eder. Bu anahtarlar tüm REST API çağrısı belirli çalışma alanı koleksiyonu üzerinde izinleri toomake sahiptir.

toouse REST çağrısı bir anahtar authorization üstbilgisi aşağıdaki hello ekleyin:            

    Authorization: AppKey {your key}

**Uygulama belirteci** -uygulama belirteçleri katıştırma tüm istekler için kullanılır. Oldukları çalıştırmak tasarlanmış toobe istemci-tarafı, kısıtlı bulunmaları tooa tek raporu ve kendi en iyi yöntem tooset bir sona erme zamanı.

Uygulama belirteçleri anahtarlarınızı biri tarafından imzalanan JWT (JSON Web belirteci) var.

Uygulama belirtecinizi talepler aşağıdaki hello içerebilir:

| İste | Açıklama |
| --- | --- |
| **ver** |Merhaba uygulama belirteci Hello sürümü. 0.2.0 hello geçerli sürümdür. |
| **aud** |Merhaba alıcı hello belirtecin amacı. Power BI Embedded kullanılacak: "https://analysis.windows.net/powerbi/api". |
| **ISS** |Merhaba belirteç Merhaba uygulaması gösteren bir dize. |
| **türü** |oluşturulan uygulama belirteci Hello türü. Geçerli hello yalnızca desteklenen tür **katıştırmak**. |
| **WCN** |Çalışma alanı koleksiyonu ad hello simgesi için yayımlanmaktadır. |
| **WID** |Çalışma alanı kimliği hello belirteci için yayımlanmaktadır. |
| **RID** |Kimliği hello belirteci verilen bildirin. |
| **Kullanıcı adı** (isteğe bağlı) |RLS ile kullanıldığında, bu RLS kuralları uygularken hello kullanıcı belirlemenize yardımcı olabilecek bir dize değeridir. |
| **rolleri** (isteğe bağlı) |Satır düzeyi güvenlik kuralları uygularken Hello rolleri tooselect içeren bir dize. Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır. |
| **SCP** (isteğe bağlı) |Merhaba izinleri kapsamları içeren bir dize. Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır. |
| **exp** (isteğe bağlı) |Hangi hello belirteci dolacak hello süresini gösterir. Bu UNIX zaman damgaları geçirilmesi. |
| **NBF** (isteğe bağlı) |Hangi hello belirteci geçerli olan hello başlatılışında gösterir. Bu UNIX zaman damgaları geçirilmesi. |

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

Merhaba apptokens oluşturulmasını kolaylaştırmak SDK'ları içinde kullanılabilir yöntem vardır. Örneğin, .NET için hello bakabilir [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) sınıfı ve hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemleri.

Çok başvurabilir Hello .NET SDK'sı için[kapsamları](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Kapsamları

Embed belirteçleri kullanırken toorestrict kullanım hello kaynakların erişim hakkı vermek isteyebilirsiniz. Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz.

Merhaba, Power BI Embedded için kullanılabilir kapsamı hello verilmiştir.

|Kapsam|Açıklama|
|---|---|
|Dataset.Read|İzin sağlar tooread hello belirtilen veri kümesi.|
|Dataset.Write|Belirtilen izin toowrite toohello sağlayan veri kümesi.|
|Dataset.ReadWrite|İzin tooread ve yazma toohello komutla veri kümesi sağlar.|
|Report.Read|İzin sağlar tooview hello belirtilen rapor.|
|Report.ReadWrite|Belirtilen rapor izni tooview ve düzenleme hello sağlar.|
|Workspace.Report.Create|Yeni bir rapor içinde belirtilen hello izni toocreate sağlar çalışma.|
|Workspace.Report.Copy|Var olan bir raporu belirtilen hello içinde izin tooclone sağlar çalışma.|

Merhaba aşağıdaki gibi hello kapsamları arasında bir boşluk kullanarak birden çok kapsam sağlayabilir.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Gerekli talep - kapsamları**

SCP: {scopesClaim} scopesClaim bir dize veya hello izin verilen izinleri tooworkspace kaynakları (rapor, veri kümesi, vb.) belirlenerek bir dizeler dizisi olabilir

Tanımlı, kapsamları bir kodu çözülmüş belirteciyle benzer toohello aşağıdaki görünür.

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
|(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun ve hello raporu kaydedin.|Veri kümesi|* Dataset.Read<br>* Workspace.Report.Create|
|Görüntüleyin ve (bellek içi) var olan bir raporu keşfedin/düzenleyin. Report.Read Dataset.Read anlamına gelir. Bu izinleri toosave düzenlemeleri izin vermez.|Rapor|Report.Read|
|Düzenle ve var olan bir raporu kaydedin.|Rapor|Report.ReadWrite|
|(Farklı Kaydet) bir raporun bir kopyasını kaydedin.|Rapor|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>İşte hello akışı nasıl çalışır?
1. Merhaba API anahtarları tooyour uygulaması kopyalayın. Merhaba anahtarları alabileceğiniz **Azure Portal**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Belirteç talep onaylar ve sona erme süresi vardır.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Belirteci bir API erişim anahtarlarla imzalanması.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Kullanıcı bir rapor tooview ister.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Belirteç API'si erişim tuşları ile doğrulanır.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded rapor toouser gönderir.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Sonra **Power BI Embedded** bir rapor toohello kullanıcı gönderir hello kullanıcı özel uygulamanızda hello raporu görüntüleyebilirsiniz. Örneğin, hello aldıysanız [çözümleme satış verileri PBIX örnek](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello örnek web uygulaması şuna benzeyebilir:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Ayrıca Bkz.

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Microsoft Power BI Embedded örneği kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Microsoft Power BI Embedded senaryoları](power-bi-embedded-scenarios.md)  
[Microsoft Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md)  
[Powerbı CSharp Git deposu](https://github.com/Microsoft/PowerBI-CSharp)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)

