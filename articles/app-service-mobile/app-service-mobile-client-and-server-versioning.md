---
title: "Mobil uygulamaları ve Mobile Services aaaClient ve sunucu SDK sürüm | Microsoft Docs"
description: "İstemci SDK'ları listesi ve Mobile Services ve Azure mobil uygulamalar sunucusu SDK sürümleriyle uyumluluk"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Mobil uygulamaları ve Mobile Services istemci ve sunucu sürüm oluşturma
Merhaba en son Azure Mobile Services sürümüdür hello **Mobile Apps** Azure uygulama hizmeti özelliğidir.

Mobil uygulamaları istemci hello ve sunucu SDK başlangıçta temel Mobile Services de, ancak bunlar *değil* birbiriyle uyumlu.
Diğer bir deyişle, kullanmanız gereken bir *Mobile Apps* istemci SDK'sı ile bir *Mobile Apps* sunucusu SDK ve benzer şekilde *Mobile Services*. Bu sözleşme hello istemci ve sunucu SDK'ları, tarafından kullanılan bir özel üstbilgi değeri aracılığıyla zorlanır `ZUMO-API-VERSION`.

Not: her bu belgeyi başvuruyor tooa *Mobile Services* arka uç, onu mutlaka gerekmez Mobile Services üzerinde barındırılan toobe. Şu anda olası toomigrate kod değişiklikleri olmadan uygulama hizmeti üzerinde bir mobil hizmet toorun durumdadır ancak hello hizmet hala kullanıyor *Mobile Services* SDK sürümleri.

hakkında daha fazla bilgi toolearn hello makaleye bakın tooApp hizmet kod değişiklikleri olmadan geçirme [mobil hizmeti tooAzure uygulama hizmeti geçirmek].

## <a name="header-specification"></a>Üstbilgi belirtimi
başlangıç anahtarı `ZUMO-API-VERSION` hello HTTP üstbilgisi veya hello sorgu dizesi olarak belirtilebilir. Merhaba değerdir hello formunda bir sürüm dizesi **x.y.z**.

Örneğin:

Https://Service.azurewebsites.NET/Tables/TodoItem Al

ÜSTBİLGİLERİ: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Sürüm denetimi dışında kullanmama
Sürüm değerine ayarlayarak denetimini dışında seçebilirsiniz **true** hello uygulama ayarı için **MS_SkipVersionCheck**. Bu, web.config dosyanıza veya hello hello Azure portalında uygulama ayarları bölümü belirtin.

> [!NOTE]
> Mobile Services ve çevrimdışı eşitleme, kimlik doğrulaması ve anında iletme bildirimleri hello alanlarda özellikle mobil uygulamalar arasında davranış değişiklikleri mevcuttur. Bu davranış değişiklikleri uygulamanızın işlevselliği bozmadığını sonra tam sınama tooensure denetimi sürüm dışında yalnızca tercih.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Tüm sürümler için Uyumluluk özeti
tüm istemci ve sunucu türleri arasında hello uyumluluk aşağıdaki Hello grafik gösterir. Bir arka uç ya da mobil sınıflandırılır **Hizmetleri** ya da mobil **uygulamaları** kullandığı SDK hello sunucuya göre.

|  | **Mobil Hizmetler** Node.js veya .NET | **Mobil uygulamaları** Node.js veya .NET |
| --- | --- | --- |
| [Mobile Services istemcileri] |Tamam |Hata\* |
| [Mobile Apps istemcileri] |Hata\* |Tamam |

\*Bu belirterek denetlenebilir **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Mobile Services İstemcisi ve sunucusu
Aşağıdaki hello tablosundaki Hello istemci SDK'ları ile uyumlu **Mobile Services**.

Not: Mobile Services istemci SDK'ları hello *sağlamadığı* bir üstbilgi değeri göndermek `ZUMO-API-VERSION`. Bu üst bilgi veya sorgu dizesi değerini Hello hizmet alırsa, açıkça yukarıda açıklandığı gibi out çevirdiniz sürece bir hata döndürülür.

### <a name="MobileServicesClients"></a>Mobil *Hizmetleri* istemci SDK'ları
| İstemci Platformu | Sürüm | Version üstbilgi değeri |
| --- | --- | --- |
| Yönetilen istemci (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |yok |
| iOS |[2.2.2](http://aka.ms/gc6fex) |yok |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |yok |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |yok |

### <a name="mobile-services-server-sdks"></a>Mobil *Hizmetleri* sunucusu SDK
| Sunucu platformu | Sürüm | Kabul edilen sürüm üst bilgisi |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* sürüm 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |** Hiçbir sürüm üst bilgisi ** |
| Node.js |(yakında) |**Hiçbir sürüm üst bilgisi** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Mobile Services arka uçlarını davranışı
| ZUMO-API-VERSION | MS_SkipVersionCheck değeri | Yanıt |
| --- | --- | --- |
| Belirtilmemiş. |Herhangi biri |200 - TAMAM |
| Herhangi bir değer |True |200 - TAMAM |
| Herhangi bir değer |Belirtilen false/değil |400 - Hatalı istek |

## <a name="2.0.0"></a>Azure Mobile Apps istemci ve sunucu
### <a name="MobileAppsClients"></a>Mobil *uygulamaları* istemci SDK'ları
Sürüm denetimi sunulmuştur hello istemci SDK sürümleri aşağıdaki hello ile başlatma için **Azure Mobile Apps**:

| İstemci Platformu | Sürüm | Version üstbilgi değeri |
| --- | --- | --- |
| Yönetilen istemci (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>Mobil *uygulamaları* sunucusu SDK
Sürüm denetimi server SDK sürümleri aşağıdaki eklenmiştir:

| Sunucu platformu | SDK | Kabul edilen sürüm üst bilgisi |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[Azure-mobile-uygulamalar)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Mobile Apps arka uçlarını davranışı
| ZUMO-API-VERSION | MS_SkipVersionCheck değeri | Yanıt |
| --- | --- | --- |
| x.y.z ya da Null |True |200 - TAMAM |
| Null |Belirtilen false/değil |400 - Hatalı istek |
| 1.x.y |Belirtilen false/değil |400 - Hatalı istek |
| 2.0.0-2.x.y |Belirtilen false/değil |200 - TAMAM |
| 3.0.0-3.x.y |Belirtilen false/değil |400 - Hatalı istek |

## <a name="next-steps"></a>Sonraki Adımlar
* [mobil hizmeti tooAzure uygulama hizmeti geçirmek]

[Mobile Services istemcileri]: #MobileServicesClients
[Mobile Apps istemcileri]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[mobil hizmeti tooAzure uygulama hizmeti geçirmek]: app-service-mobile-migrating-from-mobile-services.md
