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
# <a name="reliable-actors-state-management"></a><span data-ttu-id="bb0dd-103">Güvenilir aktörler durum yönetimi</span><span class="sxs-lookup"><span data-stu-id="bb0dd-103">Reliable Actors state management</span></span>
<span data-ttu-id="bb0dd-104">Güvenilir aktörler mantığı ve durumu sarmalayabilen tek iş parçacıklı nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="bb0dd-105">Aktör Reliable Services üzerinde çalıştığından, bunlar güvenilir bir şekilde kullanarak durumunu korumak hello Reliable Services kullandığı aynı Kalıcılık ve çoğaltma mekanizmaları.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="bb0dd-106">Bu şekilde çöp toplamadan sonra veya son tooresource Dengeleme veya yükseltmeler kümedeki düğümler arasında taşındıklarında yeniden etkinleştirme sırasında hatadan sonra durumlarına aktörler kaybetmeyin.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="bb0dd-107">Durum kalıcılığını ve çoğaltma</span><span class="sxs-lookup"><span data-stu-id="bb0dd-107">State persistence and replication</span></span>
<span data-ttu-id="bb0dd-108">Tüm Reliable Actors kabul *durum bilgisi olan* her aktör örneği tooa benzersiz kimliği eşlendiğinden</span><span class="sxs-lookup"><span data-stu-id="bb0dd-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="bb0dd-109">Bu aynı aktör kimliği, yinelenen çağrıları toohello yönlendirilen toohello anlamına gelir. aynı aktör örneği.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="bb0dd-110">Durum bilgisi olmayan bir sistemde Bunun aksine, istemci çağrılarını yönlendirilen toobe toohello garanti edilmez aynı sunucu her zaman.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="bb0dd-111">Bu nedenle, aktör Hizmetleri zaman durum bilgisi olan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="bb0dd-112">Aktörler stateful kabul edilen olsa bile, durum güvenilir bir şekilde depolamalısınız anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="bb0dd-113">Aktör durumunun kalıcı olmasını hello düzeyini seçebilirsiniz ve çoğaltma kendi veri depolama gereksinimleri dayalı:</span><span class="sxs-lookup"><span data-stu-id="bb0dd-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="bb0dd-114">**Durum kalıcı**: durumu kalıcı toodisk ve çoğaltılmış too3 ya da daha fazla yineleme.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="bb0dd-115">Bu hello en sağlam durumu depolama, durumu tam küme kesinti burada kalıcı seçenektir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="bb0dd-116">**Volatile durumu**: durumu çoğaltılmış too3 ya da daha fazla çoğaltmaları ve yalnızca bellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="bb0dd-117">Bu düğüm hatası ve aktör hatası karşı ve yükseltmeleri ve kaynak Dengeleme sırasında esnekliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="bb0dd-118">Ancak, durumu kalıcı toodisk değil.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="bb0dd-119">Tüm çoğaltmaları aynı anda kaybolursa, bu nedenle hello durumu da kaybolur.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="bb0dd-120">**Kalıcı durum yok**: durum çoğaltılan değil veya toodisk yazılmış.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="bb0dd-121">Yalnızca güvenilir bir şekilde toomaintain durumu ihtiyacınız aktörler için düzeydir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="bb0dd-122">Her Kalıcılık yalnızca farklı düzeyidir *durum sağlayıcısı* ve *çoğaltma* hizmetinizin yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="bb0dd-123">Durum yazılmış olup olmadığına bakılmaksızın toodisk hello durumu sağlayıcısı--durumu depolar güvenilir bir hizmet hello bileşeninde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="bb0dd-124">Çoğaltma hizmeti kaç çoğaltmaları dağıtıldığından bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="bb0dd-125">Güvenilir hizmetler gibi hem de durum sağlayıcısı hello ve çoğaltma sayısı kolayca el ile ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="bb0dd-126">Merhaba aktör framework üzerinde kullanıldığında bir aktör varsayılan durumu sağlayıcısı otomatik olarak seçer ve çoğaltma sayısı tooachieve bu üç Kalıcılık ayarlarından birini ayarlarını otomatik olarak oluşturur, bir öznitelik sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="bb0dd-127">Merhaba StatePersistence özniteliği türetilmiş sınıf tarafından devralınır değil, her aktör türü StatePersistence düzeyiyle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="bb0dd-128">Kalıcı durum</span><span class="sxs-lookup"><span data-stu-id="bb0dd-128">Persisted state</span></span>
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
<span data-ttu-id="bb0dd-129">Bu ayar veri diskte depolar ve hello hizmet yineleme sayısı too3 otomatik olarak ayarlayan bir durum sağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="bb0dd-130">Volatile durumu</span><span class="sxs-lookup"><span data-stu-id="bb0dd-130">Volatile state</span></span>
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
<span data-ttu-id="bb0dd-131">Yineleme sayısı too3 kümeleri hello ve bu ayar içindeki bellek-yalnızca durum sağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="bb0dd-132">Kalıcı durum yok</span><span class="sxs-lookup"><span data-stu-id="bb0dd-132">No persisted state</span></span>
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
<span data-ttu-id="bb0dd-133">Yineleme sayısı too1 kümeleri hello ve bu ayar içindeki bellek-yalnızca durum sağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="bb0dd-134">Varsayılanlar ve oluşturulan ayarları</span><span class="sxs-lookup"><span data-stu-id="bb0dd-134">Defaults and generated settings</span></span>
<span data-ttu-id="bb0dd-135">Merhaba kullanırken `StatePersistence` öznitelik, bir durum sağlayıcısı otomatik olarak seçilir, çalışma zamanında hello aktör hizmeti başladığında.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="bb0dd-136">Merhaba çoğaltma sayısı, ancak, derleme zamanında Visual Studio aktör hello tarafından derleme araçları ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="bb0dd-137">Merhaba derleme araçları otomatik olarak oluşturacak bir *varsayılan hizmet* ApplicationManifest.xml hello aktör hizmeti için.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="bb0dd-138">Parametreler için oluşturulan **en küçük çoğaltma kümesi boyutu** ve **hedef çoğaltma kümesi boyutu**.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="bb0dd-139">Bu parametreler el ile değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-139">You can change these parameters manually.</span></span> <span data-ttu-id="bb0dd-140">Ancak her zaman hello `StatePersistence` özniteliği değiştirildiğinde, hello parametrelerinin toohello varsayılan çoğaltma kümesi boyutu değerleri seçili hello ayarlandığı `StatePersistence` özniteliği, önceki tüm değerleri geçersiz kılma.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="bb0dd-141">Diğer bir deyişle, ServiceManifest.xml içinde ayarlanan hello değerlerdir *yalnızca* hello değiştirdiğinizde derleme zamanında geçersiz kılınmış `StatePersistence` öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="bb0dd-142">Durum Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="bb0dd-142">State manager</span></span>
<span data-ttu-id="bb0dd-143">Kendi durum Yöneticisi her aktör örneği vardır: depoladıktan bir sözlük benzeri veri yapısı anahtar/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="bb0dd-144">Merhaba durum Yöneticisi durum sağlayıcısı çevresinde bir sarmalayıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="bb0dd-145">Bu yöntemi hangi Kalıcılık ayarı kullanıldığına bakılmaksızın toostore verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="bb0dd-146">Durumu ayarı verileri korurken yükseltme üzerinden çalışan bir aktör hizmeti volatile (içindeki bellek-yalnızca) durumu ayarı tooa değiştirilebilir garanti kalıcı sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="bb0dd-147">Ancak, çalışan bir hizmetiniz için olası toochange yineleme sayısı olur.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="bb0dd-148">Durum Yöneticisi anahtarları dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-148">State manager keys must be strings.</span></span> <span data-ttu-id="bb0dd-149">Değerler genel ve herhangi bir türü olabilir özel türleri dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="bb0dd-150">Merhaba ağ tooother düğümleri üzerinde çoğaltma sırasında aktarılan ve bir aktör'ın durum Kalıcılık ayarını bağlı olarak toodisk yazılmış olabilir çünkü hello durum Yöneticisi'nde depolanan değerleri veri sözleşmesi seri hale getirilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="bb0dd-151">Merhaba durum Yöneticisi durum, güvenilir sözlükte bulunan benzer toothose yönetmek için ortak sözlüğü yöntemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="bb0dd-152">Erişim durumu</span><span class="sxs-lookup"><span data-stu-id="bb0dd-152">Accessing state</span></span>
<span data-ttu-id="bb0dd-153">Durum anahtarının hello durumu Yöneticisi üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="bb0dd-154">Durum Yöneticisi yöntemlerini tüm zaman uyumsuz olduklarından aktörler durumu kalıcı olduğunda disk g/ç gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="bb0dd-155">İlk erişim kaybedilmez durum nesneleri bellekte önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="bb0dd-156">Erişim işlemleri erişimi nesneleri doğrudan bellekten yineleyin ve disk g/ç veya zaman uyumsuz bağlam geçişi yükü yansıtılmasını olmadan zaman uyumlu olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="bb0dd-157">Bir durum nesnesi durumlarda aşağıdaki hello hello önbelleğinde kaldırılır:</span><span class="sxs-lookup"><span data-stu-id="bb0dd-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="bb0dd-158">Merhaba durum Yöneticisi'nden bir nesneyi alır sonra aktör yöntemi işlenmeyen bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="bb0dd-159">Bir aktör, devre dışı bırakılan sonra veya hatadan sonra yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="bb0dd-160">Merhaba durumu sağlayıcısı sayfalarını toodisk durumu.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="bb0dd-161">Bu davranış hello durumu sağlayıcısı uygulaması üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="bb0dd-162">Merhaba varsayılan durum sağlayıcısı hello için `Persisted` ayarının bu davranışı.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="bb0dd-163">Standart bir kullanarak durumu alabilirsiniz *almak* oluşturur işlemi `KeyNotFoundException`(C#) veya `NoSuchElementException`(bir girdi için hello anahtar mevcut değilse Java):</span><span class="sxs-lookup"><span data-stu-id="bb0dd-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

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

