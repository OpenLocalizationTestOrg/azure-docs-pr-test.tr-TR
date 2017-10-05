---
title: Azure Service Fabric DNS hizmeti | Microsoft Docs
description: "Service Fabric'in dns hizmeti mikro hizmetler küme içindeki bulmak için kullanın."
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
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="d3307-103">Azure Service Fabric DNS hizmeti</span><span class="sxs-lookup"><span data-stu-id="d3307-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="d3307-104">DNS hizmeti DNS protokolünü kullanarak diğer hizmetleri bulmak için kümeyi olanak veren bir isteğe bağlı sistem hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="d3307-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="d3307-105">Birçok hizmetler, özellikle kapsayıcılı hizmetler var olan bir URL adına sahip olabilir ve standart DNS Protokolü (adlandırma hizmeti Protokolü yerine) kullanarak bunları gidermek için özellikle "kaldırın ve shift" senaryolarda tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="d3307-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="d3307-106">DNS hizmeti, bir hizmet adı DNS adlarını eşlemek ve bu nedenle uç noktası IP adreslerini çözümlemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3307-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="d3307-107">DNS hizmeti sırayla Adlandırma Hizmeti uç noktası döndürmek için hizmet tarafından çözümlenen hizmet adları için DNS adlarını eşler.</span><span class="sxs-lookup"><span data-stu-id="d3307-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="d3307-108">Hizmeti için DNS ad oluşturma sırasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d3307-108">The DNS name for the service is provided at the time of creation.</span></span> 

![Hizmet uç noktaları][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="d3307-110">DNS hizmeti etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3307-110">Enabling the DNS service</span></span>
<span data-ttu-id="d3307-111">İlk DNS hizmeti kümenizdeki etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3307-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="d3307-112">Şablonu dağıtmak istediğiniz kümenin alın.</span><span class="sxs-lookup"><span data-stu-id="d3307-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="d3307-113">Kullanabilir [örnek şablonlarından](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) veya Resource Manager şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d3307-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="d3307-114">Aşağıdaki adımlarla DNS hizmeti etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d3307-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="d3307-115">Denetleyin `apiversion` ayarlanır `2017-07-01-preview` için `Microsoft.ServiceFabric/clusters` kaynak ve aksi durumda aşağıdaki kod parçacığında gösterildiği gibi güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d3307-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="d3307-116">DNS hizmeti aşağıdakileri ekleyerek şimdi etkinleştirmek `addonFeatures` sonra bölümünde `fabricSettings` bölümünde aşağıdaki kod parçacığında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="d3307-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="d3307-117">Küme şablonunuzu önceki değişiklikleriyle güncelleştirdikten sonra bunları uygulamak ve yükseltme izin tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="d3307-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="d3307-118">Tamamlandıktan sonra DNS sistem hizmetini başlatır çağrılan kümenizde çalışan `fabric:/System/DnsService` sistem hizmeti bölümünde bulunan Service Fabric explorer.</span><span class="sxs-lookup"><span data-stu-id="d3307-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="d3307-119">Alternatif olarak, küme oluşturma sırasında portal üzerinden DNS hizmeti etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3307-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="d3307-120">DNS hizmeti için kutuyu işaretleyerek etkin hale getirilebilir `Include DNS service` içinde `Cluster configuration` aşağıdaki ekran görüntüsünde gösterildiği gibi menüsü:</span><span class="sxs-lookup"><span data-stu-id="d3307-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![DNS hizmeti portal üzerinden etkinleştirme][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="d3307-122">Hizmetiniz için DNS adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="d3307-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="d3307-123">DNS hizmeti kümenizdeki çalışmaya başladıktan sonra hizmetleriniz için bir DNS adı ya da varsayılan Hizmetleri için bildirimli olarak ayarlayabileceğiniz `ApplicationManifest.xml` veya Powershell komutları ile.</span><span class="sxs-lookup"><span data-stu-id="d3307-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="d3307-124">Varsayılan hizmet için DNS adı ApplicationManifest.xml ayarlama</span><span class="sxs-lookup"><span data-stu-id="d3307-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="d3307-125">Visual Studio veya tercih ettiğiniz Düzenleyicisi projenizi açın ve açık `ApplicationManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="d3307-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="d3307-126">Varsayılan Hizmetleri bölümüne gidin ve her hizmet için ekleyin `ServiceDnsName` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d3307-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="d3307-127">Aşağıdaki örnek hizmeti DNS adı ayarlamak nasıl gösterir`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="d3307-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="d3307-128">Uygulama dağıtıldığında, Service Fabric Explorer'da hizmet örneği aşağıdaki resimde gösterildiği gibi bu örneği için DNS adını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d3307-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![Hizmet uç noktaları][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="d3307-130">Powershell kullanarak bir hizmet için DNS adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="d3307-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="d3307-131">Bir hizmet için DNS adını kullanarak oluştururken ayarlayabilirsiniz `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="d3307-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="d3307-132">Aşağıdaki örnek, DNS adıyla yeni bir durum bilgisiz hizmeti oluşturur`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="d3307-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="d3307-133">DNS, Hizmetleri'ni kullanarak</span><span class="sxs-lookup"><span data-stu-id="d3307-133">Using DNS in your services</span></span>
<span data-ttu-id="d3307-134">Birden fazla hizmet dağıtırsanız, uç noktaları ile bir DNS adı kullanarak iletişim kurmak için diğer hizmetlerin bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3307-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="d3307-135">DNS hizmeti, yalnızca DNS protokolü durum bilgisi olan Hizmetleri ile iletişim kuramıyor beri durum bilgisi olmayan hizmetler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d3307-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="d3307-136">Durum bilgisi olan hizmetler için belirli bir hizmet bölümü çağırmak için yerleşik bir ters proxy http çağrıları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3307-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="d3307-137">Aşağıdaki kod, yalnızca bir normal http bağlantı noktası ve isteğe bağlı bir yoldur URL'SİNİN bir parçası verdiğiniz çağrıdır başka bir hizmete çağrı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d3307-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d3307-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3307-138">Next steps</span></span>
<span data-ttu-id="d3307-139">Hizmet iletişimi ile küme içindeki hakkında daha fazla bilgi [bağlanmak ve Hizmetleri ile iletişim](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="d3307-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
