---
title: "aaaDebug ve Hadoop Hizmetleri yığın dökümleri - Azure ile çözümleme | Microsoft Docs"
description: "Otomatik olarak yığın dökümleri Hadoop Hizmetleri için toplamak ve hello hata ayıklama ve analiz için Azure Blob Depolama hesabı içine yerleştirin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="39c03-103">Blob Depolama toodebug içinde yığın dökümleri toplama ve Hadoop Hizmetleri Çözümle</span><span class="sxs-lookup"><span data-stu-id="39c03-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="39c03-104">Yığın dökümleri hello döküm oluşturuldu hello zamanında değişkenlerin hello değerleri dahil olmak üzere hello uygulamanın belleğin anlık görüntüsünü içerir.</span><span class="sxs-lookup"><span data-stu-id="39c03-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="39c03-105">Bu nedenle bunlar çalışma zamanında oluşan sorunları tanılamak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="39c03-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="39c03-106">Yığın dökümleri kullanılabilir otomatik olarak Hadoop Hizmetleri için toplanan ve hello Azure Blob Depolama hesabı, bir kullanıcının HDInsightHeapDumps altında içine yerleştirilen /.</span><span class="sxs-lookup"><span data-stu-id="39c03-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="39c03-107">Merhaba koleksiyonu yığın dökümleri çeşitli hizmetler için ayrı ayrı kümelerde Hizmetleri için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="39c03-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="39c03-108">Bu özellik için Hello varsayılan toobe bir küme için kapalıdır.</span><span class="sxs-lookup"><span data-stu-id="39c03-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="39c03-109">Merhaba koleksiyonu etkinleştirildikten sonra bunlar kaydedildiği önerilir toomonitor hello Blob storage hesabı olacak şekilde bu yığın dökümleri büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="39c03-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39c03-110">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="39c03-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="39c03-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="39c03-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="39c03-112">Bu makaledeki Hello bilgiler yalnızca tooWindows tabanlı Hdınsight geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="39c03-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="39c03-113">Linux tabanlı Hdınsight hakkında daha fazla bilgi için bkz: [etkinleştir yığın dökümleri Linux tabanlı hdınsight'ta Hadoop Hizmetleri için](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="39c03-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="39c03-114">Uygun hizmetler için yığın dökümleri</span><span class="sxs-lookup"><span data-stu-id="39c03-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="39c03-115">Yığın dökümleri Hizmetleri aşağıdaki hello için etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39c03-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="39c03-116">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="39c03-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="39c03-117">**Hive** -hiveserver2, meta depo, derbyserver</span><span class="sxs-lookup"><span data-stu-id="39c03-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="39c03-118">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="39c03-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="39c03-119">**yarn** -resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="39c03-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="39c03-120">**hdfs** -datanode, secondarynamenode, iş</span><span class="sxs-lookup"><span data-stu-id="39c03-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="39c03-121">Yığın dökümleri etkinleştirmek yapılandırma öğeleri</span><span class="sxs-lookup"><span data-stu-id="39c03-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="39c03-122">tooturn bir hizmet için yığın dökümleri üzerinde ihtiyacınız hello bölümünde tooset hello uygun yapılandırma öğeleri tarafından belirtilen bu hizmet için **servıce_name**.</span><span class="sxs-lookup"><span data-stu-id="39c03-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="39c03-123">Merhaba değerini **servıce_name** burada listelenen hello hizmetlerinden herhangi biri olabilir: tempelton, hiveserver2 meta depo, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, veya İş.</span><span class="sxs-lookup"><span data-stu-id="39c03-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="39c03-124">Azure PowerShell kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="39c03-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="39c03-125">Örneğin, tooturn jobhistoryserver için Azure PowerShell kullanarak yığın dökümleri üzerinde komut dosyası izleyen hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39c03-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="39c03-126">.NET SDK kullanarak etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="39c03-126">Enable using .NET SDK</span></span>
<span data-ttu-id="39c03-127">Örneğin, tooturn için jobhistoryserver hello Azure Hdınsight .NET SDK kullanarak yığın dökümleri üzerinde hello aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39c03-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
