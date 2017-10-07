---
title: "aaaAzure geçiş kimlik doğrulama ve yetkilendirme | Microsoft Docs"
description: "Azure geçişi, paylaşılan erişim imzası (SAS) kimlik doğrulamasına genel bakış"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Azure geçiş kimlik doğrulama ve yetkilendirme
Uygulamaları tooAzure kimlik doğrulaması paylaşılan erişim imzası (SAS) kimlik doğrulaması kullanarak geçiş. Benzer çok[Service Bus Mesajlaşma](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS kimlik doğrulama uygulamaları tooauthenticate toohello hello geçiş ad yapılandırılmış bir erişim anahtarı kullanarak Azure geçiş hizmeti sağlar. Daha sonra bu anahtar toogenerate istemcileri tooauthenticate toohello geçiş hizmeti kullanabileceğiniz bir paylaşılan erişim imzası belirteci kullanabilirsiniz.

## <a name="shared-access-signature-authentication"></a>Paylaşılan erişim imzası kimlik doğrulaması
[SAS kimlik doğrulaması](../service-bus-messaging/service-bus-sas.md) , toogrant belirli haklarına sahip bir kullanıcı erişim tooAzure geçiş kaynakları sağlar. SAS kimlik doğrulaması, bir şifreleme anahtarıyla ilişkili haklar bir kaynakta hello yapılandırmasını içerir. İstemciler daha sonra erişim toothat kaynak hello Kaynak URI erişilen oluşan bir SAS belirteci sunarak erişebilir ve anahtar hello ile imzalanmış bir sona erme yapılandırılır.

Bir geçiş ad için SAS anahtarları yapılandırabilirsiniz. Service Bus Mesajlaşma, aksine [geçişi karma bağlantılar](relay-hybrid-connections-protocol.md) yetkisiz veya anonim göndericiler destekler. Oluşturduğunuzda hello hello portalından ekran aşağıdaki gösterildiği gibi hello varlık için anonim erişimi etkinleştirebilirsiniz:

![][0]

yapılandırabileceğiniz toouse SAS, bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) hello aşağıdaki oluşur geçiş ad alanı nesnede:

* *KeyName* hello kuralı tanımlar.
* *PrimaryKey* olan bir şifreleme anahtarı kullanılan SAS belirteci toosign ve doğrulayın.
* *SecondaryKey* olan bir şifreleme anahtarı kullanılan SAS belirteci toosign ve doğrulayın.
* *Hakları* dinleme hello koleksiyonunu temsil eden, Gönder veya haklar verildi yönetin.

Merhaba ad alanı düzeyinde yapılandırılan yetkilendirme kuralları, hello karşılık gelen anahtar kullanılarak imzalanmış belirteçleri ile istemciler için bir ad alanındaki tooall geçiş bağlantıları erişim izni verebilir. Too12 böyle yetkilendirme kuralları bir geçiş ad yapılandırılabilir. Varsayılan olarak, bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) ilk sağlandığında tüm haklara sahip her ad alanı için yapılandırılır.

tooaccess varlık hello istemci gerektiren belirli bir kullanılarak oluşturulan bir SAS belirteci [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Merhaba SAS belirteci hello yetkilendirme kuralı ile ilişkili bir şifreleme anahtarı ile Merhaba Kaynak URI toowhich erişim içeren bir kaynak dize HMAC SHA256 talep hello ve bir süre sonu kullanılarak oluşturulur.

' Hello Azure .NET SDK'sını sürümlerinde 2.0 ve sonraki sürümlerinde Azure geçişi için SAS kimlik doğrulama desteği. SAS desteği içeren bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Bir bağlantı dizesi parametresi olarak kabul tüm API'leri SAS bağlantı dizeleri için destek içerir.

## <a name="next-steps"></a>Sonraki adımlar
- Okuma devam [paylaşılan erişim imzaları ile Service Bus kimlik doğrulaması](../service-bus-messaging/service-bus-sas.md) SAS hakkında daha fazla ayrıntı için.
- Merhaba bkz [Azure geçişi karma bağlantılar Protokolü Kılavuzu](relay-hybrid-connections-protocol.md) hello karma bağlantılar yetenek hakkında ayrıntılı bilgi için.
- Service Bus Mesajlaşma hizmeti kimlik doğrulama ve yetkilendirme hakkında ilgili bilgi için bkz: [Service Bus kimlik doğrulama ve yetkilendirme](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png