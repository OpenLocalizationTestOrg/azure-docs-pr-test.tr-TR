---
title: aaaReliable Azure Service Fabric, koleksiyon nesnesi seri hale getirme | Microsoft Docs
description: "Azure Service Fabric güvenilir koleksiyonları nesne seri hale getirme"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="74258-103">Azure Service Fabric güvenilir koleksiyon nesnesi serileştirmede</span><span class="sxs-lookup"><span data-stu-id="74258-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="74258-104">Güvenilir koleksiyonları çoğaltmak ve makine hataları ve güç kesintileri arasında dayanıklı olduklarından emin kendi öğeleri toomake kalır.</span><span class="sxs-lookup"><span data-stu-id="74258-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="74258-105">Tooreplicate ve toopersist öğeleri, güvenilir koleksiyonları gerek tooserialize bunları.</span><span class="sxs-lookup"><span data-stu-id="74258-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="74258-106">Güvenilir koleksiyonları hello uygun seri hale getirici için belirli bir türde güvenilir durum Yöneticisi'nden alın.</span><span class="sxs-lookup"><span data-stu-id="74258-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="74258-107">Güvenilir durum Yöneticisi yerleşik serileştiricileri içerir ve belirli bir türde için özel serileştiricileri toobe kayıtlı sağlar.</span><span class="sxs-lookup"><span data-stu-id="74258-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="74258-108">Yerleşik serileştiricileri</span><span class="sxs-lookup"><span data-stu-id="74258-108">Built-in Serializers</span></span>

<span data-ttu-id="74258-109">Varsayılan olarak verimli bir şekilde serileştirilebilir böylece güvenilir durum Yöneticisi bazı ortak türleri için yerleşik seri hale getirici içerir.</span><span class="sxs-lookup"><span data-stu-id="74258-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="74258-110">Diğer türleri için güvenilir durum Yöneticisi toouse hello geri döner [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="74258-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="74258-111">Yerleşik serileştiricileri türlerini değiştiremezsiniz ve türü adı gibi hello türü hakkında bilgi tooinclude gerekmez bildikleri olduğundan daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="74258-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="74258-112">Güvenilir durum Yöneticisi aşağıdaki türleri için yerleşik seri hale getirici sahiptir:</span><span class="sxs-lookup"><span data-stu-id="74258-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="74258-113">GUID</span><span class="sxs-lookup"><span data-stu-id="74258-113">Guid</span></span>
- <span data-ttu-id="74258-114">bool</span><span class="sxs-lookup"><span data-stu-id="74258-114">bool</span></span>
- <span data-ttu-id="74258-115">Bayt</span><span class="sxs-lookup"><span data-stu-id="74258-115">byte</span></span>
- <span data-ttu-id="74258-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="74258-116">sbyte</span></span>
- <span data-ttu-id="74258-117">Byte]</span><span class="sxs-lookup"><span data-stu-id="74258-117">byte[]</span></span>
- <span data-ttu-id="74258-118">char</span><span class="sxs-lookup"><span data-stu-id="74258-118">char</span></span>
- <span data-ttu-id="74258-119">Dize</span><span class="sxs-lookup"><span data-stu-id="74258-119">string</span></span>
- <span data-ttu-id="74258-120">Ondalık</span><span class="sxs-lookup"><span data-stu-id="74258-120">decimal</span></span>
- <span data-ttu-id="74258-121">Çift</span><span class="sxs-lookup"><span data-stu-id="74258-121">double</span></span>
- <span data-ttu-id="74258-122">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="74258-122">float</span></span>
- <span data-ttu-id="74258-123">Int</span><span class="sxs-lookup"><span data-stu-id="74258-123">int</span></span>
- <span data-ttu-id="74258-124">uint</span><span class="sxs-lookup"><span data-stu-id="74258-124">uint</span></span>
- <span data-ttu-id="74258-125">uzun</span><span class="sxs-lookup"><span data-stu-id="74258-125">long</span></span>
- <span data-ttu-id="74258-126">ulong</span><span class="sxs-lookup"><span data-stu-id="74258-126">ulong</span></span>
- <span data-ttu-id="74258-127">kısa</span><span class="sxs-lookup"><span data-stu-id="74258-127">short</span></span>
- <span data-ttu-id="74258-128">ushort</span><span class="sxs-lookup"><span data-stu-id="74258-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="74258-129">Özel seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="74258-129">Custom Serialization</span></span>

