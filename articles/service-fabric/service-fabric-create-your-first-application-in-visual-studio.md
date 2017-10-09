---
title: "C# ile Azure Service Fabric güvenilir hizmet aaaCreate"
description: "Visual Studio ile, Azure Service Fabric üzerinde derlenmiş bir Güvenilir Hizmet uygulaması oluşturun, dağıtım ve hatalarını ayıklayın."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="3db96-103">İlk C# Service Fabric durum bilgisi olan reliable services uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3db96-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="3db96-104">Bilgi nasıl toodeploy ilk Service Fabric uygulamanızı .NET Windows için yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="3db96-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="3db96-105">Tamamladığınızda, güvenilir hizmet uygulamasıyla çalışan bir yerel kümeniz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3db96-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3db96-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3db96-106">Prerequisites</span></span>

<span data-ttu-id="3db96-107">Başlamadan önce [geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started.md) emin olun.</span><span class="sxs-lookup"><span data-stu-id="3db96-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="3db96-108">Bu, hello Service Fabric SDK ve Visual Studio 2017 veya 2015 yüklenmesini içerir.</span><span class="sxs-lookup"><span data-stu-id="3db96-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="3db96-109">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3db96-109">Create hello application</span></span>

<span data-ttu-id="3db96-110">Visual Studio'yu **yönetici** olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="3db96-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="3db96-111">`CTRL`+`SHIFT`+`N` ile bir proje oluşturun</span><span class="sxs-lookup"><span data-stu-id="3db96-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="3db96-112">Merhaba, **yeni proje** iletişim kutusunda, seçin **bulut > Service Fabric uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="3db96-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="3db96-113">Ad Merhaba uygulaması **MyApplication** ve basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3db96-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Visual Studio'da yeni proje iletişim kutusu][1]

<span data-ttu-id="3db96-115">Service Fabric uygulaması herhangi bir türde hello sonraki iletişim kutusundan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3db96-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="3db96-116">Bu Hızlı Başlangıç için **Durum Bilgisi Olan Hizmet**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="3db96-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="3db96-117">Ad hello hizmeti **Mystatefulservice'ten** ve basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3db96-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Visual Studio'da yeni hizmet iletişim kutusu][2]


<span data-ttu-id="3db96-119">Visual Studio hello uygulama projesi ve hello durum bilgisi olan hizmet projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3db96-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Durum bilgisi olan hizmeti içeren uygulama oluşturulduktan sonra Çözüm Gezgini][3]

<span data-ttu-id="3db96-121">Merhaba uygulama projesi (**MyApplication**) herhangi bir kod doğrudan içermiyor.</span><span class="sxs-lookup"><span data-stu-id="3db96-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="3db96-122">Bunun yerine, bir dizi hizmet projesine başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="3db96-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="3db96-123">Ayrıca, bunlardan farklı olarak üç tür içerik daha barındırır:</span><span class="sxs-lookup"><span data-stu-id="3db96-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="3db96-124">**Yayımlama profilleri**</span><span class="sxs-lookup"><span data-stu-id="3db96-124">**Publish profiles**</span></span>  
<span data-ttu-id="3db96-125">Toodifferent ortamları dağıtmak için profiller.</span><span class="sxs-lookup"><span data-stu-id="3db96-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="3db96-126">**Betikler**</span><span class="sxs-lookup"><span data-stu-id="3db96-126">**Scripts**</span></span>  
<span data-ttu-id="3db96-127">Uygulamanızı dağıtmak/yükseltmek için PowerShell betiği.</span><span class="sxs-lookup"><span data-stu-id="3db96-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="3db96-128">**Uygulama tanımı**</span><span class="sxs-lookup"><span data-stu-id="3db96-128">**Application definition**</span></span>  
<span data-ttu-id="3db96-129">Merhaba ApplicationManifest.xml dosyası altında içerir *ApplicationPackageRoot* uygulamanızın birleşim açıklar.</span><span class="sxs-lookup"><span data-stu-id="3db96-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="3db96-130">İlişkili uygulama parametreleri dosyalarını olan altında *ApplicationParameters*, hangi kullanılan toospecify ortama özel parametreler olabilir.</span><span class="sxs-lookup"><span data-stu-id="3db96-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="3db96-131">Yayımlama profili dağıtım tooa sırasında belirli bir ortamın hello belirtilen bir uygulama parametre dosyası ilişkili visual Studio seçer.</span><span class="sxs-lookup"><span data-stu-id="3db96-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="3db96-132">Merhaba hizmet projesi Merhaba içeriğine genel bakış için bkz: [Reliable Services ile çalışmaya başlama](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="3db96-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="3db96-133">Dağıtma ve hello uygulamanızın hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="3db96-133">Deploy and debug hello application</span></span>

<span data-ttu-id="3db96-134">Artık bir uygulamanız olduğuna göre uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3db96-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="3db96-135">Visual Studio'da basın `F5` hata ayıklama için toodeploy Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3db96-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="3db96-136">Merhaba ilk kez çalıştırma ve yerel olarak hello uygulamayı Visual Studio dağıtmak hata ayıklama için yerel bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3db96-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="3db96-137">Bu işlem biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="3db96-137">This may take some time.</span></span> <span data-ttu-id="3db96-138">Merhaba küme oluşturma durumunu hello Visual Studio çıktı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3db96-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="3db96-139">Merhaba küme hazır olduğunda, uygulamadan hello SDK ile dahil hello yerel küme sistemi Tepsisi Yöneticisi bir bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="3db96-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Yerel küme sistemi tepsisi bildirimi][4]

