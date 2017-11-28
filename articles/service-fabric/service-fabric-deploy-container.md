---
title: "aaaService doku ve kapsayıcıları dağıtma | Microsoft Docs"
description: "Service Fabric ve Merhaba kapsayıcılara toodeploy mikro hizmet uygulamaları kullanın. Bu makale, Service Fabric kapsayıcıları ve nasıl toodeploy Windows kapsayıcı görüntü bir kümede sağlar hello özellikleri açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="0333c-104">Bir Windows kapsayıcı tooService doku dağıtma</span><span class="sxs-lookup"><span data-stu-id="0333c-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0333c-105">Windows kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="0333c-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="0333c-106">Docker kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="0333c-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="0333c-107">Bu makalede Windows kapsayıcılarında kapsayıcılı Hizmetleri oluşturmanın hello işlemiyle anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0333c-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="0333c-108">Service Fabric oluşan mikro kapsayıcılarda çalışan uygulamaları oluşturmaya yardımcı çeşitli özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="0333c-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="0333c-109">Merhaba özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0333c-109">hello capabilities include:</span></span>

* <span data-ttu-id="0333c-110">Kapsayıcı görüntü dağıtımı ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0333c-110">Container image deployment and activation</span></span>
* <span data-ttu-id="0333c-111">Kaynak İdaresi</span><span class="sxs-lookup"><span data-stu-id="0333c-111">Resource governance</span></span>
* <span data-ttu-id="0333c-112">Depo kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0333c-112">Repository authentication</span></span>
* <span data-ttu-id="0333c-113">Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme</span><span class="sxs-lookup"><span data-stu-id="0333c-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="0333c-114">Kapsayıcıya bulma ve iletişim</span><span class="sxs-lookup"><span data-stu-id="0333c-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="0333c-115">Özelliği tooconfigure ve ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="0333c-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="0333c-116">Uygulamanıza dahil kapsayıcılı hizmet toobe paketleme zaman özelliklerin her biri işleyişi konumundaki bakalım.</span><span class="sxs-lookup"><span data-stu-id="0333c-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="0333c-117">Paket bir Windows kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="0333c-117">Package a Windows container</span></span>
<span data-ttu-id="0333c-118">Bir kapsayıcı paketini oluşturduğunuzda, bir ya da Visual Studio Proje şablonu toouse seçebilirsiniz veya [hello uygulama paketini el ile oluşturmak](#manually).</span><span class="sxs-lookup"><span data-stu-id="0333c-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="0333c-119">Kullandığınızda, Visual Studio, hello uygulama paketi yapısı ve bildirim dosyası hello yeni proje şablonu tarafından sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0333c-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="0333c-120">Merhaba en kolay yolu toopackage var olan bir kapsayıcı görüntüsünü bir hizmete toouse Visual Studio ' dir.</span><span class="sxs-lookup"><span data-stu-id="0333c-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="0333c-121">Visual Studio toopackage var olan bir kapsayıcı görüntüsünü kullanın</span><span class="sxs-lookup"><span data-stu-id="0333c-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="0333c-122">Visual Studio Service Fabric hizmet şablonu toohelp bir kapsayıcı tooa Service Fabric kümesi dağıtma sağlar.</span><span class="sxs-lookup"><span data-stu-id="0333c-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="0333c-123">Seçin **dosya** > **yeni proje**ve bir Service Fabric uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0333c-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="0333c-124">Seçin **Konuk kapsayıcı** hello hizmet şablonu olarak.</span><span class="sxs-lookup"><span data-stu-id="0333c-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="0333c-125">Seçin **görüntü adı** ve kapsayıcı deponuzun hello yolu toohello resmi belirtin.</span><span class="sxs-lookup"><span data-stu-id="0333c-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="0333c-126">Örneğin, `myrepo/myimage:v1` https://hub.docker.com içinde</span><span class="sxs-lookup"><span data-stu-id="0333c-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="0333c-127">Hizmetinize bir ad verin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0333c-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="0333c-128">Kapsayıcılı hizmetinizi iletişim için bir uç nokta gerekiyorsa, artık hello protokolü, bağlantı noktası ve türü toohello ServiceManifest.xml dosya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0333c-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="0333c-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0333c-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="0333c-130">Merhaba sağlayarak `UriScheme`, Service Fabric otomatik olarak kaydeder hello kapsayıcı uç nokta hello bulunabilirlik için adlandırma hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="0333c-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="0333c-131">başlangıç bağlantı noktası (örnek önceki hello gösterildiği gibi) sabit veya dinamik olarak ayrılan.</span><span class="sxs-lookup"><span data-stu-id="0333c-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="0333c-132">Bir bağlantı noktası belirtmezseniz, (hizmet olacağını gibi) hello uygulama bağlantı noktası aralığından dinamik ayrılır.</span><span class="sxs-lookup"><span data-stu-id="0333c-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="0333c-133">Ayrıca belirterek tooconfigure hello kapsayıcı toohost bağlantı noktası eşlemesi gerekir bir `PortBinding` hello uygulama bildiriminde ilkesi.</span><span class="sxs-lookup"><span data-stu-id="0333c-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="0333c-134">Daha fazla bilgi için bkz: [kapsayıcı toohost bağlantı noktası eşlemesi yapılandırma](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="0333c-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="0333c-135">Kapsayıcı kaynak İdaresi gereken ardından ekleyin, bir `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="0333c-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="0333c-136">Ardından, kapsayıcı bir özel deposu ile tooauthenticate gerekirse, ekleyin `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="0333c-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="0333c-137">Kapsayıcı desteği etkinleştirilmiş bir Windows Server 2016 makinede çalıştırılıyorsa hello paketini kullanmak ve eylem toodeploy tooyour yerel küme yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="0333c-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="0333c-138">Hazır olduğunuzda, yayımlama hello uygulama tooa uzaktan küme veya hello çözüm toosource denetiminde denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0333c-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="0333c-139">Bir örnek checkout hello [github'da Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="0333c-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="0333c-140">Windows Server 2016 küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="0333c-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="0333c-141">toodeploy kapsayıcılı uygulamanız Windows Server 2016 kapsayıcı desteğiyle çalıştıran bir kümeye etkin toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="0333c-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="0333c-142">Kümenizi çalıştıran yerel olarak veya azure'da Azure Resource Manager aracılığıyla dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="0333c-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="0333c-143">toodeploy Azure Kaynak Yöneticisi'ni kullanarak bir küme seçin hello **Windows Server 2016 kapsayıcılarla** görüntü Azure seçeneği.</span><span class="sxs-lookup"><span data-stu-id="0333c-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="0333c-144">Merhaba makalesine bakın [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="0333c-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="0333c-145">Azure Resource Manager ayarları aşağıdaki hello kullandığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="0333c-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="0333c-146">Merhaba de kullanabilirsiniz [beş düğümü Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate bir küme.</span><span class="sxs-lookup"><span data-stu-id="0333c-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="0333c-147">Alternatif olarak bir topluluk okuma [blog gönderisi](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) Service Fabric ve Windows kapsayıcıları kullanma.</span><span class="sxs-lookup"><span data-stu-id="0333c-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="0333c-148">El ile paketini ve kapsayıcı görüntüsünü Dağıt</span><span class="sxs-lookup"><span data-stu-id="0333c-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="0333c-149">el ile kapsayıcılı hizmet paketleme hello işlemi aşağıdaki adımları hello üzerinde dayanır:</span><span class="sxs-lookup"><span data-stu-id="0333c-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="0333c-150">Merhaba kapsayıcılara tooyour depo yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="0333c-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="0333c-151">Merhaba paket dizin yapısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0333c-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="0333c-152">Merhaba hizmet bildirim dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="0333c-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="0333c-153">Merhaba uygulama bildirim dosyasının düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="0333c-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="0333c-154">Dağıtma ve kapsayıcı görüntü etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="0333c-154">Deploy and activate a container image</span></span>
<span data-ttu-id="0333c-155">Merhaba Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0333c-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="0333c-156">toodeploy ve etkinleştirme kapsayıcı, put hello adını hello kapsayıcı görüntüsüne bir `ContainerHost` hello hizmet bildirimi öğesinde.</span><span class="sxs-lookup"><span data-stu-id="0333c-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="0333c-157">Merhaba hizmet bildiriminde eklemek bir `ContainerHost` hello giriş noktası için.</span><span class="sxs-lookup"><span data-stu-id="0333c-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="0333c-158">Ardından kümesi hello `ImageName` toobe hello adını hello kapsayıcı depo ve görüntü.</span><span class="sxs-lookup"><span data-stu-id="0333c-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="0333c-159">Merhaba aşağıdaki kısmi bildirimi gösterir nasıl toodeploy hello kapsayıcı olarak adlandırılan bir örnek `myimage:v1` adlı bir depodan `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="0333c-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="0333c-160">İsteğe bağlı komutları toorun hello kapsayıcısı hello altında başlatma belirtebilirsiniz `Commands` öğesi.</span><span class="sxs-lookup"><span data-stu-id="0333c-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="0333c-161">Birden çok komutlarında virgülle-bunları sınırlar.</span><span class="sxs-lookup"><span data-stu-id="0333c-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="0333c-162">Kaynak İdaresi anlama</span><span class="sxs-lookup"><span data-stu-id="0333c-162">Understand resource governance</span></span>
<span data-ttu-id="0333c-163">Kaynak İdaresi kapsayıcı hello hello kaynakları kısıtlayan hello kapsayıcı yeteneğini hello konakta kullanabilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="0333c-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="0333c-164">Merhaba `ResourceGovernancePolicy`, kendisi hello uygulama bildiriminde belirtilen bir hizmeti kod paketi için kullanılan toodeclare kaynak sınırları olduğu.</span><span class="sxs-lookup"><span data-stu-id="0333c-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="0333c-165">Kaynak sınırları kaynakları aşağıdaki Merhaba ayarlanabilir:</span><span class="sxs-lookup"><span data-stu-id="0333c-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="0333c-166">Bellek</span><span class="sxs-lookup"><span data-stu-id="0333c-166">Memory</span></span>
* <span data-ttu-id="0333c-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="0333c-167">MemorySwap</span></span>
* <span data-ttu-id="0333c-168">CpuShares (CPU göreli ağırlık)</span><span class="sxs-lookup"><span data-stu-id="0333c-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="0333c-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="0333c-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="0333c-170">BlkioWeight (BlockIO göreli ağırlık).</span><span class="sxs-lookup"><span data-stu-id="0333c-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="0333c-171">IOPS gibi belirli blok g/ç sınırları belirtmek için destek, okuma/yazma BPS ve diğerleri için gelecekteki bir sürüm planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0333c-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="0333c-172">Bir depo kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0333c-172">Authenticate a repository</span></span>
<span data-ttu-id="0333c-173">bir kapsayıcı toodownload tooprovide oturum açma kimlik bilgileri toohello kapsayıcı deposu olabilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="0333c-174">Merhaba uygulama bildiriminde belirtilen hello oturum açma kimlik bilgileri, kullanılan toospecify hello oturum açma bilgileri veya hello kapsayıcı görüntü hello görüntü deposundan karşıdan yüklemek için SSH anahtarı, ' dir.</span><span class="sxs-lookup"><span data-stu-id="0333c-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="0333c-175">Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser* hello parola düz metin birlikte (*değil* önerilen):</span><span class="sxs-lookup"><span data-stu-id="0333c-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="0333c-176">Toohello makine dağıtmış olan bir sertifikayı kullanarak hello parolayı şifrelemek öneririz.</span><span class="sxs-lookup"><span data-stu-id="0333c-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="0333c-177">Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser*, burada hello parola adı verilen bir sertifika kullanılarak şifrelenmiş *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="0333c-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="0333c-178">Merhaba kullanabilirsiniz `Invoke-ServiceFabricEncryptText` PowerShell komut toocreate hello gizli şifreli metin hello parolası.</span><span class="sxs-lookup"><span data-stu-id="0333c-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="0333c-179">Daha fazla bilgi için hello makalesine bakın [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="0333c-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="0333c-180">Merhaba toodecrypt hello parola kullandı hello sertifikasının özel anahtarı yerel makinede bir bant dışı yöntem dağıtılan toohello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0333c-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="0333c-181">(Azure'da, Azure Resource Manager bu yöntem budur.) Ardından, Service Fabric hello hizmet paketi toohello makine dağıtırken hello gizli şifresini çözebilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="0333c-182">Merhaba gizli hello hesap adı ile birlikte kullanarak, onu hello kapsayıcı deposuyla sonra doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <span data-ttu-id="0333c-183"><a name ="Portsection"></a>Kapsayıcı toohost bağlantı noktası eşlemesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0333c-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="0333c-184">Belirterek hello kapsayıcı ile bir ana bilgisayar kullanılan bağlantı noktası toocommunicate yapılandırabilirsiniz bir `PortBinding` hello uygulama bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="0333c-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="0333c-185">Merhaba kapsayıcı tooa bağlantı hello konaktaki içinde dinleyen bir Hello bağlantı noktası bağlama eşlemeleri hello bağlantı noktası toowhich hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="0333c-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="0333c-186">Kapsayıcıya bulma ve iletişim yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0333c-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="0333c-187">Merhaba kullanabilirsiniz `PortBinding` öğesi toomap hello hizmet bildiriminde bir kapsayıcı bağlantı noktası tooan uç noktası.</span><span class="sxs-lookup"><span data-stu-id="0333c-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="0333c-188">Uç noktası aşağıdaki örneğine hello hello `Endpoint1` 8905 sabit bir bağlantı noktasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="0333c-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="0333c-189">Rastgele bir bağlantı noktası hello kümenin uygulama bağlantı noktası aralığından sizin için bu durumda seçilen bağlantı noktası yok hiç da belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
<span data-ttu-id="0333c-190">Bir uç nokta belirtirseniz, hello kullanarak `Endpoint` hello hizmet bildirimi Konuk kapsayıcı, Service Fabric etiketinde otomatik olarak bu uç nokta toohello adlandırma hizmeti yayımlama.</span><span class="sxs-lookup"><span data-stu-id="0333c-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="0333c-191">Merhaba kümede çalışan diğer hizmetler, böylece çözümlemek için hello REST sorgularını kullanarak bu kapsayıcı bulabilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="0333c-192">Merhaba Naming service ile kaydederek-kapsayıcıya iletişimi kapsayıcı içinde hello kullanarak gerçekleştirebileceğiniz [ters proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="0333c-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="0333c-193">İletişim hello ters proxy http dinleme bağlantı noktası ve ortam değişkenleri olarak toocommunicate ile istediğiniz hello Hizmetleri hello adını sağlayarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="0333c-194">Daha fazla bilgi için hello sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="0333c-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="0333c-195">Ortam değişkenlerini yapılandırma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="0333c-195">Configure and set environment variables</span></span>
<span data-ttu-id="0333c-196">Ortam değişkenleri, her kod paketi hello hizmet bildiriminde için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="0333c-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="0333c-197">Bu özellik, kapsayıcı olarak mı dağıtıldıklarına yoksa konuk yürütülebilir dosyası olarak mı işlendiklerine bakılmaksızın tüm hizmetlerde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0333c-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="0333c-198">Merhaba uygulaması değerleri bildirim veya onları uygulama parametreleri olarak dağıtımı sırasında belirttiğiniz ortam değişkeni geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0333c-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="0333c-199">Merhaba aşağıdaki hizmet bildirim XML parçacığını gösterir nasıl bir örneği için bir kod paketi toospecify ortam değişkenleri:</span><span class="sxs-lookup"><span data-stu-id="0333c-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="0333c-200">Bu ortam değişkenleri hello uygulama bildirim düzeyinde geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="0333c-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="0333c-201">Merhaba önceki örnekte, biz hello için açık bir değer belirtilen `HttpGateway` ortam değişkeni (Merhaba değeri ayarlarız sırada 19000) `BackendServiceName` hello parametresi `[BackendSvc]` uygulama parametresi.</span><span class="sxs-lookup"><span data-stu-id="0333c-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="0333c-202">Bu ayarlar için toospecify hello değer etkinleştirmek `BackendServiceName`değer hello uygulamayı dağıttıktan sonra hello bildiriminde sabit bir değere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="0333c-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="0333c-203">Yalıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0333c-203">Configure isolation mode</span></span>

