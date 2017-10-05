---
title: "Hive ve Hadoop - Azure Hdınsight kullanarak algılayıcı verilerini çözümleme | Microsoft Docs"
description: "Hive sorgusu konsol Hdınsight (Hadoop) kullanarak algılayıcı verilerini çözümlemeyi öğrenin ve ardından PowerView ile Microsoft Excel verilerini görselleştirin."
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
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="85336-103">Hdınsight'ta Hadoop Hive sorgusu Konsolu kullanarak algılayıcı verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="85336-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="85336-104">Hive sorgusu konsol Hdınsight (Hadoop) kullanarak algılayıcı verilerini çözümlemeyi öğrenin ve Power View'ı kullanarak Microsoft Excel verilerini görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="85336-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85336-105">Bu belgede yer alan adımlar, yalnızca Windows tabanlı Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="85336-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="85336-106">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="85336-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="85336-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="85336-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="85336-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="85336-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="85336-109">Bu örnekte, Hive geçmiş verileri işlemek ve ısıtma sistemleriyle sorunlarını belirlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="85336-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="85336-110">Özellikle, sistemleri belirlemek aşağıdaki görevleri gerçekleştirerek ayarlı sıcaklığı güvenilir bir şekilde korumak mümkün değildir:</span><span class="sxs-lookup"><span data-stu-id="85336-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="85336-111">HIVE tablolarını virgülle ayrılmış değer (CSV) dosyasında depolanan verileri sorgulayamadı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85336-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="85336-112">Verileri çözümlemek için HIVE sorguları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85336-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="85336-113">Çözümlenen verileri almak üzere Hdınsight'a bağlanmak için Microsoft Excel kullanın.</span><span class="sxs-lookup"><span data-stu-id="85336-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="85336-114">Verileri görselleştirmek için Power View'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="85336-114">To visualize the data, use Power View.</span></span>

![Çözüm mimarisi diyagramı](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="85336-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85336-116">Prerequisites</span></span>

* <span data-ttu-id="85336-117">Hdınsight (Hadoop) kümesi: bkz [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md) bir küme oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="85336-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="85336-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="85336-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="85336-119">Microsoft Excel ile verileri görselleştirme için kullanıldığından [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="85336-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="85336-120">Microsoft Hive ODBC sürücüsü</span><span class="sxs-lookup"><span data-stu-id="85336-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="85336-121">Örneği çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="85336-121">To run the sample</span></span>

1. <span data-ttu-id="85336-122">Web tarayıcınızdan aşağıdaki URL'sine gidin:</span><span class="sxs-lookup"><span data-stu-id="85336-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="85336-123">`<clustername>` değerini HDInsight kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85336-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="85336-124">İstendiğinde, yönetici kullanıcı adını ve bu küme hazırlama sırasında kullanılan parola kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="85336-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="85336-125">Web açan sayfasından tıklatın **alma başlatıldı galeri** sekmesi ve ardından **örnek verilerle çözümleri** kategorisi, tıklatın **algılayıcı verilerini çözümleme** örnek.</span><span class="sxs-lookup"><span data-stu-id="85336-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Başlatılan galeri görüntüsü alma](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="85336-127">Örnek tamamlamak için web sayfasında sağlanan yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="85336-127">Follow the instructions provided on the web page to finish the sample.</span></span>