<span data-ttu-id="74258-130">Özel serileştiricileri yaygın olarak kullanılan tooincrease performans veya tooencrypt hello hello kablo üzerinden ve diskteki verilerdir.</span><span class="sxs-lookup"><span data-stu-id="74258-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="74258-131">Merhaba türü hakkında bilgi tooserialize gerekmeyen beri diğer nedenlerin yanı sıra özel serileştiricileri genel seri hale getirici yaygın olarak daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="74258-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="74258-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) kullanılan tooregister verilen türdeki T. hello özel seri hale getirici olduğu Bu kayıt hello StatefulServiceBase tooensure hello yapısında kurtarma başlamadan önce tüm güvenilir koleksiyonları sahip olacağını toohello ilgili seri hale getirici tooread kalıcı verilerine erişim.</span><span class="sxs-lookup"><span data-stu-id="74258-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="74258-133">Özel serileştiricileri yerleşik serileştiricileri öncelik verilir.</span><span class="sxs-lookup"><span data-stu-id="74258-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="74258-134">İnt özel seri hale getirici kaydedildiğinde, örneğin, int için yerleşik serileştirici hello yerine kullanılan tooserialize tamsayılar olmasından</span><span class="sxs-lookup"><span data-stu-id="74258-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="74258-135">Nasıl tooimplement özel bir seri hale getirici</span><span class="sxs-lookup"><span data-stu-id="74258-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="74258-136">Özel bir seri hale getirici tooimplement hello gereken [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) arabirimi.</span><span class="sxs-lookup"><span data-stu-id="74258-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="74258-137">IStateSerializer<T> aşırı yazma ve alan okuma için taban değeri olarak adlandırılan bir ek T içerir.</span><span class="sxs-lookup"><span data-stu-id="74258-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="74258-138">Değişiklikleri seri hale getirme için API'dir.</span><span class="sxs-lookup"><span data-stu-id="74258-138">This API is for differential serialization.</span></span> <span data-ttu-id="74258-139">Şu anda değişiklikleri seri hale getirme özellik gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="74258-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="74258-140">Değişiklikleri seri hale getirme gösterilir ve etkin kadar bu nedenle, bu iki aşırı denir değil.</span><span class="sxs-lookup"><span data-stu-id="74258-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="74258-141">Aşağıdaki dört özellikler içeren OrderKey adlı bir örnek özel türüdür</span><span class="sxs-lookup"><span data-stu-id="74258-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="74258-142">Aşağıdadır IStateSerializer örnek uygulaması<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="74258-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="74258-143">Okuma ve yazma içinde baseValue alın, ileten uyumluluk için kendi ilgili aşırı yüklemesini çağırın aşırı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="74258-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="74258-144">Upgradability</span><span class="sxs-lookup"><span data-stu-id="74258-144">Upgradability</span></span>
<span data-ttu-id="74258-145">İçinde bir [uygulama yükseltmesinde](service-fabric-application-upgrade.md), hello yükseltmedir uygulanan tooa alt düğümler, aynı anda bir yükseltme etki alanı.</span><span class="sxs-lookup"><span data-stu-id="74258-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="74258-146">Bu işlem sırasında bazı yükseltme etki alanlarının hello daha yeni sürümü, uygulamanızın üzerinde olacaktır ve bazı yükseltme etki alanlarının hello eski uygulamanızı sürümünde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="74258-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="74258-147">Merhaba piyasaya çıkma sırasında hello yeni sürümü, uygulamanızın mümkün tooread hello eski sürümü verilerinizi olmalıdır ve hello eski sürümü, uygulamanızın verilerinizin mümkün tooread hello yeni sürüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="74258-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="74258-148">Merhaba veri biçimi ileriye ve geriye dönük uyumlu hello yükseltme değilse başarısız ya da kötüsü, veri kayıp bozuk veya.</span><span class="sxs-lookup"><span data-stu-id="74258-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="74258-149">Yerleşik seri hale getirici kullanıyorsanız, uyumluluğu hakkında tooworry yok.</span><span class="sxs-lookup"><span data-stu-id="74258-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="74258-150">Ancak, özel seri hale getirici veya hello DataContractSerializer kullanıyorsanız, hello veri toobe sonsuz geriye doğru olması ve uyumlu iletir.</span><span class="sxs-lookup"><span data-stu-id="74258-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="74258-151">Diğer bir deyişle, seri hale getirici her sürümü toobe mümkün tooserialize gerekir ve seri durumdan hello türü herhangi bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="74258-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="74258-152">Veri sözleşmesi kullanıcılar ekleme, kaldırma ve alanları değiştirme hello iyi tanımlanmış sürüm kuralları başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="74258-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="74258-153">Veri sözleşmesi bilinmeyen alanlarla ilgilenme hello seri hale getirme ve seri durumdan çıkarma işlemi takma ve sınıf devralma ile ilgilenen için destek de vardır.</span><span class="sxs-lookup"><span data-stu-id="74258-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="74258-154">Daha fazla bilgi için bkz: [kullanarak veri sözleşmesi](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="74258-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="74258-155">Özel seri hale getirici kullanıcılar toomake geriye doğru olduğundan ve uyumluluğa emin kullandıkları hello seri hale getirici toohello yönergelerini uymanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="74258-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="74258-156">Tüm sürümler destekleyen en yaygın yolu hello yalnızca isteğe bağlı özellikler ekleme başında ve boyutu bilgi eklemektir.</span><span class="sxs-lookup"><span data-stu-id="74258-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="74258-157">Bu şekilde, olabildiğince fazla kullanabilirsiniz ve hello kalan kısmını hello akış atlama her sürümü okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="74258-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74258-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="74258-158">Next steps</span></span>
  * [<span data-ttu-id="74258-159">Seri hale getirme ve yükseltme</span><span class="sxs-lookup"><span data-stu-id="74258-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="74258-160">Güvenilir koleksiyonlar için Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="74258-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="74258-161">[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="74258-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="74258-162">[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="74258-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="74258-163">Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="74258-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="74258-164">Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="74258-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="74258-165">Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="74258-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
