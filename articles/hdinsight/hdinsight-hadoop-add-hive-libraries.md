---
title: "Hdınsight küme oluşturma işlemi sırasında - Azure Hıve kitaplıkları ekleme | Microsoft Docs"
description: "Hive kitaplıkları (jar dosyaları) eklemek bir Hdınsight kümesine küme oluşturma sırasında öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="38a64-103">Özel Hıve kitaplıkları, Hdınsight kümesi oluştururken ekleme</span><span class="sxs-lookup"><span data-stu-id="38a64-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="38a64-104">Hdınsight'ta Hive sık kullandığınız kitaplıkları varsa, bu belge kitaplıkları küme oluşturma sırasında önceden yüklemek için bir betik eylemi kullanarak bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="38a64-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="38a64-105">Bu belgede yer alan adımları kullanarak eklenen kitaplıkları genel olarak kullanılabilir kovanında - kullanmaya gerek yoktur [eklemek JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) bunları yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="38a64-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="38a64-106">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="38a64-106">How it works</span></span>

<span data-ttu-id="38a64-107">Bir küme oluştururken, bunlar oluşturulurken, bir komut dosyası küme düğümlerinde çalışan betik eylemi isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38a64-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="38a64-108">Bu belge komut dosyasını önceden yüklenmiş olmasını (jar dosyaları olarak depolanır) kitaplıkları içeren bir WASB konumunun tek bir parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="38a64-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="38a64-109">Küme oluşturma sırasında komut dosyaları sıralar, kopyalar `/usr/lib/customhivelibs/` head ve çalışan düğümleri üzerinde dizin sonra ekler onlara `hive.aux.jars.path` özelliğinde `core-site.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="38a64-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="38a64-110">Ayrıca Linux tabanlı kümelerde güncelleştirir `hive-env.sh` dosyalarının konumunu dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="38a64-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="38a64-111">Bu makalede betik eylemleri kullanılarak kitaplıkları aşağıdaki senaryolarda kullanılabilir hale getirir:</span><span class="sxs-lookup"><span data-stu-id="38a64-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="38a64-112">**Linux tabanlı Hdınsight** - kullanırken bir Hive istemci **WebHCat**, ve **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="38a64-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="38a64-113">**Windows tabanlı Hdınsight** - Hive istemci kullanırken ve **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="38a64-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="38a64-114">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="38a64-114">The script</span></span>

<span data-ttu-id="38a64-115">**Komut dosyası konumu**</span><span class="sxs-lookup"><span data-stu-id="38a64-115">**Script location**</span></span>

<span data-ttu-id="38a64-116">İçin **Linux tabanlı kümelerde**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="38a64-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="38a64-117">İçin **Windows tabanlı kümeler**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="38a64-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38a64-118">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="38a64-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="38a64-119">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="38a64-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="38a64-120">**Gereksinimleri**</span><span class="sxs-lookup"><span data-stu-id="38a64-120">**Requirements**</span></span>

* <span data-ttu-id="38a64-121">Betikler her ikisini de uygulanması gereken **baş düğümler** ve **çalışan düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="38a64-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="38a64-122">Azure Blob depolama alanına yüklemek istediğiniz Kavanoz saklanmalıdır bir **tek kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="38a64-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="38a64-123">Kitaplığın adı jar dosyalarını içeren depolama hesabı **gerekir** oluşturma sırasında bağlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="38a64-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="38a64-124">Ya da varsayılan depolama hesabı olması gerekir ya da bir hesap üzerinden eklenen __isteğe bağlı yapılandırma__.</span><span class="sxs-lookup"><span data-stu-id="38a64-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="38a64-125">Kapsayıcı WASB yoluna betik eylemi parametresi olarak belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="38a64-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="38a64-126">Örneğin Kavanoz adlı bir kapsayıcıda depolanır, **kitaplıklar** bir depolama hesabında adlı **mystorage**, parametre olacaktır  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="38a64-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="38a64-127">Bu belgede zaten oluşturduğunuz bir depolama hesabı blob kapsayıcısı ve kendisine karşıya yüklenen dosyaların varsayar.</span><span class="sxs-lookup"><span data-stu-id="38a64-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="38a64-128">Bir depolama hesabı oluşturmadıysanız, bu nedenle aracılığıyla yapabileceğiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38a64-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="38a64-129">Ardından bir programı gibi kullanabilir [Azure Storage Gezgini](http://storageexplorer.com/) bir kapsayıcı hesabı oluşturun ve dosyaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="38a64-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="38a64-130">Komut dosyası kullanarak bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="38a64-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="38a64-131">Aşağıdaki adımlar Linux tabanlı Hdınsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="38a64-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="38a64-132">Windows tabanlı bir küme oluşturmak için seçin **Windows** (PowerShell) Windows komut dosyası yerine bash betik kullanımını ve küme oluştururken, işletim sistemi kümesi olarak.</span><span class="sxs-lookup"><span data-stu-id="38a64-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="38a64-133">Bu komut dosyası kullanarak bir küme oluşturmak için Azure PowerShell veya Hdınsight .NET SDK'sını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38a64-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="38a64-134">Bu yöntemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="38a64-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="38a64-135">' Ndaki adımları kullanarak bir küme hazırlama Başlat [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md), ancak sağlama tamamlamayın.</span><span class="sxs-lookup"><span data-stu-id="38a64-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="38a64-136">Üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **betik eylemleri**ve aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="38a64-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="38a64-137">**AD**: betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="38a64-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="38a64-138">**BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="38a64-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="38a64-139">**HEAD**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="38a64-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="38a64-140">**ÇALIŞAN**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="38a64-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="38a64-141">**ZOOKEEPER**: Bu alanı boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="38a64-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="38a64-142">**PARAMETRELERİ**: Kavanoz içeren kapsayıcı ve depolama hesabına WASB adresini girin.</span><span class="sxs-lookup"><span data-stu-id="38a64-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="38a64-143">Örneğin,  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="38a64-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="38a64-144">Ekranın alt kısmındaki **betik eylemleri**, kullanın **seçin** yapılandırmayı kaydetmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38a64-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="38a64-145">Üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **bağlantılı depolama hesapları** seçip **depolama anahtarı eklemek** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="38a64-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="38a64-146">Kavanoz içeren depolama hesabını seçin ve ardından **seçin** ayarları kaydedin ve dönüş düğmeleri **isteğe bağlı yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="38a64-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="38a64-147">Kullanım **seçin** alt kısmındaki düğmesi **isteğe bağlı yapılandırma** isteğe bağlı yapılandırma bilgilerini kaydetmek için dikey penceresini.</span><span class="sxs-lookup"><span data-stu-id="38a64-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="38a64-148">Bölümünde açıklandığı gibi küme hazırlama devam [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="38a64-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="38a64-149">Küme oluşturma tamamlandıktan sonra bu komut dosyası aracılığıyla kullanmak zorunda kalmadan kovanından eklenen Kavanoz kullanabilmek için `ADD JAR` deyimi.</span><span class="sxs-lookup"><span data-stu-id="38a64-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38a64-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38a64-150">Next steps</span></span>

<span data-ttu-id="38a64-151">Hive ile çalışma hakkında daha fazla bilgi için bkz: [Hdınsight ile Hive kullanma](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="38a64-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
