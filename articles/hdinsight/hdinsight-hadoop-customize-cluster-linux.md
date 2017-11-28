---
title: "aaaCustomize betik eylemleri - Azure kullanarak Hdınsight kümelerini | Microsoft Docs"
description: "Betik eylemleri kullanılarak tooLinux tabanlı Hdınsight kümeleri özel bileşenleri ekleyin. Betik eylemleri, kullanılan toocustomize hello küme yapılandırması veya ek hizmetleri ve yardımcı programları ton, Solr veya r gibi ekleme Bash betikleridir"
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="8e035-104">Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8e035-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="8e035-105">Hdınsight adlı bir yapılandırma seçeneği sağlar **betik eylemi** hello küme özelleştirme özel komut dosyaları çağırır.</span><span class="sxs-lookup"><span data-stu-id="8e035-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="8e035-106">Bu komut dosyaları kullanılan tooinstall ek bileşenleridir ve yapılandırma ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="8e035-107">Betik eylemleri, sırasında veya Küme oluşturulduktan sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e035-108">Merhaba özelliği toouse betik eylemleri zaten çalışan bir kümede yalnızca Linux tabanlı Hdınsight kümeleri için mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="8e035-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="8e035-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="8e035-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8e035-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8e035-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="8e035-111">Betik eylemleri, ayrıca bir Hdınsight uygulaması olarak yayımlanan toohello Azure Marketi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="8e035-112">Bu belgedeki örneklerde hello bazıları, PowerShell ve .NET SDK'sı hello betik eylemi komutları kullanarak bir Hdınsight uygulamasının nasıl yükleyebileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="8e035-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="8e035-113">Hdınsight uygulamaları hakkında daha fazla bilgi için bkz: [hello Azure Marketi'nde yayımlama Hdınsight uygulamalarınızı](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="8e035-114">İzinler</span><span class="sxs-lookup"><span data-stu-id="8e035-114">Permissions</span></span>

<span data-ttu-id="8e035-115">Bir etki alanına katılmış Hdınsight kümesi kullanıyorsanız, betik eylemleri ile Merhaba kümesi kullanırken gerekli olan iki Ambari izinleri vardır:</span><span class="sxs-lookup"><span data-stu-id="8e035-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="8e035-116">**AMBARI. ÇALIŞTIRMA\_özel\_KOMUTU**: Merhaba Ambari Yönetici rolü varsayılan olarak bu izne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8e035-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="8e035-117">**KÜME. ÇALIŞTIRMA\_özel\_KOMUTU**: her ikisi de Hdınsight küme yöneticisinin hello ve Ambari yönetici varsayılan olarak bu izne sahip.</span><span class="sxs-lookup"><span data-stu-id="8e035-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="8e035-118">İzinleri etki alanına katılmış Hdınsight ile çalışma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="8e035-119">Erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="8e035-119">Access control</span></span>

<span data-ttu-id="8e035-120">Azure aboneliğiniz hello Yöneticisi/sahibi değilseniz, hesabınızın en az olmalı **katkıda bulunan** hello Hdınsight kümesi içeren erişim toohello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="8e035-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="8e035-121">Ayrıca, Hdınsight kümesi, birisi ile en az oluşturuyorsanız **katkıda bulunan** erişim toohello Azure aboneliği gerekir daha önce kaydettiğiniz Hdınsight için hello sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8e035-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="8e035-122">Katkıda bulunan erişim toohello aboneliği olan bir kullanıcı ilk kez hello abonelikte hello için bir kaynak oluşturduğunda sağlayıcı kaydı olur.</span><span class="sxs-lookup"><span data-stu-id="8e035-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="8e035-123">Bu işlem ayrıca [REST ile bir sağlayıcı kaydedilerek](https://msdn.microsoft.com/library/azure/dn790548.aspx) kaynak oluşturulmadan gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="8e035-124">Erişim yönetimi ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="8e035-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="8e035-125">Hello Azure portalına erişim yönetimi kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8e035-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="8e035-126">Rol atamaları toomanage erişim tooyour Azure aboneliği kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="8e035-127">Anlama betik eylemleri</span><span class="sxs-lookup"><span data-stu-id="8e035-127">Understanding Script Actions</span></span>

<span data-ttu-id="8e035-128">Bir komut dosyası yalnızca bir URI sağlayın Bash komut dosyası ve parametreleri bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="8e035-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="8e035-129">Merhaba Hdınsight küme düğümlerinde Hello komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="8e035-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="8e035-130">özellikleri ve betik eylemleri özelliklerini Hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8e035-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="8e035-131">Merhaba Hdınsight kümeden erişilebilir olduğunu URI üzerinde depolanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e035-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="8e035-132">Merhaba, olası depolama konumları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8e035-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="8e035-133">Bir **Azure Data Lake Store** hello Hdınsight küme tarafından erişilebilir olan hesap.</span><span class="sxs-lookup"><span data-stu-id="8e035-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="8e035-134">Hdınsight ile Azure Data Lake Store hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="8e035-135">Data Lake Store'da depolanan bir komut dosyası, hello URI biçimi kullanıldığında `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="8e035-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="8e035-136">Merhaba hizmet asıl Hdınsight kullandığı tooaccess Data Lake Store okuma erişimi toohello komut dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e035-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="8e035-137">Bir blobu bir **Azure depolama hesabı** hello Hdınsight kümesi için herhangi bir hello birincil ya da ek depolama hesabı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="8e035-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="8e035-138">Hdınsight küme oluşturma sırasında depolama hesapları bu tür erişim tooboth verilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="8e035-139">Paylaşım Hizmeti Azure Blob, GitHub, OneDrive, Dropbox, vb. gibi ortak bir dosya.</span><span class="sxs-lookup"><span data-stu-id="8e035-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="8e035-140">Örneğin URI, bakın hello [örnek betik eylemi betikler](#example-script-action-scripts) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8e035-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="8e035-141">Hdınsight yalnızca destekler __genel amaçlı__ Azure depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="8e035-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="8e035-142">Merhaba şu anda desteklemiyor __Blob storage__ hesap türü.</span><span class="sxs-lookup"><span data-stu-id="8e035-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="8e035-143">Çok kısıtlanabilir**yalnızca belirli düğüm türleri üzerinde çalıştırmak**örnek baş düğümler ve çalışan düğümleri için.</span><span class="sxs-lookup"><span data-stu-id="8e035-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8e035-144">Hdınsight Premium ile birlikte kullanıldığında, hello betik hello kenar düğümüne kullanılması gerektiğini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="8e035-145">Olabilir **kalıcı** veya **geçici**.</span><span class="sxs-lookup"><span data-stu-id="8e035-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="8e035-146">**Kalıcı** betiklerdir uygulanan tooworker düğümleri eklenen toohello küme hello betik çalıştıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="8e035-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="8e035-147">Örneğin, Hello küme ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="8e035-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="8e035-148">Kalıcı bir betik bir baş düğüm gibi değişiklikler tooanother düğüm türü de geçerli.</span><span class="sxs-lookup"><span data-stu-id="8e035-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8e035-149">Kalıcı betik eylemleri benzersiz bir ad olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e035-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="8e035-150">**Geçici** betikleri kalıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="8e035-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="8e035-151">Sahip Hello betiği çalıştırdıktan sonra bunlar uygulanan tooworker düğümleri eklenen toohello küme olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="8e035-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="8e035-152">Sonradan bir geçici kod tooa yükseltebilirsiniz betik kalıcı ya da kalıcı betik tooan geçici betik indirgemek.</span><span class="sxs-lookup"><span data-stu-id="8e035-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8e035-153">Küme oluşturma sırasında kullanılan betik eylemleri otomatik olarak kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8e035-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="8e035-154">Başarısız olmayan betikleri özellikle olması gerektiğini belirtmek olsa bile kalıcı.</span><span class="sxs-lookup"><span data-stu-id="8e035-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="8e035-155">Kabul edebilir **parametreleri** kullanılan hello komut dosyası tarafından yürütme sırasında.</span><span class="sxs-lookup"><span data-stu-id="8e035-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="8e035-156">Çalıştırma **kök düzeyinde ayrıcalıklara** hello küme düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="8e035-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="8e035-157">Merhaba kullanılabilir **Azure portal**, **Azure PowerShell**, **Azure CLI**, veya **Hdınsight .NET SDK'sı**</span><span class="sxs-lookup"><span data-stu-id="8e035-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="8e035-158">Merhaba küme çalıştırdığınız sahip tüm betikler geçmişini tutar.</span><span class="sxs-lookup"><span data-stu-id="8e035-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="8e035-159">hello geçmişi, yükseltme veya indirgeme işlemleri için bir komut dosyası toofind hello kimliği gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8e035-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e035-160">Hiçbir otomatik şekilde tooundo yoktur hello bir betik eylemi tarafından yapılan değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="8e035-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="8e035-161">El ile Merhaba değişiklikleri ters ya da bunları tersine çevirir bir komut dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="8e035-162">Betik eylemi hello küme oluşturma işlemi</span><span class="sxs-lookup"><span data-stu-id="8e035-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="8e035-163">Küme oluşturma sırasında kullanılan betik eylemleri eylemler var olan bir küme üzerinde çalışan komut dosyasından biraz farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="8e035-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="8e035-164">Merhaba komut dosyası **otomatik olarak kalıcı**.</span><span class="sxs-lookup"><span data-stu-id="8e035-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="8e035-165">A **hatası** hello betik hello küme oluşturma işlemi toofail neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="8e035-166">Betik eylemi hello oluşturma işlemi sırasında çalıştırıldığında hello Aşağıdaki diyagramda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="8e035-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="8e035-167">![Hdınsight küme özelleştirme ve küme oluşturma sırasında aşamaları][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="8e035-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="8e035-168">Hdınsight yapılandırılırken hello komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="8e035-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="8e035-169">Bu aşamada, tüm paralel hello komut dosyasını çalıştırır hello küme ve kök ayrıcalıklarıyla çalıştırır hello düğümlerde bulunan belirli düğümler hello.</span><span class="sxs-lookup"><span data-stu-id="8e035-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="8e035-170">Merhaba komut dosyası kök düzeyinde ayrıcalığıyla hello küme düğümleri üzerinde çalıştığı için durdurma ve Hadoop ile ilgili hizmetlerin gibi hizmetler başlatma gibi işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="8e035-171">Hizmetleri durdurursanız, hello komut dosyası çalıştırma tamamlanmadan önce hello ambarı hizmet ve diğer Hadoop ile ilgili hizmetlerin hazır ve çalışır olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8e035-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="8e035-172">Bu hizmetler gerekli toosuccessfully, hello sistem durumu ve hello küme durumunu, oluşturulurken belirler.</span><span class="sxs-lookup"><span data-stu-id="8e035-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="8e035-173">Küme oluşturma sırasında aynı anda birden çok betik eylemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="8e035-174">Bu komut dosyalarını belirtilmiş olması hello sırayla çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8e035-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e035-175">Betik eylemleri, 60 dakika veya zaman aşımı içinde tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e035-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="8e035-176">Küme hazırlama sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak hello komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="8e035-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="8e035-177">CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden hello betik tootake uzun toofinish neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="8e035-178">toominimize hello alır toorun hello komut dosyası zaman, yükleme ve kaynak uygulamalardan derleme gibi görevleri kaçının.</span><span class="sxs-lookup"><span data-stu-id="8e035-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="8e035-179">Uygulamaları önceden derleme ve Azure depolama alanına hello ikili depolar.</span><span class="sxs-lookup"><span data-stu-id="8e035-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="8e035-180">Betik eylemi çalıştıran bir kümede</span><span class="sxs-lookup"><span data-stu-id="8e035-180">Script action on a running cluster</span></span>

<span data-ttu-id="8e035-181">Aksine, bir komut dosyasında hata küme oluşturma sırasında kullanılan eylemler zaten çalışan bir küme üzerinde çalışan komut dosyası otomatik olarak hello küme toochange başarısız tooa durumunun neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="8e035-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="8e035-182">Bir komut dosyası tamamlandıktan sonra hello küme "çalışır" tooa döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="8e035-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e035-183">Merhaba küme 'çalışıyor' durumu olsa bile hello başarısız betik şeyler kopuk olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="8e035-184">Örneğin, bir komut dosyası hello kümenin gerektirdiği dosyaları silebilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="8e035-185">Tooyour küme uygulamadan önce bir komut dosyası yaptığı anladığınızdan emin olmanız gerekir böylece komut dosyalarını eylemleri kök ayrıcalıkları ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e035-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="8e035-186">Bir komut dosyası tooa küme uygularken toofrom hello küme durumunu değiştirir **çalıştıran** çok**kabul edilen**, ardından **Hdınsight yapılandırma**ve son olarak çok geri**Çalıştıran** başarılı bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8e035-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="8e035-187">Merhaba betik durum hello betik eylemi geçmişinde günlüğe kaydedilir ve hello komut başarılı veya başarısız olup olmadığını, bu bilgileri toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="8e035-188">Örneğin, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet'ini bir komut dosyası kullanılan tooview hello durumu olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="8e035-189">Metin aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="8e035-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="8e035-190">Merhaba Küme oluşturulduktan sonra hello küme kullanıcı (Yönetici) parolasını değiştirdiyseniz, bu küme karşı eylemler çalışan betik başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="8e035-191">Bu hedef çalışan düğümleri kalıcı betik eylemleri varsa, bu komut dosyalarını hello küme ölçeklendirdiğinizde başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="8e035-192">Örnek betik eylemi betikler</span><span class="sxs-lookup"><span data-stu-id="8e035-192">Example Script Action scripts</span></span>

<span data-ttu-id="8e035-193">Betik eylemi betikleri yardımcı programlarını aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8e035-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="8e035-194">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="8e035-194">Azure portal</span></span>
* <span data-ttu-id="8e035-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e035-195">Azure PowerShell</span></span>
* <span data-ttu-id="8e035-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e035-196">Azure CLI</span></span>
* <span data-ttu-id="8e035-197">HDInsight .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="8e035-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="8e035-198">Hdınsight Hdınsight kümelerinde bileşenleri aşağıdaki betikler tooinstall hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="8e035-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="8e035-199">Ad</span><span class="sxs-lookup"><span data-stu-id="8e035-199">Name</span></span> | <span data-ttu-id="8e035-200">Betik</span><span class="sxs-lookup"><span data-stu-id="8e035-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="8e035-201">**Bir Azure depolama hesabı ekleme**</span><span class="sxs-lookup"><span data-stu-id="8e035-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="8e035-202">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.sh. Bkz: [ekle ek depolama alanı tooan Hdınsight kümesi](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="8e035-203">**Hue yüklemek**</span><span class="sxs-lookup"><span data-stu-id="8e035-203">**Install Hue**</span></span> |<span data-ttu-id="8e035-204">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/install-Hue-uber-v02.sh. Bkz: [yükleme ve kullanma ton hdınsight kümeleri](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="8e035-205">**Presto yükleyin**</span><span class="sxs-lookup"><span data-stu-id="8e035-205">**Install Presto**</span></span> |<span data-ttu-id="8e035-206">https://RAW.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Bkz: [yükleme ve kullanma Presto hdınsight kümeleri](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="8e035-207">**Solr yükleyin**</span><span class="sxs-lookup"><span data-stu-id="8e035-207">**Install Solr**</span></span> |<span data-ttu-id="8e035-208">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-installer-v01.sh. Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="8e035-209">**Giraph yükleyin**</span><span class="sxs-lookup"><span data-stu-id="8e035-209">**Install Giraph**</span></span> |<span data-ttu-id="8e035-210">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="8e035-211">**Ön yük Hıve kitaplıkları**</span><span class="sxs-lookup"><span data-stu-id="8e035-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="8e035-212">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Bkz: [eklemek Hive kitaplıkları Hdınsight kümelerinde](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="8e035-213">**Mono yükleme veya güncelleştirme**</span><span class="sxs-lookup"><span data-stu-id="8e035-213">**Install or update Mono**</span></span> | <span data-ttu-id="8e035-214">https://hdiconfigactions.BLOB.Core.Windows.NET/install-Mono/install-Mono.bash.</span><span class="sxs-lookup"><span data-stu-id="8e035-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="8e035-215">Bkz: [yükleme veya güncelleştirme Mono hdınsight'ta](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="8e035-216">Küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="8e035-217">Bu bölümde, betik eylemleri bir Hdınsight kümesi oluştururken kullanabileceğiniz hello farklı yolları üzerinde örnekler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8e035-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="8e035-218">Hello Azure Portalı'ndan küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="8e035-219">Konusunda açıklandığı gibi bir küme oluşturmaya başlamak [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="8e035-220">Merhaba ulaştığında Durdur __küme Özet__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="8e035-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="8e035-221">Merhaba gelen __küme Özet__ bölümü, select hello __Düzenle__ için bağlantı __Gelişmiş ayarları__.</span><span class="sxs-lookup"><span data-stu-id="8e035-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Gelişmiş ayarlar bağlantısı](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="8e035-223">Merhaba gelen __Gelişmiş ayarları__ bölümünde, select __betik eylemleri__.</span><span class="sxs-lookup"><span data-stu-id="8e035-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="8e035-224">Merhaba gelen __betik eylemleri__ bölümünde, select __+ yeni Gönder__</span><span class="sxs-lookup"><span data-stu-id="8e035-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Yeni betik eylemi Gönder](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="8e035-226">Kullanım hello __bir komut dosyası seçin__ girişi tooselect önceden yapılmış bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8e035-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="8e035-227">toouse özel bir komut dosyası seçin __özel__ ve hello sağlamak __adı__ ve __betik URI Bash__ betiği için.</span><span class="sxs-lookup"><span data-stu-id="8e035-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Merhaba select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="8e035-229">Aşağıdaki tablonun hello hello öğeleri hello formunda açıklar:</span><span class="sxs-lookup"><span data-stu-id="8e035-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="8e035-230">Özellik</span><span class="sxs-lookup"><span data-stu-id="8e035-230">Property</span></span> | <span data-ttu-id="8e035-231">Değer</span><span class="sxs-lookup"><span data-stu-id="8e035-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8e035-232">Bir komut dosyası seçin</span><span class="sxs-lookup"><span data-stu-id="8e035-232">Select a script</span></span> | <span data-ttu-id="8e035-233">toouse select kendi betiğinizi __özel__.</span><span class="sxs-lookup"><span data-stu-id="8e035-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="8e035-234">Aksi durumda, sağlanan hello komut dosyalarından birini seçin.</span><span class="sxs-lookup"><span data-stu-id="8e035-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="8e035-235">Ad</span><span class="sxs-lookup"><span data-stu-id="8e035-235">Name</span></span> |<span data-ttu-id="8e035-236">Merhaba betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="8e035-237">Bash betik URI</span><span class="sxs-lookup"><span data-stu-id="8e035-237">Bash script URI</span></span> |<span data-ttu-id="8e035-238">Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="8e035-239">HEAD/çalışan/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="8e035-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="8e035-240">Merhaba düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) hangi hello özelleştirme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e035-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="8e035-241">Parametreler</span><span class="sxs-lookup"><span data-stu-id="8e035-241">Parameters</span></span> |<span data-ttu-id="8e035-242">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="8e035-243">Kullanım hello __bu betik eylemini Sürdür__ betik hello girişi tooensure ölçeklendirme işlemleri sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8e035-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="8e035-244">Seçin __oluşturma__ toosave hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8e035-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="8e035-245">Daha sonra __+ gönderme yeni__ tooadd başka bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8e035-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Birden çok betik eylemleri](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="8e035-247">Komut dosyaları eklemeyi bitirdiğinizde, hello kullan __seçin__ düğmesine tıklayın ve ardından hello __sonraki__ düğmesini tooreturn toohello __küme Özet__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="8e035-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="8e035-248">toocreate hello küme, select __oluşturma__ hello gelen __küme Özet__ seçim.</span><span class="sxs-lookup"><span data-stu-id="8e035-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="8e035-249">Azure Resource Manager şablonları bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="8e035-250">Bu bölümdeki Hello örnekleri toouse Eylemler Azure Resource Manager şablonları ile nasıl komut dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8e035-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="8e035-251">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8e035-251">Before you begin</span></span>

* <span data-ttu-id="8e035-252">Bir iş istasyonu toorun Hdınsight Powershell cmdlet'leri yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e035-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="8e035-253">Yönergeler için bkz: toocreate şablonları [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8e035-254">Resource Manager ile daha önce Azure PowerShell kullanmadıysanız, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="8e035-255">Betik eylemi kullanarak kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e035-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="8e035-256">Şablon tooa konumu bilgisayarınızda aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8e035-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="8e035-257">Bu şablon Giraph hello kümedeki hello headnodes ve çalışan düğümlere yükler.</span><span class="sxs-lookup"><span data-stu-id="8e035-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="8e035-258">Merhaba JSON şablonunu geçerli olduğunu da doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="8e035-259">Şablonunuzu içerik içine yapıştırma [JSONLint](http://jsonlint.com/), bir çevrimiçi JSON doğrulama aracı.</span><span class="sxs-lookup"><span data-stu-id="8e035-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="8e035-260">Azure PowerShell'i başlatın ve Azure hesabı tooyour içinde oturum.</span><span class="sxs-lookup"><span data-stu-id="8e035-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="8e035-261">Kimlik bilgilerinizi girdikten sonra hello komut, hesabınız hakkında bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="8e035-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="8e035-262">Merhaba abonelik kimliği sağlayın, birden çok aboneliğiniz varsa dağıtım için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="8e035-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="8e035-263">Kullanabileceğiniz `Get-AzureRmSubscription` tooget hello abonelik kimliği her biri için içerir hesabınızla ilişkili tüm Aboneliklerin listesini.</span><span class="sxs-lookup"><span data-stu-id="8e035-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="8e035-264">Varolan bir kaynak grubu yoksa, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8e035-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="8e035-265">Merhaba kaynak grubunu ve çözümünüz için gereksinim duyduğunuz konumu Hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8e035-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="8e035-266">Merhaba yeni kaynak grubu özetini döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8e035-266">A summary of hello new resource group is returned.</span></span>

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

5. <span data-ttu-id="8e035-267">toocreate hello çalıştırmak kaynak grubunuz için bir dağıtım **New-AzureRmResourceGroupDeployment** komut ve hello gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="8e035-268">Merhaba parametreler veri aşağıdaki hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="8e035-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="8e035-269">Dağıtımınız için bir ad</span><span class="sxs-lookup"><span data-stu-id="8e035-269">A name for your deployment</span></span>
    * <span data-ttu-id="8e035-270">Kaynak grubunuzun Hello adı</span><span class="sxs-lookup"><span data-stu-id="8e035-270">hello name of your resource group</span></span>
    * <span data-ttu-id="8e035-271">Merhaba yolu veya URL'si toohello şablonu oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="8e035-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="8e035-272">Şablonunuzu herhangi bir parametre gerektiriyorsa, bu parametreler de geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e035-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="8e035-273">Bu durumda, hello betik eylemi tooinstall R hello kümedeki herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="8e035-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="8e035-274">İstendiğinde tooprovide hello şablonda tanımlanan hello parametreler için değerler.</span><span class="sxs-lookup"><span data-stu-id="8e035-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="8e035-275">Merhaba kaynak grubu dağıtıldığında hello dağıtımının bir özeti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8e035-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="8e035-276">Dağıtımınızı başarısız olursa, aşağıdaki cmdlet'leri tooget bilgilerle hello hataları hakkında hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="8e035-277">Azure PowerShell üzerinden küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="8e035-278">Bu bölümde, hello kullanırız [Ekle AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) betik eylemi toocustomize bir küme kullanarak cmdlet tooinvoke komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="8e035-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="8e035-279">Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8e035-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="8e035-280">Bir iş istasyonu toorun Hdınsight PowerShell cmdlet'leri yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e035-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="8e035-281">Merhaba aşağıdaki komut dosyası gösterilmektedir nasıl tooapply PowerShell kullanarak bir küme oluştururken bir betik eylemi:</span><span class="sxs-lookup"><span data-stu-id="8e035-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="8e035-282">Merhaba küme oluşturulmadan önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="8e035-283">Merhaba Hdınsight .NET SDK'sı öğesinden küme oluşturma sırasında bir betik eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="8e035-284">Merhaba Hdınsight .NET SDK'sı bir .NET uygulamasında Hdınsight ile daha kolay toowork kolaylaştırır istemci kitaplıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="8e035-285">Kod örneği için bkz: [.NET SDK kullanarak Hdınsight'ta oluşturma Linux tabanlı kümelerde hello](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="8e035-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="8e035-286">Küme çalışan betik eylemi tooa Uygula</span><span class="sxs-lookup"><span data-stu-id="8e035-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="8e035-287">Bu bölümde, nasıl tooapply betik çalıştıran küme eylemleri tooa öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8e035-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="8e035-288">Küme hello Azure portal ' çalışan betik eylemi tooa Uygula</span><span class="sxs-lookup"><span data-stu-id="8e035-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="8e035-289">Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="8e035-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="8e035-290">Merhaba Hdınsight küme genel bakış'tan, hello seçin **betik eylemleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="8e035-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="8e035-292">Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** hello ayarları bölümünün gelen.</span><span class="sxs-lookup"><span data-stu-id="8e035-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="8e035-293">Merhaba betik eylemleri bölümünde Hello üstten seçin **gönderme yeni**.</span><span class="sxs-lookup"><span data-stu-id="8e035-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Küme çalışan bir komut dosyası tooa Ekle](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="8e035-295">Kullanım hello __bir komut dosyası seçin__ girişi tooselect önceden yapılmış bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8e035-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="8e035-296">toouse özel bir komut dosyası seçin __özel__ ve hello sağlamak __adı__ ve __betik URI Bash__ betiği için.</span><span class="sxs-lookup"><span data-stu-id="8e035-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Merhaba select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="8e035-298">Aşağıdaki tablonun hello hello öğeleri hello formunda açıklar:</span><span class="sxs-lookup"><span data-stu-id="8e035-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="8e035-299">Özellik</span><span class="sxs-lookup"><span data-stu-id="8e035-299">Property</span></span> | <span data-ttu-id="8e035-300">Değer</span><span class="sxs-lookup"><span data-stu-id="8e035-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8e035-301">Bir komut dosyası seçin</span><span class="sxs-lookup"><span data-stu-id="8e035-301">Select a script</span></span> | <span data-ttu-id="8e035-302">toouse select kendi betiğinizi __özel__.</span><span class="sxs-lookup"><span data-stu-id="8e035-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="8e035-303">Aksi durumda, sağlanan komut dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="8e035-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="8e035-304">Ad</span><span class="sxs-lookup"><span data-stu-id="8e035-304">Name</span></span> |<span data-ttu-id="8e035-305">Merhaba betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="8e035-306">Bash betik URI</span><span class="sxs-lookup"><span data-stu-id="8e035-306">Bash script URI</span></span> |<span data-ttu-id="8e035-307">Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="8e035-308">HEAD/çalışan/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="8e035-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="8e035-309">Merhaba düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) hangi hello özelleştirme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e035-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="8e035-310">Parametreler</span><span class="sxs-lookup"><span data-stu-id="8e035-310">Parameters</span></span> |<span data-ttu-id="8e035-311">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e035-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="8e035-312">Kullanım hello __bu betik eylemini Sürdür__ girişi toomake emin hello betik ölçeklendirme işlemleri sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8e035-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="8e035-313">Son olarak, hello kullan **oluşturma** düğmesini tooapply hello betik toohello küme.</span><span class="sxs-lookup"><span data-stu-id="8e035-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="8e035-314">Küme Azure Powershell'den çalışan betik eylemi tooa Uygula</span><span class="sxs-lookup"><span data-stu-id="8e035-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="8e035-315">Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8e035-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="8e035-316">Bir iş istasyonu toorun Hdınsight PowerShell cmdlet'leri yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e035-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="8e035-317">Merhaba aşağıdaki örnekte gösterilmiştir nasıl tooapply bir betik eylemi tooa çalışan küme:</span><span class="sxs-lookup"><span data-stu-id="8e035-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="8e035-318">Merhaba işlemi tamamlandığında, metin aşağıdaki bilgileri benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="8e035-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="8e035-319">Küme hello Azure CLI ' çalışan betik eylemi tooa Uygula</span><span class="sxs-lookup"><span data-stu-id="8e035-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="8e035-320">Devam etmeden önce hello Azure CLI yükleyip yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8e035-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="8e035-321">Daha fazla bilgi için bkz: [yükleme hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="8e035-322">tooswitch tooAzure Resource Manager moduna komutu hello komut satırında aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="8e035-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="8e035-323">Tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="8e035-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="8e035-324">Küme çalışan bir komut dosyası eylemi tooa komutu tooapply aşağıdaki hello kullanın</span><span class="sxs-lookup"><span data-stu-id="8e035-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="8e035-325">Bu komutun parametresini atlarsanız, bunlar için istenir.</span><span class="sxs-lookup"><span data-stu-id="8e035-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="8e035-326">Varsa hello belirttiğiniz ile komut dosyası `-u` belirtebilirsiniz parametreleri kabul hello kullanarak bunları `-p` parametresi.</span><span class="sxs-lookup"><span data-stu-id="8e035-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="8e035-327">Geçerli düğüm türleri `headnode`, `workernode`, ve `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="8e035-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="8e035-328">Merhaba betik uygulanan toomultiple düğüm türleri gerekiyorsa, belirtin hello türleri tarafından ayrılmış bir ';'.</span><span class="sxs-lookup"><span data-stu-id="8e035-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="8e035-329">Örneğin, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="8e035-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="8e035-330">toopersist Merhaba komut dosyası, hello eklemek `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="8e035-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="8e035-331">Ayrıca hello betik daha sonra kullanarak kalıcı `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="8e035-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="8e035-332">Merhaba işi tamamlandığında, çıkış benzer toohello metin aşağıdaki alırsınız:</span><span class="sxs-lookup"><span data-stu-id="8e035-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="8e035-333">REST API kullanarak küme çalışan betik eylemi tooa Uygula</span><span class="sxs-lookup"><span data-stu-id="8e035-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="8e035-334">Bkz: [çalıştırmak betik eylemleri çalıştıran bir kümede](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e035-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="8e035-335">Küme hello Hdınsight .NET SDK ' çalışan betik eylemi tooa Uygula</span><span class="sxs-lookup"><span data-stu-id="8e035-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="8e035-336">Merhaba .NET SDK'sı tooapply betikleri tooa küme kullanarak bir örnek için bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="8e035-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="8e035-337">Betik eylemleri indirgemek geçmişini görüntülemek ve Yükselt</span><span class="sxs-lookup"><span data-stu-id="8e035-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="8e035-338">Hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="8e035-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="8e035-339">Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="8e035-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="8e035-340">Merhaba Hdınsight küme genel bakış'tan, hello seçin **betik eylemleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="8e035-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="8e035-342">Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** hello ayarları bölümünün gelen.</span><span class="sxs-lookup"><span data-stu-id="8e035-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="8e035-343">Bu küme için komut geçmişini hello betik eylemleri bölüm üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8e035-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="8e035-344">Bu bilgiler kalıcı komut listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="8e035-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="8e035-345">Merhaba ekran görüntüsünde, betiği bırakıldı Solr bu küme üzerinde çalışan bu hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="8e035-346">Merhaba ekran kalıcı herhangi bir komut dosyası göstermez.</span><span class="sxs-lookup"><span data-stu-id="8e035-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Betik eylemleri bölümünde](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="8e035-348">Bir komut dosyası hello geçmişinden seçerek bu komut dosyası için hello özellikleri bölümünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8e035-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="8e035-349">Merhaba ekranında Hello üstten hello betiği yeniden çalıştırın ya da bunu yükseltin.</span><span class="sxs-lookup"><span data-stu-id="8e035-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Betik eylemleri özellikleri](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="8e035-351">Merhaba de kullanabilirsiniz **... ** hello betik eylemleri bölümünde tooperform Eylemler girişlerde sağında toohello.</span><span class="sxs-lookup"><span data-stu-id="8e035-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Eylemler... komut dosyası kullanımı](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="8e035-353">Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="8e035-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="8e035-354">Merhaba aşağıdaki kullanın...</span><span class="sxs-lookup"><span data-stu-id="8e035-354">Use hello following...</span></span> | <span data-ttu-id="8e035-355">çok...</span><span class="sxs-lookup"><span data-stu-id="8e035-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="8e035-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="8e035-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="8e035-357">Kalıcı betik eylemleri hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="8e035-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="8e035-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="8e035-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="8e035-359">Komut dosyası uygulanan eylemler toohello küme ya da belirli bir komut dosyası ayrıntılarını geçmişini alma</span><span class="sxs-lookup"><span data-stu-id="8e035-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="8e035-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="8e035-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="8e035-361">Bir geçici yükseltir betik eylemi tooa kalıcı betik eylemi</span><span class="sxs-lookup"><span data-stu-id="8e035-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="8e035-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="8e035-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="8e035-363">Kalıcı betik eylemi tooan geçici eylem indirger</span><span class="sxs-lookup"><span data-stu-id="8e035-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="8e035-364">Kullanarak `Remove-AzureRmHDInsightPersistedScriptAction` hello eylemlerin bir komut dosyası tarafından geri almaz.</span><span class="sxs-lookup"><span data-stu-id="8e035-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="8e035-365">Bu cmdlet, yalnızca hello kalıcı bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8e035-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="8e035-366">Örnek komut dosyası izleyen hello hello cmdlet'leri toopromote kullanarak gösterir, ardından bir komut dosyası indirgemek.</span><span class="sxs-lookup"><span data-stu-id="8e035-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="8e035-367">Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="8e035-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="8e035-368">Merhaba aşağıdaki kullanın...</span><span class="sxs-lookup"><span data-stu-id="8e035-368">Use hello following...</span></span> | <span data-ttu-id="8e035-369">çok...</span><span class="sxs-lookup"><span data-stu-id="8e035-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="8e035-370">Kalıcı betik eylemlerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="8e035-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="8e035-371">Belirli kalıcı betik eylemi hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="8e035-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="8e035-372">Komut dosyası uygulanan eylemler toohello küme geçmişini alma</span><span class="sxs-lookup"><span data-stu-id="8e035-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="8e035-373">Bir özel betik eylemi hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="8e035-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="8e035-374">Bir geçici yükseltir betik eylemi tooa kalıcı betik eylemi</span><span class="sxs-lookup"><span data-stu-id="8e035-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="8e035-375">Kalıcı betik eylemi tooan geçici eylem indirger</span><span class="sxs-lookup"><span data-stu-id="8e035-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="8e035-376">Kullanarak `azure hdinsight script-action persisted delete` hello eylemlerin bir komut dosyası tarafından geri almaz.</span><span class="sxs-lookup"><span data-stu-id="8e035-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="8e035-377">Bu cmdlet, yalnızca hello kalıcı bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8e035-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="8e035-378">Merhaba Hdınsight .NET SDK'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="8e035-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="8e035-379">Merhaba .NET SDK'sı tooretrieve betik geçmişi bir kümeden kullanma örneği için yükseltmek veya betikleri indirgemek, bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="8e035-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="8e035-380">Bu örnek ayrıca .NET SDK kullanarak bir Hdınsight uygulaması tooinstall hello nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8e035-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="8e035-381">Hdınsight kümelerinde kullanılan açık kaynaklı yazılım desteği</span><span class="sxs-lookup"><span data-stu-id="8e035-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="8e035-382">Merhaba Microsoft Azure Hdınsight hizmeti, açık kaynaklı teknolojileri Hadoop biçimlendirilmiş bir ekosistemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="8e035-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="8e035-383">Microsoft Azure, açık kaynaklı teknolojileri için genel düzeyde desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="8e035-384">Merhaba daha fazla bilgi için bkz: **destek kapsamı** hello bölümünü [Azure destek SSS Web sitesine](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="8e035-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="8e035-385">Merhaba Hdınsight hizmeti yerleşik bileşenleri için destek, ek bir düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="8e035-386">Merhaba Hdınsight hizmeti açık kaynak bileşenlerini iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="8e035-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="8e035-387">**Yerleşik bileşenlerini** -bu bileşenler Hdınsight kümelerinde önceden yüklenmiş ve hello küme çekirdek işlevselliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="8e035-388">Örneğin, YARN ResourceManager, hello Hive sorgu dili (HiveQL) ve hello Mahout kitaplık toothis kategori ait.</span><span class="sxs-lookup"><span data-stu-id="8e035-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="8e035-389">Küme bileşenlerin tam bir listesi kullanılabilir [hello Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="8e035-390">**Özel bileşenler** -, hello küme, bir kullanıcı olarak yükleyebilir veya herhangi bir bileşeni hello topluluk bulunan ya da sizin tarafınızdan oluşturulan, iş yükü kullanın.</span><span class="sxs-lookup"><span data-stu-id="8e035-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="8e035-391">Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="8e035-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="8e035-392">Microsoft Support tooisolate yardımcı olur ve sorunları ilgili toothese bileşenler çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="8e035-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="8e035-393">Özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="8e035-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="8e035-394">Bunlar tooengage kullanılabilir kanalları hello açık kaynak teknolojileri için bu teknoloji derin uzmanlık bulunduğu isteyebilir veya Microsoft desteği mümkün tooresolve hello sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="8e035-395">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="8e035-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="8e035-396">Merhaba Hdınsight hizmeti toouse özel bileşenleri çeşitli yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="8e035-397">Merhaba, nasıl bir bileşen kullanılan veya hello kümeye yüklü bakılmaksızın aynı düzeyde desteği uygular.</span><span class="sxs-lookup"><span data-stu-id="8e035-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="8e035-398">Merhaba aşağıdaki listede açıklanmaktadır hello en yaygın şekilde özel bileşenlerin kullanılabilir Hdınsight kümelerinde:</span><span class="sxs-lookup"><span data-stu-id="8e035-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="8e035-399">İş gönderme - Hadoop veya diğer tür execute veya özel bileşenleri kullanan işi gönderilen toohello kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="8e035-400">Küme özelleştirme - küme oluşturma sırasında ek ayarlar ve hello küme düğümlerinde yüklü özel bileşenleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="8e035-401">Örnekler - popüler özel bileşenleri, Microsoft ve diğerleri için bu bileşenlerin hello Hdınsight kümelerinde nasıl kullanılabileceğini örnek sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="8e035-402">Bu örnekler desteği olmadan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8e035-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8e035-403">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="8e035-403">Troubleshooting</span></span>

<span data-ttu-id="8e035-404">Betik eylemleri tarafından günlüğe kaydedilen Ambari web kullanıcı Arabirimi tooview bilgi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="8e035-405">Küme oluşturma sırasında Hello komut başarısız olursa, hello günlükleri hello kümesi ile ilişkili hello varsayılan depolama hesabı mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="8e035-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="8e035-406">Bu bölümde, nasıl tooretrieve hello hem bu seçenekleri kullanarak oturum açtığında bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e035-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="8e035-407">Merhaba Ambari Web kullanıcı arabirimini kullanarak</span><span class="sxs-lookup"><span data-stu-id="8e035-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="8e035-408">Tarayıcınızda, toohttps://CLUSTERNAME.azurehdinsight.net gidin.</span><span class="sxs-lookup"><span data-stu-id="8e035-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="8e035-409">CLUSTERNAME hello Hdınsight kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8e035-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="8e035-410">İstendiğinde, hello küme için hello yönetici hesabı adını (Yönetici) ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="8e035-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="8e035-411">Bir web formunda tooreenter hello yönetici kimlik bilgilerine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="8e035-412">Merhaba hello sayfanın üst kısmındaki hello Hello çubuğundan seçin **ops** girişi.</span><span class="sxs-lookup"><span data-stu-id="8e035-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="8e035-413">Ambari aracılığıyla hello kümede gerçekleştirilen geçerli ve önceki işlemleri listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8e035-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Seçili ops ile Ambari web kullanıcı Arabirimi çubuğu](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="8e035-415">Bul hello girişlerine sahip **çalıştırmak\_customscriptaction** hello içinde **Operations** sütun.</span><span class="sxs-lookup"><span data-stu-id="8e035-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="8e035-416">Merhaba betik eylemleri çalıştırdığınızda bu girişleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8e035-416">These entries are created when hello Script Actions run.</span></span>

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="8e035-418">tooview hello STDOUT ve STDERR çıktısı hello run\customscriptaction girişi seçin ve hello bağlantılar aracılığıyla detaya.</span><span class="sxs-lookup"><span data-stu-id="8e035-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="8e035-419">Merhaba komut dosyası çalıştığında, bu çıkışı oluşturulur ve yararlı bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="8e035-420">Merhaba varsayılan depolama hesabı erişim günlükleri</span><span class="sxs-lookup"><span data-stu-id="8e035-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="8e035-421">Merhaba küme oluşturma tooa betik eylemi hatası başarısız olursa, hello günlükleri hello küme depolama hesabından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="8e035-422">Merhaba depolama günlüklerine kullanılabilir `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="8e035-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="8e035-424">Bu dizin altında headnode, workernode ve zookeeper düğümleri hello günlükleri ayrı olarak düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="8e035-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="8e035-425">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8e035-425">Some examples are:</span></span>

    * <span data-ttu-id="8e035-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="8e035-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="8e035-427">**Çalışan düğümü** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="8e035-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="8e035-428">**Zookeeper düğümü** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="8e035-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="8e035-429">Tüm stdout ve stderr hello karşılık gelen konağının toohello depolama hesabı karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8e035-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="8e035-430">Bir **çıkış -\*.txt** ve **hataları -\*.txt** her komut dosyası eylemi için.</span><span class="sxs-lookup"><span data-stu-id="8e035-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="8e035-431">Merhaba çıkış *.txt dosya hello konakta çalışan hello betik hello URI hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="8e035-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="8e035-432">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8e035-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="8e035-433">Betik eylemi küme sürekli ile Merhaba oluşturmak mümkündür aynı adı.</span><span class="sxs-lookup"><span data-stu-id="8e035-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="8e035-434">Böyle bir durumda hello tarih klasör adını temel alarak hello ilgili günlükleri ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="8e035-435">Örneğin, farklı tarihlerde oluşturulan bir küme (contoso.com) hello klasör yapısını günlük girişlerini aşağıdaki benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="8e035-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="8e035-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="8e035-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="8e035-437">Merhaba ile bir betik eylemi kümesi oluşturursanız, aynı hello üzerinde aynı adı günü, başlangıç benzersiz önek tooidentify hello ilgili günlük dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="8e035-438">Bir küme 12: 00'da (gece yarısı) yakın oluşturursanız, hello günlük dosyaları iki gün boyunca span mümkündür.</span><span class="sxs-lookup"><span data-stu-id="8e035-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="8e035-439">Böyle durumlarda, gördüğünüz Merhaba için iki farklı tarih klasörleri aynı küme.</span><span class="sxs-lookup"><span data-stu-id="8e035-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="8e035-440">Karşıya yükleme günlük dosyalarını toohello varsayılan kapsayıcı yukarı özellikle büyük kümeleri için too5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8e035-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="8e035-441">Tooaccess hello günlükleri istiyorsanız, bir komut dosyası eylemi başarısız olursa bu nedenle, hemen hello küme silmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="8e035-442">Ambari izleme</span><span class="sxs-lookup"><span data-stu-id="8e035-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="8e035-443">Linux tabanlı Hdınsight kümenizdeki hello Ambari izleme (hdinsightwatchdog) Hello parolasını değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="8e035-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8e035-444">Bu hesap için başlangıç parolası değiştiriliyor hello özelliği toorun yeni betik eylemleri hello Hdınsight kümesinde keser.</span><span class="sxs-lookup"><span data-stu-id="8e035-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="8e035-445">Ad BlobService içeri aktarılamıyor</span><span class="sxs-lookup"><span data-stu-id="8e035-445">Can't import name BlobService</span></span>

<span data-ttu-id="8e035-446">__Belirtiler__: Merhaba betik eylemi başarısız.</span><span class="sxs-lookup"><span data-stu-id="8e035-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="8e035-447">Ambari içinde hello işlemi görüntülediğinizde metin benzer toohello aşağıdaki hata görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="8e035-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="8e035-448">__Neden__: Merhaba Hdınsight kümesi ile birlikte hello Python Azure Storage istemcisi yükseltirseniz, bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="8e035-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="8e035-449">Hdınsight Azure Storage istemci 0.20.0 bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8e035-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="8e035-450">__Çözümleme__: tooresolve bu hatayı tooeach küme düğümünü kullanarak el ile bağlanmanız `ssh` ve kullanım hello aşağıdaki komut tooreinstall hello doğru depolama istemci sürümü:</span><span class="sxs-lookup"><span data-stu-id="8e035-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="8e035-451">SSH ile bağlantı toohello kümesi hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8e035-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="8e035-452">Küme oluşturma sırasında kullanılan komut geçmişi göstermiyor</span><span class="sxs-lookup"><span data-stu-id="8e035-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="8e035-453">Kümenizi 15 Mart 2016'dan önce oluşturulduysa, bir giriş betik eylemi geçmişinde göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e035-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="8e035-454">15 Mart 2016'dan sonra hello küme yeniden boyutlandırma uygulandıkları gibi küme oluşturma sırasında kullanarak hello komut geçmişinde hello bir parçası olarak hello kümedeki toonew düğümler yeniden boyutlandırma işlemi görünür.</span><span class="sxs-lookup"><span data-stu-id="8e035-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="8e035-455">İki istisna mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="8e035-455">There are two exceptions:</span></span>

* <span data-ttu-id="8e035-456">Kümenizi 1 Eylül 2015 önce oluşturulduysa.</span><span class="sxs-lookup"><span data-stu-id="8e035-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="8e035-457">Betik eylemleri kullanıma sunulan, bu tarih olur.</span><span class="sxs-lookup"><span data-stu-id="8e035-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="8e035-458">Bu tarihten önce oluşturulan herhangi bir küme betik eylemleri küme oluşturma için kullanılmamış.</span><span class="sxs-lookup"><span data-stu-id="8e035-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="8e035-459">Küme oluşturma sırasında birden çok betik eylemleri kullandıysanız ve aynı birden fazla komut dosyası için bir ad verin veya hello hello kullanılan aynı adı, birden fazla komut dosyası için farklı parametreler ancak aynı URI.</span><span class="sxs-lookup"><span data-stu-id="8e035-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="8e035-460">Bu durumlarda, aşağıdaki hata hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="8e035-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="8e035-461">Varolan komut dosyalarında tooconflicting betik adları nedeniyle bu kümede eylemler olabilir yeni betik verdi.</span><span class="sxs-lookup"><span data-stu-id="8e035-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="8e035-462">Kümesine sağlanan betik adları oluşturmak gereken tüm benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e035-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="8e035-463">Varolan komut dosyalarını yeniden boyutlandırma üzerinde verdi.</span><span class="sxs-lookup"><span data-stu-id="8e035-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e035-464">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8e035-464">Next steps</span></span>

* [<span data-ttu-id="8e035-465">Hdınsight için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="8e035-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="8e035-466">Yükleme ve Hdınsight kümelerinde Solr kullanma</span><span class="sxs-lookup"><span data-stu-id="8e035-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="8e035-467">Yükleme ve Hdınsight kümelerinde Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="8e035-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="8e035-468">Ek depolama alanı tooan Hdınsight kümesi Ekle</span><span class="sxs-lookup"><span data-stu-id="8e035-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Küme oluşturma sırasında aşamaları"
