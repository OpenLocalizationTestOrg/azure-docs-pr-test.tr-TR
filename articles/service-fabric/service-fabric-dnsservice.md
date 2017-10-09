---
title: Service Fabric DNS hizmeti aaaAzure | Microsoft Docs
description: "Gelen mikro bulmak için Service Fabric'in dns hizmetini kullanmak hello küme içindeki."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a>Azure Service Fabric DNS hizmeti
Merhaba DNS hizmeti hizmettir, küme toodiscover olanak veren bir isteğe bağlı sistem hello DNS protokolünü kullanarak diğer hizmetler.

Birçok hizmetler, özellikle kapsayıcılı hizmetler var olan bir URL adı ve mümkün tooresolve olması olabilir bunları hello standart DNS Protokolü (Merhaba adlandırma hizmeti Protokolü yerine) kullanarak özellikle "kaldırın ve shift" senaryolarda önerilir. Merhaba DNS hizmeti, toomap DNS adları tooa hizmet adı sağlar ve bu nedenle uç nokta IP adresleri çözümleyin. 

Merhaba DNS hizmeti sırayla hello adlandırma hizmeti tooreturn hello hizmet uç noktası tarafından çözümlenen DNS adlarını tooservice adlarını eşler. Merhaba hizmeti için Hello DNS ad hello oluşturma sırasında sağlanır. 

![Hizmet uç noktaları][0]

## <a name="enabling-hello-dns-service"></a>Merhaba DNS hizmetini etkinleştirme
İlk kümenizdeki tooenable hello DNS hizmeti gerekir. Merhaba şablonu toodeploy istediğiniz hello küme için alın. Ya da kullanım hello yapabilecekleriniz [örnek şablonlarından](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) veya Resource Manager şablonu oluşturun. Aşağıdaki adımları hello ile Merhaba DNS hizmeti etkinleştirebilirsiniz:

1. Bu hello denetleyin `apiversion` çok ayarlanır`2017-07-01-preview` hello için `Microsoft.ServiceFabric/clusters` kaynak ve aksi durumda, hello aşağıdaki kod parçacığında gösterildiği gibi güncelleştirebilirsiniz:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Merhaba aşağıdakileri ekleyerek hello DNS hizmeti şimdi etkinleştirmek `addonFeatures` bölümünden hello sonra `fabricSettings` bölümünde hello aşağıdaki kod parçacığında gösterildiği gibi: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Değişiklikleri önceki hello ile küme şablonunuzu güncelleştirdikten sonra bunları uygulamak ve yükseltme tamamlandı hello sağlayabilirsiniz. Tamamlandıktan sonra hello DNS sistem hizmeti başlatır çağrılan kümenizde çalışan `fabric:/System/DnsService` sistem hizmeti hello Service Fabric explorer bölümünde. 

Alternatif olarak, küme oluşturma hello aynı anda hello DNS hizmeti hello portal üzerinden etkinleştirebilirsiniz. Merhaba DNS hizmeti için hello kutuyu işaretleyerek etkinleştirilebilir `Include DNS service` hello içinde `Cluster configuration` hello ekran aşağıdaki gösterildiği gibi menüsü:

![DNS hizmeti hello portal üzerinden etkinleştirme][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Merhaba DNS adı hizmetiniz için ayarlama
Kümenizdeki Hello DNS hizmeti çalışmaya başladıktan sonra hizmetleriniz için bir DNS adı ya da varsayılan hizmetler için bildirimli olarak hello ayarlayabileceğiniz `ApplicationManifest.xml` veya Powershell komutları ile.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Varsayılan hizmet için Hello DNS adı hello ApplicationManifest.xml ayarlama
Projeniz Visual Studio'da veya tercih ettiğiniz Düzenleyicisi ve açın hello `ApplicationManifest.xml` dosya. Toohello varsayılan Hizmetleri bölümüne gidin ve her hizmet Ekle hello için `ServiceDnsName` özniteliği. Aşağıdaki örnek hello nasıl tooset hello hello hizmetin DNS adı çok gösterir`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Merhaba uygulama dağıtıldığında, hello hizmet örneği hello Service Fabric explorer içinde hello aşağıdaki şekilde gösterildiği gibi hello DNS adı bu örneğin gösterir: 

![Hizmet uç noktaları][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Powershell kullanarak bir hizmet için Hello DNS adı ayarlama
Hello kullanarak oluştururken hello DNS adı bir hizmet için ayarlayabileceğiniz `New-ServiceFabricService` Powershell. Merhaba aşağıdaki örnek yeni bir durum bilgisiz hizmet hello DNS adıyla oluşturur`service1.application1`

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a>DNS, Hizmetleri'ni kullanarak
Birden fazla hizmet dağıtırsanız, DNS adını kullanarak hello uç noktaları ile diğer hizmetleri toocommunicate bulabilirsiniz. Merhaba DNS protokolü durum bilgisi olan Hizmetleri ile iletişim kuramıyor hello DNS hizmeti yalnızca geçerli toostateless Hizmetleri taşımaktadır. Durum bilgisi olan hizmetler için http çağrıları toocall belirli bir hizmet bölümü hello yerleşik ters proxy kullanabilirsiniz.

Merhaba aşağıdaki kod toocall yalnızca normal HTTP başka bir hizmet nasıl çağrı hello bağlantı noktası ve isteğe bağlı bir yoldur hello URL'SİNİN bir parçası verdiğiniz gösterir.

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
Hizmet iletişimi ile Merhaba kümedeki hakkında daha fazla bilgi [bağlanmak ve Hizmetleri ile iletişim](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
