---
title: "aaaQuickly var olan bir uygulama tooan Azure Service Fabric kümesi dağıtma"
description: "Azure Service Fabric kümesi toohost var olan bir Node.js uygulamasını Visual Studio ile kullanın."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="9dbc9-103">Node.js uygulamasını Azure Service Fabric'te barındırma</span><span class="sxs-lookup"><span data-stu-id="9dbc9-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="9dbc9-104">Bu hızlı başlangıç Azure üzerinde çalışan bir var olan uygulama (Bu örnekte Node.js) tooa Service Fabric kümesi dağıtmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dbc9-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9dbc9-105">Prerequisites</span></span>

<span data-ttu-id="9dbc9-106">Başlamadan önce [geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started.md) emin olun.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="9dbc9-107">Merhaba Service Fabric SDK ve Visual Studio 2017 veya 2015 yüklenmesini içerir.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="9dbc9-108">Dağıtım için toohave var olan bir Node.js uygulamasını da gerekir.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="9dbc9-109">Bu hızlı başlangıçta, [buradan][download-sample] indirilebilen basit bir Node.js web sitesi kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="9dbc9-110">Bu dosya tooyour ayıklamak `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` hello sonraki adımda hello projesi oluşturduktan sonra klasör.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="9dbc9-111">Azure aboneliğiniz yoksa [ücretsiz bir hesap][create-account] oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="9dbc9-112">Merhaba hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="9dbc9-112">Create hello service</span></span>

<span data-ttu-id="9dbc9-113">Visual Studio'yu **yönetici** olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="9dbc9-114">`CTRL`+`SHIFT`+`N` ile bir proje oluşturun</span><span class="sxs-lookup"><span data-stu-id="9dbc9-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="9dbc9-115">Merhaba, **yeni proje** iletişim kutusunda, seçin **bulut > Service Fabric uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="9dbc9-116">Ad Merhaba uygulaması **MyGuestApp** ve basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9dbc9-117">Node.js hello 260 karakter sınırını windows olan yollar için kolayca bozulabilir.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="9dbc9-118">Kısa bir yol hello projesi için kendisini gibi kullandığınız **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Visual Studio'da yeni proje iletişim kutusu][new-project]

<span data-ttu-id="9dbc9-120">Service Fabric hizmeti herhangi bir türde hello sonraki iletişim kutusundan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="9dbc9-121">Bu hızlı başlangıç için **Konuk Yürütülebilir Dosyası**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="9dbc9-122">Ad hello hizmeti **MyGuestService** ve hello sağ toohello üzerinde hello seçeneklerini ayarlama aşağıdaki değerler:</span><span class="sxs-lookup"><span data-stu-id="9dbc9-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="9dbc9-123">Ayar</span><span class="sxs-lookup"><span data-stu-id="9dbc9-123">Setting</span></span>                   | <span data-ttu-id="9dbc9-124">Değer</span><span class="sxs-lookup"><span data-stu-id="9dbc9-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="9dbc9-125">Kod Paketi Klasörü</span><span class="sxs-lookup"><span data-stu-id="9dbc9-125">Code Package Folder</span></span>       | <span data-ttu-id="9dbc9-126">_&lt;Node.js uygulamanızı Hello klasörüyle&gt;_</span><span class="sxs-lookup"><span data-stu-id="9dbc9-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="9dbc9-127">Kod Paketi Davranışı</span><span class="sxs-lookup"><span data-stu-id="9dbc9-127">Code Package Behavior</span></span>     | <span data-ttu-id="9dbc9-128">Klasör içeriği tooproject kopyalama</span><span class="sxs-lookup"><span data-stu-id="9dbc9-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="9dbc9-129">Program</span><span class="sxs-lookup"><span data-stu-id="9dbc9-129">Program</span></span>                   | <span data-ttu-id="9dbc9-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="9dbc9-130">node.exe</span></span> |
| <span data-ttu-id="9dbc9-131">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="9dbc9-131">Arguments</span></span>                 | <span data-ttu-id="9dbc9-132">server.js</span><span class="sxs-lookup"><span data-stu-id="9dbc9-132">server.js</span></span> |
| <span data-ttu-id="9dbc9-133">Çalışma Klasörü</span><span class="sxs-lookup"><span data-stu-id="9dbc9-133">Working Folder</span></span>            | <span data-ttu-id="9dbc9-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="9dbc9-134">CodePackage</span></span> |

<span data-ttu-id="9dbc9-135">**Tamam**'a basın.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-135">Press **OK**.</span></span>

