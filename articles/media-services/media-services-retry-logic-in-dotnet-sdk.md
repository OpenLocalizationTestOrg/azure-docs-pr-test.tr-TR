---
title: "Merhaba .NET için Media Services SDK'sı aaaRetry mantığı | Microsoft Docs"
description: "Merhaba konu .NET için hello Media Services SDK'sı yeniden deneme mantığı genel bir bakış sağlar."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>.NET için Media Services SDK'sı hello mantığı yeniden deneyin
Microsoft Azure Hizmetleri ile çalışırken, geçici hataları oluşabilir. Geçici bir hata oluşursa, çoğu durumda, birkaç denemeden sonra hello işlemi başarılı olur. .NET için Media Services SDK'sı Hello hello yeniden deneme mantığı toohandle geçici hataları özel durumlar ve sorgular, değişiklikler ve depolama işlemleri kaydetme yürütmeden web isteklerine göre neden hataları ile ilişkili uygular.  Varsayılan olarak, hello özel durum tooyour uygulama yeniden atmadan önce hello .NET için Media Services SDK'sı dört yeniden denemenin yürütür. Merhaba kodu, uygulamanızda sonra bu özel durumun düzgün işlemesi gerekir.  

 Merhaba, kısa bir kılavuz Web isteğine, depolama, sorgu ve SaveChanges ilkelerin aşağıdadır:  

* Merhaba depolama ilkesi (yüklemeleri veya varlık dosyaları indirme) blob depolama işlemleri için kullanılır.  
* Merhaba Web isteği ilkesi, genel web istekleri (örneğin, bir kimlik doğrulama belirteci alma ve uç nokta hello kullanıcılar küme çözme) için kullanılır.  
* Merhaba Sorgu İlkesi REST (örneğin, mediaContext.Assets.Where(...)). varlıkları sorgulamak için kullanılır  
* Merhaba SaveChanges İlkesi hello hizmet (örneğin, bir hizmet işlevi için bir işlem çağırma bir varlık, güncelleştirme bir varlık oluşturma) içinde veri değişikliklerini herhangi bir şey yapmak için kullanılır.  
  
  Bu konu özel durum türleri listeler ve .NET için Media Services SDK'sı hello tarafından işlenen hata kodları mantığı yeniden deneyin.  

## <a name="exception-types"></a>Özel durum türleri
Merhaba aşağıdaki tablo, ' % s'hello Media Services SDK'sı .NET tanıtıcıları için özel durumlar açıklanmaktadır veya geçici hatalarına neden olabilir bazı işlemler için işlemez.  

| Özel durum | Web isteği | Depolama | Sorgu | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Daha fazla bilgi için bkz: Merhaba [WebException durum kodları](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) bölümü. |Evet |Evet |Evet |Evet |
| DataServiceClientException<br/> Daha fazla bilgi için bkz: [HTTP hata durum kodları](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Hayır |Evet |Evet |Evet |
| DataServiceQueryException<br/> Daha fazla bilgi için bkz: [HTTP hata durum kodları](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Hayır |Evet |Evet |Evet |
| DataServiceRequestException<br/> Daha fazla bilgi için bkz: [HTTP hata durum kodları](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Hayır |Evet |Evet |Evet |
| DataServiceTransportException |Hayır |Hayır |Evet |Evet |
| TimeoutException |Evet |Evet |Evet |Hayır |
| SocketException |Evet |Evet |Evet |Evet |
| StorageException |Hayır |Yes |Hayır |Hayır |
| Ioexception |Hayır |Yes |Hayır |Hayır |

### <a name="WebExceptionStatus"></a>WebException durum kodları
Merhaba aşağıdaki tabloda WebException hata kodları hello yeniden deneme mantığı uygulanır gösterilmektedir. Merhaba [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) numaralandırma hello durum kodları tanımlar.  

| Durum | Web isteği | Depolama | Sorgu | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |Evet |Evet |Evet |Evet |
| NameResolutionFailure |Evet |Evet |Evet |Evet |
| ProxyNameResolutionFailure |Evet |Evet |Evet |Evet |
| SendFailure |Evet |Evet |Evet |Evet |
| PipelineFailure |Evet |Evet |Evet |Hayır |
| ConnectionClosed |Evet |Evet |Evet |Hayır |
| KeepAliveFailure |Evet |Evet |Evet |Hayır |
| Başvuruları |Evet |Evet |Evet |Hayır |
| ReceiveFailure |Evet |Evet |Evet |Hayır |
| RequestCanceled |Evet |Evet |Evet |Hayır |
| Zaman aşımı |Evet |Evet |Evet |Hayır |
| ProtocolError <br/>ProtocolError Hello yeniden hello HTTP durum kodu işleme tarafından denetlenir. Daha fazla bilgi için bkz: [HTTP hata durum kodları](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Evet |Evet |Evet |Evet |

### <a name="HTTPStatusCode"></a>HTTP hata durum kodları
Sorgu ve SaveChanges işlemleri DataServiceClientException, DataServiceQueryException veya DataServiceQueryException throw hello HTTP hata durum kodu hello StatusCode özelliği döndürülür.  Merhaba aşağıdaki tabloda için hangi hata kodları hello yeniden deneme mantığı uygulanır gösterilmektedir.  

| Durum | Web isteği | Depolama | Sorgu | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |Hayır |Yes |Hayır |Hayır |
| 403 |Hayır |Evet<br/>İşleme deneme ile uzun bekler. |Hayır |Hayır |
| 408 |Evet |Evet |Evet |Evet |
| 429 |Evet |Evet |Evet |Evet |
| 500 |Evet |Evet |Evet |Hayır |
| 502 |Evet |Evet |Evet |Hayır |
| 503 |Evet |Evet |Evet |Evet |
| 504 |Evet |Evet |Evet |Hayır |

.NET yeniden deneme mantığı için tootake hello gerçek hello Media Services SDK'sı uyarlamasını bakmak istiyorsanız bkz [azure SDK'sı için media services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

