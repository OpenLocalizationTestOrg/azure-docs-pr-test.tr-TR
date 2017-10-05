---
title: "Betik eylemleri - Azure kullanarak Hdınsight kümelerini özelleştirme | Microsoft Docs"
description: "Özel bileşenler için betik eylemleri kullanarak Linux tabanlı Hdınsight kümelerini ekleyin. Betik eylemleri küme yapılandırmasını özelleştirebilir veya ek hizmetleri ve yardımcı programları ton, Solr veya r gibi eklemek için kullanılan Bash betikleridir"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="bc5f0-104">Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="bc5f0-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="bc5f0-105">Hdınsight adlı bir yapılandırma seçeneği sağlar **betik eylemi** küme özelleştirme özel komut dosyaları çağırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="bc5f0-106">Bu komut dosyalarını ek bileşenler yükleme ve yapılandırma ayarlarını değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="bc5f0-107">Betik eylemleri, sırasında veya Küme oluşturulduktan sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5f0-108">Betik eylemleri zaten çalışan bir kümede kullanma olanağı yalnızca Linux tabanlı Hdınsight kümeleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="bc5f0-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bc5f0-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="bc5f0-111">Betik eylemleri de Azure Marketi'nde bir Hdınsight uygulaması olarak yayımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="bc5f0-112">Bu belgedeki örneklerde bazıları, PowerShell ve .NET SDK'sı betik eylemi komutları kullanarak bir Hdınsight uygulamasının nasıl yükleyebileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="bc5f0-113">Hdınsight uygulamaları hakkında daha fazla bilgi için bkz: [yayımlama Hdınsight uygulamalarını Azure Marketi'nde](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="bc5f0-114">İzinler</span><span class="sxs-lookup"><span data-stu-id="bc5f0-114">Permissions</span></span>

<span data-ttu-id="bc5f0-115">Bir etki alanına katılmış Hdınsight kümesi kullanıyorsanız, betik eylemleri kümeyle kullanırken gerekli olan iki Ambari izinleri vardır:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="bc5f0-116">**AMBARI. ÇALIŞTIRMA\_özel\_KOMUTU**: Ambari Yönetici rolü varsayılan olarak bu izne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="bc5f0-117">**KÜME. ÇALIŞTIRMA\_özel\_KOMUTU**: her iki Hdınsight küme yöneticisinin ve Ambari yönetici varsayılan olarak bu izne sahip.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="bc5f0-118">İzinleri etki alanına katılmış Hdınsight ile çalışma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="bc5f0-119">Erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="bc5f0-119">Access control</span></span>

