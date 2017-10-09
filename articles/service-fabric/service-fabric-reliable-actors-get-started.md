---
title: "aaaCreate, ilk aktör tabanlı Azure mikro hizmet C# | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma hello adımlarda size yol gösterir."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Reliable Actors ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-actors-get-started.md)
> * [Linux üzerinde Java](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Bu makalede, Azure Service Fabric Reliable Actors hello temelleri açıklanır ve oluşturma, hata ayıklama ve Visual Studio basit bir güvenilir aktör uygulama dağıtma size yol gösterir.

## <a name="installation-and-setup"></a>Yükleme ve Kurulum
Başlamadan önce makinenizde ayarlanan hello Service Fabric geliştirme ortamı olduğundan emin olun.
Tooset gerekiyorsa, görmek ayrıntılı yönergeler üzerinde [nasıl hello geliştirme ortamını ayarlama tooset](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Temel kavramlar
Reliable Actors ile yalnızca, başlatılan tooget birkaç temel kavramları toounderstand gerekir:

* **Aktör hizmeti**. Güvenilir aktörler hello Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir. Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.
* **Aktör kayıt**. Olarak Reliable Services ile güvenilir aktör hizmeti ile Merhaba Service Fabric çalışma zamanı kayıtlı toobe gerekir. Ayrıca, hello aktör türü hello aktör çalışma zamanı ile kayıtlı toobe gerekir.
* **Aktör arabirimi**. Merhaba aktör kullanılan toodefine bir aktör kesin türü belirtilmiş bir ortak arabiriminin bir arabirimdir. Hello güvenilir aktör modeli terminolojisi, aktör Merhaba ileti türlerini anlamak ve işleyebilirsiniz hello hello aktör arabirimi tanımlar. Merhaba aktör arabirimi diğer aktörler tarafından kullanılır ve istemci uygulamaları çok "(uyumsuz) iletileri toohello aktör Gönder". Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.
* **ActorProxy sınıfı**. Merhaba ActorProxy sınıfı istemci uygulamaları tooinvoke tarafından kullanılan hello hello aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri. Merhaba ActorProxy sınıfı iki önemli işlevleri sağlar:
  
  * Ad çözümlemesi: mümkün toolocate hello aktör (bunu barındırıldığı hello kümesinin Bul hello düğümü) hello kümedeki olduğu.
  * Hata işleme: Bu yöntem çağrılarına yeniden deneyin ve sonra hello aktör konumu yeniden çözümlemek, örneğin, hello aktör toobe gerektiren bir hata hello kümedeki tooanother düğümde yeniden konumlandırılmasını.

tooactor arabirimleri ilgilidir kuralları aşağıdaki hello tümleştirilmediği şunlardır:

* Aktör arabirim yöntemleri aşırı yüklenemez.
* Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.
* Genel arabirimler desteklenmez.

## <a name="create-a-new-project-in-visual-studio"></a>Visual Studio'da yeni proje oluşturma
Visual Studio 2015 veya Visual Studio 2017 yönetici olarak başlatın ve yeni bir Service Fabric uygulaması projesi oluşturun:

![Visual Studio - yeni proje için Service Fabric araçları][1]

Merhaba sonraki iletişim kutusunda toocreate istediğiniz proje hello türünü seçebilirsiniz.

![Service Fabric proje şablonları][5]

Merhaba HelloWorld projesi için hello Service Fabric Reliable Actors hizmet kullanalım.

Merhaba çözüm oluşturduktan sonra yapı izlenerek hello görmeniz gerekir:

![Service Fabric Proje yapısı][2]

## <a name="reliable-actors-basic-building-blocks"></a>Güvenilir aktörler temel yapı taşları
Tipik bir Reliable Actors çözümü üç projeyi oluşur:

* **Merhaba uygulama projesi (MyActorApplication)**. Bu, tüm hello Hizmetleri birlikte dağıtım paketleri hello projesidir. Merhaba içerdiği *ApplicationManifest.xml* ve Merhaba uygulaması yönetmek için PowerShell komut dosyaları.
* **Merhaba arabirimi proje (MyActor.Interfaces)**. Bu arabirim tanımı hello aktör hello içeren hello projesidir. Merhaba MyActor.Interfaces projesinde hello aktör hello çözümde tarafından kullanılan hello arabirimleri tanımlayabilirsiniz. Merhaba arabirimi hello aktör uygulama ve genellikle algılama toodefine kolaylaştırır şekilde hello aktör çağırma hello istemcileri tarafından paylaşılan hello aktör sözleşmesini tanımlayan ancak aktör arabirimlerinizi herhangi bir ad ile herhangi bir projeye tanımlanabilir, derleme içinde Merhaba aktör uygulamasından ayırın ve birden çok diğer projeler tarafından paylaşılabilir.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **Merhaba aktör hizmeti projesi (MyActor)**. Bu, devam eden toohost hello aktör olan hello kullanılan proje toodefine hello Service Fabric hizmetidir. Merhaba aktör hello uygulamasını içerir. Aktör hello taban türünden türeyen bir sınıf uygulamasıdır `Actor` ve Implements hello hello MyActor.Interfaces projesinde tanımlanan arabirimi. Aktör sınıfı da kabul eden bir oluşturucu uygulamalıdır bir `ActorService` örneği ve bir `ActorId` ve bunları toohello temel geçirir `Actor` sınıfı. Bu oluşturucu bağımlılık ekleme platform bağımlılıklar için sağlar.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

Merhaba aktör hizmeti hello Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir. Merhaba, aktör örneklerinizi aktör hizmeti toorun sipariş, aktör türünüz hello aktör hizmeti ile da kayıtlı olması gerekir. Merhaba `ActorRuntime` kayıt yöntemi, bu iş aktörleri gerçekleştirir.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Visual Studio'da yeni bir proje başlangıç ve yalnızca bir aktör tanımı varsa hello kayıt Visual Studio'nun oluşturduğu hello kodda varsayılan olarak dahil edilir. Merhaba hizmetinde diğer aktörler tanımlarsanız kullanarak tooadd hello aktör kayıt gerekir:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Merhaba Service Fabric aktör çalışma zamanı bazı yayar [olaylar ve performans sayaçları ilgili tooactor yöntemler](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Bunlar, tanılama ve performans izlemesi kullanışlıdır.
> 
> 

## <a name="debugging"></a>Hata ayıklama
Visual Studio için Hello Service Fabric araçları yerel makinenizde hata ayıklama desteği. Hata ayıklama oturumu basarsa hello tarafından F5 tuşuna başlatabilirsiniz. Derlemeler (gerekirse) Visual Studio paketler. Ayrıca hello yerel Service Fabric kümesi hello uygulama dağıtır ve hello hata ayıklayıcı ekler.

Merhaba dağıtım işlemi sırasında hello hello ediyor görebilirsiniz **çıkış** penceresi.

![Service Fabric hata ayıklama çıktı penceresi][3]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [Reliable Actors hello Service Fabric platformundan kullanma](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
