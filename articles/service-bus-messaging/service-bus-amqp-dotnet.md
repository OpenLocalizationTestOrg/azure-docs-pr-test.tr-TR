---
title: aaaService Bus .NET ve AMQP 1.0 ile | Microsoft Docs
description: .NET gelen Azure hizmet veri yolu AMQP ile kullanma
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>.NET gelen hizmet veri yolu AMQP 1.0 ile kullanma

## <a name="downloading-hello-service-bus-sdk"></a>Merhaba hizmet veri yolu SDK'sını indirme

AMQP 1.0 desteği hello hizmet veri yolu SDK 2.1 veya sonraki bir sürümü kullanılabilir. Merhaba Service Bus bitten yükleyerek hello en son sürümüne sahip olmak [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>.NET uygulamaları toouse AMQP 1.0 yapılandırma

Varsayılan olarak, hello Service Bus .NET istemci kitaplığı hello adanmış bir SOAP tabanlı protokolü kullanarak Service Bus hizmeti ile iletişim kurar. toouse AMQP 1.0 hello varsayılan protokolü yerine hello sonraki bölümde açıklandığı gibi hello hizmet veri yolu bağlantı dizesini açık yapılandırma gerektirir. Bu değişiklik dışında AMQP 1.0 kullanırken uygulama kodu değişmeden kalır.

Merhaba geçerli sürümde AMQP kullanırken desteklenmez birkaç API özellikler vardır. Desteklenmeyen bu özellikleri daha sonra hello bölümünde listelenen [desteklenmeyen özellikler, sınırlamalar ve davranış farklılıkları](#unsupported-features-restrictions-and-behavioral-differences). Bazı gelişmiş yapılandırma ayarları hello ayrıca farklı bir anlam AMQP kullanırken sahiptir.

### <a name="configuration-using-appconfig"></a>App.config kullanarak yapılandırma

Uygulamaları toouse hello App.config yapılandırma dosyası toostore ayarları iyi bir uygulamadır. Hizmet veri yolu uygulamaları için App.config toostore hello hizmet veri yolu bağlantı dizesi kullanabilirsiniz. Örnek bir App.config dosyası aşağıdaki gibidir:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

Merhaba hello değerini `Microsoft.ServiceBus.ConnectionString` kullanılan tooconfigure hello bağlantı tooService veri yolu olan hello hizmet veri yolu bağlantı dizesi bir ayardır. Merhaba biçimi aşağıdaki gibidir:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Burada `[namespace]` ve `SharedAccessKey` hello elde edilen [Azure portal] [ Azure portal] bir hizmet veri yolu ad alanı oluşturduğunuzda. Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturma][Create a Service Bus namespace using hello Azure portal].

AMQP kullanırken hello bağlantı dizesi ile sona `;TransportType=Amqp`. Bu gösterim hello istemci kitaplığı toomake kendi bağlantı tooService veri yolu AMQP 1.0 kullanarak bildirir.

## <a name="message-serialization"></a>İleti seri hale getirme

Merhaba varsayılan protokolü kullanılırken hello varsayılan seri hale getirme hello .NET istemci kitaplığı toouse hello davranıştır [DataContractSerializer] [ DataContractSerializer] tooserialize yazın bir [BrokeredMessage ] [ BrokeredMessage] hello istemci kitaplığı ile Merhaba Service Bus hizmeti arasında aktarım için örneği. Merhaba AMQP aktarım modu kullanırken hello istemci kitaplığı hello AMQP tür sistemi hello serileştirmek için kullanır. [aracılı ileti] [ BrokeredMessage] bir AMQP iletisine. Bu seri hale getirme alınan ve potansiyel olarak, örneğin, hello JMS API tooaccess Service Bus kullanan bir Java uygulaması gibi farklı bir platform üzerinde çalışan bir alıcı uygulama tarafından yorumlanan hello ileti toobe sağlar.

Oluşturduğunuzda bir [BrokeredMessage] [ BrokeredMessage] örneği, bir parametre toohello Oluşturucusu tooserve hello hello ileti gövdesi olarak olarak .NET nesnesi sağlayabilir. Eşlenen tooAMQP ilkel türler olabilir nesneler için AMQP veri türleriyle hello gövde serileştirilir. Merhaba nesne doğrudan bir AMQP ilkel türe eşlenemez Merhaba uygulaması sonra hello nesnesi tarafından tanımlanan bir özel tür hello kullanılarak başka bir deyişle, serileştirilmiş [DataContractSerializer][DataContractSerializer], ve seri hello bayt bir AMQP veri iletisi gönderilir.

.NET olmayan istemcileri ile toofacilitate birlikte çalışabilirlik hello hello ileti gövdesi için AMQP türleri doğrudan serileştirilen .NET türleri kullanın. Aşağıdaki tablonun hello bu türleri ve hello karşılık gelen eşleme toohello AMQP tür sistemi ayrıntıları.

| .NET gövdesi nesne türü | Eşlenen AMQP türü | AMQP gövde bölümü türü |
| --- | --- | --- |
| bool |Boole değeri |AMQP değeri |
| Bayt |ubyte |AMQP değeri |
| ushort |ushort |AMQP değeri |
| uint |uint |AMQP değeri |
| ulong |ulong |AMQP değeri |
| sbyte |Bayt |AMQP değeri |
| kısa |kısa |AMQP değeri |
| Int |Int |AMQP değeri |
| uzun |uzun |AMQP değeri |
| Kayan nokta |Kayan nokta |AMQP değeri |
| Çift |Çift |AMQP değeri |
| Ondalık |decimal128 |AMQP değeri |
| char |char |AMQP değeri |
| Tarih saat |timestamp |AMQP değeri |
| GUID |UUID |AMQP değeri |
| Byte] |İkili |AMQP değeri |
| Dize |Dize |AMQP değeri |
| System.Collections.IList |Liste |AMQP değeri: hello derlemesinde öğeleri yalnızca, bu tabloda tanımlı olabilir. |
| System.Array |Dizi |AMQP değeri: hello derlemesinde öğeleri yalnızca, bu tabloda tanımlı olabilir. |
| System.Collections.IDictionary |eşleme |AMQP değeri: hello derlemesinde öğeleri yalnızca, bu tabloda tanımlı olabilir. Not: yalnızca dize anahtarları desteklenir. |
| URI |Dize açıklanan (aşağıdaki tablonun hello bakın) |AMQP değeri |
| DateTimeOffset |Uzun açıklanan (aşağıdaki tablonun hello bakın) |AMQP değeri |
| TimeSpan |Uzun açıklanan (Merhaba aşağıdakilere bakın) |AMQP değeri |
| Akış |İkili |AMQP verileri (birden çok olabilir). Merhaba veri bölümler hello Stream nesnesi okunan hello ham bayt içerir. |
| Başka bir nesne |İkili |AMQP verileri (birden çok olabilir). Serileştirilmiş hello ikili hello DataContractSerializer veya hello uygulama tarafından sağlanan bir seri hale getirici kullanan hello nesnesinin içerir. |

