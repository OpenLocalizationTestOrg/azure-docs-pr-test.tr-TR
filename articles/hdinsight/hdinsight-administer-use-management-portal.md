---
title: "Azure portal kullanarak Hdınsight'ta aaaManage Windows tabanlı Hadoop kümeleri hello | Microsoft Docs"
description: "Bilgi nasıl tooadminister Hdınsight hizmeti. Bir Hdınsight kümesi, açık hello etkileşimli JavaScript konsolu ve açık hello Hadoop komut konsolundan oluşturun."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a><span data-ttu-id="5169e-104">Windows tabanlı Hadoop kümeleri hdınsight'ta hello Azure portal kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="5169e-104">Manage Windows-based Hadoop clusters in HDInsight by using hello Azure portal</span></span>

<span data-ttu-id="5169e-105">Hello kullanarak [Azure portal][azure-portal], Azure Hdınsight'ta Windows tabanlı Hadoop kümeleri oluşturma, Hadoop kullanıcı parolası değiştirme ve etkinleştirme Uzak Masaüstü Protokolü (RDP), erişebilmesi için Hadoop hello Merhaba küme konsolda komutu.</span><span class="sxs-lookup"><span data-stu-id="5169e-105">Using hello [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access hello Hadoop command console on hello cluster.</span></span>

<span data-ttu-id="5169e-106">Bu makaledeki Hello bilgiler yalnızca tooWindow tabanlı Hdınsight kümeleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5169e-106">hello information in this article only applies tooWindow-based HDInsight clusters.</span></span> <span data-ttu-id="5169e-107">Linux tabanlı kümelerde yönetme hakkında daha fazla bilgi için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-portal-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5169e-108">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="5169e-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5169e-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5169e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5169e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5169e-110">Prerequisites</span></span>

