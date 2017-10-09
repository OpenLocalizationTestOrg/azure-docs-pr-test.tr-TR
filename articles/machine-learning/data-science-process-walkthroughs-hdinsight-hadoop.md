---
title: "Azure üzerinde Hive kullanarak aaaHDInsight Hadoop veri bilimi talimatları | Microsoft Docs"
description: "Azure Hdınsight Hadoop toodo Tahmine dayalı analizleri hello Hive kullanarak yol hello takım veri bilimi işlemi örnekler."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="d03ac-103">Hdınsight Hadoop veri bilimi Azure üzerinde Hive kullanarak izlenecek yollar</span><span class="sxs-lookup"><span data-stu-id="d03ac-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="d03ac-104">Bu izlenecek yollar Hdınsight Hadoop bir küme toodo Tahmine dayalı analiz ile Hive kullanma.</span><span class="sxs-lookup"><span data-stu-id="d03ac-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="d03ac-105">Bunlar hello takım veri bilimi işlemi özetlenen hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d03ac-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="d03ac-106">Merhaba takım veri bilimi işlemine genel bakış için bkz: [veri bilimi işlemi](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d03ac-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="d03ac-107">Bir giriş tooAzure Hdınsight için bkz: [giriş tooAzure, Hdınsight Hadoop teknoloji yığınının ve Hadoop kümeleri hello](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d03ac-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="d03ac-108">Merhaba takım veri bilimi işlemi yürütme ek veri bilimi talimatları hello tarafından gruplandırılır **platform** kullandıkları:</span><span class="sxs-lookup"><span data-stu-id="d03ac-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="d03ac-109">Hdınsight Hadoop ile Hive kullanma ücreti ipuçları tahmin etme</span><span class="sxs-lookup"><span data-stu-id="d03ac-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="d03ac-110">Merhaba [kullanım Hdınsight Hadoop kümeleri](machine-learning-data-science-process-hive-walkthrough.md) izlenecek New York taksiler toopredict verilerden kullanır:</span><span class="sxs-lookup"><span data-stu-id="d03ac-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="d03ac-111">Bir ipucu olup Ücretli</span><span class="sxs-lookup"><span data-stu-id="d03ac-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="d03ac-112">İpucu tutarlarının Hello dağıtım</span><span class="sxs-lookup"><span data-stu-id="d03ac-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="d03ac-113">Merhaba senaryo ile Hive kullanarak gerçekleştirilir bir [Azure Hdınsight Hadoop kümesi](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d03ac-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="d03ac-114">Nasıl toostore, keşfetmek, bir genel kullanıma açık NYC ücreti seyahat mühendislik verilerden özellik ve veri kümesi masrafları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d03ac-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="d03ac-115">Ayrıca Azure Machine Learning toobuild kullanabilir ve hello modelleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d03ac-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="d03ac-116">Hdınsight Hadoop ile Hive kullanma reklam tıklatma tahmin etme</span><span class="sxs-lookup"><span data-stu-id="d03ac-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="d03ac-117">Merhaba [kullanım Azure Hdınsight Hadoop kümeleri 1 TB veri kümesi üzerinde](machine-learning-data-science-process-hive-criteo-walkthrough.md) izlenecek kullanan bir genel kullanıma açık [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) bir ipucu ödenen ve hello beklenen tutarlar aralığını olup olmadığını dataset toopredict'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d03ac-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="d03ac-118">Merhaba senaryo ile Hive kullanarak gerçekleştirilir bir [Azure Hdınsight Hadoop kümesi](https://azure.microsoft.com/services/hdinsight/) toostore, keşfetme, özellik mühendislik ve aşağı örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="d03ac-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="d03ac-119">Azure Machine Learning toobuild kullanır, eğitmek ve bir tanıtım bir kullanıcı olup olmadığını tahmin etmeye ikili sınıflandırma modeli Puanlama.</span><span class="sxs-lookup"><span data-stu-id="d03ac-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="d03ac-120">Merhaba izlenecek nasıl toopublish bunlardan birini bir Web hizmeti olarak modeller gösteren sonlanır.</span><span class="sxs-lookup"><span data-stu-id="d03ac-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d03ac-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d03ac-121">Next steps</span></span>

<span data-ttu-id="d03ac-122">Merhaba takım veri bilimi işlemi oluşturan hello anahtar bileşenleri bir tartışma için bkz: [takım veri bilimi işlemine genel bakış](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d03ac-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="d03ac-123">Veri bilimi projelerinizi toostructure kullanabileceğiniz hello takım veri bilimi işlemi yaşam döngüsünün bir tartışma için bkz [takım veri bilimi işlemi yaşam döngüsü](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="d03ac-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="d03ac-124">Merhaba yaşam döngüsü hello adımları, bunlar çalıştırıldığında izleyen projeleri genellikle başlangıç toofinish özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d03ac-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

