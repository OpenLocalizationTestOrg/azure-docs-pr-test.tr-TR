---
title: "Kullanmaya başlama Azure geçiş WCF geçişleri .NET ile | Microsoft Docs"
description: "Azure geçiş WCF geçişler farklı konumlarda barındırılan iki uygulamalara bağlanmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 1af1ac78398d65e6a87f0d24d6198f3dfbc82ffd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="3581a-103">Geçişleri .NET ile Azure geçiş WCF kullanma</span><span class="sxs-lookup"><span data-stu-id="3581a-103">How to use Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="3581a-104">Bu makalede, Azure geçişi hizmetini kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="3581a-104">This article describes how to use the Azure Relay service.</span></span> <span data-ttu-id="3581a-105">Bu örnekler, C# dilinde yazılmıştır ve Service Bus derlemesinde bulundurulan uzantıları içeren Windows Communication Foundation (WCF) API'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3581a-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span></span> <span data-ttu-id="3581a-106">Azure geçişi hakkında daha fazla bilgi için bkz: [Azure geçişine genel bakış](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="3581a-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="3581a-107">WCF geçişi nedir?</span><span class="sxs-lookup"><span data-stu-id="3581a-107">What is WCF Relay?</span></span>

<span data-ttu-id="3581a-108">Azure [ *WCF geçiş* ](relay-what-is-it.md) hizmeti, hem Azure veri merkezinde hem de kendi şirket içi Kurumsal ortamınızda çalışan karma uygulamalar oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3581a-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="3581a-109">Geçiş hizmeti bu bir güvenlik duvarı bağlantısını açmanıza veya izinsiz gerekliliği olmadan genel bulutta Kurumsal işletme ağında bulunan Windows Communication Foundation (WCF) hizmetlerini güvenli bir şekilde kullanıma olanak tanıyarak kolaylaştırır. Kurumsal ağ altyapısına yapılan değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="3581a-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span></span>

