---
title: "Aktör aaaReliable aktörler Notlar türü seri hale getirme | Microsoft Docs"
description: "Service Fabric Reliable Actors durumları kullanılan toodefine olabilir serileştirilebilir sınıflar ve arabirimler tanımlamak için temel gereksinimler açıklanır"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Service Fabric Reliable Actors Notlar serileştirme yazın
Merhaba bağımsız değişkenleri tüm yöntemlerin aktör arabirimdeki her yöntem tarafından döndürülen sonuç türleri'hello görevlerin ve bir aktör'ın durum Yöneticisi'nde depolanan nesneler olmalıdır [veri sözleşmesi seri hale getirilebilir](https://msdn.microsoft.com/library/ms731923.aspx). Bu aynı zamanda tanımlanan hello yöntemleri toohello bağımsız geçerlidir [aktör olay arabirimleri](service-fabric-reliable-actors-events.md). (Aktör olay arabirim yöntemleri her zaman boş döndürmeleri.)

## <a name="custom-data-types"></a>Özel veri türleri
Bu örnekte, aktör arabirimi aşağıdaki hello adlı bir özel veri türü döndüren bir yöntem tanımlar `VoicemailBox`:

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

Merhaba arabirimi hello durumu Yöneticisi toostore kullanan bir oyuncu tarafından uygulanan bir `VoicemailBox` nesnesi:

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

Bu örnekte, hello `VoicemailBox` nesne seri hale getirilmiş zaman:

* Merhaba nesne çağıran aktör örneği arasında aktarılır.
* Merhaba nesne burada kalıcı toodisk ve tooother düğümleri çoğaltılan hello durum Yöneticisi'nde kaydedilir.

Merhaba güvenilir aktör çerçevesi DataContract serileştirme kullanır. Bu nedenle, özel veri nesneleri hello ve üyeleri hello ile Açıklama eklenmelidir **DataContract** ve **DataMember** öznitelikleri, sırasıyla.

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a>Sonraki adımlar
* [Aktör yaşam döngüsü ve çöp toplama](service-fabric-reliable-actors-lifecycle.md)
* [Aktör zamanlayıcılar ve anımsatıcıları](service-fabric-reliable-actors-timers-reminders.md)
* [Aktör olayları](service-fabric-reliable-actors-events.md)
* [Aktör yeniden giriş](service-fabric-reliable-actors-reentrancy.md)
* [Aktör çok biçimlilik ve nesne odaklı tasarım desenleri](service-fabric-reliable-actors-polymorphism.md)
* [Aktör tanılama ve performans izleme](service-fabric-reliable-actors-diagnostics.md)
