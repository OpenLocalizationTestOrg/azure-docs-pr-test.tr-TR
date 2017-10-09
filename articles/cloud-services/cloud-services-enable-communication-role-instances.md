---
title: "Bulut Hizmetleri rolleri için aaaCommunication | Microsoft Docs"
description: "Bulut Hizmetleri rol örneklerinin hello dışında veya diğer rol örnekleri arasında iletişim kendileri için tanımlanmış uç noktaları (http, https, tcp, udp) olabilir."
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
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="57b4c-103">Azure rol örneklerinin iletişimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="57b4c-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="57b4c-104">Bulut hizmeti rollerinizi iç ve dış bağlantıları iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="57b4c-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="57b4c-105">Dış bağlantılar denir **giriş uç noktaları** iç bağlantılar denir sırada **iç uç noktalar**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="57b4c-106">Bu konuda açıklanmaktadır nasıl toomodify hello [hizmet tanımı](cloud-services-model-and-package.md#csdef) toocreate uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="57b4c-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="57b4c-107">Giriş uç noktası</span><span class="sxs-lookup"><span data-stu-id="57b4c-107">Input endpoint</span></span>
<span data-ttu-id="57b4c-108">dışında bir bağlantı noktası toohello tooexpose istediğinizde hello giriş uç noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57b4c-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="57b4c-109">Merhaba protokol türü ve her iki hello iç ve dış bağlantı noktaları için hello uç noktası için uygulanan hello endpoint hello bağlantı noktası belirtin.</span><span class="sxs-lookup"><span data-stu-id="57b4c-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="57b4c-110">İsterseniz, hello uç noktası için farklı bir iç bağlantı ile Merhaba belirtebilirsiniz [yerel bağlantı noktası](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) özniteliği.</span><span class="sxs-lookup"><span data-stu-id="57b4c-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="57b4c-111">Merhaba giriş uç noktası protokolleri aşağıdaki hello kullanabilirsiniz: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="57b4c-112">toocreate bir giriş uç noktası ekleme hello **Inputendpoint** alt öğesi toohello **uç noktaları** web veya çalışan rolü öğesidir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="57b4c-113">Örnek giriş uç noktası</span><span class="sxs-lookup"><span data-stu-id="57b4c-113">Instance input endpoint</span></span>
<span data-ttu-id="57b4c-114">Örnek giriş uç noktaları benzer tooinput noktalarıdır ancak sağlar hello yük dengeleyicideki bağlantı noktası iletme kullanarak her tek rol örneği için belirli genel kullanıma yönelik bağlantı noktalarını eşleyin.</span><span class="sxs-lookup"><span data-stu-id="57b4c-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="57b4c-115">Tek bir genel kullanıma yönelik bağlantı noktası veya bağlantı noktası aralığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57b4c-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="57b4c-116">Merhaba örnek giriş uç noktası yalnızca kullanabilir **tcp** veya **udp** hello protokol olarak.</span><span class="sxs-lookup"><span data-stu-id="57b4c-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="57b4c-117">toocreate bir örnek giriş uç noktası, ekleme hello **InstanceInputEndpoint** alt öğesi toohello **uç noktaları** web veya çalışan rolü öğesidir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="57b4c-118">İç bitiş noktası</span><span class="sxs-lookup"><span data-stu-id="57b4c-118">Internal endpoint</span></span>
<span data-ttu-id="57b4c-119">İç uç noktalar örneği, örnek iletişimi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="57b4c-120">başlangıç bağlantı noktası isteğe bağlıdır ve atlanırsa, dinamik bir bağlantı noktası toohello endpoint atanır.</span><span class="sxs-lookup"><span data-stu-id="57b4c-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="57b4c-121">Bir bağlantı noktası aralığı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-121">A port range can be used.</span></span> <span data-ttu-id="57b4c-122">Beş iç uç noktalar için rol başına bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="57b4c-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="57b4c-123">Merhaba dahili uç noktayı protokolleri aşağıdaki hello kullanabilirsiniz: **http, tcp, udp herhangi**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="57b4c-124">toocreate bir iç giriş uç noktası ekleme hello **InternalEndpoint** alt öğesi toohello **uç noktaları** web veya çalışan rolü öğesidir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="57b4c-125">Bir bağlantı noktası aralığı de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57b4c-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="57b4c-126">Çalışan rollerini vs. Web rolleri</span><span class="sxs-lookup"><span data-stu-id="57b4c-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="57b4c-127">Worker ve web rolleri ile çalışırken, uç noktaları küçük bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="57b4c-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="57b4c-128">Merhaba web rolü en azından hello kullanarak tek bir giriş uç noktası olmalıdır **HTTP** protokolü.</span><span class="sxs-lookup"><span data-stu-id="57b4c-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="57b4c-129">Merhaba .NET SDK'sı tooaccess bir uç nokta kullanma</span><span class="sxs-lookup"><span data-stu-id="57b4c-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="57b4c-130">Hello Azure yönetilen kitaplık çalışma zamanında rol örnekleri toocommunicate için yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="57b4c-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="57b4c-131">İçinde bir rol örneği çalıştıran koddan hello varlığını diğer rol örnekleri ve bunların uç noktalar hakkında bilgi ve hello geçerli rol örneği hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57b4c-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="57b4c-132">Yalnızca bulut hizmetiniz çalıştıran ve en az bir iç uç nokta tanımlayan rol örnekleri hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57b4c-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="57b4c-133">Farklı bir hizmet olarak çalışan rolü örnekleri hakkında veri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="57b4c-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="57b4c-134">Merhaba kullanabilirsiniz [örnekleri](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) özelliği tooretrieve bir rolün örnekleri.</span><span class="sxs-lookup"><span data-stu-id="57b4c-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="57b4c-135">İlk hello kullan [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn bir başvuru toohello geçerli rol örneği ve hello kullan [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) özelliği tooreturn başvuru toohello rol kendisi.</span><span class="sxs-lookup"><span data-stu-id="57b4c-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="57b4c-136">Tooa rol örneği program aracılığıyla hello .NET SDK'sı bağlanıyorsa, görece olarak daha kolay tooaccess hello uç nokta bilgileri önerilir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="57b4c-137">Örneğin, tooa belirli rol ortamı zaten bağlandıktan sonra kodu içeren belirli bir uç noktası başlangıç bağlantı noktası alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="57b4c-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="57b4c-138">Merhaba **örnekleri** özelliği bir koleksiyonunu döndürür **RoleInstance** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="57b4c-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="57b4c-139">Bu koleksiyon her zaman hello geçerli örneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="57b4c-140">Merhaba rol iç uç nokta tanımlamıyorsa hello koleksiyon hello geçerli örneği, ancak başka bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="57b4c-141">Merhaba sayıda rol örneği hello koleksiyondaki her zaman 1 iç bitiş noktası hello rolü için tanımlandığı hello durumda olacaktır.</span><span class="sxs-lookup"><span data-stu-id="57b4c-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="57b4c-142">Merhaba rol iç uç nokta tanımlıyorsa, onun örneklerinin çalışma zamanında bulunabilir ve hello koleksiyonu örneği hello sayısı toohello hello hizmet yapılandırma dosyasında hello rolü için belirtilen örneklerinin sayısını karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="57b4c-143">Hello Azure yönetilen kitaplığı, diğer rol örneklerine hello durumunu belirlemek için bir araç sağlamaz, ancak hizmetiniz bu işlevsellik gerektiriyorsa, bu tür sistem durumu değerlendirmesi kendiniz uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57b4c-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="57b4c-144">Kullanabileceğiniz [Azure tanılama](cloud-services-dotnet-diagnostics.md) rol örnekleri çalıştırma hakkında bilgi tooobtain.</span><span class="sxs-lookup"><span data-stu-id="57b4c-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="57b4c-145">toodetermine hello bağlantı noktası numarası bir rol örneğinde iç uç nokta için kullanabileceğiniz hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) özelliği tooreturn uç nokta adlarını ve karşılık gelen IP içeren bir sözlük nesnesi adresleri ve bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="57b4c-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="57b4c-146">Merhaba [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) özelliği, başlangıç IP adresi ve belirtilen bir uç noktası için bağlantı noktası döndürür.</span><span class="sxs-lookup"><span data-stu-id="57b4c-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="57b4c-147">Merhaba **PublicIPEndpoint** özelliği, bir yük dengeli uç noktası için başlangıç bağlantı noktası döndürür.</span><span class="sxs-lookup"><span data-stu-id="57b4c-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="57b4c-148">Başlangıç IP adresi hello kısmını **PublicIPEndpoint** özelliği kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="57b4c-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="57b4c-149">Rol örnekleri tekrarlanan örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="57b4c-150">Merhaba hizmet tanımı kullanıma sunulan hello endpoint alır ve bağlantıları dinlemeyi başlatır çalışan rolü bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="57b4c-151">Bu kod yalnızca dağıtılan bir hizmet olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="57b4c-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="57b4c-152">Doğrudan bağlantı noktası uç noktaları oluşturma yapılandırma öğeleri Hello Azure işlem öykünücüsü çalıştırırken, hizmet (**InstanceInputEndpoint** öğeleri) göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
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
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="57b4c-153">Ağ trafiği kuralları toocontrol rol iletişimi</span><span class="sxs-lookup"><span data-stu-id="57b4c-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="57b4c-154">İç uç noktalar tanımladıktan sonra ağ trafiği kuralları (oluşturduğunuz hello uç noktalarda bağlı olarak) toocontrol rol örnekleri birbirleri ile nasıl iletişim kurabilir ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57b4c-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="57b4c-155">Merhaba Aşağıdaki diyagramda rol iletişimi denetlemek için bazı yaygın senaryolar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="57b4c-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="57b4c-156">![Ağ trafik kuralı senaryoları](./media/cloud-services-enable-communication-role-instances/scenarios.png "ağ trafik kuralı senaryoları")</span><span class="sxs-lookup"><span data-stu-id="57b4c-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="57b4c-157">Merhaba aşağıdaki kod örneğinde rol tanımları hello önceki diyagramda gösterildiği hello rolleri için gösterir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="57b4c-158">Her rol tanımı tanımlanan en az bir dahili uç noktayı içerir:</span><span class="sxs-lookup"><span data-stu-id="57b4c-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="57b4c-159">Kısıtlama rolleri arasındaki iletişim, hem sabit ve bağlantı noktaları otomatik olarak atanan iç uç nokta ile ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="57b4c-160">İç uç nokta tanımlandıktan sonra varsayılan olarak, herhangi bir rolün herhangi bir kısıtlamanın olmadığı rol toohello iç uç noktasından iletişimi akabilir.</span><span class="sxs-lookup"><span data-stu-id="57b4c-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="57b4c-161">toorestrict iletişim eklemelisiniz bir **NetworkTrafficRules** öğesi toohello **ServiceDefinition** hello hizmet tanımı dosyasındaki öğesi.</span><span class="sxs-lookup"><span data-stu-id="57b4c-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="57b4c-162">Senaryo 1</span><span class="sxs-lookup"><span data-stu-id="57b4c-162">Scenario 1</span></span>
<span data-ttu-id="57b4c-163">Yalnızca gelen ağ trafiğinin izin **WebRole1** çok**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="57b4c-164">Senaryo 2</span><span class="sxs-lookup"><span data-stu-id="57b4c-164">Scenario 2</span></span>
<span data-ttu-id="57b4c-165">Yalnızca gelen ağ trafiğine izin verir **WebRole1** çok**WorkerRole1** ve **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="57b4c-166">Senaryo 3</span><span class="sxs-lookup"><span data-stu-id="57b4c-166">Scenario 3</span></span>
<span data-ttu-id="57b4c-167">Yalnızca gelen ağ trafiğine izin verir **WebRole1** çok**WorkerRole1**, ve **WorkerRole1** çok**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="57b4c-168">Senaryo 4</span><span class="sxs-lookup"><span data-stu-id="57b4c-168">Scenario 4</span></span>
<span data-ttu-id="57b4c-169">Yalnızca gelen ağ trafiğine izin verir **WebRole1** çok**WorkerRole1**, **WebRole1** çok**WorkerRole2**, ve  **WorkerRole1** çok**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="57b4c-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="57b4c-170">Yukarıda kullanılan hello öğeleri için bir XML Şeması Başvurusu bulunabilir [burada](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="57b4c-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="57b4c-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57b4c-171">Next steps</span></span>
<span data-ttu-id="57b4c-172">Bulut hizmeti hakkında daha fazlasını okuyun hello [modeli](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="57b4c-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

