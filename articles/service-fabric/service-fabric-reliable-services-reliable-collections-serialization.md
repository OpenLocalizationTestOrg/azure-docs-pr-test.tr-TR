---
title: "Azure Service Fabric güvenilir koleksiyon nesnesi serileştirmede | Microsoft Docs"
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
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="19d2f-103">Azure Service Fabric güvenilir koleksiyon nesnesi serileştirmede</span><span class="sxs-lookup"><span data-stu-id="19d2f-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="19d2f-104">Güvenilir koleksiyonları çoğaltmak ve makine hataları ve güç kesintileri arasında dayanıklı olduklarından emin olmak için kendi öğeleri kalır.</span><span class="sxs-lookup"><span data-stu-id="19d2f-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="19d2f-105">Çoğaltmak için hem öğeleri kalıcı hale getirmek için bunları seri hale getirmek güvenilir koleksiyonları gerekir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="19d2f-106">Güvenilir koleksiyonları uygun seri hale getirici için belirli bir türde güvenilir durum Yöneticisi'nden alın.</span><span class="sxs-lookup"><span data-stu-id="19d2f-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="19d2f-107">Güvenilir durum Yöneticisi yerleşik serileştiricileri içerir ve verilen bir tür için kayıtlı olması özel serileştiricileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="19d2f-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="19d2f-108">Yerleşik serileştiricileri</span><span class="sxs-lookup"><span data-stu-id="19d2f-108">Built-in Serializers</span></span>

<span data-ttu-id="19d2f-109">Varsayılan olarak verimli bir şekilde serileştirilebilir böylece güvenilir durum Yöneticisi bazı ortak türleri için yerleşik seri hale getirici içerir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="19d2f-110">Diğer türleri için güvenilir durum Yöneticisi geri kullanılacak döner [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="19d2f-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="19d2f-111">Yerleşik serileştiricileri türlerini değiştiremezsiniz ve türü adı gibi türü hakkındaki bilgileri içerecek şekilde gerekmez bildikleri olduğundan daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="19d2f-112">Güvenilir durum Yöneticisi aşağıdaki türleri için yerleşik seri hale getirici sahiptir:</span><span class="sxs-lookup"><span data-stu-id="19d2f-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="19d2f-113">GUID</span><span class="sxs-lookup"><span data-stu-id="19d2f-113">Guid</span></span>
- <span data-ttu-id="19d2f-114">bool</span><span class="sxs-lookup"><span data-stu-id="19d2f-114">bool</span></span>
- <span data-ttu-id="19d2f-115">Bayt</span><span class="sxs-lookup"><span data-stu-id="19d2f-115">byte</span></span>
- <span data-ttu-id="19d2f-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="19d2f-116">sbyte</span></span>
- <span data-ttu-id="19d2f-117">Byte]</span><span class="sxs-lookup"><span data-stu-id="19d2f-117">byte[]</span></span>
- <span data-ttu-id="19d2f-118">char</span><span class="sxs-lookup"><span data-stu-id="19d2f-118">char</span></span>
- <span data-ttu-id="19d2f-119">Dize</span><span class="sxs-lookup"><span data-stu-id="19d2f-119">string</span></span>
- <span data-ttu-id="19d2f-120">Ondalık</span><span class="sxs-lookup"><span data-stu-id="19d2f-120">decimal</span></span>
- <span data-ttu-id="19d2f-121">Çift</span><span class="sxs-lookup"><span data-stu-id="19d2f-121">double</span></span>
- <span data-ttu-id="19d2f-122">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="19d2f-122">float</span></span>
- <span data-ttu-id="19d2f-123">Int</span><span class="sxs-lookup"><span data-stu-id="19d2f-123">int</span></span>
- <span data-ttu-id="19d2f-124">uint</span><span class="sxs-lookup"><span data-stu-id="19d2f-124">uint</span></span>
- <span data-ttu-id="19d2f-125">uzun</span><span class="sxs-lookup"><span data-stu-id="19d2f-125">long</span></span>
- <span data-ttu-id="19d2f-126">ulong</span><span class="sxs-lookup"><span data-stu-id="19d2f-126">ulong</span></span>
- <span data-ttu-id="19d2f-127">kısa</span><span class="sxs-lookup"><span data-stu-id="19d2f-127">short</span></span>
- <span data-ttu-id="19d2f-128">ushort</span><span class="sxs-lookup"><span data-stu-id="19d2f-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="19d2f-129">Özel seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="19d2f-129">Custom Serialization</span></span>

<span data-ttu-id="19d2f-130">Özel serileştiricileri, performansı artırmak için veya kablo üzerinden ve diskteki verileri şifrelemek için yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19d2f-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="19d2f-131">Türü hakkında bilgi serileştirmek gerekmeyen beri diğer nedenlerin yanı sıra özel serileştiricileri genel seri hale getirici yaygın olarak daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="19d2f-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) T. belirtilen tür için özel bir seri hale getirici kaydetmek için kullanılır Bu kayıt kurtarma başlamadan önce tüm güvenilir koleksiyonları kalıcı verilerini okumak için ilgili seri hale getirici erişiminiz olduğundan emin olmak için StatefulServiceBase yapımı gerçekleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="19d2f-133">Özel serileştiricileri yerleşik serileştiricileri öncelik verilir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="19d2f-134">İnt özel seri hale getirici kaydedildiğinde, örneğin, bunu int için yerleşik serileştirici yerine tamsayılar serileştirmek için kullanılır</span><span class="sxs-lookup"><span data-stu-id="19d2f-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="19d2f-135">Özel bir seri hale getirici gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="19d2f-135">How to implement a custom serializer</span></span>