<span data-ttu-id="3db96-141">Bir kez hello uygulama başladığında Visual Studio otomatik olarak hello getirir **Tanılama Olay Görüntüleyicisi'ni**, burada, Hizmetleri'nden izleme çıktısını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3db96-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Tanılama olayları görüntüleyicisi][5]

<span data-ttu-id="3db96-143">Merhaba kullandık durum bilgisi olan hizmet şablonu yalnızca bir sayaç değeri hello artırma gösterir `RunAsync` yöntemi **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="3db96-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="3db96-144">Merhaba olayları toosee birini hello düğümü hello kod çalıştığı dahil olmak üzere daha fazla ayrıntı genişletin.</span><span class="sxs-lookup"><span data-stu-id="3db96-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="3db96-145">Bu durumda, \_Node\_2 genişletilir ancak makinenize göre değişiklik gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="3db96-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Tanılama olayları görüntüleyicisi ayrıntıları][6]

<span data-ttu-id="3db96-147">Merhaba yerel küme tek bir makinede barındırılan beş düğüm içerir.</span><span class="sxs-lookup"><span data-stu-id="3db96-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="3db96-148">Üretim ortamında, her düğüm ayrı fiziksel veya sanal makinelerde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="3db96-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="3db96-149">Visual Studio hello uygulanması sırasında makine toosimulate hello kaybı hata ayıklayıcı hello aynı saat, hello yerel kümede hello düğümlerinden biri aşağı atalım.</span><span class="sxs-lookup"><span data-stu-id="3db96-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="3db96-150">Merhaba, **Çözüm Gezgini** penceresi açık **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="3db96-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="3db96-151">Hello bulur `RunAsync` yöntemi ve hello yönteminin hello ilk satırında bir kesme noktası ayarlama.</span><span class="sxs-lookup"><span data-stu-id="3db96-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Durum bilgisi olan hizmetin RunAsync yönteminde kesme noktası ayarlama][7]

<span data-ttu-id="3db96-153">Merhaba başlatma **Service Fabric Explorer** hello üzerinde sağ tıklanarak aracı **yerel Küme Yöneticisi** sistem tepsisi uygulaması ve **yerel kümeyi Yönet**.</span><span class="sxs-lookup"><span data-stu-id="3db96-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Hello yerel Küme Yöneticisi ' Service Fabric Explorer'ı başlatın][systray-launch-sfx]

<span data-ttu-id="3db96-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) kümenin görsel bir gösterimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3db96-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="3db96-156">Dağıtılan uygulamalar tooit hello kümesi ve onu oluşturan fiziksel düğümlerin hello kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="3db96-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="3db96-157">Merhaba sol bölmesinde **küme > düğümler** ve kodunuzun çalıştığı Bul hello düğüm.</span><span class="sxs-lookup"><span data-stu-id="3db96-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="3db96-158">Tıklatın **Eylemler > devre dışı bırak (yeniden)** makinenin yeniden başlatılması toosimulate.</span><span class="sxs-lookup"><span data-stu-id="3db96-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Service Fabric Explorer'da bir düğümü durdurma][sfx-stop-node]

<span data-ttu-id="3db96-160">Kısa bir süre içinde isabetini göreceksiniz tooanother yaptığınız işlem bir düğüme sorunsuz bir şekilde hello hesaplama başarısız olarak Visual Studio'da isabet.</span><span class="sxs-lookup"><span data-stu-id="3db96-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="3db96-161">Ardından, toohello Tanılama Olayları Görüntüleyicisi dönün ve hello iletileri gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="3db96-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="3db96-162">Merhaba olaylar gerçekte farklı bir düğümden geliyor olsa bile hello sayacın artmaya devam.</span><span class="sxs-lookup"><span data-stu-id="3db96-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Yük devretme sonrası tanılama olayları görüntüleyicisi][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="3db96-164">Merhaba yerel küme (isteğe bağlı) temizleme</span><span class="sxs-lookup"><span data-stu-id="3db96-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="3db96-165">Bu yerel kümenin gerçek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3db96-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="3db96-166">Merhaba hata ayıklayıcı durdurma uygulama örneğinizi kaldırır ve hello uygulama türü kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="3db96-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="3db96-167">Ancak, hello küme toorun hello arka planda devam eder.</span><span class="sxs-lookup"><span data-stu-id="3db96-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="3db96-168">Hazır toostop hello yerel küme olduğunuzda, birkaç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="3db96-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="3db96-169">Uygulamayı ve izleme verilerini koruma</span><span class="sxs-lookup"><span data-stu-id="3db96-169">Keep application and trace data</span></span>

<span data-ttu-id="3db96-170">Merhaba üzerinde sağ tıklayarak Hello kümeyi kapatın **yerel Küme Yöneticisi** sistem tepsisi uygulaması ve ardından **yerel kümeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="3db96-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="3db96-171">Merhaba küme ve tüm verileri silme</span><span class="sxs-lookup"><span data-stu-id="3db96-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="3db96-172">Merhaba üzerinde sağ tıklayarak Hello kümesini kaldırmak **yerel Küme Yöneticisi** sistem tepsisi uygulaması ve ardından **yerel kümeyi Kaldır**.</span><span class="sxs-lookup"><span data-stu-id="3db96-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="3db96-173">Bu seçeneği seçerseniz, Visual Studio hello küme hello çalıştırma hello uygulama sonraki sefer yeniden.</span><span class="sxs-lookup"><span data-stu-id="3db96-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="3db96-174">Bir süredir toouse hello yerel küme planlamıyorsanız veya tooreclaim kaynakları gerekiyorsa bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3db96-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3db96-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3db96-175">Next steps</span></span>
<span data-ttu-id="3db96-176">[Reliable services](service-fabric-reliable-services-introduction.md) hakkındaki diğer yazıları okuyun.</span><span class="sxs-lookup"><span data-stu-id="3db96-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
