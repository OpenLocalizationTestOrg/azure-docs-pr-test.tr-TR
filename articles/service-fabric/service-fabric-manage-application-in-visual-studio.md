---
title: "aaaManage Visual Studio uygulamalarınızda | Microsoft Docs"
description: "Visual Studio toocreate kullanın, geliştirmek, paket, dağıtmak ve Service Fabric uygulamaları ve Hizmetleri hata ayıklama."
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
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="a6677-103">Visual Studio toosimplify yazma ve Service Fabric uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="a6677-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="a6677-104">Azure Service Fabric uygulamaları ve Hizmetleri Visual Studio aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6677-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="a6677-105">Seçtiğiniz sonra [geliştirme ortamınızı ayarlama](service-fabric-get-started.md), Visual Studio toocreate Service Fabric uygulamaları, hizmetleri veya paket, kayıt eklemeniz ve yerel geliştirme kümenizdeki uygulamaları dağıtma.</span><span class="sxs-lookup"><span data-stu-id="a6677-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="a6677-106">Service Fabric uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="a6677-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="a6677-107">Varsayılan olarak, bir uygulama dağıtımı aşağıdaki adımları basit tek bir işlemle hello birleştirir:</span><span class="sxs-lookup"><span data-stu-id="a6677-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="a6677-108">Merhaba uygulama paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6677-108">Creating hello application package</span></span>
2. <span data-ttu-id="a6677-109">Merhaba uygulama paketi toohello görüntü deposuna karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="a6677-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="a6677-110">Merhaba uygulama türünü kaydetme</span><span class="sxs-lookup"><span data-stu-id="a6677-110">Registering hello application type</span></span>
4. <span data-ttu-id="a6677-111">Herhangi bir kaldırma uygulama örnekleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a6677-111">Removing any running application instances</span></span>
5. <span data-ttu-id="a6677-112">Uygulama örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6677-112">Creating an application instance</span></span>

<span data-ttu-id="a6677-113">Visual Studio'da tuşuna basarak **F5** uygulamanızı dağıtır ve hello hata ayıklayıcı tooall uygulama örnekleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a6677-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="a6677-114">Kullanabileceğiniz **Ctrl + F5** toodeploy uygulamanın hata ayıklama veya olmadan tooa yerel yayımlayarak veya hello kullanarak uzak küme yayımlama profili.</span><span class="sxs-lookup"><span data-stu-id="a6677-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="a6677-115">Daha fazla bilgi için bkz: [Visual Studio kullanarak bir uygulama tooa uzaktan küme yayımlama](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a6677-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="a6677-116">Uygulama hata ayıklama modu</span><span class="sxs-lookup"><span data-stu-id="a6677-116">Application Debug Mode</span></span>
<span data-ttu-id="a6677-117">Visual Studio sağlamak adlı bir özellik **uygulama hata ayıklama modu**, Visual stüdyoları toohandle uygulama dağıtımı hata ayıklama bir parçası olarak nasıl istediğiniz kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="a6677-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="a6677-118">tooset hello uygulama hata ayıklama modu özelliği</span><span class="sxs-lookup"><span data-stu-id="a6677-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="a6677-119">Merhaba Service Fabric uygulaması projenin (*.sfproj) üzerinde kısayol menüsünü seçin **özellikleri** (veya tuşuna hello **F4** anahtar).</span><span class="sxs-lookup"><span data-stu-id="a6677-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="a6677-120">Merhaba, **özellikleri** penceresinde, kümesi hello **uygulama hata ayıklama modu** özelliği.</span><span class="sxs-lookup"><span data-stu-id="a6677-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Uygulama hata ayıklama modu özelliğini ayarlayın][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="a6677-122">Uygulama hata ayıklama modu</span><span class="sxs-lookup"><span data-stu-id="a6677-122">Application Debug Modes</span></span>

1. <span data-ttu-id="a6677-123">**Uygulamayı yenileyin** Bu mod tooquickly değişiklik sağlar ve hata ayıklama sırasında statik web dosyaları düzenleme destekler ve kod hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="a6677-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="a6677-124">Yerel geliştirme kümenizi ise bu modu yalnızca çalışır [1 düğümü modunu](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="a6677-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="a6677-125">**Uygulamayı kaldırmak** nedenler hello uygulama toobe hello hata ayıklama oturumu bittikten sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a6677-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="a6677-126">**Yükseltme otomatik** Merhaba uygulaması hello hata ayıklama oturumu sona erdiğinde toorun devam eder.</span><span class="sxs-lookup"><span data-stu-id="a6677-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="a6677-127">Merhaba sonraki hata ayıklama oturumu hello dağıtım yükseltme olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="a6677-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="a6677-128">Merhaba yükseltme işlemi önceki bir hata ayıklama oturumunda girdiğiniz herhangi bir veriyi korur.</span><span class="sxs-lookup"><span data-stu-id="a6677-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="a6677-129">**Uygulama tutmak** hello zaman hello kümede çalışan hello uygulama tutar hata ayıklama oturumu sona erer.</span><span class="sxs-lookup"><span data-stu-id="a6677-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="a6677-130">Merhaba başlangıcında hello sonraki hata ayıklama oturumu, Merhaba uygulaması kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a6677-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="a6677-131">İçin **otomatik yükseltme** hello uygulama yükseltme özelliklerini Service Fabric uygulayarak veriler korunur.</span><span class="sxs-lookup"><span data-stu-id="a6677-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="a6677-132">Uygulamalar ve gerçek bir ortamda bir yükseltme nasıl yerine getirmeyebilir yükseltme hakkında daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="a6677-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="a6677-133">Hizmet tooyour Service Fabric uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="a6677-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="a6677-134">Yeni hizmetler tooyour uygulama tooextend işlevselliğini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6677-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="a6677-135">Merhaba hizmeti uygulama paketinizi bulunur tooensure eklemek hello hizmeti hello aracılığıyla **yeni Fabric hizmeti...**  menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="a6677-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Yeni bir Service Fabric hizmeti ekleyin][newservice]

