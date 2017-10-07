---
title: "Azure Service Fabric ile Mac OS X toowork üzerinde geliştirme ortamınızı aaaSet | Microsoft Docs"
description: "Merhaba çalışma zamanı, SDK ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra Mac OS x hazır toobuild uygulamalar olur."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="5733c-104">Mac OS X’te geliştirme ortamınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="5733c-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5733c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="5733c-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="5733c-106">Linux</span><span class="sxs-lookup"><span data-stu-id="5733c-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="5733c-107">OSX</span><span class="sxs-lookup"><span data-stu-id="5733c-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="5733c-108">Mac OS X kullanarak Linux kümelerinde Service Fabric uygulamaları toorun oluşturabilirsiniz. Bu makalede yer almaktadır nasıl tooset Mac geliştirme için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5733c-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5733c-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5733c-109">Prerequisites</span></span>
<span data-ttu-id="5733c-110">Service Fabric OS x toorun üzerinde yerel olarak yerel bir Service Fabric kümesi çalışmaz, Vagrant ve VirtualBox kullanarak önceden yapılandırılmış bir Ubuntu sanal makine sağlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="5733c-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="5733c-111">Başlamadan önce şunlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="5733c-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="5733c-112">Vagrant (v1.8.4 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="5733c-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="5733c-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="5733c-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="5733c-114">Vagrant ve VirtualBox toouse birbirini desteklenen sürümleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="5733c-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="5733c-115">Vagrant desteklenmeyen bir VirtualBox sürümünde kararsız davranabilir.</span><span class="sxs-lookup"><span data-stu-id="5733c-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="5733c-116">Oluşturma yerel VM hello</span><span class="sxs-lookup"><span data-stu-id="5733c-116">Create hello local VM</span></span>
<span data-ttu-id="5733c-117">toocreate 5 düğümlü Service Fabric kümesi içeren yerel VM Merhaba, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5733c-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="5733c-118">Kopya hello `Vagrantfile` deposu</span><span class="sxs-lookup"><span data-stu-id="5733c-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="5733c-119">Bu adımları Getir listeleri hello dosya `Vagrantfile` hello VM içeren yapılandırma hello konumu hello VM ile birlikte gelen indirilir.</span><span class="sxs-lookup"><span data-stu-id="5733c-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="5733c-120">Merhaba depoyu yerel kopyasını toohello gidin</span><span class="sxs-lookup"><span data-stu-id="5733c-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="5733c-121">(İsteğe bağlı) Merhaba varsayılan VM ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="5733c-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="5733c-122">Varsayılan olarak, hello yerel VM aşağıdaki gibi yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="5733c-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="5733c-123">3 GB ayrılmış bellek</span><span class="sxs-lookup"><span data-stu-id="5733c-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="5733c-124">IP 192.168.50.50 yapılandırılmış özel konak ağ trafiğinin hello Mac ana bilgisayardan geçiş etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5733c-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="5733c-125">Bu ayarlardan herhangi birini değiştirmek veya diğer yapılandırma toohello VM hello eklemek `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="5733c-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="5733c-126">Merhaba bkz [Vagrant belgelerine](http://www.vagrantup.com/docs) hello yapılandırma seçeneklerinin tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="5733c-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="5733c-127">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="5733c-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="5733c-128">Bu adım, önceden yapılandırılmış hello VM görüntüsü, yerel olarak ayarlayın ve ardından yerel bir Service Fabric yukarı içinde küme önyükleme indirir.</span><span class="sxs-lookup"><span data-stu-id="5733c-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="5733c-129">Bunu tootake birkaç dakika beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5733c-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="5733c-130">Kurulum başarıyla tamamlarsa, hello çıkışı bu hello küme başlatılıyor belirten bir ileti görür.</span><span class="sxs-lookup"><span data-stu-id="5733c-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![Sanal makine hazırlama sonrasında başlayan küme ayarı][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="5733c-132">Merhaba VM indirme uzun sürüyorsa, wget veya curl kullanarak yükleyebilirsiniz veya toohello bağlantı tarafından belirtilen gezinme tarafından bir tarayıcı aracılığıyla **config.vm.box_url** hello dosyasında `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="5733c-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="5733c-133">Onu yerel olarak indirdikten sonra düzenleme `Vagrantfile` hello görüntü indirdiğiniz toopoint toohello yerel yolu.</span><span class="sxs-lookup"><span data-stu-id="5733c-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="5733c-134">Hello görüntü too/home/users/test/azureservicefabric.tp8.box yüklediyseniz örnek daha sonra ayarlamak için **config.vm.box_url** toothat yolu.</span><span class="sxs-lookup"><span data-stu-id="5733c-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="5733c-135">Bu hello test küme ayarlanmış doğru tooService Fabric Explorer http://192.168.50.50:19080/Explorer (Merhaba varsayılan özel ağ IP tutulan varsayılarak) konumunda giderek.</span><span class="sxs-lookup"><span data-stu-id="5733c-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Service Fabric Explorer Mac hello ana bilgisayardan görüntülenebilir][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="5733c-137">Yeoman kullanarak Mac uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5733c-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="5733c-138">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="5733c-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="5733c-139">Lütfen makinenizde çalışma hello Service Fabric yeoman şablon oluşturucu sahip tooensure hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5733c-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="5733c-140">Toohave Node.js ve NPM, mac üzerinde yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="5733c-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="5733c-141">Aksi durumda, Node.js ve NPM hello aşağıdakileri kullanarak Homebrew kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5733c-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="5733c-142">toocheck hello sürümleri Node.js ve NPM Mac'inizde yüklü, kullanabileceğiniz hello ``-v`` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5733c-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="5733c-143">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="5733c-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="5733c-144">Merhaba Yeoman yükleme Oluşturucu istediğiniz toouse, Başlarken hello hello adımlarını izleyerek [belgelerine](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5733c-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="5733c-145">Yeoman, kullanarak toocreate Service Fabric uygulamaları hello adımları-</span><span class="sxs-lookup"><span data-stu-id="5733c-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="5733c-146">Service Fabric Java uygulaması Mac üzerinde toobuild, ihtiyacınız - JDK 1.8 ve Gradle hello makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="5733c-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="5733c-147">Eclipse Neon Hello Service Fabric eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="5733c-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="5733c-148">Service Fabric sağlayan bir eklenti Merhaba **Java IDE için Eclipse Neon** oluşturma, derleme ve Java Hizmetleri dağıtma hello sürecini basitleştirmek.</span><span class="sxs-lookup"><span data-stu-id="5733c-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="5733c-149">Bu genel bahsedilen hello yükleme adımlarını izleyin [belgelerine](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) yükleme veya Service Fabric Eclipse eklentisi güncelleştirme hakkında.</span><span class="sxs-lookup"><span data-stu-id="5733c-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="5733c-150">Varsayılan olarak hello varsayılan IP hello belirtildiği gibi destekliyoruz ``Vagrantfile`` hello içinde ``Local.json`` oluşturulan hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="5733c-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="5733c-151">Hello karşılık gelen IP değiştirmek ve farklı bir IP Vagrant dağıtma durumunda, lütfen güncelleştirmek ``Local.json`` de uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="5733c-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5733c-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5733c-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="5733c-153">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="5733c-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="5733c-154">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="5733c-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="5733c-155">Hello Azure portalında bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="5733c-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="5733c-156">Azure Resource Manager Hello kullanarak bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="5733c-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="5733c-157">Merhaba Service Fabric uygulama modelini anlama</span><span class="sxs-lookup"><span data-stu-id="5733c-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
