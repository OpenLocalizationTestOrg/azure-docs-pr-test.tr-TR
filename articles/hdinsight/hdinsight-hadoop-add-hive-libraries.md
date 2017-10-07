---
title: "Hdınsight sırasında aaaAdd Hıve kitaplıkları küme oluşturma - Azure | Microsoft Docs"
description: "Nasıl tooadd Hıve kitaplıkları (jar dosyaları), tooan Hdınsight Küme Küme oluşturma sırasında öğrenin."
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
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="23940-103">Özel Hıve kitaplıkları, Hdınsight kümesi oluştururken ekleme</span><span class="sxs-lookup"><span data-stu-id="23940-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="23940-104">Hdınsight'ta Hive sık kullandığınız kitaplıkları varsa, bu belgede küme oluşturma sırasında bir betik eylemi toopre yük hello kitaplıklarını kullanma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="23940-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="23940-105">Bu belgede Hello adımları kullanarak eklenen kitaplıkları genel olarak kullanılabilir kovanında - gerek toouse [eklemek JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload bunları.</span><span class="sxs-lookup"><span data-stu-id="23940-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="23940-106">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="23940-106">How it works</span></span>

<span data-ttu-id="23940-107">Bir küme oluştururken, bunlar oluşturulurken hello küme düğümleri üzerinde bir komut dosyası çalıştırılan bir komut dosyası eylemi isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23940-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="23940-108">Bu belgedeki Hello betik önceden yüklenmiş hello (jar dosyaları olarak depolanır) kitaplıkları toobe içeren bir WASB konumunun tek bir parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="23940-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="23940-109">Küme oluşturma sırasında hello betik hello dosyaları sıralar, toohello kopyalar `/usr/lib/customhivelibs/` head ve çalışan düğümleri üzerinde dizin sonra toohello bunları ekler `hive.aux.jars.path` hello özelliğinde `core-site.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="23940-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="23940-110">Linux tabanlı kümelerde de hello güncelleştirir `hive-env.sh` hello hello dosyalarının konumunu dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="23940-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="23940-111">Bu makalede Hello betik eylemleri kullanılarak hello kitaplıkları senaryoları aşağıdaki hello yapar:</span><span class="sxs-lookup"><span data-stu-id="23940-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="23940-112">**Linux tabanlı Hdınsight** - kullanarak hello olduğunda bir Hive istemci **WebHCat**, ve **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="23940-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="23940-113">**Windows tabanlı Hdınsight** - hello Hive istemci kullanırken ve **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="23940-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="23940-114">Merhaba komut dosyası</span><span class="sxs-lookup"><span data-stu-id="23940-114">hello script</span></span>

<span data-ttu-id="23940-115">**Komut dosyası konumu**</span><span class="sxs-lookup"><span data-stu-id="23940-115">**Script location**</span></span>

<span data-ttu-id="23940-116">İçin **Linux tabanlı kümelerde**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="23940-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="23940-117">İçin **Windows tabanlı kümeler**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="23940-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23940-118">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="23940-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="23940-119">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="23940-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="23940-120">**Gereksinimleri**</span><span class="sxs-lookup"><span data-stu-id="23940-120">**Requirements**</span></span>

* <span data-ttu-id="23940-121">Merhaba betikleri uygulanan tooboth hello olmalıdır **baş düğümler** ve **çalışan düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="23940-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="23940-122">Merhaba istiyor tooinstall depolanan, Azure Blob Depolama Kavanoz bir **tek kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="23940-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="23940-123">Merhaba kitaplığı jar dosyalarını içeren hello depolama hesabı **gerekir** bağlantılı toohello Hdınsight kümesi oluşturma sırasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="23940-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="23940-124">Ya da hello varsayılan depolama hesabı olması gerekir ya da bir hesap üzerinden eklenen __isteğe bağlı yapılandırma__.</span><span class="sxs-lookup"><span data-stu-id="23940-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="23940-125">Merhaba WASB yolu toohello kapsayıcı parametresi toohello betik eylemi belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="23940-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="23940-126">Örneğin, hello varsa Kavanoz adlı bir kapsayıcıda depolanır **kitaplıklar** bir depolama hesabında adlı **mystorage**, hello parametre olacaktır  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="23940-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="23940-127">Bu belge sahip önceden oluşturduğunuz bir depolama hesabı, blob kapsayıcısı ve karşıya yüklenen hello dosyaları tooit varsayar.</span><span class="sxs-lookup"><span data-stu-id="23940-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="23940-128">Bir depolama hesabı oluşturmadıysanız hello bunu yapabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23940-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="23940-129">Ardından bir programı gibi kullanabilir [Azure Storage Gezgini](http://storageexplorer.com/) toocreate hello hesabı ve karşıya yükleme kapsayıcısında tooit dosyaları.</span><span class="sxs-lookup"><span data-stu-id="23940-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="23940-130">Merhaba komut dosyası kullanarak bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="23940-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="23940-131">Aşağıdaki adımları hello Linux tabanlı Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23940-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="23940-132">toocreate Windows tabanlı bir küme seçin **Windows** hello küme oluştururken, işletim sistemi hello küme ve hello bash betik yerine hello Windows (PowerShell) komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="23940-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="23940-133">Azure PowerShell veya hello Hdınsight .NET SDK'sı toocreate bu komut dosyası kullanarak bir küme de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23940-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="23940-134">Bu yöntemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="23940-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="23940-135">Merhaba adımları kullanarak bir küme hazırlama Başlat [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md), ancak sağlama tamamlamayın.</span><span class="sxs-lookup"><span data-stu-id="23940-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="23940-136">Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **betik eylemleri**ve aşağıdaki bilgilerle hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="23940-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="23940-137">**AD**: hello betik eylemi için kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="23940-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="23940-138">**BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="23940-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="23940-139">**HEAD**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="23940-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="23940-140">**ÇALIŞAN**: Bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="23940-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="23940-141">**ZOOKEEPER**: Bu alanı boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="23940-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="23940-142">**PARAMETRELERİ**: hello Kavanoz içeren hello WASB adresi toohello kapsayıcı ve depolama hesabını girin.</span><span class="sxs-lookup"><span data-stu-id="23940-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="23940-143">Örneğin,  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="23940-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="23940-144">Merhaba hello sonundaki **betik eylemleri**, hello kullan **seçin** düğme toosave hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="23940-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="23940-145">Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **bağlantılı depolama hesapları** ve select hello **depolama anahtarı eklemek** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="23940-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="23940-146">Hello Kavanoz içeren hello depolama hesabını seçin ve sonra hello **seçin** düğmeleri toosave ayarları ve dönüş hello **isteğe bağlı yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="23940-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="23940-147">Kullanım hello **seçin** düğmesi hello hello sonundaki **isteğe bağlı yapılandırma** dikey toosave hello isteğe bağlı yapılandırma bilgileri.</span><span class="sxs-lookup"><span data-stu-id="23940-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="23940-148">Bölümünde açıklandığı gibi Hello küme hazırlama devam [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="23940-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="23940-149">Küme oluşturma tamamlandıktan sonra bu komut dosyası aracılığıyla toouse hello gerek kalmadan kovanından eklenen mümkün toouse hello Kavanoz olan `ADD JAR` deyimi.</span><span class="sxs-lookup"><span data-stu-id="23940-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23940-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23940-150">Next steps</span></span>

<span data-ttu-id="23940-151">Hive ile çalışma hakkında daha fazla bilgi için bkz: [Hdınsight ile Hive kullanma](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="23940-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
