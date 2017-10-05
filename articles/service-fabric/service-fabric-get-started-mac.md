---
title: "Azure Service Fabric ile çalışmak için Mac OS X’te geliştirme ortamınızı ayarlama | Microsoft Docs"
description: "Çalışma zamanını, SDK'yı ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra Mac OS X üzerinde uygulama derlemek için hazır hale gelirsiniz."
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
ms.openlocfilehash: 8b4fc0ab9034263418cac42ced203035e0a8fcad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="22786-104">Mac OS X’te geliştirme ortamınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="22786-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22786-105">Windows</span><span class="sxs-lookup"><span data-stu-id="22786-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="22786-106">Linux</span><span class="sxs-lookup"><span data-stu-id="22786-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="22786-107">OSX</span><span class="sxs-lookup"><span data-stu-id="22786-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="22786-108">Mac OS X kullanarak Linux kümelerinde çalışacak Service Fabric uygulamaları derleyebilirsiniz. Bu makalede Mac’inizi geliştirme için nasıl ayarlayacağınız ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="22786-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22786-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="22786-109">Prerequisites</span></span>
<span data-ttu-id="22786-110">Service Fabric, OS X üzerinde yerel olarak çalışmaz. Yerel bir Service Fabric kümesini çalıştırmak için Vagrant ve VirtualBox kullanarak önceden yapılandırılmış bir Ubuntu sanal makinesi sağlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="22786-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="22786-111">Başlamadan önce şunlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="22786-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="22786-112">Vagrant (v1.8.4 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="22786-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="22786-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="22786-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="22786-114">Birbirini destekleyen Vagrant ve VirtualBox sürümleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="22786-114">You need to use mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="22786-115">Vagrant desteklenmeyen bir VirtualBox sürümünde kararsız davranabilir.</span><span class="sxs-lookup"><span data-stu-id="22786-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-the-local-vm"></a><span data-ttu-id="22786-116">Yerel sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="22786-116">Create the local VM</span></span>
<span data-ttu-id="22786-117">5 düğümlü Service Fabric kümesini içeren yerel bir sanal makine oluşturmak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="22786-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span></span>

1. <span data-ttu-id="22786-118">`Vagrantfile` deposunu kopyalama</span><span class="sxs-lookup"><span data-stu-id="22786-118">Clone the `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="22786-119">Bu adımlar VM yapılandırması ile birlikte VM’nin indirildiği konumu içeren `Vagrantfile` dosyasını getirir.</span><span class="sxs-lookup"><span data-stu-id="22786-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span></span>

2. <span data-ttu-id="22786-120">Deponun yerel kopyasına gidin</span><span class="sxs-lookup"><span data-stu-id="22786-120">Navigate to the local clone of the repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="22786-121">(İsteğe bağlı) Varsayılan sanal makine ayarlarını değiştirin</span><span class="sxs-lookup"><span data-stu-id="22786-121">(Optional) Modify the default VM settings</span></span>

    <span data-ttu-id="22786-122">Varsayılan olarak, yerel sanal makine aşağıdaki gibi yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="22786-122">By default, the local VM is configured as follows:</span></span>

   * <span data-ttu-id="22786-123">3 GB ayrılmış bellek</span><span class="sxs-lookup"><span data-stu-id="22786-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="22786-124">Mac ana bilgisayarından trafik geçişini sağlayan 192.168.50.50 numaralı IP’de yapılandırılmış özel ana bilgisayar ağı</span><span class="sxs-lookup"><span data-stu-id="22786-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span></span>

     <span data-ttu-id="22786-125">Bu ayarların her birini değiştirebilir veya `Vagrantfile` içinde VM’ye başka bir yapılandırma ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22786-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span></span> <span data-ttu-id="22786-126">Yapılandırma seçeneklerinin tam listesi için bkz. [Vagrant belgeleri](http://www.vagrantup.com/docs).</span><span class="sxs-lookup"><span data-stu-id="22786-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span></span>
4. <span data-ttu-id="22786-127">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="22786-127">Create the VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="22786-128">Bu adım önceden yapılandırılmış sanal makine görüntüsünü indirir, yerel olarak önyükler ve ardından içinde yerel bir Service Fabric kümesi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="22786-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="22786-129">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="22786-129">You should expect it to take a few minutes.</span></span> <span data-ttu-id="22786-130">Kurulum başarıyla tamamlanırsa çıktıda kümenin başlatıldığını belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="22786-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span></span>

    ![Sanal makine hazırlama sonrasında başlayan küme ayarı][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="22786-132">VM’yi indirmek uzun sürüyorsa, wget veya curl kullanarak ya da bir tarayıcı üzerinden `Vagrantfile` dosyasındaki **config.vm.box_url** tarafından belirtilen bağlantıya giderek indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22786-132">If the VM download is taking a long time, you can download it using wget or curl or through a browser by navigating to the link specified by **config.vm.box_url** in the file `Vagrantfile`.</span></span> <span data-ttu-id="22786-133">Yerel olarak indirdikten sonra, `Vagrantfile` öğesini, görüntüyü indirdiğiniz yerel yolu işaret edecek şekilde düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="22786-133">After downloading it locally, edit `Vagrantfile` to point to the local path where you downloaded the image.</span></span> <span data-ttu-id="22786-134">Örneğin, görüntüyü /home/users/test/azureservicefabric.tp8.box dizinine indirdiyseniz, **config.vm.box_url** öğesini bu yola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="22786-134">For example if you downloaded the image to /home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** to that path.</span></span>
    >

5. <span data-ttu-id="22786-135">http://192.168.50.50:19080/Explorer adresinde (varsayılan özel ağ IP’sini tuttuğunuzu varsayarak) Service Fabric Explorer’a giderek kümenin doğru ayarlanıp ayarlanmadığını sınayın.</span><span class="sxs-lookup"><span data-stu-id="22786-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span></span>

    ![Ana Mac bilgisayarından görüntülenen Service Fabric Explorer][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="22786-137">Yeoman kullanarak Mac uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="22786-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="22786-138">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="22786-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="22786-139">Lütfen makinenizde çalışan bir Service Fabric yeoman şablon oluşturucu olduğundan emin olmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="22786-139">Please follow the steps below to ensure you have the Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="22786-140">Mac’inizde Node.js ve NPM yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="22786-140">You need to have Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="22786-141">Yüklü değilse, Node.js ve NPM’yi Homebrew kullanarak aşağıdaki gibi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22786-141">If not you can install Node.js and NPM using Homebrew using the following.</span></span> <span data-ttu-id="22786-142">Mac'inizde yüklü Node.js ve NPM sürümlerini denetlemek için ``-v`` seçeneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22786-142">To check the versions of Node.js and NPM installed on your Mac, you can use the ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="22786-143">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="22786-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="22786-144">Başlarken [belgelerinde](service-fabric-get-started-linux.md) bulunan adımları izleyerek kullanmak istediğiniz Yeoman oluşturucuyu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="22786-144">Install the Yeoman generator you want to use, following the steps in the getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="22786-145">Yeoman kullanarak Service Fabric uygulamaları oluşturmak için adımları takip edin.</span><span class="sxs-lookup"><span data-stu-id="22786-145">To create Service Fabric Applications using Yeoman, follow the steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="22786-146">Mac üzerinde bir Service Fabric Java uygulaması oluşturmak için makinenizde JDK 1.8 ve Gradle yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="22786-146">To build a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on the machine.</span></span>


## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="22786-147">Eclipse Neon için Service Fabric eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="22786-147">Install the Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="22786-148">Service Fabric, **Java IDE için Eclipse Neon** için Java hizmetlerini oluşturma, derleme ve dağıtmayı kolaylaştırabilen bir eklenti sağlar.</span><span class="sxs-lookup"><span data-stu-id="22786-148">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="22786-149">Service Fabric Eclipse eklentisini yükleme veya güncelleştirme hakkındaki bu genel [belgede](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) bahsedilen yükleme adımlarını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22786-149">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="22786-150">Varsayılan olarak, oluşturulan uygulamada ``Local.json`` dosyasındaki ``Vagrantfile`` değerinde belirtilen varsayılan IP’yi destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="22786-150">By default we support the default IP as mentioned in the ``Vagrantfile`` in the ``Local.json`` of the generated application.</span></span> <span data-ttu-id="22786-151">Bunu değiştirir ve Vagrant’ı farklı bir IP ile dağıtırsanız lütfen uygulamanızdaki ``Local.json`` dosyasında da IP’yi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="22786-151">In case you change that and deploy Vagrant with a different IP, please update the corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22786-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="22786-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="22786-153">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="22786-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="22786-154">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="22786-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="22786-155">Azure portalında bir Service Fabric kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="22786-155">Create a Service Fabric cluster in the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="22786-156">Azure Resource Manager’ı kullanarak bir Service Fabric kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="22786-156">Create a Service Fabric cluster using the Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="22786-157">Service Fabric uygulama modelini anlama</span><span class="sxs-lookup"><span data-stu-id="22786-157">Understand the Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