<span data-ttu-id="0333c-204">Windows için kapsayıcı - işlem ve Hyper-V iki yalıtım modunu destekler.</span><span class="sxs-lookup"><span data-stu-id="0333c-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="0333c-205">Merhaba işlem yalıtım moduyla üzerinde çalışan tüm Merhaba kapsayıcılara aynı ana bilgisayar makine paylaşımı hello çekirdek hello ana bilgisayarla hello.</span><span class="sxs-lookup"><span data-stu-id="0333c-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="0333c-206">Merhaba Hyper-V yalıtım moduyla hello tekrar her Hyper-V kapsayıcı ve hello kapsayıcı konak arasında yalıtılır.</span><span class="sxs-lookup"><span data-stu-id="0333c-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="0333c-207">Merhaba yalıtım modunu hello belirtilen `ContainerHostPolicies` hello uygulama bildirim dosyasının etiketinde.</span><span class="sxs-lookup"><span data-stu-id="0333c-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="0333c-208">belirtilebilir hello yalıtım modlar `process`, `hyperv`, ve `default`.</span><span class="sxs-lookup"><span data-stu-id="0333c-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="0333c-209">Merhaba `default` yalıtım modunu Varsayılanları çok`process` Windows Server'da barındıran ve çok varsayılanlarını`hyperv` Windows 10 konaklarda.</span><span class="sxs-lookup"><span data-stu-id="0333c-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="0333c-210">Merhaba aşağıdaki kod parçacığında hello uygulama bildirim dosyasında belirtilen hello yalıtım modu nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="0333c-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="0333c-211">Uygulama ve hizmet bildirimi için örnekler tamamlayın</span><span class="sxs-lookup"><span data-stu-id="0333c-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="0333c-212">Bir örnek uygulama bildirimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0333c-212">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="0333c-213">Bir örnek hizmet bildirimi (uygulama bildirimi önceki hello belirtilen) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0333c-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="0333c-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0333c-214">Next steps</span></span>
<span data-ttu-id="0333c-215">Kapsayıcılı hizmetini dağıttıysanız, bilgi nasıl toomanage okuyarak kendi ömrü [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0333c-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="0333c-216">Service Fabric ve kapsayıcıları genel bakış</span><span class="sxs-lookup"><span data-stu-id="0333c-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="0333c-217">Bir örnek checkout [github'da Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="0333c-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
