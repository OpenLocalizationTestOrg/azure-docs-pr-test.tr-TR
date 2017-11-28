---
title: "Linux üzerinde geliştirme ortamınızı ayarlama | Microsoft Belgeleri"
description: "Linux üzerinde çalışma zamanını ve SDK'yı yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra uygulama derlemek için hazır hale gelirsiniz."
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
ms.openlocfilehash: 58c6bbbb16d7008e6b573cf8dbc8cf62da9789f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="9ad03-104">Linux üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="9ad03-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ad03-105">Windows</span><span class="sxs-lookup"><span data-stu-id="9ad03-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="9ad03-106">Linux</span><span class="sxs-lookup"><span data-stu-id="9ad03-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="9ad03-107">OSX</span><span class="sxs-lookup"><span data-stu-id="9ad03-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="9ad03-108">Linux geliştirme makinenizde [Azure Service Fabric uygulamaları](service-fabric-application-model.md) dağıtıp çalıştırmak için çalışma zamanını ve ortak SDK'yı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span></span> <span data-ttu-id="9ad03-109">Ayrıca isteğe bağlı Java ve .NET Core SDK’larını yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ad03-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9ad03-110">Prerequisites</span></span>

<span data-ttu-id="9ad03-111">Geliştirme için şu işletim sistemi sürümleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="9ad03-111">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="9ad03-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="9ad03-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="9ad03-113">APT kaynaklarınızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9ad03-113">Update your APT sources</span></span>
<span data-ttu-id="9ad03-114">SDK ve ilişkili çalışma zamanı paketini apt-get komut satırı aracıyla yüklemek için, öncelikle Advanced Packaging Tool (APT) kaynaklarınızı güncelleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-114">To install the SDK and the associated runtime package via the apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="9ad03-115">Bir terminal açın.</span><span class="sxs-lookup"><span data-stu-id="9ad03-115">Open a terminal.</span></span>
2. <span data-ttu-id="9ad03-116">Service Fabric deponuzu kaynaklar listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-116">Add the Service Fabric repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="9ad03-117">`dotnet` deposunu kaynak listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-117">Add the `dotnet` repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="9ad03-118">Yeni Gnu Privacy Guard (GnuPG, veya GPG) anahtarını APT anahtarlığınıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-118">Add the new Gnu Privacy Guard (GnuPG, or GPG) key to your APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="9ad03-119">Resmi Docker GPG anahtarını APT anahtarlığınıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-119">Add the official Docker GPG key to your APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="9ad03-120">Docker deposunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ad03-120">Set up the Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="9ad03-121">Paket listelerinizi yeni eklenen depolara göre yenileyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-121">Refresh your package lists based on the newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-the-sdk-for-local-cluster-setup"></a><span data-ttu-id="9ad03-122">Yerel küme kurulumu için SDK'yı yükleme ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ad03-122">Install and set up the SDK for local cluster setup</span></span>