| .NET türü | Eşlenen AMQP türü açıklanan | Notlar |
| --- | --- | --- |
| URI |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| DateTimeOffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Desteklenmeyen özellikler, sınırlamalar ve davranış farklılıkları

AMQP kullanırken hello Service Bus .NET API özelliklerini aşağıdaki hello şu anda desteklenmez:

* İşlemler
* Aktarım hedef Gönder

Aynı zamanda AMQP, karşılaştırılan toohello varsayılan protokolü kullanırken ayrıca hello Service Bus .NET API hello davranışını bazı küçük farklılıklar vardır:

* Merhaba [OperationTimeout] [ OperationTimeout] özelliği yoksayılır.
* `MessageReceiver.Receive(TimeSpan.Zero)`olarak uygulanan `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Kilit belirteçleri tarafından iletileri Tamamlanıyor yalnızca başlangıçta Merhaba iletileri alınan hello ileti alıcı tarafından yapılabilir.

## <a name="controlling-amqp-protocol-settings"></a>AMQP protokol ayarlarını denetleme

Merhaba [.NET API'lerini](/dotnet/api/) çeşitli ayarları toocontrol hello davranışını hello AMQP protokolünü kullanıma:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: denetimleri hello uygulanan ilk kredi tooa bağlantı. Merhaba varsayılan 0'dır.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: denetimleri hello maksimum AMQP çerçeve boyutu sunulan bağlantı açık zaman hello anlaşması sırasında. Merhaba, 65,536 bayt varsayılandır.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: aktarımları batchable varsa, bu değer değerlendirmeleri göndermek için en büyük gecikme hello belirler. Varsayılan olarak Gönderenler/alıcılar tarafından devralınır. Tek tek gönderenin alıcı 20 milisaniyedir hello Varsayılanı geçersiz kılabilirsiniz.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: AMQP bağlantı bir SSL bağlantısı üzerinden kuran olup olmadığını denetler. Merhaba varsayılandır **doğru**.

## <a name="next-steps"></a>Sonraki adımlar

Toolearn daha hazır mısınız? Aşağıdaki bağlantılar hello ziyaret edin:

* [Hizmet veri yolu AMQP genel bakış]
* [AMQP 1.0 desteği bölümlenmiş Service Bus kuyrukları ve konuları]
* [Windows Server için hizmet veri yolu AMQP]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Hizmet veri yolu AMQP genel bakış]: service-bus-amqp-overview.md
[AMQP 1.0 desteği bölümlenmiş Service Bus kuyrukları ve konuları]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server için hizmet veri yolu AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
