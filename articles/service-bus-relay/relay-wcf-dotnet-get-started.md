---
title: ".NET Azure geçiş WCF geçişlerine aaaGet Başlarken | Microsoft Docs"
description: "Toouse Azure geçiş WCF farklı konumlarda barındırılan tooconnect iki uygulamaları nasıl geçişleri öğrenin."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="59e0a-103">Nasıl toouse Azure geçiş WCF geçişleri .NET ile</span><span class="sxs-lookup"><span data-stu-id="59e0a-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="59e0a-104">Bu makalede nasıl toouse hello Azure geçiş hizmeti açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="59e0a-105">Hello örnekler C# dilinde yazılmıştır ve Service Bus derlemesine hello bulundurulan uzantıları ile hello Windows Communication Foundation (WCF) API'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="59e0a-106">Hello Azure geçişi hakkında daha fazla bilgi için bkz: [Azure geçişine genel bakış](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="59e0a-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="59e0a-107">WCF geçişi nedir?</span><span class="sxs-lookup"><span data-stu-id="59e0a-107">What is WCF Relay?</span></span>

<span data-ttu-id="59e0a-108">Hello Azure [ *WCF geçiş* ](relay-what-is-it.md) hizmet, hem Azure veri merkezinde hem de kendi şirket içi Kurumsal ortamınızda çalışan karma uygulamalar toobuild sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="59e0a-109">Merhaba geçiş hizmeti kolaylaştıran bu sağlayarak toosecurely tooopen bir güvenlik duvarı bağlantı olması veya gerekliliği olmadan bir kurumsal ağ toohello genel bulut içinde bulunan Windows Communication Foundation (WCF) hizmetlerini kullanıma sunma tooa kurumsal ağ altyapısına müdahale eden değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="59e0a-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![WCF Geçişi Kavramları](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="59e0a-111">Azure geçişi, var olan Kuruluş ortamınızda toohost WCF hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="59e0a-112">Ardından, Azure'da çalışan gelen oturumları ve istekleri toothese WCF hizmetleri toohello geçiş hizmeti için dinleme devredebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59e0a-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="59e0a-113">Bu, Azure, veya toomobile çalışanlara veya extranet iş ortağı ortamlarına içinde çalışan bu hizmetleri tooapplication kodu, tooexpose sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="59e0a-114">Geçiş hizmetlerin ayrıntılı erişebilen toosecurely denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="59e0a-115">Mevcut Kurumsal çözümleri ve hello buluttan yararlanma bunu verilerini ve güçlü ve güvenli bir yöntem tooexpose uygulama işlevselliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="59e0a-116">Bu makalede toouse Azure geçiş toocreate bir WCF web hizmeti nasıl gösterilen iki taraf arasında güvenli bir konuşma uygulayan bir TCP kanal bağlaması kullanılarak anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="59e0a-117">Merhaba Service Bus NuGet paketi alma</span><span class="sxs-lookup"><span data-stu-id="59e0a-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="59e0a-118">Merhaba [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus) hello en kolay yolu tooget hello hizmet veri yolu API'sini ve tooconfigure tüm hello Service Bus bağımlılıklarıyla uygulamanızla olduğu.</span><span class="sxs-lookup"><span data-stu-id="59e0a-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="59e0a-119">tooinstall hello NuGet paketini projenize, hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="59e0a-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="59e0a-120">Çözüm Gezgini'nde, **Başvurular**'a sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="59e0a-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="59e0a-121">"Hizmet veri yolu" ve select hello arama **Microsoft Azure Service Bus** öğesi.</span><span class="sxs-lookup"><span data-stu-id="59e0a-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="59e0a-122">Tıklatın **yükleme** toocomplete hello yükleme sonra Kapat iletişim kutusunda aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="59e0a-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="59e0a-123">Kullanıma ve bir SOAP web hizmetini TCP ile kullanma</span><span class="sxs-lookup"><span data-stu-id="59e0a-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="59e0a-124">var olan WCF SOAP web hizmetini dış tüketim tooexpose, değişiklikleri toohello hizmet bağlamalarında ve adreslerinde olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="59e0a-125">Bu değişiklikleri tooyour yapılandırma dosyası gerektirebilir veya nasıl, ayarladığınız ve WCF hizmetlerinizi yapılandırılmış bağlı olarak kod değişiklikleri gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="59e0a-126">WCF, toohave izin verildiğini unutmayın aynı hizmet üzerinden birden çok ağ uç nokta Merhaba, hello varolan koruyabileceğinizi dış geçiş uç noktaları ekleme çalışırken iç uç noktalar hello aynı erişim süresi.</span><span class="sxs-lookup"><span data-stu-id="59e0a-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="59e0a-127">Bu görevde, basit bir WCF hizmeti oluşturma ve aktarma dinleyici tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59e0a-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="59e0a-128">Bu alıştırma Visual Studio aşina varsayar ve proje oluşturmanın tüm hello ayrıntılarını içermez.</span><span class="sxs-lookup"><span data-stu-id="59e0a-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="59e0a-129">Bunun yerine, hello kodu odaklanır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="59e0a-130">Bu adımları başlamadan önce ortamınızı yordamı tooset aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="59e0a-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="59e0a-131">Visual Studio içinde iki proje, "İstemci" ve "Hizmet" Merhaba çözümünde içeren bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59e0a-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="59e0a-132">Merhaba Service Bus NuGet paketi tooboth projeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59e0a-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="59e0a-133">Bu paket tüm hello gerekli derleme başvurularını tooyour projeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="59e0a-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="59e0a-134">Nasıl toocreate hello hizmeti</span><span class="sxs-lookup"><span data-stu-id="59e0a-134">How toocreate hello service</span></span>
<span data-ttu-id="59e0a-135">İlk olarak hello hizmetin kendisini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59e0a-135">First, create hello service itself.</span></span> <span data-ttu-id="59e0a-136">Tüm WCF hizmetleri en az üç farklı bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="59e0a-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="59e0a-137">Değiştirilen mesajları ve çağrılan toobe hangi işlemleridir açıklayan sözleşme tanımı.</span><span class="sxs-lookup"><span data-stu-id="59e0a-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="59e0a-138">Bu sözleşmenin uygulaması.</span><span class="sxs-lookup"><span data-stu-id="59e0a-138">Implementation of that contract.</span></span>
* <span data-ttu-id="59e0a-139">Merhaba WCF hizmetini barındıran ve birkaç uç noktalarını kullanıma sunar ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="59e0a-140">Bu bölümdeki Hello kod örnekleri bu bileşenlerin her birini adres.</span><span class="sxs-lookup"><span data-stu-id="59e0a-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="59e0a-141">Merhaba sözleşmesini tanımlayan tek bir işlem `AddNumbers`, iki sayı ekleyen ve hello sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="59e0a-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="59e0a-142">Merhaba `IProblemSolverChannel` arabirimi etkinleştirir hello istemci toomore hello Ara sunucu ömrünü kolayca yönetin.</span><span class="sxs-lookup"><span data-stu-id="59e0a-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="59e0a-143">Böyle bir arabirim oluşturmak en iyi uygulama olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="59e0a-144">İyi bir fikir tooput olduğundan bu sözleşme tanımı ayrı bir dosyaya böylece bu dosyayı "İstemci" ve "Hizmet" projenizden başvurabilirsiniz ancak hello kodu her iki projeye de kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59e0a-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="59e0a-145">Merhaba sözleşme mevcutsa, hello uygulaması aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="59e0a-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="59e0a-146">Hizmet ana bilgisayarını programlamayla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59e0a-146">Configure a service host programmatically</span></span>
<span data-ttu-id="59e0a-147">Merhaba sözleşme ve uygulama elverişli olduğunda, şimdi hello hizmeti barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="59e0a-148">Barındırma oluşur içinde bir [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) nesnesi, hangi hello hizmet örneklerini yönetme mvc'deki ve ana hello iletiler için dinleme bitiş noktası.</span><span class="sxs-lookup"><span data-stu-id="59e0a-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="59e0a-149">Merhaba aşağıdaki kodu hello hizmet normal yerel uç ve bir geçiş uç nokta tooillustrate hello görünümü, iç ve dış uç noktaların yan yana ile yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="59e0a-150">Merhaba dizesini değiştirmek *ad alanı* ad alanındaki adla ve *yourKey* hello önceki Kurulum adımında elde hello SAS anahtarıyla.</span><span class="sxs-lookup"><span data-stu-id="59e0a-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="59e0a-151">Merhaba üzerinde iki uç nokta oluşturma Hello örnekte, aynı sözleşme uygulama.</span><span class="sxs-lookup"><span data-stu-id="59e0a-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="59e0a-152">Yerel biridir ve bir Azure geçiş aracılığıyla yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="59e0a-153">Merhaba arasındaki temel farklılıklar hello bağlamaları değil; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) hello yerel için ve [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) hello geçiş uç nokta ve hello adresleri.</span><span class="sxs-lookup"><span data-stu-id="59e0a-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="59e0a-154">Merhaba yerel uç nokta farklı bir bağlantı noktası ile yerel ağ adresine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="59e0a-155">Merhaba geçiş endpoint sahip hello dizesi oluşan bir uç nokta adresi `sb`, ad alanı adı ve hello yolu "solver."</span><span class="sxs-lookup"><span data-stu-id="59e0a-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="59e0a-156">Bu hello URI sonuçları `sb://[serviceNamespace].servicebus.windows.net/solver`, hello Hizmeti uç noktası (geçiş) Service Bus TCP uç noktası olarak tam bir dış DNS adı ile tanımlama.</span><span class="sxs-lookup"><span data-stu-id="59e0a-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="59e0a-157">Merhaba yer tutucuları hello değiştirme hello kodu yerleştirin, `Main` hello işlevinin **hizmet** uygulama, işlevsel bir hizmet olacaktır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="59e0a-158">Merhaba geçiş üzerinde özel olarak, hizmet toolisten istiyorsanız hello yerel uç nokta bildirimini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="59e0a-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="59e0a-159">Merhaba App.config dosyasında bir hizmet ana bilgisayarı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59e0a-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="59e0a-160">Merhaba konak hello App.config dosyasını kullanarak da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59e0a-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="59e0a-161">kod bu durumda barındırma hello hizmet hello sonraki örnekte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="59e0a-162">Merhaba uç nokta tanımları hello App.config dosyasına taşınır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="59e0a-163">Merhaba NuGet paketi, Azure geçiş için gerekli hello yapılandırma uzantıları olan tanımları toohello App.config dosyasının bir aralık zaten eklemiştir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="59e0a-164">Merhaba hello tam örnek, hello önceki kod, denk doğrudan hello ögesinin altında görünmelidir **system.serviceModel** öğesi.</span><span class="sxs-lookup"><span data-stu-id="59e0a-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="59e0a-165">Bu kod örneği, projenizin C# ad alanının **Hizmet** olarak adlandırıldığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="59e0a-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="59e0a-166">Merhaba yer tutucuları, geçiş ad alanı adını ve SAS anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59e0a-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="59e0a-167">Bu değişiklikleri yaptıktan sonra hello hizmeti önce yaptığınız gibi ancak iki dinamik uç noktayla birlikte başlar: biri yerel ve bir hello bulutta dinleyen.</span><span class="sxs-lookup"><span data-stu-id="59e0a-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="59e0a-168">Merhaba istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="59e0a-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="59e0a-169">Programlama ile istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59e0a-169">Configure a client programmatically</span></span>
<span data-ttu-id="59e0a-170">tooconsume hello hizmet kullanan bir WCF istemcisi oluşturmak bir [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="59e0a-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="59e0a-171">Service Bus, SAS kullanılarak uygulanan belirteç tabanlı bir güvenlik modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="59e0a-172">Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) sınıfı, bazı iyi bilinen belirteç sağlayıcılarını döndüren, fabrikada yerleştirilen yöntemleri ile bir güvenlik belirteci sağlayıcısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="59e0a-173">Merhaba aşağıdaki örnek kullanır hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) yöntemi toohandle hello hello uygun SAS belirteci alımını.</span><span class="sxs-lookup"><span data-stu-id="59e0a-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="59e0a-174">Merhaba adı ve anahtarı hello önceki bölümde açıklandığı gibi hello portalından alınan dosyalardır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="59e0a-175">İlk, başvuru veya kopyalama hello `IProblemSolver` istemci projenize hello hizmet kodundan sözleşme.</span><span class="sxs-lookup"><span data-stu-id="59e0a-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="59e0a-176">Merhaba hello kodda yerine `Main` hello istemci, geçiş ad alanı ve SAS anahtarı ile yeniden hello yer tutucu metin değiştirme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="59e0a-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="59e0a-177">Hello hizmet, bunları çalıştırmak ve hello istemci şimdi yapı (Merhaba hizmeti çalıştırın), ve hello istemci hello hizmetini çağırır ve yazdırır **9**.</span><span class="sxs-lookup"><span data-stu-id="59e0a-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="59e0a-178">Merhaba istemci ve sunucu farklı makinelerde ağlarda bile çalıştırabilirsiniz ve hello iletişimi çalışmaya devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="59e0a-179">Merhaba istemci kodu da hello Bulut veya yerel olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59e0a-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="59e0a-180">Merhaba App.config dosyasında istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59e0a-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="59e0a-181">koddan hello nasıl tooconfigure hello istemcisini kullanarak hello App.config dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="59e0a-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="59e0a-182">Merhaba uç nokta tanımları hello App.config dosyasına taşınır.</span><span class="sxs-lookup"><span data-stu-id="59e0a-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="59e0a-183">Merhaba hello kodu daha önce listelenen aynı hello olduğundan, aşağıdaki örnek, doğrudan hello altında görünmelidir `<system.serviceModel>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="59e0a-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="59e0a-184">Burada, önceki gibi hello yer tutucuları geçiş ad alanı ve SAS anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59e0a-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="59e0a-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59e0a-185">Next steps</span></span>
<span data-ttu-id="59e0a-186">Artık Azure geçiş hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="59e0a-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="59e0a-187">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="59e0a-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="59e0a-188">Azure Service Bus mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="59e0a-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="59e0a-189">Service Bus örneklerini indirin [Azure örneklerinden] [ Azure samples] veya hello bkz [Service Bus örneklerine genel bakış][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="59e0a-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
