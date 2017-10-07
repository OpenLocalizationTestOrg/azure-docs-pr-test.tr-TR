---
title: Azure Blob depolama biriminden aaaMove veri tooand | Microsoft Docs
description: "Azure Blob depolama alanından veri tooand Taşı"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="29916-103">Azure Blob depolama alanından veri tooand Taşı</span><span class="sxs-lookup"><span data-stu-id="29916-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="29916-104">Hangi sizin için en iyi bir yöntemdir, senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="29916-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="29916-105">Merhaba [senaryoları Azure Machine Learning, gelişmiş analizler için](machine-learning-data-science-plan-sample-scenarios.md) makale ihtiyacınız analytics işlem Gelişmiş hello kullanılan veri bilimi iş akışları çeşitli hello kaynakları belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="29916-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="29916-106">Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="29916-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="29916-107">Alternatif olarak, kullandığınız [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) için:</span><span class="sxs-lookup"><span data-stu-id="29916-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="29916-108">oluşturun ve veriler Azure blob depolama alanından yükler ardışık zamanlama</span><span class="sxs-lookup"><span data-stu-id="29916-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="29916-109">Bunu iletirsiniz tooa yayımlanan Azure Machine Learning web hizmeti</span><span class="sxs-lookup"><span data-stu-id="29916-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="29916-110">Merhaba Tahmine dayalı analiz sonuçlarını almak ve</span><span class="sxs-lookup"><span data-stu-id="29916-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="29916-111">Merhaba sonuçları toostorage karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="29916-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="29916-112">Daha fazla bilgi için bkz: [Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı işlem hatlarını oluşturmak](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="29916-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29916-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="29916-113">Prerequisites</span></span>
<span data-ttu-id="29916-114">Bu belge, Azure aboneliği bir depolama hesabı ve o hesap için karşılık gelen depolama anahtar hello sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="29916-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="29916-115">Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="29916-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="29916-116">bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29916-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="29916-117">Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="29916-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

