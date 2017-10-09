---
title: "aaaLoad veri analizi için Azure depolama ortamlara | Microsoft Docs"
description: "Azure Blob depolama alanından veri tooand Taşı"
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
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="55969-103">Analiz için depolama ortamlarına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="55969-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="55969-104">Merhaba takım veri bilimi işlemi veri veya alınan işlenen veya hello en uygun şekilde hello işleminin her aşamada analiz farklı depolama ortamları toobe çeşitli yüklenen olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="55969-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="55969-105">İşleme için yaygın olarak kullanılan veri hedefleri Azure Blob Storage, SQL Azure veritabanının SQL Server Azure VM, Hdınsight (Hadoop) ve Azure Machine Learning içerir.</span><span class="sxs-lookup"><span data-stu-id="55969-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="55969-106">Bu **menü** burada hello veri depolanabilir ve işlenebilir ortamları nasıl hedef tooingest verileri bu açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="55969-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="55969-107">Teknik ve iş gereksinimlerinize yanı sıra, hello ilk konum, biçimlendirme ve hangi hello veri alınan toobe tooachieve hello hedefleri çözümleme gereken hello hedef ortamları verilerinizi boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="55969-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="55969-108">Çeşitli ortamlar tooachieve hello çeşitli görevleri gerekli tooconstruct Tahmine dayalı bir model arasında taşınan bir senaryo toorequire veri toobe seyrek değil.</span><span class="sxs-lookup"><span data-stu-id="55969-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="55969-109">Bu görev dizisi, örneğin, veri keşfi, ön işleme, temizleme, aşağı örnekleme ve model eğitim içerebilir.</span><span class="sxs-lookup"><span data-stu-id="55969-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

