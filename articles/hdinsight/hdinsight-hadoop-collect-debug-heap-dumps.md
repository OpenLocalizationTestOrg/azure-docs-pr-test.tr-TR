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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Blob Depolama toodebug içinde yığın dökümleri toplama ve Hadoop Hizmetleri Çözümle
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Yığın dökümleri hello döküm oluşturuldu hello zamanında değişkenlerin hello değerleri dahil olmak üzere hello uygulamanın belleğin anlık görüntüsünü içerir. Bu nedenle bunlar çalışma zamanında oluşan sorunları tanılamak için kullanışlıdır. Yığın dökümleri kullanılabilir otomatik olarak Hadoop Hizmetleri için toplanan ve hello Azure Blob Depolama hesabı, bir kullanıcının HDInsightHeapDumps altında içine yerleştirilen /.

Merhaba koleksiyonu yığın dökümleri çeşitli hizmetler için ayrı ayrı kümelerde Hizmetleri için etkinleştirilmesi gerekir. Bu özellik için Hello varsayılan toobe bir küme için kapalıdır. Merhaba koleksiyonu etkinleştirildikten sonra bunlar kaydedildiği önerilir toomonitor hello Blob storage hesabı olacak şekilde bu yığın dökümleri büyük olabilir.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Bu makaledeki Hello bilgiler yalnızca tooWindows tabanlı Hdınsight geçerlidir. Linux tabanlı Hdınsight hakkında daha fazla bilgi için bkz: [etkinleştir yığın dökümleri Linux tabanlı hdınsight'ta Hadoop Hizmetleri için](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Uygun hizmetler için yığın dökümleri
Yığın dökümleri Hizmetleri aşağıdaki hello için etkinleştirebilirsiniz:

* **hcatalog** -tempelton
* **Hive** -hiveserver2, meta depo, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager, nodemanager, timelineserver
* **hdfs** -datanode, secondarynamenode, iş

## <a name="configuration-elements-that-enable-heap-dumps"></a>Yığın dökümleri etkinleştirmek yapılandırma öğeleri
tooturn bir hizmet için yığın dökümleri üzerinde ihtiyacınız hello bölümünde tooset hello uygun yapılandırma öğeleri tarafından belirtilen bu hizmet için **servıce_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Merhaba değerini **servıce_name** burada listelenen hello hizmetlerinden herhangi biri olabilir: tempelton, hiveserver2 meta depo, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, veya İş.

## <a name="enable-using-azure-powershell"></a>Azure PowerShell kullanarak etkinleştirme
Örneğin, tooturn jobhistoryserver için Azure PowerShell kullanarak yığın dökümleri üzerinde komut dosyası izleyen hello kullanabilirsiniz:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>.NET SDK kullanarak etkinleştirin
Örneğin, tooturn için jobhistoryserver hello Azure Hdınsight .NET SDK kullanarak yığın dökümleri üzerinde hello aşağıdaki kodu kullanabilirsiniz:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
