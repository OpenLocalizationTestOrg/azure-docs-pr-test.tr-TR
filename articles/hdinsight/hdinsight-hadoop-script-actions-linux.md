---
title: "Linux tabanlı Hdınsight - Azure ile aaaScript eylem geliştirme | Microsoft Docs"
description: "Nasıl toocustomize Linux tabanlı Hdınsight kümeleri toouse Bash betiklerini öğrenin. Merhaba betik eylemi özelliği hdınsight sırasında veya Küme oluşturulduktan sonra toorun komut dosyaları sağlar. Komut dosyaları, küme yapılandırma ayarlarının kullanılan toochange olması veya ek yazılım yüklemesi."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="89ff4-105">Hdınsight ile betik eylemi geliştirme</span><span class="sxs-lookup"><span data-stu-id="89ff4-105">Script action development with HDInsight</span></span>

<span data-ttu-id="89ff4-106">Bilgi toocustomize Hdınsight küme kullanarak nasıl Bash betikleri.</span><span class="sxs-lookup"><span data-stu-id="89ff4-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="89ff4-107">Betik yolu toocustomize Hdınsight sırasında veya Küme oluşturulduktan sonra eylemlerdir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89ff4-108">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="89ff4-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="89ff4-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="89ff4-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="89ff4-111">Betik eylemleri nelerdir</span><span class="sxs-lookup"><span data-stu-id="89ff4-111">What are script actions</span></span>

<span data-ttu-id="89ff4-112">Betik eylemleri hello küme düğümleri toomake yapılandırma değişiklikleri Azure çalışır Bash betikleridir veya yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="89ff4-113">Betik eylemi kök olarak yürütülür ve tam erişim hakları toohello küme düğümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="89ff4-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="89ff4-114">Betik eylemleri yöntemler aşağıdaki hello uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="89ff4-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="89ff4-115">Bu yöntem tooapply bir komut dosyası kullan...</span><span class="sxs-lookup"><span data-stu-id="89ff4-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="89ff4-116">Sırasında oluşturma küme...</span><span class="sxs-lookup"><span data-stu-id="89ff4-116">During cluster creation...</span></span> | <span data-ttu-id="89ff4-117">Çalıştıran bir kümede...</span><span class="sxs-lookup"><span data-stu-id="89ff4-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="89ff4-118">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="89ff4-118">Azure portal</span></span> |<span data-ttu-id="89ff4-119">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-119">✓</span></span> |<span data-ttu-id="89ff4-120">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-120">✓</span></span> |
| <span data-ttu-id="89ff4-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89ff4-121">Azure PowerShell</span></span> |<span data-ttu-id="89ff4-122">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-122">✓</span></span> |<span data-ttu-id="89ff4-123">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-123">✓</span></span> |
| <span data-ttu-id="89ff4-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="89ff4-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="89ff4-125">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-125">✓</span></span> |
| <span data-ttu-id="89ff4-126">HDInsight .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="89ff4-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="89ff4-127">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-127">✓</span></span> |<span data-ttu-id="89ff4-128">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-128">✓</span></span> |
| <span data-ttu-id="89ff4-129">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="89ff4-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="89ff4-130">✓</span><span class="sxs-lookup"><span data-stu-id="89ff4-130">✓</span></span> |&nbsp; |