![Visual Studio'da yeni hizmet iletişim kutusu][new-service]

<span data-ttu-id="9dbc9-137">Visual Studio hello uygulama projesi ve hello aktör hizmeti projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="9dbc9-138">Merhaba uygulama projesi (**MyGuestApp**) herhangi bir kod doğrudan içermiyor.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="9dbc9-139">Bunun yerine, bir dizi hizmet projesine başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="9dbc9-140">Ayrıca, bunlardan farklı olarak üç tür içerik daha barındırır:</span><span class="sxs-lookup"><span data-stu-id="9dbc9-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="9dbc9-141">**Yayımlama profilleri**</span><span class="sxs-lookup"><span data-stu-id="9dbc9-141">**Publish profiles**</span></span>  
<span data-ttu-id="9dbc9-142">Farklı ortamlar için araç tercihleri.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="9dbc9-143">**Betikler**</span><span class="sxs-lookup"><span data-stu-id="9dbc9-143">**Scripts**</span></span>  
<span data-ttu-id="9dbc9-144">Uygulamanızı dağıtmak/yükseltmek için PowerShell betiği.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="9dbc9-145">**Uygulama tanımı**</span><span class="sxs-lookup"><span data-stu-id="9dbc9-145">**Application definition**</span></span>  
<span data-ttu-id="9dbc9-146">Merhaba uygulama bildirimi içerir *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="9dbc9-147">İlişkili uygulama parametreleri dosyalarını olan altında *ApplicationParameters*, hello uygulamayı tanımlayan ve tooconfigure izin özellikle belirli bir ortam için.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="9dbc9-148">Merhaba hizmet projesi Merhaba içeriğine genel bakış için bkz: [Reliable Services ile çalışmaya başlama](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="9dbc9-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="9dbc9-149">Ağı ayarlama</span><span class="sxs-lookup"><span data-stu-id="9dbc9-149">Set up networking</span></span>

<span data-ttu-id="9dbc9-150">Node.js uygulaması dağıtma kullandığı bağlantı noktası hello örnek **80** ve tootell kullanıma sunulan bağlantı noktası olduğunu ihtiyacımız Service Fabric ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="9dbc9-151">Açık hello **ServiceManifest.xml** hello proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="9dbc9-152">Hello bildirimi Hello kısımda olduğu bir `<Resources> \ <Endpoints>` önceden tanımlanmış bir girişi.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="9dbc9-153">Bu giriş tooadd değiştirme `Port`, `Protocol`, ve `Type`.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="9dbc9-154">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="9dbc9-154">Deploy tooAzure</span></span>

<span data-ttu-id="9dbc9-155">Basarsanız **F5** ve başlangıç projesi çalıştırın, dağıtılan toohello yerel küme olabilir.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="9dbc9-156">Ancak, şimdi tooAzure yerine dağıtın.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="9dbc9-157">Merhaba projeye sağ tıklayın ve seçin **Yayımla...**  iletişim toopublish tooAzure açar.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Yayımlama yapı hizmeti için tooazure iletişim kutusu][publish]

<span data-ttu-id="9dbc9-159">Select hello **PublishProfiles\Cloud.xml** hedef profil.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="9dbc9-160">Daha önce yapmadıysanız, bir Azure hesabı toodeploy seçin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="9dbc9-161">Henüz hesabınız yoksa, [bir hesap için kaydolun][create-account].</span><span class="sxs-lookup"><span data-stu-id="9dbc9-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="9dbc9-162">Altında **bağlantı uç noktasının**, hello Service Fabric kümesi toodeploy seçin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="9dbc9-163">Bir yoksa seçin  **&lt;yeni küme oluştur... &gt;**  web tarayıcısı penceresi toohello Azure portal açar.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="9dbc9-164">Daha fazla bilgi için bkz: [hello Portalı'nda bir küme oluşturma](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9dbc9-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="9dbc9-165">Merhaba Service Fabric kümesi oluşturduğunuzda, emin tooset hello olun **özel uç noktaları** çok ayarı**80**.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Uç noktayla Service Fabric düğüm türü yapılandırması][custom-endpoint]

<span data-ttu-id="9dbc9-167">Yeni bir Service Fabric kümesi oluşturuluyor bazı zaman toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="9dbc9-168">Edildikten sonra oluşturulan, Git geri toohello yayımlama iletişim kutusu ve seçin  **&lt;yenileme&gt;**.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="9dbc9-169">Merhaba yeni küme hello açılan kutusunda listelenir; bunu seçin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="9dbc9-170">Tuşuna **Yayımla** ve hello dağıtım toofinish için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="9dbc9-171">Bu birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-171">This may take a few minutes.</span></span> <span data-ttu-id="9dbc9-172">İşlem tamamlandıktan sonra hello uygulama toobe tam olarak kullanılabilir için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="9dbc9-173">Test hello Web sitesi</span><span class="sxs-lookup"><span data-stu-id="9dbc9-173">Test hello website</span></span>

<span data-ttu-id="9dbc9-174">Hizmetiniz yayımlandıktan sonra, hizmeti web tarayıcısında test edin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="9dbc9-175">İlk olarak, hello Azure portalını açın ve Service Fabric hizmetinizi bulun.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="9dbc9-176">Hello hizmeti adresi Hello genel bakış dikey penceresini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="9dbc9-177">Hello kullan hello etki alanı adından _istemci bağlantı uç noktasının_ özelliği.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="9dbc9-178">Örneğin, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Service fabric genel bakış dikey penceresinde hello Azure portalı][overview]

<span data-ttu-id="9dbc9-180">Merhaba göreceğiniz toothis adresine gidin `HELLO WORLD` yanıt.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="9dbc9-181">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="9dbc9-181">Delete hello cluster</span></span>

<span data-ttu-id="9dbc9-182">Siz bu hızlı başlangıç için oluşturduğunuz hello kaynakların tümünü bu kaynakları için ücretlendirilirsiniz toodelete unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dbc9-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9dbc9-183">Next steps</span></span>
<span data-ttu-id="9dbc9-184">[Konuk yürütülebilir dosyaları](service-fabric-deploy-existing-app.md) hakkındaki diğer yazıları okuyun.</span><span class="sxs-lookup"><span data-stu-id="9dbc9-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F