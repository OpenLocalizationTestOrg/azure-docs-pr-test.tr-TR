---
title: "Azure Service Fabric uygulaması bir taraf kümeye dağıtma | Microsoft Docs"
description: "Bir uygulamayı bir taraf kümesine dağıtmayı öğrenin."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 6624d683edb548a65d07ab4012c599faaf940ed0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-to-a-party-cluster-in-azure"></a><span data-ttu-id="8bb52-103">Azure taraf kümede bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="8bb52-103">Deploy an application to a Party Cluster in Azure</span></span>
<span data-ttu-id="8bb52-104">Bu öğretici iki serinin bir parçasıdır ve Azure taraf kümede Azure Service Fabric uygulama dağıtma gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-104">This tutorial is part two of a series and shows you how to deploy an Azure Service Fabric application to a Party Cluster in Azure.</span></span>

<span data-ttu-id="8bb52-105">Bölümünde öğretici dizisinin iki bilgi nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="8bb52-105">In part two of the tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8bb52-106">Visual Studio kullanarak uzak bir küme bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="8bb52-106">Deploy an application to a remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="8bb52-107">Bir uygulama Service Fabric Explorer kullanarak kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="8bb52-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="8bb52-108">Bu öğretici serisinde öğrenin nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="8bb52-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="8bb52-109">Bir .NET Service Fabric uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bb52-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="8bb52-110">Uzak bir küme için uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="8bb52-110">Deploy the application to a remote cluster</span></span>
> * [<span data-ttu-id="8bb52-111">CI/CD Visual Studio Team Services kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8bb52-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="8bb52-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8bb52-112">Prerequisites</span></span>
<span data-ttu-id="8bb52-113">Bu öğreticiye başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="8bb52-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="8bb52-114">Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="8bb52-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="8bb52-115">[Visual Studio 2017 yükleme](https://www.visualstudio.com/) yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="8bb52-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="8bb52-116">Service Fabric SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="8bb52-116">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-the-voting-sample-application"></a><span data-ttu-id="8bb52-117">Oylama örnek uygulamayı indirin</span><span class="sxs-lookup"><span data-stu-id="8bb52-117">Download the Voting sample application</span></span>
<span data-ttu-id="8bb52-118">Oylama örnek uygulama yapı içinde değil, [Bu öğretici seri birini Kısım](service-fabric-tutorial-create-dotnet-app.md), yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bb52-118">If you did not build the Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="8bb52-119">Bir komut penceresinde örnek uygulama depoyu yerel makinenize kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8bb52-119">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="8bb52-120">Taraf küme ayarlama</span><span class="sxs-lookup"><span data-stu-id="8bb52-120">Set up a Party Cluster</span></span>
<span data-ttu-id="8bb52-121">Grup kümeleri, Azure üzerinde barındırılan ve Service Fabric ekibi tarafından sunulan ücretsiz, sınırlı süreli Service Fabric kümeleridir. Bu kümelerde herkes uygulama dağıtabilir ve platform hakkında bilgi edinebilir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by the Service Fabric team where anyone can deploy applications and learn about the platform.</span></span> <span data-ttu-id="8bb52-122">Ücretsiz!</span><span class="sxs-lookup"><span data-stu-id="8bb52-122">For free!</span></span>

<span data-ttu-id="8bb52-123">Bir taraf kümesine erişmek için bu siteye göz atın: http://aka.ms/tryservicefabric ve bir küme erişmek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8bb52-123">To get access to a Party Cluster, browse to this site: http://aka.ms/tryservicefabric and follow the instructions to get access to a cluster.</span></span> <span data-ttu-id="8bb52-124">Bir taraf kümesine erişmek için bir Facebook veya GitHub hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-124">You need a Facebook or GitHub account to get access to a Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8bb52-125">Parti kümeleri sağlanmaz, bu nedenle uygulamalarınız ve bunları put herhangi bir veri başkalarına görünür olabilir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-125">Party clusters are not secured, so your applications and any data you put in them may be visible to others.</span></span> <span data-ttu-id="8bb52-126">Başkalarının görmesini istemiyorsanız herhangi bir şey dağıtmazsınız.</span><span class="sxs-lookup"><span data-stu-id="8bb52-126">Don't deploy anything you don't want others to see.</span></span> <span data-ttu-id="8bb52-127">Tüm Ayrıntılar için kullanım koşullarını üzerinden okuduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8bb52-127">Be sure to read over our Terms of Use for all the details.</span></span>

## <a name="configure-the-listening-port"></a><span data-ttu-id="8bb52-128">Dinleme bağlantı noktasını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8bb52-128">Configure the listening port</span></span>
<span data-ttu-id="8bb52-129">VotingWeb ön uç hizmeti oluşturulduğunda, Visual Studio bir bağlantı noktası üzerinde dinleme hizmeti için rastgele seçer.</span><span class="sxs-lookup"><span data-stu-id="8bb52-129">When the VotingWeb front-end service is created, Visual Studio randomly selects a port for the service to listen on.</span></span>  <span data-ttu-id="8bb52-130">VotingWeb hizmeti bu uygulama için ön uç gibi davranır ve dış trafiği kabul eder, sağlandığından hizmet sabit bir bağlayabilir ve bağlantı noktası iyi biliyor.</span><span class="sxs-lookup"><span data-stu-id="8bb52-130">The VotingWeb service acts as the front-end for this application and accepts external traffic, so let's bind that service to a fixed and well-know port.</span></span> <span data-ttu-id="8bb52-131">Çözüm Gezgini'nde açık *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="8bb52-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="8bb52-132">Bul **Endpoint** kaynak **kaynakları** bölümünde ve değiştirme **bağlantı noktası** 80 değeri.</span><span class="sxs-lookup"><span data-stu-id="8bb52-132">Find the **Endpoint** resource in the **Resources** section and change the **Port** value to 80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="8bb52-133">Ayrıca 'F5' kullanarak hata ayıklamasını yaparken doğru bağlantı noktasına bir web tarayıcısı açar şekilde oylama Proje uygulama URL'si özelliği değeri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8bb52-133">Also update the Application URL property value in the Voting project so a web browser opens to the correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="8bb52-134">Çözüm Gezgini'nde seçin **oylama** proje ve güncelleştirme **uygulama URL'si** özelliği.</span><span class="sxs-lookup"><span data-stu-id="8bb52-134">In Solution Explorer, select the **Voting** project and update the **Application URL** property.</span></span>

![Uygulama URL'si](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-the-app-to-the-azure"></a><span data-ttu-id="8bb52-136">Uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="8bb52-136">Deploy the app to the Azure</span></span>
<span data-ttu-id="8bb52-137">Uygulama hazır, Visual Studio'dan doğrudan taraf kümeye dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bb52-137">Now that the application is ready, you can deploy it to the Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="8bb52-138">Sağ **oylama** Çözüm Gezgini'nde ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="8bb52-138">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span>

    ![Yayımla İletişim Kutusu](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="8bb52-140">Bağlantı uç noktasının türünde taraf kümede **bağlantı uç noktasının** alanına gelin ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="8bb52-140">Type in the Connection Endpoint of the Party Cluster in the **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="8bb52-141">Yayımla tamamlandıktan sonra uygulamayı bir tarayıcı aracılığıyla bir istek göndermek görebilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-141">Once the publish has finished, you should be able to send a request to the application via a browser.</span></span>

3. <span data-ttu-id="8bb52-142">Küme adresi (bağlantı uç noktasının bağlantı noktası bilgilerini - örneğin, win1kw5649s.westus.cloudapp.azure.com olmadan) açın, tercih edilen tarayıcı ve yazın.</span><span class="sxs-lookup"><span data-stu-id="8bb52-142">Open you preferred browser and type in the cluster address (the connection endpoint without the port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="8bb52-143">Uygulamayı yerel olarak çalıştırırken gördüğünüz gibi şimdi aynı sonucu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-143">You should now see the same result as you saw when running the application locally.</span></span>

    ![Küme API yanıtından](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-the-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="8bb52-145">Uygulama Service Fabric Explorer kullanarak kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="8bb52-145">Remove the application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="8bb52-146">Service Fabric Explorer keşfedin ve Service Fabric kümesi uygulamaları yönetmek için bir grafik kullanıcı arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="8bb52-146">Service Fabric Explorer is a graphical user interface to explore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="8bb52-147">Uygulamayı taraf kümeden kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="8bb52-147">To remove the application from the Party Cluster:</span></span>

1. <span data-ttu-id="8bb52-148">Taraf küme kaydolma sayfası tarafından sağlanan bağlantıyı kullanarak Service Fabric Explorer gidin.</span><span class="sxs-lookup"><span data-stu-id="8bb52-148">Browse to the Service Fabric Explorer, using the link provided by the Party Cluster sign-up page.</span></span> <span data-ttu-id="8bb52-149">Örneğin, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="8bb52-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="8bb52-150">Service Fabric Gezgini'ne gidin **fabric://Voting** sol taraftaki treeview düğümüne.</span><span class="sxs-lookup"><span data-stu-id="8bb52-150">In Service Fabric Explorer, navigate to the **fabric://Voting** node in the treeview on the left-hand side.</span></span>

3. <span data-ttu-id="8bb52-151">' I tıklatın **eylem** düğmesini sağ **Essentials** bölmesinde ve **uygulama Sil**.</span><span class="sxs-lookup"><span data-stu-id="8bb52-151">Click the **Action** button in the right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="8bb52-152">Kümede çalışan uygulamamız örneğini kaldırır Uygulama örneğinin silmeden onaylayın.</span><span class="sxs-lookup"><span data-stu-id="8bb52-152">Confirm deleting the application instance, which removes the instance of our application running in the cluster.</span></span>

![Service Fabric Explorer'da uygulama silme](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-the-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="8bb52-154">Uygulama türü Service Fabric Explorer kullanarak kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="8bb52-154">Remove the application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="8bb52-155">Uygulamaları, birden çok örnekleri ve küme içinde çalışan uygulama sürümlerini olanak tanıyan bir Service Fabric kümesi uygulama türü olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8bb52-155">Applications are deployed as application types in a Service Fabric cluster, which enables you to have multiple instances and versions of the application running within the cluster.</span></span> <span data-ttu-id="8bb52-156">Uygulamamız çalışan örneği kaldırdıktan sonra biz temizleme dağıtım işlemini tamamlamak için türü de kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bb52-156">After having removed the running instance of our application, we can also remove the type, to complete the cleanup of the deployment.</span></span>

<span data-ttu-id="8bb52-157">Service Fabric uygulaması modelleri hakkında daha fazla bilgi için bkz: [Service Fabric uygulamada Model](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="8bb52-157">For more information about the application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="8bb52-158">Gidin **VotingType** treeview düğümüne.</span><span class="sxs-lookup"><span data-stu-id="8bb52-158">Navigate to the **VotingType** node in the treeview.</span></span>

2. <span data-ttu-id="8bb52-159">' I tıklatın **eylem** düğmesini sağ **Essentials** bölmesinde ve **sağlamayı kaldırma türü**.</span><span class="sxs-lookup"><span data-stu-id="8bb52-159">Click the **Action** button in the right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="8bb52-160">Uygulama türü sağlamanın kaldırılması onaylayın.</span><span class="sxs-lookup"><span data-stu-id="8bb52-160">Confirm unprovisioning the application type.</span></span>

![Service Fabric Explorer'da uygulama türü sağlama](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="8bb52-162">Bu öğreticiyi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="8bb52-162">This concludes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bb52-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8bb52-163">Next steps</span></span>
<span data-ttu-id="8bb52-164">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="8bb52-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8bb52-165">Visual Studio kullanarak uzak bir küme bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="8bb52-165">Deploy an application to a remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="8bb52-166">Bir uygulama Service Fabric Explorer kullanarak kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="8bb52-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="8bb52-167">Sonraki öğretici ilerleyin:</span><span class="sxs-lookup"><span data-stu-id="8bb52-167">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8bb52-168">Visual Studio Team Services kullanarak sürekli tümleştirme kurup</span><span class="sxs-lookup"><span data-stu-id="8bb52-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)