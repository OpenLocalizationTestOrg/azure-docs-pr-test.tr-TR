---
title: "Linux tabanlı Hdınsight - Azure ile betik eylemi geliştirme | Microsoft Docs"
description: "Linux tabanlı Hdınsight kümelerini özelleştirme için Bash betiklerini kullanmayı öğrenin. Hdınsight betik eylemi özelliğidir sırasında veya Küme oluşturulduktan sonra komut dosyaları çalıştırmanıza olanak sağlar. Komut dosyaları, küme yapılandırma ayarlarını değiştirmek veya ek yazılım yüklemek için kullanılabilir."
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
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="94d8d-105">Hdınsight ile betik eylemi geliştirme</span><span class="sxs-lookup"><span data-stu-id="94d8d-105">Script action development with HDInsight</span></span>

<span data-ttu-id="94d8d-106">Bash betiklerini kullanarak Hdınsight kümenize özelleştirmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="94d8d-107">Betik eylemleri, sırasında veya Küme oluşturulduktan sonra Hdınsight özelleştirmek için bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="94d8d-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94d8d-108">Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="94d8d-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="94d8d-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="94d8d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="94d8d-111">Betik eylemleri nelerdir</span><span class="sxs-lookup"><span data-stu-id="94d8d-111">What are script actions</span></span>

<span data-ttu-id="94d8d-112">Betik eylemleri Azure yapılandırma değişiklikler yapabilir veya yazılım yükleme küme düğümlerinde çalışır Bash betikleridir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="94d8d-113">Betik eylemi kök olarak yürütülen ve küme düğümleri için tam erişim hakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d8d-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="94d8d-114">Betik eylemleri aşağıdaki yöntemleri kullanarak uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="94d8d-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="94d8d-115">Bir komut dosyası uygulamak için bu yöntemi kullanın...</span><span class="sxs-lookup"><span data-stu-id="94d8d-115">Use this method to apply a script...</span></span> | <span data-ttu-id="94d8d-116">Sırasında oluşturma küme...</span><span class="sxs-lookup"><span data-stu-id="94d8d-116">During cluster creation...</span></span> | <span data-ttu-id="94d8d-117">Çalıştıran bir kümede...</span><span class="sxs-lookup"><span data-stu-id="94d8d-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="94d8d-118">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="94d8d-118">Azure portal</span></span> |<span data-ttu-id="94d8d-119">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-119">✓</span></span> |<span data-ttu-id="94d8d-120">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-120">✓</span></span> |
| <span data-ttu-id="94d8d-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="94d8d-121">Azure PowerShell</span></span> |<span data-ttu-id="94d8d-122">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-122">✓</span></span> |<span data-ttu-id="94d8d-123">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-123">✓</span></span> |
| <span data-ttu-id="94d8d-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="94d8d-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="94d8d-125">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-125">✓</span></span> |
| <span data-ttu-id="94d8d-126">HDInsight .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="94d8d-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="94d8d-127">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-127">✓</span></span> |<span data-ttu-id="94d8d-128">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-128">✓</span></span> |
| <span data-ttu-id="94d8d-129">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="94d8d-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="94d8d-130">✓</span><span class="sxs-lookup"><span data-stu-id="94d8d-130">✓</span></span> |&nbsp; |

