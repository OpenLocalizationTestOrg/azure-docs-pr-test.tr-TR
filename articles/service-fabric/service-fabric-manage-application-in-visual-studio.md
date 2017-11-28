---
title: "Visual Studio uygulamalarınızda yönetme | Microsoft Docs"
description: "Oluşturmak, geliştirmek, paketi, dağıtmak ve Service Fabric uygulamaları ve Hizmetleri hata ayıklamak için Visual Studio'yu kullanın."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="63b40-103">Yazma ve Service Fabric uygulamaları yönetme basitleştirmek için Visual Studio kullanma</span><span class="sxs-lookup"><span data-stu-id="63b40-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="63b40-104">Azure Service Fabric uygulamaları ve Hizmetleri Visual Studio aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63b40-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="63b40-105">Seçtiğiniz sonra [geliştirme ortamınızı ayarlama](service-fabric-get-started.md), Service Fabric uygulamaları oluşturmak, hizmetleri veya paket, kayıt eklemek ve yerel geliştirme kümenizdeki uygulamaları dağıtmak için Visual Studio'yu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63b40-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="63b40-106">Service Fabric uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="63b40-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="63b40-107">Varsayılan olarak, bir uygulama dağıtımı aşağıdaki adımları basit bir işlemde birleştirir:</span><span class="sxs-lookup"><span data-stu-id="63b40-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="63b40-108">Uygulama paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="63b40-108">Creating the application package</span></span>
2. <span data-ttu-id="63b40-109">Uygulama paketi görüntü deposuna karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="63b40-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="63b40-110">Uygulama türünü kaydetme</span><span class="sxs-lookup"><span data-stu-id="63b40-110">Registering the application type</span></span>
4. <span data-ttu-id="63b40-111">Herhangi bir kaldırma uygulama örnekleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="63b40-111">Removing any running application instances</span></span>
5. <span data-ttu-id="63b40-112">Uygulama örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="63b40-112">Creating an application instance</span></span>

<span data-ttu-id="63b40-113">Visual Studio'da tuşuna basarak **F5** uygulamanızı dağıtır ve tüm uygulama örneklerine hata ayıklayıcısını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63b40-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="63b40-114">Kullanabileceğiniz **Ctrl + F5** hata ayıklama veya bir uygulamayı dağıtmak için yerel veya uzak bir küme için yayımlama profili kullanarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63b40-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="63b40-115">Daha fazla bilgi için bkz: [Visual Studio kullanarak uzak bir küme için bir uygulama yayımlamak](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="63b40-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="63b40-116">Uygulama hata ayıklama modu</span><span class="sxs-lookup"><span data-stu-id="63b40-116">Application Debug Mode</span></span>
<span data-ttu-id="63b40-117">Visual Studio sağlamak adlı bir özellik **uygulama hata ayıklama modu**, uygulama dağıtımı hata ayıklama bir parçası olarak işlemek için görsel stüdyoları istediğiniz kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="63b40-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="63b40-118">Uygulama hata ayıklama modu özelliğini ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="63b40-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="63b40-119">Service Fabric uygulaması projenin (*.sfproj) üzerinde kısayol menüsünü seçin **özellikleri** (veya basın **F4** anahtar).</span><span class="sxs-lookup"><span data-stu-id="63b40-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="63b40-120">İçinde **özellikleri** penceresindeki ayarlayın **uygulama hata ayıklama modu** özelliği.</span><span class="sxs-lookup"><span data-stu-id="63b40-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![Uygulama hata ayıklama modu özelliğini ayarlayın][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="63b40-122">Uygulama hata ayıklama modu</span><span class="sxs-lookup"><span data-stu-id="63b40-122">Application Debug Modes</span></span>

1. <span data-ttu-id="63b40-123">**Uygulamayı yenileyin** hızlı bir şekilde değiştirin ve statik web dosyaları ayıklarken düzenlemeyi destekler ve kod hatalarını ayıklamak bu modu sağlar.</span><span class="sxs-lookup"><span data-stu-id="63b40-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="63b40-124">Yerel geliştirme kümenizi ise bu modu yalnızca çalışır [1 düğümü modunu](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="63b40-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="63b40-125">**Uygulamayı kaldırmak** uygulamanın hata ayıklama oturumu sona erdiğinde kaldırılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="63b40-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="63b40-126">**Yükseltme otomatik** uygulama hata ayıklama oturumu sona erdiğinde çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="63b40-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="63b40-127">Sonraki hata ayıklama oturumu dağıtım yükseltme olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="63b40-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="63b40-128">Yükseltme işlemi önceki bir hata ayıklama oturumunda girdiğiniz herhangi bir veriyi korur.</span><span class="sxs-lookup"><span data-stu-id="63b40-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="63b40-129">**Uygulama tutmak** hata ayıklama oturumu sona erdiğinde uygulama kümede çalışan tutar.</span><span class="sxs-lookup"><span data-stu-id="63b40-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="63b40-130">Sonraki hata ayıklama oturumu başlangıcında, uygulama kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="63b40-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="63b40-131">İçin **otomatik yükseltme** veriler Service Fabric uygulama yükseltme özelliklerini uygulayarak korunur.</span><span class="sxs-lookup"><span data-stu-id="63b40-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="63b40-132">Uygulamalar ve gerçek bir ortamda bir yükseltme nasıl yerine getirmeyebilir yükseltme hakkında daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="63b40-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="63b40-133">Service Fabric uygulamanızı bir hizmet Ekle</span><span class="sxs-lookup"><span data-stu-id="63b40-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="63b40-134">Uygulamanızı işlevselliğini genişletmek için yeni hizmetler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63b40-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="63b40-135">Hizmet, uygulama paketinde bulunduğundan emin olun, hizmeti aracılığıyla eklemek **yeni Fabric hizmeti...**  menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="63b40-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Yeni bir Service Fabric hizmeti ekleyin][newservice]

