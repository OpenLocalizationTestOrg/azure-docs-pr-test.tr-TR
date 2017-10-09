---
title: "aaaAzure Service Bus kimlik doğrulama ve yetkilendirme | Microsoft Docs"
description: "Paylaşılan erişim imzası (SAS) kimlik doğrulaması ile uygulamaları tooService veri yolu kimlik doğrulaması."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Service Bus kimlik doğrulaması ve yetkilendirme

Uygulamaları tooAzure Service Bus paylaşılan erişim imzası (SAS) kullanarak kimlik doğrulaması kimlik doğrulaması. Paylaşılan erişim imzası kimlik doğrulamasını etkinleştirir uygulamaları tooauthenticate tooService hello ad alanı veya belirli haklar ilişkili hello varlık yapılandırılmış bir erişim anahtarı kullanarak veri yolu. Daha sonra bu anahtar toogenerate tooauthenticate tooService veri yolu istemcileri kullanabileceğiniz bir paylaşılan erişim imzası belirteci kullanabilirsiniz.

> [!IMPORTANT]
> ACS kullanım dışı olduğundan SAS Azure Active Directory erişim denetimi yerine (erişim denetimi hizmeti veya ACS olarak da bilinir) kullanmanız gerekir. SAS basit, esnek ve kullanımı kolay kimlik doğrulaması düzeni için hizmet veri yolu sağlar. Uygulamalar, bunlar toomanage hello yetkili bir "kullanıcı." kavramı gerekmez senaryolarında SAS kullanabilirsiniz Daha fazla bilgi için bkz: [bu blog gönderisine](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Paylaşılan erişim imzası kimlik doğrulaması

[SAS kimlik doğrulaması](service-bus-sas.md) , toogrant belirli haklarına sahip bir kullanıcı erişim tooService veri yolu kaynakları sağlar. Hizmet veri yolu SAS kimlik doğrulaması, bir şifreleme anahtarıyla ilişkili haklar bir Service Bus kaynakta hello yapılandırmasını içerir. İstemciler daha sonra erişim toothat kaynak hello Kaynak URI erişilen oluşan bir SAS belirteci sunarak erişebilir ve anahtar hello ile imzalanmış bir sona erme yapılandırılır.

Üzerinde bir hizmet veri yolu ad alanı için SAS anahtarları yapılandırabilirsiniz. Bu ad alanında Mesajlaşma varlıkları tooall Hello anahtar geçerlidir. Anahtarları aynı zamanda, Service Bus kuyrukları ve konuları da yapılandırabilirsiniz. SAS üzerinde desteklenen de [Azure geçiş](../service-bus-relay/relay-authentication-and-authorization.md).

yapılandırabileceğiniz toouse SAS, bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) ad alanı, kuyruk veya konu nesnesi. Bu kural öğeleri aşağıdaki hello oluşur:

* *KeyName* hello kuralı tanımlar.
* *PrimaryKey* olan bir şifreleme anahtarı kullanılan SAS belirteci toosign ve doğrulayın.
* *SecondaryKey* olan bir şifreleme anahtarı kullanılan SAS belirteci toosign ve doğrulayın.
* *Hakları* dinleme hello koleksiyonunu temsil eden, Gönder veya haklar verildi yönetin.

Merhaba ad alanı düzeyinde yapılandırılan yetkilendirme kuralları bir ad alanındaki varlıklara tooall istemciler için hello karşılık gelen anahtar kullanılarak imzalanmış belirteçleri ile erişim verebilir. Too12, bir hizmet veri yolu ad alanı, kuyruk veya konu gibi yetkilendirme kuralları yapılandırılabilir. Varsayılan olarak, bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) ilk sağlandığında tüm haklara sahip her ad alanı için yapılandırılır.

tooaccess varlık hello istemci gerektiren belirli bir kullanılarak oluşturulan bir SAS belirteci [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Merhaba SAS belirteci hello yetkilendirme kuralı ile ilişkili bir şifreleme anahtarı ile Merhaba Kaynak URI toowhich erişim içeren bir kaynak dize HMAC SHA256 talep hello ve bir süre sonu kullanılarak oluşturulur.

Hizmet veri yolu için SAS kimlik doğrulama desteği dahil hello Azure .NET SDK'sı sürüm 2.0 ve üzeri. SAS desteği içeren bir [Rootmanagesharedaccesskey](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Bir bağlantı dizesi parametresi olarak kabul tüm API'leri SAS bağlantı dizeleri için destek içerir.

## <a name="next-steps"></a>Sonraki adımlar

- Okuma devam [paylaşılan erişim imzaları ile Service Bus kimlik doğrulaması](service-bus-sas.md) SAS hakkında daha fazla ayrıntı için.
- [TooACS etkin ad alanları değiştirir.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Karşılık gelen Azure geçiş kimlik doğrulama ve yetkilendirme hakkında bilgi için [Azure geçiş kimlik doğrulama ve yetkilendirme](../service-bus-relay/relay-authentication-and-authorization.md). 

