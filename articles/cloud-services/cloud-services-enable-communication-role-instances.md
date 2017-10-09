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
# <a name="enable-communication-for-role-instances-in-azure"></a>Azure rol örneklerinin iletişimi etkinleştir
Bulut hizmeti rollerinizi iç ve dış bağlantıları iletişim kurar. Dış bağlantılar denir **giriş uç noktaları** iç bağlantılar denir sırada **iç uç noktalar**. Bu konuda açıklanmaktadır nasıl toomodify hello [hizmet tanımı](cloud-services-model-and-package.md#csdef) toocreate uç noktaları.

## <a name="input-endpoint"></a>Giriş uç noktası
dışında bir bağlantı noktası toohello tooexpose istediğinizde hello giriş uç noktası kullanılır. Merhaba protokol türü ve her iki hello iç ve dış bağlantı noktaları için hello uç noktası için uygulanan hello endpoint hello bağlantı noktası belirtin. İsterseniz, hello uç noktası için farklı bir iç bağlantı ile Merhaba belirtebilirsiniz [yerel bağlantı noktası](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) özniteliği.

Merhaba giriş uç noktası protokolleri aşağıdaki hello kullanabilirsiniz: **http, https, tcp, udp**.

toocreate bir giriş uç noktası ekleme hello **Inputendpoint** alt öğesi toohello **uç noktaları** web veya çalışan rolü öğesidir.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Örnek giriş uç noktası
Örnek giriş uç noktaları benzer tooinput noktalarıdır ancak sağlar hello yük dengeleyicideki bağlantı noktası iletme kullanarak her tek rol örneği için belirli genel kullanıma yönelik bağlantı noktalarını eşleyin. Tek bir genel kullanıma yönelik bağlantı noktası veya bağlantı noktası aralığını belirtebilirsiniz.

Merhaba örnek giriş uç noktası yalnızca kullanabilir **tcp** veya **udp** hello protokol olarak.

toocreate bir örnek giriş uç noktası, ekleme hello **InstanceInputEndpoint** alt öğesi toohello **uç noktaları** web veya çalışan rolü öğesidir.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>İç bitiş noktası
İç uç noktalar örneği, örnek iletişimi için kullanılabilir. başlangıç bağlantı noktası isteğe bağlıdır ve atlanırsa, dinamik bir bağlantı noktası toohello endpoint atanır. Bir bağlantı noktası aralığı kullanılabilir. Beş iç uç noktalar için rol başına bir sınır yoktur.

Merhaba dahili uç noktayı protokolleri aşağıdaki hello kullanabilirsiniz: **http, tcp, udp herhangi**.

toocreate bir iç giriş uç noktası ekleme hello **InternalEndpoint** alt öğesi toohello **uç noktaları** web veya çalışan rolü öğesidir.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

Bir bağlantı noktası aralığı de kullanabilirsiniz.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Çalışan rollerini vs. Web rolleri
Worker ve web rolleri ile çalışırken, uç noktaları küçük bir fark yoktur. Merhaba web rolü en azından hello kullanarak tek bir giriş uç noktası olmalıdır **HTTP** protokolü.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Merhaba .NET SDK'sı tooaccess bir uç nokta kullanma
Hello Azure yönetilen kitaplık çalışma zamanında rol örnekleri toocommunicate için yöntemleri sağlar. İçinde bir rol örneği çalıştıran koddan hello varlığını diğer rol örnekleri ve bunların uç noktalar hakkında bilgi ve hello geçerli rol örneği hakkında bilgi alabilirsiniz.

> [!NOTE]
> Yalnızca bulut hizmetiniz çalıştıran ve en az bir iç uç nokta tanımlayan rol örnekleri hakkında bilgi alabilirsiniz. Farklı bir hizmet olarak çalışan rolü örnekleri hakkında veri alınamıyor.
> 
> 

Merhaba kullanabilirsiniz [örnekleri](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) özelliği tooretrieve bir rolün örnekleri. İlk hello kullan [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn bir başvuru toohello geçerli rol örneği ve hello kullan [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) özelliği tooreturn başvuru toohello rol kendisi.

Tooa rol örneği program aracılığıyla hello .NET SDK'sı bağlanıyorsa, görece olarak daha kolay tooaccess hello uç nokta bilgileri önerilir. Örneğin, tooa belirli rol ortamı zaten bağlandıktan sonra kodu içeren belirli bir uç noktası başlangıç bağlantı noktası alabilirsiniz:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Merhaba **örnekleri** özelliği bir koleksiyonunu döndürür **RoleInstance** nesneleri. Bu koleksiyon her zaman hello geçerli örneğini içerir. Merhaba rol iç uç nokta tanımlamıyorsa hello koleksiyon hello geçerli örneği, ancak başka bir örnek içerir. Merhaba sayıda rol örneği hello koleksiyondaki her zaman 1 iç bitiş noktası hello rolü için tanımlandığı hello durumda olacaktır. Merhaba rol iç uç nokta tanımlıyorsa, onun örneklerinin çalışma zamanında bulunabilir ve hello koleksiyonu örneği hello sayısı toohello hello hizmet yapılandırma dosyasında hello rolü için belirtilen örneklerinin sayısını karşılık gelir.

> [!NOTE]
> Hello Azure yönetilen kitaplığı, diğer rol örneklerine hello durumunu belirlemek için bir araç sağlamaz, ancak hizmetiniz bu işlevsellik gerektiriyorsa, bu tür sistem durumu değerlendirmesi kendiniz uygulayabilirsiniz. Kullanabileceğiniz [Azure tanılama](cloud-services-dotnet-diagnostics.md) rol örnekleri çalıştırma hakkında bilgi tooobtain.
> 
> 

toodetermine hello bağlantı noktası numarası bir rol örneğinde iç uç nokta için kullanabileceğiniz hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) özelliği tooreturn uç nokta adlarını ve karşılık gelen IP içeren bir sözlük nesnesi adresleri ve bağlantı noktaları. Merhaba [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) özelliği, başlangıç IP adresi ve belirtilen bir uç noktası için bağlantı noktası döndürür. Merhaba **PublicIPEndpoint** özelliği, bir yük dengeli uç noktası için başlangıç bağlantı noktası döndürür. Başlangıç IP adresi hello kısmını **PublicIPEndpoint** özelliği kullanılamıyor.

Rol örnekleri tekrarlanan örnek aşağıda verilmiştir.

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

Merhaba hizmet tanımı kullanıma sunulan hello endpoint alır ve bağlantıları dinlemeyi başlatır çalışan rolü bir örneği burada verilmiştir.

> [!WARNING]
> Bu kod yalnızca dağıtılan bir hizmet olarak çalışır. Doğrudan bağlantı noktası uç noktaları oluşturma yapılandırma öğeleri Hello Azure işlem öykünücüsü çalıştırırken, hizmet (**InstanceInputEndpoint** öğeleri) göz ardı edilir.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Ağ trafiği kuralları toocontrol rol iletişimi
İç uç noktalar tanımladıktan sonra ağ trafiği kuralları (oluşturduğunuz hello uç noktalarda bağlı olarak) toocontrol rol örnekleri birbirleri ile nasıl iletişim kurabilir ekleyebilirsiniz. Merhaba Aşağıdaki diyagramda rol iletişimi denetlemek için bazı yaygın senaryolar gösterilmektedir:

![Ağ trafik kuralı senaryoları](./media/cloud-services-enable-communication-role-instances/scenarios.png "ağ trafik kuralı senaryoları")

Merhaba aşağıdaki kod örneğinde rol tanımları hello önceki diyagramda gösterildiği hello rolleri için gösterir. Her rol tanımı tanımlanan en az bir dahili uç noktayı içerir:

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
> Kısıtlama rolleri arasındaki iletişim, hem sabit ve bağlantı noktaları otomatik olarak atanan iç uç nokta ile ortaya çıkabilir.
> 
> 

İç uç nokta tanımlandıktan sonra varsayılan olarak, herhangi bir rolün herhangi bir kısıtlamanın olmadığı rol toohello iç uç noktasından iletişimi akabilir. toorestrict iletişim eklemelisiniz bir **NetworkTrafficRules** öğesi toohello **ServiceDefinition** hello hizmet tanımı dosyasındaki öğesi.

### <a name="scenario-1"></a>Senaryo 1
Yalnızca gelen ağ trafiğinin izin **WebRole1** çok**WorkerRole1**.

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

### <a name="scenario-2"></a>Senaryo 2
Yalnızca gelen ağ trafiğine izin verir **WebRole1** çok**WorkerRole1** ve **WorkerRole2**.

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

### <a name="scenario-3"></a>Senaryo 3
Yalnızca gelen ağ trafiğine izin verir **WebRole1** çok**WorkerRole1**, ve **WorkerRole1** çok**WorkerRole2**.

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

### <a name="scenario-4"></a>Senaryo 4
Yalnızca gelen ağ trafiğine izin verir **WebRole1** çok**WorkerRole1**, **WebRole1** çok**WorkerRole2**, ve  **WorkerRole1** çok**WorkerRole2**.

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

Yukarıda kullanılan hello öğeleri için bir XML Şeması Başvurusu bulunabilir [burada](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Sonraki adımlar
Bulut hizmeti hakkında daha fazlasını okuyun hello [modeli](cloud-services-model-and-package.md).