<span data-ttu-id="bc5f0-120">Hesabınızın, Azure aboneliğinizin Yöneticisi/sahibi değilseniz, en az olmalı **katkıda bulunan** Hdınsight kümesi içeren kaynak grubuna erişim.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="bc5f0-121">Ayrıca, Hdınsight kümesi, birisi ile en az oluşturuyorsanız **katkıda bulunan** Azure aboneliğine erişiminiz gerekir daha önce kaydettiğiniz Hdınsight için sağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="bc5f0-122">Sağlayıcı kaydı, aboneliğe Katkıda Bulunan erişimi olan bir kullanıcı abonelikte ilk kez kaynak oluşturduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="bc5f0-123">Bu işlem ayrıca [REST ile bir sağlayıcı kaydedilerek](https://msdn.microsoft.com/library/azure/dn790548.aspx) kaynak oluşturulmadan gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="bc5f0-124">Erişim yönetimiyle çalışma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="bc5f0-125">Azure portalında erişim yönetimi ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="bc5f0-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="bc5f0-126">Azure abonelik kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="bc5f0-127">Anlama betik eylemleri</span><span class="sxs-lookup"><span data-stu-id="bc5f0-127">Understanding Script Actions</span></span>

<span data-ttu-id="bc5f0-128">Bir komut dosyası yalnızca bir URI sağlayın Bash komut dosyası ve parametreleri bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="bc5f0-129">Hdınsight küme düğümlerinde komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="bc5f0-130">Aşağıdaki özellikleri ve betik eylemleri özelliklerini geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="bc5f0-131">Hdınsight küme erişilebilen bir URI üzerinde depolanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="bc5f0-132">Olası depolama konumları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="bc5f0-133">Bir **Azure Data Lake Store** Hdınsight küme tarafından erişilebilir olan hesap.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="bc5f0-134">Hdınsight ile Azure Data Lake Store hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="bc5f0-135">Data Lake Store'da depolanan bir komut dosyası kullanıldığında, URI biçimi `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="bc5f0-136">Hdınsight Data Lake Store erişmek için kullandığı hizmet sorumlusu komut dosyasını okuma erişimi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="bc5f0-137">Bir blobu bir **Azure depolama hesabı** diğer bir deyişle ya da birincil ya da ek depolama hesabı için Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="bc5f0-138">Hdınsight küme oluşturma sırasında iki depolama hesapları bu tür erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="bc5f0-139">Paylaşım Hizmeti Azure Blob, GitHub, OneDrive, Dropbox, vb. gibi ortak bir dosya.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="bc5f0-140">URI, örneğin bkz [örnek betik eylemi betikler](#example-script-action-scripts) bölümü.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="bc5f0-141">Hdınsight yalnızca destekler __genel amaçlı__ Azure depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="bc5f0-142">Şu anda desteklemediği __Blob storage__ hesap türü.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="bc5f0-143">Kısıtlanmış olabilir **yalnızca belirli düğüm türleri üzerinde çalıştırmak**örnek baş düğümler ve çalışan düğümleri için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bc5f0-144">Hdınsight Premium ile birlikte kullanıldığında, komut dosyası edge düğüm üzerinde kullanılmalıdır belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="bc5f0-145">Olabilir **kalıcı** veya **geçici**.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="bc5f0-146">**Kalıcı** komut dosyaları, komut çalıştıktan sonra kümesine çalışan düğümlerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="bc5f0-147">Örneğin, küme ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="bc5f0-148">Kalıcı bir betik, ayrıca bir baş düğüm gibi başka bir düğüm türü için değişiklikler uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="bc5f0-149">Kalıcı betik eylemleri benzersiz bir ad olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="bc5f0-150">**Geçici** betikleri kalıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="bc5f0-151">Çalışan düğümlerine sahip komut dosyasını çalıştırdıktan sonra kümesine uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="bc5f0-152">Daha sonra kalıcı bir betik için geçici bir komut dosyası yükseltmek veya geçici bir komut dosyası için kalıcı bir betik indirgemek.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="bc5f0-153">Küme oluşturma sırasında kullanılan betik eylemleri otomatik olarak kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="bc5f0-154">Başarısız olmayan betikleri özellikle olması gerektiğini belirtmek olsa bile kalıcı.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="bc5f0-155">Kabul edebilir **parametreleri** kullanılan komut dosyası tarafından yürütme sırasında.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="bc5f0-156">Çalıştırma **kök düzeyinde ayrıcalıklara** küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="bc5f0-157">Aracılığıyla kullanılan **Azure portal**, **Azure PowerShell**, **Azure CLI**, veya **Hdınsight .NET SDK'sı**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="bc5f0-158">Küme çalıştırdığınız sahip tüm betikler geçmişini tutar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="bc5f0-159">Geçmiş, yükseltme veya indirgeme işlemleri için bir komut dosyası Kimliğini bulmanız gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5f0-160">Bir komut dosyası eylemi tarafından yapılan değişiklikleri geri almak için otomatik bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="bc5f0-161">El ile değişikliklerinizi geri ya da bunları tersine çevirir bir komut dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="bc5f0-162">Küme oluşturma işlemi betik eylemi</span><span class="sxs-lookup"><span data-stu-id="bc5f0-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="bc5f0-163">Küme oluşturma sırasında kullanılan betik eylemleri eylemler var olan bir küme üzerinde çalışan komut dosyasından biraz farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="bc5f0-164">Komut dosyası **otomatik olarak kalıcı**.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="bc5f0-165">A **hatası** komut dosyasında küme oluşturma işleminin başarısız olmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="bc5f0-166">Betik eylemi oluşturma işlemi sırasında çalıştırıldığında aşağıdaki diyagramda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="bc5f0-167">![Hdınsight küme özelleştirme ve küme oluşturma sırasında aşamaları][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="bc5f0-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="bc5f0-168">Hdınsight yapılandırılırken komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="bc5f0-169">Bu aşamada, betik belirtilen kümedeki tüm düğümler üzerinde paralel olarak çalışır ve düğümlerde kök ayrıcalıklarıyla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="bc5f0-170">Komut dosyası kök düzeyinde ayrıcalığıyla küme düğümleri üzerinde çalıştığı için durdurma ve Hadoop ile ilgili hizmetlerin gibi hizmetler başlatma gibi işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="bc5f0-171">Hizmetleri durdurun, çalışan betik tamamlanmadan önce Ambari hizmet ve diğer Hadoop ile ilgili hizmetlerin hazır ve çalışır olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="bc5f0-172">Bu hizmetler, oluşturulurken başarıyla sistem durumunu ve küme durumunu belirlemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="bc5f0-173">Küme oluşturma sırasında aynı anda birden çok betik eylemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="bc5f0-174">Bu komut belirtilen sırada çağrılır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5f0-175">Betik eylemleri, 60 dakika veya zaman aşımı içinde tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="bc5f0-176">Küme hazırlama sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="bc5f0-177">CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden tamamlanması daha uzun sürmesine betik neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="bc5f0-178">Komut dosyasını çalıştırmak için gereken süreyi en aza indirmek için karşıdan yükleme ve kaynak uygulamalardan derleme gibi görevleri kaçının.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="bc5f0-179">Uygulamaları önceden derleme ve Azure depolama alanına ikili depolar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="bc5f0-180">Betik eylemi çalıştıran bir kümede</span><span class="sxs-lookup"><span data-stu-id="bc5f0-180">Script action on a running cluster</span></span>

<span data-ttu-id="bc5f0-181">Aksine, bir komut dosyasında hata küme oluşturma sırasında kullanılan eylemler zaten çalışan bir küme üzerinde çalışan komut dosyası otomatik olarak başarısız duruma değiştirmek küme neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="bc5f0-182">Bir komut dosyası tamamlandıktan sonra kümenin bir "çalışır" duruma dönmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5f0-183">Küme bir 'çalışıyor' durumuna sahip olsa bile, başarısız olan kodu şeyler kopuk olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="bc5f0-184">Örneğin, bir komut dosyası küme için gerekli dosyaları silebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="bc5f0-185">Kümenize uygulamadan önce bir komut dosyası yaptığı anladığınızdan emin olmanız gerekir böylece komut dosyalarını eylemleri kök ayrıcalıkları ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="bc5f0-186">Bir komut dosyası bir kümeye uygularken, küme durumunu için değişiklikleri **çalıştıran** için **kabul edilen**, ardından **Hdınsight yapılandırma**ve son olarak yeniden **çalıştıran** başarılı bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="bc5f0-187">Komut durumu betik eylemi geçmişinde kaydedilir ve komut başarılı veya başarısız olup olmadığını belirlemek için bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="bc5f0-188">Örneğin, `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet, bir komut dosyası durumunu görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="bc5f0-189">Bilgi aşağıdaki metni benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="bc5f0-190">Küme oluşturulduktan sonra küme kullanıcı (Yönetici) parolasını değiştirdiyseniz, bu küme karşı eylemler çalışan betik başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="bc5f0-191">Bu hedef çalışan düğümleri kalıcı betik eylemleri varsa, küme ölçeklendirdiğinizde bu komut dosyaları başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="bc5f0-192">Örnek betik eylemi betikler</span><span class="sxs-lookup"><span data-stu-id="bc5f0-192">Example Script Action scripts</span></span>

<span data-ttu-id="bc5f0-193">Betik eylemi komut dosyaları aşağıdaki yardımcı programlar kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="bc5f0-194">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="bc5f0-194">Azure portal</span></span>
* <span data-ttu-id="bc5f0-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc5f0-195">Azure PowerShell</span></span>
* <span data-ttu-id="bc5f0-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bc5f0-196">Azure CLI</span></span>
* <span data-ttu-id="bc5f0-197">HDInsight .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="bc5f0-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="bc5f0-198">Hdınsight Hdınsight kümelerinde aşağıdaki bileşenleri yüklemek için komut dosyaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="bc5f0-199">Ad</span><span class="sxs-lookup"><span data-stu-id="bc5f0-199">Name</span></span> | <span data-ttu-id="bc5f0-200">Betik</span><span class="sxs-lookup"><span data-stu-id="bc5f0-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="bc5f0-201">**Bir Azure depolama hesabı ekleme**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="bc5f0-202">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.sh. Bkz: [Hdınsight kümesi için ek depolama alanı eklentisi](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="bc5f0-203">**Hue yüklemek**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-203">**Install Hue**</span></span> |<span data-ttu-id="bc5f0-204">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/install-Hue-uber-v02.sh. Bkz: [yükleme ve kullanma ton hdınsight kümeleri](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="bc5f0-205">**Presto yükleyin**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-205">**Install Presto**</span></span> |<span data-ttu-id="bc5f0-206">https://RAW.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Bkz: [yükleme ve kullanma Presto hdınsight kümeleri](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="bc5f0-207">**Solr yükleyin**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-207">**Install Solr**</span></span> |<span data-ttu-id="bc5f0-208">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-installer-v01.sh. Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="bc5f0-209">**Giraph yükleyin**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-209">**Install Giraph**</span></span> |<span data-ttu-id="bc5f0-210">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="bc5f0-211">**Ön yük Hıve kitaplıkları**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="bc5f0-212">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Bkz: [eklemek Hive kitaplıkları Hdınsight kümelerinde](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="bc5f0-213">**Mono yükleme veya güncelleştirme**</span><span class="sxs-lookup"><span data-stu-id="bc5f0-213">**Install or update Mono**</span></span> | <span data-ttu-id="bc5f0-214">https://hdiconfigactions.BLOB.Core.Windows.NET/install-Mono/install-Mono.bash.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="bc5f0-215">Bkz: [yükleme veya güncelleştirme Mono hdınsight'ta](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="bc5f0-216">Küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="bc5f0-217">Bu bölümde, betik eylemleri bir Hdınsight kümesi oluştururken kullanabileceğiniz farklı yolları hakkında örnekler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="bc5f0-218">Azure portalından küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="bc5f0-219">Konusunda açıklandığı gibi bir küme oluşturmaya başlamak [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="bc5f0-220">Ulaştığınızda Durdur __küme Özet__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="bc5f0-221">Gelen __küme Özet__ bölümünde, select __Düzenle__ için bağlantı __Gelişmiş ayarları__.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![Gelişmiş ayarlar bağlantısı](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="bc5f0-223">Gelen __Gelişmiş ayarları__ bölümünde, select __betik eylemleri__.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="bc5f0-224">Gelen __betik eylemleri__ bölümünde, select __+ yeni Gönder__</span><span class="sxs-lookup"><span data-stu-id="bc5f0-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Yeni betik eylemi Gönder](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="bc5f0-226">Kullanım __bir komut dosyası seçin__ girişi önceden yapılmış bir komut dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="bc5f0-227">Özel bir komut dosyası kullanmayı seçin __özel__ ve ardından sağlayın __adı__ ve __betik URI Bash__ betiği için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="bc5f0-229">Aşağıdaki tabloda formda öğeleri açıklar:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="bc5f0-230">Özellik</span><span class="sxs-lookup"><span data-stu-id="bc5f0-230">Property</span></span> | <span data-ttu-id="bc5f0-231">Değer</span><span class="sxs-lookup"><span data-stu-id="bc5f0-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bc5f0-232">Bir komut dosyası seçin</span><span class="sxs-lookup"><span data-stu-id="bc5f0-232">Select a script</span></span> | <span data-ttu-id="bc5f0-233">Kendi komut dosyası kullanmayı seçin __özel__.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="bc5f0-234">Aksi durumda, sağlanan komut dosyalarından birini seçin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="bc5f0-235">Ad</span><span class="sxs-lookup"><span data-stu-id="bc5f0-235">Name</span></span> |<span data-ttu-id="bc5f0-236">Betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="bc5f0-237">Bash betik URI</span><span class="sxs-lookup"><span data-stu-id="bc5f0-237">Bash script URI</span></span> |<span data-ttu-id="bc5f0-238">Küme özelleştirmek için çağrılan betik URI'si belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="bc5f0-239">HEAD/çalışan/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="bc5f0-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="bc5f0-240">Düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) özelleştirme betik çalıştığı şirket.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="bc5f0-241">Parametreler</span><span class="sxs-lookup"><span data-stu-id="bc5f0-241">Parameters</span></span> |<span data-ttu-id="bc5f0-242">Komut dosyası tarafından gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="bc5f0-243">Kullanım __bu betik eylemini Sürdür__ komut dosyası işlemleri ölçeklendirme sırasında uygulandığından emin olmak için giriş.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="bc5f0-244">Seçin __oluşturma__ komut dosyasını kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="bc5f0-245">Daha sonra __+ gönderme yeni__ başka bir komut dosyası eklemek için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![Birden çok betik eylemleri](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="bc5f0-247">Komut dosyaları eklemeyi bitirdiğinizde, kullanmak __seçin__ düğmesine ve ardından __sonraki__ geri dönmek için düğmesini __küme özeti__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="bc5f0-248">Küme oluşturmak için seçin __oluşturma__ gelen __küme Özet__ seçim.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="bc5f0-249">Azure Resource Manager şablonları bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="bc5f0-250">Bu bölümdeki örnek betik eylemleri Azure Resource Manager şablonları ile kullanmak nasıl ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="bc5f0-251">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="bc5f0-251">Before you begin</span></span>

* <span data-ttu-id="bc5f0-252">Hdınsight Powershell cmdlet'lerini çalıştırmak için bir iş istasyonu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="bc5f0-253">Şablonlarının nasıl oluşturulacağı hakkında yönergeler için bkz [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="bc5f0-254">Resource Manager ile daha önce Azure PowerShell kullanmadıysanız, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="bc5f0-255">Betik eylemi kullanarak kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="bc5f0-256">Aşağıdaki şablonu bilgisayarınızdaki bir konuma kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="bc5f0-257">Bu şablon Giraph headnodes ve çalışan düğümleri yükler.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="bc5f0-258">Ayrıca, JSON şablonunu geçerli olup olmadığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="bc5f0-259">Şablonunuzu içerik içine yapıştırma [JSONLint](http://jsonlint.com/), bir çevrimiçi JSON doğrulama aracı.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="bc5f0-260">Azure PowerShell ve oturum açma Azure hesabınızda başlatın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="bc5f0-261">Kimlik bilgilerinizi girdikten sonra komutu, hesabınız hakkında bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="bc5f0-262">Birden çok aboneliğiniz varsa, dağıtım için kullanmak istediğiniz abonelik kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="bc5f0-263">Kullanabileceğiniz `Get-AzureRmSubscription` her biri için abonelik Kimliğini içeren, hesabınızla ilişkili tüm Aboneliklerin listesini almak için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="bc5f0-264">Varolan bir kaynak grubu yoksa, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="bc5f0-265">Çözümünüz için gereksinim duyduğunuz konumu ve kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="bc5f0-266">Yeni kaynak grubu özetini döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-266">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="bc5f0-267">Kaynak grubunuz için bir dağıtım oluşturmak için çalıştırın **New-AzureRmResourceGroupDeployment** komut ve gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="bc5f0-268">Parametreler aşağıdaki veriler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="bc5f0-269">Dağıtımınız için bir ad</span><span class="sxs-lookup"><span data-stu-id="bc5f0-269">A name for your deployment</span></span>
    * <span data-ttu-id="bc5f0-270">Kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="bc5f0-270">The name of your resource group</span></span>
    * <span data-ttu-id="bc5f0-271">Yolu veya URL'si, oluşturduğunuz şablon.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="bc5f0-272">Şablonunuzu herhangi bir parametre gerektiriyorsa, bu parametreler de geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="bc5f0-273">Bu durumda, küme üzerinde R yüklemek için betik eylemi herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="bc5f0-274">Şablonda tanımlanan parametreler için değerler sağlamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="bc5f0-275">Kaynak grubu dağıttığınızda dağıtımın bir özeti gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="bc5f0-276">Dağıtımınızı başarısız olursa hatalar hakkında bilgi almak için aşağıdaki cmdlet'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="bc5f0-277">Azure PowerShell üzerinden küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="bc5f0-278">Bu bölümde, kullanırız [Ekle AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) bir küme özelleştirmek için betik eylemi kullanarak komut dosyalarını çağrılacak cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="bc5f0-279">Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="bc5f0-280">Hdınsight PowerShell cmdlet'lerini çalıştırmak için bir iş istasyonu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="bc5f0-281">Aşağıdaki komut dosyası, PowerShell kullanarak bir küme oluştururken, bir komut dosyası eylemi uygulanacak gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="bc5f0-282">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="bc5f0-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="bc5f0-283">Küme oluşturulmadan önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="bc5f0-284">Hdınsight .NET SDK küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="bc5f0-285">Hdınsight .NET SDK'sı bir .NET uygulamasından Hdınsight ile çalışmayı kolaylaştırır istemci kitaplıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="bc5f0-286">Kod örneği için bkz: [.NET SDK kullanarak Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="bc5f0-287">Betik eylemi çalıştıran bir kümeye uygulama</span><span class="sxs-lookup"><span data-stu-id="bc5f0-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="bc5f0-288">Bu bölümde, betik eylemleri çalıştıran bir kümeye uygulamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="bc5f0-289">Betik eylemi çalıştıran bir kümeye Azure portalından uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="bc5f0-290">Gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="bc5f0-291">Hdınsight küme genel bakış'tan, seçin **betik eylemleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="bc5f0-293">Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** ayarları bölümünden.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="bc5f0-294">Betik eylemleri bölümünde üstten seçin **gönderme yeni**.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![Bir komut dosyası çalıştıran bir kümeye ekleme](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="bc5f0-296">Kullanım __bir komut dosyası seçin__ girişi önceden yapılmış bir komut dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="bc5f0-297">Özel bir komut dosyası kullanmayı seçin __özel__ ve ardından sağlayın __adı__ ve __betik URI Bash__ betiği için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="bc5f0-299">Aşağıdaki tabloda formda öğeleri açıklar:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="bc5f0-300">Özellik</span><span class="sxs-lookup"><span data-stu-id="bc5f0-300">Property</span></span> | <span data-ttu-id="bc5f0-301">Değer</span><span class="sxs-lookup"><span data-stu-id="bc5f0-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bc5f0-302">Bir komut dosyası seçin</span><span class="sxs-lookup"><span data-stu-id="bc5f0-302">Select a script</span></span> | <span data-ttu-id="bc5f0-303">Kendi komut dosyası kullanmayı seçin __özel__.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="bc5f0-304">Aksi durumda, sağlanan komut dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="bc5f0-305">Ad</span><span class="sxs-lookup"><span data-stu-id="bc5f0-305">Name</span></span> |<span data-ttu-id="bc5f0-306">Betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="bc5f0-307">Bash betik URI</span><span class="sxs-lookup"><span data-stu-id="bc5f0-307">Bash script URI</span></span> |<span data-ttu-id="bc5f0-308">Küme özelleştirmek için çağrılan betik URI'si belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="bc5f0-309">HEAD/çalışan/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="bc5f0-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="bc5f0-310">Düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) özelleştirme betik çalıştığı şirket.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="bc5f0-311">Parametreler</span><span class="sxs-lookup"><span data-stu-id="bc5f0-311">Parameters</span></span> |<span data-ttu-id="bc5f0-312">Komut dosyası tarafından gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="bc5f0-313">Kullanım __bu betik eylemini Sürdür__ komut dosyası işlemleri ölçeklendirme sırasında uygulanan emin olmak için giriş.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="bc5f0-314">Son olarak, **oluşturma** betik kümeye uygulamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="bc5f0-315">Betik eylemi çalıştıran bir kümeye Azure Powershell'den uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="bc5f0-316">Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="bc5f0-317">Hdınsight PowerShell cmdlet'lerini çalıştırmak için bir iş istasyonu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="bc5f0-318">Aşağıdaki örnek betik eylemi çalıştıran bir kümeye uygulama gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="bc5f0-319">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="bc5f0-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="bc5f0-320">İşlem tamamlandığında, aşağıdakine benzer bilgiler alırsınız:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="bc5f0-321">Betik eylemi çalıştıran bir kümeye Azure CLI üzerinden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="bc5f0-322">Devam etmeden önce Azure CLI yükleyip yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="bc5f0-323">Daha fazla bilgi için bkz: [Azure CLI yükleme](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="bc5f0-324">Azure Resource Manager moduna geçmek için komut satırında aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="bc5f0-325">Azure aboneliğinize kimliğini doğrulamak için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="bc5f0-326">Betik eylemi çalıştıran bir kümeye uygulamak için aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="bc5f0-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="bc5f0-327">Bu komutun parametresini atlarsanız, bunlar için istenir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="bc5f0-328">Komut dosyası ile belirtirseniz, `-u` parametreleri kabul belirtebilmeniz için kullanarak `-p` parametresi.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="bc5f0-329">Geçerli düğüm türleri `headnode`, `workernode`, ve `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="bc5f0-330">Komut dosyası birden çok düğüm türleri için uygulanması gereken, ayrılmış türlerini belirtin. bir ';'.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="bc5f0-331">Örneğin, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="bc5f0-332">Komut dosyası kalıcı hale getirmek için ekleme `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="bc5f0-333">Ayrıca komut dosyası daha sonra kullanarak kalıcı `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="bc5f0-334">İş tamamlandığında, aşağıdakine benzer bir çıktı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="bc5f0-335">REST API kullanarak çalışan bir küme için bir betik eylemi Uygula</span><span class="sxs-lookup"><span data-stu-id="bc5f0-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="bc5f0-336">Bkz: [çalıştırmak betik eylemleri çalıştıran bir kümede](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="bc5f0-337">Betik eylemi çalıştıran bir kümeye Hdınsight .NET SDK uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="bc5f0-338">Bir kümeye betikleri uygulamak için .NET SDK kullanarak bir örnek için bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="bc5f0-339">Betik eylemleri indirgemek geçmişini görüntülemek ve Yükselt</span><span class="sxs-lookup"><span data-stu-id="bc5f0-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="bc5f0-340">Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-340">Using the Azure portal</span></span>

1. <span data-ttu-id="bc5f0-341">Gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="bc5f0-342">Hdınsight küme genel bakış'tan, seçin **betik eylemleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="bc5f0-344">Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** ayarları bölümünden.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="bc5f0-345">Bu küme için komut geçmişini betik eylemleri bölümünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="bc5f0-346">Bu bilgiler kalıcı komut listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="bc5f0-347">Aşağıdaki ekran görüntüsünde, betiği bırakıldı Solr bu küme üzerinde çalışan görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="bc5f0-348">Ekran kalıcı herhangi bir komut dosyası göstermez.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-348">The screenshot does not show any persisted scripts.</span></span>

    ![Betik eylemleri bölümünde](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="bc5f0-350">Bir komut dosyası geçmişinden seçerek bu komut dosyası için özellikler bölümü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="bc5f0-351">Ekranın üst kısmından komut dosyasını yeniden çalıştırın ya da bunu yükseltin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Betik eylemleri özellikleri](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="bc5f0-353">Aynı zamanda **...**  eylemleri gerçekleştirmek için betik eylemleri bölümünde girişleri sağındaki.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![Eylemler... komut dosyası kullanımı](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="bc5f0-355">Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="bc5f0-356">Aşağıdaki kullan...</span><span class="sxs-lookup"><span data-stu-id="bc5f0-356">Use the following...</span></span> | <span data-ttu-id="bc5f0-357">Hedef...</span><span class="sxs-lookup"><span data-stu-id="bc5f0-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="bc5f0-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="bc5f0-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="bc5f0-359">Kalıcı betik eylemleri hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="bc5f0-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="bc5f0-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="bc5f0-361">Betik eylemleri küme veya belirli bir komut dosyası ayrıntılarını uygulanan geçmişini alma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="bc5f0-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="bc5f0-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="bc5f0-363">Bir geçici betik eylemi kalıcı betik eylemi yükseltir</span><span class="sxs-lookup"><span data-stu-id="bc5f0-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="bc5f0-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="bc5f0-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="bc5f0-365">Geçici bir eyleme kalıcı betik eylemi indirger</span><span class="sxs-lookup"><span data-stu-id="bc5f0-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bc5f0-366">Kullanarak `Remove-AzureRmHDInsightPersistedScriptAction` bir komut dosyası tarafından gerçekleştirilen eylemler geri almaz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="bc5f0-367">Bu cmdlet, yalnızca kalıcı bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="bc5f0-368">Aşağıdaki örnek betik yükseltin, sonra bir komut dosyası indirgemek için cmdlet'leri kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="bc5f0-369">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="bc5f0-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="bc5f0-370">Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-370">Using the Azure CLI</span></span>

| <span data-ttu-id="bc5f0-371">Aşağıdaki kullan...</span><span class="sxs-lookup"><span data-stu-id="bc5f0-371">Use the following...</span></span> | <span data-ttu-id="bc5f0-372">Hedef...</span><span class="sxs-lookup"><span data-stu-id="bc5f0-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="bc5f0-373">Kalıcı betik eylemlerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="bc5f0-374">Belirli kalıcı betik eylemi hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="bc5f0-375">Betik eylemleri kümeye uygulanan geçmişini alma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="bc5f0-376">Bir özel betik eylemi hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="bc5f0-377">Bir geçici betik eylemi kalıcı betik eylemi yükseltir</span><span class="sxs-lookup"><span data-stu-id="bc5f0-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="bc5f0-378">Geçici bir eyleme kalıcı betik eylemi indirger</span><span class="sxs-lookup"><span data-stu-id="bc5f0-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bc5f0-379">Kullanarak `azure hdinsight script-action persisted delete` bir komut dosyası tarafından gerçekleştirilen eylemler geri almaz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="bc5f0-380">Bu cmdlet, yalnızca kalıcı bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="bc5f0-381">Hdınsight .NET SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="bc5f0-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="bc5f0-382">Bir kümeden betik geçmişi almak için .NET SDK kullanarak bir örnek için yükseltmek veya betikleri indirgemek, bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="bc5f0-383">Bu örnek ayrıca .NET SDK kullanarak bir Hdınsight uygulamasının nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="bc5f0-384">Hdınsight kümelerinde kullanılan açık kaynaklı yazılım desteği</span><span class="sxs-lookup"><span data-stu-id="bc5f0-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="bc5f0-385">Microsoft Azure Hdınsight hizmeti, açık kaynaklı teknolojileri Hadoop biçimlendirilmiş bir ekosistemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="bc5f0-386">Microsoft Azure, açık kaynaklı teknolojileri için genel düzeyde desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="bc5f0-387">Daha fazla bilgi için bkz: **destek kapsamı** bölümünü [Azure destek SSS Web sitesine](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="bc5f0-388">Hdınsight hizmeti yerleşik bileşenleri için destek, ek bir düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="bc5f0-389">Hdınsight hizmetinde bulunan açık kaynak bileşenleri iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="bc5f0-390">**Yerleşik bileşenlerini** -bu bileşenlerin Hdınsight kümelerinde önceden yüklü olduğundan ve küme çekirdek işlevselliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="bc5f0-391">Örneğin, YARN ResourceManager, Hive sorgu dili (HiveQL) ve Mahout kitaplık bu kategoriye ait.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="bc5f0-392">Küme bileşenlerin tam bir listesi kullanılabilir [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="bc5f0-393">**Özel bileşenler** -, bir kullanıcı kümesi olarak yükleyebilir veya topluluk bulunan ya da sizin tarafınızdan oluşturulan herhangi bir bileşenin, iş yükü kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="bc5f0-394">Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="bc5f0-395">Microsoft Support yalıtmak ve bu bileşenleri ilgili sorunları gidermek için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="bc5f0-396">Özel bileşenler, daha fazla sorun gidermenize yardımcı olması için ticari koşulların elverdiği oranda makul destek alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="bc5f0-397">Microsoft destek sorunu çözmek mümkün olabilir veya bu teknoloji derin uzmanlık bulunduğu açık kaynak teknolojileri için kullanılabilir kanalları gerçekleştirmesine olanak isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="bc5f0-398">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="bc5f0-399">Hdınsight hizmeti özel bileşenleri kullanmak için çeşitli yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="bc5f0-400">Aynı düzeyde desteği nasıl bir bileşen kullanılan veya kümeye yüklü bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="bc5f0-401">En sık karşılaşılan aşağıdaki listede açıklanmaktadır özel bileşenler Hdınsight kümelerinde kullanılabileceği yol vardır:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="bc5f0-402">İş gönderme - Hadoop veya diğer tür execute veya özel bileşenleri kullanan işi kümeye gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="bc5f0-403">Küme özelleştirme - küme oluşturma sırasında ek ayarlar ve küme düğümlerinde yüklü özel bileşenleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="bc5f0-404">Örnekler - popüler özel bileşenleri, Microsoft ve diğerleri için bu bileşenlerin Hdınsight kümelerinde nasıl kullanılabileceğini örnek sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="bc5f0-405">Bu örnekler desteği olmadan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bc5f0-406">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="bc5f0-406">Troubleshooting</span></span>

<span data-ttu-id="bc5f0-407">Betik eylemleri tarafından günlüğe kaydedilen bilgi görüntülemek için Ambari web kullanıcı Arabirimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="bc5f0-408">Küme oluşturma sırasında komut başarısız olursa, günlükleri kümeyle ilişkili varsayılan depolama hesabı mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="bc5f0-409">Bu bölümde hem bu seçenekleri kullanarak günlüklerini alma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="bc5f0-410">Ambari Web kullanıcı Arabirimi kullanma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="bc5f0-411">Tarayıcınızda, https://CLUSTERNAME.azurehdinsight.net için gidin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="bc5f0-412">CLUSTERNAME Hdınsight kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="bc5f0-413">İstendiğinde, küme için yönetici hesabı adını (Yönetici) ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="bc5f0-414">Bir web formunda yönetici kimlik bilgilerinizi yeniden girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="bc5f0-415">Sayfanın üstündeki çubuğundan seçin **ops** girişi.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="bc5f0-416">Ambari aracılığıyla küme üzerinde gerçekleştirilen işlemler geçerli ve önceki bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Seçili ops ile Ambari web kullanıcı Arabirimi çubuğu](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="bc5f0-418">Sahip girişlerini bulmak **çalıştırmak\_customscriptaction** içinde **Operations** sütun.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="bc5f0-419">Betik eylemleri çalıştırdığınızda bu girişleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-419">These entries are created when the Script Actions run.</span></span>

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="bc5f0-421">STDOUT ve STDERR çıktısı görüntülemek için run\customscriptaction girişi seçin ve bağlantılar aracılığıyla detaya.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="bc5f0-422">Komut dosyası çalıştığında, bu çıkışı oluşturulur ve yararlı bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="bc5f0-423">Varsayılan depolama hesabı erişim günlükleri</span><span class="sxs-lookup"><span data-stu-id="bc5f0-423">Access logs from the default storage account</span></span>

<span data-ttu-id="bc5f0-424">Küme oluşturma bir betik eylemi hatası nedeniyle başarısız olursa, günlükleri küme depolama hesabından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="bc5f0-425">Depolama günlüklerine kullanılabilir `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="bc5f0-427">Bu dizin altında headnode, workernode ve zookeeper düğümleri için günlükleri ayrı olarak düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="bc5f0-428">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-428">Some examples are:</span></span>

    * <span data-ttu-id="bc5f0-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="bc5f0-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="bc5f0-430">**Çalışan düğümü** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="bc5f0-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="bc5f0-431">**Zookeeper düğümü** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="bc5f0-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="bc5f0-432">Tüm stdout ve stderr karşılık gelen konağının depolama hesabına karşıya.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="bc5f0-433">Bir **çıkış -\*.txt** ve **hataları -\*.txt** her komut dosyası eylemi için.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="bc5f0-434">Çıktı *.txt dosya konakta çalışan komut dosyasının URI hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="bc5f0-435">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="bc5f0-436">Betik eylemi küme sürekli olarak aynı ada sahip oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="bc5f0-437">Böyle bir durumda tarih klasör adını temel alarak ilgili günlükleri ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="bc5f0-438">Örneğin, farklı tarihlerde oluşturulan bir küme (contoso.com) için klasör yapısı aşağıdaki günlük girdileri benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="bc5f0-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="bc5f0-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="bc5f0-440">Aynı gün içinde aynı ada sahip bir komut dosyası eylemi kümesi oluşturursanız, ilgili günlük dosyalarını tanımlamak için benzersiz önek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="bc5f0-441">Bir küme 12: 00'da (gece yarısı) yakın oluşturursanız, günlük dosyaları iki gün boyunca span mümkündür.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="bc5f0-442">Böyle durumlarda, aynı küme için iki farklı tarih klasörleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="bc5f0-443">Günlük dosyaları için varsayılan kapsayıcı karşıya yükleme, özellikle büyük kümeleri için 5 dakika kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="bc5f0-444">Günlüklere erişmek istiyorsanız, bir komut dosyası eylemi başarısız olursa bu nedenle, hemen küme silmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="bc5f0-445">Ambari izleme</span><span class="sxs-lookup"><span data-stu-id="bc5f0-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="bc5f0-446">Linux tabanlı Hdınsight kümenizdeki Ambari izleme (hdinsightwatchdog) için parolayı değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="bc5f0-447">Bu hesabın parolasını değiştirme Hdınsight kümesinde yeni betik eylemleri çalıştırma yeteneğini keser.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="bc5f0-448">Ad BlobService içeri aktarılamıyor</span><span class="sxs-lookup"><span data-stu-id="bc5f0-448">Can't import name BlobService</span></span>

<span data-ttu-id="bc5f0-449">__Belirtiler__: betik eylemi başarısız.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="bc5f0-450">İşlemi Ambari içinde görüntülediğinizde, aşağıdakine benzer bir metin görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="bc5f0-451">__Neden__: Hdınsight kümesi ile birlikte Python Azure Storage istemcisi yükseltirseniz, bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="bc5f0-452">Hdınsight Azure Storage istemci 0.20.0 bekliyor.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="bc5f0-453">__Çözümleme__: Bu hatayı gidermek için el ile her küme düğümünü kullanarak bağlanma `ssh` ve doğru depolama istemci sürümünü yeniden yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="bc5f0-454">SSH kümeye bağlanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bc5f0-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="bc5f0-455">Küme oluşturma sırasında kullanılan komut geçmişi göstermiyor</span><span class="sxs-lookup"><span data-stu-id="bc5f0-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="bc5f0-456">Kümenizi 15 Mart 2016'dan önce oluşturulduysa, bir giriş betik eylemi geçmişinde göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="bc5f0-457">15 Mart 2016'dan sonra kümeyi yeniden boyutlandırmak, bunlar yeni düğümleri yeniden boyutlandırma işlemi bir parçası olarak uygulanır olarak küme oluşturma sırasında kullanarak komut geçmişinde görünür.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="bc5f0-458">İki istisna mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-458">There are two exceptions:</span></span>

* <span data-ttu-id="bc5f0-459">Kümenizi 1 Eylül 2015 önce oluşturulduysa.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="bc5f0-460">Betik eylemleri kullanıma sunulan, bu tarih olur.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="bc5f0-461">Bu tarihten önce oluşturulan herhangi bir küme betik eylemleri küme oluşturma için kullanılmamış.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="bc5f0-462">Birden çok betik eylemleri küme oluşturma sırasında kullanılır ve birden fazla komut dosyası için aynı adı veya aynı adı, aynı URI, ancak farklı parametreler birden fazla komut dosyası için kullanılan istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="bc5f0-463">Bu durumlarda, aşağıdaki hatayı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="bc5f0-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="bc5f0-464">Varolan komut dosyalarında çakışan betik adları nedeniyle bu kümede eylemler olabilir yeni betik verdi.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="bc5f0-465">Kümesine sağlanan betik adları oluşturmak gereken tüm benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="bc5f0-466">Varolan komut dosyalarını yeniden boyutlandırma üzerinde verdi.</span><span class="sxs-lookup"><span data-stu-id="bc5f0-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc5f0-467">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc5f0-467">Next steps</span></span>

* [<span data-ttu-id="bc5f0-468">Hdınsight için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="bc5f0-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="bc5f0-469">Yükleme ve Hdınsight kümelerinde Solr kullanma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="bc5f0-470">Yükleme ve Hdınsight kümelerinde Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="bc5f0-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="bc5f0-471">Hdınsight kümesi için ek depolama alanı eklentisi</span><span class="sxs-lookup"><span data-stu-id="bc5f0-471">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

<span data-ttu-id="bc5f0-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Küme oluşturma sırasında aşamaları"</span><span class="sxs-lookup"><span data-stu-id="bc5f0-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
