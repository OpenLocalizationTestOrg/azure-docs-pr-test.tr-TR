---
title: "aaaService doku ve Linux kapsayıcıları dağıtma | Microsoft Docs"
description: "Service Fabric ve hello Linux kapsayıcıları toodeploy mikro hizmet uygulamaları kullanın. Bu makalede kapsayıcıları ve nasıl toodeploy Linux kapsayıcı görüntü bir kümede Service Fabric sağlar hello özellikleri"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="f043f-104">Linux kapsayıcı tooService doku dağıtma</span><span class="sxs-lookup"><span data-stu-id="f043f-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f043f-105">Windows kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="f043f-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="f043f-106">Linux kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="f043f-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="f043f-107">Bu makalede Linux'ta Docker kapsayıcılarında kapsayıcılı hizmetleri oluşturma sürecinde anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f043f-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="f043f-108">Service Fabric oluşan kapsayıcılı, mikro uygulamaları oluşturmaya yardımcı birkaç kapsayıcı özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f043f-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="f043f-109">Bu hizmetler kapsayıcılı Hizmetleri olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="f043f-109">These services are called containerized services.</span></span>

<span data-ttu-id="f043f-110">Merhaba yeteneklere;</span><span class="sxs-lookup"><span data-stu-id="f043f-110">hello capabilities include;</span></span>

