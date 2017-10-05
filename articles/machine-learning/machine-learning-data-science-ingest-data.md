---
title: "Analiz için Azure depolama ortamlara veri yükleme | Microsoft Docs"
description: "Azure Blob Depolamadan/Depolamaya Veri Taşıma"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="c6b61-103">Analiz için depolama ortamlarına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="c6b61-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="c6b61-104">Takım veri bilimi işlemi veri veya alınan işlenen ya da işlemin her aşamasında en uygun şekilde analiz için farklı depolama ortamları çeşitli yüklenen olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c6b61-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="c6b61-105">İşleme için yaygın olarak kullanılan veri hedefleri Azure Blob Storage, SQL Azure veritabanının SQL Server Azure VM, Hdınsight (Hadoop) ve Azure Machine Learning içerir.</span><span class="sxs-lookup"><span data-stu-id="c6b61-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="c6b61-106">Bu **menü** bunları veri alma nasıl açıklayan konulara bağlantılar hedef burada veri depolanabilir ve işlenebilir ortamları.</span><span class="sxs-lookup"><span data-stu-id="c6b61-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="c6b61-107">Teknik ve iş gereksinimlerinize yanı sıra, ilk konum biçimlendirin ve içine veri çözümleme hedeflerinize ulaşmak için alınan gerekiyor hedef ortamları verilerinizi boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="c6b61-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="c6b61-108">Tahmine dayalı bir modeli oluşturmak için gereken görevler çeşitli elde etmek için çeşitli ortamlar arasında taşınacak veri gerektirecek şekilde bir senaryo için seyrek değil.</span><span class="sxs-lookup"><span data-stu-id="c6b61-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="c6b61-109">Bu görev dizisi, örneğin, veri keşfi, ön işleme, temizleme, aşağı örnekleme ve model eğitim içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c6b61-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

