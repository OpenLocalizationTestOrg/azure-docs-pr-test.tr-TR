---
title: "aaaHow toodelete Hdınsight kümesi - Azure | Microsoft Docs"
description: "Merhaba Hdınsight kümesi silebilmek için çeşitli yollar hakkında bilgiler."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="41dd5-103">Tarayıcı, PowerShell veya hello Azure CLI kullanarak bir Hdınsight kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="41dd5-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="41dd5-104">Hdınsight küme faturalandırma bir küme oluşturulur ve hello küme silindiğinde durdurur sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="41dd5-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="41dd5-105">Artık kullanımda olmadığında, küme her zaman silmelisiniz Faturalaması dakika başına Faturalaması olduğundan.</span><span class="sxs-lookup"><span data-stu-id="41dd5-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="41dd5-106">Bu belgede, kullanarak bir küme toodelete nasıl hello Azure portalı, Azure PowerShell ve Azure CLI 1.0 hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41dd5-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41dd5-107">Bir Hdınsight kümesi siliniyor hello Azure depolama hesapları silmez veya Data Lake Store hello kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="41dd5-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="41dd5-108">Bu hizmetlerin gelecekteki hello içinde depolanan verileri yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41dd5-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="41dd5-109">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="41dd5-109">Azure portal</span></span>

1. <span data-ttu-id="41dd5-110">İçinde toohello oturum [Azure portal](https://portal.azure.com) ve Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="41dd5-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="41dd5-111">Hdınsight kümenize sabitlenmiş toohello Pano değilse, bunun için hello arama alanı kullanarak ada göre arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41dd5-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![Portal arama](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="41dd5-113">Merhaba küme için Hello dikey pencere açılır sonra hello seçeneğini **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="41dd5-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="41dd5-114">İstendiğinde, seçin **Evet** toodelete hello küme.</span><span class="sxs-lookup"><span data-stu-id="41dd5-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![Sil simgesi](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="41dd5-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41dd5-116">Azure PowerShell</span></span>

<span data-ttu-id="41dd5-117">Bir PowerShell isteminden komutu toodelete hello küme aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41dd5-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="41dd5-118">Değiştir **CLUSTERNAME** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="41dd5-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="41dd5-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="41dd5-119">Azure CLI 1.0</span></span>

<span data-ttu-id="41dd5-120">Bir isteminden toodelete hello küme aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41dd5-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="41dd5-121">Değiştir **CLUSTERNAME** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="41dd5-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="41dd5-122">Azure CLI 2.0 silme Hdınsight kümeleri şu anda (31 Temmuz 2017) desteklemez.</span><span class="sxs-lookup"><span data-stu-id="41dd5-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>