<span data-ttu-id="a6677-137">Bir Service Fabric proje türü tooadd tooyour uygulaması'nı seçin ve hello hizmeti için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="a6677-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="a6677-138">Bkz: [hizmetiniz için bir çerçeve seçme](service-fabric-choose-framework.md) hangi hizmet karar toohelp toouse yazın.</span><span class="sxs-lookup"><span data-stu-id="a6677-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Bir Service Fabric hizmeti proje türü tooadd tooyour uygulamasını seçin][addserviceproject]

<span data-ttu-id="a6677-140">Merhaba yeni hizmet tooyour çözümü ve mevcut uygulama paketi eklenir.</span><span class="sxs-lookup"><span data-stu-id="a6677-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="a6677-141">Merhaba hizmeti başvuruları ve varsayılan hizmet örneği eklenen toohello uygulama bildirimi olacaktır, neden hello hizmet toobe oluşturulan ve hello başlattığınızda hello uygulamayı dağıtmak başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="a6677-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![Merhaba yeni hizmet tooyour uygulama bildirimi eklenir][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="a6677-143">Service Fabric uygulamanızı paketleme</span><span class="sxs-lookup"><span data-stu-id="a6677-143">Package your Service Fabric application</span></span>
<span data-ttu-id="a6677-144">toodeploy hello uygulama ve kendi Hizmetleri tooa küme, toocreate bir uygulama paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6677-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="a6677-145">Merhaba paket hello uygulama bildirimi, hizmet bildirimlerini ve diğer gerekli dosyaları belirli bir düzende düzenler.</span><span class="sxs-lookup"><span data-stu-id="a6677-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="a6677-146">Visual Studio ayarlayan ve hello 'pkg' dizini için hello uygulama projenin klasöründe hello paketini yönetir.</span><span class="sxs-lookup"><span data-stu-id="a6677-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="a6677-147">Tıklatarak **paket** hello gelen **uygulama** bağlam menüsü oluşturur veya güncelleştirmeleri hello uygulama paketi.</span><span class="sxs-lookup"><span data-stu-id="a6677-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="a6677-148">Uygulamalar ve uygulama türleri bulut Gezgini'ni kullanarak kaldırma</span><span class="sxs-lookup"><span data-stu-id="a6677-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="a6677-149">Merhaba başlatabilirsiniz bulut Gezgini'ni kullanarak Visual Studio içinden temel küme yönetim işlemlerini gerçekleştirebilirsiniz **Görünüm** menüsü.</span><span class="sxs-lookup"><span data-stu-id="a6677-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="a6677-150">Örneğin, uygulamaları silin ve yerel veya uzak kümelerde uygulama türleri sağlamasını.</span><span class="sxs-lookup"><span data-stu-id="a6677-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Bir uygulamayı kaldırma][removeapplication]

> [!TIP]
> <span data-ttu-id="a6677-152">Daha zengin küme yönetim işlevselliği için bkz: [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a6677-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="a6677-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6677-153">Next steps</span></span>
* [<span data-ttu-id="a6677-154">Service Fabric uygulama modeli</span><span class="sxs-lookup"><span data-stu-id="a6677-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="a6677-155">Service Fabric uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="a6677-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="a6677-156">Birden çok ortamlar için uygulama parametreleri yönetme</span><span class="sxs-lookup"><span data-stu-id="a6677-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="a6677-157">Service Fabric uygulamanızı hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a6677-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="a6677-158">Service Fabric Explorer kullanarak kümenizi Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="a6677-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png