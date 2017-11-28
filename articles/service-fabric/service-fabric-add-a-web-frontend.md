---
title: "Bir web ön uç için ASP.NET Core kullanarak Azure Service Fabric uygulamanızı oluşturma | Microsoft Docs"
description: "Web Service Fabric uygulamanızı bir ASP.NET Core proje ve hizmet Remoting aracılığıyla hizmet içi iletişim kullanarak kullanıma sunar."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: b19aaa652f2c15573ded632ca1348e1a6752f080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="163de-103">Web hizmeti ön uç için ASP.NET Core kullanarak uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="163de-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="163de-104">Varsayılan olarak, Azure Service Fabric Hizmetleri Web ortak bir arabirim sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="163de-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="163de-105">HTTP istemcilere, uygulamanın işlevselliğini kullanıma sunmak için bir giriş noktası olarak davranmasına ve tek tek hizmetlerinizi buradan iletişim kurmak için bir web projesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-105">To expose your application's functionality to HTTP clients, you have to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="163de-106">Bu öğreticide, biz ayrılacağı yeri biz de seçmek [Visual Studio'da ilk uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md) öğretici ve ASP.NET Core web hizmetini durum bilgisi olan sayacı hizmetini önüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="163de-106">In this tutorial, we pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of the stateful counter service.</span></span> <span data-ttu-id="163de-107">Zaten yapmadıysanız, geri dönün ve Bu öğreticide ilk adım gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="163de-108">ASP.NET Core için ortamınızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="163de-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="163de-109">Bu öğretici ile birlikte izlemek için Visual Studio 2017 gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-109">You need Visual Studio 2017 to follow along with this tutorial.</span></span> <span data-ttu-id="163de-110">Herhangi bir sürümünü yapın.</span><span class="sxs-lookup"><span data-stu-id="163de-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="163de-111">Visual Studio 2017 yükleyin</span><span class="sxs-lookup"><span data-stu-id="163de-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="163de-112">ASP.NET Core Service Fabric uygulamaları geliştirmek için aşağıdaki iş yüklerini yüklü olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="163de-112">To develop ASP.NET Core Service Fabric applications, you should have the following workloads installed:</span></span>
 - <span data-ttu-id="163de-113">**Azure geliştirme** (altında *Web ve bulut*)</span><span class="sxs-lookup"><span data-stu-id="163de-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="163de-114">**ASP.NET ve web geliştirme** (altında *Web ve bulut*)</span><span class="sxs-lookup"><span data-stu-id="163de-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="163de-115">**.NET core platformlar arası geliştirme** (altında *diğer Toolsets*)</span><span class="sxs-lookup"><span data-stu-id="163de-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="163de-116">Visual Studio 2015 kullanmaya devam ediyorsanız olması gerekiyor ancak .NET Core araçları Visual Studio 2015 için artık, güncelleştirilmekte olan [.NET Core VS 2015 Tooling Önizleme 2](https://www.microsoft.com/net/download/core) yüklü.</span><span class="sxs-lookup"><span data-stu-id="163de-116">The .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="163de-117">Uygulamanız için bir ASP.NET Core Hizmet Ekle</span><span class="sxs-lookup"><span data-stu-id="163de-117">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="163de-118">ASP.NET Core API web ve modern web kullanıcı Arabirimi oluşturmak için kullanabileceğiniz bir basit, platformlar arası web geliştirme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="163de-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> 

<span data-ttu-id="163de-119">Bir ASP.NET Web API projesi mevcut uygulamamız ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="163de-119">Let's add an ASP.NET Web API project to our existing application.</span></span>

1. <span data-ttu-id="163de-120">Çözüm Gezgini'nde sağ **Hizmetleri** uygulama içinde proje ve seçin **Ekle > Yeni yapı hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="163de-120">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Varolan bir uygulamaya yeni bir hizmet ekleme][vs-add-new-service]
2. <span data-ttu-id="163de-122">Üzerinde **bir hizmet oluşturma** sayfasında, **ASP.NET Core** ve bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="163de-122">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![ASP.NET web hizmeti yeni hizmet iletişim kutusunda seçme][vs-new-service-dialog]

