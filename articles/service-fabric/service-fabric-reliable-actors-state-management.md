---
title: "aaaReliable aktörler durum yönetimi | Microsoft Docs"
description: "Nasıl Reliable Actors durumu yönetilen kalıcı ve yüksek kullanılabilirlik için çoğaltılan açıklar."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a>Güvenilir aktörler durum yönetimi
Güvenilir aktörler mantığı ve durumu sarmalayabilen tek iş parçacıklı nesneleridir. Aktör Reliable Services üzerinde çalıştığından, bunlar güvenilir bir şekilde kullanarak durumunu korumak hello Reliable Services kullandığı aynı Kalıcılık ve çoğaltma mekanizmaları. Bu şekilde çöp toplamadan sonra veya son tooresource Dengeleme veya yükseltmeler kümedeki düğümler arasında taşındıklarında yeniden etkinleştirme sırasında hatadan sonra durumlarına aktörler kaybetmeyin.

## <a name="state-persistence-and-replication"></a>Durum kalıcılığını ve çoğaltma
Tüm Reliable Actors kabul *durum bilgisi olan* her aktör örneği tooa benzersiz kimliği eşlendiğinden Bu aynı aktör kimliği, yinelenen çağrıları toohello yönlendirilen toohello anlamına gelir. aynı aktör örneği. Durum bilgisi olmayan bir sistemde Bunun aksine, istemci çağrılarını yönlendirilen toobe toohello garanti edilmez aynı sunucu her zaman. Bu nedenle, aktör Hizmetleri zaman durum bilgisi olan hizmetleridir.

Aktörler stateful kabul edilen olsa bile, durum güvenilir bir şekilde depolamalısınız anlamına gelmez. Aktör durumunun kalıcı olmasını hello düzeyini seçebilirsiniz ve çoğaltma kendi veri depolama gereksinimleri dayalı:

* **Durum kalıcı**: durumu kalıcı toodisk ve çoğaltılmış too3 ya da daha fazla yineleme. Bu hello en sağlam durumu depolama, durumu tam küme kesinti burada kalıcı seçenektir.
* **Volatile durumu**: durumu çoğaltılmış too3 ya da daha fazla çoğaltmaları ve yalnızca bellekte depolanır. Bu düğüm hatası ve aktör hatası karşı ve yükseltmeleri ve kaynak Dengeleme sırasında esnekliği sağlar. Ancak, durumu kalıcı toodisk değil. Tüm çoğaltmaları aynı anda kaybolursa, bu nedenle hello durumu da kaybolur.
* **Kalıcı durum yok**: durum çoğaltılan değil veya toodisk yazılmış. Yalnızca güvenilir bir şekilde toomaintain durumu ihtiyacınız aktörler için düzeydir.

Her Kalıcılık yalnızca farklı düzeyidir *durum sağlayıcısı* ve *çoğaltma* hizmetinizin yapılandırma. Durum yazılmış olup olmadığına bakılmaksızın toodisk hello durumu sağlayıcısı--durumu depolar güvenilir bir hizmet hello bileşeninde bağlıdır. Çoğaltma hizmeti kaç çoğaltmaları dağıtıldığından bağlıdır. Güvenilir hizmetler gibi hem de durum sağlayıcısı hello ve çoğaltma sayısı kolayca el ile ayarlanabilir. Merhaba aktör framework üzerinde kullanıldığında bir aktör varsayılan durumu sağlayıcısı otomatik olarak seçer ve çoğaltma sayısı tooachieve bu üç Kalıcılık ayarlarından birini ayarlarını otomatik olarak oluşturur, bir öznitelik sağlar. Merhaba StatePersistence özniteliği türetilmiş sınıf tarafından devralınır değil, her aktör türü StatePersistence düzeyiyle sağlamanız gerekir.

### <a name="persisted-state"></a>Kalıcı durum
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
Bu ayar veri diskte depolar ve hello hizmet yineleme sayısı too3 otomatik olarak ayarlayan bir durum sağlayıcısı kullanır.

### <a name="volatile-state"></a>Volatile durumu
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
Yineleme sayısı too3 kümeleri hello ve bu ayar içindeki bellek-yalnızca durum sağlayıcısı kullanır.

### <a name="no-persisted-state"></a>Kalıcı durum yok
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
Yineleme sayısı too1 kümeleri hello ve bu ayar içindeki bellek-yalnızca durum sağlayıcısı kullanır.

### <a name="defaults-and-generated-settings"></a>Varsayılanlar ve oluşturulan ayarları
Merhaba kullanırken `StatePersistence` öznitelik, bir durum sağlayıcısı otomatik olarak seçilir, çalışma zamanında hello aktör hizmeti başladığında. Merhaba çoğaltma sayısı, ancak, derleme zamanında Visual Studio aktör hello tarafından derleme araçları ayarlanır. Merhaba derleme araçları otomatik olarak oluşturacak bir *varsayılan hizmet* ApplicationManifest.xml hello aktör hizmeti için. Parametreler için oluşturulan **en küçük çoğaltma kümesi boyutu** ve **hedef çoğaltma kümesi boyutu**.

