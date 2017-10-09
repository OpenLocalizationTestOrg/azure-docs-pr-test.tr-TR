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
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="b9b95-103">Azure Service Fabric DNS hizmeti</span><span class="sxs-lookup"><span data-stu-id="b9b95-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="b9b95-104">Merhaba DNS hizmeti hizmettir, küme toodiscover olanak veren bir isteğe bağlı sistem hello DNS protokolünü kullanarak diğer hizmetler.</span><span class="sxs-lookup"><span data-stu-id="b9b95-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="b9b95-105">Birçok hizmetler, özellikle kapsayıcılı hizmetler var olan bir URL adı ve mümkün tooresolve olması olabilir bunları hello standart DNS Protokolü (Merhaba adlandırma hizmeti Protokolü yerine) kullanarak özellikle "kaldırın ve shift" senaryolarda önerilir.</span><span class="sxs-lookup"><span data-stu-id="b9b95-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="b9b95-106">Merhaba DNS hizmeti, toomap DNS adları tooa hizmet adı sağlar ve bu nedenle uç nokta IP adresleri çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="b9b95-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="b9b95-107">Merhaba DNS hizmeti sırayla hello adlandırma hizmeti tooreturn hello hizmet uç noktası tarafından çözümlenen DNS adlarını tooservice adlarını eşler.</span><span class="sxs-lookup"><span data-stu-id="b9b95-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="b9b95-108">Merhaba hizmeti için Hello DNS ad hello oluşturma sırasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b9b95-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Hizmet uç noktaları][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="b9b95-110">Merhaba DNS hizmetini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b9b95-110">Enabling hello DNS service</span></span>
<span data-ttu-id="b9b95-111">İlk kümenizdeki tooenable hello DNS hizmeti gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9b95-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="b9b95-112">Merhaba şablonu toodeploy istediğiniz hello küme için alın.</span><span class="sxs-lookup"><span data-stu-id="b9b95-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="b9b95-113">Ya da kullanım hello yapabilecekleriniz [örnek şablonlarından](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) veya Resource Manager şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9b95-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="b9b95-114">Aşağıdaki adımları hello ile Merhaba DNS hizmeti etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b9b95-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="b9b95-115">Bu hello denetleyin `apiversion` çok ayarlanır`2017-07-01-preview` hello için `Microsoft.ServiceFabric/clusters` kaynak ve aksi durumda, hello aşağıdaki kod parçacığında gösterildiği gibi güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b9b95-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="b9b95-116">Merhaba aşağıdakileri ekleyerek hello DNS hizmeti şimdi etkinleştirmek `addonFeatures` bölümünden hello sonra `fabricSettings` bölümünde hello aşağıdaki kod parçacığında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="b9b95-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="b9b95-117">Değişiklikleri önceki hello ile küme şablonunuzu güncelleştirdikten sonra bunları uygulamak ve yükseltme tamamlandı hello sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9b95-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="b9b95-118">Tamamlandıktan sonra hello DNS sistem hizmeti başlatır çağrılan kümenizde çalışan `fabric:/System/DnsService` sistem hizmeti hello Service Fabric explorer bölümünde.</span><span class="sxs-lookup"><span data-stu-id="b9b95-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="b9b95-119">Alternatif olarak, küme oluşturma hello aynı anda hello DNS hizmeti hello portal üzerinden etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9b95-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="b9b95-120">Merhaba DNS hizmeti için hello kutuyu işaretleyerek etkinleştirilebilir `Include DNS service` hello içinde `Cluster configuration` hello ekran aşağıdaki gösterildiği gibi menüsü:</span><span class="sxs-lookup"><span data-stu-id="b9b95-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![DNS hizmeti hello portal üzerinden etkinleştirme][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="b9b95-122">Merhaba DNS adı hizmetiniz için ayarlama</span><span class="sxs-lookup"><span data-stu-id="b9b95-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="b9b95-123">Kümenizdeki Hello DNS hizmeti çalışmaya başladıktan sonra hizmetleriniz için bir DNS adı ya da varsayılan hizmetler için bildirimli olarak hello ayarlayabileceğiniz `ApplicationManifest.xml` veya Powershell komutları ile.</span><span class="sxs-lookup"><span data-stu-id="b9b95-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="b9b95-124">Varsayılan hizmet için Hello DNS adı hello ApplicationManifest.xml ayarlama</span><span class="sxs-lookup"><span data-stu-id="b9b95-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="b9b95-125">Projeniz Visual Studio'da veya tercih ettiğiniz Düzenleyicisi ve açın hello `ApplicationManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="b9b95-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="b9b95-126">Toohello varsayılan Hizmetleri bölümüne gidin ve her hizmet Ekle hello için `ServiceDnsName` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="b9b95-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="b9b95-127">Aşağıdaki örnek hello nasıl tooset hello hello hizmetin DNS adı çok gösterir`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="b9b95-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="b9b95-128">Merhaba uygulama dağıtıldığında, hello hizmet örneği hello Service Fabric explorer içinde hello aşağıdaki şekilde gösterildiği gibi hello DNS adı bu örneğin gösterir:</span><span class="sxs-lookup"><span data-stu-id="b9b95-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![Hizmet uç noktaları][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="b9b95-130">Powershell kullanarak bir hizmet için Hello DNS adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="b9b95-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="b9b95-131">Hello kullanarak oluştururken hello DNS adı bir hizmet için ayarlayabileceğiniz `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="b9b95-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="b9b95-132">Merhaba aşağıdaki örnek yeni bir durum bilgisiz hizmet hello DNS adıyla oluşturur`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="b9b95-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="b9b95-133">DNS, Hizmetleri'ni kullanarak</span><span class="sxs-lookup"><span data-stu-id="b9b95-133">Using DNS in your services</span></span>
<span data-ttu-id="b9b95-134">Birden fazla hizmet dağıtırsanız, DNS adını kullanarak hello uç noktaları ile diğer hizmetleri toocommunicate bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9b95-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="b9b95-135">Merhaba DNS protokolü durum bilgisi olan Hizmetleri ile iletişim kuramıyor hello DNS hizmeti yalnızca geçerli toostateless Hizmetleri taşımaktadır.</span><span class="sxs-lookup"><span data-stu-id="b9b95-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="b9b95-136">Durum bilgisi olan hizmetler için http çağrıları toocall belirli bir hizmet bölümü hello yerleşik ters proxy kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9b95-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="b9b95-137">Merhaba aşağıdaki kod toocall yalnızca normal HTTP başka bir hizmet nasıl çağrı hello bağlantı noktası ve isteğe bağlı bir yoldur hello URL'SİNİN bir parçası verdiğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9b95-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b9b95-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9b95-138">Next steps</span></span>
<span data-ttu-id="b9b95-139">Hizmet iletişimi ile Merhaba kümedeki hakkında daha fazla bilgi [bağlanmak ve Hizmetleri ile iletişim](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="b9b95-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