<span data-ttu-id="19d2f-136">Özel bir seri hale getirici uygulamak gereken [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) arabirimi.</span><span class="sxs-lookup"><span data-stu-id="19d2f-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="19d2f-137">IStateSerializer<T> aşırı yazma ve alan okuma için taban değeri olarak adlandırılan bir ek T içerir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="19d2f-138">Değişiklikleri seri hale getirme için API'dir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-138">This API is for differential serialization.</span></span> <span data-ttu-id="19d2f-139">Şu anda değişiklikleri seri hale getirme özellik gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="19d2f-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="19d2f-140">Değişiklikleri seri hale getirme gösterilir ve etkin kadar bu nedenle, bu iki aşırı denir değil.</span><span class="sxs-lookup"><span data-stu-id="19d2f-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="19d2f-141">Aşağıdaki dört özellikler içeren OrderKey adlı bir örnek özel türüdür</span><span class="sxs-lookup"><span data-stu-id="19d2f-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="19d2f-142">Aşağıdadır IStateSerializer örnek uygulaması<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="19d2f-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="19d2f-143">Okuma ve yazma içinde baseValue alın, ileten uyumluluk için kendi ilgili aşırı yüklemesini çağırın aşırı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="19d2f-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="19d2f-144">Upgradability</span><span class="sxs-lookup"><span data-stu-id="19d2f-144">Upgradability</span></span>
<span data-ttu-id="19d2f-145">İçinde bir [uygulama yükseltmesinde](service-fabric-application-upgrade.md), alt düğümler, aynı anda bir yükseltme etki alanı yükseltme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="19d2f-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="19d2f-146">Bu işlem sırasında bazı yükseltme etki alanları, uygulamanızın sürümü olacaktır ve bazı yükseltme etki alanları, uygulamanızın eski sürümünde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="19d2f-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="19d2f-147">Piyasaya çıkma sırasında uygulamanın yeni sürümü verilerinizin eski sürümü okuyabilir ve uygulamanızın eski sürümünü verilerinizin yeni sürümü okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="19d2f-148">Veri biçimi ileriye ve geriye dönük olarak uyumlu değilse, yükseltme başarısız olabilir ya da kötüsü, veriler kaybolmuş veya bozulmuş.</span><span class="sxs-lookup"><span data-stu-id="19d2f-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="19d2f-149">Yerleşik seri hale getirici kullanıyorsanız, uyumluluğu hakkında endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="19d2f-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="19d2f-150">Özel bir seri hale getirici veya DataContractSerializer kullanıyorsanız, ancak verileri sonsuz İleri ve geri girmek uyumlu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="19d2f-151">Diğer bir deyişle, her sürümü seri hale getirici, serileştirme ve seri durumdan türü herhangi bir sürümü gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="19d2f-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="19d2f-152">Veri sözleşmesi kullanıcılar ekleme, kaldırma ve alanları değiştirme için iyi tanımlanmış sürüm kuralları başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19d2f-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="19d2f-153">Veri sözleşmesi bilinmeyen alanlarla ilgilenme, seri hale getirme ve seri durumdan çıkarma işlemine takma ve sınıf devralma ile ilgilenen için destek de vardır.</span><span class="sxs-lookup"><span data-stu-id="19d2f-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="19d2f-154">Daha fazla bilgi için bkz: [kullanarak veri sözleşmesi](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="19d2f-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="19d2f-155">Özel seri hale getirici kullanıcılar geriye doğru olduğundan ve iletir uyumlu hale getirmek için kullandıkları seri hale getirici yönergeleriyle uyumlu.</span><span class="sxs-lookup"><span data-stu-id="19d2f-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="19d2f-156">Tüm sürümler destekleyen en yaygın yolu başında boyutu bilgileri eklemek ve yalnızca isteğe bağlı özellikler ekleme.</span><span class="sxs-lookup"><span data-stu-id="19d2f-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="19d2f-157">Çok olabilir ve akış kalan kısmını atlama olarak bu şekilde her sürümü okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19d2f-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19d2f-158">Next steps</span></span>
  * [<span data-ttu-id="19d2f-159">Seri hale getirme ve yükseltme</span><span class="sxs-lookup"><span data-stu-id="19d2f-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="19d2f-160">Güvenilir koleksiyonlar için Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="19d2f-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="19d2f-161">[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="19d2f-162">[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="19d2f-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="19d2f-163">Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="19d2f-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="19d2f-164">Gelişmiş işlevselliği başvurarak uygulamanızı yükseltirken kullanmayı öğrenin [Gelişmiş konular](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="19d2f-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="19d2f-165">Adımlarına bakarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="19d2f-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