<span data-ttu-id="89ff4-131">Bu yöntemleri tooapply betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="89ff4-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="89ff4-132"><a name="bestPracticeScripting"></a>Komut dosyası geliştirme için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="89ff4-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="89ff4-133">Hdınsight kümesi için özel bir komut dosyası geliştirirken göz önünde birkaç en iyi yöntemler tookeep vardır:</span><span class="sxs-lookup"><span data-stu-id="89ff4-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="89ff4-134">Hedef hello Hadoop sürümü</span><span class="sxs-lookup"><span data-stu-id="89ff4-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="89ff4-135">Hedef hello işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="89ff4-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="89ff4-136">Kararlı tooscript kaynaklara bağlantılar sağlar</span><span class="sxs-lookup"><span data-stu-id="89ff4-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="89ff4-137">Önceden derlenmiş kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="89ff4-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="89ff4-138">Komut dosyasını Hello kümede özelleştirme ıdempotent olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="89ff4-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="89ff4-139">Yüksek kullanılabilirlik hello küme mimarisinin emin olun</span><span class="sxs-lookup"><span data-stu-id="89ff4-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="89ff4-140">Merhaba özel bileşenler toouse Azure Blob depolama alanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89ff4-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="89ff4-141">Bilgi tooSTDOUT ve STDERR yazma</span><span class="sxs-lookup"><span data-stu-id="89ff4-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="89ff4-142">Dosyaları ASCII olarak LF satır sonları ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="89ff4-143">Geçici hataları yeniden deneme mantığı toorecover kullanın</span><span class="sxs-lookup"><span data-stu-id="89ff4-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="89ff4-144">Betik eylemleri 60 dakika içinde tamamlamanız gerekir veya hello işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="89ff4-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="89ff4-145">Düğüm sağlama işlemi sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak hello komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="89ff4-146">CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden hello betik tootake uzun toofinish neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="89ff4-147"><a name="bPS1"></a>Hedef hello Hadoop sürümü</span><span class="sxs-lookup"><span data-stu-id="89ff4-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="89ff4-148">Farklı sürümlerini Hdınsight Hadoop Hizmetleri ve bileşenleri yüklü farklı sürümlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="89ff4-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="89ff4-149">Komut bir hizmet veya bileşenin belirli bir sürümünü görüyorsa yalnızca hello betik hello gerekli bileşenleri içerir Hdınsight hello sürümü ile kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="89ff4-150">Hello kullanarak Hdınsight ile dahil bileşen sürümleri hakkında bilgi bulabilirsiniz [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.</span><span class="sxs-lookup"><span data-stu-id="89ff4-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="89ff4-151"><a name="bps10"></a>Hedef hello işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="89ff4-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="89ff4-152">Linux tabanlı Hdınsight Ubuntu Linux dağıtım hello üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="89ff4-153">Hdınsight farklı sürümlerini farklı sürümlerine ilişkin kodunuzu nasıl davranacağını değişebilir Ubuntu kullanır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="89ff4-154">Örneğin, Hdınsight 3.4 ve önceki Upstart kullanmak Ubuntu sürümlerinde dayalı.</span><span class="sxs-lookup"><span data-stu-id="89ff4-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="89ff4-155">Sürüm 3.5 Systemd kullanan Ubuntu 16.04 üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="89ff4-156">Kodunuzu toowork hem yazılması gereken şekilde Systemd ve Upstart farklı komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="89ff4-157">Başka bir önemli fark Hdınsight 3.4 3.5 arasındaki `JAVA_HOME` şimdi tooJava 8 işaret eder.</span><span class="sxs-lookup"><span data-stu-id="89ff4-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="89ff4-158">Merhaba işletim sistemi sürümünü kullanarak denetleyebilirsiniz `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="89ff4-159">Merhaba aşağıdaki kodu toodetermine Merhaba, nasıl bir komut dosyası gösterilmektedir Ubuntu 14 ya da 16 çalıştırıyor:</span><span class="sxs-lookup"><span data-stu-id="89ff4-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="89ff4-160">Bu parçacıkları https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh adresindeki içeren hello tam komut dosyası bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89ff4-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="89ff4-161">Merhaba Hdınsight tarafından kullanılan Ubuntu Hello sürümü için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md) belge.</span><span class="sxs-lookup"><span data-stu-id="89ff4-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="89ff4-162">toounderstand hello farklarını Systemd ve Upstart, bkz: [Systemd Upstart kullanıcılar için](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="89ff4-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="89ff4-163"><a name="bPS2"></a>Kararlı tooscript kaynaklara bağlantılar sağlar</span><span class="sxs-lookup"><span data-stu-id="89ff4-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="89ff4-164">Merhaba komut dosyası ve ilişkili kaynakları hello küme hello ömrü kullanılabilir kalmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="89ff4-165">Yeni düğümler toohello küme ölçeklendirme işlemleri sırasında eklenirse, bu kaynakları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="89ff4-166">Merhaba en iyi uygulama toodownload olduğunu ve her şeyi aboneliğinizi Azure depolama hesabında arşivleyin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89ff4-167">Itanium tabanlı sistemler için hello varsayılan depolama hesabı hello küme ya da bir ortak, salt okunur kapsayıcı için başka bir depolama hesabı üzerinde kullanılan hello depolama hesabı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="89ff4-168">Örneğin, Microsoft tarafından sağlanan hello örnekleri hello depolanan [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="89ff4-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="89ff4-169">Bu hello Hdınsight ekibi tarafından korunan bir ortak, salt okunur kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="89ff4-170"><a name="bPS4"></a>Önceden derlenmiş kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="89ff4-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="89ff4-171">tooreduce hello alır toorun hello betik süresi, kaynak kodu kaynaklardan derleme işlemlerden kaçının.</span><span class="sxs-lookup"><span data-stu-id="89ff4-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="89ff4-172">Örneğin, önceden derleme kaynakları ve bunları bir Azure depolama hesabı blob hello depolamak Hdınsight olarak aynı veri merkezinde.</span><span class="sxs-lookup"><span data-stu-id="89ff4-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="89ff4-173"><a name="bPS3"></a>Komut dosyasını Hello kümede özelleştirme ıdempotent olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="89ff4-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="89ff4-174">Komut dosyaları ıdempotent olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-174">Scripts must be idempotent.</span></span> <span data-ttu-id="89ff4-175">Merhaba betik birden çok kez çalıştırılıp çalıştırılmadığını döndürme zorunluluğu her zaman aynı durumu kümeyi toohello hello.</span><span class="sxs-lookup"><span data-stu-id="89ff4-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="89ff4-176">Örneğin, yapılandırma dosyalarını değiştiren bir komut dosyası yinelenen giriş varsa eklememelisiniz birden çok kez çalıştı.</span><span class="sxs-lookup"><span data-stu-id="89ff4-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="89ff4-177"><a name="bPS5"></a>Yüksek kullanılabilirlik hello küme mimarisinin emin olun</span><span class="sxs-lookup"><span data-stu-id="89ff4-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="89ff4-178">Linux tabanlı Hdınsight kümeleri hello küme içinde etkin olan iki baş düğümler sağlar ve her iki düğümde betik eylemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89ff4-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="89ff4-179">Yüklediğiniz hello bileşenleri tek bir baş düğüm bekliyorsanız, hello bileşenleri her iki baş düğümler üzerinde yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89ff4-180">Hdınsight bir parçası olarak sağlanan tasarlanmış toofail üzerinden hello iki baş düğümler arasında gerektiği gibi hizmetlerdir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="89ff4-181">Bu işlev toocustom bileşenleri betik eylemleri ile genişletilmedi.</span><span class="sxs-lookup"><span data-stu-id="89ff4-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="89ff4-182">Özel bileşenler için yüksek kullanılabilirlik gerekiyorsa, kendi yük devretme mekanizması uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="89ff4-183"><a name="bPS6"></a>Merhaba özel bileşenler toouse Azure Blob depolama alanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89ff4-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="89ff4-184">Merhaba kümede yüklemek bileşenleri Hadoop dağıtılmış dosya sistemi (HDFS) depolama kullanan bir varsayılan yapılandırmaya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="89ff4-185">Hdınsight Azure Storage veya Data Lake Store hello varsayılan depolama alanı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="89ff4-186">Her iki hello küme silinse bile veri devam ederse bir HDFS uyumlu bir dosya sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="89ff4-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="89ff4-187">Tooconfigure bileşenleri toouse WASB veya HDFS yerine ADL yüklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="89ff4-188">İşlemlerinin çoğu için toospecify hello dosya sistemi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="89ff4-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="89ff4-189">Örneğin, hello aşağıdaki hello giraph examples.jar dosya hello yerel dosya sistemi toocluster depolama biriminden kopyalar:</span><span class="sxs-lookup"><span data-stu-id="89ff4-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="89ff4-190">Bu örnekte, hello `hdfs` komutu hello varsayılan küme depolama saydam olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="89ff4-191">Bazı işlemler için toospecify hello URI gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="89ff4-192">Örneğin, `adl:///example/jars` Data Lake Store için veya `wasb:///example/jars` Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="89ff4-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="89ff4-193"><a name="bPS7"></a>Bilgi tooSTDOUT ve STDERR yazma</span><span class="sxs-lookup"><span data-stu-id="89ff4-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="89ff4-194">Hdınsight yazılı tooSTDOUT ve STDERR komut çıktısının günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="89ff4-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="89ff4-195">Merhaba Ambari web kullanıcı arabirimini kullanarak bu bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89ff4-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="89ff4-196">Ambari, yalnızca hello küme başarıyla oluşturulduysa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="89ff4-197">Küme oluşturma ve oluşturma başarısız sırasında bir betik eylemi kullanın, hello sorun giderme bölümüne bakın. [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) günlüğe kaydedilen bilgileri erişme diğer yolları için.</span><span class="sxs-lookup"><span data-stu-id="89ff4-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="89ff4-198">Tooadd ek günlük isteyebilirsiniz ancak çoğu yardımcı programları ve yükleme paketleri zaten bilgi tooSTDOUT ve STDERR, yazma.</span><span class="sxs-lookup"><span data-stu-id="89ff4-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="89ff4-199">toosend metin tooSTDOUT, kullanım `echo`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="89ff4-200">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="89ff4-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="89ff4-201">Varsayılan olarak, `echo` hello dize tooSTDOUT gönderir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="89ff4-202">toodirect, tooSTDERR, ekleme `>&2` önce `echo`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="89ff4-203">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="89ff4-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="89ff4-204">Bunun yerine tooSTDOUT tooSTDERR (2) yazılan bilgilerin yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="89ff4-205">G/ç yeniden yönlendirme hakkında daha fazla bilgi için bkz: [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="89ff4-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="89ff4-206">Betik eylemleri tarafından günlüğe kaydedilen bilgi görüntüleme hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="89ff4-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="89ff4-207"><a name="bps8"></a>Dosyaları ASCII olarak LF satır sonları ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="89ff4-208">Bash betiklerini ASCII biçiminde LF tarafından sonlandırıldı çizgili depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="89ff4-209">UTF-8 olarak depolanır veya CRLF hello satır bitiş olarak kullanan dosyalar hello aşağıdaki hata ile başarısız:</span><span class="sxs-lookup"><span data-stu-id="89ff4-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="89ff4-210"><a name="bps9"></a>Geçici hataları yeniden deneme mantığı toorecover kullanın</span><span class="sxs-lookup"><span data-stu-id="89ff4-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="89ff4-211">Dosyaları indirilirken alma apt ya da üzerinden veri aktaran diğer eylemler kullanarak paketleri yükleme Internet Merhaba, hello eylem tootransient ağ hataları başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="89ff4-212">Örneğin, hello uzak kaynak ile iletişim kuran tooa yedekleme düğüm üzerinde başarısız hello işleminde olabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="89ff4-213">toomake, komut dosyası dayanıklı tootransient hataları yeniden deneme mantığı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89ff4-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="89ff4-214">tooimplement mantığı nasıl yeniden deneme işlevi aşağıdaki hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="89ff4-215">Bu, üç kez başarısız olmadan önce hello işlemini yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="89ff4-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="89ff4-216">Merhaba aşağıdaki örneklerde görüldüğü nasıl toouse bu işlev.</span><span class="sxs-lookup"><span data-stu-id="89ff4-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="89ff4-217"><a name="helpermethods"></a>Özel komut dosyaları için yardımcı yöntemleri</span><span class="sxs-lookup"><span data-stu-id="89ff4-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="89ff4-218">Betik eylem Yardımcısı yöntemleri özel komut dosyaları yazılırken kullanabileceğiniz yardımcı programları ' dir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="89ff4-219">Bu yöntemler bulunan[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="89ff4-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="89ff4-220">Toodownload aşağıdaki hello ve komut dosyanızı bir parçası olarak kullanın:</span><span class="sxs-lookup"><span data-stu-id="89ff4-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="89ff4-221">komut dosyanız için kullanılabilir Yardımcıları aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="89ff4-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="89ff4-222">Yardımcı kullanımı</span><span class="sxs-lookup"><span data-stu-id="89ff4-222">Helper usage</span></span> | <span data-ttu-id="89ff4-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89ff4-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="89ff4-224">Bir dosya hello Kaynak URI toohello belirtilen dosya yolundan indirir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="89ff4-225">Varsayılan olarak, varolan bir dosyanın üzerine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="89ff4-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="89ff4-226">Tar dosyasını ayıklar (kullanarak `-xf`) toohello hedef dizini.</span><span class="sxs-lookup"><span data-stu-id="89ff4-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="89ff4-227">Bir küme baş düğümünde, dönüş 1; çalışan Aksi takdirde, 0.</span><span class="sxs-lookup"><span data-stu-id="89ff4-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="89ff4-228">Merhaba geçerli düğüm (çalışan) veri düğümü ise 1 döner; Aksi takdirde, 0.</span><span class="sxs-lookup"><span data-stu-id="89ff4-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="89ff4-229">Merhaba geçerli düğüm hello ilk veri (çalışan) ise düğümü (adlandırılmış workernode0) 1 döner; Aksi takdirde, 0.</span><span class="sxs-lookup"><span data-stu-id="89ff4-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="89ff4-230">Merhaba headnodes hello kümedeki dönüş hello tam etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="89ff4-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="89ff4-231">Virgülle ayrılmış adlardır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-231">Names are comma delimited.</span></span> <span data-ttu-id="89ff4-232">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89ff4-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="89ff4-233">Merhaba birincil headnode Hello tam etki alanı adını alır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="89ff4-234">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89ff4-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="89ff4-235">Merhaba ikincil headnode Hello tam etki alanı adını alır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="89ff4-236">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89ff4-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="89ff4-237">Merhaba birincil headnode Hello sayısal sonekini alır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="89ff4-238">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89ff4-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="89ff4-239">Merhaba ikincil headnode Hello sayısal sonekini alır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="89ff4-240">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89ff4-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="89ff4-241"><a name="commonusage"></a>Genel kullanım desenleri</span><span class="sxs-lookup"><span data-stu-id="89ff4-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="89ff4-242">Bu bölümde, kendi özel bir komut dosyası yazılırken içine çalışabilecek hello ortak kullanım desenlerini bazıları uygulama yönergeler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="89ff4-243">Tooa komut parametreleri geçirme</span><span class="sxs-lookup"><span data-stu-id="89ff4-243">Passing parameters tooa script</span></span>

<span data-ttu-id="89ff4-244">Bazı durumlarda, komut parametreleri gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="89ff4-245">Örneğin, hello Ambari REST API kullanırken hello küme için hello yönetici parolası gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="89ff4-246">Toohello betik geçirilen parametre olarak bilinen *konumsal parametreler*ve çok atanan`$1` hello ilk parametresi, `$2` hello ikinci ve böylece açma için.</span><span class="sxs-lookup"><span data-stu-id="89ff4-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="89ff4-247">`$0`Merhaba komut dosyasının kendisini Hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="89ff4-248">Toohello betik parametre olarak geçirilen değerleri (') tek tırnak içine.</span><span class="sxs-lookup"><span data-stu-id="89ff4-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="89ff4-249">Geçirilen değer bu hello sabit değer olarak kabul edilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="89ff4-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="89ff4-250">Ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="89ff4-250">Setting environment variables</span></span>

<span data-ttu-id="89ff4-251">Bir ortam değişkeni ayarı deyiminden hello tarafından gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="89ff4-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="89ff4-252">Burada VARIABLENAME hello hello değişkenin adıdır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="89ff4-253">tooaccess hello değişken, kullanım `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="89ff4-254">Örneğin, parola tooassign adlı konumsal parametre olarak bir ortam değişkeni tarafından sağlanan bir değer, aşağıdaki ifadeyi hello kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="89ff4-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="89ff4-255">Sonraki erişim toohello bilgileri daha sonra kullanabilir `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="89ff4-256">Ortam değişkenleri Hello betik Ayarla yalnızca hello hello betik kapsamında mevcut.</span><span class="sxs-lookup"><span data-stu-id="89ff4-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="89ff4-257">Bazı durumlarda, hello betik tamamlandıktan sonra korunur tooadd sistem geneli ortam değişkenleri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="89ff4-258">tooadd sistem geneli ortam değişkenleri eklemek hello değişkeni çok`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="89ff4-259">Örneğin, aşağıdaki ifadeyi hello ekler `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="89ff4-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="89ff4-260">Merhaba özel komut dosyalarının depolandığı toolocations erişim</span><span class="sxs-lookup"><span data-stu-id="89ff4-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="89ff4-261">Kullanılan komut toocustomize bir küme hello aşağıdaki konumlardan birinde depolanan toobe gerekir:</span><span class="sxs-lookup"><span data-stu-id="89ff4-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="89ff4-262">Bir __Azure depolama hesabı__ hello kümeyle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="89ff4-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="89ff4-263">Bir __ek depolama alanı hesabı__ hello kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="89ff4-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="89ff4-264">A __herkese açık şekilde okunabilir URI__.</span><span class="sxs-lookup"><span data-stu-id="89ff4-264">A __publicly readable URI__.</span></span> <span data-ttu-id="89ff4-265">Örneğin, bir URL toodata OneDrive, Dropbox veya barındırma hizmeti başka bir dosyaya depolanan.</span><span class="sxs-lookup"><span data-stu-id="89ff4-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="89ff4-266">Bir __Azure Data Lake Store hesabı__ hello Hdınsight kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="89ff4-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="89ff4-267">Hdınsight ile Azure Data Lake Store kullanma hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="89ff4-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="89ff4-268">Merhaba hizmet asıl Hdınsight kullandığı tooaccess Data Lake Store okuma erişimi toohello komut dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="89ff4-269">Merhaba komut dosyası tarafından kullanılan kaynakları da genel kullanıma açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="89ff4-270">Bir Azure depolama hesabı ya da Azure Data Lake Store Hello dosyaların depolanması hello Azure ağı içinde her ikisi olarak hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="89ff4-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="89ff4-271">Merhaba URI kullanılan biçimi tooreference hello betik kullanılan hello hizmete bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="89ff4-272">Merhaba Hdınsight kümesiyle ilişkili depolama hesapları için `wasb://` veya `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="89ff4-273">Genel olarak okunabilir URI'ler için kullanmak `http://` veya `https://`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="89ff4-274">Data Lake Store için kullanma `adl://`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="89ff4-275">Merhaba işletim sistemi sürüm denetimi</span><span class="sxs-lookup"><span data-stu-id="89ff4-275">Checking hello operating system version</span></span>

<span data-ttu-id="89ff4-276">Hdınsight farklı sürümlerini Ubuntu belirli sürümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="89ff4-277">Komut dosyanız için denetlemelisiniz işletim sistemi sürümleri arasındaki farklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="89ff4-278">Örneğin, tooinstall Ubuntu bağlı toohello sürümü bir ikili gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="89ff4-279">toocheck hello işletim sistemi sürümü, kullanım `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="89ff4-280">Örneğin, komut dosyası izleyen hello nasıl işletim sistemi sürümü hello bağlı olarak dosya tooreference belirli tar gösterir:</span><span class="sxs-lookup"><span data-stu-id="89ff4-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="89ff4-281"><a name="deployScript"></a>Betik eylemi dağıtma denetim listesi</span><span class="sxs-lookup"><span data-stu-id="89ff4-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="89ff4-282">Biz toodeploy bu komut dosyalarını hazırlanırken sürdü hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="89ff4-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="89ff4-283">Merhaba, dağıtım sırasında hello küme düğümleri tarafından erişilebilen bir yerde özel komut dosyaları içeren hello dosyaları yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="89ff4-284">Örneğin, varsayılan depolama hello küme için hello.</span><span class="sxs-lookup"><span data-stu-id="89ff4-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="89ff4-285">Dosyaları herkese açık şekilde okunabilir barındırma hizmetleri de depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="89ff4-286">Merhaba betik impotent olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="89ff4-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="89ff4-287">Bunun yapılması verir hello betik toobe yürütülen birden çok kez hello üzerinde aynı düğüm.</span><span class="sxs-lookup"><span data-stu-id="89ff4-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="89ff4-288">Bir geçici dosya dizin tmp tookeep hello kullan hello komut dosyaları tarafından kullanılan dosyaları indirilir ve komut dosyaları çalıştırdıktan sonra sonra bunları Temizle.</span><span class="sxs-lookup"><span data-stu-id="89ff4-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="89ff4-289">İşletim sistemi düzeyinde ayarlarını veya Hadoop hizmeti yapılandırma dosyalarını değiştirdiyseniz, toorestart Hdınsight Hizmetleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89ff4-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="89ff4-290"><a name="runScriptAction"></a>Nasıl toorun betik eylemi</span><span class="sxs-lookup"><span data-stu-id="89ff4-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="89ff4-291">Yöntemler aşağıdaki hello kullanarak betik eylemleri toocustomize Hdınsight kümelerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89ff4-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="89ff4-292">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="89ff4-292">Azure portal</span></span>
* <span data-ttu-id="89ff4-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89ff4-293">Azure PowerShell</span></span>
* <span data-ttu-id="89ff4-294">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="89ff4-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="89ff4-295">Merhaba Hdınsight .NET SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="89ff4-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="89ff4-296">Her yöntemi kullanma hakkında daha fazla bilgi için bkz: [nasıl toouse betik eylemi](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="89ff4-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="89ff4-297"><a name="sampleScripts"></a>Özel kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="89ff4-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="89ff4-298">Microsoft, bir Hdınsight kümesine tooinstall bileşenleri örnek komut dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="89ff4-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="89ff4-299">Daha fazla örnek betik eylemleri için bağlantıları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="89ff4-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="89ff4-300">Yükleme ve Hdınsight kümelerinde ton kullanın</span><span class="sxs-lookup"><span data-stu-id="89ff4-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="89ff4-301">Yükleme ve Hdınsight kümelerinde Solr kullanma</span><span class="sxs-lookup"><span data-stu-id="89ff4-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="89ff4-302">Yükleme ve Hdınsight kümelerinde Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="89ff4-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="89ff4-303">Yükleme veya Hdınsight kümelerinde Mono yükseltme</span><span class="sxs-lookup"><span data-stu-id="89ff4-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="89ff4-304">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="89ff4-304">Troubleshooting</span></span>

<span data-ttu-id="89ff4-305">Merhaba, geliştirilmiş komut dosyaları kullanırken karşılaşabileceğiniz hatalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="89ff4-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="89ff4-306">**Hata**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="89ff4-307">Bazen arkasından `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="89ff4-308">*Neden*: CRLF ile bir betik hello satırlarında sonlandırdığınızda, bu hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="89ff4-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="89ff4-309">UNIX sistemleri yalnızca LF hello satır bitiş olarak bekler.</span><span class="sxs-lookup"><span data-stu-id="89ff4-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="89ff4-310">Merhaba komut dosyası bir Windows ortamı yazılan CRLF birçok metin düzenleyicileri Windows'da için bitiş ortak bir çizgi olarak çoğunlukla oluşur.</span><span class="sxs-lookup"><span data-stu-id="89ff4-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="89ff4-311">*Çözümleme*: metin düzenleyicinizde bir seçenek ise, UNIX biçimini veya LF hello satır bitiş için seçin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="89ff4-312">Ayrıca UNIX sistem toochange hello CRLF tooan LF komutları aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89ff4-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="89ff4-313">Merhaba CRLF satır sonları tooLF değiştirmeniz gerekir, hello aşağıdaki komutlar kabaca eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="89ff4-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="89ff4-314">Merhaba yardımcı programları sisteminizdeki kullanılabilir göre seçin.</span><span class="sxs-lookup"><span data-stu-id="89ff4-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="89ff4-315">Komut</span><span class="sxs-lookup"><span data-stu-id="89ff4-315">Command</span></span> | <span data-ttu-id="89ff4-316">Notlar</span><span class="sxs-lookup"><span data-stu-id="89ff4-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="89ff4-317">Merhaba özgün dosya yedeklenir ile bir. BAK uzantısı</span><span class="sxs-lookup"><span data-stu-id="89ff4-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="89ff4-318">Yalnızca LF sonları sürümüyle ÇIKIŞDOSYASI içerir</span><span class="sxs-lookup"><span data-stu-id="89ff4-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="89ff4-319">Merhaba dosyasını doğrudan değiştirir</span><span class="sxs-lookup"><span data-stu-id="89ff4-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="89ff4-320">ÇIKIŞDOSYASI yalnızca LF sonları ile bir sürüm içeriyor.</span><span class="sxs-lookup"><span data-stu-id="89ff4-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="89ff4-321">**Hata**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="89ff4-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="89ff4-322">*Neden*: Bu hata hello betik UTF-8 bir bayt sırası işareti (BOM) ile olarak kaydedildi oluşur.</span><span class="sxs-lookup"><span data-stu-id="89ff4-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="89ff4-323">*Çözümleme*: Kaydet hello dosya olarak ASCII veya UTF-8 bir ürün reçetesi olmadan olarak.</span><span class="sxs-lookup"><span data-stu-id="89ff4-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="89ff4-324">Ayrıca, bir Linux veya UNIX sistem toocreate hello AĞACI olmadan bir dosya üzerinde komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89ff4-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="89ff4-325">Değiştir `INFILE` hello dosyasıyla AĞACI hello içeren.</span><span class="sxs-lookup"><span data-stu-id="89ff4-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="89ff4-326">`OUTFILE`Merhaba AĞACI kullanmadan hello komut içeren yeni bir dosya adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89ff4-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="89ff4-327"><a name="seeAlso"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89ff4-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="89ff4-328">Nasıl çok öğrenin[özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="89ff4-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="89ff4-329">Kullanım hello [Hdınsight .NET SDK'sı başvurusu](https://msdn.microsoft.com/library/mt271028.aspx) toolearn Hdınsight yönetmek .NET uygulamaları oluşturma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="89ff4-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="89ff4-330">Kullanım hello [Hdınsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn nasıl toouse REST tooperform yönetim eylemleri hdınsight kümeleri.</span><span class="sxs-lookup"><span data-stu-id="89ff4-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
