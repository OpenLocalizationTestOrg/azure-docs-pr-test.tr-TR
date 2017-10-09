---
title: "İstek-yanıt tabanlı Azure Service Bus işlemlerinde 1.0 aaaAMQP | Microsoft Docs"
description: "Microsoft Azure Service Bus istek/yanıt tabanlı işlemleri listesi."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>Microsoft Azure hizmet veri yolu AMQP 1.0: istek-yanıt tabanlı işlemleri

Bu konu, Microsoft Azure Service Bus istek/yanıt tabanlı işlemleri hello listesini tanımlar. Bu bilgiler üzerinde hello AMQP yönetim sürüm 1.0 çalışma taslak dayanır.  
  
Merhaba nasıl Service Bus uygular ve OASIS AMQP teknik belirtim hello üzerinde derlemeler açıklayan, ayrıntılı Hat düzeyinde AMQP 1.0 protokolü kılavuzu için bkz: [AMQP 1.0 Azure Service Bus ve Event Hubs Protokolü Kılavuzu'nda](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Kavramlar  
  
### <a name="entity-description"></a>Varlık açıklaması  

Bir varlık açıklaması tooeither Service Bus başvuruyor [QueueDescription sınıfı](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription sınıfı](/dotnet/api/microsoft.servicebus.messaging.topicdescription), veya [SubscriptionDescription sınıfı](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) nesnesi.  
  
### <a name="brokered-message"></a>Aracılık edilen ileti  

Eşlenen tooan AMQP iletisi Service Bus içinde bir ileti temsil eder. Merhaba eşleme hello tanımlanan [hizmet veri yolu AMQP protokolünü Kılavuzu](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Tooentity yönetim düğümü ekleme  

Bu belgede açıklanan tüm hello işlemleri istek/yanıt desenler izleyen, kapsamlı tooan varlığı ve tooan varlık yönetim düğümü bağlanmasını gerektirir.  
  
### <a name="create-link-for-sending-requests"></a>İstekleri göndermek için bağlantı oluşturma  

İstekleri göndermek için bir bağlantı toohello yönetim düğümü oluşturur.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Yanıtları almak için bağlantı oluşturma  

Merhaba yönetim düğümden yanıtları almak için bir bağlantı oluşturur.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Bir istek iletisi Aktarım  

Bir istek iletisi aktarır.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Bir yanıt iletisi alıyorsunuz  

Merhaba yanıt bağlantısından Hello yanıt iletisini alır.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
Merhaba yanıt iletisi hello form aşağıdaki gibidir:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Service Bus varlık adresi  

Hizmet veri yolu varlıklarını gibi ele alınması gerekir:  
  
|Varlık türü|Adres|Örnek|  
|-----------------|-------------|-------------|  
|Sırası|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|Konu|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|aboneliği|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Mesaj işlemleri  
  
### <a name="message-renew-lock"></a>İleti kilit yenileme  

Merhaba varlık açıklamasında belirtilen hello zamana göre bir iletinin Hello kilit genişletir.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
 Merhaba istek ileti gövdesi girişleri aşağıdaki hello ile eşleme içeren bir amqp değer bölümünde oluşması gerekir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|UUID dizisi|Evet|İleti kilit belirteçleri toorenew.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu.|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi girişleri aşağıdaki hello ile eşleme içeren bir amqp değer bölümünde oluşması gerekir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|süre sonu|zaman damgası dizisi|Evet|İleti belirteci yeni sona erme karşılık gelen toohello kilit belirteç isteme kilitleyin.|  
  
### <a name="peek-message"></a>İletiye Gözat  

İletileri kilitlemeden iletiye göz atar.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|uzun|Evet|Hangi toostart gözlem numarasından dizisi.|  
|`message-count`|Int|Evet|İletileri toopeek maksimum sayısı.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – daha fazla ileti sahip<br /><br /> 0xcc: Hayır içerik – daha fazla ileti yok|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sayısı|eşlemeleri listesi|Evet|Her eşleme bir iletiyi temsil eden iletilerinin listesi.|  
  
bir ileti temsil eden hello harita girişleri aşağıdaki hello içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|İleti|bayt dizisi|Evet|Hat üzeri olarak kodlanmış bir AMQP 1.0 ileti.|  
  
### <a name="schedule-message"></a>Zamanlama iletisi  

İletileri zamanlar.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sayısı|eşlemeleri listesi|Evet|Her eşleme bir iletiyi temsil eden iletilerinin listesi.|  
  
bir ileti temsil eden hello harita girişleri aşağıdaki hello içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|ileti kimliği|Dize|Evet|`amqpMessage.Properties.MessageId`dize olarak|  
|oturum kimliği|Dize|Evet|`amqpMessage.Properties.GroupId as string`|  
|Bölüm anahtarı|Dize|Evet|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|İleti|bayt dizisi|Evet|Hat üzeri olarak kodlanmış bir AMQP 1.0 ileti.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu.|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölümü girdileri aşağıdaki hello ile eşleme içeren:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sıra numaraları|uzun dizi|Evet|Zamanlanmış ileti sıra numarası. Sıra numarası kullanılan toocancel ' dir.|  
  
### <a name="cancel-scheduled-message"></a>Zamanlanmış iletiyi iptal etme  

Zamanlanmış iletileri iptal eder.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sıra numaraları|uzun dizi|Evet|Zamanlanmış iletileri toocancel sıra numarası.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu.|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölümü girdileri aşağıdaki hello ile eşleme içeren:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sıra numaraları|uzun dizi|Evet|Zamanlanmış ileti sıra numarası. Sıra numarası kullanılan toocancel ' dir.|  
  
## <a name="session-operations"></a>Oturum işlemleri  
  
### <a name="session-renew-lock"></a>Oturum kilidi yenileme  

Merhaba varlık açıklamasında belirtilen hello zamana göre bir iletinin Hello kilit genişletir.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|oturum kimliği|Dize|Evet|Oturum kimliği|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – daha fazla ileti sahip<br /><br /> 0xcc: Hayır içerik – daha fazla ileti yok|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölümü girdileri aşağıdaki hello ile eşleme içeren:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|süre sonu|timestamp|Evet|Yeni süre sonu.|  
  
### <a name="peek-session-message"></a>Oturum İletiye Gözat  

Oturum iletileri kilitlemeden iletiye göz atar.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sırası-sayı|uzun|Evet|Hangi toostart gözlem numarasından dizisi.|  
|ileti sayısı|Int|Evet|İletileri toopeek maksimum sayısı.|  
|oturum kimliği|Dize|Evet|Oturum kimliği|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – daha fazla ileti sahip<br /><br /> 0xcc: Hayır içerik – daha fazla ileti yok|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölümü girdileri aşağıdaki hello ile eşleme içeren:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sayısı|eşlemeleri listesi|Evet|Her eşleme bir iletiyi temsil eden iletilerinin listesi.|  
  
 bir ileti temsil eden hello harita girişleri aşağıdaki hello içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|İleti|bayt dizisi|Evet|Hat üzeri olarak kodlanmış bir AMQP 1.0 ileti.|  
  
### <a name="set-session-state"></a>Oturum durumunu belirle  

Ayarlar, bir oturum durumunu hello.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|oturum kimliği|Dize|Evet|Oturum kimliği|  
|oturum durumu|bir bayt dizisi|Evet|Donuk ikili veri.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
### <a name="get-session-state"></a>Get oturum durumu  

Bir oturum Hello durumunu alır.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|oturum kimliği|Dize|Evet|Oturum kimliği|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|oturum durumu|bir bayt dizisi|Evet|Donuk ikili veri.|  
  
### <a name="enumerate-sessions"></a>Oturumları listeleme  

Bir Mesajlaşma varlığı oturumlarını numaralandırır.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|Son güncelleştirme saati|timestamp|Evet|Belirli bir süre sonra güncelleştirilmiş tooinclude yalnızca oturumları filtreleyin.|  
|Atla|Int|Evet|Oturum sayısını atlayın.|  
|Sayfanın Üstü|Int|Evet|En fazla oturum sayısını.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – daha fazla ileti sahip<br /><br /> 0xcc: Hayır içerik – daha fazla ileti yok|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|Atla|Int|Evet|Durum kodu 200 ise Atlanan oturum sayısı.|  
|oturumları kimlikleri|Dize dizisi|Evet|Oturum durum kodu 200 ise kimlikleri dizisi.|  
  
## <a name="rule-operations"></a>Kuralı işlemleri  
  
### <a name="add-rule"></a>Kural Ekle  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|Kural adı|Dize|Evet|Kural adı, abonelik ve konu adları dahil edilmez.|  
|Kural açıklaması|eşleme|Evet|Sonraki bölümde belirtildiği gibi kural açıklaması.|  
  
Merhaba **kural açıklaması** harita girişleri, aşağıdaki hello içermelidir nerede **sql filtresi** ve **bağıntı filtresi** karşılıklı olarak birbirini dışlar:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|SQL filtresi|eşleme|Evet|`sql-filter`, hello sonraki bölümde belirtildiği gibi.|  
|Bağıntı filtresi|eşleme|Evet|`correlation-filter`, hello sonraki bölümde belirtildiği gibi.|  
|SQL kural eylemi|eşleme|Evet|`sql-rule-action`, hello sonraki bölümde belirtildiği gibi.|  
  
Merhaba sql filtresi eşleme girdileri aşağıdaki hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|ifade|Dize|Evet|SQL filtre ifadesi.|  
  
Merhaba **bağıntı filtresi** harita girişleri aşağıdaki hello en az birini içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|Bağıntı Kimliği|Dize|Hayır||  
|ileti kimliği|Dize|Hayır||  
|-|Dize|Hayır||  
|Yanıtla|Dize|Hayır||  
|Etiket|Dize|Hayır||  
|oturum kimliği|Dize|Hayır||  
|yanıt için oturum kimliği|Dize|Hayır||  
|içerik türü|Dize|Hayır||  
|properties|eşleme|Hayır|TooService Bus eşlemeleri [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Merhaba **sql kural eylemi** harita girişleri aşağıdaki hello içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|ifade|Dize|Evet|SQL eylem ifade.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
### <a name="remove-rule"></a>Kuralını Kaldır  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|Kural adı|Dize|Evet|Kural adı, abonelik ve konu adları dahil edilmez.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
## <a name="deferred-message-operations"></a>Ertelenmiş ileti işlemleri  
  
### <a name="receive-by-sequence-number"></a>Seri numarasına göre alma  

Sıra numarası tarafından ertelenmiş iletilerini alır.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sıra numaraları|uzun dizi|Evet|Sıra numaraları.|  
|Alıcı kapatma modu|ubyte|Evet|**Alıcı kapatma** AMQP çekirdek v1.0 belirtildiği gibi modu.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|  
  
Merhaba yanıt ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|sayısı|eşlemeleri listesi|Evet|Her eşleme bir ileti temsil ettiği ileti listesi.|  
  
bir ileti temsil eden hello harita girişleri aşağıdaki hello içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|kilit simgesi|UUID|Evet|Kilit belirteci IF `receiver-settle-mode` 1'dir.|  
|İleti|bayt dizisi|Evet|Hat üzeri olarak kodlanmış bir AMQP 1.0 ileti.|  
  
### <a name="update-disposition-status"></a>Değerlendirme durumunu güncelleştir  

Ertelenmiş iletilerin Hello değerlendirme durumunu güncelleştirir.  
  
#### <a name="request"></a>İstek  

Merhaba istek iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|işlemi|Dize|Evet|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|Hayır|Milisaniye cinsinden işlem sunucusu zaman aşımı.|  
  
Merhaba istek ileti gövdesi oluşmalıdır bir **amqp değeri** bölüm içeren bir **harita** girişleri aşağıdaki hello ile:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|Değerlendirme durumu|Dize|Evet|tamamlandı<br /><br /> terk<br /><br /> askıya alındı|  
|Kilit belirteçleri|UUID dizisi|Evet|İleti kilit belirteçleri tooupdate değerlendirme durumu.|  
|sahipsiz nedeni|Dize|Hayır|Değerlendirme durumu çok ayarlandıysa ayarlanabilir**askıya**.|  
|sahipsiz açıklaması|Dize|Hayır|Değerlendirme durumu çok ayarlandıysa ayarlanabilir**askıya**.|  
|değiştirme özellikleri|eşleme|Hayır|Hizmet veri yolu listesi ileti özellikleri toomodify aracılı.|  
  
#### <a name="response"></a>Yanıt  

Merhaba yanıt iletisi aşağıdaki uygulama özelliklere hello şunları içermelidir:  
  
|Anahtar|Değer türü|Gerekli|Değer içeriği|  
|---------|----------------|--------------|--------------------|  
|statusCode|Int|Evet|HTTP yanıt kodunu [RFC2616]<br /><br /> 200: Tamam – başarılı, aksi takdirde başarısız oldu|  
|StatusDescription|Dize|Hayır|Merhaba durum açıklaması.|

## <a name="next-steps"></a>Sonraki adımlar

AMQP ve Service Bus hakkında daha fazla toolearn bağlantılar aşağıdaki hello ziyaret edin:

* [Hizmet veri yolu AMQP genel bakış]
* [AMQP 1.0 desteği bölümlenmiş Service Bus kuyrukları ve konuları]
* [Windows Server için hizmet veri yolu AMQP]

[Hizmet veri yolu AMQP genel bakış]: service-bus-amqp-overview.md
[AMQP 1.0 desteği bölümlenmiş Service Bus kuyrukları ve konuları]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server için hizmet veri yolu AMQP]: https://msdn.microsoft.com/library/dn574799.asp