---
title: "aaaUse etkileşimli Hive hdınsight'ta - Azure | Microsoft Docs"
description: "Bilgi nasıl toouse etkileşimli (Hive LLAP üzerinde) hdınsight'ta Hive."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>(Önizleme) hdınsight'ta etkileşimli Hive kullanma
Etkileşimli (paketini yığını [Canlı uzun ve işlem](https://cwiki.apache.org/confluence/display/Hive/LLAP)) yeni bir Hdınsight olan [küme türü](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).  Etkileşimli Hive bellek çok daha etkileşimli ve daha hızlı Hive sorgularını yapan önbelleğe alma de sağlar. Bu yeni özellik Hdınsight hello birini dünyanın çoğu kullanıcı, esnek ve açık büyük veri çözümleri hello buluttaki (Hive ve Spark kullanarak) bellek içi önbellek ile yapar ve Gelişmiş analitikler R hizmetleriyle derin tümleştirme aracılığıyla. 

Merhaba etkileşimli Hive küme hello Hadoop kümeden farklıdır. Yalnızca hello Hive hizmeti de içerir. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie ve diğer hizmetler bu küme türü ile yakında kaldırılır.
> Merhaba hello etkileşimli Hive küme Hive hizmetinde yalnızca hello Ambari Hive görünümünü, Beeline ve Hive ODBC erişilebilir. Hive konsol, Templeton, Azure CLI ve Azure PowerShell erişilemiyor. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Etkileşimli Hive kümesi oluşturma
Etkileşimli Hive küme yalnızca Linux tabanlı kümelerde desteklenir. Hdınsight kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Etkileşimli kovanından Hive yürütme
Vardır farklı Hive sorguları nasıl yürütebilir seçenekleri:

* Merhaba Ambari Hive görünümünü kullanarak Hive çalıştırın
  
    Merhaba bilgi hello Hive görünümü kullanma hakkında bkz [kullanım hello hdınsight'ta Hadoop ile Hive görünümü](hdinsight-hadoop-use-hive-ambari-view.md).
* Hive Beeline kullanarak çalıştırma
  
    Beeline kullanarak hello hakkında bilgi için bkz: [Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md).
  
    Beeline hello headnode veya boş kenar düğümünü kullanın.  Bir boş kenar düğümden Beeline kullanılması önerilir.  Boş bir edgenode ile Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).
* Hive ODBC kullanarak Hive çalıştırın
  
    Hive ODBC kullanarak hello hakkında bilgi için bkz: [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md).

**toofind hello JDBC bağlantı dizesi:**

1. Üzerinde tooAmbari URL aşağıdaki hello kullanarak oturum açın: https://<ClusterName>. AzureHDInsight.net.
2. Tıklatın **Hive** hello sol menüden.
3. Vurgulanan hello simgesi toocopy hello URL'yi tıklatın:
   
   ![Hdınsight Hadoop etkileşimli Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Ayrıca bkz.
* [Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight'ta nasıl toocreate etkileşimli Hive kümeleri öğrenin.
* [Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md): öğrenin nasıl toouse Beeline toosubmit Hive sorguları.
* [Excel tooHadoop hello Microsoft Hive ODBC sürücüsü ile bağlantı](hdinsight-connect-excel-hive-odbc-driver.md): öğrenin nasıl tooconnect Excel tooHive.