<span data-ttu-id="5169e-111">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5169e-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="5169e-112">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="5169e-112">**An Azure subscription**.</span></span> <span data-ttu-id="5169e-113">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5169e-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5169e-114">**Azure depolama hesabı** -bir Hdınsight kümesi bir Azure Blob Depolama kapsayıcısını hello varsayılan dosya sistemi olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="5169e-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as hello default file system.</span></span> <span data-ttu-id="5169e-115">Azure Blob storage Hdınsight kümeleri ile sorunsuz bir deneyim nasıl sağladığını hakkında daha fazla bilgi için bkz: [kullanım Azure Blob Storage Hdınsight ile](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="5169e-116">Bir Azure Storage hesabı oluşturma hakkında daha fazla bilgi için bkz: [nasıl tooCreate bir depolama hesabı](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-116">For details on creating an Azure Storage account, see [How tooCreate a Storage Account](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="open-hello-portal"></a><span data-ttu-id="5169e-117">Merhaba Portal açın</span><span class="sxs-lookup"><span data-stu-id="5169e-117">Open hello Portal</span></span>
1. <span data-ttu-id="5169e-118">Çok oturum[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5169e-118">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5169e-119">Merhaba portal açtıktan sonra şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5169e-119">After you open hello portal, you can:</span></span>

   * <span data-ttu-id="5169e-120">Tıklatın **yeni** hello soldaki menüden toocreate yeni bir küme gelen:</span><span class="sxs-lookup"><span data-stu-id="5169e-120">Click **New** from hello left menu toocreate a new cluster:</span></span>

       ![Yeni Hdınsight küme düğmesi](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * <span data-ttu-id="5169e-122">Tıklatın **Hdınsight kümeleri** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="5169e-122">Click **HDInsight Clusters** from hello left menu.</span></span>

       ![Azure portal Hdınsight küme düğmesi](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     <span data-ttu-id="5169e-124">Varsa **Hdınsight** hello soldaki menüde görünür değil'ye tıklayın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="5169e-124">If **HDInsight** doesn't appear in hello left menu, click **Browse**.</span></span>

     ![Azure portal gözatma küme düğmesi](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a><span data-ttu-id="5169e-126">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="5169e-126">Create clusters</span></span>
<span data-ttu-id="5169e-127">Merhaba Portal kullanarak hello oluşturma yönergeleri için bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-127">For hello creation instructions using hello Portal, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="5169e-128">Hdınsight geniş Hadoop bileşenleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="5169e-128">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="5169e-129">Doğrulandı ve desteklenen hello bileşenler Hello listesi için bkz [hangi sürümüdür Azure Hdınsight'ta hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-129">For hello list of hello components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="5169e-130">Seçenekler aşağıdaki hello birini kullanarak Hdınsight özelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5169e-130">You can customize HDInsight by using one of hello following options:</span></span>

* <span data-ttu-id="5169e-131">Bir küme tooeither özelleştirebileceğiniz betik eylemi toorun özel komut dosyası kullanma küme yapılandırmasını değiştirmek veya Giraph veya Solr gibi özel bileşenlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-131">Use Script Action toorun custom scripts that can customize a cluster tooeither change cluster configuration or install custom components such as Giraph or Solr.</span></span> <span data-ttu-id="5169e-132">Daha fazla bilgi için bkz: [betik eylemi kullanarak özelleştirme Hdınsight kümesi](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span>
* <span data-ttu-id="5169e-133">Küme oluşturma sırasında Hello küme özelleştirme parametreleri hello Hdınsight .NET SDK veya Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="5169e-133">Use hello cluster customization parameters in hello HDInsight .NET SDK or Azure PowerShell during cluster creation.</span></span> <span data-ttu-id="5169e-134">Bu yapılandırma değişikliklerini hello küme hello ömrü sonra korunur ve Azure platformu düzenli olarak bakımını gerçekleştirir küme düğümü reimages etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="5169e-134">These configuration changes are then preserved through hello lifetime of hello cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span></span> <span data-ttu-id="5169e-135">Hello küme özelleştirme parametreleri kullanma hakkında daha fazla bilgi için bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-135">For more information on using hello cluster customization parameters, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="5169e-136">Mahout ve basamaklama, gibi yerel bazı Java bileşenleri hello kümede JAR dosyaları olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-136">Some native Java components, like Mahout and Cascading, can be run on hello cluster as JAR files.</span></span> <span data-ttu-id="5169e-137">Bu JAR dosyalarını dağıtılmış tooAzure Blob Depolama olabilir ve tooHDInsight kümeleri Hadoop iş gönderme mekanizmalar aracılığıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-137">These JAR files can be distributed tooAzure Blob storage, and submitted tooHDInsight clusters through Hadoop job submission mechanisms.</span></span> <span data-ttu-id="5169e-138">Daha fazla bilgi için bkz: [gönderme Hadoop işleri program aracılığıyla](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

  > [!NOTE]
  > <span data-ttu-id="5169e-139">Hdınsight kümelerinde JAR dosyalarını çağırma başvurun veya JAR dosyalarını tooHDInsight kümelerini dağıtma sorunları varsa [Microsoft Support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="5169e-139">If you have issues deploying JAR files tooHDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
  >
  > <span data-ttu-id="5169e-140">Geçişli Hdınsight tarafından desteklenmiyor ve Microsoft Support uygun değil.</span><span class="sxs-lookup"><span data-stu-id="5169e-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="5169e-141">Desteklenen bileşenlerin bir listesi için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-141">For lists of supported components, see [What's new in hello cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
  >
  >

<span data-ttu-id="5169e-142">Uzak Masaüstü bağlantısı kullanarak hello kümede özel yazılım yüklemesi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5169e-142">Installation of custom software on hello cluster by using Remote Desktop Connection is not supported.</span></span> <span data-ttu-id="5169e-143">Toore ihtiyacınız varsa bunlar kaybolur gibi hello sürücülerinde hello baş düğümü, herhangi bir dosya depolama kaçınmalısınız-hello kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="5169e-143">You should avoid storing any files on hello drives of hello head node, as they will be lost if you need toore-create hello clusters.</span></span> <span data-ttu-id="5169e-144">Azure Blob Depolama dosyalarda depolamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5169e-144">We recommend storing files on Azure Blob storage.</span></span> <span data-ttu-id="5169e-145">BLOB Depolama kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5169e-145">Blob storage is persistent.</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="5169e-146">Liste ve kümeleri Göster</span><span class="sxs-lookup"><span data-stu-id="5169e-146">List and show clusters</span></span>
1. <span data-ttu-id="5169e-147">Çok oturum[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5169e-147">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5169e-148">Tıklatın **Hdınsight kümeleri** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="5169e-148">Click **HDInsight Clusters** from hello left menu.</span></span>
3. <span data-ttu-id="5169e-149">Merhaba küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-149">Click hello cluster name.</span></span> <span data-ttu-id="5169e-150">Merhaba küme listesi uzunsa hello sayfa hello üstündeki filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-150">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="5169e-151">Merhaba listesi tooshow hello ayrıntılarını kümeden çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-151">Double-click a cluster from hello list tooshow hello details.</span></span>

    <span data-ttu-id="5169e-152">**Menü ve essentials**:</span><span class="sxs-lookup"><span data-stu-id="5169e-152">**Menu and essentials**:</span></span>

    ![Azure portal Hdınsight küme temelleri](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * <span data-ttu-id="5169e-154">toocustomize hello menüsünde, başlangıç menüsünde herhangi bir yere sağ tıklayın ve ardından **Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="5169e-154">toocustomize hello menu, right-click anywhere on hello menu, and then click **Customize**.</span></span>
   * <span data-ttu-id="5169e-155">**Ayarları** ve **tüm ayarları**: görüntüler hello **ayarları** tooaccess sağlayan hello küme dikey penceresinde hello küme için yapılandırma bilgilerini ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="5169e-155">**Settings** and **All Settings**: Displays hello **Settings** blade for hello cluster, which allows you tooaccess detailed configuration information for hello cluster.</span></span>
   * <span data-ttu-id="5169e-156">**Pano**, **küme Panosu** ve **URL: Linux tabanlı kümeler için Ambari Web olan tüm yolları tooaccess hello küme Panosu, bunlar. -**Güvenli Kabuk **: Hello yönergeleri tooconnect toohello küme güvenli Kabuk (SSH) bağlantısı kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="5169e-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways tooaccess hello cluster dashboard, which is Ambari Web for Linux-based clusters. -**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="5169e-157">**Küme ölçeklendirme**: Bu küme için toochange hello çalışan düğümü sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5169e-157">**Scale Cluster**: Allows you toochange hello number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="5169e-158">**Silme**: hello küme siler.</span><span class="sxs-lookup"><span data-stu-id="5169e-158">**Delete**: Deletes hello cluster.</span></span>
   * <span data-ttu-id="5169e-159">**Hızlı Başlangıç**: yardımcı olacak bilgileri görüntüler, Hdınsight kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-159">**Quickstart**: Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="5169e-160">** Kullanıcıları: tooset izinlerini verir *portal Yönetim* diğer kullanıcılar için bu kümenin, Azure aboneliğinizin üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5169e-160">**Users: Allows you tooset permissions for *portal management* of this cluster for other users on your Azure subscription.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="5169e-161">Bu *yalnızca* hello Azure portalına erişim ve izinleri toothis kümede etkiler ve tooor gönderme işleri toohello Hdınsight kümesi bağlanan üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="5169e-161">This *only* affects access and permissions toothis cluster in hello Azure portal, and has no effect on who can connect tooor submit jobs toohello HDInsight cluster.</span></span>
     >
     >
   * <span data-ttu-id="5169e-162">**Etiketler**: etiketleri bulut hizmetlerinizi, özel bir sınıflandırma, tooset anahtar/değer çiftleri toodefine izin.</span><span class="sxs-lookup"><span data-stu-id="5169e-162">**Tags**: Tags allow you tooset key/value pairs toodefine a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="5169e-163">Örneğin, adlı bir anahtar oluşturabilir **proje**ve ardından belirli bir projeyle ilişkili tüm hizmetler için ortak bir değer kullanın.</span><span class="sxs-lookup"><span data-stu-id="5169e-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="5169e-164">**Ambari görünümleri**: tooAmbari Web bağlar.</span><span class="sxs-lookup"><span data-stu-id="5169e-164">**Ambari Views**: Links tooAmbari Web.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="5169e-165">toomanage hello Hizmetleri Hdınsight kümesi hello tarafından sağlanan, Ambari REST API hello veya Ambari Web kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5169e-165">toomanage hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="5169e-166">Ambari kullanarak daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
     >
     >

     <span data-ttu-id="5169e-167">**Kullanım**:</span><span class="sxs-lookup"><span data-stu-id="5169e-167">**Usage**:</span></span>

     ![Azure portal Hdınsight küme kullanımı](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. <span data-ttu-id="5169e-169">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5169e-169">Click **Settings**.</span></span>

    ![Azure portal Hdınsight küme kullanımı](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * <span data-ttu-id="5169e-171">**Özellikleri**: hello küme özelliklerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-171">**Properties**: View hello cluster properties.</span></span>
   * <span data-ttu-id="5169e-172">**Küme AAD kimlik**:</span><span class="sxs-lookup"><span data-stu-id="5169e-172">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="5169e-173">**Azure depolama anahtarları**: hello varsayılan depolama hesabı ve anahtarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-173">**Azure Storage Keys**: View hello default storage account and its key.</span></span> <span data-ttu-id="5169e-174">Merhaba depolama hesabı hello küme oluşturma işlemi sırasında bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5169e-174">hello storage account is configuration during hello cluster creation process.</span></span>
   * <span data-ttu-id="5169e-175">**Oturum açma küme**: hello küme HTTP kullanıcı adınızı ve parolanızı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5169e-175">**Cluster Login**: Change hello cluster HTTP user name and password.</span></span>
   * <span data-ttu-id="5169e-176">**Dış meta deponuz**: hello Hive ve Oozie meta deponuz görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-176">**External Metastores**: View hello Hive and Oozie metastores.</span></span> <span data-ttu-id="5169e-177">Merhaba meta deponuz yalnızca hello küme oluşturma işlemi sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-177">hello metastores can only be configured during hello cluster creation process.</span></span>
   * <span data-ttu-id="5169e-178">**Küme ölçeklendirme**: artırma ve azaltma hello küme çalışan düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="5169e-178">**Scale Cluster**: Increase and decrease hello number of cluster worker nodes.</span></span>
   * <span data-ttu-id="5169e-179">**Uzak Masaüstü**: etkinleştirmek ve Uzak Masaüstü (RDP) erişimi devre dışı bırakın ve hello RDP kullanıcı adı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5169e-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure hello RDP username.</span></span>  <span data-ttu-id="5169e-180">Merhaba RDP kullanıcı adı hello HTTP kullanıcı adından farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5169e-180">hello RDP user name must be different from hello HTTP user name.</span></span>
   * <span data-ttu-id="5169e-181">**Kayıtlı iş ortağı**:</span><span class="sxs-lookup"><span data-stu-id="5169e-181">**Partner of Record**:</span></span>

     > [!NOTE]
     > <span data-ttu-id="5169e-182">Bu, kullanılabilir ayarlar genel bir listesi verilmiştir; tümünü değil, tüm küme türleri için mevcut olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5169e-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span></span>
     >
     >
6. <span data-ttu-id="5169e-183">Tıklatın **özellikleri**:</span><span class="sxs-lookup"><span data-stu-id="5169e-183">Click **Properties**:</span></span>

    <span data-ttu-id="5169e-184">Merhaba özellikler bölümü hello aşağıdakiler yer alır:</span><span class="sxs-lookup"><span data-stu-id="5169e-184">hello properties section lists hello following:</span></span>

   * <span data-ttu-id="5169e-185">**Ana bilgisayar adı**: küme adı.</span><span class="sxs-lookup"><span data-stu-id="5169e-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="5169e-186">**Küme URL**.</span><span class="sxs-lookup"><span data-stu-id="5169e-186">**Cluster URL**.</span></span>
   * <span data-ttu-id="5169e-187">**Durum**: dahil, kabul iptal ClusterStorageProvisioned, AzureVMConfiguration, çalıştığından, silme, hatası, HDInsightConfiguration, işletimsel, silinen, süresi sona erdi, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="5169e-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="5169e-188">**Bölge**: Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="5169e-188">**Region**: Azure location.</span></span> <span data-ttu-id="5169e-189">Merhaba desteklenen Azure konumu listesi için bkz **bölge** açılan liste kutusunu [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5169e-189">For a list of supported Azure locations, see hello **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="5169e-190">**Oluşturulan veri**.</span><span class="sxs-lookup"><span data-stu-id="5169e-190">**Data created**.</span></span>
   * <span data-ttu-id="5169e-191">**İşletim sistemi**: ya da **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="5169e-191">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="5169e-192">**Tür**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="5169e-192">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="5169e-193">**Sürüm**.</span><span class="sxs-lookup"><span data-stu-id="5169e-193">**Version**.</span></span> <span data-ttu-id="5169e-194">Bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="5169e-194">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="5169e-195">**Abonelik**: Abonelik adı.</span><span class="sxs-lookup"><span data-stu-id="5169e-195">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="5169e-196">**Abonelik kimliği**.</span><span class="sxs-lookup"><span data-stu-id="5169e-196">**Subscription ID**.</span></span>
   * <span data-ttu-id="5169e-197">**Birincil veri kaynağını**.</span><span class="sxs-lookup"><span data-stu-id="5169e-197">**Primary data source**.</span></span> <span data-ttu-id="5169e-198">Hello Azure Blob Depolama hesabı Hadoop dosya sistemi hello varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5169e-198">hello Azure Blob storage account used as hello default Hadoop file system.</span></span>
   * <span data-ttu-id="5169e-199">**Çalışan düğüm fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="5169e-199">**Worker nodes pricing tier**.</span></span>
   * <span data-ttu-id="5169e-200">**Baş düğüm fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="5169e-200">**Head node pricing tier**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="5169e-201">Küme silme</span><span class="sxs-lookup"><span data-stu-id="5169e-201">Delete clusters</span></span>
<span data-ttu-id="5169e-202">Bir küme silme hello varsayılan depolama hesabı ya da bağlı tüm depolama hesaplarını silmez.</span><span class="sxs-lookup"><span data-stu-id="5169e-202">Delete a cluster will not delete hello default storage account or any linked storage accounts.</span></span> <span data-ttu-id="5169e-203">Merhaba küme kullanarak yeniden oluşturabileceğiniz hello aynı depolama hesapları ve hello aynı meta depolar.</span><span class="sxs-lookup"><span data-stu-id="5169e-203">You can re-create hello cluster by using hello same storage accounts and hello same metastores.</span></span>

1. <span data-ttu-id="5169e-204">İçinde toohello oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5169e-204">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="5169e-205">Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-205">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="5169e-206">Tıklatın **silmek** hello üst menüsünden ve hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-206">Click **Delete** from hello top menu, and then follow hello instructions.</span></span>

<span data-ttu-id="5169e-207">Ayrıca bkz. [Duraklat/kümeleri kapatma](#pauseshut-down-clusters).</span><span class="sxs-lookup"><span data-stu-id="5169e-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="5169e-208">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5169e-208">Scale clusters</span></span>
<span data-ttu-id="5169e-209">özellik ölçeklendirme hello küme toochange hello Azure Hdınsight'ta toore gerek kalmadan çalışan bir küme tarafından kullanılan çalışan düğüm sayısı sağlar-hello kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5169e-209">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5169e-210">Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="5169e-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="5169e-211">Kümenizin hello sürümü değilseniz hello özellikler sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-211">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="5169e-212">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="5169e-212">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="5169e-213">hello etkisini, her tür Hdınsight tarafından desteklenen küme için veri düğümünün hello numarasını değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="5169e-213">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="5169e-214">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5169e-214">Hadoop</span></span>

    <span data-ttu-id="5169e-215">Sorunsuz bir şekilde hello tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-215">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="5169e-216">Merhaba işlemi devam ederken yeni işleri da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-216">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="5169e-217">Böylece Hello küme her zaman işlevsel bir durumda bırakılır bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="5169e-217">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="5169e-218">Bir Hadoop kümesine veri düğümlerini hello sayısını azaltarak ölçeklendirilir, bazı hello kümedeki hello hizmetleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="5169e-218">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="5169e-219">Bu, tüm çalışan ve işleri toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olur.</span><span class="sxs-lookup"><span data-stu-id="5169e-219">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="5169e-220">Hello işlemi tamamlandıktan sonra ancak, hello sunmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-220">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="5169e-221">HBase</span><span class="sxs-lookup"><span data-stu-id="5169e-221">HBase</span></span>

    <span data-ttu-id="5169e-222">Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5169e-222">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="5169e-223">Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli.</span><span class="sxs-lookup"><span data-stu-id="5169e-223">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="5169e-224">Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello hello headnode açarak el ile de hello bölgesel sunucular dengeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5169e-224">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="5169e-225">Merhaba HBase Kabuğu'nu kullanarak daha fazla bilgi için bkz:]</span><span class="sxs-lookup"><span data-stu-id="5169e-225">For more information on using hello HBase shell, see []</span></span>
* <span data-ttu-id="5169e-226">Storm</span><span class="sxs-lookup"><span data-stu-id="5169e-226">Storm</span></span>

    <span data-ttu-id="5169e-227">Sorunsuz bir şekilde ekleyebilir veya çalışırken veri düğümleri tooyour Storm kümesi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-227">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="5169e-228">Ancak hello ölçekleme işlemi başarıyla tamamlandıktan sonra toorebalance hello topoloji gerekir.</span><span class="sxs-lookup"><span data-stu-id="5169e-228">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="5169e-229">İki yolla yeniden dengelenmesi gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="5169e-229">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="5169e-230">Storm web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="5169e-230">Storm web UI</span></span>
  * <span data-ttu-id="5169e-231">Komut satırı arabirimi (CLI) aracı</span><span class="sxs-lookup"><span data-stu-id="5169e-231">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="5169e-232">Lütfen toohello bakın [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="5169e-232">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="5169e-233">Merhaba Storm web kullanıcı Arabirimi hello Hdınsight kümesinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="5169e-233">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![Hdınsight storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="5169e-235">Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:</span><span class="sxs-lookup"><span data-stu-id="5169e-235">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="5169e-236">**tooscale kümeleri**</span><span class="sxs-lookup"><span data-stu-id="5169e-236">**tooscale clusters**</span></span>

1. <span data-ttu-id="5169e-237">İçinde toohello oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5169e-237">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="5169e-238">Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-238">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="5169e-239">Tıklatın **ayarları** hello üst menüsünden ve ardından **ölçekte küme**.</span><span class="sxs-lookup"><span data-stu-id="5169e-239">Click **Settings** from hello top menu, and then click **Scale Cluster**.</span></span>
4. <span data-ttu-id="5169e-240">Girin **sayı, alt düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="5169e-240">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="5169e-241">Merhaba küme düğümü hello sayısı Azure abonelikleri arasında değişiklik gösterir.</span><span class="sxs-lookup"><span data-stu-id="5169e-241">hello limit on hello number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="5169e-242">Faturalama desteği tooincrease hello sınırı başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-242">You can contact billing support tooincrease hello limit.</span></span>  <span data-ttu-id="5169e-243">Merhaba maliyet bilgileri toohello düğüm sayısını yapmış olduğunuz hello değişiklikleri yansıtır.</span><span class="sxs-lookup"><span data-stu-id="5169e-243">hello cost information will reflect hello changes you have made toohello number of nodes.</span></span>

    ![Hdınsight Hadoop HBase Storm Spark ölçek](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="5169e-245">Kümeleri Duraklat/kapatma</span><span class="sxs-lookup"><span data-stu-id="5169e-245">Pause/shut down clusters</span></span>
<span data-ttu-id="5169e-246">Hadoop işlerinin çoğu yalnızca toplu işleri bazen çalışan ' dir.</span><span class="sxs-lookup"><span data-stu-id="5169e-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span></span> <span data-ttu-id="5169e-247">Çoğu Hadoop kümeleri için büyük nokta vardır süresini bu hello küme işleme için kullanılmayan.</span><span class="sxs-lookup"><span data-stu-id="5169e-247">For most Hadoop clusters, there are large periods of time that hello cluster is not being used for processing.</span></span> <span data-ttu-id="5169e-248">HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="5169e-249">Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-249">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="5169e-250">Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="5169e-250">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span>

<span data-ttu-id="5169e-251">Merhaba işlem programı birçok yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="5169e-251">There are many ways you can program hello process:</span></span>

* <span data-ttu-id="5169e-252">Kullanıcı Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5169e-252">User Azure Data Factory.</span></span> <span data-ttu-id="5169e-253">Bkz: [Azure Hdınsight bağlı hizmeti](../data-factory/data-factory-compute-linked-services.md) ve [dönüştürme ve Azure Data Factory kullanarak Analiz](../data-factory/data-factory-data-transformation-activities.md) Hizmetleri için isteğe bağlı ve otomatik olarak tanımlanan Hdınsight bağlı.</span><span class="sxs-lookup"><span data-stu-id="5169e-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span></span>
* <span data-ttu-id="5169e-254">Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="5169e-254">Use Azure PowerShell.</span></span>  <span data-ttu-id="5169e-255">Bkz: [uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="5169e-256">Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="5169e-256">Use Azure CLI.</span></span> <span data-ttu-id="5169e-257">Bkz: [Azure CLI kullanarak Hdınsight kümelerini yönetme](hdinsight-administer-use-command-line.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="5169e-258">Hdınsight .NET SDK'yı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5169e-258">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="5169e-259">Bkz: [gönderme Hadoop işlerini](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="5169e-260">Fiyatlandırma bilgileri hello için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5169e-260">For hello pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="5169e-261">toodelete hello Portal, bir kümeden bkz [küme silme](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="5169e-261">toodelete a cluster from hello Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-cluster-username"></a><span data-ttu-id="5169e-262">Değişiklik kümesi kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="5169e-262">Change cluster username</span></span>
<span data-ttu-id="5169e-263">Hdınsight kümesi, iki kullanıcı hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-263">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="5169e-264">Merhaba Hdınsight küme kullanıcı hesabı hello oluşturma işlemi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5169e-264">hello HDInsight cluster user account is created during hello creation process.</span></span> <span data-ttu-id="5169e-265">RDP aracılığıyla hello küme erişmek için bir RDP kullanıcı hesabı da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-265">You can also create an RDP user account for accessing hello cluster via RDP.</span></span> <span data-ttu-id="5169e-266">Bkz: [etkinleştir Uzak Masaüstü](#connect-to-hdinsight-clusters-by-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="5169e-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span></span>

<span data-ttu-id="5169e-267">**toochange hello Hdınsight küme kullanıcı adı ve parola**</span><span class="sxs-lookup"><span data-stu-id="5169e-267">**toochange hello HDInsight cluster user name and password**</span></span>

1. <span data-ttu-id="5169e-268">İçinde toohello oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5169e-268">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="5169e-269">Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-269">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="5169e-270">Tıklatın **ayarları** hello üst menüsünden ve ardından **küme oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5169e-270">Click **Settings** from hello top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="5169e-271">Varsa **küme oturum açma** bırakıldı etkin'ı tıklatmalısınız **devre dışı**ve ardından **etkinleştirmek** hello kullanıcı adı ve parola değiştirmeden önce...</span><span class="sxs-lookup"><span data-stu-id="5169e-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change hello username and password..</span></span>
5. <span data-ttu-id="5169e-272">Değişiklik hello **küme oturum açma adı** ve/veya hello **küme oturum açma parolasını**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5169e-272">Change hello **Cluster Login Name** and/or hello **Cluster Login Password**, and then click **Save**.</span></span>

    ![Hdınsight küme, kullanıcı, kullanıcı adı, parola, http, kullanıcı değiştirme](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a><span data-ttu-id="5169e-274">GRANT/revoke erişim</span><span class="sxs-lookup"><span data-stu-id="5169e-274">Grant/revoke access</span></span>
<span data-ttu-id="5169e-275">Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="5169e-275">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="5169e-276">ODBC</span><span class="sxs-lookup"><span data-stu-id="5169e-276">ODBC</span></span>
* <span data-ttu-id="5169e-277">JDBC</span><span class="sxs-lookup"><span data-stu-id="5169e-277">JDBC</span></span>
* <span data-ttu-id="5169e-278">Ambari</span><span class="sxs-lookup"><span data-stu-id="5169e-278">Ambari</span></span>
* <span data-ttu-id="5169e-279">Oozie</span><span class="sxs-lookup"><span data-stu-id="5169e-279">Oozie</span></span>
* <span data-ttu-id="5169e-280">Templeton</span><span class="sxs-lookup"><span data-stu-id="5169e-280">Templeton</span></span>

<span data-ttu-id="5169e-281">Varsayılan olarak, bu hizmetleri için erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-281">By default, these services are granted for access.</span></span> <span data-ttu-id="5169e-282">İptal etme/hello erişim hello Azure portal ' sağlayıcısını.</span><span class="sxs-lookup"><span data-stu-id="5169e-282">You can revoke/grant hello access from hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5169e-283">Verme/hello erişimi iptal ederek, hello küme kullanıcı adı ve parola sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="5169e-283">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="5169e-284">**toogrant/revoke HTTP web hizmetleri erişimi**</span><span class="sxs-lookup"><span data-stu-id="5169e-284">**toogrant/revoke HTTP web services access**</span></span>

1. <span data-ttu-id="5169e-285">İçinde toohello oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5169e-285">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="5169e-286">Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-286">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="5169e-287">Tıklatın **ayarları** hello üst menüsünden ve ardından **küme oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5169e-287">Click **Settings** from hello top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="5169e-288">Varsa **küme oturum açma** bırakıldı etkin'ı tıklatmalısınız **devre dışı**ve ardından **etkinleştirmek** hello kullanıcı adı ve parola değiştirmeden önce...</span><span class="sxs-lookup"><span data-stu-id="5169e-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change hello username and password..</span></span>
5. <span data-ttu-id="5169e-289">İçin **küme oturum açma kullanıcı** ve **küme oturum açma parolasını**, hello yeni bir kullanıcı adı ve parola hello küme için (sırasıyla) girin.</span><span class="sxs-lookup"><span data-stu-id="5169e-289">For **Cluster Login Username** and **Cluster Login Password**, enter hello new user name and password (respectively) for hello cluster.</span></span>
6. <span data-ttu-id="5169e-290">**KAYDET**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-290">Click **SAVE**.</span></span>

    ![Hdınsight genel http web hizmeti erişimi Kaldır](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="5169e-292">Merhaba varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="5169e-292">Find hello default storage account</span></span>
<span data-ttu-id="5169e-293">Her Hdınsight kümesinde bir varsayılan depolama hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="5169e-293">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="5169e-294">Merhaba varsayılan depolama hesabı ve alt anahtarları altında bir küme görünür **ayarları**/**özellikleri**/**Azure depolama anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="5169e-294">hello default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span></span> <span data-ttu-id="5169e-295">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="5169e-295">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-resource-group"></a><span data-ttu-id="5169e-296">Merhaba kaynak grup bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="5169e-296">Find hello resource group</span></span>
<span data-ttu-id="5169e-297">Hello Azure Kaynak Yöneticisi modunda her Hdınsight kümesi içeren bir Azure kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5169e-297">In hello Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span></span> <span data-ttu-id="5169e-298">bir küme içinde tooappears ait hello Azure kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="5169e-298">hello Azure resource group that a cluster belongs tooappears in:</span></span>

* <span data-ttu-id="5169e-299">Merhaba küme listesi olan bir **kaynak grubu** sütun.</span><span class="sxs-lookup"><span data-stu-id="5169e-299">hello cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="5169e-300">Küme **temel** döşeme.</span><span class="sxs-lookup"><span data-stu-id="5169e-300">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="5169e-301">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="5169e-301">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="open-hdinsight-query-console"></a><span data-ttu-id="5169e-302">Hdınsight sorgu Konsolu'nu Aç</span><span class="sxs-lookup"><span data-stu-id="5169e-302">Open HDInsight Query console</span></span>
<span data-ttu-id="5169e-303">Merhaba Hdınsight sorgu konsol hello aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="5169e-303">hello HDInsight Query console includes hello following features:</span></span>

* <span data-ttu-id="5169e-304">**Düzenleyici hive**: Hive işlerini göndermenin bir GUI web arabirimi.</span><span class="sxs-lookup"><span data-stu-id="5169e-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span></span>  <span data-ttu-id="5169e-305">Bkz: [kullanarak Hive sorgularını çalıştırma hello sorgu konsol](hdinsight-hadoop-use-hive-query-console.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-305">See [Run Hive queries using hello Query Console](hdinsight-hadoop-use-hive-query-console.md).</span></span>

    ![Hdınsight portal hive Düzenleyicisi](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* <span data-ttu-id="5169e-307">**İş Geçmişi**: İzleyici Hadoop işler.</span><span class="sxs-lookup"><span data-stu-id="5169e-307">**Job history**: Monitor Hadoop jobs.</span></span>  

    ![Hdınsight portal iş geçmişi](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    <span data-ttu-id="5169e-309">Tıklatın **sorgu adı** iş özellikleri dahil olmak üzere tooshow hello ayrıntılarını **sorgu iş**, ve ** iş çıktısı.</span><span class="sxs-lookup"><span data-stu-id="5169e-309">Click **Query Name** tooshow hello details including Job properties, **Job Query**, and **Job Output.</span></span> <span data-ttu-id="5169e-310">Ayrıca, hello sorgu ve hello çıktı tooyour iş istasyonu indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-310">You can also download both hello query and hello output tooyour workstation.</span></span>
* <span data-ttu-id="5169e-311">**Tarayıcı dosya**: hello varsayılan depolama hesabını bulun ve bağlantılı depolama hesapları hello.</span><span class="sxs-lookup"><span data-stu-id="5169e-311">**File Browser**: Browse hello default storage account and hello linked storage accounts.</span></span>

    ![Hdınsight portal dosya tarayıcısı Gözat](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    <span data-ttu-id="5169e-313">Merhaba ekran hello  **<Account>**  hello öğesi olan bir Azure depolama hesabı türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="5169e-313">On hello screenshot, hello **<Account>** type indicates hello item is an Azure storage account.</span></span>  <span data-ttu-id="5169e-314">Merhaba hesap adı toobrowse hello dosyalar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5169e-314">Click hello account name toobrowse hello files.</span></span>
* <span data-ttu-id="5169e-315">**Hadoop UI**.</span><span class="sxs-lookup"><span data-stu-id="5169e-315">**Hadoop UI**.</span></span>

    ![Hdınsight portal Hadoop kullanıcı Arabirimi](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    <span data-ttu-id="5169e-317">Gelen **Hadoop UI*, dosyalara gözatın ve günlüklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-317">From **Hadoop UI*, you can browse files, and check logs.</span></span>
* <span data-ttu-id="5169e-318">**Yarn UI**.</span><span class="sxs-lookup"><span data-stu-id="5169e-318">**Yarn UI**.</span></span>

    ![Hdınsight portal YARN kullanıcı Arabirimi](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a><span data-ttu-id="5169e-320">Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5169e-320">Run Hive queries</span></span>
<span data-ttu-id="5169e-321">Merhaba Portal, tooran Hive işlerini tıklatın **Hive Düzenleyicisi** hello Hdınsight sorgu konsol.</span><span class="sxs-lookup"><span data-stu-id="5169e-321">tooran Hive jobs from hello Portal, click **Hive Editor** in hello HDInsight Query console.</span></span> <span data-ttu-id="5169e-322">Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="5169e-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="5169e-323">İşleri izleme</span><span class="sxs-lookup"><span data-stu-id="5169e-323">Monitor jobs</span></span>
<span data-ttu-id="5169e-324">Merhaba Portal, toomonitor işlerden tıklatın **iş geçmişi** hello Hdınsight sorgu konsol.</span><span class="sxs-lookup"><span data-stu-id="5169e-324">toomonitor jobs from hello Portal, click **Job History** in hello HDInsight Query console.</span></span> <span data-ttu-id="5169e-325">Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="5169e-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="browse-files"></a><span data-ttu-id="5169e-326">Gözatma dosyaları</span><span class="sxs-lookup"><span data-stu-id="5169e-326">Browse files</span></span>
<span data-ttu-id="5169e-327">toobrowse dosyaları hello varsayılan depolama hesabında depolanan ve bağlantılı depolama hesapları Merhaba, tıklatın **dosya tarayıcısı** hello Hdınsight sorgu konsol.</span><span class="sxs-lookup"><span data-stu-id="5169e-327">toobrowse files stored in hello default storage account and hello linked storage accounts, click **File Browser** in hello HDInsight Query console.</span></span> <span data-ttu-id="5169e-328">Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="5169e-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

<span data-ttu-id="5169e-329">Merhaba de kullanabilirsiniz **Gözat hello dosya sistemi** yardımcı programı'ndan hello **Hadoop UI** hello Hdınsight konsolunda.</span><span class="sxs-lookup"><span data-stu-id="5169e-329">You can also use hello **Browse hello file system** utility from hello **Hadoop UI** in hello HDInsight console.</span></span>  <span data-ttu-id="5169e-330">Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="5169e-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="5169e-331">Küme kullanımını izleme</span><span class="sxs-lookup"><span data-stu-id="5169e-331">Monitor cluster usage</span></span>
<span data-ttu-id="5169e-332">Merhaba **kullanım** hello Hdınsight kümesi dikey bölümünü hello toothis küme ve bulundukları nasıl ayrılan çekirdek sayısı yanı sıra, Hdınsight ile kullanmak için çekirdek kullanılabilir tooyour abonelik hello sayısı hakkında bilgileri görüntüler Bu küme içindeki hello düğümler için ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="5169e-332">hello **Usage** section of hello HDInsight cluster blade displays information about hello number of cores available tooyour subscription for use with HDInsight, as well as hello number of cores allocated toothis cluster and how they are allocated for hello nodes within this cluster.</span></span> <span data-ttu-id="5169e-333">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="5169e-333">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5169e-334">toomonitor hello Hizmetleri Hdınsight kümesi hello tarafından sağlanan, Ambari REST API hello veya Ambari Web kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5169e-334">toomonitor hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="5169e-335">Ambari kullanarak daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="5169e-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="open-hadoop-ui"></a><span data-ttu-id="5169e-336">Hadoop kullanıcı arabirimini açın</span><span class="sxs-lookup"><span data-stu-id="5169e-336">Open Hadoop UI</span></span>
<span data-ttu-id="5169e-337">toomonitor hello küme, Gözat hello dosya sistemi ve onay günlükleri, **Hadoop UI** hello Hdınsight sorgu konsol.</span><span class="sxs-lookup"><span data-stu-id="5169e-337">toomonitor hello cluster, browse hello file system, and check logs, click **Hadoop UI** in hello HDInsight Query console.</span></span> <span data-ttu-id="5169e-338">Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="5169e-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="open-yarn-ui"></a><span data-ttu-id="5169e-339">Yarn kullanıcı arabirimini açın</span><span class="sxs-lookup"><span data-stu-id="5169e-339">Open Yarn UI</span></span>
<span data-ttu-id="5169e-340">toouse Yarn kullanıcı arabirimi, tıklatın **Yarn kullanıcı Arabiriminde** hello Hdınsight sorgu konsol.</span><span class="sxs-lookup"><span data-stu-id="5169e-340">toouse Yarn user interface, click **Yarn UI** in hello HDInsight Query console.</span></span> <span data-ttu-id="5169e-341">Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="5169e-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="connect-tooclusters-using-rdp"></a><span data-ttu-id="5169e-342">RDP kullanarak tooclusters Bağlan</span><span class="sxs-lookup"><span data-stu-id="5169e-342">Connect tooclusters using RDP</span></span>
<span data-ttu-id="5169e-343">Merhaba kimlik bilgilerini, oluşturma sırasında sağlanan hello küme toohello Hizmetleri hello küme ancak değil toohello kümenin kendisi Uzak Masaüstü aracılığıyla erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5169e-343">hello credentials for hello cluster that you provided at its creation give access toohello services on hello cluster, but not toohello cluster itself through Remote Desktop.</span></span> <span data-ttu-id="5169e-344">Bir küme sağladığınızda veya bir küme sağlandıktan sonra Uzak Masaüstü erişimi kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span></span> <span data-ttu-id="5169e-345">Oluşturma sırasında Uzak Masaüstü'nü etkinleştirme hakkında hello yönergeler için bkz: [oluşturma Hdınsight kümesi](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5169e-345">For hello instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="5169e-346">**tooenable Uzak Masaüstü**</span><span class="sxs-lookup"><span data-stu-id="5169e-346">**tooenable Remote Desktop**</span></span>

1. <span data-ttu-id="5169e-347">İçinde toohello oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5169e-347">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="5169e-348">Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-348">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="5169e-349">Tıklatın **ayarları** hello üst menüsünden ve ardından **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="5169e-349">Click **Settings** from hello top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="5169e-350">Girin **süresi**, **Uzak Masaüstü kullanıcı adı** ve **Uzak Masaüstü parola**ve ardından **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="5169e-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span></span>

    ![Hdınsight etkinleştirme devre dışı bırakma, Uzak Masaüstü'nü yapılandırma](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    <span data-ttu-id="5169e-352">Merhaba varsayılan değerleri süresi bir hafta olur.</span><span class="sxs-lookup"><span data-stu-id="5169e-352">hello default values for Expires On is a week.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5169e-353">Bir kümede hello Hdınsight .NET SDK'sı tooenable Uzak Masaüstü'nü de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-353">You can also use hello HDInsight .NET SDK tooenable Remote Desktop on a cluster.</span></span> <span data-ttu-id="5169e-354">Kullanım hello **EnableRdp** hello Hdınsight istemci şekilde aşağıdaki hello nesnesinde yöntemi: **istemci. EnableRdp (clustername, konum, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span><span class="sxs-lookup"><span data-stu-id="5169e-354">Use hello **EnableRdp** method on hello HDInsight client object in hello following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span></span> <span data-ttu-id="5169e-355">Benzer şekilde, Uzak Masaüstü toodisable hello kümede kullanabileceğiniz **istemci. DisableRdp (clustername, konum)**.</span><span class="sxs-lookup"><span data-stu-id="5169e-355">Similarly, toodisable Remote Desktop on hello cluster, you can use **client.DisableRdp(clustername, location)**.</span></span> <span data-ttu-id="5169e-356">Bu yöntemleri hakkında daha fazla bilgi için bkz: [Hdınsight .NET SDK'sı başvurusu](http://go.microsoft.com/fwlink/?LinkId=529017).</span><span class="sxs-lookup"><span data-stu-id="5169e-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span></span> <span data-ttu-id="5169e-357">Bu, yalnızca Windows üzerinde çalışan Hdınsight kümeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5169e-357">This is applicable only for HDInsight clusters running on Windows.</span></span>
   >
   >

<span data-ttu-id="5169e-358">**RDP kullanarak tooconnect tooa küme**</span><span class="sxs-lookup"><span data-stu-id="5169e-358">**tooconnect tooa cluster by using RDP**</span></span>

1. <span data-ttu-id="5169e-359">İçinde toohello oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5169e-359">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="5169e-360">Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5169e-360">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="5169e-361">Tıklatın **ayarları** hello üst menüsünden ve ardından **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="5169e-361">Click **Settings** from hello top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="5169e-362">Tıklatın **Bağlan** ve hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5169e-362">Click **Connect** and follow hello instructions.</span></span> <span data-ttu-id="5169e-363">Bağlantı devre dışı ise, önce etkinleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-363">If Connect is disable, you must enable it first.</span></span> <span data-ttu-id="5169e-364">Merhaba Uzak Masaüstü kullanıcı adı ve parola kullanarak emin olun.</span><span class="sxs-lookup"><span data-stu-id="5169e-364">Make sure using hello Remote Desktop user username and password.</span></span>  <span data-ttu-id="5169e-365">Merhaba küme kullanıcı kimlik bilgilerini kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="5169e-365">You can't use hello Cluster user credentials.</span></span>

## <a name="open-hadoop-command-line"></a><span data-ttu-id="5169e-366">Hadoop komut satırı açın</span><span class="sxs-lookup"><span data-stu-id="5169e-366">Open Hadoop command line</span></span>
<span data-ttu-id="5169e-367">Uzak Masaüstü'nü ve kullanım hello Hadoop komut satırını kullanarak tooconnect toohello küme, önce Uzak Masaüstü erişimi toohello küme hello önceki bölümde açıklandığı gibi etkinleştirmiş olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5169e-367">tooconnect toohello cluster by using Remote Desktop and use hello Hadoop command line, you must first have enabled Remote Desktop access toohello cluster as described in hello previous section.</span></span>

<span data-ttu-id="5169e-368">**tooopen Hadoop komut satırı**</span><span class="sxs-lookup"><span data-stu-id="5169e-368">**tooopen a Hadoop command line**</span></span>

1. <span data-ttu-id="5169e-369">Uzak Masaüstü kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5169e-369">Connect toohello cluster using Remote Desktop.</span></span>
2. <span data-ttu-id="5169e-370">Merhaba masaüstünden çift **Hadoop komut satırı**.</span><span class="sxs-lookup"><span data-stu-id="5169e-370">From hello desktop, double-click **Hadoop Command Line**.</span></span>

    <span data-ttu-id="5169e-371">![HDI. HadoopCommandLine][image-hadoopcommandline]</span><span class="sxs-lookup"><span data-stu-id="5169e-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span></span>

    <span data-ttu-id="5169e-372">Hadoop komutları hakkında daha fazla bilgi için bkz: [Hadoop komutları başvuru](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span><span class="sxs-lookup"><span data-stu-id="5169e-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span></span>

<span data-ttu-id="5169e-373">Merhaba önceki ekran görüntüsünde, hello klasör adı katıştırılmış hello Hadoop sürüm numarasına sahip.</span><span class="sxs-lookup"><span data-stu-id="5169e-373">In hello previous screenshot, hello folder name has hello Hadoop version number embedded.</span></span> <span data-ttu-id="5169e-374">Merhaba sürüm numarası hello kümeye yüklü hello Hadoop bileşenleri değiştirilen göre hello sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="5169e-374">hello version number can changed based on hello version of hello Hadoop components installed on hello cluster.</span></span> <span data-ttu-id="5169e-375">Hadoop ortam değişkenleri toorefer toothose klasörleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-375">You can use Hadoop environment variables toorefer toothose folders.</span></span> <span data-ttu-id="5169e-376">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5169e-376">For example:</span></span>

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a><span data-ttu-id="5169e-377">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5169e-377">Next steps</span></span>
<span data-ttu-id="5169e-378">Bu makalede, nasıl toocreate kullanarak bir Hdınsight kümesi hello Portal ve nasıl tooopen hello Hadoop komut satırı aracı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="5169e-378">In this article, you have learned how toocreate an HDInsight cluster by using hello Portal, and how tooopen hello Hadoop command-line tool.</span></span> <span data-ttu-id="5169e-379">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="5169e-379">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="5169e-380">Hdınsight Azure PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="5169e-380">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="5169e-381">Hdınsight Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="5169e-381">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="5169e-382">Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5169e-382">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="5169e-383">Hadoop işlerini programlı olarak gönderme</span><span class="sxs-lookup"><span data-stu-id="5169e-383">Submit Hadoop jobs programmatically</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="5169e-384">Azure Hdınsight kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5169e-384">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="5169e-385">Azure Hdınsight'ta Hadoop hangi sürümünün mi?</span><span class="sxs-lookup"><span data-stu-id="5169e-385">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop komut satırı"
