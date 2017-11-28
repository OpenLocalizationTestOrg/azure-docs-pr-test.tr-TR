---
title: "Service Fabric ve Linux dağıtma kapsayıcılarında | Microsoft Docs"
description: "Service Fabric ve Linux kapsayıcıları kullanımını mikro hizmet uygulamalarını dağıtmak için. Bu makalede kapsayıcıları için Service Fabric sağlayan özellikleri ve bir küme içinde Linux kapsayıcı görüntü dağıtma"
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
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a><span data-ttu-id="3117d-104">Service Fabric Linux kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3117d-104">Deploy a Linux container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3117d-105">Windows kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3117d-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="3117d-106">Linux kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3117d-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="3117d-107">Bu makalede Linux'ta Docker kapsayıcılarında kapsayıcılı hizmetleri oluşturma sürecinde anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3117d-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="3117d-108">Service Fabric oluşan kapsayıcılı, mikro uygulamaları oluşturmaya yardımcı birkaç kapsayıcı özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="3117d-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="3117d-109">Bu hizmetler kapsayıcılı Hizmetleri olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3117d-109">These services are called containerized services.</span></span>

<span data-ttu-id="3117d-110">Yetenekler içerir;</span><span class="sxs-lookup"><span data-stu-id="3117d-110">The capabilities include;</span></span>

