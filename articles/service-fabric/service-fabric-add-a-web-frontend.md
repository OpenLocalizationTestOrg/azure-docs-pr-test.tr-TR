---
title: "aaaCreate ASP.NET Core kullanarak Azure Service Fabric uygulamanızı bir web ön uç | Microsoft Docs"
description: "Service Fabric uygulaması toohello web bir ASP.NET Core proje ve hizmet Remoting aracılığıyla hizmet içi iletişim kullanarak kullanıma sunar."
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
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="1a195-103">Web hizmeti ön uç için ASP.NET Core kullanarak uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="1a195-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="1a195-104">Varsayılan olarak, Azure Service Fabric Hizmetleri ortak arabirimi toohello web sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1a195-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="1a195-105">tooexpose uygulamanızın işlevselliği tooHTTP istemciler, bir web tooact giriş noktası olarak proje ve orada tooyour iletişim toocreate sahip tek tek Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="1a195-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="1a195-106">Bu öğreticide, biz ayrılacağı yeri biz hello seçmek [Visual Studio'da ilk uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md) öğretici ve ASP.NET Core web hizmetini hello durum bilgisi olan sayacı hizmetini önüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1a195-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="1a195-107">Zaten yapmadıysanız, geri dönün ve Bu öğreticide ilk adım gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a195-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="1a195-108">ASP.NET Core için ortamınızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1a195-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="1a195-109">Bu öğretici yanı sıra Visual Studio 2017 toofollow gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a195-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="1a195-110">Herhangi bir sürümünü yapın.</span><span class="sxs-lookup"><span data-stu-id="1a195-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="1a195-111">Visual Studio 2017 yükleyin</span><span class="sxs-lookup"><span data-stu-id="1a195-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="1a195-112">toodevelop ASP.NET Core Service Fabric uygulamaları yüklü iş yükleri aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1a195-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="1a195-113">**Azure geliştirme** (altında *Web ve bulut*)</span><span class="sxs-lookup"><span data-stu-id="1a195-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="1a195-114">**ASP.NET ve web geliştirme** (altında *Web ve bulut*)</span><span class="sxs-lookup"><span data-stu-id="1a195-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="1a195-115">**.NET core platformlar arası geliştirme** (altında *diğer Toolsets*)</span><span class="sxs-lookup"><span data-stu-id="1a195-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="1a195-116">Visual Studio 2015 kullanmaya devam ediyorsanız toohave gerekiyor ancak hello .NET Core araçları Visual Studio 2015 için artık, güncelleştirilmekte olan [.NET Core VS 2015 Tooling Önizleme 2](https://www.microsoft.com/net/download/core) yüklü.</span><span class="sxs-lookup"><span data-stu-id="1a195-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="1a195-117">ASP.NET Core hizmet tooyour uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="1a195-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="1a195-118">ASP.NET Core toocreate modern web kullanıcı arabirimini kullanın ve API web bir basit, platformlar arası web geliştirme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="1a195-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="1a195-119">Bir ASP.NET Web API projesi tooour mevcut uygulamayı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="1a195-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="1a195-120">Çözüm Gezgini'nde sağ **Hizmetleri** içinde hello uygulama projesi ve seçin **Ekle > Yeni yapı hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="1a195-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Yeni bir hizmet tooan varolan uygulama ekleme][vs-add-new-service]
2. <span data-ttu-id="1a195-122">Merhaba üzerinde **bir hizmet oluşturma** sayfasında, **ASP.NET Core** ve bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="1a195-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![ASP.NET web hizmeti hello yeni hizmet iletişim kutusunda seçme][vs-new-service-dialog]

3. <span data-ttu-id="1a195-124">Merhaba sonraki sayfaya ASP.NET Core birtakım proje şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a195-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="1a195-125">Bunlar olan Merhaba, aynı Not ASP.NET Core projesinde bir Service Fabric uygulaması dışında bir miktarda ek kod tooregister oluşturduysanız görür seçimler hello hizmeti ile Merhaba Service Fabric çalışma zamanı.</span><span class="sxs-lookup"><span data-stu-id="1a195-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="1a195-126">Bu öğretici için seçin **Web API**.</span><span class="sxs-lookup"><span data-stu-id="1a195-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="1a195-127">Ancak, uygulayabilirsiniz hello aynı kavramları toobuilding tam web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1a195-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![ASP.NET proje türü seçme][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="1a195-129">Web API projeniz oluşturulduktan sonra iki hizmet uygulamanızda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1a195-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="1a195-130">Uygulamanızı toobuild devam ederken, daha fazla hizmet tam olarak hello ekleyebilirsiniz aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="1a195-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="1a195-131">Her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a195-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="1a195-132">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="1a195-132">Run hello application</span></span>
<span data-ttu-id="1a195-133">tooget ne biz, şimdi yaptığınız bir fikir hello yeni uygulama ve ASP.NET Core Web API şablon hello hello varsayılan davranışı göz sağlar Al dağıtın.</span><span class="sxs-lookup"><span data-stu-id="1a195-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="1a195-134">Visual Studio toodebug hello uygulamasında F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="1a195-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="1a195-135">Dağıtım tamamlandığında, Visual Studio tarayıcı toohello kökündeki hello ASP.NET Web API hizmetini başlatır.</span><span class="sxs-lookup"><span data-stu-id="1a195-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="1a195-136">404 hatası hello tarayıcıda görmeniz gerekir böylece hello ASP.NET çekirdek Web API şablon hello kökü için varsayılan davranış sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1a195-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="1a195-137">Ekleme `/api/values` hello tarayıcıda toohello konumu.</span><span class="sxs-lookup"><span data-stu-id="1a195-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="1a195-138">Bu hello çağırır `Get` hello ValuesController hello Web API şablonunda yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1a195-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="1a195-139">Merhaba şablon--iki dizeyi içeren bir JSON dizisi tarafından sağlanan hello varsayılan yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="1a195-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![ASP.NET Core Web API şablondan döndürülen varsayılan değerler][browser-aspnet-template-values]
   
    <span data-ttu-id="1a195-141">Merhaba öğretici Hello sonuna bu sayfayı varsayılan dizeleri hello durum bilgisi olan hizmetimizi hello yerine en son sayaç değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1a195-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="1a195-142">Merhaba Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="1a195-142">Connect hello services</span></span>
<span data-ttu-id="1a195-143">Service Fabric reliable services ile nasıl iletişim kuracağını tam esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a195-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="1a195-144">Tek bir uygulama içinde TCP, bir HTTP REST API üzerinden erişilebilen diğer hizmetler ve hala web yuvalarını erişilebilir diğer hizmetler aracılığıyla erişilebilen hizmetler olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a195-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="1a195-145">Merhaba seçenekleri ve hello bileşim ilgili arka plan için bkz: [hizmetleriyle iletişim kurmasını](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="1a195-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="1a195-146">Bu öğreticide, kullandığımız [Service Fabric hizmeti Remoting](service-fabric-reliable-services-communication-remoting.md), hello SDK'te sağlanan.</span><span class="sxs-lookup"><span data-stu-id="1a195-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="1a195-147">Hello (uzaktan yordam çağrısı veya RPC'ler Modellenen) hizmeti Remoting yaklaşım, hello ortak sözleşme hello hizmeti için bir arabirim tooact tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="1a195-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="1a195-148">Ardından, bu arabirimi toogenerate proxy sınıfı hello hizmetiyle etkileşim için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1a195-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="1a195-149">Merhaba remoting arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a195-149">Create hello remoting interface</span></span>
<span data-ttu-id="1a195-150">Merhaba durum bilgisi olan hizmet ve diğer hizmetleri, bu örneği hello ASP.NET Core web projesi arasında hello sözleşme olarak hello arabirimi tooact oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1a195-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="1a195-151">Bu arabirim, kendi sınıf kitaplığı proje oluşturacağız şekilde toomake RPC çağrısı, kullanan tüm hizmetleri tarafından paylaşılan gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a195-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="1a195-152">Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve seçin **Ekle** > **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="1a195-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="1a195-153">Merhaba seçin **Visual C#** sol gezinti bölmesi ve ardından hello hello girişi **sınıf kitaplığı** şablonu.</span><span class="sxs-lookup"><span data-stu-id="1a195-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="1a195-154">Bu hello .NET Framework sürümü olarak ayarlanmış çok olun**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="1a195-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Durum bilgisi olan hizmetiniz için bir arabirim projesi oluşturma][vs-add-class-library-project]

3. <span data-ttu-id="1a195-156">Merhaba yüklemek **Microsoft.ServiceFabric.Services.Remoting** NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="1a195-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="1a195-157">Arama **Microsoft.ServiceFabric.Services.Remoting** hello NuGet Paket Yöneticisi ve hizmet Remoting kullanan tüm projelerde hello çözümde yükleme de dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="1a195-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="1a195-158">Merhaba hizmet arabirimi içeren hello sınıf kitaplığı proje</span><span class="sxs-lookup"><span data-stu-id="1a195-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="1a195-159">Merhaba durum bilgisi olan hizmet projesi</span><span class="sxs-lookup"><span data-stu-id="1a195-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="1a195-160">Merhaba ASP.NET Core web hizmeti projesi</span><span class="sxs-lookup"><span data-stu-id="1a195-160">hello ASP.NET Core web service project</span></span>
   
    ![Merhaba Hizmetleri NuGet paketi ekleme][vs-services-nuget-package]

4. <span data-ttu-id="1a195-162">Merhaba Sınıf Kitaplığı'nda tek bir yönteme bir arabirim oluşturmak `GetCountAsync`, ve hello arabiriminden genişletmek `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="1a195-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="1a195-163">Hello remoting arabirimi hizmet Remoting arabirimi olduğunu bu arabirimi tooindicate türetilmelidir.</span><span class="sxs-lookup"><span data-stu-id="1a195-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
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

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="1a195-164">Durum bilgisi olan hizmet hello arabirimi uygulama</span><span class="sxs-lookup"><span data-stu-id="1a195-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="1a195-165">Merhaba arabirimi tanımlamış olduğunuz, tooimplement ihtiyacımız hello durum bilgisi olan hizmet içinde.</span><span class="sxs-lookup"><span data-stu-id="1a195-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="1a195-166">Durum bilgisi olan hizmetinizi hello arabirimi içeren bir başvuru toohello sınıf kitaplığı proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1a195-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Bir başvuru toohello sınıf kitaplığı proje hello durum bilgisi olan hizmet ekleme][vs-add-class-library-reference]
2. <span data-ttu-id="1a195-168">Öğesinden devralınan hello sınıfını bulun `StatefulService`, gibi `MyStatefulService`ve tooimplement hello genişletmek `ICounter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="1a195-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="1a195-169">Şimdi hello tanımlanan tek bir yöntem hello uygulamak `ICounter` arabirimi, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="1a195-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
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

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="1a195-170">Bir hizmet remoting dinleyici kullanarak hello durum bilgisi olan hizmet kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="1a195-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="1a195-171">Merhaba ile `ICounter` uygulanan hello son adım arabirimidir tooopen hello hizmet Remoting iletişim kanalı.</span><span class="sxs-lookup"><span data-stu-id="1a195-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="1a195-172">Durum bilgisi olan hizmetler için Service Fabric adlı geçersiz kılınabilir bir yöntem sağlar. `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="1a195-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="1a195-173">Bu yöntemle tooenable hizmetiniz için istediğiniz iletişim hello türüne göre bir veya daha fazla iletişim dinleyicileri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a195-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="1a195-174">bir iletişim kanalı toostateless Hizmetleri açmak için hello eşdeğer yöntemi çağrıldığında `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="1a195-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="1a195-175">Bu durumda, biz hello varolan `CreateServiceReplicaListeners` yöntemi ve örneği sağlayan `ServiceRemotingListener`, istemcilerden aranabilir, RPC bitiş noktası oluşturur `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="1a195-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="1a195-176">Merhaba `CreateServiceRemotingListener` hello üzerinde genişletme yöntemi `IService` arabirimi tooeasily verir oluşturma bir `ServiceRemotingListener` tüm varsayılan ayarlarla.</span><span class="sxs-lookup"><span data-stu-id="1a195-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="1a195-177">toouse bu genişletme yöntemi hello olduğundan emin olun `Microsoft.ServiceFabric.Services.Remoting.Runtime` içeri aktarılan ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1a195-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

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


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="1a195-178">Merhaba hizmeti ile Merhaba ServiceProxy sınıfı toointeract kullanın</span><span class="sxs-lookup"><span data-stu-id="1a195-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="1a195-179">Durum bilgisi olan hizmetimizi şimdi hazır tooreceive diğer hizmetlerden RPC üzerinden trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="1a195-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="1a195-180">Bu nedenle tüm kalır ekleme hello kod toocommunicate onunla hello ASP.NET web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1a195-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="1a195-181">ASP.NET projenizde hello içeren bir başvuru toohello sınıf kitaplığı eklemek `ICounter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="1a195-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="1a195-182">Merhaba daha önce eklediğiniz **Microsoft.ServiceFabric.Services.Remoting** NuGet paketi toohello ASP.NET projesi.</span><span class="sxs-lookup"><span data-stu-id="1a195-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="1a195-183">Bu paket hello sağlar `ServiceProxy` kullanacağınız sınıfı toomake RPC toohello durum bilgisi olan hizmet çağırır.</span><span class="sxs-lookup"><span data-stu-id="1a195-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="1a195-184">Bu NuGet paketi hello ASP.NET Core web hizmeti projesi yüklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1a195-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="1a195-185">Merhaba, **denetleyicileri** klasörü, açık hello `ValuesController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1a195-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="1a195-186">Bu hello Not `Get` yöntemi şu anda yalnızca "değer1" ve "önceki hello tarayıcıda ne gördüğümüz eşleşen değer2"--sabit kodlanmış bir dize dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1a195-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="1a195-187">Bu uygulama, kod aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1a195-187">Replace this implementation with hello following code:</span></span>
   
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
   
    <span data-ttu-id="1a195-188">Kodun ilk satırı Hello hello bir anahtardır.</span><span class="sxs-lookup"><span data-stu-id="1a195-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="1a195-189">toocreate hello ICounter proxy toohello durum bilgisi olan hizmet, tooprovide iki parça bilgi gerekir: bir bölüm kimliği ve hello hello hizmetin adını.</span><span class="sxs-lookup"><span data-stu-id="1a195-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="1a195-190">Kendi durumunun farklı demet içine bir müşteri kimliği veya posta kodu gibi tanımlayan bir anahtara göre bölerek bölümleme tooscale durum bilgisi olan hizmetler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a195-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="1a195-191">Önemsiz uygulamamız hello durum bilgisi olan hizmet yalnızca bir bölüm sahiptir, böylece Hello anahtar önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="1a195-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="1a195-192">Sağladığınız herhangi bir tuşa toohello götürür aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="1a195-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="1a195-193">Hizmetleri, bölümleme hakkında daha fazla toolearn bkz [nasıl toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="1a195-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="1a195-194">Merhaba hizmet adıdır hello form doku URI'sini: /&lt;Uygulama_adı&gt;/&lt;servıce_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="1a195-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="1a195-195">Bu iki parça bilgi ile Service Fabric istekleri gönderilmesi gereken hello makine benzersiz şekilde tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1a195-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="1a195-196">Merhaba `ServiceProxy` sınıfı onun yerine aynı zamanda sorunsuz bir şekilde hello durum bilgisi olan hizmet bölüm barındırdığı hello makine başarısız olduğu ve başka bir makine yükseltilen tootake olmalıdır hello durumu işler.</span><span class="sxs-lookup"><span data-stu-id="1a195-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="1a195-197">Bu soyutlama yazma yapar istemci kodu toodeal önemli ölçüde daha basit diğer hizmetlerle hello.</span><span class="sxs-lookup"><span data-stu-id="1a195-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="1a195-198">Biz hello proxy olduktan sonra biz yalnızca hello çağırma `GetCountAsync` yöntemi ve sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1a195-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="1a195-199">F5 tuşuna basın yeniden toorun hello uygulama değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="1a195-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="1a195-200">Olarak daha önce Visual Studio otomatik olarak hello tarayıcı toohello hello web projesi kökündeki başlatır.</span><span class="sxs-lookup"><span data-stu-id="1a195-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="1a195-201">Merhaba "API/değerleri" yolu ekleyin ve döndürülen hello geçerli sayaç değeri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a195-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![Merhaba tarayıcıda görüntülenen hello durum bilgisi olan bir sayaç değeri][browser-aspnet-counter-value]
   
    <span data-ttu-id="1a195-203">Merhaba tarayıcıyı yenilemek düzenli aralıklarla toosee hello sayaç değeri güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="1a195-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="1a195-204">Kestrel ve WebListener</span><span class="sxs-lookup"><span data-stu-id="1a195-204">Kestrel and WebListener</span></span>

<span data-ttu-id="1a195-205">Merhaba Kestrel bilinen, varsayılan ASP.NET Core web sunucusu olduğundan [doğrudan Internet trafiğini işlemek için şu anda desteklenmeyen](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="1a195-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="1a195-206">Sonuç olarak, hello Service Fabric için ASP.NET Core durum bilgisiz hizmet şablonu kullanan [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="1a195-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="1a195-207">Service Fabric Hizmetleri'ndeki Kestrel ve WebListener hakkında daha fazla toolearn başvurun çok[Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="1a195-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="1a195-208">Tooa güvenilir aktör hizmeti bağlanma</span><span class="sxs-lookup"><span data-stu-id="1a195-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="1a195-209">Bu öğretici bir durum bilgisi olan hizmeti ile iletişim web ön ucu ekleme odaklanır.</span><span class="sxs-lookup"><span data-stu-id="1a195-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="1a195-210">Ancak, çok benzer bir model tootalk tooactors izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a195-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="1a195-211">Bir güvenilir aktör projesi oluşturduğunuzda, Visual Studio, sizin için otomatik olarak bir arabirim projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a195-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="1a195-212">Bu arabirim toogenerate aktör proxy ile Merhaba aktör hello web projesi toocommunicate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a195-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="1a195-213">Merhaba iletişim kanalı otomatik olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1a195-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="1a195-214">Toodo herhangi bir şey gerekmez, olduğundan eşdeğer tooestablishing bir `ServiceRemotingListener` Bu öğreticide hello durum bilgisi olan hizmeti için yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="1a195-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="1a195-215">Web hizmetleri yerel kümenizde nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="1a195-215">How web services work on your local cluster</span></span>
<span data-ttu-id="1a195-216">Genel olarak, tam olarak aynı Service Fabric uygulaması tooa çok makineli, dağıtılan yerel kümenizde küme ve beklendiği gibi çalıştığını yüksek oranda emin hello dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a195-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="1a195-217">Yerel kümenizdeki tooa tek makine yalnızca bir beş düğümlü yapılandırmasını daraltılmış olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="1a195-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="1a195-218">Tooweb Hizmetleri gelir ancak olduğunda bir anahtar ayrıntı.</span><span class="sxs-lookup"><span data-stu-id="1a195-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="1a195-219">Azure'da yaptığı gibi bir yük dengeleyicinin arkasına kümenizi bulunur, web hizmetlerinizi hello yük dengeleyici itibaren her makineye dağıtılan emin olmalısınız yalnızca hepsini-bir kez deneme trafik hello makinelerde.</span><span class="sxs-lookup"><span data-stu-id="1a195-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="1a195-220">Bu ayarı hello tarafından yapabileceğiniz `InstanceCount` hello hizmet toohello özel bir değer için "-"1.</span><span class="sxs-lookup"><span data-stu-id="1a195-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="1a195-221">Bunun aksine, bir web hizmeti yerel olarak çalıştırdığınızda, tooensure gerekir hello hizmet, yalnızca bir örneği çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="1a195-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="1a195-222">Aksi takdirde, çakışmaları hello üzerinde aynı dinleyen birden çok işlemlerini çalıştırmak yolu ve bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1a195-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="1a195-223">Sonuç olarak, hello web hizmeti örnek sayısı çok ayarlanmalıdır yerel dağıtımlar için "1".</span><span class="sxs-lookup"><span data-stu-id="1a195-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="1a195-224">Farklı ortam için farklı değerler tooconfigure nasıl görürüm toolearn [birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="1a195-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a195-225">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a195-225">Next steps</span></span>
<span data-ttu-id="1a195-226">ASP.NET Core uygulamanızla için kümesi sonlandırmak için daha fazla bilgi edinmek için bir web ön sahip olduğunuza [Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) ASP.NET Core Service Fabric ile nasıl çalıştığı bir derinlemesine anlamak için.</span><span class="sxs-lookup"><span data-stu-id="1a195-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="1a195-227">Ardından, [hizmetleriyle iletişim kurmasını hakkında daha fazla bilgi](service-fabric-connect-and-communicate-with-services.md) genel tooget tam bir resim olarak nasıl hizmet iletişimi Service Fabric çalışır.</span><span class="sxs-lookup"><span data-stu-id="1a195-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="1a195-228">Hizmet iletişimi nasıl çalıştığını, iyi anlamış olmanız sonra [bir küme oluşturmak ve uygulama toohello bulut dağıtma](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1a195-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

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