Bu parametreler el ile değiştirebilirsiniz. Ancak her zaman hello `StatePersistence` özniteliği değiştirildiğinde, hello parametrelerinin toohello varsayılan çoğaltma kümesi boyutu değerleri seçili hello ayarlandığı `StatePersistence` özniteliği, önceki tüm değerleri geçersiz kılma. Diğer bir deyişle, ServiceManifest.xml içinde ayarlanan hello değerlerdir *yalnızca* hello değiştirdiğinizde derleme zamanında geçersiz kılınmış `StatePersistence` öznitelik değeri.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a>Durum Yöneticisi
Kendi durum Yöneticisi her aktör örneği vardır: depoladıktan bir sözlük benzeri veri yapısı anahtar/değer çiftleri. Merhaba durum Yöneticisi durum sağlayıcısı çevresinde bir sarmalayıcı ' dir. Bu yöntemi hangi Kalıcılık ayarı kullanıldığına bakılmaksızın toostore verileri kullanabilirsiniz. Durumu ayarı verileri korurken yükseltme üzerinden çalışan bir aktör hizmeti volatile (içindeki bellek-yalnızca) durumu ayarı tooa değiştirilebilir garanti kalıcı sağlamaz. Ancak, çalışan bir hizmetiniz için olası toochange yineleme sayısı olur.

Durum Yöneticisi anahtarları dize olmalıdır. Değerler genel ve herhangi bir türü olabilir özel türleri dahil olmak üzere. Merhaba ağ tooother düğümleri üzerinde çoğaltma sırasında aktarılan ve bir aktör'ın durum Kalıcılık ayarını bağlı olarak toodisk yazılmış olabilir çünkü hello durum Yöneticisi'nde depolanan değerleri veri sözleşmesi seri hale getirilebilir olmalıdır.

Merhaba durum Yöneticisi durum, güvenilir sözlükte bulunan benzer toothose yönetmek için ortak sözlüğü yöntemlerini gösterir.

### <a name="accessing-state"></a>Erişim durumu
Durum anahtarının hello durumu Yöneticisi üzerinden erişilebilir. Durum Yöneticisi yöntemlerini tüm zaman uyumsuz olduklarından aktörler durumu kalıcı olduğunda disk g/ç gerektirebilir. İlk erişim kaybedilmez durum nesneleri bellekte önbelleğe alınır. Erişim işlemleri erişimi nesneleri doğrudan bellekten yineleyin ve disk g/ç veya zaman uyumsuz bağlam geçişi yükü yansıtılmasını olmadan zaman uyumlu olarak döndürür. Bir durum nesnesi durumlarda aşağıdaki hello hello önbelleğinde kaldırılır:

* Merhaba durum Yöneticisi'nden bir nesneyi alır sonra aktör yöntemi işlenmeyen bir özel durum oluşturur.
* Bir aktör, devre dışı bırakılan sonra veya hatadan sonra yeniden başlatılır.
* Merhaba durumu sağlayıcısı sayfalarını toodisk durumu. Bu davranış hello durumu sağlayıcısı uygulaması üzerinde bağlıdır. Merhaba varsayılan durum sağlayıcısı hello için `Persisted` ayarının bu davranışı.

Standart bir kullanarak durumu alabilirsiniz *almak* oluşturur işlemi `KeyNotFoundException`(C#) veya `NoSuchElementException`(bir girdi için hello anahtar mevcut değilse Java):

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

Kullanarak durumu alabilirsiniz bir *TryGet* bir girdi için bir anahtar mevcut değilse oluşturmadığını yöntemi:

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a>Durum kaydetme
Merhaba durum Yöneticisi Alma yöntemlerini yerel belleğe başvuru tooan nesnesi döndürür. Bu nesne yerel bellek tek başına değiştirme işlemi kaydedilmiş toobe kılmaz. Bir nesne hello durum Yöneticisi'nden alınır ve değişiklik olduğunda hello durumu Yöneticisi toobe işlemi kaydedilmiş yeniden gerekir.

Bir koşulsuz kullanarak durumu ekleyebilirsiniz *ayarlamak*, hangi olduğu hello hello karşılığıdır `dictionary["key"] = value` sözdizimi:

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

Kullanarak durumu ekleyebilirsiniz bir *Ekle* yöntemi. Bu yöntem oluşturulur `InvalidOperationException`(C#) veya `IllegalStateException`(tooadd zaten bir anahtar çalıştığında Java).

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

Kullanarak durumu ekleyebilirsiniz bir *TryAdd* yöntemi. Bu yöntem throw tooadd zaten bir anahtar çalıştığında değil.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

Aktör yöntemi Hello sonunda hello durum Yöneticisi eklenen veya bir ekleme veya güncelleştirme işlemi tarafından değiştiren herhangi bir değeri otomatik olarak kaydeder. "Kaydet" kalıcı toodisk ve kullanılan hello ayarlarına bağlı olarak çoğaltma içerebilir. Değiştirilmemiş değerleri kalıcı veya çoğaltılan değil. Hiçbir değer değiştirilmişse, kaydetme işlemi hello hiçbir şey yapmaz. Başarısız kaydetme, hello değiştirilmiş durum atılır ve hello özgün durumuna geri yüklenir.

Ayrıca durumu el ile arama hello tarafından kaydedebilirsiniz `SaveStateAsync` hello aktör temel yöntemi:

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a>Durum kaldırma
Durum kalıcı olarak bir aktör'ın durum Yöneticisi'nden tarafından arama hello kaldırabilirsiniz *kaldırmak* yöntemi. Bu yöntem oluşturulur `KeyNotFoundException`(C#) veya `NoSuchElementException`(tooremove mevcut olmayan bir anahtar çalıştığında Java).

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

Ayrıca durumu kalıcı olarak hello kullanarak kaldırabilirsiniz *TryRemove* yöntemi. Bu yöntem throw tooremove var olmayan bir anahtar çalıştığında değil.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar

Reliable Actors içinde depolanan durumu, yazılı toodisk önce seri hale getirilmiş ve yüksek kullanılabilirlik için çoğaltılır. Daha fazla bilgi edinmek [aktör türü seri hale getirme](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Ardından, daha fazla bilgi edinmek [aktör tanılama ve performans izlemesi](service-fabric-reliable-actors-diagnostics.md).
