---
title: "Hadoop mimarisi - Azure Hdınsight | Microsoft Docs"
description: "Hadoop depolama ve işleme Hdınsight kümelerinde açıklar."
services: hdinsight
documentationcenter: 
author: ashishthaps
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/19/2018
ms.author: ashishth
ms.openlocfilehash: 85383cc32e67db1f7e6964dc0b55bf3977311d40
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2018
---
# <a name="hadoop-architecture-in-hdinsight"></a>Hdınsight'ta Hadoop mimarisi

Hadoop iki çekirdek bileşeni, yüksek yoğunluk dosya sistemi (depolama sağlayan HDFS) ve henüz başka bir kaynak Uzlaştırıcı (işleme sağlayan YARN) içerir. Depolama ve işleme özelliklerini bir küme istenen veri işleme gerçekleştirmek için MapReduce programları çalıştırabilen haline gelir.

> [!NOTE]
> Bir HDFS genellikle depolama sağlamak için Hdınsight küme içinde dağıtılır. Bunun yerine, bir HDFS uyumlu arabirim katmanı Hadoop bileşenleri tarafından kullanılır. Gerçek depolama yeteneği, Azure Storage veya Azure Data Lake Store tarafından sağlanır. Hadoop, Hdınsight kümesinde yürütme MapReduce işleri bir HDFS mevcut değilmiş gibi çalıştırın ve bu nedenle depolama ihtiyaçlarını desteklemek için herhangi bir değişiklik gerektirir. Hdınsight'ta Hadoop, depolama dış kaynaklı ancak çekirdek bileşen YARN işleme kalır. 

<!--   As described in [HDInsight architecture](hdinsight-architecture.md)  -->

Bu makalede YARN ve nasıl Hdınsight uygulamalarının yürütme koordinatları tanıtır.

## <a name="yarn-basics"></a>YARN temelleri 

YARN yönetir ve Hadoop veri işlemeye yönetir. YARN kümedeki düğümlere işlemleri olarak çalışan iki çekirdek hizmetler şunlardır: 

* ResourceManager 
* NodeManager

ResourceManager MapReduce işleri gibi uygulamalar için küme işlem kaynakları verir. ResourceManager bu kaynakların nerede her kapsayıcı CPU çekirdekleri ve RAM bellek ayırma oluşur kapsayıcılar olarak verir. Bir kümede kullanılabilir tüm kaynakları birleştirilmiş ve bunları belirli sayıda çekirdek ve bellek bloklarını dağıtılmış, her bir bloğunda kaynakları bir kapsayıcıdır. Kümedeki her düğümde belirli bir sayıda kapsayıcı için bir kapasite, ve bu nedenle küme kapsayıcıları kullanılabilir sayısına sabit bir sınıra sahiptir. Bir kapsayıcıda kaynakların ayırmayı yapılandırılabilir. 

Bir MapReduce uygulaması bir kümede çalıştığında, ResourceManager uygulama yürütmek kapsayıcı sağlar. ResourceManager çalışan uygulamalar, kullanılabilir küme kapasite durumunu izler ve bunlar tam olarak uygulamaları izler ve kaynaklarını serbest bırakın. 

ResourceManager uygulamaların durumunu izlemek için kullanabileceğiniz bir web kullanıcı arabirimi sağlayan bir web sunucusu işlemi de çalışır. 

Bir kullanıcı bir MapReduce uygulamayı, küme üzerinde çalıştırmak için gönderdiğinde, uygulama için ResourceManager gönderilir. Buna karşılık, bir kapsayıcı kullanılabilir NodeManager düğümlerde ResourceManager ayırır. Burada uygulama gerçekte yürütür NodeManager düğümleri olan. Ayrılan ilk kapsayıcı ApplicationMaster adlı özel bir uygulamayı çalıştırır. Bu ApplicationMaster kaynaklarında gönderilen uygulamayı çalıştırmak için gereken sonraki kapsayıcılar formunu alınırken sorumludur. Uygulama aşamalarını ApplicationMaster inceler (harita aşama ve aşama azaltmak) ve ne kadar veri işlenmesi gereken Etkenler. ApplicationMaster sonra istekleri (*görüşür*) uygulama adına ResourceManager kaynaklardan. ResourceManager sırayla kaynakları kümedeki NodeManagers gelen uygulama yürütülürken kullanmak için de ApplicationMaster için verir. 

Uygulamayı oluşturan görevleri çalıştırmak NodeManagers sonra rapor kendi ilerleme durumu ve durumu geri ApplicationMaster. ApplicationMaster sırayla uygulamayı ResourceManager durumunu raporlar. ResourceManager istemciye herhangi bir sonuç döndürür.

## <a name="yarn-on-hdinsight"></a>Hdınsight YARN

Tüm Hdınsight küme türleri YARN dağıtın. ResourceManager, küme içindeki ilk ve ikinci baş düğümler sırasıyla çalıştırdığınız bir birincil ve ikincil örnekle yüksek kullanılabilirlik için dağıtılır. ResourceManager yalnızca bir örneği aynı anda etkindir. Kümedeki kullanılabilir çalışan düğümleri arasında NodeManager örnekleri çalıştırın.

![Hdınsight YARN](./media/hdinsight-hadoop-architecture/yarn-on-hdinsight.png)

## <a name="see-also"></a>Ayrıca bkz.

* [Hdınsight'ta Hadoop MapReduce kullanın](hadoop/hdinsight-use-mapreduce.md)

<!--  * [HDInsight Architecture](hdinsight-architecture.md)  -->
