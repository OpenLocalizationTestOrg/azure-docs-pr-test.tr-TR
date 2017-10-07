---
title: aaaAzure uygulama Insights Telemetri veri modeli - istek Telemetri | Microsoft Docs
description: "İstek telemetri için uygulama Öngörüler veri modeli"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Telemetri isteği: Application Insights veri modeli

Bir istek telemetri öğesi (içinde [Application Insights](app-insights-overview.md)) hello mantıksal bir dış istek tooyour uygulama tarafından tetiklenen yürütme sırasını temsil eder. Her istek yürütme benzersiz tarafından tanımlanan `ID` ve `url` tüm hello yürütme parametreleri içeren. İsteği mantıksal olarak gruplayabilirsiniz `name` ve hello tanımlamak `source` bu isteğin. Kod yürütmeyi sonuçlanabilir `success` veya `fail` ve belirli bir sahip `duration`. Başarı ve başarısızlık yürütmeleri gruplandırılmış tarafından daha fazla `resultCode`. Merhaba Zarf düzeyinde tanımlanan hello isteği telemetri için başlangıç saati.

Telemetri destekleyen özel kullanarak hello standart genişletilebilirlik modeli isteği `properties` ve `measurements`.

## <a name="name"></a>Ad

Merhaba isteği adını kod yolu gerçekleştirilecek tooprocess hello isteği temsil eder. Düşük önem düzeyi değeri tooallow daha iyi isteklerinin gruplandırma. Temsil, HTTP istekleri için HTTP yöntemi ve URL yolu şablonu gibi hello `GET /values/{id}` hello gerçek olmadan `id` değeri.

Uygulama Insights web SDK "olduğu gibi" isteği adı bakımından tooletter durumuyla gönderir. UI gruplandırılması büyük küçük harfe duyarlı şekilde `GET /Home/Index` gelen ayrı olarak sayılan `GET /home/INDEX` çoğunlukla bunlar hello aynı sonucu olsa bile denetleyici ve eylem yürütme. Merhaba, URL'leri genel olduğunu nedeni [büyük küçük harfe duyarlı](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). Tüm toosee isteyebilirsiniz `404` büyük yazılan hello URL'ler için oldu. Daha fazla üzerinde isteği adı koleksiyonunda ASP.Net Web SDK'sı tarafından hello okuyabilirsiniz [blog gönderisi](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

En fazla uzunluk: 1024 karakter

## <a name="id"></a>Kimlik

Bir istek çağrısı örneği tanımlayıcısı. İstek ve diğer telemetri öğeleri arasında bağıntı için kullanılır. Kimliği küresel olarak benzersiz olmalıdır. Daha fazla bilgi için bkz: [bağıntı](application-insights-correlation.md) sayfası.

En fazla uzunluk: 128 karakter

## <a name="url"></a>Url

Tüm sorgu dizesi parametreleri ile istek URL'si.

En fazla uzunluk: 2048 karakter

## <a name="source"></a>Kaynak

Merhaba istek kaynağı. Merhaba çağıran hello izleme anahtarını hello adını veya IP adresini hello çağıran örnektir. Daha fazla bilgi için bkz: [bağıntı](application-insights-correlation.md) sayfası.

En fazla uzunluk: 1024 karakter

## <a name="duration"></a>Süre

Süre biçimde istek: `DD.HH:MM:SS.MMMMMM`. Pozitif ve daha az olmalıdır daha `1000` gün. İstek telemetri hello başlangıcını ve bitişini hello ile Merhaba işlemini temsil eden gibi bu gerekli bir alandır.

## <a name="response-code"></a>Yanıt kodu

Bir istek yürütme sonucu. HTTP isteklerini HTTP durum kodu. Bu olabilir `HRESULT` diğer istek türleri için değer veya özel durum türü.

En fazla uzunluk: 1024 karakter

## <a name="success"></a>Başarılı

Başarılı veya başarısız çağrının gösterimi. Bu alan gereklidir. Açıkça çok ayarlandığında değil`false` -toobe başarılı olarak kabul isteği. Bu değeri çok ayarlayın`false` işlemi özel durum nedeniyle kesildi veya bir hata sonucu kodu döndürdü.

Merhaba web uygulamaları için Application Insights istek hello yanıt kodu daha az hello olduğunda başarısız olarak tanımlamak `400` çok eşit veya`401`. Ancak bu varsayılan eşleme hello hello uygulamasının anlamsal eşleşmediğinde durumlar vardır. Yanıt kodu `404` "Normal akışının parçası olabilen hiç kayıt" gösteriyor olabilir. Bozuk bir bağlantı da işaret edebilir. Bağlantılar bozuk hello için daha gelişmiş mantık bile uygulayabilirsiniz. Bu bağlantıları aynı url başvuran çözümleyerek site hello üzerinde bulunduğunda bağlantıların hataları olarak işaretleyebilirsiniz. Ya da bunları hello şirketin mobil uygulamadan erişildiğinde hataları olarak işaretleyin. Benzer şekilde `301` ve `302` yeniden yönlendirme desteklemiyor hello istemciden erişildiğinde başarısız olduğunu gösterir.

Kısmen, içerik kabul `206` genel bir istek bir hata göstergesi olabilir. Örneğin, Application Insights endpoint telemetri öğeleri toplu tek bir istek alır. Döndürdüğü `206` zaman bazı öğeler hello toplu olmayan başarıyla işlendi. Artan oranını `206` toobe araştırılması gereken bir sorun olduğunu gösterir. Benzer mantığı uygular çok`207` burada hello başarı çok Status hello ayrı yanıt kodları en kötü.

Daha fazla üzerinde istek sonucu okuyabilir kodu ve durum kodunu hello [blog gönderisi](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Özel Özellikler

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Özel ölçümleri

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Sonraki adımlar

- [Özel bir istek telemetri yazma](app-insights-api-custom-events-metrics.md#trackrequest)
- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- Nasıl çok öğrenin[ASP.NET Core yapılandırma](app-insights-asp-net.md) Application Insights ile uygulama.
- Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.
