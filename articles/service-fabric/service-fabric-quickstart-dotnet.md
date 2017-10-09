---
title: "aaaCreate Azure .NET Service Fabric uygulaması | Microsoft Docs"
description: "Bir .NET uygulaması hello Service Fabric hızlı başlangıç örnek kullanarak Azure için oluşturun."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="032df-103">.NET Service Fabric uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="032df-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="032df-104">Azure Service Fabric; ölçeklenebilir ve güvenilir mikro hizmetleri ve kapsayıcıları dağıtmayı ve yönetmeyi sağlayan bir dağıtılmış sistemler platformudur.</span><span class="sxs-lookup"><span data-stu-id="032df-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="032df-105">Bu hızlı başlangıç gösterir nasıl toodeploy, ilk .NET uygulama tooService doku.</span><span class="sxs-lookup"><span data-stu-id="032df-105">This quickstart shows how toodeploy your first .NET application tooService Fabric.</span></span> <span data-ttu-id="032df-106">İşlemi tamamladığınızda, oylama bir durum bilgisi olan bir arka uç hizmetinde hello kümedeki Oylama sonuçlarını kaydettiği ön uç bir ASP.NET Core web uygulamasıyla sahip.</span><span class="sxs-lookup"><span data-stu-id="032df-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span>

![Uygulama ekran görüntüsü](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="032df-108">Bu uygulama hakkında bilgi edineceksiniz kullanarak nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="032df-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="032df-109">.NET ve Service Fabric kullanarak uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="032df-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="032df-110">Bir web ön uç ASP.NET core kullanın</span><span class="sxs-lookup"><span data-stu-id="032df-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="032df-111">Durum bilgisi olan hizmet uygulama verilerini depolamak</span><span class="sxs-lookup"><span data-stu-id="032df-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="032df-112">Uygulamanızı yerel olarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="032df-112">Debug your application locally</span></span>
> * <span data-ttu-id="032df-113">Azure'da Hello uygulama tooa kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="032df-113">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="032df-114">Birden çok düğüm arasında genişleme Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="032df-114">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="032df-115">Uygulama yükseltme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="032df-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="032df-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="032df-116">Prerequisites</span></span>
<span data-ttu-id="032df-117">toocomplete Bu hızlı başlangıç:</span><span class="sxs-lookup"><span data-stu-id="032df-117">toocomplete this quickstart:</span></span>
1. <span data-ttu-id="032df-118">[Visual Studio 2017 yükleme](https://www.visualstudio.com/) hello ile **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="032df-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. [<span data-ttu-id="032df-119">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="032df-119">Install Git</span></span>](https://git-scm.com/)
3. [<span data-ttu-id="032df-120">Merhaba Microsoft Azure Service Fabric SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="032df-120">Install hello Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="032df-121">Komut tooenable Visual Studio toodeploy toohello yerel Service Fabric kümesi aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="032df-121">Run hello following command tooenable Visual Studio toodeploy toohello local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a><span data-ttu-id="032df-122">Merhaba örnek indirme</span><span class="sxs-lookup"><span data-stu-id="032df-122">Download hello sample</span></span>
<span data-ttu-id="032df-123">Bir komut penceresinde komut tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="032df-123">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="032df-124">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="032df-124">Run hello application locally</span></span>
<span data-ttu-id="032df-125">Başlat menüsü hello Hello Visual Studio simgesini sağ tıklatın ve seçin **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="032df-125">Right-click hello Visual Studio icon in hello Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="032df-126">Sipariş tooattach hello hata ayıklayıcı tooyour Hizmetleri'nde, yönetici olarak Visual Studio toorun gerekir.</span><span class="sxs-lookup"><span data-stu-id="032df-126">In order tooattach hello debugger tooyour services, you need toorun Visual Studio as administrator.</span></span>

<span data-ttu-id="032df-127">Açık hello **Voting.sln** kopyaladığınız hello depodan Visual Studio çözümü.</span><span class="sxs-lookup"><span data-stu-id="032df-127">Open hello **Voting.sln** Visual Studio solution from hello repository you cloned.</span></span>

<span data-ttu-id="032df-128">toodeploy Merhaba uygulaması, basın **F5**.</span><span class="sxs-lookup"><span data-stu-id="032df-128">toodeploy hello application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="032df-129">Merhaba ilk kez çalıştırma ve hello uygulama, Visual Studio dağıtmak hata ayıklama için yerel bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="032df-129">hello first time you run and deploy hello application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="032df-130">Bu işlem biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="032df-130">This operation may take some time.</span></span> <span data-ttu-id="032df-131">Merhaba küme oluşturma durumunu hello Visual Studio çıktı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="032df-131">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="032df-132">Merhaba dağıtım tamamlandığında, bir tarayıcı başlatmak ve bu sayfayı açın: `http://localhost:8080` -hello web Merhaba uygulaması ön uç.</span><span class="sxs-lookup"><span data-stu-id="032df-132">When hello deployment is complete, launch a browser and open this page: `http://localhost:8080` - hello web front-end of hello application.</span></span>

![Uygulama ön uç](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="032df-134">Şimdi, oylama seçenekleri kümesi ekleyin ve oy almaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="032df-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="032df-135">Merhaba uygulaması çalıştıran ve ayrı bir veritabanı için hello gerek kalmadan, Service Fabric kümesindeki tüm verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="032df-135">hello application runs and stores all data in your Service Fabric cluster, without hello need for a separate database.</span></span>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="032df-136">Örnek uygulama oylama hello yol</span><span class="sxs-lookup"><span data-stu-id="032df-136">Walk through hello voting sample application</span></span>
<span data-ttu-id="032df-137">Uygulama oylama hello iki hizmetinden oluşur:</span><span class="sxs-lookup"><span data-stu-id="032df-137">hello voting application consists of two services:</span></span>
- <span data-ttu-id="032df-138">Web ön uç hizmeti (VotingWeb) - bir ASP.NET Core web hello web sayfası hizmet ön uç hizmeti ve düzenlemenizi sağlayan web API'leri toocommunicate hello arka uç hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="032df-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="032df-139">Arka uç hizmetine (VotingData)-disk üzerinde bir API toostore hello oy sonuçları güvenilir sözlükte çıkarır kalıcı bir ASP.NET Core web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="032df-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Uygulama diyagramı](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="032df-141">Olaylar, aşağıdaki hello uygulama hello oy oluşur:</span><span class="sxs-lookup"><span data-stu-id="032df-141">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="032df-142">JavaScript hello oy isteği toohello web API hello web ön uç hizmetinde bir HTTP PUT İsteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="032df-142">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="032df-143">Merhaba web ön uç hizmeti proxy toolocate kullanır ve bir HTTP PUT İsteği toohello arka uç hizmeti iletin.</span><span class="sxs-lookup"><span data-stu-id="032df-143">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="032df-144">Merhaba arka uç hizmeti hello gelen isteği alır ve depolar hello hello kümede çoğaltılmış toomultiple düğüm alır ve diskte kalıcı bir güvenilir bir sözlük sonucunda güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="032df-144">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="032df-145">Hiçbir veritabanı gerektiği şekilde tüm hello uygulamanın veri hello kümesinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="032df-145">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="032df-146">Visual Studio'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="032df-146">Debug in Visual Studio</span></span>
<span data-ttu-id="032df-147">Visual Studio uygulamasında hata ayıklama sırasında yerel bir Service Fabric geliştirme küme kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="032df-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="032df-148">Hata ayıklama deneyimini tooyour senaryonuz hello seçeneği tooadjust var.</span><span class="sxs-lookup"><span data-stu-id="032df-148">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="032df-149">Bu uygulamada, veri arka uç hizmetimizi güvenilir sözlüğünü kullanarak depolarız.</span><span class="sxs-lookup"><span data-stu-id="032df-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="032df-150">Merhaba hata ayıklayıcıyı durdurduğunuzda visual Studio hello uygulama varsayılan başına kaldırır.</span><span class="sxs-lookup"><span data-stu-id="032df-150">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="032df-151">Merhaba arka ucun neden hello veri Hello uygulamasını kaldırma hizmet tooalso kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="032df-151">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="032df-152">hata ayıklama oturumları arasında toopersist hello veri hello değiştirebilirsiniz **uygulama hata ayıklama modu** hello bir özellik olarak **oylama** Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="032df-152">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="032df-153">toolook nedir hello kod, aşağıdaki adımları tam hello olur:</span><span class="sxs-lookup"><span data-stu-id="032df-153">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="032df-154">Açık hello **VotesController.cs** dosya ve hello web API'nin bir kesme noktası belirleyerek **Put** yöntemi (satır 47) - hello Visual Studio'da Çözüm Gezgini'nde hello dosyasında arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-154">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="032df-155">Açık hello **VoteDataController.cs** dosya ve bu web API'nin bir kesme noktası belirleyerek **Put** yöntemi (satır 50).</span><span class="sxs-lookup"><span data-stu-id="032df-155">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="032df-156">Toohello tarayıcı geri dönün ve oylama seçeneği tıklatın veya yeni bir oylama seçeneği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="032df-156">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="032df-157">Merhaba hello web ön uç 's API denetleyicisi içinde ilk kesme noktası isabet.</span><span class="sxs-lookup"><span data-stu-id="032df-157">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    - <span data-ttu-id="032df-158">Burada hello JavaScript hello tarayıcıda hello ön uç hizmetinde bir istek toohello web API denetleyicisi gönderir budur.</span><span class="sxs-lookup"><span data-stu-id="032df-158">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Oy ön uç Hizmet Ekle](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="032df-160">Biz arka uç hizmetimizi hello URL toohello ReverseProxy ilk oluşturmak **(1)**.</span><span class="sxs-lookup"><span data-stu-id="032df-160">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="032df-161">Biz hello HTTP PUT İsteği toohello ReverseProxy Gönder sonra **(2)**.</span><span class="sxs-lookup"><span data-stu-id="032df-161">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="032df-162">Son olarak hello hello yanıt hello arka uç hizmetine toohello istemciden döndürürüz **(3)**.</span><span class="sxs-lookup"><span data-stu-id="032df-162">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="032df-163">Tuşuna **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="032df-163">Press **F5** toocontinue</span></span>
    - <span data-ttu-id="032df-164">Artık hello arka uç hizmetinde hello kesme noktası bulunur.</span><span class="sxs-lookup"><span data-stu-id="032df-164">You are now at hello break point in hello back-end service.</span></span>
    
    ![Oy arka uç hizmeti ekleme](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="032df-166">Hello yönteminin ilk satırında hello **(1)** hello kullanıyoruz `StateManager` tooget veya adlı güvenilir bir sözlük ekleme `counts`.</span><span class="sxs-lookup"><span data-stu-id="032df-166">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="032df-167">Kullanarak bu işlem, güvenilir bir sözlükteki değerlerle tüm etkileşimleri gerektiren deyimi **(2)** bu işlem oluşturur.</span><span class="sxs-lookup"><span data-stu-id="032df-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="032df-168">Merhaba işlemde sonra hello hello seçeneğine oy verdiğiniz için hello ilgili anahtarın değerini güncelleştiriyoruz ve yürütme işlemi hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="032df-168">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="032df-169">Merhaba yürüttükten sonra yöntemi döndürür, veri hello sözlükte güncelleştirilir ve hello kümedeki tooother düğümler çoğaltılan hello.</span><span class="sxs-lookup"><span data-stu-id="032df-169">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="032df-170">Merhaba veriler artık güvenli bir şekilde hello kümesinde depolanır ve hello arka uç hizmetine kullanılabilir hello veri yaşamaya tooother düğümler başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="032df-170">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="032df-171">Tuşuna **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="032df-171">Press **F5** toocontinue</span></span>

<span data-ttu-id="032df-172">hata ayıklama oturumunun, basın toostop hello **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="032df-172">toostop hello debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="032df-173">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="032df-173">Deploy hello application tooAzure</span></span>
<span data-ttu-id="032df-174">toodeploy hello uygulama tooa küme azure'da kendi küme ya da kullanım taraf küme toocreate ya da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-174">toodeploy hello application tooa cluster in Azure, you can either choose toocreate your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="032df-175">Parti kümeleri Azure üzerinde barındırılan ve burada herkes uygulamaları dağıtabilir ve hello platform hakkında bilgi edinin hello Service Fabric ekibi tarafından çalıştırılan ücretsiz, sınırlı süre Service Fabric kümeleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="032df-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="032df-176">tooget erişim tooa taraf küme [hello yönergeleri izleyerek](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="032df-176">tooget access tooa Party Cluster, [follow hello instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="032df-177">Kendi kümenizi oluşturma hakkında daha fazla bilgi için bkz. [Azure'da ilk Service Fabric kümenizi oluşturma](service-fabric-get-started-azure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="032df-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="032df-178">Merhaba web ön uç 8080 bağlantı noktasından gelen trafiği için yapılandırılmış toolisten hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="032df-178">hello web front-end service is configured toolisten on port 8080 for incoming traffic.</span></span> <span data-ttu-id="032df-179">Kümenizde bu bağlantı noktasının açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="032df-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="032df-180">Merhaba taraf küme kullanıyorsanız, bu bağlantı noktasının açık olduğundan.</span><span class="sxs-lookup"><span data-stu-id="032df-180">If you are using hello Party Cluster, this port is open.</span></span>
>

### <a name="deploy-hello-application-using-visual-studio"></a><span data-ttu-id="032df-181">Visual Studio kullanarak hello uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="032df-181">Deploy hello application using Visual Studio</span></span>
<span data-ttu-id="032df-182">Merhaba uygulama hazır, Visual Studio'dan doğrudan tooa küme dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-182">Now that hello application is ready, you can deploy it tooa cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="032df-183">Sağ **oylama** içinde Çözüm Gezgini hello ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="032df-183">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="032df-184">Merhaba Yayımla iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="032df-184">hello Publish dialog appears.</span></span>

    ![Yayımla İletişim Kutusu](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="032df-186">Merhaba hello kümede hello bağlantı uç noktasının türünde **bağlantı uç noktasının** alanına gelin ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="032df-186">Type in hello Connection Endpoint of hello cluster in hello **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="032df-187">Merhaba taraf küme kaydolduğunuzda hello bağlantı uç noktasının hello tarayıcıda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="032df-187">When signing up for hello Party Cluster, hello Connection Endpoint is provided in hello browser.</span></span> <span data-ttu-id="032df-188">-Örneğin, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span><span class="sxs-lookup"><span data-stu-id="032df-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="032df-189">Bir tarayıcı hello küme adresi - Örneğin, açıp `http://winh1x87d1d.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="032df-189">Open a browser and type in hello cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="032df-190">Azure'da hello kümede çalışan hello uygulama görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-190">You should now see hello application running in hello cluster in Azure.</span></span>

![Uygulama ön uç](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="032df-192">Bir kümedeki uygulamaları ve hizmetleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="032df-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="032df-193">Service Fabric hizmetleri arasında bir küme tooaccommodate hello yük hello services üzerinde bir değişiklik için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="032df-193">Service Fabric services can easily be scaled across a cluster tooaccommodate for a change in hello load on hello services.</span></span> <span data-ttu-id="032df-194">Bir hizmet hello hello kümede çalışan örneği sayısı değiştirerek ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="032df-194">You scale a service by changing hello number of instances running in hello cluster.</span></span> <span data-ttu-id="032df-195">Hizmetlerinizin ölçeklendirme birkaç yolu vardır, betikleri veya komutları PowerShell veya Service Fabric CLI (sfctl) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="032df-196">Bu örnekte, Service Fabric Explorer kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="032df-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="032df-197">Service Fabric Explorer tüm Service Fabric kümelerinde çalışır ve toohello kümeleri HTTP yönetim bağlantı noktası (19080), örneğin, göz atarak bir tarayıcıdan erişilebilir `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="032df-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing toohello clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="032df-198">tooscale hello web ön uç hizmeti, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="032df-198">tooscale hello web front-end service, do hello following steps:</span></span>

1. <span data-ttu-id="032df-199">Kümenizde Service Fabric Explorer'ı açın. Örneğin: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="032df-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="032df-200">Merhaba üç nokta (üç nokta) sonraki toohello'ı tıklatın **fabric: / oylama/VotingWeb** düğümü treeview hello ve seçin **ölçek hizmet**.</span><span class="sxs-lookup"><span data-stu-id="032df-200">Click on hello ellipsis (three dots) next toohello **fabric:/Voting/VotingWeb** node in hello treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="032df-202">Şimdi tooscale hello hello web ön uç hizmeti örneklerinin sayısını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-202">You can now choose tooscale hello number of instances of hello web front-end service.</span></span>

3. <span data-ttu-id="032df-203">Merhaba numarasını da değiştirmeniz**2** tıklatıp **ölçek hizmet**.</span><span class="sxs-lookup"><span data-stu-id="032df-203">Change hello number too**2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="032df-204">Tıklatın hello üzerinde **fabric: / oylama/VotingWeb** düğümünde hello ağaç görünümü ve (bir GUID ile temsil edilen) hello bölüm düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="032df-204">Click on hello **fabric:/Voting/VotingWeb** node in hello tree-view and expand hello partition node (represented by a GUID).</span></span>

    ![Service Fabric Explorer ölçek hizmeti](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="032df-206">Şimdi iki örneği hello hizmeti var ve hello ağaç görünümünde hello örneklerinde Çalıştır hangi düğümlerin görmek görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-206">You can now see that hello service has two instances, and in hello tree view you see which nodes hello instances run on.</span></span>

<span data-ttu-id="032df-207">Bu basit yönetim görevi tarafından biz hello kaynaklar bizim için ön uç hizmeti tooprocess kullanıcı yükü iki katına.</span><span class="sxs-lookup"><span data-stu-id="032df-207">By this simple management task, we doubled hello resources available for our front-end service tooprocess user load.</span></span> <span data-ttu-id="032df-208">Birden çok örneğini çalıştırın güvenilir bir hizmet toohave gerekmez önemli toounderstand olur.</span><span class="sxs-lookup"><span data-stu-id="032df-208">It's important toounderstand that you do not need multiple instances of a service toohave it run reliably.</span></span> <span data-ttu-id="032df-209">Bir hizmet başarısız olursa, Service Fabric hello kümesinde yeni bir hizmet örneği çalıştıran emin olur.</span><span class="sxs-lookup"><span data-stu-id="032df-209">If a service fails, Service Fabric makes sure a new service instance runs in hello cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="032df-210">Uygulama yükseltme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="032df-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="032df-211">Yeni güncelleştirmeler tooyour Uygulama dağıtırken, Service Fabric hello güncelleştirmeyi güvenli bir yolla yapar.</span><span class="sxs-lookup"><span data-stu-id="032df-211">When deploying new updates tooyour application, Service Fabric rolls out hello update in a safe way.</span></span> <span data-ttu-id="032df-212">Çalışırken hataları gerçekleşeceğini yanı sıra otomatik geri alma yükseltirken kapalı kalma süresi sağlar.</span><span class="sxs-lookup"><span data-stu-id="032df-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="032df-213">tooupgrade Merhaba uygulama, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="032df-213">tooupgrade hello application, do hello following:</span></span>

1. <span data-ttu-id="032df-214">Açık hello **Index.cshtml** dosyasını Visual Studio'da - hello Visual Studio'da Çözüm Gezgini'nde hello dosyasında arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-214">Open hello **Index.cshtml** file in Visual Studio - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="032df-215">Örneğin bazı metin - ekleyerek Hello başlık hello sayfasında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="032df-215">Change hello heading on hello page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="032df-216">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="032df-216">Save hello file.</span></span>
4. <span data-ttu-id="032df-217">Sağ **oylama** içinde Çözüm Gezgini hello ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="032df-217">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="032df-218">Merhaba Yayımla iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="032df-218">hello Publish dialog appears.</span></span>
5. <span data-ttu-id="032df-219">Merhaba tıklatın **bildirim sürüm** düğmesini toochange hello sürümü hello hizmet ve uygulama.</span><span class="sxs-lookup"><span data-stu-id="032df-219">Click hello **Manifest Version** button toochange hello version of hello service and application.</span></span>
6. <span data-ttu-id="032df-220">Değişiklik hello hello sürümü **kod** öğesinin altında **VotingWebPkg** çok "2.0.0" Örneğin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="032df-220">Change hello version of hello **Code** element under **VotingWebPkg** too"2.0.0", for example, and click **Save**.</span></span>

    ![Değişiklik sürüm iletişim](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="032df-222">Merhaba, **Service Fabric uygulaması yayımlama** iletişim kutusu, onay hello yükseltme hello uygulama onay kutusunu ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="032df-222">In hello **Publish Service Fabric Application** dialog, check hello Upgrade hello Application checkbox, and click **Publish**.</span></span>

    ![Yayımlama iletişim kutusu ayarı yükseltme](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="032df-224">Tarayıcınızı açın ve örneğin, bağlantı noktası 19080 - toohello küme adresi Gözat `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="032df-224">Open your browser and browse toohello cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="032df-225">Tıklatın hello üzerinde **uygulamaları** hello ağaç görünümünde düğümünü ve ardından **yükseltme devam eden** hello sağ taraftaki bölmede.</span><span class="sxs-lookup"><span data-stu-id="032df-225">Click on hello **Applications** node in hello tree view, and then **Upgrades in Progress** in hello right-hand pane.</span></span> <span data-ttu-id="032df-226">Her etki alanı sonraki devam etmeden önce toohello sağlıklı olduğundan emin olmanızı nasıl hello yükseltme hello yükseltme etki alanlarında ilerlerken, kümede yapar bakın.</span><span class="sxs-lookup"><span data-stu-id="032df-226">You see how hello upgrade rolls through hello upgrade domains in your cluster, making sure each domain is healthy before proceeding toohello next.</span></span>
    <span data-ttu-id="032df-227">![Service Fabric Explorer görünümünde yükseltme](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="032df-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="032df-228">Service Fabric yükseltmelerinin hello hizmet hello kümedeki her düğümde yükselttikten sonra iki dakika bekleyerek güvenli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="032df-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading hello service on each node in hello cluster.</span></span> <span data-ttu-id="032df-229">Merhaba tüm güncelleştirme tootake yaklaşık sekiz dakika bekler.</span><span class="sxs-lookup"><span data-stu-id="032df-229">Expect hello entire update tootake approximately eight minutes.</span></span>

10. <span data-ttu-id="032df-230">Merhaba yükseltme çalışırken hello uygulamayı kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-230">While hello upgrade is running, you can still use hello application.</span></span> <span data-ttu-id="032df-231">İki örneği hello kümede çalışan hello hizmeti olduğundan, diğerleri hello eski sürümü hala alabilir ancak bazı isteklerinizi Merhaba uygulaması yükseltilmiş sürümünü alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="032df-231">Because you have two instances of hello service running in hello cluster, some of your requests may get an upgraded version of hello application, while others may still get hello old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="032df-232">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="032df-232">Next steps</span></span>
<span data-ttu-id="032df-233">Bu hızlı başlangıçta şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="032df-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="032df-234">.NET ve Service Fabric kullanarak uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="032df-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="032df-235">Bir web ön uç ASP.NET core kullanın</span><span class="sxs-lookup"><span data-stu-id="032df-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="032df-236">Durum bilgisi olan hizmet uygulama verilerini depolamak</span><span class="sxs-lookup"><span data-stu-id="032df-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="032df-237">Uygulamanızı yerel olarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="032df-237">Debug your application locally</span></span>
> * <span data-ttu-id="032df-238">Azure'da Hello uygulama tooa kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="032df-238">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="032df-239">Birden çok düğüm arasında genişleme Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="032df-239">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="032df-240">Uygulama yükseltme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="032df-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="032df-241">Service Fabric ve .NET hakkında daha fazla toolearn Bu öğretici göz alın:</span><span class="sxs-lookup"><span data-stu-id="032df-241">toolearn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="032df-242">Service Fabric üzerinde .NET uygulaması</span><span class="sxs-lookup"><span data-stu-id="032df-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)