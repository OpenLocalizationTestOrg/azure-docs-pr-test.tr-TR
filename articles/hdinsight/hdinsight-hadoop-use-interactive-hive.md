---
title: "Hdınsight'ta - Azure etkileşimli Hive kullanma | Microsoft Docs"
description: "Etkileşimli Hive (Hive LLAP üzerinde) kullanmak Hdınsight'ta öğrenin."
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
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>(Önizleme) hdınsight'ta etkileşimli Hive kullanma
Etkileşimli (paketini yığını [Canlı uzun ve işlem](https://cwiki.apache.org/confluence/display/Hive/LLAP)) yeni bir Hdınsight olan [küme türü](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).  Etkileşimli Hive bellek çok daha etkileşimli ve daha hızlı Hive sorgularını yapan önbelleğe alma de sağlar. Bu yeni özellik dünyanın, Hdınsight (Hive ve Spark kullanarak) bellek içi önbellek ile çoğu kullanıcı, esnek ve açık büyük veri çözümlerini bulut sağlar ve Gelişmiş analitikler R hizmetleriyle derin tümleştirme aracılığıyla. 

Etkileşimli Hive küme Hadoop küme farklıdır. Yalnızca Hive hizmeti de içerir. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie ve diğer hizmetler bu küme türü ile yakında kaldırılır.
> Etkileşimli Hive küme Hive hizmetinde yalnızca Ambari Hive görünümü, Beeline ve Hive ODBC erişilebilir. Hive konsol, Templeton, Azure CLI ve Azure PowerShell erişilemiyor. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Etkileşimli Hive kümesi oluşturma
Etkileşimli Hive küme yalnızca Linux tabanlı kümelerde desteklenir. Hdınsight kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Etkileşimli kovanından Hive yürütme
Vardır farklı Hive sorguları nasıl yürütebilir seçenekleri:

* Ambari Hive görünümünü kullanarak Hive çalıştırın
  
    Hive görünümünü kullanma hakkında bilgi için bkz: [hdınsight'ta Hadoop ile Hive görünümünü kullanın](hdinsight-hadoop-use-hive-ambari-view.md).
* Hive Beeline kullanarak çalıştırma
  
    Hdınsight üzerinde Beeline kullanma hakkında bilgi için bkz: [Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md).
  
    Beeline headnode veya boş kenar düğümünü kullanın.  Bir boş kenar düğümden Beeline kullanılması önerilir.  Boş bir edgenode ile Hdınsight kümesi oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).
* Hive ODBC kullanarak Hive çalıştırın
  
    Hive ODBC kullanma hakkında bilgi için bkz: [bağlanmak Excel için Microsoft Hive ODBC sürücüsü ile hadoop'a](hdinsight-connect-excel-hive-odbc-driver.md).

**JDBC bağlantı dizesi bulmak için:**

1. Aşağıdaki URL'yi kullanarak ambarı'na oturum açma: https://<ClusterName>. AzureHDInsight.net.
2. Tıklatın **Hive** sol menüden.
3. URL'yi kopyalamak için vurgulanan simgesine tıklayın:
   
   ![Hdınsight Hadoop etkileşimli Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Ayrıca bkz.
* [Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight'ta etkileşimli Hive kümeleri oluşturmayı öğrenin.
* [Beeline ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md): Beeline Hive sorguları göndermek için nasıl kullanılacağını öğrenin.
* [Excel'i Microsoft Hive ODBC sürücüsü ile Hadoop için bağlama](hdinsight-connect-excel-hive-odbc-driver.md): Excel kovana bağlamayı öğrenin.

