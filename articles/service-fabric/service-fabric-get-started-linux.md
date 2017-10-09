---
title: "Linux üzerinde geliştirme ortamınızı aaaSet | Microsoft Docs"
description: "Merhaba çalışma zamanı ve SDK'sını yükleyin ve Linux üzerinde yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra hazır toobuild uygulamalar olur."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="90a22-104">Linux üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="90a22-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90a22-105">Windows</span><span class="sxs-lookup"><span data-stu-id="90a22-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="90a22-106">Linux</span><span class="sxs-lookup"><span data-stu-id="90a22-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="90a22-107">OSX</span><span class="sxs-lookup"><span data-stu-id="90a22-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="90a22-108">toodeploy çalıştırıp [Azure Service Fabric uygulamaları](service-fabric-application-model.md) hello çalışma zamanı ve ortak SDK Linux geliştirme makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="90a22-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="90a22-109">Ayrıca isteğe bağlı Java ve .NET Core SDK’larını yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90a22-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90a22-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="90a22-110">Prerequisites</span></span>

<span data-ttu-id="90a22-111">işletim sistemi sürümleri aşağıdaki hello geliştirme için desteklenir:</span><span class="sxs-lookup"><span data-stu-id="90a22-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="90a22-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="90a22-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="90a22-113">APT kaynaklarınızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="90a22-113">Update your APT sources</span></span>
<span data-ttu-id="90a22-114">tooinstall hello SDK ve hello ilişkili çalışma zamanı paketi üzerinden hello get apt komut satırı aracı, Gelişmiş paketleme Aracı (APT) kaynaklarınızı önce güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a22-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="90a22-115">Bir terminal açın.</span><span class="sxs-lookup"><span data-stu-id="90a22-115">Open a terminal.</span></span>
2. <span data-ttu-id="90a22-116">Merhaba Service Fabric depodaki tooyour kaynakları listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90a22-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="90a22-117">Merhaba eklemek `dotnet` depodaki tooyour kaynakları listesi.</span><span class="sxs-lookup"><span data-stu-id="90a22-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="90a22-118">Merhaba ekleme yeni Gnu gizlilik Guard (GnuPG veya GPG) tooyour APT keyring anahtar.</span><span class="sxs-lookup"><span data-stu-id="90a22-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="90a22-119">Merhaba resmi Docker GPG anahtar tooyour APT keyring ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90a22-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="90a22-120">Merhaba Docker deposu ayarlama.</span><span class="sxs-lookup"><span data-stu-id="90a22-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="90a22-121">Paketinizi Yenile eklenen depoları hello üzerinde yeni göre listeler.</span><span class="sxs-lookup"><span data-stu-id="90a22-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="90a22-122">Yükleme ve hello SDK yerel Küme kurulumu için ayarlama</span><span class="sxs-lookup"><span data-stu-id="90a22-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="90a22-123">Kaynaklarınızın güncelleştirildikten sonra hello SDK yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90a22-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="90a22-124">Merhaba Service Fabric SDK paketini yükleyin, hello yükleme onaylayın ve toohello Lisans Sözleşmesi'ni kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="90a22-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="90a22-125">Merhaba aşağıdaki komutları kabul hello lisans Service Fabric paketler için otomatikleştirin:</span><span class="sxs-lookup"><span data-stu-id="90a22-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="90a22-126">Yerel küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="90a22-126">Set up a local cluster</span></span>
  <span data-ttu-id="90a22-127">Merhaba yükleme başarılı olursa, mümkün toostart yerel bir küme olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90a22-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="90a22-128">Merhaba Küme kurulumu betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="90a22-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="90a22-129">Bir web tarayıcısı açın ve çok Git[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="90a22-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="90a22-130">Merhaba küme başlatılmış olup olmadığını hello Service Fabric Explorer Pano görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a22-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Linux üzerinde Service Fabric Explorer][sfx-linux]

  <span data-ttu-id="90a22-132">Bu noktada, önceden oluşturulmuş Service Fabric uygulama paketlerini ve yeni paketleri konuk kapsayıcılar veya konuk yürütülebilir öğelere göre dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90a22-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="90a22-133">Merhaba Java veya .NET Core SDK kullanarak toobuild yeni hizmetler, sonraki bölümlerde verilmiştir hello isteğe bağlı kurulum adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="90a22-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="90a22-134">Tek başına kümeler Linux’da desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="90a22-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="90a22-135">Merhaba Önizleme destekler yalnızca bir kutusunu ve Azure Linux çoklu makine kümeleri.</span><span class="sxs-lookup"><span data-stu-id="90a22-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="90a22-136">Service Fabric CLI Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="90a22-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="90a22-137">Merhaba [Service Fabric CLI](service-fabric-cli.md) kümeleri ve uygulamalar dahil olmak üzere Service Fabric varlıkları ile etkileşim için komut yok.</span><span class="sxs-lookup"><span data-stu-id="90a22-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="90a22-138">Python üzerinde dayanır, bu nedenle toohave python ve PIP komutu aşağıdaki hello ile devam etmeden önce yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="90a22-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="90a22-139">Yükleme ve hello oluşturucuları kapsayıcıları ve Konuk yürütülebilir dosyalar için ayarlama</span><span class="sxs-lookup"><span data-stu-id="90a22-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="90a22-140">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulamaları oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="90a22-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="90a22-141">Lütfen makinenizde çalışmak için hello Service Fabric yeoman şablon oluşturucu sahip tooensure hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="90a22-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="90a22-142">Makinenize nodejs ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="90a22-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="90a22-143">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="90a22-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="90a22-144">Merhaba Service Fabric Yeo kapsayıcı oluşturucu ve Konuk execuatble Oluşturucu NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="90a22-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="90a22-145">Merhaba oluşturucuları yukarıda yükledikten sonra çalıştırarak Konuk çalıştırılabilir veya kapsayıcı Hizmetleri mümkün toocreate uygulamalarla olmalıdır `yo azuresfguest` veya `yo azuresfcontainer` sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="90a22-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="90a22-146">Merhaba gerekli Java yapıları (isteğe bağlı, modelleri programlama toouse hello Java istiyorsanız) yükleyin</span><span class="sxs-lookup"><span data-stu-id="90a22-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="90a22-147">Java kullanarak toobuild Service Fabric Hizmetleri emin olun JDK derleme görevleri çalıştırmak için kullanılan Gradle ile birlikte yüklenen 1.8.</span><span class="sxs-lookup"><span data-stu-id="90a22-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="90a22-148">Aşağıdaki kod parçacığında hello açık JDK 1.8 Gradle birlikte yükler.</span><span class="sxs-lookup"><span data-stu-id="90a22-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="90a22-149">Merhaba Service Fabric Java kitaplıkları Maven alınır.</span><span class="sxs-lookup"><span data-stu-id="90a22-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="90a22-150">Merhaba Eclipse Neon eklentisini yükleyin (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="90a22-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="90a22-151">Hizmet yapıdan için hello içinde hello Eclipse eklenti yükleyebilirsiniz **Java geliştiricileri için Eclipse IDE**.</span><span class="sxs-lookup"><span data-stu-id="90a22-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="90a22-152">Toplama tooService doku Java uygulamaları Eclipse toocreate Service Fabric Konuk yürütülebilir uygulamalar ve kapsayıcı uygulamaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90a22-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="90a22-153">Eclipse'te, en son Eclipse Neon olduğundan ve en son Buildship sürümü hello emin olun (1.0.17 veya sonraki bir sürümü) yüklü.</span><span class="sxs-lookup"><span data-stu-id="90a22-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="90a22-154">Seçerek yüklü bileşenlerin hello sürümlerini kontrol edebilirsiniz **yardımcı** > **Yükleme ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="90a22-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="90a22-155">Merhaba yönergeleri kullanarak Buildship güncelleştirebilirsiniz [Eclipse Buildship: Eclipse için eklentilerini Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="90a22-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="90a22-156">tooinstall hello Service Fabric eklentisini seçin **yardımcı** > **yeni yazılımı yükle**.</span><span class="sxs-lookup"><span data-stu-id="90a22-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="90a22-157">Merhaba, **çalışmak** kutusuna **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="90a22-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="90a22-158">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90a22-158">Click **Add**.</span></span>

    ![Merhaba kullanılabilir yazılım sayfası][sf-eclipse-plugin]