<span data-ttu-id="94d8d-131">Betik eylemleri uygulamak için bu yöntemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94d8d-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="94d8d-132"><a name="bestPracticeScripting"></a>Komut dosyası geliştirme için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="94d8d-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="94d8d-133">Hdınsight kümesi için özel bir komut dosyası geliştirirken dikkate alınması gereken birkaç en iyi yöntemler vardır:</span><span class="sxs-lookup"><span data-stu-id="94d8d-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="94d8d-134">Hedef Hadoop sürümü</span><span class="sxs-lookup"><span data-stu-id="94d8d-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="94d8d-135">Hedef işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="94d8d-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="94d8d-136">Komut dosyası kaynaklara kararlı bağlantılar sağlar</span><span class="sxs-lookup"><span data-stu-id="94d8d-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="94d8d-137">Önceden derlenmiş kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="94d8d-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="94d8d-138">Küme özelleştirme betik ıdempotent olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="94d8d-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="94d8d-139">Küme mimari yüksek kullanılabilirliğini sağlamak</span><span class="sxs-lookup"><span data-stu-id="94d8d-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="94d8d-140">Azure Blob storage kullanma özel bileşenlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="94d8d-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="94d8d-141">STDOUT ve STDERR bilgi yazma</span><span class="sxs-lookup"><span data-stu-id="94d8d-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="94d8d-142">Dosyaları ASCII olarak LF satır sonları ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="94d8d-143">Geçici hataları kurtarmak için yeniden deneme mantığı kullanın</span><span class="sxs-lookup"><span data-stu-id="94d8d-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="94d8d-144">Betik eylemleri 60 dakika içinde tamamlamanız gerekir veya işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="94d8d-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="94d8d-145">Düğüm sağlama işlemi sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="94d8d-146">CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden tamamlanması daha uzun sürmesine betik neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="94d8d-147"><a name="bPS1"></a>Hedef Hadoop sürümü</span><span class="sxs-lookup"><span data-stu-id="94d8d-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="94d8d-148">Farklı sürümlerini Hdınsight Hadoop Hizmetleri ve bileşenleri yüklü farklı sürümlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="94d8d-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="94d8d-149">Komut bir hizmet veya bileşenin belirli bir sürümünü görüyorsa yalnızca komut dosyasını gerekli bileşenleri içerir Hdınsight sürümü ile kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="94d8d-150">Hdınsight kullanma ile dahil bileşen sürümleri hakkında bilgi bulabilirsiniz [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.</span><span class="sxs-lookup"><span data-stu-id="94d8d-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="94d8d-151"><a name="bps10"></a>Hedef işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="94d8d-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="94d8d-152">Linux tabanlı Hdınsight Ubuntu Linux dağıtım temel alır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="94d8d-153">Hdınsight farklı sürümlerini farklı sürümlerine ilişkin kodunuzu nasıl davranacağını değişebilir Ubuntu kullanır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="94d8d-154">Örneğin, Hdınsight 3.4 ve önceki Upstart kullanmak Ubuntu sürümlerinde dayalı.</span><span class="sxs-lookup"><span data-stu-id="94d8d-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="94d8d-155">Sürüm 3.5 Systemd kullanan Ubuntu 16.04 üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="94d8d-156">İkisi ile çalışmak için komut dosyanızı yazılması gereken şekilde Systemd ve Upstart farklı komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="94d8d-157">Başka bir önemli fark Hdınsight 3.4 3.5 arasındaki `JAVA_HOME` şimdi Java 8 işaret eder.</span><span class="sxs-lookup"><span data-stu-id="94d8d-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="94d8d-158">Kullanarak işletim sistemi sürümü denetleyebilirsiniz `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="94d8d-159">Aşağıdaki kod, komut dosyası Ubuntu 14 veya 16 üzerinde çalışıp çalışmadığı belirlenemedi gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="94d8d-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="94d8d-160">Bu parçacıkları https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh adresindeki içeren tam komut dosyası bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d8d-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="94d8d-161">Hdınsight tarafından kullanılan Ubuntu sürümü için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md) belge.</span><span class="sxs-lookup"><span data-stu-id="94d8d-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="94d8d-162">Systemd ve Upstart arasındaki farkları anlamak için bkz: [Systemd Upstart kullanıcılar için](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="94d8d-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="94d8d-163"><a name="bPS2"></a>Komut dosyası kaynaklara kararlı bağlantılar sağlar</span><span class="sxs-lookup"><span data-stu-id="94d8d-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="94d8d-164">Komut dosyası ve ilişkili kaynakları kümenin kullanım ömrü kullanılabilir kalmalıdır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="94d8d-165">Yeni düğümler için küme ölçeklendirme işlemleri sırasında eklenirse, bu kaynakları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="94d8d-166">Karşıdan yükle ve her şeyi aboneliğinizi Azure depolama hesabında arşivlemek için en iyi uygulamadır bakın.</span><span class="sxs-lookup"><span data-stu-id="94d8d-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94d8d-167">Kullanılan depolama hesabı başka bir depolama hesabı üzerinde Küme ya da bir ortak, salt okunur kapsayıcı için varsayılan depolama hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="94d8d-168">Örneğin, Microsoft tarafından sağlanan örnekleri depolanmış [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="94d8d-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="94d8d-169">Bu Hdınsight ekibi tarafından korunan bir ortak, salt okunur kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="94d8d-170"><a name="bPS4"></a>Önceden derlenmiş kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="94d8d-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="94d8d-171">Komut dosyasını çalıştırmak için gereken süreyi azaltmak için kaynak kodu kaynaklardan derleme işlemleri kaçının.</span><span class="sxs-lookup"><span data-stu-id="94d8d-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="94d8d-172">Örneğin, önceden derleme kaynakları ve Hdınsight aynı veri merkezindeki bir Azure depolama hesabı blob depolayın.</span><span class="sxs-lookup"><span data-stu-id="94d8d-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="94d8d-173"><a name="bPS3"></a>Küme özelleştirme betik ıdempotent olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="94d8d-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="94d8d-174">Komut dosyaları ıdempotent olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-174">Scripts must be idempotent.</span></span> <span data-ttu-id="94d8d-175">Komut dosyası birden çok kez çalıştırıyorsa, bu her zaman aynı duruma küme döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="94d8d-176">Örneğin, yapılandırma dosyalarını değiştiren bir komut dosyası yinelenen giriş varsa eklememelisiniz birden çok kez çalıştı.</span><span class="sxs-lookup"><span data-stu-id="94d8d-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="94d8d-177"><a name="bPS5"></a>Küme mimari yüksek kullanılabilirliğini sağlamak</span><span class="sxs-lookup"><span data-stu-id="94d8d-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="94d8d-178">Linux tabanlı Hdınsight kümeleri küme içinde etkin olan iki baş düğümler sağlar ve her iki düğümde betik eylemleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94d8d-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="94d8d-179">Yüklediğiniz bileşenlerin tek bir baş düğüm bekliyorsanız, bileşenleri her iki baş düğümler üzerinde yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94d8d-180">Hdınsight bir parçası olarak sağlanan hizmetlerin iki baş düğümler arasında gerektiğinde yük devredecek biçimde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="94d8d-181">Bu işlevsellik, betik eylemleri yüklü özel bileşenlerine genişletilmedi.</span><span class="sxs-lookup"><span data-stu-id="94d8d-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="94d8d-182">Özel bileşenler için yüksek kullanılabilirlik gerekiyorsa, kendi yük devretme mekanizması uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="94d8d-183"><a name="bPS6"></a>Azure Blob storage kullanma özel bileşenlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="94d8d-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="94d8d-184">Kümede yüklemeniz bileşenleri Hadoop dağıtılmış dosya sistemi (HDFS) depolama kullanan bir varsayılan yapılandırmaya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="94d8d-185">Hdınsight, varsayılan depolama alanı olarak Azure Storage veya Data Lake Store kullanır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="94d8d-186">Her iki küme silinse bile veri devam ederse bir HDFS uyumlu bir dosya sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d8d-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="94d8d-187">WASB veya ADL HDFS yerine kullanmak için yüklediğiniz bileşenler yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="94d8d-188">İşlemlerinin çoğu için dosya sistemi belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="94d8d-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="94d8d-189">Örneğin, aşağıdaki giraph examples.jar dosyanın yerel dosya sisteminden küme depolama birimine kopyalar:</span><span class="sxs-lookup"><span data-stu-id="94d8d-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="94d8d-190">Bu örnekte, `hdfs` komut varsayılan küme depolama saydam olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="94d8d-191">Bazı işlemler için URI belirtmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="94d8d-192">Örneğin, `adl:///example/jars` Data Lake Store için veya `wasb:///example/jars` Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="94d8d-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="94d8d-193"><a name="bPS7"></a>STDOUT ve STDERR bilgi yazma</span><span class="sxs-lookup"><span data-stu-id="94d8d-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="94d8d-194">Hdınsight STDOUT ve STDERR yazılan komut dosyası çıkışını günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="94d8d-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="94d8d-195">Ambari web kullanıcı arabirimini kullanarak bu bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d8d-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="94d8d-196">Ambari, yalnızca küme başarıyla oluşturulduysa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="94d8d-197">Küme oluşturma ve oluşturma başarısız sırasında bir betik eylemi kullanın, sorun giderme bölümüne bakın. [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) günlüğe kaydedilen bilgileri erişme diğer yolları için.</span><span class="sxs-lookup"><span data-stu-id="94d8d-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="94d8d-198">Ek günlük eklemek isteyebilirsiniz ancak çoğu yardımcı programları ve yükleme paketleri zaten bilgi STDOUT ve STDERR, yazma.</span><span class="sxs-lookup"><span data-stu-id="94d8d-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="94d8d-199">Metin STDOUT göndermek için kullanmak `echo`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="94d8d-200">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="94d8d-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="94d8d-201">Varsayılan olarak, `echo` STDOUT dizesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="94d8d-202">STDERR yönlendirmek için ekleme `>&2` önce `echo`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="94d8d-203">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="94d8d-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="94d8d-204">STDOUT STDERR (2) için bunun yerine yazılan bilgilerin yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="94d8d-205">G/ç yeniden yönlendirme hakkında daha fazla bilgi için bkz: [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="94d8d-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="94d8d-206">Betik eylemleri tarafından günlüğe kaydedilen bilgi görüntüleme hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="94d8d-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="94d8d-207"><a name="bps8"></a>Dosyaları ASCII olarak LF satır sonları ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="94d8d-208">Bash betiklerini ASCII biçiminde LF tarafından sonlandırıldı çizgili depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="94d8d-209">UTF-8 olarak depolanır veya satır sonu olarak CRLF kullanan dosyalar, şu hata ile başarısız:</span><span class="sxs-lookup"><span data-stu-id="94d8d-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="94d8d-210"><a name="bps9"></a>Geçici hataları kurtarmak için yeniden deneme mantığı kullanın</span><span class="sxs-lookup"><span data-stu-id="94d8d-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="94d8d-211">Get apt veya Internet üzerinden veri aktaran diğer eylemler kullanarak paketleri yükleme dosyaları indirilirken eylemi geçici ağ hataları nedeniyle başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="94d8d-212">Örneğin, bir yedekleme düğüme yapabilmesini sürecinde ile iletişim kuran uzak kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="94d8d-213">Kodunuzu geçici hataları esnek hale getirmek için yeniden deneme mantığı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d8d-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="94d8d-214">Aşağıdaki işlevi, yeniden deneme mantığını uygulaması gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="94d8d-215">Bu, üç kez başarısız olmadan önce işlemi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="94d8d-215">It retries the operation three times before failing.</span></span>

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

<span data-ttu-id="94d8d-216">Aşağıdaki örnekler, bu işlevi kullanmak nasıl ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="94d8d-217"><a name="helpermethods"></a>Özel komut dosyaları için yardımcı yöntemleri</span><span class="sxs-lookup"><span data-stu-id="94d8d-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="94d8d-218">Betik eylem Yardımcısı yöntemleri özel komut dosyaları yazılırken kullanabileceğiniz yardımcı programları ' dir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="94d8d-219">Bu yöntemler bulunan[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="94d8d-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="94d8d-220">Karşıdan yüklemek ve komut dosyanızı bir parçası olarak kullanmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d8d-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="94d8d-221">Aşağıdaki Yardımcıları komut dosyanız için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="94d8d-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="94d8d-222">Yardımcı kullanımı</span><span class="sxs-lookup"><span data-stu-id="94d8d-222">Helper usage</span></span> | <span data-ttu-id="94d8d-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94d8d-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="94d8d-224">Bir dosya için belirtilen dosya yolu Kaynak URI'sı yükler.</span><span class="sxs-lookup"><span data-stu-id="94d8d-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="94d8d-225">Varsayılan olarak, varolan bir dosyanın üzerine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="94d8d-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="94d8d-226">Tar dosyasını ayıklar (kullanarak `-xf`) hedef dizin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="94d8d-227">Bir küme baş düğümünde, dönüş 1; çalışan Aksi takdirde, 0.</span><span class="sxs-lookup"><span data-stu-id="94d8d-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="94d8d-228">Geçerli düğüm (çalışan) veri düğümü ise 1 döner; Aksi takdirde, 0.</span><span class="sxs-lookup"><span data-stu-id="94d8d-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="94d8d-229">Geçerli düğüm (çalışan) ilk veri ise düğümü (adlandırılmış workernode0) 1 döner; Aksi takdirde, 0.</span><span class="sxs-lookup"><span data-stu-id="94d8d-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="94d8d-230">Kümede headnodes tam etki alanı adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="94d8d-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="94d8d-231">Virgülle ayrılmış adlardır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-231">Names are comma delimited.</span></span> <span data-ttu-id="94d8d-232">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94d8d-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="94d8d-233">Birincil headnode tam etki alanı adını alır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="94d8d-234">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94d8d-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="94d8d-235">İkincil headnode tam etki alanı adını alır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="94d8d-236">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94d8d-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="94d8d-237">Birincil headnode sayısal sonekini alır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="94d8d-238">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94d8d-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="94d8d-239">İkincil headnode sayısal sonekini alır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="94d8d-240">Boş bir dize hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94d8d-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="94d8d-241"><a name="commonusage"></a>Genel kullanım desenleri</span><span class="sxs-lookup"><span data-stu-id="94d8d-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="94d8d-242">Bu bölümde, kendi özel bir komut dosyası yazılırken içine çalışabilir ortak kullanım desenlerini bazıları uygulama yönergeler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="94d8d-243">Bir komut dosyası parametreleri geçirme</span><span class="sxs-lookup"><span data-stu-id="94d8d-243">Passing parameters to a script</span></span>

<span data-ttu-id="94d8d-244">Bazı durumlarda, komut parametreleri gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="94d8d-245">Örneğin, Ambari REST API kullanırken küme için yönetici parolasını gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="94d8d-246">Komut dosyasına iletilen parametreler olarak bilinen *konumsal parametreler*ve atanan `$1` ilk parametresi için `$2` ikinci için ve böylece açma.</span><span class="sxs-lookup"><span data-stu-id="94d8d-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="94d8d-247">`$0`komut dosyasının kendisini adını içerir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="94d8d-248">Parametreler (') tek tırnak içine alınması gibi değerler komut dosyasına iletilen.</span><span class="sxs-lookup"><span data-stu-id="94d8d-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="94d8d-249">Geçirilen değeri sabit değer olarak davranılır sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d8d-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="94d8d-250">Ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="94d8d-250">Setting environment variables</span></span>

<span data-ttu-id="94d8d-251">Bir ortam değişkeni ayarı aşağıdaki deyimi tarafından gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="94d8d-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="94d8d-252">Burada VARIABLENAME değişkenin adıdır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="94d8d-253">Değişkeni erişmek için `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="94d8d-254">Örneğin, parola adlı bir ortam değişkeni bir konumsal parametre tarafından sağlanan bir değer atamak için şu deyimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d8d-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="94d8d-255">Sonraki bilgilere erişimi daha sonra kullanabilir `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="94d8d-256">Komut dosyası içinde ayarlamak ortam değişkenleri yalnızca betik kapsamında mevcut.</span><span class="sxs-lookup"><span data-stu-id="94d8d-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="94d8d-257">Bazı durumlarda, komut dosyası tamamlandıktan sonra korunur sistem geneli ortam değişkenleri eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="94d8d-258">Sistem geneli ortam değişkenleri eklemek için değişkeni eklemek `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="94d8d-259">Örneğin, aşağıdaki ifadeyi ekler `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="94d8d-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="94d8d-260">Özel komut dosyaları depolandığı konumuna erişim</span><span class="sxs-lookup"><span data-stu-id="94d8d-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="94d8d-261">Bir küme özelleştirmek için kullanılan komut aşağıdaki konumlardan birinde depolanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="94d8d-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="94d8d-262">Bir __Azure depolama hesabı__ kümeyle ilişkili.</span><span class="sxs-lookup"><span data-stu-id="94d8d-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="94d8d-263">Bir __ek depolama alanı hesabı__ kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="94d8d-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="94d8d-264">A __herkese açık şekilde okunabilir URI__.</span><span class="sxs-lookup"><span data-stu-id="94d8d-264">A __publicly readable URI__.</span></span> <span data-ttu-id="94d8d-265">Örneğin, OneDrive, Dropbox veya barındırma hizmeti başka bir dosyaya depolanan verileri URL'sine.</span><span class="sxs-lookup"><span data-stu-id="94d8d-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="94d8d-266">Bir __Azure Data Lake Store hesabı__ Hdınsight kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="94d8d-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="94d8d-267">Hdınsight ile Azure Data Lake Store kullanma hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94d8d-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="94d8d-268">Hdınsight Data Lake Store erişmek için kullandığı hizmet sorumlusu komut dosyasını okuma erişimi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="94d8d-269">Komut dosyası tarafından kullanılan kaynakları da genel kullanıma açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="94d8d-270">Bir Azure depolama hesabı ya da Azure Data Lake Store dosyaların depolanması Azure ağından her ikisi olarak hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d8d-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="94d8d-271">Komut dosyası başvurmak için kullanılan URI biçimi kullanılan hizmete bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="94d8d-272">Hdınsight kümesi ile ilişkili depolama hesapları için `wasb://` veya `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="94d8d-273">Genel olarak okunabilir URI'ler için kullanmak `http://` veya `https://`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="94d8d-274">Data Lake Store için kullanma `adl://`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="94d8d-275">İşletim sistemi sürümü denetimi</span><span class="sxs-lookup"><span data-stu-id="94d8d-275">Checking the operating system version</span></span>

<span data-ttu-id="94d8d-276">Hdınsight farklı sürümlerini Ubuntu belirli sürümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="94d8d-277">Komut dosyanız için denetlemelisiniz işletim sistemi sürümleri arasındaki farklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="94d8d-278">Örneğin, Ubuntu sürümüne bağlı bir ikili yüklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="94d8d-279">İşletim sistemi sürümü denetlemek için kullanmak `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="94d8d-280">Örneğin, aşağıdaki komut dosyası işletim sistemi sürümüne bağlı olarak belirli tar dosyasına başvurmak gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="94d8d-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

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

## <span data-ttu-id="94d8d-281"><a name="deployScript"></a>Betik eylemi dağıtma denetim listesi</span><span class="sxs-lookup"><span data-stu-id="94d8d-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="94d8d-282">Biz bu komut dosyaları dağıtmak hazırlarken sürdü adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="94d8d-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="94d8d-283">Dağıtım sırasında küme düğümleri tarafından erişilebilen bir yerde özel komut dosyaları içeren dosyaları yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="94d8d-284">Örneğin, kümenin varsayılan depolama.</span><span class="sxs-lookup"><span data-stu-id="94d8d-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="94d8d-285">Dosyaları herkese açık şekilde okunabilir barındırma hizmetleri de depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="94d8d-286">Komut dosyası impotent olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="94d8d-286">Verify that the script is impotent.</span></span> <span data-ttu-id="94d8d-287">Bunun yapılması, birden çok kez aynı düğümde yürütülmek üzere betik sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d8d-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="94d8d-288">Komut dosyaları tarafından kullanılan indirilen dosyaları korumak ve komut dosyaları çalıştırdıktan sonra sonra bunları temizlemek için bir geçici dosya dizin tmp kullanın.</span><span class="sxs-lookup"><span data-stu-id="94d8d-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="94d8d-289">İşletim sistemi düzeyinde ayarlarını veya Hadoop hizmeti yapılandırma dosyalarını değiştirdiyseniz, Hdınsight hizmetlerini yeniden başlatmak istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="94d8d-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="94d8d-290"><a name="runScriptAction"></a>Betik eylemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="94d8d-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="94d8d-291">Aşağıdaki yöntemleri kullanarak Hdınsight kümelerini özelleştirme için betik eylemleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d8d-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="94d8d-292">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="94d8d-292">Azure portal</span></span>
* <span data-ttu-id="94d8d-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="94d8d-293">Azure PowerShell</span></span>
* <span data-ttu-id="94d8d-294">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="94d8d-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="94d8d-295">Hdınsight .NET SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="94d8d-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="94d8d-296">Her yöntemi kullanma hakkında daha fazla bilgi için bkz: [betik eyleminin nasıl kullanılacağını](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94d8d-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="94d8d-297"><a name="sampleScripts"></a>Özel kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="94d8d-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="94d8d-298">Microsoft, bir Hdınsight kümesine bileşenleri yüklemek için örnek komut dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d8d-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="94d8d-299">Daha fazla örnek betik eylemleri için aşağıdaki bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="94d8d-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="94d8d-300">Yükleme ve Hdınsight kümelerinde ton kullanın</span><span class="sxs-lookup"><span data-stu-id="94d8d-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="94d8d-301">Yükleme ve Hdınsight kümelerinde Solr kullanma</span><span class="sxs-lookup"><span data-stu-id="94d8d-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="94d8d-302">Yükleme ve Hdınsight kümelerinde Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="94d8d-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="94d8d-303">Yükleme veya Hdınsight kümelerinde Mono yükseltme</span><span class="sxs-lookup"><span data-stu-id="94d8d-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="94d8d-304">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="94d8d-304">Troubleshooting</span></span>

<span data-ttu-id="94d8d-305">Geliştirilmiş komut dosyaları kullanırken karşılaşabileceğiniz hatalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="94d8d-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="94d8d-306">**Hata**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="94d8d-307">Bazen arkasından `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="94d8d-308">*Neden*: bir komut satırları ile CRLF sonlandırdığınızda, bu hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="94d8d-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="94d8d-309">UNIX sistemleri yalnızca LF satır bitiş olarak bekler.</span><span class="sxs-lookup"><span data-stu-id="94d8d-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="94d8d-310">Komut dosyası bir Windows ortamı yazılan CRLF birçok metin düzenleyicileri Windows'da için bitiş ortak bir çizgi olarak çoğunlukla oluşur.</span><span class="sxs-lookup"><span data-stu-id="94d8d-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="94d8d-311">*Çözümleme*: metin düzenleyicinizde bir seçenek ise, UNIX biçimini veya LF için satır sonu seçin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="94d8d-312">Bir LF CRLF değiştirmek için bir Unix sistem üzerinde aşağıdaki komutları de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="94d8d-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="94d8d-313">Aşağıdaki komutlar için LF CRLF satır sonları değiştirmeniz gerekir, kabaca eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="94d8d-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="94d8d-314">Sisteminizde yardımcı programları göre seçin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="94d8d-315">Komut</span><span class="sxs-lookup"><span data-stu-id="94d8d-315">Command</span></span> | <span data-ttu-id="94d8d-316">Notlar</span><span class="sxs-lookup"><span data-stu-id="94d8d-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="94d8d-317">Özgün dosya ile yedeklenir bir. BAK uzantısı</span><span class="sxs-lookup"><span data-stu-id="94d8d-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="94d8d-318">Yalnızca LF sonları sürümüyle ÇIKIŞDOSYASI içerir</span><span class="sxs-lookup"><span data-stu-id="94d8d-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="94d8d-319">Dosyayı doğrudan değiştirir</span><span class="sxs-lookup"><span data-stu-id="94d8d-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="94d8d-320">ÇIKIŞDOSYASI yalnızca LF sonları ile bir sürüm içeriyor.</span><span class="sxs-lookup"><span data-stu-id="94d8d-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="94d8d-321">**Hata**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="94d8d-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="94d8d-322">*Neden*: UTF-8 bir bayt sırası işareti (BOM) ile olarak komut dosyası kaydedildiğinde bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="94d8d-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="94d8d-323">*Çözümleme*: dosyayı olarak ASCII veya UTF-8 bir ürün reçetesi olmadan olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="94d8d-324">Bir dosya AĞACI olmadan oluşturmak için bir Linux veya UNIX sistemde aşağıdaki komutu de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="94d8d-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="94d8d-325">Değiştir `INFILE` AĞACI içeren dosya ile.</span><span class="sxs-lookup"><span data-stu-id="94d8d-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="94d8d-326">`OUTFILE`Ürün reçetesi olmadan komut dosyasını içeren yeni bir dosya adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="94d8d-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="94d8d-327"><a name="seeAlso"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94d8d-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="94d8d-328">Bilgi edinmek için nasıl [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="94d8d-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="94d8d-329">Kullanım [Hdınsight .NET SDK'sı başvurusu](https://msdn.microsoft.com/library/mt271028.aspx) Hdınsight yönetmek .NET uygulamaları oluşturma hakkında daha fazla bilgi edinmek için</span><span class="sxs-lookup"><span data-stu-id="94d8d-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="94d8d-330">Kullanmak [Hdınsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) REST Hdınsight kümelerinde yönetim eylemleri gerçekleştirmek için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="94d8d-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