* <span data-ttu-id="f043f-111">Kapsayıcı görüntü dağıtımı ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f043f-111">Container image deployment and activation</span></span>
* <span data-ttu-id="f043f-112">Kaynak İdaresi</span><span class="sxs-lookup"><span data-stu-id="f043f-112">Resource governance</span></span>
* <span data-ttu-id="f043f-113">Depo kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f043f-113">Repository authentication</span></span>
* <span data-ttu-id="f043f-114">Kapsayıcı bağlantı noktası toohost bağlantı noktası eşleme</span><span class="sxs-lookup"><span data-stu-id="f043f-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="f043f-115">Kapsayıcıya bulma ve iletişim</span><span class="sxs-lookup"><span data-stu-id="f043f-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="f043f-116">Özelliği tooconfigure ve ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="f043f-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="f043f-117">Docker kapsayıcısı ile yeoman paketleme</span><span class="sxs-lookup"><span data-stu-id="f043f-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="f043f-118">Linux üzerinde bir kapsayıcı paketleme, ya da toouse yeoman şablonu seçebilirsiniz veya [hello uygulama paketini el ile oluşturmak](#manually).</span><span class="sxs-lookup"><span data-stu-id="f043f-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="f043f-119">Service Fabric uygulaması her hello uygulamanın işlevselliğini aktarma konusunda belirli bir rol ile bir veya daha fazla kapsayıcıları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="f043f-120">Merhaba Linux için Service Fabric SDK içerir bir [Yeoman](http://yeoman.io/) kolay toocreate kolaylaştırır Oluşturucu uygulamanız ve kapsayıcı görüntü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f043f-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="f043f-121">Yeoman tek bir Docker kapsayıcısı uygulamayla adlı toocreate kullanalım *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="f043f-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="f043f-122">Oluşturulan hello bildirim dosyalarını düzenleyerek daha fazla hizmet daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f043f-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="f043f-123">Docker geliştirme kutunuzun yükleyin</span><span class="sxs-lookup"><span data-stu-id="f043f-123">Install Docker on your development box</span></span>

<span data-ttu-id="f043f-124">Çalışma hello aşağıdaki komutları Linux geliştirme kutunuzda tooinstall docker (OSX üzerinde hello vagrant görüntüsü kullanıyorsanız, docker zaten yüklü):</span><span class="sxs-lookup"><span data-stu-id="f043f-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="f043f-125">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f043f-125">Create hello application</span></span>
1. <span data-ttu-id="f043f-126">Bir terminal penceresinde `yo azuresfcontainer` yazın.</span><span class="sxs-lookup"><span data-stu-id="f043f-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="f043f-127">Örneğin, mycontainerap uygulamanızın - adı</span><span class="sxs-lookup"><span data-stu-id="f043f-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="f043f-128">Merhaba kapsayıcı DockerHub depodaki görüntüden için Hello URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="f043f-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="f043f-129">Merhaba resim parametresi alır hello formu [repo] / [görüntü adı]</span><span class="sxs-lookup"><span data-stu-id="f043f-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="f043f-130">Merhaba görüntü bir iş yükü giriş tanımlanmış noktası yok sonra tooexplicitly ihtiyacınız başlatma işleminden sonra çalışan hello kapsayıcı tutar hello kapsayıcı içindeki komutları toorun virgülle ayrılmış bir dizi giriş komutları belirtin.</span><span class="sxs-lookup"><span data-stu-id="f043f-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="f043f-132">Merhaba uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="f043f-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="f043f-133">XPlat CLI aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="f043f-133">Using XPlat CLI</span></span>
<span data-ttu-id="f043f-134">Merhaba uygulama oluşturulduktan sonra toohello yerel küme hello Azure CLI kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f043f-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="f043f-135">Toohello yerel Service Fabric kümesi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f043f-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="f043f-136">Kullanım hello hello şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan komut dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f043f-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="f043f-137">Bir tarayıcı açın ve http://localhost: 19080/Explorer (Merhaba Vagrant Mac OS X kullanıyorsanız VM hello özel IP ile değiştir localhost) konumunda tooService Fabric Gezgini'ne gidin.</span><span class="sxs-lookup"><span data-stu-id="f043f-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="f043f-138">Merhaba uygulamaları düğümünü genişletin ve şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir yoktur.</span><span class="sxs-lookup"><span data-stu-id="f043f-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="f043f-139">Merhaba kaldırma komut dosyası kullan hello şablon toodelete hello uygulama örneği içinde sağlanan ve hello uygulama türü kaydını silin.</span><span class="sxs-lookup"><span data-stu-id="f043f-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="f043f-140">Azure CLI 2.0 aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="f043f-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="f043f-141">Merhaba başvuru belge yönetme hakkında bkz bir [uygulama yaşam döngüsü kullanmayı hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="f043f-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="f043f-142">Örnek bir uygulama için [checkout hello Service Fabric kapsayıcı kodu Github'da örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="f043f-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="f043f-143">Daha fazla Hizmetleri tooan varolan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="f043f-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="f043f-144">tooadd başka bir kapsayıcı hizmet zaten kullanılarak oluşturulan tooan uygulaması `yo`, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f043f-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="f043f-145">Merhaba var olan uygulamanın toohello kök dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f043f-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="f043f-146">Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f043f-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="f043f-147">`yo azuresfcontainer:AddService` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f043f-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="f043f-148">El ile paketini ve kapsayıcı görüntüsünü Dağıt</span><span class="sxs-lookup"><span data-stu-id="f043f-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="f043f-149">el ile kapsayıcılı hizmet paketleme hello işlemi aşağıdaki adımları hello üzerinde dayanır:</span><span class="sxs-lookup"><span data-stu-id="f043f-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="f043f-150">Merhaba kapsayıcılara tooyour depo yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="f043f-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="f043f-151">Merhaba paket dizin yapısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f043f-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="f043f-152">Merhaba hizmet bildirim dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f043f-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="f043f-153">Merhaba uygulama bildirim dosyasının düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f043f-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="f043f-154">Dağıtma ve kapsayıcı görüntü etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="f043f-154">Deploy and activate a container image</span></span>
<span data-ttu-id="f043f-155">Merhaba Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f043f-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="f043f-156">toodeploy ve etkinleştirme kapsayıcı, put hello adını hello kapsayıcı görüntüsüne bir `ContainerHost` hello hizmet bildirimi öğesinde.</span><span class="sxs-lookup"><span data-stu-id="f043f-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="f043f-157">Merhaba hizmet bildiriminde eklemek bir `ContainerHost` hello giriş noktası için.</span><span class="sxs-lookup"><span data-stu-id="f043f-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="f043f-158">Ardından kümesi hello `ImageName` toobe hello adını hello kapsayıcı depo ve görüntü.</span><span class="sxs-lookup"><span data-stu-id="f043f-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="f043f-159">Merhaba aşağıdaki kısmi bildirimi gösterir nasıl toodeploy hello kapsayıcı olarak adlandırılan bir örnek `myimage:v1` adlı bir depodan `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="f043f-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="f043f-160">İsteğe bağlı hello belirterek giriş komutları sağlayabilir `Commands` hello kapsayıcı içindeki komutları toorun virgülle ayrılmış bir dizi öğesi.</span><span class="sxs-lookup"><span data-stu-id="f043f-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="f043f-161">Merhaba görüntü bir iş yükü giriş tanımlanmış noktası yok sonra tooexplicitly ihtiyacınız içindeki giriş komutları belirtin `Commands` hello kapsayıcı çalıştırdıktan sonra devam edilecek hello kapsayıcı içindeki komutları toorun virgülle ayrılmış bir dizi öğesi Başlangıç.</span><span class="sxs-lookup"><span data-stu-id="f043f-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="f043f-162">Kaynak İdaresi anlama</span><span class="sxs-lookup"><span data-stu-id="f043f-162">Understand resource governance</span></span>
<span data-ttu-id="f043f-163">Kaynak İdaresi kapsayıcı hello hello kaynakları kısıtlayan hello kapsayıcı yeteneğini hello konakta kullanabilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="f043f-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="f043f-164">Merhaba `ResourceGovernancePolicy`, kendisi hello uygulama bildiriminde belirtilen bir hizmeti kod paketi için kullanılan toodeclare kaynak sınırları olduğu.</span><span class="sxs-lookup"><span data-stu-id="f043f-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="f043f-165">Kaynak sınırları kaynakları aşağıdaki Merhaba ayarlanabilir:</span><span class="sxs-lookup"><span data-stu-id="f043f-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="f043f-166">Bellek</span><span class="sxs-lookup"><span data-stu-id="f043f-166">Memory</span></span>
* <span data-ttu-id="f043f-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="f043f-167">MemorySwap</span></span>
* <span data-ttu-id="f043f-168">CpuShares (CPU göreli ağırlık)</span><span class="sxs-lookup"><span data-stu-id="f043f-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="f043f-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="f043f-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="f043f-170">BlkioWeight (BlockIO göreli ağırlık).</span><span class="sxs-lookup"><span data-stu-id="f043f-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="f043f-171">Gelecekteki bir sürümde, IOPS gibi belirli blok g/ç sınırları belirtmek için destek BPS okuma/yazma ve diğerleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="f043f-172">Bir depo kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f043f-172">Authenticate a repository</span></span>
<span data-ttu-id="f043f-173">bir kapsayıcı toodownload tooprovide oturum açma kimlik bilgileri toohello kapsayıcı deposu olabilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="f043f-174">Merhaba uygulama bildiriminde belirtilen hello oturum açma kimlik bilgileri, kullanılan toospecify hello oturum açma bilgileri veya hello kapsayıcı görüntü hello görüntü deposundan karşıdan yüklemek için SSH anahtarı, ' dir.</span><span class="sxs-lookup"><span data-stu-id="f043f-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="f043f-175">Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser* hello parola düz metin birlikte (*değil* önerilen):</span><span class="sxs-lookup"><span data-stu-id="f043f-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="f043f-176">Toohello makine dağıtmış olan bir sertifikayı kullanarak hello parolayı şifrelemek öneririz.</span><span class="sxs-lookup"><span data-stu-id="f043f-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="f043f-177">Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser*, burada hello parola adı verilen bir sertifika kullanılarak şifrelenmiş *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="f043f-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="f043f-178">Merhaba kullanabilirsiniz `Invoke-ServiceFabricEncryptText` PowerShell komut toocreate hello gizli şifreli metin hello parolası.</span><span class="sxs-lookup"><span data-stu-id="f043f-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="f043f-179">Daha fazla bilgi için hello makalesine bakın [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="f043f-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="f043f-180">Merhaba toodecrypt hello parola kullandı hello sertifikasının özel anahtarı yerel makinede bir bant dışı yöntem dağıtılan toohello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f043f-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="f043f-181">(Azure'da, Azure Resource Manager bu yöntem budur.) Ardından, Service Fabric hello hizmet paketi toohello makine dağıtırken hello gizli şifresini çözebilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="f043f-182">Merhaba gizli hello hesap adı ile birlikte kullanarak, onu hello kapsayıcı deposuyla sonra doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="f043f-183">Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f043f-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="f043f-184">Belirterek hello kapsayıcı ile bir ana bilgisayar kullanılan bağlantı noktası toocommunicate yapılandırabilirsiniz bir `PortBinding` hello uygulama bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="f043f-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="f043f-185">Merhaba kapsayıcı tooa bağlantı hello konaktaki içinde dinleyen bir Hello bağlantı noktası bağlama eşlemeleri hello bağlantı noktası toowhich hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="f043f-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="f043f-186">Kapsayıcıya bulma ve iletişim yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f043f-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="f043f-187">Hello kullanarak `PortBinding` İlkesi, bir kapsayıcı bağlantı noktası tooan eşleyebilirsiniz `Endpoint` hello hizmet bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="f043f-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="f043f-188">uç nokta hello `Endpoint1` sabit bir bağlantı noktası (örneğin, bağlantı noktası 80) belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f043f-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="f043f-189">Rastgele bir bağlantı noktası hello kümenin uygulama bağlantı noktası aralığından sizin için bu durumda seçilen bağlantı noktası yok hiç da belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="f043f-190">Bir uç nokta belirtirseniz, hello kullanarak `Endpoint` hello hizmet bildirimi Konuk kapsayıcı, Service Fabric etiketinde otomatik olarak bu uç nokta toohello adlandırma hizmeti yayımlama.</span><span class="sxs-lookup"><span data-stu-id="f043f-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="f043f-191">Merhaba kümede çalışan diğer hizmetler, böylece çözümlemek için hello REST sorgularını kullanarak bu kapsayıcı bulabilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="f043f-192">Merhaba Naming service ile kaydederek kolayca hello kod-kapsayıcıya iletişiminde, kapsayıcı içinde hello kullanarak yapabileceğiniz [ters proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="f043f-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="f043f-193">İletişim hello ters proxy http dinleme bağlantı noktası ve ortam değişkenleri olarak toocommunicate ile istediğiniz hello Hizmetleri hello adını sağlayarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="f043f-194">Daha fazla bilgi için hello sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="f043f-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="f043f-195">Ortam değişkenlerini yapılandırma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="f043f-195">Configure and set environment variables</span></span>
<span data-ttu-id="f043f-196">Ortam değişkenleri, her kod paketi bildiriminde hello hizmet, hem kapsayıcılarında dağıtılan Hizmetleri ya da işlemler/Konuk yürütülebilir dosyaları dağıtılan Hizmetleri için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="f043f-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="f043f-197">Bu ortam değişkeni değerlerini özellikle hello uygulama bildiriminde geçersiz veya uygulama parametreleri olarak dağıtım sırasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="f043f-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="f043f-198">Merhaba aşağıdaki hizmet bildirim XML parçacığını gösterir nasıl bir örneği için bir kod paketi toospecify ortam değişkenleri:</span><span class="sxs-lookup"><span data-stu-id="f043f-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="f043f-199">Bu ortam değişkenleri hello uygulama bildirim düzeyinde geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="f043f-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="f043f-200">Merhaba önceki örnekte, biz hello için açık bir değer belirtilen `HttpGateway` ortam değişkeni (Merhaba değeri ayarlarız sırada 19000) `BackendServiceName` hello parametresi `[BackendSvc]` uygulama parametresi.</span><span class="sxs-lookup"><span data-stu-id="f043f-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="f043f-201">Bu ayarlar için toospecify hello değer etkinleştirmek `BackendServiceName`değer hello uygulamayı dağıttıktan sonra hello bildiriminde sabit bir değere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="f043f-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="f043f-202">Uygulama ve hizmet bildirimi için örnekler tamamlayın</span><span class="sxs-lookup"><span data-stu-id="f043f-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="f043f-203">Bir örnek uygulama bildirimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f043f-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="f043f-204">Bir örnek hizmet bildirimi (uygulama bildirimi önceki hello belirtilen) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f043f-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f043f-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f043f-205">Next steps</span></span>
<span data-ttu-id="f043f-206">Kapsayıcılı hizmetini dağıttıysanız, bilgi nasıl toomanage okuyarak kendi ömrü [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="f043f-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="f043f-207">Service Fabric ve kapsayıcıları genel bakış</span><span class="sxs-lookup"><span data-stu-id="f043f-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="f043f-208">Hello Azure CLI kullanarak Service Fabric kümeleri ile etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="f043f-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="f043f-209">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="f043f-209">Related articles</span></span>

* [<span data-ttu-id="f043f-210">Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f043f-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="f043f-211">Service Fabric XPlat CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f043f-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
