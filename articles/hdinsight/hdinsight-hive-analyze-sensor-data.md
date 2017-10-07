---
title: "Hive ve Hadoop - Azure Hdınsight kullanarak aaaAnalyze algılayıcı verilerini | Microsoft Docs"
description: "Hive sorgusu Konsolu Hdınsight (Hadoop) ile kullanarak tooanalyze algılayıcı verilerini nasıl hello öğrenin ve ardından PowerView ile Microsoft Excel'i hello verileri görselleştirmek."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="a9b57-103">Hdınsight'ta Hadoop Hive sorgusu konsol Hello kullanarak algılayıcı verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="a9b57-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="a9b57-104">Tooanalyze algılayıcı verilerini kullanarak Hive sorgusu Konsolu Hdınsight (Hadoop) ile nasıl hello öğrenin ve ardından hello Microsoft Excel'de Power View kullanarak görselleştirmek.</span><span class="sxs-lookup"><span data-stu-id="a9b57-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9b57-105">Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları.</span><span class="sxs-lookup"><span data-stu-id="a9b57-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a9b57-106">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a9b57-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="a9b57-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="a9b57-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a9b57-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a9b57-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="a9b57-109">Bu örnekte, Hive tooprocess geçmiş verileri kullanın ve sorunları ısıtma sistemleriyle tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="a9b57-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="a9b57-110">Özellikle, sistemleri belirlemek olan erişilemiyor tooreliably korumak ayarlı sıcaklığı hello aşağıdaki görevleri gerçekleştirerek:</span><span class="sxs-lookup"><span data-stu-id="a9b57-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="a9b57-111">Oluşturma HIVE tabloları tooquery verileri virgülle ayrılmış değer (CSV) dosyalarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="a9b57-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="a9b57-112">HIVE sorguları tooanalyze hello veri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9b57-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="a9b57-113">tooretrieve analiz hello veriler, Microsoft Excel tooconnect tooHDInsight kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9b57-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="a9b57-114">toovisualize hello verileri, Power View kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9b57-114">toovisualize hello data, use Power View.</span></span>

![Merhaba çözüm mimarisi diyagramı](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="a9b57-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9b57-116">Prerequisites</span></span>

* <span data-ttu-id="a9b57-117">Hdınsight (Hadoop) kümesi: bkz [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md) bir küme oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a9b57-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="a9b57-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="a9b57-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="a9b57-119">Microsoft Excel ile verileri görselleştirme için kullanıldığından [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="a9b57-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="a9b57-120">Microsoft Hive ODBC sürücüsü</span><span class="sxs-lookup"><span data-stu-id="a9b57-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="a9b57-121">toorun hello örnek</span><span class="sxs-lookup"><span data-stu-id="a9b57-121">toorun hello sample</span></span>

1. <span data-ttu-id="a9b57-122">Web tarayıcınızdan URL aşağıdaki toohello gidin:</span><span class="sxs-lookup"><span data-stu-id="a9b57-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="a9b57-123">Değiştir `<clustername>` Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="a9b57-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="a9b57-124">İstendiğinde, hello yönetici kullanıcı adını ve bu küme hazırlama sırasında kullanılan parola kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="a9b57-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="a9b57-125">Hello web açan sayfasından hello tıklatın **alma başlatıldı galeri** sekmesinde hello altında ve **çözümleri örnek verilerle** kategorisi, hello tıklatın **algılayıcı verilerini çözümleme** örnek.</span><span class="sxs-lookup"><span data-stu-id="a9b57-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Başlatılan galeri görüntüsü alma](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="a9b57-127">Merhaba web sayfası toofinish hello örnek üzerinde sağlanan hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a9b57-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
