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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Azure Service Fabric güvenilir koleksiyon nesnesi serileştirmede
Güvenilir koleksiyonları çoğaltmak ve makine hataları ve güç kesintileri arasında dayanıklı olduklarından emin kendi öğeleri toomake kalır.
Tooreplicate ve toopersist öğeleri, güvenilir koleksiyonları gerek tooserialize bunları.

Güvenilir koleksiyonları hello uygun seri hale getirici için belirli bir türde güvenilir durum Yöneticisi'nden alın.
Güvenilir durum Yöneticisi yerleşik serileştiricileri içerir ve belirli bir türde için özel serileştiricileri toobe kayıtlı sağlar.

## <a name="built-in-serializers"></a>Yerleşik serileştiricileri

Varsayılan olarak verimli bir şekilde serileştirilebilir böylece güvenilir durum Yöneticisi bazı ortak türleri için yerleşik seri hale getirici içerir. Diğer türleri için güvenilir durum Yöneticisi toouse hello geri döner [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Yerleşik serileştiricileri türlerini değiştiremezsiniz ve türü adı gibi hello türü hakkında bilgi tooinclude gerekmez bildikleri olduğundan daha verimlidir.

Güvenilir durum Yöneticisi aşağıdaki türleri için yerleşik seri hale getirici sahiptir: 
- GUID
- bool
- Bayt
- sbyte
- Byte]
- char
- Dize
- Ondalık
- Çift
- Kayan nokta
- Int
- uint
- uzun
- ulong
- kısa
- ushort

## <a name="custom-serialization"></a>Özel seri hale getirme

Özel serileştiricileri yaygın olarak kullanılan tooincrease performans veya tooencrypt hello hello kablo üzerinden ve diskteki verilerdir. Merhaba türü hakkında bilgi tooserialize gerekmeyen beri diğer nedenlerin yanı sıra özel serileştiricileri genel seri hale getirici yaygın olarak daha verimlidir. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) kullanılan tooregister verilen türdeki T. hello özel seri hale getirici olduğu Bu kayıt hello StatefulServiceBase tooensure hello yapısında kurtarma başlamadan önce tüm güvenilir koleksiyonları sahip olacağını toohello ilgili seri hale getirici tooread kalıcı verilerine erişim.

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
> Özel serileştiricileri yerleşik serileştiricileri öncelik verilir. İnt özel seri hale getirici kaydedildiğinde, örneğin, int için yerleşik serileştirici hello yerine kullanılan tooserialize tamsayılar olmasından

### <a name="how-tooimplement-a-custom-serializer"></a>Nasıl tooimplement özel bir seri hale getirici

Özel bir seri hale getirici tooimplement hello gereken [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) arabirimi.

> [!NOTE]
> IStateSerializer<T> aşırı yazma ve alan okuma için taban değeri olarak adlandırılan bir ek T içerir. Değişiklikleri seri hale getirme için API'dir. Şu anda değişiklikleri seri hale getirme özellik gösterilmez. Değişiklikleri seri hale getirme gösterilir ve etkin kadar bu nedenle, bu iki aşırı denir değil.

Aşağıdaki dört özellikler içeren OrderKey adlı bir örnek özel türüdür

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

Aşağıdadır IStateSerializer örnek uygulaması<OrderKey>.
Okuma ve yazma içinde baseValue alın, ileten uyumluluk için kendi ilgili aşırı yüklemesini çağırın aşırı unutmayın.

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

## <a name="upgradability"></a>Upgradability
İçinde bir [uygulama yükseltmesinde](service-fabric-application-upgrade.md), hello yükseltmedir uygulanan tooa alt düğümler, aynı anda bir yükseltme etki alanı. Bu işlem sırasında bazı yükseltme etki alanlarının hello daha yeni sürümü, uygulamanızın üzerinde olacaktır ve bazı yükseltme etki alanlarının hello eski uygulamanızı sürümünde olacaktır. Merhaba piyasaya çıkma sırasında hello yeni sürümü, uygulamanızın mümkün tooread hello eski sürümü verilerinizi olmalıdır ve hello eski sürümü, uygulamanızın verilerinizin mümkün tooread hello yeni sürüm olmalıdır. Merhaba veri biçimi ileriye ve geriye dönük uyumlu hello yükseltme değilse başarısız ya da kötüsü, veri kayıp bozuk veya.

Yerleşik seri hale getirici kullanıyorsanız, uyumluluğu hakkında tooworry yok.
Ancak, özel seri hale getirici veya hello DataContractSerializer kullanıyorsanız, hello veri toobe sonsuz geriye doğru olması ve uyumlu iletir.
Diğer bir deyişle, seri hale getirici her sürümü toobe mümkün tooserialize gerekir ve seri durumdan hello türü herhangi bir sürümü.

Veri sözleşmesi kullanıcılar ekleme, kaldırma ve alanları değiştirme hello iyi tanımlanmış sürüm kuralları başvurmalıdır. Veri sözleşmesi bilinmeyen alanlarla ilgilenme hello seri hale getirme ve seri durumdan çıkarma işlemi takma ve sınıf devralma ile ilgilenen için destek de vardır. Daha fazla bilgi için bkz: [kullanarak veri sözleşmesi](https://msdn.microsoft.com/library/ms733127.aspx).

Özel seri hale getirici kullanıcılar toomake geriye doğru olduğundan ve uyumluluğa emin kullandıkları hello seri hale getirici toohello yönergelerini uymanız gerekir.
Tüm sürümler destekleyen en yaygın yolu hello yalnızca isteğe bağlı özellikler ekleme başında ve boyutu bilgi eklemektir.
Bu şekilde, olabildiğince fazla kullanabilirsiniz ve hello kalan kısmını hello akış atlama her sürümü okuyabilir.

## <a name="next-steps"></a>Sonraki adımlar
  * [Seri hale getirme ve yükseltme](service-fabric-application-upgrade-data-serialization.md)
  * [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.
  * [Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.
  * Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).
  * Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).
  * Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).
