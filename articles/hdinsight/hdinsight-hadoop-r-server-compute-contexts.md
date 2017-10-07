---
title: "hdınsight'ta - Azure R Server aaaCompute bağlamı seçeneklerini | Microsoft Docs"
description: "Merhaba farklı işlem bağlamı seçenekleri kullanılabilir toousers hdınsight'ta R Server ile hakkında bilgi edinin"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Hdınsight'ta R Server için içerik seçeneklerini işlem

Microsoft Azure hdınsight'ta R Server çağrıları ayarı hello işlem bağlamı tarafından yürütülen nasıl denetler. Bu makalede, kullanılabilir toospecify olup hello seçenekleri ve nasıl yürütme hello kenar düğümüne veya Hdınsight küme çekirdeği arasında paralel birkaç ölçeklendirin özetlenmektedir.

kümenin Hello kenar düğümü uygun bir yer tooconnect toohello küme ve toorun R komut dosyalarınızı sağlar. Bir kenar düğümüne ile Merhaba Çekirdeğinde hello kenar düğümü sunucusunun ScaleR hello paralel birkaç ölçeklendirin çalışan hello seçeneğini dağıtılmış işlevlerini sahip. Ayrıca bunları hello hello küme düğümleri arasında ScaleR'ın eşlemesi Hadoop azaltın veya Spark kullanarak işlem bağlamları çalıştırabilirsiniz.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Azure hdınsight'ta Microsoft R Server
[Microsoft Azure hdınsight'ta R Server](hdinsight-hadoop-r-server-overview.md) R tabanlı analizi için hello en son özellikleri sağlar. HDFS kapsayıcısında depolanan verileri kullanabilir, [Azure Blob](../storage/common/storage-introduction.md "Azure Blob Depolama") depolama hesabı, bir Data Lake store veya hello yerel Linux dosya sistemi. R Server açık kaynak R kurulu olduğundan, yapı hello R tabanlı uygulamalar hello 8000 + R açık kaynak paketlerinden birini uygulayabilirsiniz. Merhaba çalışmalarında de kullanabilir [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), R Server'ın içerdiği Microsoft'un büyük veri analizi paket.  

## <a name="compute-contexts-for-an-edge-node"></a>Bir kenar düğümüne bağlamları işlem
Genel olarak, R Server hello kenar düğümü üzerinde çalışacak bir R betiği hello R yorumlayıcı içinde bu düğüm üzerinde çalışır. Merhaba, ScaleR işlevini çağırın bu adımları durumlardır. Merhaba ScaleR işlem bağlamı nasıl ayarlanacağını belirlenen bir işlem ortamında Hello ScaleR çağrıları çalıştırın.  R betiği bir kenar düğümden çalıştırdığınızda, bağlam olan hello hello olası değerlerini hesaplama:

- Yerel sıralı (*'local'*)
- yerel paralel (*'localpar'*)
- Harita azaltın
- Spark

Merhaba *'local'* ve *'localpar'* seçenekleri yalnızca nasıl farklı **rxExec** çağrıları çalıştırılır. Her ikisi de diğer rx işlev çağrılarını paralel bir şekilde kullanılabilir tüm çekirdek arasında hello ScaleR kullanımla aksi belirtilmediği sürece yürütme **numCoresToUse** seçeneği, örneğin `rxOptions(numCoresToUse=6)`. Paralel yürütme seçeneklerini en iyi performans sunar.

Aşağıdaki tablonun hello çeşitli çağrıları nasıl yürütülen bağlam seçenekleri tooset işlem hello özetlenmektedir:

| İşlem bağlamı  | Nasıl tooset                      | Yürütme bağlamı                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Yerel sıralı | rxSetComputeContext('local')    | Paralel birkaç ölçeklendirin yürütülmesi hello Çekirdeğinde seri olarak yürütülen rxExec çağrıları dışında hello kenar düğümü sunucusu |
| Yerel paralel   | rxSetComputeContext('localpar') | Paralel birkaç ölçeklendirin yürütülmesi hello Çekirdeğinde hello kenar düğümü sunucusu |
| Spark            | RxSpark()                       | Dağıtılmış yürütülmesi Spark aracılığıyla hello düğümleri arasında hello HDI kümesi paralel birkaç ölçeklendirin |
| Harita azaltın       | RxHadoopMR()                    | Dağıtılmış yürütülmesi harita azaltmak aracılığıyla hello düğümleri arasında hello HDI kümesi paralel birkaç ölçeklendirin |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Bir işlem bağlamı karar verme yönergeleri

Paralel birkaç ölçeklendirin yürütme sağlayan seçtiğiniz hello üç seçenekten hangisinin analytics iş, hello boyutu ve verilerinizi hello konumu üzerinde hello yapısına bağlıdır. Hangi içerik toouse işlem belirten Basit formül yoktur. Ancak, hello doğru seçim yapın veya en azından bir Kıyaslama çalıştırmadan önce seçimleri daraltmak yardımcı yardımcı olabilecek temel bazı ilkeler vardır. Bu ilkeler yönlendirmede şunları içerir:

- Merhaba yerel Linux dosya sistemi HDFS hızlıdır.
- Yinelenen çözümlemeler hello veri yerel olmadığını ve XDF içinde olup olmadığını hızlıdır.
- Bir metin veri kaynağından küçük miktarda tercih toostream olur. Merhaba miktarda veri büyükse, analiz önce tooXDF dönüştürün.
- Merhaba yükünü kopyalama veya hello veri toohello kenar düğümüne çözümleme için akış için çok büyük miktarlarda verinin yönetilemeyen haline gelir.
- Spark harita azaltmak için Hadoop analizi daha hızlıdır.

Bu ilkeler verildiğinde, hello aşağıdaki bölümlerde bazı genel kurallar için bir işlem bağlamında seçme altın sunar.

### <a name="local"></a>Yerel
* Veri tooanalyze Hello miktarını küçük ise ve yinelenen analiz gerektirmez, ardından bunu doğrudan hello analiz yordamı kullanarak akış *'local'* veya *'localpar'*.
* Veri tooanalyze Hello miktarını küçük veya orta ölçekli ve yinelenen analiz gerektiriyorsa, ardından toohello yerel dosya sistemine kopyalama, tooXDF almak ve aracılığıyla analiz *'local'* veya *'localpar'*.

### <a name="hadoop-spark"></a>Hadoop Spark
* Veri tooanalyze Hello miktarını büyükse, tooa Spark DataFrame alma kullanarak **RxHiveData** veya **RxParquetData**, veya hdfs'deki tooXDF (depolama birimi bir sorun olmadığı sürece) ve hello Spark kullanarak analiz edin işlem bağlamı.

### <a name="hadoop-map-reduce"></a>Hadoop harita azaltın
* Genellikle daha yavaş olduğundan yalnızca hello Spark işlem bağlamına sahip insurmountable bir sorunla karşılaşırsanız hello harita azaltmak işlem bağlamı kullanın.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Satır içi Yardım rxSetComputeContext
Daha fazla bilgi ve örnekler ScaleR bağlamları işlem, R hello rxSetComputeContext yöntemi, örneğin yardımcı hello satır içi bakın:

    > ?rxSetComputeContext

Toohello de başvurabilir "[ScaleR dağıtılmış bilgi işlem kılavuzu](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" Merhaba kullanılabilir [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server MSDN'de") kitaplığı.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, kullanılabilir toospecify hakkında hello seçenekleri ve bunun nasıl yürütme hello kenar düğümüne veya Hdınsight küme çekirdeği arasında paralel birkaç ölçeklendirin öğrendiniz. Aşağıdaki konularda hello nasıl toouse Hdınsight R Server kümeleri, hakkında daha fazla toolearn bakın:

* [R Server Hadoop için genel bakış](hdinsight-hadoop-r-server-overview.md)
* [R Server ile için Hadoop kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md)
* [Rstudio'dan Server tooHDInsight (küme oluşturma sırasında eklenmedi varsa) ekleyin.](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight üzerinde R Server için Azure Depolama seçenekleri](hdinsight-hadoop-r-server-storage.md)

