---
title: "aaaManage Hadoop kümeleri Azure CLI - Azure Hdınsight kullanma | Microsoft Docs"
description: "Azure Hdınsight'ta nasıl toouse hello Azure komut satırı arabirimi toomanage Hadoop kümeleri hakkında bilgi edinin. Hello Azure CLI, Windows, Mac ve Linux üzerinde çalışır."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="66663-104">Hello Azure CLI kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="66663-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="66663-105">Bilgi nasıl toouse hello [Azure komut satırı arabirimi](../cli-install-nodejs.md) Azure Hdınsight'ta toomanage Hadoop kümeleri.</span><span class="sxs-lookup"><span data-stu-id="66663-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="66663-106">Hello Azure CLI, Node.js içinde uygulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="66663-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="66663-107">Windows, Mac ve Linux da dahil olmak üzere, Node.js'yi destekleyen herhangi bir platformda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66663-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="66663-108">Bu makalede, yalnızca Hdınsight ile hello Azure CLI kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="66663-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="66663-109">Nasıl genel bir kılavuz için toouse Azure CLI bkz [yükleyin ve Azure CLI yapılandırma][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="66663-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="66663-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66663-110">Prerequisites</span></span>
<span data-ttu-id="66663-111">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="66663-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="66663-112">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="66663-112">**An Azure subscription**.</span></span> <span data-ttu-id="66663-113">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="66663-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="66663-114">**Azure CLI** -bkz [yükleme ve yapılandırma hello Azure CLI](../cli-install-nodejs.md) yükleme ve yapılandırma bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="66663-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="66663-115">**TooAzure bağlanmak**kullanarak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="66663-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="66663-116">Bir iş veya Okul hesabı kullanarak kimlik doğrulaması ile ilgili daha fazla bilgi için bkz: [tooan Azure aboneliği hello Azure CLI ' bağlanma](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="66663-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="66663-117">**Anahtar toohello Azure Resource Manager moduna**kullanarak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="66663-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="66663-118">tooget Yardımını kullanma hello **-h** geçin.</span><span class="sxs-lookup"><span data-stu-id="66663-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="66663-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="66663-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="66663-120">CLI hello ile kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="66663-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="66663-121">Bkz: [kullanarak Hdınsight'ta oluşturma kümeleri hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="66663-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="66663-122">Liste ve küme ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="66663-122">List and show cluster details</span></span>
<span data-ttu-id="66663-123">Aşağıdaki komutları toolist hello kullanın ve küme ayrıntıları göster:</span><span class="sxs-lookup"><span data-stu-id="66663-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="66663-124">![Komut satırı görünümünü küme listesi][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="66663-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="66663-125">Küme silme</span><span class="sxs-lookup"><span data-stu-id="66663-125">Delete clusters</span></span>
<span data-ttu-id="66663-126">Komut toodelete bir küme aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="66663-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="66663-127">Bir küme hello küme içeren hello kaynak grubunu silerek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66663-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="66663-128">Lütfen unutmayın, bu hello varsayılan depolama hesabı dahil olmak üzere hello grubundaki tüm hello kaynaklarını siler.</span><span class="sxs-lookup"><span data-stu-id="66663-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="66663-129">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="66663-129">Scale clusters</span></span>
<span data-ttu-id="66663-130">toochange hello Hadoop küme boyutu:</span><span class="sxs-lookup"><span data-stu-id="66663-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="66663-131">Bir küme için HTTP erişimi etkinleştir/devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="66663-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="66663-132">Bir küme için RDP erişimini etkinleştir/devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="66663-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="66663-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66663-133">Next steps</span></span>
<span data-ttu-id="66663-134">Bu makalede, öğrendiğiniz nasıl tooperform farklı Hdınsight küme yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="66663-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="66663-135">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="66663-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="66663-136">[Hdınsight hello Azure Portal kullanarak yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="66663-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="66663-137">[Hdınsight Azure PowerShell kullanarak yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="66663-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="66663-138">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="66663-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="66663-139">[Nasıl toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="66663-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Liste ve kümeleri Göster"