<span data-ttu-id="63b40-137">Uygulamanıza eklemek için Service Fabric proje türü seçin ve hizmet için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="63b40-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="63b40-138">Bkz: [hizmetiniz için bir çerçeve seçme](service-fabric-choose-framework.md) kullanmak için hangi hizmet türü karar vermenize yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="63b40-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Uygulamanıza eklemek için Service Fabric hizmeti proje türü seçin][addserviceproject]

<span data-ttu-id="63b40-140">Yeni hizmet, çözüm ve mevcut uygulama paketi eklenir.</span><span class="sxs-lookup"><span data-stu-id="63b40-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="63b40-141">Hizmet başvuruları ve varsayılan hizmet örneği oluşturulabilir ve başladığı sonraki saat uygulamayı dağıtmak hizmetin neden uygulama bildirimine eklenir.</span><span class="sxs-lookup"><span data-stu-id="63b40-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![Yeni hizmet uygulama bildiriminizi eklenir][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="63b40-143">Service Fabric uygulamanızı paketleme</span><span class="sxs-lookup"><span data-stu-id="63b40-143">Package your Service Fabric application</span></span>
<span data-ttu-id="63b40-144">Bir kümeye uygulama ve Hizmetleri dağıtmak için bir uygulama paketi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63b40-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="63b40-145">Paket uygulama bildirimi, hizmet bildirimlerini ve diğer gerekli dosyaları belirli bir düzende düzenler.</span><span class="sxs-lookup"><span data-stu-id="63b40-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="63b40-146">Visual Studio ayarlayan ve 'pkg' dizini için uygulama projenin klasöründe paketini yönetir.</span><span class="sxs-lookup"><span data-stu-id="63b40-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="63b40-147">Tıklatarak **paket** gelen **uygulama** bağlam menüsü oluşturur veya uygulama paketini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="63b40-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="63b40-148">Uygulamalar ve uygulama türleri bulut Gezgini'ni kullanarak kaldırma</span><span class="sxs-lookup"><span data-stu-id="63b40-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="63b40-149">Temel küme yönetimi işlemleri çalıştırmanızı sağlayan bulut Gezgini'ni kullanarak Visual Studio içinden gerçekleştirebilirsiniz **Görünüm** menüsü.</span><span class="sxs-lookup"><span data-stu-id="63b40-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="63b40-150">Örneğin, uygulamaları silin ve yerel veya uzak kümelerde uygulama türleri sağlamasını.</span><span class="sxs-lookup"><span data-stu-id="63b40-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Bir uygulamayı kaldırma][removeapplication]

> [!TIP]
> <span data-ttu-id="63b40-152">Daha zengin küme yönetim işlevselliği için bkz: [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="63b40-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="63b40-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63b40-153">Next steps</span></span>
* [<span data-ttu-id="63b40-154">Service Fabric uygulama modeli</span><span class="sxs-lookup"><span data-stu-id="63b40-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="63b40-155">Service Fabric uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="63b40-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="63b40-156">Birden çok ortamlar için uygulama parametreleri yönetme</span><span class="sxs-lookup"><span data-stu-id="63b40-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="63b40-157">Service Fabric uygulamanızı hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="63b40-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="63b40-158">Service Fabric Explorer kullanarak kümenizi Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="63b40-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png