3. <span data-ttu-id="163de-124">Sonraki sayfanın bir dizi ASP.NET Core proje şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="163de-124">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="163de-125">Bu hizmet Service Fabric çalışma zamanı ile kaydetmek için ek kod küçük miktarda bir Service Fabric uygulaması dışında bir ASP.NET Core proje oluşturduysanız görür aynı seçenek olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="163de-125">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="163de-126">Bu öğretici için seçin **Web API**.</span><span class="sxs-lookup"><span data-stu-id="163de-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="163de-127">Ancak, tam web uygulamasını oluşturmak için aynı kavramları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163de-127">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![ASP.NET proje türü seçme][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="163de-129">Web API projeniz oluşturulduktan sonra iki hizmet uygulamanızda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="163de-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="163de-130">Uygulamanızı yapılandırmaya devam ederken, daha fazla hizmet tam olarak aynı şekilde ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163de-130">As you continue to build your application, you can add more services in exactly the same way.</span></span> <span data-ttu-id="163de-131">Her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="163de-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="163de-132">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="163de-132">Run the application</span></span>
<span data-ttu-id="163de-133">Biz ne yaptıklarını bir fikir almak için şimdi yeni uygulama dağıtın ve ASP.NET Core Web API şablonu sağlar varsayılan davranışı göz atın.</span><span class="sxs-lookup"><span data-stu-id="163de-133">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="163de-134">Uygulama hata ayıklamak için Visual Studio'da F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="163de-134">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="163de-135">Dağıtım tamamlandığında, Visual Studio ASP.NET Web API hizmetinin kökü tarayıcıya başlatır.</span><span class="sxs-lookup"><span data-stu-id="163de-135">When deployment is complete, Visual Studio launches a browser to the root of the ASP.NET Web API service.</span></span> <span data-ttu-id="163de-136">404 hatası tarayıcıda görmeniz gerekir böylece ASP.NET çekirdek Web API şablon kökü için varsayılan davranış sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="163de-136">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you should see a 404 error in the browser.</span></span>
3. <span data-ttu-id="163de-137">Ekleme `/api/values` tarayıcıda konumuna.</span><span class="sxs-lookup"><span data-stu-id="163de-137">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="163de-138">Bu çağırır `Get` Web API şablonunda ValuesController yöntemi.</span><span class="sxs-lookup"><span data-stu-id="163de-138">This invokes the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="163de-139">Şablon--iki dizeyi içeren bir JSON dizisi tarafından sağlanan varsayılan yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="163de-139">It returns the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![ASP.NET Core Web API şablondan döndürülen varsayılan değerler][browser-aspnet-template-values]
   
    <span data-ttu-id="163de-141">Öğreticide sonuna kadar bu sayfayı durum bilgisi olan hizmetimizi varsayılan dizeler yerine en son sayaç değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="163de-141">By the end of the tutorial, this page will show the most recent counter value from our stateful service instead of the default strings.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="163de-142">Hizmetlere bağlanma</span><span class="sxs-lookup"><span data-stu-id="163de-142">Connect the services</span></span>
<span data-ttu-id="163de-143">Service Fabric reliable services ile nasıl iletişim kuracağını tam esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="163de-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="163de-144">Tek bir uygulama içinde TCP, bir HTTP REST API üzerinden erişilebilen diğer hizmetler ve hala web yuvalarını erişilebilir diğer hizmetler aracılığıyla erişilebilen hizmetler olabilir.</span><span class="sxs-lookup"><span data-stu-id="163de-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="163de-145">Kullanılabilir seçenekler ve söz konusu bileşim arka plan için bkz: [hizmetleriyle iletişim kurmasını](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="163de-145">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="163de-146">Bu öğreticide, kullandığımız [Service Fabric hizmeti Remoting](service-fabric-reliable-services-communication-remoting.md), sağlanan SDK.</span><span class="sxs-lookup"><span data-stu-id="163de-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in the SDK.</span></span>

<span data-ttu-id="163de-147">(Uzaktan yordam çağrısı veya RPC'ler Modellenen) hizmeti Remoting yaklaşım ortak sözleşme hizmeti olarak görev yapması için bir arabirim tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="163de-147">In the Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="163de-148">Ardından, bu arabirim hizmetiyle etkileşim için bir proxy sınıfı oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="163de-148">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-remoting-interface"></a><span data-ttu-id="163de-149">Uzaktan iletişim arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="163de-149">Create the remoting interface</span></span>
<span data-ttu-id="163de-150">Durum bilgisi olan hizmeti ve diğer hizmetler arasında sözleşme olarak davranmak için bu durumda ASP.NET Core project web arabirimi oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="163de-150">Let's start by creating the interface to act as the contract between the stateful service and other services, in this case the ASP.NET Core web project.</span></span> <span data-ttu-id="163de-151">Bu arabirim, kendi sınıf kitaplığı proje oluşturacağız RPC çağrısı, olmak için kullanan tüm hizmetleri tarafından paylaşılan gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-151">This interface must be shared by all services that use it to make RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="163de-152">Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve seçin **Ekle** > **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="163de-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="163de-153">Seçin **Visual C#** girişi seçin ve sol gezinti bölmesindeki **sınıf kitaplığı** şablonu.</span><span class="sxs-lookup"><span data-stu-id="163de-153">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="163de-154">.NET Framework sürümünü ayarlandığından emin olun **4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="163de-154">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![Durum bilgisi olan hizmetiniz için bir arabirim projesi oluşturma][vs-add-class-library-project]

3. <span data-ttu-id="163de-156">Yükleme **Microsoft.ServiceFabric.Services.Remoting** NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="163de-156">Install the **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="163de-157">Arama **Microsoft.ServiceFabric.Services.Remoting** NuGet Paket Yöneticisi ve hizmet Remoting kullanan tüm projeleri için yükleme de dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="163de-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in the NuGet package manager and install it for all projects in the solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="163de-158">Hizmet arabirimi içeren sınıf kitaplığı proje</span><span class="sxs-lookup"><span data-stu-id="163de-158">The Class Library project that contains the service interface</span></span>
   - <span data-ttu-id="163de-159">Durum bilgisi olan hizmet projesi</span><span class="sxs-lookup"><span data-stu-id="163de-159">The Stateful Service project</span></span>
   - <span data-ttu-id="163de-160">ASP.NET Core web hizmeti projesi</span><span class="sxs-lookup"><span data-stu-id="163de-160">The ASP.NET Core web service project</span></span>
   
    ![Hizmetleri NuGet paketi ekleme][vs-services-nuget-package]

4. <span data-ttu-id="163de-162">Sınıf Kitaplığı'nda tek bir yönteme bir arabirim oluşturmak `GetCountAsync`, ve arabirimden genişletmek `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="163de-162">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="163de-163">Uzaktan iletişim arabirimi hizmet Remoting arabirimi olduğunu belirtmek için bu arabirimden türetilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-163">The remoting interface must derive from this interface to indicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="163de-164">Durum bilgisi olan hizmetinizi arabirimini uygulama</span><span class="sxs-lookup"><span data-stu-id="163de-164">Implement the interface in your stateful service</span></span>
<span data-ttu-id="163de-165">Arabirimi tanımlamış olduğunuz, durum bilgisi olan hizmette uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-165">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="163de-166">Durum bilgisi olan hizmetinizi arabirimi içeren sınıf kitaplığı projesine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="163de-166">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![Durum bilgisi olan hizmeti sınıf kitaplığı projesine bir başvuru ekleme][vs-add-class-library-reference]
2. <span data-ttu-id="163de-168">Devraldığı sınıfı bulun `StatefulService`, gibi `MyStatefulService`, bunu uygulamak için genişletebilirsiniz `ICounter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="163de-168">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="163de-169">Şimdi tanımlanan tek bir yöntem uygulamak `ICounter` arabirimi, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="163de-169">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="163de-170">Bir hizmet remoting dinleyici kullanarak durum bilgisi olan hizmet kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="163de-170">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="163de-171">İle `ICounter` uygulanan arabirimi, son adımdır hizmet Remoting iletişim kanalı açmak için.</span><span class="sxs-lookup"><span data-stu-id="163de-171">With the `ICounter` interface implemented, the final step is to open the Service Remoting communication channel.</span></span> <span data-ttu-id="163de-172">Durum bilgisi olan hizmetler için Service Fabric adlı geçersiz kılınabilir bir yöntem sağlar. `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="163de-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="163de-173">Bu yöntemde, hizmetiniz için etkinleştirmek istediğiniz iletişim türüne göre bir veya daha fazla iletişim dinleyicileri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163de-173">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="163de-174">Durum bilgisi olmayan hizmetler için bir iletişim kanalı açmak için eşdeğer yöntemi çağrılır `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="163de-174">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="163de-175">Bu durumda, mevcut Değiştir `CreateServiceReplicaListeners` yöntemi ve örneği sağlayan `ServiceRemotingListener`, istemcilerden aranabilir, RPC bitiş noktası oluşturur `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="163de-175">In this case, we replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="163de-176">`CreateServiceRemotingListener` Genişletme yöntemi `IService` arabirimi kolayca oluşturmanıza olanak sağlayan bir `ServiceRemotingListener` tüm varsayılan ayarlarla.</span><span class="sxs-lookup"><span data-stu-id="163de-176">The `CreateServiceRemotingListener` extension method on the `IService` interface allows you to easily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="163de-177">Bu uzantı yöntemi kullanmak için olduğundan emin olun `Microsoft.ServiceFabric.Services.Remoting.Runtime` içeri aktarılan ad alanı.</span><span class="sxs-lookup"><span data-stu-id="163de-177">To use this extension method, ensure you have the `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="163de-178">Kullanım hizmeti ile etkileşim kurmak için ServiceProxy sınıfı</span><span class="sxs-lookup"><span data-stu-id="163de-178">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="163de-179">Durum bilgisi olan hizmetimizi artık trafiği üzerinden RPC hizmetlerinden almak hazırdır.</span><span class="sxs-lookup"><span data-stu-id="163de-179">Our stateful service is now ready to receive traffic from other services over RPC.</span></span> <span data-ttu-id="163de-180">Bu nedenle tüm kalır ekleme ile ASP.NET web hizmeti ile iletişim kurmak için kodu.</span><span class="sxs-lookup"><span data-stu-id="163de-180">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="163de-181">ASP.NET projenizde içeren sınıf kitaplığına bir başvuru ekleyin `ICounter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="163de-181">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="163de-182">Daha önce eklediğiniz **Microsoft.ServiceFabric.Services.Remoting** ASP.NET projesi için NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="163de-182">Earlier you added the **Microsoft.ServiceFabric.Services.Remoting** NuGet package to the ASP.NET project.</span></span> <span data-ttu-id="163de-183">Bu paket sağlar `ServiceProxy` RPC yapmak için kullanacağınız sınıfı için durum bilgisi olan hizmet çağırır.</span><span class="sxs-lookup"><span data-stu-id="163de-183">This package provides the `ServiceProxy` class which you use to make RPC calls to the stateful service.</span></span> <span data-ttu-id="163de-184">Bu NuGet paketi ASP.NET Core web hizmeti projesi yüklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="163de-184">Ensure this NuGet package is installed in the ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="163de-185">İçinde **denetleyicileri** klasörü, açık `ValuesController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="163de-185">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="163de-186">Unutmayın `Get` yöntemi şu anda yalnızca "değer1" ve "önceki tarayıcıda ne gördüğümüz eşleşen değer2"--sabit kodlanmış bir dize dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="163de-186">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="163de-187">Bu uygulama aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="163de-187">Replace this implementation with the following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="163de-188">Kodun ilk satırı anahtar adrestir.</span><span class="sxs-lookup"><span data-stu-id="163de-188">The first line of code is the key one.</span></span> <span data-ttu-id="163de-189">Durum bilgisi olan hizmet ICounter proxy'sine oluşturmak için iki parça bilgi sağlamanız gerekir: bir bölüm kimliği ve hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="163de-189">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="163de-190">Ölçek durum bilgisi olan hizmetlere durumlarına farklı demet içine oluşturan bir müşteri kimliği veya posta kodu gibi tanımlayan bir anahtara göre bölerek bölümleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163de-190">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="163de-191">Önemsiz uygulamamız durum bilgisi olan hizmet yalnızca bir bölüm sahiptir, böylece anahtar önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="163de-191">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="163de-192">Sağladığınız herhangi bir tuşa aynı bölüme götürür.</span><span class="sxs-lookup"><span data-stu-id="163de-192">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="163de-193">Hizmetleri bölümleme hakkında daha fazla bilgi için bkz: [bölüm Service Fabric Reliable Services nasıl](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="163de-193">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="163de-194">Hizmet adı form doku URI'dir: /&lt;Uygulama_adı&gt;/&lt;servıce_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="163de-194">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="163de-195">Bu iki parça bilgi ile Service Fabric istekleri gönderilmesi gereken makine benzersiz şekilde tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="163de-195">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="163de-196">`ServiceProxy` Sınıfı, durum bilgisi olan hizmet bölüm barındıran makine başarısız olduğu ve başka bir makine yerini alacak yükseltilmelidir durum aynı zamanda sorunsuz bir şekilde işler.</span><span class="sxs-lookup"><span data-stu-id="163de-196">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="163de-197">Bu soyutlama önemli ölçüde daha basit diğer hizmetlerle dağıtılacak istemci kod yazmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="163de-197">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="163de-198">Biz proxy olduktan sonra biz yalnızca çağırma `GetCountAsync` yöntemi ve sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="163de-198">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="163de-199">Yeniden değiştirilmiş uygulamayı çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="163de-199">Press F5 again to run the modified application.</span></span> <span data-ttu-id="163de-200">Olarak daha önce Visual Studio otomatik olarak web projesi kökündeki tarayıcıya başlatır.</span><span class="sxs-lookup"><span data-stu-id="163de-200">As before, Visual Studio automatically launches the browser to the root of the web project.</span></span> <span data-ttu-id="163de-201">"API/değerleri" yolu ekleyin ve döndürülen geçerli sayaç değeri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-201">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![Tarayıcıda görüntülenen durum bilgisi olan bir sayaç değeri][browser-aspnet-counter-value]
   
    <span data-ttu-id="163de-203">Düzenli aralıklarla güncelleştirme sayaç değeri görmek için tarayıcıyı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="163de-203">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="163de-204">Kestrel ve WebListener</span><span class="sxs-lookup"><span data-stu-id="163de-204">Kestrel and WebListener</span></span>

<span data-ttu-id="163de-205">Kestrel bilinen varsayılan ASP.NET Core web sunucusunun [doğrudan Internet trafiğini işlemek için şu anda desteklenmeyen](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="163de-205">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="163de-206">Sonuç olarak, Service Fabric için ASP.NET Core durum bilgisiz hizmet şablonu kullanan [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="163de-206">As a result, the ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="163de-207">Service Fabric Hizmetleri'nde Kestrel ve WebListener hakkında daha fazla bilgi edinmek için lütfen [Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="163de-207">To learn more about Kestrel and WebListener in Service Fabric services, please refer to [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-to-a-reliable-actor-service"></a><span data-ttu-id="163de-208">Bir güvenilir aktör hizmetine bağlanılıyor</span><span class="sxs-lookup"><span data-stu-id="163de-208">Connecting to a Reliable Actor service</span></span>
<span data-ttu-id="163de-209">Bu öğretici bir durum bilgisi olan hizmeti ile iletişim web ön ucu ekleme odaklanır.</span><span class="sxs-lookup"><span data-stu-id="163de-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="163de-210">Ancak, aktörler için anlaşmak için çok benzer bir model izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163de-210">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="163de-211">Bir güvenilir aktör projesi oluşturduğunuzda, Visual Studio, sizin için otomatik olarak bir arabirim projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="163de-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="163de-212">Bu arabirimi gerçekleştiren proxy aktör ile iletişim kurmak için web projesi oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163de-212">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="163de-213">Bir iletişim kanalı otomatik olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="163de-213">The communication channel is provided automatically.</span></span> <span data-ttu-id="163de-214">Oluşturulmasında eşdeğer olan bir şey yapmanız gerekmez şekilde bir `ServiceRemotingListener` Bu öğreticide durum bilgisi olan hizmeti için yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="163de-214">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="163de-215">Web hizmetleri yerel kümenizde nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="163de-215">How web services work on your local cluster</span></span>
<span data-ttu-id="163de-216">Genel olarak, tam olarak aynı Service Fabric uygulamanızı yerel kümenizde dağıtılan çoklu makine bir küme dağıtmak ve beklendiği gibi çalıştığını yüksek oranda emin.</span><span class="sxs-lookup"><span data-stu-id="163de-216">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="163de-217">Yerel kümenizdeki yalnızca tek bir makineye daraltılmış bir beş düğüm yapılandırması olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="163de-217">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="163de-218">Web hizmetlerine gelir ancak olduğunda bir anahtar ayrıntı.</span><span class="sxs-lookup"><span data-stu-id="163de-218">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="163de-219">Azure'da yaptığı gibi bir yük dengeleyicinin arkasına kümenizi bulunur, bu yana yük dengeleyici her makinede web hizmetlerinizi dağıtılan emin olmalısınız yalnızca hepsini-bir kez deneme trafik makinelerde.</span><span class="sxs-lookup"><span data-stu-id="163de-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer simply round-robins traffic across the machines.</span></span> <span data-ttu-id="163de-220">Bunu ayarlayarak yapabilirsiniz `InstanceCount` özel değere "-1" hizmeti için.</span><span class="sxs-lookup"><span data-stu-id="163de-220">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="163de-221">Bunun aksine, bir web hizmeti yerel olarak çalıştırdığınızda, yalnızca bir örneğini emin olmak gerektiğinde hizmeti çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="163de-221">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="163de-222">Aksi takdirde aynı yol ve bağlantı noktası üzerinde dinleme birden çok işlemlerden çakışmaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="163de-222">Otherwise, you run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="163de-223">Sonuç olarak, web hizmeti örnek sayısı "1" yerel dağıtımlar için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="163de-223">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="163de-224">Farklı ortam için farklı değerler yapılandırma konusunda bilgi edinmek için [birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="163de-224">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="163de-225">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="163de-225">Next steps</span></span>
<span data-ttu-id="163de-226">ASP.NET Core uygulamanızla için kümesi sonlandırmak için daha fazla bilgi edinmek için bir web ön sahip olduğunuza [Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) ASP.NET Core Service Fabric ile nasıl çalıştığı bir derinlemesine anlamak için.</span><span class="sxs-lookup"><span data-stu-id="163de-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="163de-227">Ardından, [hizmetleriyle iletişim kurmasını hakkında daha fazla bilgi](service-fabric-connect-and-communicate-with-services.md) tamamı almak için genel olarak nasıl hizmet iletişimi Service Fabric çalışır resim.</span><span class="sxs-lookup"><span data-stu-id="163de-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general to get a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="163de-228">Hizmet iletişimi nasıl çalıştığını, iyi anlamış olmanız sonra [bir küme oluşturmak ve uygulamanızı buluta dağıtmak](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="163de-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application to the cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
