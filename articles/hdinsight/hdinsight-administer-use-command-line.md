---
title: "Azure CLI - Azure Hdınsight kullanarak Hadoop kümelerini yönetme | Microsoft Docs"
description: "Azure hdınsight'ta Hadoop kümelerini yönetmek için Azure komut satırı arabirimi kullanmayı öğrenin. Azure CLI, Windows, Mac ve Linux üzerinde çalışır."
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
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="b91da-104">Azure CLI kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="b91da-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="b91da-105">Nasıl kullanacağınızı öğrenin [Azure komut satırı arabirimi](../cli-install-nodejs.md) Azure hdınsight'ta Hadoop kümelerini yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="b91da-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="b91da-106">Azure CLI, Node.js içinde uygulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b91da-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="b91da-107">Windows, Mac ve Linux da dahil olmak üzere, Node.js'yi destekleyen herhangi bir platformda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b91da-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="b91da-108">Bu makalede, yalnızca Hdınsight ile Azure CLI kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b91da-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="b91da-109">Azure CLI kullanma hakkında genel bir kılavuz için bkz: [yükleyin ve Azure CLI yapılandırma][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="b91da-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="b91da-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b91da-110">Prerequisites</span></span>
<span data-ttu-id="b91da-111">Bu makaleye başlamadan önce aşağıdakilere sahip olmanız ve aşağıdaki işlemleri yapmış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b91da-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="b91da-112">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="b91da-112">**An Azure subscription**.</span></span> <span data-ttu-id="b91da-113">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b91da-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b91da-114">**Azure CLI** - Yükleme ve yapılandırma bilgileri için bkz. [Azure CLI'yı yükleme ve yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b91da-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="b91da-115">**Azure'a bağlanmak**, aşağıdaki komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="b91da-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="b91da-116">Bir iş veya okul hesabı kullanarak kimlik doğrulama gerçekleştirme konusunda daha fazla bilgi için bkz. [Azure CLI'dan Azure aboneliğine bağlanma](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b91da-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="b91da-117">Şu komutu kullanarak **Azure Resource Manager moduna geçin**:</span><span class="sxs-lookup"><span data-stu-id="b91da-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="b91da-118">Yardım almak için kullanmak **-h** geçin.</span><span class="sxs-lookup"><span data-stu-id="b91da-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="b91da-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b91da-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="b91da-120">CLI ile kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91da-120">Create clusters with the CLI</span></span>
<span data-ttu-id="b91da-121">Bkz: [Azure CLI kullanarak Hdınsight'ta kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b91da-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="b91da-122">Liste ve küme ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="b91da-122">List and show cluster details</span></span>
<span data-ttu-id="b91da-123">Liste ve küme ayrıntıları görüntülemek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b91da-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="b91da-124">![Komut satırı görünümünü küme listesi][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="b91da-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="b91da-125">Küme silme</span><span class="sxs-lookup"><span data-stu-id="b91da-125">Delete clusters</span></span>
<span data-ttu-id="b91da-126">Bir küme silmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b91da-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="b91da-127">Ayrıca, küme içeren kaynak grubunu silerek bir küme silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91da-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="b91da-128">Lütfen unutmayın, bu varsayılan depolama hesabı dahil olmak üzere gruptaki tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="b91da-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="b91da-129">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b91da-129">Scale clusters</span></span>
<span data-ttu-id="b91da-130">Hadoop küme boyutunu değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="b91da-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="b91da-131">Bir küme için HTTP erişimi etkinleştir/devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="b91da-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="b91da-132">Bir küme için RDP erişimini etkinleştir/devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="b91da-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="b91da-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b91da-133">Next steps</span></span>
<span data-ttu-id="b91da-134">Bu makalede, farklı Hdınsight küme yönetim görevlerini gerçekleştirmek öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b91da-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="b91da-135">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="b91da-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="b91da-136">[Hdınsight Azure Portalı'nı kullanarak yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="b91da-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="b91da-137">[Hdınsight Azure PowerShell kullanarak yönetme][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="b91da-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="b91da-138">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b91da-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="b91da-139">[Azure CLI kullanma][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="b91da-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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