* <span data-ttu-id="3117d-111">Kapsayıcı görüntü dağıtımı ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3117d-111">Container image deployment and activation</span></span>
* <span data-ttu-id="3117d-112">Kaynak İdaresi</span><span class="sxs-lookup"><span data-stu-id="3117d-112">Resource governance</span></span>
* <span data-ttu-id="3117d-113">Depo kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3117d-113">Repository authentication</span></span>
* <span data-ttu-id="3117d-114">Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme</span><span class="sxs-lookup"><span data-stu-id="3117d-114">Container port to host port mapping</span></span>
* <span data-ttu-id="3117d-115">Kapsayıcıya bulma ve iletişim</span><span class="sxs-lookup"><span data-stu-id="3117d-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="3117d-116">Yapılandırma ve ortam değişkenlerini ayarlama özelliği</span><span class="sxs-lookup"><span data-stu-id="3117d-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="3117d-117">Docker kapsayıcısı ile yeoman paketleme</span><span class="sxs-lookup"><span data-stu-id="3117d-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="3117d-118">Linux üzerinde bir kapsayıcı paketleme, yeoman şablon kullanılacağını seçebilirsiniz veya [uygulama paketini el ile oluşturmak](#manually).</span><span class="sxs-lookup"><span data-stu-id="3117d-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="3117d-119">Service Fabric uygulaması her uygulamanın işlevselliğini aktarma konusunda belirli bir rol ile bir veya daha fazla kapsayıcıları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="3117d-120">Linux için Service Fabric SDK’sı uygulamanızı oluşturmayı ve kapsayıcı görüntüsü eklemeyi kolaylaştıran bir [Yeoman](http://yeoman.io/) oluşturucu içerir.</span><span class="sxs-lookup"><span data-stu-id="3117d-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="3117d-121">Şimdi Yeoman kullanarak *SimpleContainerApp* adlı tek bir Docker kapsayıcısı olan bir uygulama oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3117d-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="3117d-122">Daha fazla hizmet daha sonra oluşturulan düzenleyerek dosyaları bildirim ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3117d-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="3117d-123">Docker geliştirme kutunuzun yükleyin</span><span class="sxs-lookup"><span data-stu-id="3117d-123">Install Docker on your development box</span></span>

<span data-ttu-id="3117d-124">Linux geliştirme kutusundaki docker yüklemek için aşağıdaki komutları çalıştırın (OSX üzerinde vagrant görüntüsü kullanıyorsanız, docker zaten yüklü):</span><span class="sxs-lookup"><span data-stu-id="3117d-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="3117d-125">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="3117d-125">Create the application</span></span>
1. <span data-ttu-id="3117d-126">Bir terminal penceresinde `yo azuresfcontainer` yazın.</span><span class="sxs-lookup"><span data-stu-id="3117d-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="3117d-127">Örneğin, mycontainerap uygulamanızın - adı</span><span class="sxs-lookup"><span data-stu-id="3117d-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="3117d-128">DockerHub depodaki kapsayıcı görüntüden için URL'sini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3117d-128">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="3117d-129">Görüntü parametresi [repo] biçimini alır / [görüntü adı]</span><span class="sxs-lookup"><span data-stu-id="3117d-129">The image parameter takes the form [repo]/[image name]</span></span>
4. <span data-ttu-id="3117d-130">Görüntüyü yeniden başlatma işleminden sonra çalışan kapsayıcı tutar kapsayıcı içinde çalıştırılacak komutları virgülle ayrılmış bir dizi giriş komutları açıkça belirtmek gerekiyor bir iş yükü giriş tanımlanmış noktası yoksa.</span><span class="sxs-lookup"><span data-stu-id="3117d-130">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="3117d-132">Uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3117d-132">Deploy the application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="3117d-133">XPlat CLI aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="3117d-133">Using XPlat CLI</span></span>
<span data-ttu-id="3117d-134">Uygulama oluşturulduktan sonra Azure CLI kullanarak yerel kümeye dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3117d-134">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="3117d-135">Yerel Service Fabric kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3117d-135">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="3117d-136">Uygulama paketini kümenin görüntü deposuna kopyalamak, uygulama türünü kaydetmek ve uygulamanın bir örneğini oluşturmak için şablonda verilen yükleme betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3117d-136">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="3117d-137">Bir tarayıcı açın ve http://localhost:19080/Explorer adresindeki Service Fabric Explorer’a gidin (Vagrant’ı Mac OS X üzerinde kullanıyorsanız localhost ifadesini sanal makinenin özel IP’si ile değiştirin).</span><span class="sxs-lookup"><span data-stu-id="3117d-137">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="3117d-138">Uygulamalar düğümünü genişletin ve şu anda uygulamanızın türü için bir giriş ve bu türün ilk örneği için başka bir giriş olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3117d-138">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="3117d-139">Uygulama örneğini silin ve uygulama türü kaydını kaldırma için şablonda belirtilen kaldırma komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="3117d-139">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="3117d-140">Azure CLI 2.0 aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="3117d-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="3117d-141">Başvuru belge yönetme hakkında bkz bir [Azure CLI 2.0 kullanan uygulama yaşam döngüsü](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="3117d-141">See the reference doc on managing an [application life cycle using the Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="3117d-142">Örnek bir uygulama için [checkout Service Fabric kapsayıcı kodu Github'da örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="3117d-142">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="3117d-143">Mevcut bir uygulamaya daha fazla hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="3117d-143">Adding more services to an existing application</span></span>

<span data-ttu-id="3117d-144">Başka bir kapsayıcı hizmeti zaten kullanılarak oluşturulmuş bir uygulama eklemek için `yo`, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3117d-144">To add another container service to an application already created using `yo`, perform the following steps:</span></span>

1. <span data-ttu-id="3117d-145">Dizini mevcut uygulamanın kök dizinine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3117d-145">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="3117d-146">Örneğin Yeoman tarafından oluşturulan uygulama `MyApplication` ise `cd ~/YeomanSamples/MyApplication` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3117d-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="3117d-147">`yo azuresfcontainer:AddService` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3117d-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="3117d-148">El ile paketini ve kapsayıcı görüntüsünü Dağıt</span><span class="sxs-lookup"><span data-stu-id="3117d-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="3117d-149">El ile kapsayıcılı hizmet paketleme işlemi aşağıdaki adımları dayanır:</span><span class="sxs-lookup"><span data-stu-id="3117d-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="3117d-150">Kapsayıcılar deponuza yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="3117d-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="3117d-151">Paket dizin yapısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3117d-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="3117d-152">Hizmet bildirim dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3117d-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="3117d-153">Uygulama bildirim dosyasının düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3117d-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="3117d-154">Dağıtma ve kapsayıcı görüntü etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="3117d-154">Deploy and activate a container image</span></span>
<span data-ttu-id="3117d-155">Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3117d-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="3117d-156">Dağıtma ve bir kapsayıcı etkinleştirmek için kapsayıcı görüntüsüne adını put bir `ContainerHost` hizmet bildiriminde öğesi.</span><span class="sxs-lookup"><span data-stu-id="3117d-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="3117d-157">Hizmet bildiriminde eklemek bir `ContainerHost` giriş noktası için.</span><span class="sxs-lookup"><span data-stu-id="3117d-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="3117d-158">Ardından `ImageName` kapsayıcı depo ve görüntü adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3117d-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="3117d-159">Aşağıdaki kısmi bildirimi adlı kapsayıcıyı dağıtmak nasıl bir örneği gösterir `myimage:v1` adlı bir depodan `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="3117d-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="3117d-160">İsteğe bağlı belirterek giriş komutları sağlayabilir `Commands` öğe kapsayıcısı içindeki çalıştırılacak komutları virgülle ayrılmış bir dizi.</span><span class="sxs-lookup"><span data-stu-id="3117d-160">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

> [!NOTE]
> <span data-ttu-id="3117d-161">Görüntünün bir iş yükü giriş tanımlanmış noktası yok sonra içindeki giriş komutları açıkça belirtmek zorunda `Commands` başlatma işleminden sonra çalışan kapsayıcı tutar kapsayıcı içinde çalıştırılacak komutları virgülle ayrılmış bir dizi öğesi.</span><span class="sxs-lookup"><span data-stu-id="3117d-161">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands inside `Commands` element with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="3117d-162">Kaynak İdaresi anlama</span><span class="sxs-lookup"><span data-stu-id="3117d-162">Understand resource governance</span></span>
<span data-ttu-id="3117d-163">Kaynak İdaresi kapsayıcı konakta kullanabilirsiniz kaynakları kısıtlayan kapsayıcısının bir yetenektir.</span><span class="sxs-lookup"><span data-stu-id="3117d-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="3117d-164">`ResourceGovernancePolicy`, Bir hizmet kod paketi için kaynak sınırları bildirmek için hangi uygulama bildiriminde belirtilen kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3117d-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="3117d-165">Aşağıdaki kaynaklar için kaynak sınırlarını ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3117d-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="3117d-166">Bellek</span><span class="sxs-lookup"><span data-stu-id="3117d-166">Memory</span></span>
* <span data-ttu-id="3117d-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="3117d-167">MemorySwap</span></span>
* <span data-ttu-id="3117d-168">CpuShares (CPU göreli ağırlık)</span><span class="sxs-lookup"><span data-stu-id="3117d-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="3117d-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="3117d-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="3117d-170">BlkioWeight (BlockIO göreli ağırlık).</span><span class="sxs-lookup"><span data-stu-id="3117d-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="3117d-171">Gelecekteki bir sürümde, IOPS gibi belirli blok g/ç sınırları belirtmek için destek BPS okuma/yazma ve diğerleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="3117d-172">Bir depo kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3117d-172">Authenticate a repository</span></span>
<span data-ttu-id="3117d-173">Bir kapsayıcı indirmek için kapsayıcı deponuza oturum açma kimlik bilgilerini sağlamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="3117d-174">Uygulama bildiriminde belirtilen oturum açma kimlik bilgileri, oturum açma bilgileri veya kapsayıcı görüntünün görüntü deposundan karşıdan yüklemek için SSH anahtarı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3117d-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="3117d-175">Adlı bir hesap aşağıdaki örnekte *TestUser* düz metin parolayı birlikte (*değil* önerilen):</span><span class="sxs-lookup"><span data-stu-id="3117d-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="3117d-176">Makineye dağıtılan bir sertifika kullanarak parolayı şifrelemek öneririz.</span><span class="sxs-lookup"><span data-stu-id="3117d-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="3117d-177">Adlı bir hesap aşağıdaki örnekte *TestUser*, adı verilen bir sertifikayı kullanarak parolayı nerede şifrelenmiş *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="3117d-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="3117d-178">Kullanabileceğiniz `Invoke-ServiceFabricEncryptText` gizli şifreli metin parolası oluşturmak için PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="3117d-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="3117d-179">Daha fazla bilgi için bkz: [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="3117d-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="3117d-180">Parola şifresini çözmek için kullanılan sertifikanın özel anahtarı yerel makinede bir bant dışı yöntem dağıtılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3117d-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="3117d-181">(Azure'da, Azure Resource Manager bu yöntem budur.) Ardından, Service Fabric makineye hizmet paketini dağıtırken, gizli şifresini çözebilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="3117d-182">Gizli hesap adı ile birlikte kullanarak, bu kapsayıcı deposuyla sonra doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="3117d-183">Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3117d-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="3117d-184">Belirterek kapsayıcı ile iletişim kurmak için kullanılan bir ana bilgisayar bağlantı noktası yapılandırabilirsiniz bir `PortBinding` uygulama bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="3117d-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="3117d-185">Hizmet bağlantı noktası ana bilgisayardaki kapsayıcıya içinde dinleme yaptığı bağlantı bağlantı noktası bağlamasına eşler.</span><span class="sxs-lookup"><span data-stu-id="3117d-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="3117d-186">Kapsayıcıya bulma ve iletişim yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3117d-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="3117d-187">Kullanarak `PortBinding` İlkesi, bir kapsayıcı bağlantı noktasına eşlenebilir bir `Endpoint` hizmet bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="3117d-187">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="3117d-188">Uç nokta `Endpoint1` sabit bir bağlantı noktası (örneğin, bağlantı noktası 80) belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3117d-188">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="3117d-189">Kümenin uygulama bağlantı noktası aralığından rastgele bir bağlantı noktası sizin için bu durumda seçilen bağlantı noktası yok hiç da belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="3117d-190">Bir uç nokta belirtirseniz, kullanarak `Endpoint` Konuk kapsayıcı, Service Fabric hizmet bildirimi etiketinde adlandırma hizmeti bu bitiş noktası otomatik olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3117d-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="3117d-191">Kümede çalışan diğer hizmetler, böylece çözümlemek için REST sorgularını kullanarak bu kapsayıcı bulabilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="3117d-192">Adlandırma Hizmeti ile kaydetme tarafından kolayca kod-kapsayıcıya iletişiminde kapsayıcı içinde kullanarak yapabileceğiniz [ters proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="3117d-192">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="3117d-193">İletişim ters proxy http dinleme bağlantı noktası ve ortam değişkenleri olarak iletişim kurması için istediğiniz hizmetleri adını sağlayarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="3117d-194">Daha fazla bilgi için sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="3117d-194">For more information, see the next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="3117d-195">Ortam değişkenlerini yapılandırma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="3117d-195">Configure and set environment variables</span></span>
<span data-ttu-id="3117d-196">Ortam değişkenleri hizmet bildiriminde hem işlemler/Konuk yürütülebilir dosyaları dağıtılan Hizmetleri veya kapsayıcılarında dağıtılan Hizmetleri için her kod paketi için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3117d-196">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="3117d-197">Bu ortam değişkeni değerlerini özellikle uygulama bildiriminde geçersiz veya uygulama parametreleri olarak dağıtım sırasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="3117d-197">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="3117d-198">Aşağıdaki hizmet bildirimi XML kod parçacığı, kod paketi için ortam değişkenlerinin nasıl belirtileceğini gösteren bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="3117d-198">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="3117d-199">Bu ortam değişkenleri uygulama bildirim düzeyinde geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="3117d-199">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="3117d-200">Önceki örnekte, biz açık bir değer için belirtilen `HttpGateway` ortam değişkeni (19000), değeri ayarlarız sırada `BackendServiceName` parametresi ile `[BackendSvc]` uygulama parametresi.</span><span class="sxs-lookup"><span data-stu-id="3117d-200">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="3117d-201">Bu ayarları için değer belirtmenizi sağlayan `BackendServiceName`değer uygulamayı dağıttıktan sonra bildiriminde sabit bir değere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="3117d-201">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="3117d-202">Uygulama ve hizmet bildirimi için örnekler tamamlayın</span><span class="sxs-lookup"><span data-stu-id="3117d-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="3117d-203">Bir örnek uygulama bildirimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3117d-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="3117d-204">Bir örnek hizmet bildirimi (önceki uygulama bildiriminde belirtilen) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3117d-204">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3117d-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3117d-205">Next steps</span></span>
<span data-ttu-id="3117d-206">Kapsayıcılı hizmetini dağıttıysanız, kendi ömrü okuyarak yönetmeyi öğrenin [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="3117d-206">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="3117d-207">Service Fabric ve kapsayıcıları genel bakış</span><span class="sxs-lookup"><span data-stu-id="3117d-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="3117d-208">Azure CLI kullanarak Service Fabric kümeleriyle etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="3117d-208">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="3117d-209">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="3117d-209">Related articles</span></span>

* [<span data-ttu-id="3117d-210">Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3117d-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="3117d-211">Service Fabric XPlat CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3117d-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