<span data-ttu-id="9ad03-123">Kaynaklarınızı güncelleştirdikten sonra SDK’yı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-123">After you have updated your sources, you can install the SDK.</span></span> <span data-ttu-id="9ad03-124">Service Fabric SDK paketini yükleyin, yüklemeyi onaylayın ve lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-124">Install the Service Fabric SDK package, confirm the installation, and agree to the license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="9ad03-125">Aşağıdaki komutlar, Service Fabric paketlerine yönelik lisansı kabul etme işlemini otomatik hale getirir:</span><span class="sxs-lookup"><span data-stu-id="9ad03-125">The following commands automate accepting the license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="9ad03-126">Yerel küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ad03-126">Set up a local cluster</span></span>
  <span data-ttu-id="9ad03-127">Yükleme başarılı olduysa, yerel bir kümeyi başlatabilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ad03-127">If the installation is successful, you should be able to start a local cluster.</span></span>

  1. <span data-ttu-id="9ad03-128">Küme kurulum betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9ad03-128">Run the cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="9ad03-129">Bir web tarayıcısı açın ve [Service Fabric Explorer](http://localhost:19080/Explorer) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-129">Open a web browser and go to [Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="9ad03-130">Küme başlatıldıysa Service Fabric Explorer panosunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ad03-130">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span></span>

      ![Linux üzerinde Service Fabric Explorer][sfx-linux]

  <span data-ttu-id="9ad03-132">Bu noktada, önceden oluşturulmuş Service Fabric uygulama paketlerini ve yeni paketleri konuk kapsayıcılar veya konuk yürütülebilir öğelere göre dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="9ad03-133">Java veya .NET Core SDK’larını kullanarak yeni hizmetler oluşturmak için aşağıdaki bölümlerde yer alan kurulum adımlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-133">To build new services by using the Java or .NET Core SDKs, follow the optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="9ad03-134">Tek başına kümeler Linux’da desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9ad03-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="9ad03-135">Önizleme yalnızca tek kutu ve Azure Linux çok makineli kümeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="9ad03-135">The preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-the-service-fabric-cli"></a><span data-ttu-id="9ad03-136">Service Fabric CLI’sını ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ad03-136">Set up the Service Fabric CLI</span></span>

<span data-ttu-id="9ad03-137">[Service Fabric CLI](service-fabric-cli.md) kümeler ve uygulamalar da dahil olmak üzere Service Fabric varlıklarıyla etkileşime yönelik komutlar içerir.</span><span class="sxs-lookup"><span data-stu-id="9ad03-137">The [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="9ad03-138">Python tabanlı olduğundan aşağıdaki komutu kullanmadan önce python ve pip’in yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9ad03-138">It is based on python, so be sure to have python and pip installed before you proceed with the following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-the-generators-for-containers-and-guest-executables"></a><span data-ttu-id="9ad03-139">Kapsayıcılar ve konuk yürütülebilir dosyalar için oluşturucuları yükleme ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ad03-139">Install and set up the generators for containers and guest-executables</span></span>
<span data-ttu-id="9ad03-140">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulamaları oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ad03-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="9ad03-141">Lütfen makinenizde çalışan bir Service Fabric yeoman şablon oluşturucu olduğundan emin olmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-141">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="9ad03-142">Makinenize nodejs ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="9ad03-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="9ad03-143">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="9ad03-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="9ad03-144">NPM’den Service Fabric Yeo kapsayıcı oluşturucusunu ve konuk yürütülebilir dosya oluşturucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="9ad03-144">Install the Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="9ad03-145">Yukarıdaki oluşturucuları yükledikten sonra, sırasıyla `yo azuresfguest` ve `yo azuresfcontainer` komutlarını çalıştırarak konuk yürütülebilir dosyası ya da kapsayıcı hizmetleriyle uygulama oluşturabilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ad03-145">After you have installed the above generators, you should be able to create apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-the-necessary-java-artifacts-optional-if-you-want-to-use-the-java-programming-models"></a><span data-ttu-id="9ad03-146">Gereken Java yapıtlarını yükleme (Java programlama modellerini kullanmak istiyorsanız, isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="9ad03-146">Install the necessary Java artifacts (optional, if you want to use the Java programming models)</span></span>

<span data-ttu-id="9ad03-147">Java kullanarak Service Fabric hizmetleri oluşturmak için, derleme görevlerini çalıştırırken kullanılan Gradle ile birlikte JDK 1.8’in de yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ad03-147">To build Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="9ad03-148">Aşağıdaki kod parçacığı Open JDK 1.8’i ve Gradle’ı birlikte yükler.</span><span class="sxs-lookup"><span data-stu-id="9ad03-148">The following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="9ad03-149">Service Fabric Java kitaplıkları Maven’dan alınır.</span><span class="sxs-lookup"><span data-stu-id="9ad03-149">The Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-the-eclipse-neon-plug-in-optional"></a><span data-ttu-id="9ad03-150">Eclipse Neon eklentisini yükleme (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="9ad03-150">Install the Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="9ad03-151">Service Fabric için Eclipse eklentisini **Java Geliştiricileri için Eclipse IDE** içinden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-151">You can install the Eclipse plug-in for Service Fabric from within the **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="9ad03-152">Eclipse kullanarak, Service Fabric Java uygulamalarına ek olarak Service Fabric konuk yürütülebilir uygulamaları ve kapsayıcı uygulamaları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-152">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span></span>

1. <span data-ttu-id="9ad03-153">Eclipse’te, en son Eclipse Neon ve en son Buildship sürümünün (1.0.17 veya üstü) yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ad03-153">In Eclipse, ensure that you have latest Eclipse Neon and the latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="9ad03-154">**Yardım** > **Yükleme Ayrıntıları**’nı seçerek yüklü bileşenlerin sürümlerini denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-154">You can check the versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="9ad03-155">[Eclipse Buildship: Gradle için Eclipse eklentileri][buildship-update] bölümünde sağlanan yönergelerden yararlanarak Buildship’i güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-155">You can update Buildship by using the instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="9ad03-156">Service Fabric eklentisini yüklemek için **Yardım** > **Yeni Yazılım Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-156">To install the Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="9ad03-157">**Birlikte çalışın** kutusuna şunu yazın: **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="9ad03-157">In the **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="9ad03-158">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ad03-158">Click **Add**.</span></span>

    ![Kullanılabilir Yazılım sayfası][sf-eclipse-plugin]

5. <span data-ttu-id="9ad03-160">**ServiceFabric** eklentisini seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ad03-160">Select the **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="9ad03-161">Yükleme adımlarını tamamlayın ve ardından son kullanıcı lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-161">Complete the installation steps, and then accept the end-user license agreement.</span></span>

<span data-ttu-id="9ad03-162">Service Fabric Eclipse eklentisi zaten yüklüyse, en yeni sürümü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ad03-162">If you already have the Service Fabric Eclipse plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="9ad03-163">**Yardım** > **Yükleme Ayrıntıları**’nı seçip ardından yüklü eklentiler listesinde Service Fabric araması yaparak kontrol edebilirsiniz. Daha yeni bir sürüm varsa, **Güncelleştir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad03-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in the list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="9ad03-164">Daha fazla bilgi için bkz. [Eclipse Java uygulama geliştirmesi için Service Fabric eklentisi](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9ad03-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-the-net-core-sdk-optional-if-you-want-to-use-the-net-core-programming-models"></a><span data-ttu-id="9ad03-165">.NET Core SDK’sını yükleme (.NET Core programlama modellerini kullanmak istiyorsanız, isteğe bağlıdır)</span><span class="sxs-lookup"><span data-stu-id="9ad03-165">Install the .NET Core SDK (optional, if you want to use the .NET Core programming models)</span></span>
<span data-ttu-id="9ad03-166">.NET Core SDK’sı, .NET Core ile Service Fabric hizmetleri oluşturmak için gereken kitaplıkları ve şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ad03-166">The .NET Core SDK provides the libraries and templates that are required to build Service Fabric services with .NET Core.</span></span> <span data-ttu-id="9ad03-167">.NET Core SDK paketini aşağıdakini çalıştırarak yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ad03-167">Install the .NET Core SDK package by running the following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-the-sdk-and-runtime"></a><span data-ttu-id="9ad03-168">SDK ve çalışma zamanını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9ad03-168">Update the SDK and runtime</span></span>

<span data-ttu-id="9ad03-169">SDK ve çalışma zamanının son sürümüne güncelleştirmek için aşağıdaki komutları çalıştırın. (Tercih etmediğiniz SDK'ların seçimini kaldırın.):</span><span class="sxs-lookup"><span data-stu-id="9ad03-169">To update to the latest version of the SDK and runtime, run the following commands (deselect the SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="9ad03-170">Maven’dan alınan Java SDK'sı ikili dosyalarını güncelleştirmek için ``build.gradle`` dosyasında karşılık gelen ikili sürüm ayrıntılarını en son sürüme işaret edecek şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ad03-170">To update the Java SDK binaries from Maven, you need to update the version details of the corresponding binary in the ``build.gradle`` file to point to the latest version.</span></span> <span data-ttu-id="9ad03-171">Sürümü tam olarak nerede güncelleştirmeniz gerektiğini öğrenmek için [buradaki](https://github.com/Azure-Samples/service-fabric-java-getting-started) Service Fabric başlangıç örneklerindeki herhangi bir ``build.gradle`` dosyasına bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ad03-171">To know exactly where you need to update the version, you can refer to any ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="9ad03-172">Paketlerin güncelleştirilmesi, yerel geliştirme kümenizin çalışmayı durdurmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ad03-172">Updating the packages might cause your local development cluster to stop running.</span></span> <span data-ttu-id="9ad03-173">Yükseltme sonrasında bu sayfadaki yönergeleri uygulayarak yerel kümenizi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9ad03-173">Restart your local cluster after an upgrade by following the instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ad03-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ad03-174">Next steps</span></span>

* [<span data-ttu-id="9ad03-175">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="9ad03-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="9ad03-176">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="9ad03-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="9ad03-177">Linux üzerinde ilk CSharp uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ad03-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="9ad03-178">OSX üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="9ad03-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="9ad03-179">Uygulamalarınızı yönetmek için Service Fabric CLI'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="9ad03-179">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="9ad03-180">Service Fabric Windows/Linux farkları</span><span class="sxs-lookup"><span data-stu-id="9ad03-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="9ad03-181">Service Fabric CLI kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9ad03-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
