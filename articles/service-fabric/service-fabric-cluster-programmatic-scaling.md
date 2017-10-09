---
title: "aaaAzure Service Fabric programlı ölçeklendirme | Microsoft Docs"
description: "Bir Azure Service Fabric kümesi veya ölçeklendirmek programlı olarak toocustom Tetikleyicileri according"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Service Fabric kümesi programlı olarak ölçeklendirin 

Azure Service Fabric kümesi ölçeklendirme temellerini ele alınmıştır belgelerinde üzerinde [küme ölçeklendirme](./service-fabric-cluster-scale-up-down.md). Bu makale nasıl Service Fabric kümeleri üzerinde sanal makine ölçek kümeleri oluşturulur ve el ile veya Otomatik ölçek kurallarla Genişletilebilir kapsar. Bu belgede daha Gelişmiş senaryolar için denetleyici Azure ölçeklendirme işlemlerinin programlama yöntemleri bakar. 

## <a name="reasons-for-programmatic-scaling"></a>Programsal ölçeklendirme nedenleri
Birçok senaryoda el ile veya Otomatik ölçek kuralı aracılığıyla ölçeklendirme iyi çözümdür. Diğer senaryolarda, ancak bunlar sağ sığacak hello olmayabilir. Olası dezavantajları toothese yaklaşımlar şunlardır:

- El ile ölçeklendirme içinde toolog ve açıkça işlemleri ölçeklendirme isteği gerektirir. Ölçeklendirme işlemlerinin sık veya beklenmeyen zamanlarda gerekirse, bu yaklaşım iyi bir çözüm olmayabilir.
- Otomatik ölçek kuralı sanal makine ölçek kümesindeki bir örneği kaldırdığınızda, Gümüş veya altın dayanıklılık düzeyini hello düğüm türüne sahip olmadığı sürece bunlar otomatik olarak bilgi o düğümün ilişkili hello Service Fabric kümesinden kaldırmayın. Otomatik ölçek kuralı düzeyi Ayarla hello ölçekte (yerine hello Service Fabric düzeyi) çalışması nedeniyle otomatik ölçek kuralı düzgün biçimde kapatılıyor olmadan Service Fabric düğümleri kaldırabilirsiniz. Bu utangaç düğüm kaldırma 'hayalet' Service Fabric düğüm durumu ölçek bileşenini işlemlerinden sonra ardınızda. Tek bir (veya hizmet) tooperiodically hello Service Fabric kümesindeki kaldırılmış düğüm durumu temizlenmesi gerekir.
  - Altın veya gümüş dayanıklılık düzeyine sahip bir düğüm türü otomatik olarak temizler Not düğümleri kaldırıldı.  
- Vardır, ancak [birçok ölçümleri](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) otomatik ölçek kuralları tarafından desteklenen, hala olduğu sınırlı bir dizi. Senaryonuz bu kümesinde kapsanmayan bazı ölçüm göre ölçekleme için çağırırsa, otomatik ölçeklendirme kurallarını iyi bir seçenek olmayabilir.

Bu sınırlamalar bağlı olarak, daha özelleştirilmiş otomatik ölçekleme modelleri tooimplement isteyebilir. 

## <a name="scaling-apis"></a>Ölçeklendirme API'leri
Azure API uygulamaları tooprogrammatically iş Service Fabric kümeleri ve sanal makine ölçek kümeleri olanak mevcut. Bu API'leri varolan otomatik ölçeklendirme seçeneği senaryonuz için işe yaramazsa, olası tooimplement özel ölçeklendirme mantık kolaylaştırır. 

Bu 'giriş-yapılan' otomatik ölçeklendirme bir yaklaşım tooimplementing işlevselliği tooadd işlemleri ölçeklendirme bir yeni durum bilgisiz hizmet toohello Service Fabric uygulaması toomanage olduğu. Merhaba hizmetin içinde `RunAsync` yöntemi, bir dizi Tetikleyicileri belirleyebilir ölçeklendirme (küme boyutu üst sınırı gibi parametreleri denetleniyor ve cooldowns ölçeklendirme dahil) gerekli olup olmadığını.   

Merhaba sanal makine ölçek kümesi etkileşimler için kullanılan API (her iki toocheck hello geçerli sanal makine örnekleri ve sayısını toomodify onu) hello olan [fluent yönetim Azure işlem Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). Merhaba fluent işlem kitaplığı, sanal makine ölçek kümeleri ile etkileşmek için kullanımı kolay API sağlar.

