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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="a1f8e-103">Service Fabric Reliable Actors Notlar serileştirme yazın</span><span class="sxs-lookup"><span data-stu-id="a1f8e-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="a1f8e-104">Merhaba bağımsız değişkenleri tüm yöntemlerin aktör arabirimdeki her yöntem tarafından döndürülen sonuç türleri'hello görevlerin ve bir aktör'ın durum Yöneticisi'nde depolanan nesneler olmalıdır [veri sözleşmesi seri hale getirilebilir](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1f8e-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="a1f8e-105">Bu aynı zamanda tanımlanan hello yöntemleri toohello bağımsız geçerlidir [aktör olay arabirimleri](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="a1f8e-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="a1f8e-106">(Aktör olay arabirim yöntemleri her zaman boş döndürmeleri.)</span><span class="sxs-lookup"><span data-stu-id="a1f8e-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="a1f8e-107">Özel veri türleri</span><span class="sxs-lookup"><span data-stu-id="a1f8e-107">Custom data types</span></span>
<span data-ttu-id="a1f8e-108">Bu örnekte, aktör arabirimi aşağıdaki hello adlı bir özel veri türü döndüren bir yöntem tanımlar `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="a1f8e-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="a1f8e-109">Merhaba arabirimi hello durumu Yöneticisi toostore kullanan bir oyuncu tarafından uygulanan bir `VoicemailBox` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="a1f8e-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="a1f8e-110">Bu örnekte, hello `VoicemailBox` nesne seri hale getirilmiş zaman:</span><span class="sxs-lookup"><span data-stu-id="a1f8e-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="a1f8e-111">Merhaba nesne çağıran aktör örneği arasında aktarılır.</span><span class="sxs-lookup"><span data-stu-id="a1f8e-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="a1f8e-112">Merhaba nesne burada kalıcı toodisk ve tooother düğümleri çoğaltılan hello durum Yöneticisi'nde kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a1f8e-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="a1f8e-113">Merhaba güvenilir aktör çerçevesi DataContract serileştirme kullanır.</span><span class="sxs-lookup"><span data-stu-id="a1f8e-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="a1f8e-114">Bu nedenle, özel veri nesneleri hello ve üyeleri hello ile Açıklama eklenmelidir **DataContract** ve **DataMember** öznitelikleri, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="a1f8e-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="a1f8e-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1f8e-115">Next steps</span></span>
* [<span data-ttu-id="a1f8e-116">Aktör yaşam döngüsü ve çöp toplama</span><span class="sxs-lookup"><span data-stu-id="a1f8e-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="a1f8e-117">Aktör zamanlayıcılar ve anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="a1f8e-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="a1f8e-118">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="a1f8e-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="a1f8e-119">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="a1f8e-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="a1f8e-120">Aktör çok biçimlilik ve nesne odaklı tasarım desenleri</span><span class="sxs-lookup"><span data-stu-id="a1f8e-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="a1f8e-121">Aktör tanılama ve performans izleme</span><span class="sxs-lookup"><span data-stu-id="a1f8e-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
