---
title: "API Management genel bakış ile Service Fabric aaaAzure | Microsoft Docs"
description: "Bu makalede, bir ağ geçidi tooyour Service Fabric uygulamaları bir giriş toousing Azure API Management getirilmiştir."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Service Fabric ile Azure API Management genel bakış

Bulut uygulamalarını genellikle kullanıcılar, aygıtlar veya diğer uygulamalar için bir ön uç ağ geçidi tooprovide tek bir giriş noktası gerekir. Service Fabric bir ağ geçidi herhangi bir durum bilgisiz hizmeti gibi olabilir bir [ASP.NET Core uygulama](service-fabric-reliable-services-communication-aspnetcore.md), veya başka bir hizmeti gibi trafik giriş için tasarlanmış [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IOT hub'ı](https://docs.microsoft.com/azure/iot-hub/), veya [Azure API Management](https://docs.microsoft.com/azure/api-management/).

Bu makalede, bir ağ geçidi tooyour Service Fabric uygulamaları bir giriş toousing Azure API Management getirilmiştir. API Management Service Fabric, yönlendirme kuralları tooyour arka uç Service Fabric Hizmetleri zengin bir dizi API toopublish izin vererek ile doğrudan tümleşir. 

## <a name="architecture"></a>Mimari
Ortak bir Service Fabric mimarisi HTTP API'leri tooback uç hizmetlerinin HTTP çağrılar bir tek sayfalı web uygulaması kullanır. Merhaba [Service Fabric başlama örnek uygulama](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) Bu mimarinin bir örneği gösterir.

Bu senaryoda, bir durum bilgisi olmayan web hizmeti Service Fabric uygulaması hello hello ağ geçidi olarak görev yapar. Bu yaklaşım, HTTP proxy için bir web hizmeti toowrite tooback uç hizmetlerinin hello Aşağıdaki diyagramda gösterildiği gibi istekleri gerektirir:

![Service Fabric ile Azure API Management topolojisine genel bakış][sf-web-app-stateless-gateway]

Uygulamaları karmaşıklığı arttıkça, bu nedenle bir API çok arka uç hizmetlerini önünde sunmalıdır ağ geçitleri hello. Azure API Management, tasarlanmış toohandle yönlendirme kuralları ile karmaşık API'lere erişim denetimi, hız sınırlaması, izleme, olay günlüğünü ve bölümünüzün minimum çabayla yanıt önbelleğe alma. Azure API Management Service Fabric hizmet bulma, bölüm çözümleme destekler ve durum bilgisiz kendi API ağ geçidi toowrite aktarıp çoğaltma seçimi toointelligently rota doğrudan Service Fabric tooback uç Hizmetleri'nde ister. 

Bu senaryoda, HTTP API çağrıları yönetilen ve hello Aşağıdaki diyagramda gösterildiği gibi Azure API Management yönlendirilmiş UI hala bir web hizmeti aracılığıyla sunulan web hello:

![Service Fabric ile Azure API Management topolojisine genel bakış][sf-apim-web-app]

## <a name="application-scenarios"></a>Uygulama senaryoları

Durum bilgisiz ya da durum bilgisi olan Service Fabric Hizmetleri'nde olabilir ve üç düzenleri birini kullanarak bölümlendirilebilir: singleton, int 64 aralığı ve adlandırılmış. Hizmet uç noktası çözümleme belirli hizmet örneği, belirli bir bölüm tanımlayan gerektirir. Bir hizmetin bir uç nokta çözülürken hem de hizmet örneği adı hello (örneğin, `fabric:/myapp/myservice`) yanı sıra belirli bir bölüm hello hello hizmetinin belirtilmelidir, tek bölüm hello durumda dışındaki.

Azure API Management durum bilgisi olmayan hizmetler, durum bilgisi olan hizmetler ve tüm bölümleme düzeni, herhangi bir birleşimini ile kullanılabilir.

## <a name="send-traffic-tooa-stateless-service"></a>Trafik tooa durum bilgisiz hizmet Gönder

Merhaba en basit durumda, trafik tooa durum bilgisiz hizmet örneği iletilir. tooachieve Bu, bir API Management işlem bir Service Fabric tooa özel durum bilgisiz hizmet örneği hello Service Fabric arka uç içinde eşleyen uç gelen işleme ilkesiyle içerir. Toothat hizmeti gönderilen istekleri tooa rastgele hello durum bilgisiz hizmet örneğinin kopyasını gönderilir.

#### <a name="example"></a>Örnek
Senaryo aşağıdaki hello adlı bir durum bilgisi olmayan hizmetin Service Fabric uygulaması içeren `fabric:/app/fooservice`, iç HTTP API gösterir. Merhaba hizmet örneği adı tanınmış ve doğrudan hello API Management gelen işleme ilkesi sabit kodlanmış olabilir. 

![Service Fabric ile Azure API Management topolojisine genel bakış][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Trafik tooa durum bilgisi olan hizmet Gönder

Benzer toohello durum bilgisiz Hizmetleri senaryosu, trafik tooa durum bilgisi olan hizmet örneği iletilebilir. Bu durumda, bir API Management işlem bir Service Fabric belirli bir istek tooa belirli bölümünü eşleyen uç gelen işleme ilkesiyle içeren *durum bilgisi olan* hizmet örneği. her istek toois bazı kullanarak lambda yöntemiyle hesaplanan hello bölüm toomap hello gelen HTTP istek, bir değer hello gibi URL yolu girin. Hello İlkesi, yapılandırılmış toosend istekleri toohello yalnızca birincil çoğaltma veya okuma işlemleri için rastgele çoğaltma tooa olabilir.

#### <a name="example"></a>Örnek

Senaryo aşağıdaki hello adlı bölümlenmiş bir durum bilgisi olan hizmet Service Fabric uygulaması içeren `fabric:/app/userservice` bir iç HTTP API gösterir. Merhaba hizmet örneği adı tanınmış ve doğrudan hello API Management gelen işleme ilkesi sabit kodlanmış olabilir.  

Merhaba hizmet iki bölüm ile Merhaba Int64 bölüm düzeni ve kapsayan bir anahtar aralığı kullanılarak bölümlenen `Int64.MinValue` çok`Int64.MaxValue`. Merhaba arka uç İlkesi hesaplar bu aralıktaki bir bölüm anahtarı hello dönüştürerek `id` herhangi bir algoritma kullanılan burada toocompute hello bölüm anahtarı olabilse hello URL istek yolu tooa 64-bit tamsayı, sağlanan değer. 

![Service Fabric ile Azure API Management topolojisine genel bakış][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Toomultiple durum bilgisi olmayan hizmetler trafiği Gönder

Daha gelişmiş senaryolarda eşlemeleri toomore bir hizmet örneği ister bir API Management işlemi tanımlayabilirsiniz. Bu durumda, her işlem tooa belirli hizmet örneği değerleri hello gelen HTTP istek, durum bilgisi olan hizmetleri hello durumda ve hello URL yolu veya sorgu dizesi gibi bir bölüm hello hizmet örneği içinde temel alarak istekleri eşleyen bir ilke içeriyor . 

tooachieve bu işlemi içeren bir Service Fabric tooa durum bilgisiz hizmet örneği hello Service Fabric hello gelen HTTP isteğinden alınan değerlere göre uç içinde eşleyen uç gelen işleme ilkesiyle bir API Management. İstekleri tooa hizmet örneği hello hizmet örneğinin tooa rastgele çoğaltmasını gönderilir.

#### <a name="example"></a>Örnek

Bu örnekte, yeni bir durum bilgisiz hizmet örneği uygulamanın her bir kullanıcı için aşağıdaki formülü hello kullanarak dinamik olarak oluşturulan bir adla oluşturulur:
 
 - `fabric:/app/users/<username>`

 Her hizmet için benzersiz bir ad olsa da, hello adları eylemli veya yönetici giriş ve böylece APIM ilkeleri veya yönlendirme kuralları sabit kodlanmış olamaz hello Hizmetleri yanıt toouser oluşturulur çünkü bilinmez. Merhaba hizmet toowhich toosend bir istek hello adını hello arka uç İlkesi hello tanımından bunun yerine, üretildi `name` hello URL istek yolunda sağlanan değer. Örneğin:

  - Bir istek çok`/api/users/foo` yönlendirilmiş tooservice örneği`fabric:/app/users/foo`
  - Bir istek çok`/api/users/bar` yönlendirilmiş tooservice örneği`fabric:/app/users/bar`

![Service Fabric ile Azure API Management topolojisine genel bakış][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Toomultiple durum bilgisi olan hizmetler trafiği Gönder

Benzer toohello durum bilgisiz hizmet örneği, işlem eşlenebilir bir API Management istekleri birden toomore **durum bilgisi olan** hizmet örneği, bu, aynı zamanda durumda tooperform bölüm çözümleme her durum bilgisi olan hizmet için gereksinim duyabileceğiniz örneği.

tooachieve bu işlemi içeren bir Service Fabric hello Service Fabric hello gelen HTTP isteğinden alınan değerlere göre uç tooa durum bilgisi olan hizmet örneği eşleyen uç gelen işleme ilkesiyle bir API Management. Ayrıca toomapping hello isteği bir istek toospecific hizmet örneği, ayrıca belirli bir bölüm eşlenen tooa hello hizmet örneği ve isteğe bağlı olarak tooeither hello birincil çoğaltma içinde veya hello bölüm içinde rastgele bir ikincil çoğaltma olabilir.

#### <a name="example"></a>Örnek

Bu örnekte, formülü aşağıdaki hello kullanarak dinamik olarak oluşturulan bir adla Merhaba uygulaması her bir kullanıcı için yeni bir durum bilgisi olan hizmet örneği oluşturulur:
 
 - `fabric:/app/users/<username>`

 Her hizmet için benzersiz bir ad olsa da, hello adları eylemli veya yönetici giriş ve böylece APIM ilkeleri veya yönlendirme kuralları sabit kodlanmış olamaz hello Hizmetleri yanıt toouser oluşturulur çünkü bilinmez. Merhaba hizmet toowhich toosend bir istek hello adını hello arka uç İlkesi hello tanımından bunun yerine, üretildi `name` sağlanan değer hello URL istek yolu. Örneğin:

  - Bir istek çok`/api/users/foo` yönlendirilmiş tooservice örneği`fabric:/app/users/foo`
  - Bir istek çok`/api/users/bar` yönlendirilmiş tooservice örneği`fabric:/app/users/bar`

Her hizmet örneği iki bölüm ile Merhaba Int64 bölüm düzeni ve kapsayan bir anahtar aralığı kullanarak da bölümlenmiş `Int64.MinValue` çok`Int64.MaxValue`. Merhaba arka uç İlkesi hesaplar bu aralıktaki bir bölüm anahtarı hello dönüştürerek `id` herhangi bir algoritma kullanılan burada toocompute hello bölüm anahtarı olabilse hello URL istek yolu tooa 64-bit tamsayı, sağlanan değer. 

![Service Fabric ile Azure API Management topolojisine genel bakış][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Sonraki adımlar

Merhaba izleyin [Hızlı Başlangıç Kılavuzu](service-fabric-api-management-quick-start.md) tooset ilk Service Fabric yukarı Küme API Management tooyour Hizmetleri aracılığıyla API Management ve akış isteklerle.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png