---
title: "Azure Hdınsight kullanarak Hive aaaTroubleshoot | Microsoft Docs"
description: "Apache Hive ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
keywords: "Azure Hdınsight, Hive, SSS, sorun giderme kılavuzu, sık sorulan sorular"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Hive Azure Hdınsight kullanarak sorun giderme

Merhaba üst sorular ve bunların çözümleri hakkında Apache Ambari, Apache Hive yükü ile çalışırken öğrenin.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Nasıl bir Hive meta depo dışarı aktarma ve başka bir kümede alma


### <a name="resolution-steps"></a>Çözüm adımları

1. Bir güvenli Kabuk (SSH) istemcisi kullanarak toohello Hdınsight kümesine bağlanın. Daha fazla bilgi için bkz: [ek okuma](#additional-reading-end).

2. Komut tooexport hello meta depo istediğiniz hello Hdınsight kümesinde aşağıdaki hello çalıştırın:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Bu komut, allatables.sql adlı bir dosya oluşturur.

3. Merhaba dosya alltables.sql toohello yeni Hdınsight kümesi kopyalayın ve ardından hello aşağıdaki komutu çalıştırın:

  ```apache
  hive -f alltables.sql
  ```

Merhaba çözüm adımları Hello kodda hello yeni kümede yollardır veri aynı hello veri yolları hello eski kümedeki olarak hello olduğunu varsayar. Merhaba veri yolları farklıysa, değişiklikleri el ile oluşturulan hello alltables.sql dosya tooreflect düzenleyebilirsiniz.

### <a name="additional-reading"></a>Ek kaynaklar

- [SSH kullanarak tooan Hdınsight kümesine bağlanın](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Bir kümede nasıl Hive günlüklerini bulun

### <a name="resolution-steps"></a>Çözüm adımları

1. SSH kullanarak toohello Hdınsight kümesine bağlanın. Daha fazla bilgi için bkz: **ek okuma**.

2. tooview Hive istemci günlükleri hello aşağıdaki komutu kullanın:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. tooview Hive meta depo günlükleri, komutu aşağıdaki hello kullan:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver günlükleri, komutu aşağıdaki hello kullan:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Ek kaynaklar

- [SSH kullanarak tooan Hdınsight kümesine bağlanın](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Merhaba Hive kabuğunu bir kümede belirli yapılandırmalarla nasıl başlatma

### <a name="resolution-steps"></a>Çözüm adımları

1. Merhaba Hive kabuğunu başlattığınızda yapılandırma anahtar-değer çifti belirtin. Daha fazla bilgi için bkz: [ek okuma](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. tüm etkin yapılandırmaları Hive kabuğunu, aşağıdaki kullanım hello üzerinde toolist komutu:

  ```apache
  hive> set;
  ```

  Örneğin, komut toostart Hive kabuğunu hello konsolda etkin hata ayıklama günlüğünü ile aşağıdaki hello kullan:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Ek kaynaklar

- [Hive yapılandırma özellikleri](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Küme kritik yolunda Tez DAG verileri nasıl çözümlemek


### <a name="resolution-steps"></a>Çözüm adımları
 
1. tooanalyze bir Apache Tez Çevrimsiz grafik (DAG) bir küme kritik grafikte yönlendirilmiş, SSH kullanarak toohello Hdınsight kümesine bağlanın. Daha fazla bilgi için bkz: [ek okuma](#additional-reading-end).

2. Bir komut isteminde hello aşağıdaki komutu çalıştırın:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist kullanılan tooanalyze Tez DAG olabilecek diğer çözümleyiciler hello aşağıdaki komutu kullanın:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Merhaba ilk bağımsız değişkeni olarak bir örnek program sağlamanız gerekir.

  Geçerli program adları şunlardır:
    - **ContainerReuseAnalyzer**: yazdırma bir kapsayıcı yeniden ayrıntıları
    - **CriticalPath**: Bul hello kritik yol, bir dag'nin
    - **LocalityAnalyzer**: yazdırma bir yere göre ayrıntıları
    - **ShuffleTimeAnalyzer**: hello karışık saati ayrıntıları bir çözümleme
    - **SkewAnalyzer**: hello eğme ayrıntıları bir çözümleme
    - **SlowNodeAnalyzer**: yazdırma bir düğüm ayrıntıları
    - **SlowTaskIdentifier**: bir yazdırma yavaş görev ayrıntıları
    - **SlowestVertexAnalyzer**: yazdırma bir yavaş köşe ayrıntıları
    - **SpillAnalyzer**: bir Karmadaki ayrıntılarını yazdırma
    - **TaskConcurrencyAnalyzer**: hello görev eşzamanlılık ayrıntıları bir yazdırma
    - **VertexLevelCriticalPathAnalyzer**: köşe düzeyinde bir hello kritik yol Bul


### <a name="additional-reading"></a>Ek kaynaklar

- [SSH kullanarak tooan Hdınsight kümesine bağlanın](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Bir kümeden nasıl Tez DAG veri karşıdan


#### <a name="resolution-steps"></a>Çözüm adımları

Toocollect hello Tez DAG veri iki yolu vardır:

- Merhaba komut satırından:
 
    SSH kullanarak toohello Hdınsight kümesine bağlanın. Hello komut isteminde hello aşağıdaki komutu çalıştırın:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Merhaba Ambari Tez görünümünü kullanın:
   
  1. TooAmbari gidin. 
  2. Git tooTez Görünüm (altında hello sağ üst köşesinde hello döşeme simgedir). 
  3. Merhaba tooview istediğiniz DAG seçin.
  4. Seçin **karşıdan veri**.

### <a name="additional-reading-end"></a>Ek kaynaklar

[SSH kullanarak tooan Hdınsight kümesine bağlanın](hdinsight-hadoop-linux-use-ssh-unix.md)