Merhaba Service Fabric kümesi kendisi ile toointeract kullanmak [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Elbette, kod ölçeklendirme hello toorun bir hizmet olarak gerek yoktur ölçeklendirilmiş hello küme toobe içinde. Her ikisi de `IAzure` ve `FabricClient` hizmeti ölçeklendirme hello kolayca bir konsol uygulaması veya dış hello Service Fabric uygulamadan çalışan Windows hizmeti böylece ilişkili tootheir Azure kaynaklarını uzaktan bağlanabilirsiniz. 

## <a name="credential-management"></a>Kimlik bilgisi yönetimi
Bir hizmet toohandle ölçekleme yazma bir hello hizmeti mümkün tooaccess sanal makine ölçek kümesi kaynakları etkileşimli oturum açma olmadan olmalıdır iştir. Merhaba Service Fabric erişme Küme hizmeti ölçeklendirme hello kendi Service Fabric uygulaması değiştirme, ancak kimlik bilgileri gerekli tooaccess kolaydır hello ölçek kümesi. kullanabileceğiniz toolog içinde bir [hizmet sorumlusu](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) hello ile oluşturulan [Azure CLI 2.0](https://github.com/azure/azure-cli).

Bir hizmet sorumlusu aşağıdaki adımları hello ile oluşturulabilir:

1. Toohello Azure CLI oturum (`az login`) erişim toohello sanal makine ölçek sahip bir kullanıcı olarak ayarlayın
2. Merhaba hizmet sorumlusu ile oluşturma`az ad sp create-for-rbac`
    1. Merhaba AppID ('istemci kimliği' başka bir yerde olarak adlandırılır), adı, şifresi ve Kiracı daha sonra kullanmak için not edin.
    2. İle görüntülenebilir abonelik Kimliğinizi de gerekir`az account list`

Merhaba fluent işlem kitaplığı gibi bu kimlik bilgilerini kullanarak oturum açabilir (çekirdek fluent Azure türleri ister Not `IAzure` hello olan [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) paket):

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

Aracılığıyla oturum açtıktan sonra ölçek kümesi örnek sayısı sorgulanabilir `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Ölçeği genişletme
Merhaba fluent kullanarak Azure işlem SDK, örnekleri yalnızca birkaç aramaları ayarlamak toohello sanal makine ölçek eklenebilir-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Alternatif olarak, sanal makine ölçek kümesi boyutu PowerShell cmdlet'leri ile yönetilebilir. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)Merhaba sanal makine ölçek kümesi nesnesi alabilir. Merhaba geçerli kapasite hello depolanacağı `.sku.capacity` özelliği. İstenen değer Hello kapasite toohello değiştirme sonra Azure'da ayarlamak hello sanal makine ölçek hello ile güncelleştirilebilir [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) komutu.

Bir düğüm el ile eklerken, örnek bir ölçek kümesi ekleme şablon hello ölçek kümesi bu yana yeni bir Service Fabric düğümü içeren tüm bu gerekli toostart olması gerektiği gibi uzantıları tooautomatically yeni örnekleri toohello Service Fabric kümesi katılın. 

## <a name="scaling-in"></a>İçinde ölçeklendirme

İçinde ölçeklendirme çıkışı benzer tooscaling olur. Pratikte değişikliklerdir hello gerçek sanal makine ölçek kümesi aynı hello. Ancak, daha önce açıklandığı gibi Service Fabric kaldırılan düğümlerini altın veya Gümüş bir dayanıklılık yalnızca otomatik olarak temizlenir.. İsteğe bağlı olarak Hello Bronz dayanıklılık ölçek bileşenini durumda gerekli toointeract hello Service Fabric sahip olacak şekilde hello düğümü toobe kaldırılan aşağı tooshut ve tooremove durumuna küme.

Merhaba düğümü toobe bulma kapatma içerir hello düğümü hazırlama (Merhaba en son eklenen düğümü) kaldırıldı ve onu devre dışı bırakma. Çekirdek olmayan düğümleri için yeni düğümler karşılaştırarak bulunabilir `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Unutmayın, *çekirdek* düğümleri yok gibi görünüyor tooalways izleyin hello kuralı büyük örneği kimlikleri ilk kaldırılır.

Kaldırılan hello düğümü toobe bulunduktan sonra devre dışı bırakılabilir ve kaldırılan kullanarak, hello aynı `FabricClient` örneği ve hello `IAzure` örneğinden daha önce.

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

Komut dosyası bir yaklaşım tercih ise olarak, sanal makine ölçek değiştirmek için PowerShell cmdlet'leri ölçeğini genişletme ile kümesi kapasitesi de kullanılabilir. Merhaba sanal makine örneğini kaldırıldığında Service Fabric düğüm durumu kaldırılabilir.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Olası dezavantajları

Kod parçacıkları önceki hello gösterildiği gibi ölçeklendirme hizmetinizi oluşturma denetimi ve uygulamanızı üzerinden özelleştirilebilirliğini yüksek derecede hello davranışı ölçeklendirme sağlar. Bu, ne zaman veya nasıl bir uygulama veya ölçeklendirir üzerinde kesin denetim gerektiren senaryolar için faydalı olabilir. Ancak, bu denetim bir kod karmaşıklığı kolaylığını ile birlikte gelir. Bu yaklaşımı kullanarak, Önemsiz olmayan kod ölçeklendirme tooown gerektiği anlamına gelir.

Service Fabric ölçeklendirme nasıl ulaşmalıdır, senaryoya bağlıdır. Ölçeklendirme seyrek hello özelliği tooadd veya kaldırma düğümleri el ile ise, muhtemelen yeterli. Daha karmaşık senaryolar için otomatik ölçeklendirme kurallarını ve hello özelliği tooscale program aracılığıyla gösterme SDK'ları güçlü alternatifleri sunar.

## <a name="next-steps"></a>Sonraki adımlar

kendi otomatik ölçeklendirme mantığı uygulamak başlatılan tooget tanıyın kendiniz ile Merhaba kavramları ve yararlı API'leri aşağıdaki:

- [El ile veya Otomatik ölçek kurallarla ölçeklendirme](./service-fabric-cluster-scale-up-down.md)
- [.NET için Azure yönetim kitaplıklarını Fluent](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (bir Service Fabric kümenin temel sanal makine ölçek kümeleri ile etkileşim için yararlıdır)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (Service Fabric kümesini ve düğümlerini ile etkileşim için yararlıdır)