![WCF Geçişi Kavramları](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="3581a-111">Azure geçiş var olan Kuruluş ortamınızda WCF hizmetlerini barındırmak için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="3581a-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="3581a-112">Ardından gelen devredebilirsiniz oturumlar ve istekler bu WCF hizmetlerine Azure içinde çalışan geçiş hizmetine.</span><span class="sxs-lookup"><span data-stu-id="3581a-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span></span> <span data-ttu-id="3581a-113">Böylece hizmetleri Azure'da çalışan uygulama koduna, mobil çalışanlara veya extranet iş ortağı ortamlarına yönelik olarak kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span></span> <span data-ttu-id="3581a-114">Geçiş güvenli bir şekilde bu hizmetleri hassas düzeyinde kimlerin erişebileceğini denetlemek için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="3581a-114">Relay enables you to securely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="3581a-115">Var olan kuruluş çözümlerinizin verilerini ve uygulama işlevselliğini kullanmanız ve bunlardan bulutta faydalanmanız için güçlü ve güvenli bir yol sunar.</span><span class="sxs-lookup"><span data-stu-id="3581a-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span></span>

<span data-ttu-id="3581a-116">Bu makalede Azure geçişi iki taraf arasında güvenli bir konuşma uygulayan bağlama, TCP kanalı kullanılarak kullanıma sunulan bir WCF web hizmeti oluşturmak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3581a-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="3581a-117">Service Bus NuGet paketi alma</span><span class="sxs-lookup"><span data-stu-id="3581a-117">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="3581a-118">[Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus), Service Bus API'sini almanın ve uygulamanızı tüm Service Bus bağımlılıklarıyla yapılandırmanın en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="3581a-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span> <span data-ttu-id="3581a-119">NuGet paketini projenize yüklemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="3581a-119">To install the NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="3581a-120">Çözüm Gezgini'nde, **Başvurular**'a sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3581a-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="3581a-121">"Service Bus" için arama yapın ve **Microsoft Azure Service Bus** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3581a-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="3581a-122">Yüklemeyi tamamlamak için **Yükle**'ye tıklayın, ardından aşağıdaki iletişim kutusunu kapatın:</span><span class="sxs-lookup"><span data-stu-id="3581a-122">Click **Install** to complete the installation, then close the following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="3581a-123">Kullanıma ve bir SOAP web hizmetini TCP ile kullanma</span><span class="sxs-lookup"><span data-stu-id="3581a-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="3581a-124">Var olan WCF SOAP web hizmetini dışarıdan kullanıma açmak için hizmet bağlamalarında ve adreslerinde değişiklik yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3581a-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span></span> <span data-ttu-id="3581a-125">Bu işlem, WCF hizmetlerinizi nasıl yapılandırdığınıza veya ayarladığınıza bağlı olarak yapılandırma dosyanızda ve kodda değişiklikler yapmanızı gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="3581a-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="3581a-126">WCF aynı anda dış erişim için geçiş uç noktaları eklerken var olan dahili uç noktaları koruyabileceğinizi aynı hizmet üzerinden birden çok ağ uç noktasına sahip olmanızı izin verildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3581a-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span></span>

<span data-ttu-id="3581a-127">Bu görevde, basit bir WCF hizmeti oluşturma ve aktarma dinleyicisi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-127">In this task, you build a simple WCF service and add a relay listener to it.</span></span> <span data-ttu-id="3581a-128">Bu alıştırma Visual Studio'ya aşina olduğunuzu varsayar ve proje oluşturmanın tüm ayrıntılarını içermez.</span><span class="sxs-lookup"><span data-stu-id="3581a-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span></span> <span data-ttu-id="3581a-129">Bunun yerine, kod üzerine odaklanır.</span><span class="sxs-lookup"><span data-stu-id="3581a-129">Instead, it focuses on the code.</span></span>

<span data-ttu-id="3581a-130">Bu adımlarla işe koyulmadan önce ortamınızı oluşturmak için aşağıdaki prosedürü tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="3581a-130">Before starting these steps, complete the following procedure to set up your environment:</span></span>

1. <span data-ttu-id="3581a-131">Visual Studio'da, çözüm içinde "İstemci" ve "Hizmet" olmak üzere iki proje içeren bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3581a-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span></span>
2. <span data-ttu-id="3581a-132">Service Bus NuGet paketini her iki projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3581a-132">Add the Service Bus NuGet package to both projects.</span></span> <span data-ttu-id="3581a-133">Bu paket gerekli olan tüm derleme başvurularını projelerinize ekler.</span><span class="sxs-lookup"><span data-stu-id="3581a-133">This package adds all the necessary assembly references to your projects.</span></span>

### <a name="how-to-create-the-service"></a><span data-ttu-id="3581a-134">Hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="3581a-134">How to create the service</span></span>
<span data-ttu-id="3581a-135">Hizmetin kendisini oluşturmak ilk adımdır.</span><span class="sxs-lookup"><span data-stu-id="3581a-135">First, create the service itself.</span></span> <span data-ttu-id="3581a-136">Tüm WCF hizmetleri en az üç farklı bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="3581a-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="3581a-137">Değiştirilen mesajları ve çağrılan işlemleri açıklayan sözleşme tanımı.</span><span class="sxs-lookup"><span data-stu-id="3581a-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span></span>
* <span data-ttu-id="3581a-138">Bu sözleşmenin uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3581a-138">Implementation of that contract.</span></span>
* <span data-ttu-id="3581a-139">WCF hizmetini barındıran ve birkaç uç noktayı kullanıma sokan ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="3581a-139">Host that hosts the WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="3581a-140">Bu bölümdeki kod örnekleri, bu bileşenlerden tümüne yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="3581a-140">The code examples in this section address each of these components.</span></span>

<span data-ttu-id="3581a-141">Sözleşme, iki sayı ekleyen ve sonuç döndüren tek bir işlemi (`AddNumbers`) açıklar.</span><span class="sxs-lookup"><span data-stu-id="3581a-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span></span> <span data-ttu-id="3581a-142">`IProblemSolverChannel` arabirimi, istemcinin ara sunucu ömrünü kolayca yönetmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3581a-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span></span> <span data-ttu-id="3581a-143">Böyle bir arabirim oluşturmak en iyi uygulama olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3581a-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="3581a-144">Hem "İstemci" hem de "Hizmet" projenizden sözleşme tanımına başvurabilmeniz için bu dosyayı farklı bir dosyaya koymak faydalıdır. Ayrıca, kodu her iki projeye de kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span></span>

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

<span data-ttu-id="3581a-145">Sözleşme mevcutsa, uygulama aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3581a-145">With the contract in place, the implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="3581a-146">Hizmet ana bilgisayarını programlamayla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3581a-146">Configure a service host programmatically</span></span>
<span data-ttu-id="3581a-147">Sözleşme ve uygulama elverişli olduğunda artık hizmeti barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-147">With the contract and implementation in place, you can now host the service.</span></span> <span data-ttu-id="3581a-148">Barındırma işlemi, hizmetin yönetim örneklerinin sorumluluğunu üstlenen ve iletiler için dinleme yapan uç noktalarını barındıran [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) nesnesinde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="3581a-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span></span> <span data-ttu-id="3581a-149">Aşağıdaki kod, normal yerel uç ve görünümü, iç ve dış uç noktaların yan yana göstermek için bir geçiş uç noktası ile hizmetini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="3581a-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="3581a-150">*yourKey* dizesini önceki kurulum adımında elde ettiğiniz SAS anahtarıyla ve *namespace* dizesini de ad alanındaki adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3581a-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span></span>

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

Console.WriteLine("Press ENTER to close");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="3581a-151">Verilen örnekte, aynı sözleşme uygulamasında bulunan iki uç nokta oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="3581a-151">In the example, you create two endpoints that are on the same contract implementation.</span></span> <span data-ttu-id="3581a-152">Yerel biridir ve bir Azure geçiş aracılığıyla yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="3581a-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="3581a-153">Bunlar arasındaki temel farklılıklar bağlamalar; yine de uygun istiyor musunuz? [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) yerel biri için ve [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) geçiş uç nokta ve adresleri.</span><span class="sxs-lookup"><span data-stu-id="3581a-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span></span> <span data-ttu-id="3581a-154">Yerel uç nokta, farklı bir bağlantı noktası içeren yerel ağ adresine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3581a-154">The local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="3581a-155">Geçiş uç noktası dizesi oluşan bir uç nokta adresine sahip `sb`, ad alanı adı ve yolu "solver."</span><span class="sxs-lookup"><span data-stu-id="3581a-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span></span> <span data-ttu-id="3581a-156">Bu URI sonuçları `sb://[serviceNamespace].servicebus.windows.net/solver`, hizmet uç noktası (geçiş) Service Bus TCP uç noktası olarak tam bir dış DNS adı ile tanımlama.</span><span class="sxs-lookup"><span data-stu-id="3581a-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="3581a-157">**Hizmet** uygulamasının `Main` işlevinde yer tutucuları kaldırıp kodları yerleştirirseniz işlevsel bir hizmet elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span></span> <span data-ttu-id="3581a-158">Özel olarak geçiş üzerinde dinlenecek hizmetinizi istiyorsanız yerel uç nokta bildirimini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3581a-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-the-appconfig-file"></a><span data-ttu-id="3581a-159">App.config dosyasında bir hizmet ana bilgisayarı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3581a-159">Configure a service host in the App.config file</span></span>
<span data-ttu-id="3581a-160">App.config dosyasını kullanarak da ana bilgisayarı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-160">You can also configure the host using the App.config file.</span></span> <span data-ttu-id="3581a-161">Bu durumda kullanılan hizmet barındırma kodu bir sonraki örnekte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="3581a-161">The service hosting code in this case appears in the next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER to close");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="3581a-162">Uç nokta tanımları App.config dosyasına taşınır.</span><span class="sxs-lookup"><span data-stu-id="3581a-162">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="3581a-163">NuGet paketi zaten bir dizi tanım Azure geçiş için gerekli yapılandırma uzantıları App.config dosyasına ekledi.</span><span class="sxs-lookup"><span data-stu-id="3581a-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="3581a-164">Önceki kodun birebir eş değeri olan aşağıdaki örnek, doğrudan **system.serviceModel** ögesinin altında görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="3581a-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span></span> <span data-ttu-id="3581a-165">Bu kod örneği, projenizin C# ad alanının **Hizmet** olarak adlandırıldığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="3581a-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="3581a-166">Yer tutucuları, geçiş ad alanı adını ve SAS anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3581a-166">Replace the placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="3581a-167">Bu değişiklikleri yaptıktan sonra, uygulama önceden olduğu gibi ancak biri yerel ve biri bulutta dinleyen olmak üzere iki dinamik uç noktayla birlikte başlar.</span><span class="sxs-lookup"><span data-stu-id="3581a-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span></span>

