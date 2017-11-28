---
title: "Bulut Hizmetleri rolleri için iletişim | Microsoft Docs"
description: "Bulut Hizmetleri rol örneklerinin dışına veya diğer rol örnekleri arasında iletişim kuran kendileri için tanımlanmış uç noktaları (http, https, tcp, udp) olabilir."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="0cc7a-103">Azure rol örneklerinin iletişimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0cc7a-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="0cc7a-104">Bulut hizmeti rollerinizi iç ve dış bağlantıları iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="0cc7a-105">Dış bağlantılar denir **giriş uç noktaları** iç bağlantılar denir sırada **iç uç noktalar**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="0cc7a-106">Bu konuda nasıl değiştirileceğini açıklar [hizmet tanımı](cloud-services-model-and-package.md#csdef) uç noktaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="0cc7a-107">Giriş uç noktası</span><span class="sxs-lookup"><span data-stu-id="0cc7a-107">Input endpoint</span></span>
<span data-ttu-id="0cc7a-108">Bir dış bağlantı noktasında kullanıma sunmak istediğiniz giriş uç noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="0cc7a-109">Protokol türü ve her iki iç ve dış bağlantı noktaları için uç nokta için geçerli uç nokta bağlantı noktası belirtin.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="0cc7a-110">İsterseniz, farklı bir iç bağlantı noktası bitiş noktası belirtebilirsiniz [yerel bağlantı noktası](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="0cc7a-111">Giriş uç noktası aşağıdaki protokolleri kullanabilirsiniz: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="0cc7a-112">Bir giriş uç noktası oluşturmak için Ekle **Inputendpoint** alt öğeye **uç noktaları** web veya çalışan rolü öğesidir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="0cc7a-113">Örnek giriş uç noktası</span><span class="sxs-lookup"><span data-stu-id="0cc7a-113">Instance input endpoint</span></span>
<span data-ttu-id="0cc7a-114">Örnek giriş uç noktaları uç noktaları ancak verir giriş benzer yük dengeleyicide bağlantı noktası iletme kullanarak her tek rol örneği için belirli genel kullanıma yönelik bağlantı noktalarını eşleme.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="0cc7a-115">Tek bir genel kullanıma yönelik bağlantı noktası veya bağlantı noktası aralığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="0cc7a-116">Örnek giriş uç noktası yalnızca kullanabilirsiniz **tcp** veya **udp** protokol olarak.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="0cc7a-117">Bir örnek giriş uç noktası oluşturmak için Ekle **InstanceInputEndpoint** alt öğeye **uç noktaları** web veya çalışan rolü öğesidir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="0cc7a-118">İç bitiş noktası</span><span class="sxs-lookup"><span data-stu-id="0cc7a-118">Internal endpoint</span></span>
<span data-ttu-id="0cc7a-119">İç uç noktalar örneği, örnek iletişimi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="0cc7a-120">Bağlantı noktası isteğe bağlıdır ve atlanırsa, dinamik bir bağlantı noktası bitiş noktasına atanır.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="0cc7a-121">Bir bağlantı noktası aralığı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-121">A port range can be used.</span></span> <span data-ttu-id="0cc7a-122">Beş iç uç noktalar için rol başına bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="0cc7a-123">Dahili uç noktayı aşağıdaki protokolleri kullanabilirsiniz: **http, tcp, udp herhangi**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="0cc7a-124">Bir iç giriş uç noktası oluşturmak için Ekle **InternalEndpoint** alt öğeye **uç noktaları** web veya çalışan rolü öğesidir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="0cc7a-125">Bir bağlantı noktası aralığı de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="0cc7a-126">Çalışan rollerini vs. Web rolleri</span><span class="sxs-lookup"><span data-stu-id="0cc7a-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="0cc7a-127">Worker ve web rolleri ile çalışırken, uç noktaları küçük bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="0cc7a-128">Web rolü en azından kullanarak bir tek giriş uç noktası olmalıdır **HTTP** protokolü.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="0cc7a-129">Bir uç noktasına erişmek için .NET SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="0cc7a-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="0cc7a-130">Azure yönetilen kitaplık çalışma zamanında iletişim kurmak rol örnekleri için yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="0cc7a-131">İçinde bir rol örneği çalıştıran kodundan, diğer rol örneklerine ve kendi uç noktaları varlığını hakkında bilgi ve geçerli rol örneğiyle ilgili bilgiler alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="0cc7a-132">Yalnızca bulut hizmetiniz çalıştıran ve en az bir iç uç nokta tanımlayan rol örnekleri hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="0cc7a-133">Farklı bir hizmet olarak çalışan rolü örnekleri hakkında veri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="0cc7a-134">Kullanabileceğiniz [örnekleri](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) özelliği bir rolün örnekleri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="0cc7a-135">İlk kez kullanan [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) geçerli rol örneğine başvuru dönmek ve daha sonra kullanmak için [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) rol bir başvuru döndürmek için özellik.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="0cc7a-136">.NET SDK'sı aracılığıyla programlı olarak bir rol örneği bağlandığınızda, uç nokta bilgileri erişim oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="0cc7a-137">Örneğin, belirli bir rol ortamına zaten bağlandıktan sonra bu kod ile belirli bir uç bağlantı noktasını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0cc7a-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="0cc7a-138">**Örnekleri** özelliği bir koleksiyonunu döndürür **RoleInstance** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="0cc7a-139">Bu koleksiyon her zaman geçerli örneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-139">This collection always contains the current instance.</span></span> <span data-ttu-id="0cc7a-140">Rol iç uç nokta tanımlamıyorsa, koleksiyonu geçerli örneği, ancak başka bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="0cc7a-141">Koleksiyon rol örneği sayısı her zaman 1 iç bitiş noktası rolü için tanımlandığı durumda olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="0cc7a-142">Rol iç uç nokta tanımlıyorsa, onun örneklerinin çalışma zamanında bulunabilir ve koleksiyon örneği sayısı, rol hizmeti yapılandırma dosyasında belirtilen örnek sayısı karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="0cc7a-143">Azure yönetilen kitaplığı, diğer rol örneklerine durumunu belirlemek için bir araç sağlamaz, ancak hizmetiniz bu işlevsellik gerektiriyorsa, bu tür sistem durumu değerlendirmesi kendiniz uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="0cc7a-144">Kullanabileceğiniz [Azure tanılama](cloud-services-dotnet-diagnostics.md) rol örnekleri çalıştırma hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="0cc7a-145">Bir rol örneğinde iç uç nokta bağlantı noktası numarasını belirlemek için kullanabileceğiniz [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) uç nokta adlarını ve karşılık gelen IP içeren bir sözlük nesnesi adresleri döndürmek için özellik ve bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="0cc7a-146">[IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) özelliği, belirtilen bir uç noktası için bağlantı noktası ve IP adresi döndürür.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="0cc7a-147">**PublicIPEndpoint** özelliği, bir yük dengeli uç noktası için bağlantı noktası döndürür.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="0cc7a-148">IP adresi kısmını **PublicIPEndpoint** özelliği kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="0cc7a-149">Rol örnekleri tekrarlanan örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="0cc7a-150">Burada gösterilen uç noktası hizmet tanımını alır ve bağlantıları dinlemeyi başlatır çalışan rolü bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="0cc7a-151">Bu kod yalnızca dağıtılan bir hizmet olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="0cc7a-152">Azure işlem öykünücüsü ' çalıştırırken, doğrudan bağlantı noktası uç noktaları oluşturma yapılandırma öğelerini service (**InstanceInputEndpoint** öğeleri) göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="0cc7a-153">Rol iletişimi denetlemek için ağ trafiği kuralları</span><span class="sxs-lookup"><span data-stu-id="0cc7a-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="0cc7a-154">İç uç noktalar tanımladıktan sonra rol örnekleri birbirleri ile nasıl iletişim kurabilir denetimine (oluşturduğunuz uç noktalarda bağlı olarak) ağ trafiği kuralları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="0cc7a-155">Aşağıdaki diyagramda rol iletişimi denetlemek için bazı yaygın senaryolar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="0cc7a-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="0cc7a-156">![Ağ trafik kuralı senaryoları](./media/cloud-services-enable-communication-role-instances/scenarios.png "ağ trafik kuralı senaryoları")</span><span class="sxs-lookup"><span data-stu-id="0cc7a-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="0cc7a-157">Aşağıdaki kod örneğinde, önceki diyagramda gösterildiği rol için rol tanımları gösterir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="0cc7a-158">Her rol tanımı tanımlanan en az bir dahili uç noktayı içerir:</span><span class="sxs-lookup"><span data-stu-id="0cc7a-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="0cc7a-159">Kısıtlama rolleri arasındaki iletişim, hem sabit ve bağlantı noktaları otomatik olarak atanan iç uç nokta ile ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="0cc7a-160">İç uç nokta tanımlandıktan sonra varsayılan olarak, herhangi bir kısıtlama olmadan bir rolü iç uç noktası için herhangi bir rolü iletişimi akabilir.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="0cc7a-161">İletişim kısıtlamak için eklemelisiniz bir **NetworkTrafficRules** öğesine **ServiceDefinition** hizmet tanımı dosyasındaki öğesi.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="0cc7a-162">Senaryo 1</span><span class="sxs-lookup"><span data-stu-id="0cc7a-162">Scenario 1</span></span>
<span data-ttu-id="0cc7a-163">Yalnızca gelen ağ trafiğinin izin **WebRole1** için **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="0cc7a-164">Senaryo 2</span><span class="sxs-lookup"><span data-stu-id="0cc7a-164">Scenario 2</span></span>
<span data-ttu-id="0cc7a-165">Yalnızca gelen ağ trafiğine izin verir **WebRole1** için **WorkerRole1** ve **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="0cc7a-166">Senaryo 3</span><span class="sxs-lookup"><span data-stu-id="0cc7a-166">Scenario 3</span></span>
<span data-ttu-id="0cc7a-167">Yalnızca gelen ağ trafiğine izin verir **WebRole1** için **WorkerRole1**, ve **WorkerRole1** için **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="0cc7a-168">Senaryo 4</span><span class="sxs-lookup"><span data-stu-id="0cc7a-168">Scenario 4</span></span>
<span data-ttu-id="0cc7a-169">Yalnızca gelen ağ trafiğine izin verir **WebRole1** için **WorkerRole1**, **WebRole1** için **WorkerRole2**, ve **WorkerRole1**  için **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="0cc7a-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="0cc7a-170">Yukarıda kullanılan öğeleri için bir XML Şeması Başvurusu bulunabilir [burada](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc7a-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cc7a-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0cc7a-171">Next steps</span></span>
<span data-ttu-id="0cc7a-172">Bulut hizmeti hakkında daha fazla bilgiyi [modeli](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="0cc7a-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