5. <span data-ttu-id="90a22-160">Select hello **ServiceFabric** eklentisi ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="90a22-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="90a22-161">Merhaba yükleme adımlarını tamamlayın ve hello son kullanıcı lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="90a22-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="90a22-162">Hello Service Fabric yüklü Eclipse eklenti zaten varsa, hello en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="90a22-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="90a22-163">Seçerek kontrol **yardımcı** > **Yükleme ayrıntıları** ve ardından için Service Fabric hello listesinde arama yüklü eklentileri. Daha yeni bir sürüm varsa, **Güncelleştir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="90a22-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="90a22-164">Daha fazla bilgi için bkz. [Eclipse Java uygulama geliştirmesi için Service Fabric eklentisi](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="90a22-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="90a22-165">Merhaba .NET Core SDK (isteğe bağlı, toouse hello .NET Core programlama modelleri istiyorsanız) yükleyin</span><span class="sxs-lookup"><span data-stu-id="90a22-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="90a22-166">Merhaba .NET Core SDK hello kitaplıkları ve gerekli toobuild Service Fabric .NET Core hizmetleriyle şablonlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="90a22-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="90a22-167">Merhaba .NET Core SDK paketini çalışan hello aşağıdaki tarafından yükle-</span><span class="sxs-lookup"><span data-stu-id="90a22-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="90a22-168">Güncelleştirme hello SDK ve çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="90a22-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="90a22-169">tooupdate toohello ve en son sürümünü hello SDK çalışma zamanı, hello aşağıdaki komutları çalıştırın (istemediğiniz hello SDK'ları seçimini kaldırın):</span><span class="sxs-lookup"><span data-stu-id="90a22-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="90a22-170">tooupdate hello Java SDK'sı ikili Maven gelen tooupdate hello sürüm hello karşılık gelen ikili hello ayrıntılarını ihtiyacınız ``build.gradle`` dosya toopoint toohello en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="90a22-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="90a22-171">tam olarak tooupdate hello sürüm, ihtiyaç duyacağınız tooknow tooany başvurabilir ``build.gradle`` Service Fabric başlama örnekleri dosyasında [burada](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="90a22-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="90a22-172">Merhaba paketleri güncelleştiriliyor çalıştıran, yerel geliştirme küme toostop neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="90a22-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="90a22-173">Yerel kümenizdeki, bu sayfada hello yönergeleri izleyerek bir yükseltmeden sonra yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="90a22-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90a22-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90a22-174">Next steps</span></span>

* [<span data-ttu-id="90a22-175">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="90a22-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="90a22-176">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="90a22-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="90a22-177">Linux üzerinde ilk CSharp uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90a22-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="90a22-178">OSX üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="90a22-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="90a22-179">Merhaba Service Fabric CLI toomanage uygulamalarınızı kullanın</span><span class="sxs-lookup"><span data-stu-id="90a22-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="90a22-180">Service Fabric Windows/Linux farkları</span><span class="sxs-lookup"><span data-stu-id="90a22-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="90a22-181">Service Fabric CLI kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="90a22-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