<span data-ttu-id="bb0dd-164">Kullanarak durumu alabilirsiniz bir *TryGet* bir girdi için bir anahtar mevcut değilse oluşturmadığını yöntemi:</span><span class="sxs-lookup"><span data-stu-id="bb0dd-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="bb0dd-165">Durum kaydetme</span><span class="sxs-lookup"><span data-stu-id="bb0dd-165">Saving state</span></span>
<span data-ttu-id="bb0dd-166">Merhaba durum Yöneticisi Alma yöntemlerini yerel belleğe başvuru tooan nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="bb0dd-167">Bu nesne yerel bellek tek başına değiştirme işlemi kaydedilmiş toobe kılmaz.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="bb0dd-168">Bir nesne hello durum Yöneticisi'nden alınır ve değişiklik olduğunda hello durumu Yöneticisi toobe işlemi kaydedilmiş yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="bb0dd-169">Bir koşulsuz kullanarak durumu ekleyebilirsiniz *ayarlamak*, hangi olduğu hello hello karşılığıdır `dictionary["key"] = value` sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="bb0dd-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="bb0dd-170">Kullanarak durumu ekleyebilirsiniz bir *Ekle* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="bb0dd-171">Bu yöntem oluşturulur `InvalidOperationException`(C#) veya `IllegalStateException`(tooadd zaten bir anahtar çalıştığında Java).</span><span class="sxs-lookup"><span data-stu-id="bb0dd-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="bb0dd-172">Kullanarak durumu ekleyebilirsiniz bir *TryAdd* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="bb0dd-173">Bu yöntem throw tooadd zaten bir anahtar çalıştığında değil.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="bb0dd-174">Aktör yöntemi Hello sonunda hello durum Yöneticisi eklenen veya bir ekleme veya güncelleştirme işlemi tarafından değiştiren herhangi bir değeri otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="bb0dd-175">"Kaydet" kalıcı toodisk ve kullanılan hello ayarlarına bağlı olarak çoğaltma içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="bb0dd-176">Değiştirilmemiş değerleri kalıcı veya çoğaltılan değil.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="bb0dd-177">Hiçbir değer değiştirilmişse, kaydetme işlemi hello hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="bb0dd-178">Başarısız kaydetme, hello değiştirilmiş durum atılır ve hello özgün durumuna geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="bb0dd-179">Ayrıca durumu el ile arama hello tarafından kaydedebilirsiniz `SaveStateAsync` hello aktör temel yöntemi:</span><span class="sxs-lookup"><span data-stu-id="bb0dd-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="bb0dd-180">Durum kaldırma</span><span class="sxs-lookup"><span data-stu-id="bb0dd-180">Removing state</span></span>
<span data-ttu-id="bb0dd-181">Durum kalıcı olarak bir aktör'ın durum Yöneticisi'nden tarafından arama hello kaldırabilirsiniz *kaldırmak* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="bb0dd-182">Bu yöntem oluşturulur `KeyNotFoundException`(C#) veya `NoSuchElementException`(tooremove mevcut olmayan bir anahtar çalıştığında Java).</span><span class="sxs-lookup"><span data-stu-id="bb0dd-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

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

<span data-ttu-id="bb0dd-183">Ayrıca durumu kalıcı olarak hello kullanarak kaldırabilirsiniz *TryRemove* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="bb0dd-184">Bu yöntem throw tooremove var olmayan bir anahtar çalıştığında değil.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bb0dd-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bb0dd-185">Next steps</span></span>

<span data-ttu-id="bb0dd-186">Reliable Actors içinde depolanan durumu, yazılı toodisk önce seri hale getirilmiş ve yüksek kullanılabilirlik için çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="bb0dd-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="bb0dd-187">Daha fazla bilgi edinmek [aktör türü seri hale getirme](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="bb0dd-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="bb0dd-188">Ardından, daha fazla bilgi edinmek [aktör tanılama ve performans izlemesi](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="bb0dd-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