### <a name="create-the-client"></a><span data-ttu-id="3581a-168">İstemci oluşturma</span><span class="sxs-lookup"><span data-stu-id="3581a-168">Create the client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="3581a-169">Programlama ile istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3581a-169">Configure a client programmatically</span></span>
<span data-ttu-id="3581a-170">Hizmeti kullanmak için [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) nesnesini kullanan bir WCF istemcisi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3581a-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="3581a-171">Service Bus, SAS kullanılarak uygulanan belirteç tabanlı bir güvenlik modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="3581a-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="3581a-172">[TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) sınıfı, bazı iyi bilinen belirteç sağlayıcılarını döndüren, fabrikada yerleştirilen yöntemleri içeren bir güvenlik belirteci sağlayıcısı sunar.</span><span class="sxs-lookup"><span data-stu-id="3581a-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="3581a-173">Aşağıdaki örnek, uygun SAS belirtecini edinmeyi ele alırken [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3581a-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span></span> <span data-ttu-id="3581a-174">Ad ve anahtar, önceki bölümde açıklanan şekilde portaldan alınanlardır.</span><span class="sxs-lookup"><span data-stu-id="3581a-174">The name and key are those obtained from the portal as described in the previous section.</span></span>

<span data-ttu-id="3581a-175">İlk olarak, `IProblemSolver` sözleşmesi koduna hizmetten başvurun veya bu kodu hizmetten alarak istemci projenize kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3581a-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span></span>

<span data-ttu-id="3581a-176">Ardından, kodu değiştirin `Main` yer tutucu metin, geçiş ad alanı ve SAS anahtarı ile yeniden değiştirme istemcinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3581a-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="3581a-177">Artık istemciyi ve hizmeti oluşturup çalıştırabilirsiniz (önce hizmeti çalıştırın) ve istemci hizmeti çağırıp **9** yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3581a-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span></span> <span data-ttu-id="3581a-178">İstemciyi ve sunucuyu farklı makinelerde hatta farklı ağlarda bile çalıştırsanız konuşma yine de çalışır.</span><span class="sxs-lookup"><span data-stu-id="3581a-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span></span> <span data-ttu-id="3581a-179">Ayrıca, istemci kodu bulutta veya yerel olarak da çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="3581a-179">The client code can also run in the cloud or locally.</span></span>

#### <a name="configure-a-client-in-the-appconfig-file"></a><span data-ttu-id="3581a-180">App.config dosyasında istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3581a-180">Configure a client in the App.config file</span></span>
<span data-ttu-id="3581a-181">Aşağıdaki kodda, App.config dosyasını kullanarak istemciyi nasıl yapılandıracağınız gösterilir.</span><span class="sxs-lookup"><span data-stu-id="3581a-181">The following code shows how to configure the client using the App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="3581a-182">Uç nokta tanımları App.config dosyasına taşınır.</span><span class="sxs-lookup"><span data-stu-id="3581a-182">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="3581a-183">Önceden listelenen kodla aynı olan aşağıdaki örnek, doğrudan ögesinin altında görünmelidir `<system.serviceModel>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="3581a-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span></span> <span data-ttu-id="3581a-184">Burada, önceki gibi yer tutucular geçiş ad alanı ve SAS anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3581a-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3581a-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3581a-185">Next steps</span></span>
<span data-ttu-id="3581a-186">Azure geçişinin öğrendiğinize göre daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3581a-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span></span>

* [<span data-ttu-id="3581a-187">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="3581a-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="3581a-188">Azure Service Bus mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="3581a-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="3581a-189">Service Bus örneklerini indirin [Azure örneklerinden] [ Azure samples] veya bkz [Service Bus örneklerine genel bakış][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="3581a-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
