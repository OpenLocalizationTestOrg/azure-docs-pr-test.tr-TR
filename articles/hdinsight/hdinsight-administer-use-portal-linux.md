---
title: "Azure portalını kullanarak hdınsight'ta Hadoop kümelerini yönetme | Microsoft Docs"
description: "Oluşturma ve Azure portalını kullanarak Hdınsight kümelerini yönetme hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c9cb631aef71f72457c3517d02566a56919f82bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="e1cd0-103">Azure portalını kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="e1cd0-104">Kullanarak [Azure portal][azure-portal], Azure hdınsight'ta Hadoop kümelerini yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="e1cd0-105">Diğer araçları kullanarak hdınsight'ta Hadoop kümelerini yönetme hakkında bilgi için sekme seçicisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-105">Use the tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="e1cd0-106">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="e1cd0-106">**Prerequisites**</span></span>

<span data-ttu-id="e1cd0-107">Bu makaleye başlamadan önce aşağıdaki öğeleri sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-107">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="e1cd0-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-108">**An Azure subscription**.</span></span> <span data-ttu-id="e1cd0-109">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="e1cd0-110">Portalını açın</span><span class="sxs-lookup"><span data-stu-id="e1cd0-110">Open the portal</span></span>
1. <span data-ttu-id="e1cd0-111">Oturum [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-111">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1cd0-112">Portal açtıktan sonra şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-112">After you open the portal, you can:</span></span>

   * <span data-ttu-id="e1cd0-113">Tıklatın **yeni** sol menüden yeni bir küme oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-113">Click **New** from the left menu to create a new cluster:</span></span>

       ![Yeni Hdınsight küme düğmesi](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * <span data-ttu-id="e1cd0-115">Tıklatın **Hdınsight kümeleri** var olan kümeleri listelemek için sol menüden</span><span class="sxs-lookup"><span data-stu-id="e1cd0-115">Click **HDInsight Clusters** from the left menu to list the existing clusters</span></span>

       ![Azure portal Hdınsight küme düğmesi](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="e1cd0-117">' I tıklatın, Hdınsight kümesi görmüyorsanız, **daha fazla hizmet** listesi ve ardından altındaki **Hdınsight kümeleri** altında **Intelligence + analiz** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-117">If you don't see HDInsight cluster, click **More services** on the bottom of the list, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span></span>


## <a name="create-clusters"></a><span data-ttu-id="e1cd0-118">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e1cd0-119">Hdınsight geniş Hadoop bileşenleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="e1cd0-120">Doğrulandı ve desteklenen bileşenlerin listesi için bkz: [hangi sürümüdür Azure Hdınsight'ta hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-120">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="e1cd0-121">Genel küme oluşturma için bilgi [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-121">For the general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="e1cd0-122">Erişim denetimi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="e1cd0-122">Access control requirements</span></span>

<span data-ttu-id="e1cd0-123">Bir Hdınsight kümesi oluştururken, bir Azure aboneliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-123">You must specify an Azure subscription when you create an HDInsight cluster.</span></span> <span data-ttu-id="e1cd0-124">Bu küme, yeni bir Azure kaynak grubu veya varolan bir kaynak grubu içinde oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-124">This cluster can be created in either a new Azure Resource group or an existing Resource group.</span></span> <span data-ttu-id="e1cd0-125">Hdınsight kümeleri oluşturmak için izinlerinizi doğrulamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-125">You can use the following steps to verify your permissions for creating HDInsight clusters:</span></span>

- <span data-ttu-id="e1cd0-126">Var olan bir kaynak grubunu kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-126">To use an existing resource group.</span></span>

    1. <span data-ttu-id="e1cd0-127">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="e1cd0-128">Tıklatın **kaynak grupları** kaynak gruplarını listelemek için sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-128">Click **Resource groups** from the left menu to list the resource groups.</span></span>
    3. <span data-ttu-id="e1cd0-129">Hdınsight kümesi oluşturmak için kullanmak istediğiniz kaynak grubunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-129">Click the resource group you want to use for creating your HDInsight cluster.</span></span>
    4. <span data-ttu-id="e1cd0-130">Tıklatın **erişim denetimi (IAM)**, doğrulayın sizin (veya ait olduğunuz bir grubu) en az katkıda bulunan kaynak grubu erişimi.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-130">Click **Access control (IAM)**, and verify that you (or a group that you belong to) have at least the Contributor access to the resource group.</span></span>

- <span data-ttu-id="e1cd0-131">Yeni bir kaynak grubu oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="e1cd0-131">To create a new resource group</span></span>

    1. <span data-ttu-id="e1cd0-132">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-132">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="e1cd0-133">Tıklatın **abonelik** sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-133">Click **Subscription** from the left menu.</span></span> <span data-ttu-id="e1cd0-134">Sarı bir anahtar simgesi vardır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-134">It has a yellow key icon.</span></span> <span data-ttu-id="e1cd0-135">Aboneliklerin listesini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-135">You shall see a list of subscriptions.</span></span>
    3. <span data-ttu-id="e1cd0-136">Kümeleri oluşturmak için kullandığınız aboneliğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-136">Click the subscription that you use to create clusters.</span></span> 
    4. <span data-ttu-id="e1cd0-137">Tıklatın **izinlerimi**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-137">Click **My permissions**.</span></span>  <span data-ttu-id="e1cd0-138">Bunu gösterir, [rol](../active-directory/role-based-access-control-what-is.md#built-in-roles) abonelikte.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-138">It shows your [role](../active-directory/role-based-access-control-what-is.md#built-in-roles) on the subscription.</span></span> <span data-ttu-id="e1cd0-139">En az gereksinim duyduğunuz Hdınsight kümesi oluşturmak için katkıda bulunan erişim.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-139">You need at least Contributor access to create HDInsight cluster.</span></span>

<span data-ttu-id="e1cd0-140">NoRegisteredProviderFound hatası veya MissingSubscriptionRegistration hatası alırsanız, bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-140">If you receive the NoRegisteredProviderFound error or the MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="e1cd0-141">Liste ve kümeleri Göster</span><span class="sxs-lookup"><span data-stu-id="e1cd0-141">List and show clusters</span></span>
1. <span data-ttu-id="e1cd0-142">Oturum [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-142">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1cd0-143">Tıklatın **Hdınsight kümeleri** var olan kümeleri listelemek için sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-143">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="e1cd0-144">Küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-144">Click the cluster name.</span></span> <span data-ttu-id="e1cd0-145">Küme listesi uzunsa, sayfanın üst kısmında filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-145">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="e1cd0-146">Genel bakış sayfasında görmek için listeden bir kümeden tıklatın:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-146">Click a cluster from the list to see the overview page:</span></span>

    ![Azure portal Hdınsight küme temelleri](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * <span data-ttu-id="e1cd0-148">**Pano**: Ambari Web Linux tabanlı kümeler için olan küme panosu açılır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-148">**Dashboard**: Opens the cluster dashboard, which is Ambari Web for Linux-based clusters.</span></span>
    * <span data-ttu-id="e1cd0-149">**Güvenli Kabuk**: Güvenli Kabuk (SSH) bağlantısı kullanarak kümeye bağlanmak için yönergeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-149">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
    * <span data-ttu-id="e1cd0-150">**Küme ölçeklendirme**: Bu küme için alt düğüm sayısını değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-150">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
    * <span data-ttu-id="e1cd0-151">**Silme**: kümeyi siler.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-151">**Delete**: Deletes the cluster.</span></span>
    * <span data-ttu-id="e1cd0-152">**Etkinlik günlükleri**: Göster ve sorgu etkinlik günlükleri.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-152">**Activity logs**: Show and query activity logs.</span></span>
    * <span data-ttu-id="e1cd0-153">**Erişim denetimi (IAM)**: rol atamalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-153">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="e1cd0-154">Bkz: [Azure aboneliği kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-154">See [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
    * <span data-ttu-id="e1cd0-155">**Etiketler**: Bulut hizmetlerinizi, özel bir sınıflandırma tanımlamak için anahtar/değer çiftlerinin ayarlamanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-155">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="e1cd0-156">Örneğin, adlı bir anahtar oluşturabilir **proje**ve ardından belirli bir projeyle ilişkili tüm hizmetler için ortak bir değer kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-156">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
    * <span data-ttu-id="e1cd0-157">**Sorunları tanılamak ve**: sorun giderme bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-157">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
    * <span data-ttu-id="e1cd0-158">**Kilitler**: değiştirilmiş veya silinmiş olan küme önlemek için kilit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-158">**Locks**: Add lock to prevent the cluster being modified or deleted.</span></span>
    * <span data-ttu-id="e1cd0-159">**Otomasyon betiğini**: görüntü ve küme için Azure Resource Manager şablonunu dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-159">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span></span> <span data-ttu-id="e1cd0-160">Şu anda, yalnızca bağımlı Azure depolama hesabı dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-160">Currently, you can only export the dependent Azure storage account.</span></span> <span data-ttu-id="e1cd0-161">Bkz: [oluşturma Linux tabanlı Hadoop kümeleri Azure Resource Manager şablonları kullanarak Hdınsight'ta](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-161">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
    * <span data-ttu-id="e1cd0-162">**Hızlı Başlangıç**: yardımcı olacak bilgileri görüntüler, Hdınsight kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-162">**Quick Start**:  Displays information that helps you get started using HDInsight.</span></span>
    * <span data-ttu-id="e1cd0-163">**Hdınsight Araçları**: Hdınsight için Yardım bilgileri ilgili araçlar.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-163">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
    * <span data-ttu-id="e1cd0-164">**Oturum açma küme**: küme oturum açma bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-164">**Cluster Login**: Display the cluster login information.</span></span>
    * <span data-ttu-id="e1cd0-165">**Abonelik çekirdek kullanım**: aboneliğiniz için kullanılan ve kullanılabilir çekirdekler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-165">**Subscription Core Usage**: Display the used and available cores for your subscription.</span></span>
    * <span data-ttu-id="e1cd0-166">**Küme ölçeklendirme**: artırma ve azaltma küme çalışan düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-166">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span> <span data-ttu-id="e1cd0-167">Bkz:[ölçek kümeleri](hdinsight-administer-use-management-portal.md#scale-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-167">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
    * <span data-ttu-id="e1cd0-168">**Güvenli Kabuk**: Güvenli Kabuk (SSH) bağlantısı kullanarak kümeye bağlanmak için yönergeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-168">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="e1cd0-169">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-169">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    * <span data-ttu-id="e1cd0-170">**Hdınsight iş ortağı**: geçerli Hdınsight iş ortağı Ekle/Kaldır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-170">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span></span>
    * <span data-ttu-id="e1cd0-171">**Dış meta deponuz**: Hive ve Oozie meta deponuz görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-171">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="e1cd0-172">Meta depolar, yalnızca küme oluşturma işlemi sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-172">The metastores can only be configured during the cluster creation process.</span></span> <span data-ttu-id="e1cd0-173">Bkz: [Hive/Oozie meta depo kullanmak](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-173">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
    * <span data-ttu-id="e1cd0-174">**Betik eylemleri**: çalıştırmak Bash betikleri küme üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-174">**Script Actions**: Run Bash scripts on the cluster.</span></span> <span data-ttu-id="e1cd0-175">Bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-175">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    * <span data-ttu-id="e1cd0-176">**Uygulamaları**: Ekle/Kaldır Hdınsight uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-176">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="e1cd0-177">Bkz: [özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-177">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
    * <span data-ttu-id="e1cd0-178">**Özellikleri**: küme özelliklerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-178">**Properties**: View the cluster properties.</span></span>
    * <span data-ttu-id="e1cd0-179">**Depolama hesapları**: depolama hesaplarını ve anahtarlarını görüntülemek.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-179">**Storage accounts**: View the storage accounts and the keys.</span></span> <span data-ttu-id="e1cd0-180">Depolama hesapları küme oluşturma işlemi sırasında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-180">The storage accounts are configured during the cluster creation process.</span></span>
    * <span data-ttu-id="e1cd0-181">**Küme AAD kimlik**:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-181">**Cluster AAD Identity**:</span></span>
    * <span data-ttu-id="e1cd0-182">**Yeni destek isteği**: Microsoft desteği ile bir destek bileti oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-182">**New support request**: Allows you to create a support ticket with Microsoft support.</span></span>
    
6. <span data-ttu-id="e1cd0-183">Tıklatın **özellikleri**:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-183">Click **Properties**:</span></span>

    <span data-ttu-id="e1cd0-184">Özellikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-184">The properties are:</span></span>

   * <span data-ttu-id="e1cd0-185">**Ana bilgisayar adı**: küme adı.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="e1cd0-186">**Küme URL**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-186">**Cluster URL**.</span></span> <span data-ttu-id="e1cd0-187">Ambari web arabirimi için URL.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-187">The URL for the Ambari web interface.</span></span>
   * <span data-ttu-id="e1cd0-188">**Durum**: dahil, kabul iptal ClusterStorageProvisioned, AzureVMConfiguration, çalıştığından, silme, hatası, HDInsightConfiguration, işletimsel, silinen, süresi sona erdi, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="e1cd0-188">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="e1cd0-189">**Bölge**: Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-189">**Region**: Azure location.</span></span> <span data-ttu-id="e1cd0-190">Desteklenen Azure konumlar listesi için bkz: **bölge** açılan liste kutusunu [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-190">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="e1cd0-191">**Oluşturulma tarihi**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-191">**Date created**.</span></span>
   * <span data-ttu-id="e1cd0-192">**İşletim sistemi**: ya da **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-192">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="e1cd0-193">**Tür**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-193">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="e1cd0-194">**Sürüm**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-194">**Version**.</span></span> <span data-ttu-id="e1cd0-195">Bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="e1cd0-195">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="e1cd0-196">**Abonelik**: Abonelik adı.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-196">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="e1cd0-197">**Varsayılan veri kaynağı**: varsayılan küme dosya sistemi.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-197">**Default data source**: The default cluster file system.</span></span>
   * <span data-ttu-id="e1cd0-198">**Çalışan düğüm boyutu**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-198">**Worker nodes size**.</span></span>
   * <span data-ttu-id="e1cd0-199">**Baş düğüm boyutu**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-199">**Head node size**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="e1cd0-200">Küme silme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-200">Delete clusters</span></span>
<span data-ttu-id="e1cd0-201">Küme silme varsayılan depolama hesabı ya da bağlı tüm depolama hesaplarını silmez.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-201">Deleting a cluster does not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="e1cd0-202">Küme aynı depolama hesapları ve aynı meta deponuz kullanarak yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-202">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span> <span data-ttu-id="e1cd0-203">Kümeyi yeniden oluşturduğunuzda, yeni varsayılan Blob kapsayıcısını kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-203">It is recommended to use a new default Blob container when you re-create the cluster.</span></span>

1. <span data-ttu-id="e1cd0-204">Oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e1cd0-204">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="e1cd0-205">Tıklatın **Hdınsight kümeleri** sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-205">Click **HDInsight Clusters** from the left menu.</span></span> <span data-ttu-id="e1cd0-206">Görmüyorsanız, **Hdınsight kümeleri**, tıklatın **daha fazla hizmet** ilk.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-206">If you don't see **HDInsight Clusters**, click **More services** first.</span></span>
3. <span data-ttu-id="e1cd0-207">Silmek istediğiniz kümesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-207">Click the cluster that you want to delete.</span></span>
4. <span data-ttu-id="e1cd0-208">Tıklatın **silmek** üstteki menüden ve yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-208">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="e1cd0-209">Ayrıca bkz. [Duraklat/kümeleri kapatma](#pauseshut-down-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-209">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="e1cd0-210">Başka depolama hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-210">Add additional storage accounts</span></span>

<span data-ttu-id="e1cd0-211">Bir küme oluşturulduktan sonra ek Azure Storage ve Azure Data Lake Store hesapları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-211">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span></span> <span data-ttu-id="e1cd0-212">Daha fazla bilgi için bkz. [HDInsight’a başka depolama hesapları ekleme](./hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-212">For more information, see [Add additional storage accounts to HDInsight](./hdinsight-hadoop-add-storage.md).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="e1cd0-213">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-213">Scale clusters</span></span>
<span data-ttu-id="e1cd0-214">Özellik ölçeklendirme küme kümeye yeniden oluşturmak zorunda kalmadan Azure Hdınsight'ta çalıştıran bir küme tarafından kullanılan çalışan düğümü sayısını değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-214">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e1cd0-215">Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-215">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="e1cd0-216">Kümenizin sürümünü emin değilseniz, Özellikler sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-216">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="e1cd0-217">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-217">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="e1cd0-218">Her tür Hdınsight tarafından desteklenen küme için veri düğüm sayısını değiştirme etkisi:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-218">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="e1cd0-219">Hadoop</span><span class="sxs-lookup"><span data-stu-id="e1cd0-219">Hadoop</span></span>

    <span data-ttu-id="e1cd0-220">Sorunsuz bir şekilde tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-220">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="e1cd0-221">İşlemi devam ederken yeni işleri da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-221">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="e1cd0-222">Kümenin her zaman işlevsel bir durumda bırakılır böylece bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-222">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="e1cd0-223">Bir Hadoop kümesine veri düğüm sayısını azaltarak ölçeklendirilir, bazı kümedeki hizmetleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-223">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="e1cd0-224">Bu davranış tüm çalışan ve işleri bekleyen ölçeklendirme işlemi tamamlandığında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-224">This behavior causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="e1cd0-225">İşlemi tamamlandıktan sonra ancak, sunmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-225">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="e1cd0-226">HBase</span><span class="sxs-lookup"><span data-stu-id="e1cd0-226">HBase</span></span>

    <span data-ttu-id="e1cd0-227">Sorunsuz bir şekilde ekleyebilir veya çalışırken, HBase kümesi düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-227">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="e1cd0-228">Bölgesel sunucular otomatik olarak ölçeklendirme işlemi tamamladıktan birkaç dakika içinde dengeli.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-228">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="e1cd0-229">Ancak, küme headnode için oturum açma ve bir komut istemi penceresinden aşağıdaki komutları çalıştırarak el ile de bölgesel sunucular dengeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-229">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="e1cd0-230">HBase kabuğunu kullanma hakkında daha fazla bilgi için bkz:]</span><span class="sxs-lookup"><span data-stu-id="e1cd0-230">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="e1cd0-231">Storm</span><span class="sxs-lookup"><span data-stu-id="e1cd0-231">Storm</span></span>

    <span data-ttu-id="e1cd0-232">Sorunsuz bir şekilde ekleyebilir veya çalışırken Storm kümeniz veri düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-232">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="e1cd0-233">Ancak ölçeklendirme işlemi başarıyla tamamlandıktan sonra topoloji yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-233">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="e1cd0-234">İki yolla yeniden dengelenmesi gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-234">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="e1cd0-235">Storm web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="e1cd0-235">Storm web UI</span></span>
  * <span data-ttu-id="e1cd0-236">Komut satırı arabirimi (CLI) aracı</span><span class="sxs-lookup"><span data-stu-id="e1cd0-236">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="e1cd0-237">Başvurmak [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-237">Refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="e1cd0-238">Hdınsight kümesinde Storm web kullanıcı Arabirimi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-238">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![Hdınsight Storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="e1cd0-240">Storm topolojisini yeniden dengelemeniz CLI komutunu kullanma örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-240">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="e1cd0-241">**Küme ölçeklendirme**</span><span class="sxs-lookup"><span data-stu-id="e1cd0-241">**To scale clusters**</span></span>

1. <span data-ttu-id="e1cd0-242">Oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e1cd0-242">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="e1cd0-243">Tıklatın **Hdınsight kümeleri** sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-243">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="e1cd0-244">Ölçeklendirmek istediğiniz kümesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-244">Click the cluster you want to scale.</span></span>
3. <span data-ttu-id="e1cd0-245">Tıklatın **ölçeklendirme kümesi**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-245">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="e1cd0-246">Girin **sayı, alt düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-246">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="e1cd0-247">Küme düğümleri sayısı Azure abonelikleri arasında değişiklik gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-247">The limit on the number of cluster nodes varies among Azure subscriptions.</span></span> <span data-ttu-id="e1cd0-248">Sınırını artırmak için fatura desteğine başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-248">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="e1cd0-249">Maliyet bilgileri düğüm sayısını yapmış olduğunuz değişiklikleri yansıtır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-249">The cost information reflects the changes you have made to the number of nodes.</span></span>

    ![Hdınsight, hadoop, hbase, storm, spark, Ölçek](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="e1cd0-251">Kümeleri Duraklat/kapatma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-251">Pause/shut down clusters</span></span>

<span data-ttu-id="e1cd0-252">Hadoop işlerinin çoğu yalnızca zaman zaman çalıştırmak toplu işleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-252">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="e1cd0-253">Çoğu Hadoop kümeleri için küme işleme için kullanılmayan süreyi büyük nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-253">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="e1cd0-254">HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-254">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="e1cd0-255">Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-255">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="e1cd0-256">Küme ücretleri depolama ücretlerinin birkaç katı olduğundan, kullanılmadığında kümelerin silinmesi mantıklı olandır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-256">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="e1cd0-257">İşlem programı birçok yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-257">There are many ways you can program the process:</span></span>

* <span data-ttu-id="e1cd0-258">Kullanıcı Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-258">User Azure Data Factory.</span></span> <span data-ttu-id="e1cd0-259">Bkz: [oluşturma isteğe bağlı Linux tabanlı Hadoop kümeleri Azure Data Factory kullanarak Hdınsight'ta](hdinsight-hadoop-create-linux-clusters-adf.md) isteğe bağlı Hdınsight oluşturmak için bağlantılı Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-259">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="e1cd0-260">Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-260">Use Azure PowerShell.</span></span>  <span data-ttu-id="e1cd0-261">Bkz: [uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-261">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="e1cd0-262">Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-262">Use Azure CLI.</span></span> <span data-ttu-id="e1cd0-263">Bkz: [Azure CLI kullanarak Hdınsight kümelerini yönetme](hdinsight-administer-use-command-line.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-263">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="e1cd0-264">Hdınsight .NET SDK'yı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-264">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="e1cd0-265">Bkz: [gönderme Hadoop işlerini](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-265">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="e1cd0-266">Fiyatlandırma bilgileri için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-266">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="e1cd0-267">Portaldan bir kümeyi silmek için bkz: [küme silme](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="e1cd0-267">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>


## <a name="upgrade-clusters"></a><span data-ttu-id="e1cd0-268">Küme yükseltme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-268">Upgrade clusters</span></span>

<span data-ttu-id="e1cd0-269">Bkz: [daha yeni bir sürüme yükseltme Hdınsight kümesi](./hdinsight-upgrade-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-269">See [Upgrade HDInsight cluster to a newer version](./hdinsight-upgrade-cluster.md).</span></span>

## <a name="change-passwords"></a><span data-ttu-id="e1cd0-270">Parolaları değiştirme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-270">Change passwords</span></span>
<span data-ttu-id="e1cd0-271">Hdınsight kümesi, iki kullanıcı hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-271">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="e1cd0-272">Hdınsight küme kullanıcı hesabı (paketini</span><span class="sxs-lookup"><span data-stu-id="e1cd0-272">The HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="e1cd0-273">HTTP kullanıcı hesabı) ve SSH kullanıcı hesabı oluşturma işlemi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-273">HTTP user account) and the SSH user account are created during the creation process.</span></span> <span data-ttu-id="e1cd0-274">Küme kullanıcı hesabı kullanıcı adı ve parola ve SSH kullanıcı hesabını değiştirmek için betik eylemleri değiştirmek için Ambari web kullanıcı Arabirimi kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1cd0-274">You can use the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span></span>

### <a name="change-the-cluster-user-password"></a><span data-ttu-id="e1cd0-275">Küme kullanıcı parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-275">Change the cluster user password</span></span>
<span data-ttu-id="e1cd0-276">Küme kullanıcı parolasını değiştirmek için Ambari Web kullanıcı arabirimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-276">You can use the Ambari Web UI to change the Cluster user password.</span></span> <span data-ttu-id="e1cd0-277">Ambarı'na oturum açmak için mevcut küme kullanıcı adı ve parola kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-277">To log in to Ambari, you must use the existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="e1cd0-278">Küme kullanıcı (Yönetici) parolasını değiştirme eylemler başarısız bu kümeye karşı çalışan betik neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-278">Changing the cluster user (admin) password may cause script actions ran against this cluster to fail.</span></span> <span data-ttu-id="e1cd0-279">Kalıcı betik eylemleri, hedef alt düğümleri varsa, bu komut dosyaları küme düğümlerine operations yeniden boyutlandırma eklediğinizde başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-279">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes to the cluster through resize operations.</span></span> <span data-ttu-id="e1cd0-280">Betik eylemleri hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-280">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="e1cd0-281">Ambari Web Hdınsight küme kullanıcı kimlik bilgilerini kullanarak kullanıcı Arabirimi için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-281">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="e1cd0-282">Varsayılan kullanıcı adı **admin** şeklindedir. URL **https://&lt;Hdınsight küme adı > azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-282">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="e1cd0-283">Tıklatın **yönetici** üstteki menüden "Ambarı Yönet"'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-283">Click **Admin** from the top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="e1cd0-284">Sol menüden **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-284">From the left menu, click **Users**.</span></span>
4. <span data-ttu-id="e1cd0-285">Tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-285">Click **Admin**.</span></span>
5. <span data-ttu-id="e1cd0-286">Tıklatın **Parola Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-286">Click **Change Password**.</span></span>

<span data-ttu-id="e1cd0-287">Ambari sonra kümedeki tüm düğümlerde parolasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-287">Ambari then changes the password on all nodes in the cluster.</span></span>

### <a name="change-the-ssh-user-password"></a><span data-ttu-id="e1cd0-288">SSH kullanıcı parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-288">Change the SSH user password</span></span>
1. <span data-ttu-id="e1cd0-289">Bir metin düzenleyicisi kullanarak, aşağıdaki metni adlı bir dosya Kaydet **changepassword.sh**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-289">Using a text editor, save the following text as a file named **changepassword.sh**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e1cd0-290">Satır bitiş olarak LF kullanan bir Düzenleyicisi'ni kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-290">You must use an editor that uses LF as the line ending.</span></span> <span data-ttu-id="e1cd0-291">Düzenleyici CRLF kullanıyorsa, komut çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-291">If the editor uses CRLF, then the script does not work.</span></span>
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. <span data-ttu-id="e1cd0-292">Bir HTTP veya HTTPS adresi kullanarak Hdınsight'ta erişilebilen bir depolama konumuna dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-292">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="e1cd0-293">Örneğin, ortak bir dosyanın gibi OneDrive veya Azure Blob Depolama depolayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-293">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="e1cd0-294">Bu URI sonraki adımda gerektiğinde URI (HTTP veya HTTPS adresi) dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-294">Save the URI (HTTP or HTTPS address) to the file, as this URI is needed in the next step.</span></span>
3. <span data-ttu-id="e1cd0-295">Azure portalından tıklatın **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-295">From the Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="e1cd0-296">Hdınsight kümesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-296">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="e1cd0-297">Tıklatın **betik eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-297">Click **Script Actions**.</span></span>
4. <span data-ttu-id="e1cd0-298">Gelen **betik eylemleri** dikey penceresinde, select **gönderme yeni**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-298">From the **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="e1cd0-299">Zaman **betik eylemi Gönder** dikey penceresi görünür, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-299">When the **Submit script action** blade appears, enter the following information:</span></span>

   | <span data-ttu-id="e1cd0-300">Alan</span><span class="sxs-lookup"><span data-stu-id="e1cd0-300">Field</span></span> | <span data-ttu-id="e1cd0-301">Değer</span><span class="sxs-lookup"><span data-stu-id="e1cd0-301">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="e1cd0-302">Ad</span><span class="sxs-lookup"><span data-stu-id="e1cd0-302">Name</span></span> |<span data-ttu-id="e1cd0-303">SSH parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-303">Change ssh password</span></span> |
   | <span data-ttu-id="e1cd0-304">Bash betik URI</span><span class="sxs-lookup"><span data-stu-id="e1cd0-304">Bash script URI</span></span> |<span data-ttu-id="e1cd0-305">Changepassword.sh dosyasına URI</span><span class="sxs-lookup"><span data-stu-id="e1cd0-305">The URI to the changepassword.sh file</span></span> |
   | <span data-ttu-id="e1cd0-306">Düğümler (Head, çalışan, Nimbus, yönetici, Zookeeper, vb.)</span><span class="sxs-lookup"><span data-stu-id="e1cd0-306">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="e1cd0-307">✓ listelenen tüm düğüm türleri</span><span class="sxs-lookup"><span data-stu-id="e1cd0-307">✓ for all node types listed</span></span> |
   | <span data-ttu-id="e1cd0-308">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e1cd0-308">Parameters</span></span> |<span data-ttu-id="e1cd0-309">SSH kullanıcı adı ve yeni parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-309">Enter the SSH user name and then the new password.</span></span> <span data-ttu-id="e1cd0-310">Kullanıcı adı ve parola arasında bir boşluk olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-310">There should be one space between the user name and the password.</span></span> |
   | <span data-ttu-id="e1cd0-311">Bu betik eylemini Sürdür...</span><span class="sxs-lookup"><span data-stu-id="e1cd0-311">Persist this script action ...</span></span> |<span data-ttu-id="e1cd0-312">Bu alan işaretli bırakın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-312">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="e1cd0-313">Seçin **oluşturma** komut dosyasını uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-313">Select **Create** to apply the script.</span></span> <span data-ttu-id="e1cd0-314">Komut dosyası tamamlandıktan sonra yeni bir parola ile SSH kullanarak kümeye bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-314">Once the script finishes, you are able to connect to the cluster using SSH with the new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="e1cd0-315">GRANT/revoke erişim</span><span class="sxs-lookup"><span data-stu-id="e1cd0-315">Grant/revoke access</span></span>
<span data-ttu-id="e1cd0-316">Hdınsight kümeleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki HTTP web hizmetleri vardır:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-316">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="e1cd0-317">ODBC</span><span class="sxs-lookup"><span data-stu-id="e1cd0-317">ODBC</span></span>
* <span data-ttu-id="e1cd0-318">JDBC</span><span class="sxs-lookup"><span data-stu-id="e1cd0-318">JDBC</span></span>
* <span data-ttu-id="e1cd0-319">Ambari</span><span class="sxs-lookup"><span data-stu-id="e1cd0-319">Ambari</span></span>
* <span data-ttu-id="e1cd0-320">Oozie</span><span class="sxs-lookup"><span data-stu-id="e1cd0-320">Oozie</span></span>
* <span data-ttu-id="e1cd0-321">Templeton</span><span class="sxs-lookup"><span data-stu-id="e1cd0-321">Templeton</span></span>

<span data-ttu-id="e1cd0-322">Varsayılan olarak, bu hizmetleri için erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-322">By default, these services are granted for access.</span></span> <span data-ttu-id="e1cd0-323">Revoke/kullanarak erişim ver [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) ve [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-323">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-the-subscription-id"></a><span data-ttu-id="e1cd0-324">Abonelik kimliği bulunamadı</span><span class="sxs-lookup"><span data-stu-id="e1cd0-324">Find the subscription ID</span></span>

<span data-ttu-id="e1cd0-325">**Azure aboneliğiniz kimliklerini bulmak için**</span><span class="sxs-lookup"><span data-stu-id="e1cd0-325">**To find your Azure subscription IDs**</span></span>

1. <span data-ttu-id="e1cd0-326">Oturum [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e1cd0-326">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="e1cd0-327">Tıklatın **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-327">Click **Subscriptions**.</span></span> <span data-ttu-id="e1cd0-328">Her abonelik bir ada ve bir kimliğe sahip</span><span class="sxs-lookup"><span data-stu-id="e1cd0-328">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="e1cd0-329">Her küme bir Azure aboneliğine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-329">Each cluster is tied to an Azure subscription.</span></span> <span data-ttu-id="e1cd0-330">Kimliği kümede gösterilen abonelik **temel** döşeme.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-330">The subscription ID is shown on the cluster **Essential** tile.</span></span> <span data-ttu-id="e1cd0-331">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-331">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="e1cd0-332">Kaynak Grup bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="e1cd0-332">Find the resource group</span></span>
<span data-ttu-id="e1cd0-333">Azure Kaynak Yöneticisi modunda her Hdınsight kümesi içeren bir Azure Resource Manager grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-333">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="e1cd0-334">Bir kümeye ait olduğu kaynak yöneticisi grubu görünür:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-334">The Resource Manager group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="e1cd0-335">Küme listesi olan bir **kaynak grubu** sütun.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-335">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="e1cd0-336">Küme **temel** döşeme.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-336">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="e1cd0-337">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-337">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="e1cd0-338">Varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="e1cd0-338">Find the default storage account</span></span>
<span data-ttu-id="e1cd0-339">Her Hdınsight kümesinde bir varsayılan depolama hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-339">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="e1cd0-340">Varsayılan depolama hesabı ve kendi anahtarları bir küme için görünür altında **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-340">The default storage account and its keys for a cluster appears under **Storage Accounts**.</span></span> <span data-ttu-id="e1cd0-341">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-341">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="e1cd0-342">Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-342">Run Hive queries</span></span>
<span data-ttu-id="e1cd0-343">Doğrudan Azure Portalı'ndan Hive işi çalıştırılamıyor. ancak Ambari Web kullanıcı arabirimini Hive görünümde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-343">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="e1cd0-344">**Ambari Hive görünümünü kullanarak Hive sorguları çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="e1cd0-344">**To run Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="e1cd0-345">Ambari Web Hdınsight küme kullanıcı kimlik bilgilerini kullanarak kullanıcı Arabirimi için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-345">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="e1cd0-346">Varsayılan kullanıcı adı **admin** şeklindedir. URL **https://&lt;Hdınsight küme adı > azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-346">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="e1cd0-347">Aşağıdaki ekran görüntüsünde gösterildiği gibi Hive görünümü açın:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-347">Open Hive View as shown in the following screenshot:</span></span>  

    ![Hdınsight hive görünümü](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. <span data-ttu-id="e1cd0-349">Tıklatın **sorgu** üstteki menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-349">Click **Query** from the top menu.</span></span>
4. <span data-ttu-id="e1cd0-350">Bir Hive sorgusu girin **sorgu Düzenleyicisi'ni**ve ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-350">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="e1cd0-351">İşleri izleme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-351">Monitor jobs</span></span>
<span data-ttu-id="e1cd0-352">Bkz: [Hdınsight kümelerini yönetme Ambari Web kullanıcı arabirimini kullanarak](hdinsight-hadoop-manage-ambari.md#monitoring).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-352">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="e1cd0-353">Gözatma dosyaları</span><span class="sxs-lookup"><span data-stu-id="e1cd0-353">Browse files</span></span>
<span data-ttu-id="e1cd0-354">Azure Portalı'nı kullanarak, varsayılan kapsayıcı içeriğini göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-354">Using the Azure portal, you can browse the content of the default container.</span></span>

1. <span data-ttu-id="e1cd0-355">Oturum [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-355">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1cd0-356">Tıklatın **Hdınsight kümeleri** var olan kümeleri listelemek için sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-356">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="e1cd0-357">Küme adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-357">Click the cluster name.</span></span> <span data-ttu-id="e1cd0-358">Küme listesi uzunsa, sayfanın üst kısmında filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-358">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="e1cd0-359">Tıklatın **depolama hesapları** küme sol menüden.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-359">Click **Storage Accounts** from the cluster left menu.</span></span>
5. <span data-ttu-id="e1cd0-360">Bir depolama hesabı'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-360">Click a Storage account.</span></span>
7. <span data-ttu-id="e1cd0-361">Tıklatın **BLOB'lar** döşeme.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-361">Click the **Blobs** tile.</span></span>
8. <span data-ttu-id="e1cd0-362">Varsayılan kapsayıcı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-362">Click the default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="e1cd0-363">Küme kullanımını izleme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-363">Monitor cluster usage</span></span>
<span data-ttu-id="e1cd0-364">**Kullanım** Hdınsight küme dikey bölümde aboneliğinize Hdınsight ile kullanmak için kullanılabilir çekirdek sayısı gibi bu küme ve bu küme içindeki düğümler için nasıl ayrılacağını ayrılan çekirdek sayısı hakkında bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-364">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="e1cd0-365">Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1cd0-365">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1cd0-366">Hdınsight küme tarafından sağlanan hizmetlerin izlemek için Ambari Web veya Ambari REST API kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-366">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="e1cd0-367">Ambari kullanarak daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="e1cd0-367">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="connect-to-a-cluster"></a><span data-ttu-id="e1cd0-368">Bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="e1cd0-368">Connect to a cluster</span></span>

* [<span data-ttu-id="e1cd0-369">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-369">Use Hive with HDInsight</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="e1cd0-370">HDInsight ile SSH kullanma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-370">Use SSH with HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a><span data-ttu-id="e1cd0-371">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1cd0-371">Next steps</span></span>
<span data-ttu-id="e1cd0-372">Bu makalede, bazı temel daki Hizmetler'i işlevleri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="e1cd0-372">In this article, you have learned some basic administative functions.</span></span> <span data-ttu-id="e1cd0-373">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="e1cd0-373">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="e1cd0-374">Hdınsight Azure PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-374">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="e1cd0-375">Hdınsight Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="e1cd0-375">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="e1cd0-376">Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-376">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="e1cd0-377">Hdınsight'ta Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-377">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e1cd0-378">Hdınsight'ta pig kullanma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-378">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e1cd0-379">Hdınsight'ta Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="e1cd0-379">Use Sqoop in HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="e1cd0-380">Azure Hdınsight kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e1cd0-380">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="e1cd0-381">Azure Hdınsight'ta Hadoop hangi sürümünün mi?</span><span class="sxs-lookup"><span data-stu-id="e1cd0-381">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop komut satırı"
