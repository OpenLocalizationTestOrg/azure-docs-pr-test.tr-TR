---
title: "Azure Hdınsight kullanarak YARN aaaTroubleshoot | Microsoft Docs"
description: "Apache Hadoop YARN ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
keywords: "Azure Hdınsight, YARN, SSS, sorun giderme kılavuzu, sık sorulan sorular"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>YARN Azure Hdınsight kullanarak sorun giderme

Apache Ambari, Apache Hadoop YARN yükü ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Bir kümede nasıl yeni bir YARN sıra oluşturulsun mu


### <a name="resolution-steps"></a>Çözüm adımları 

Kullanım hello aşağıdaki Ambari toocreate yeni bir YARN sırası adımları ve hello kapasite ayırma tüm hello sıraları arasında dengeleyin. 

Bu örnekte, iki mevcut sıraları (**varsayılan** ve **thriftsvr**) hem de hello yeni sıra (spark) % 50 kapasitesini sunan % 50 kapasite too25% kapasiteden, değiştirilir.
| Kuyruk | Kapasite | Maksimum kapasite |
| --- | --- | --- | --- |
| Varsayılan | %25 | 50% |
| thrftsvr | %25 | 50% |
| Spark | 50% | 50% |

1. Select hello **Ambari görünümleri** simgesine ve ardından hello Kılavuz düzeni. Ardından, **YARN sıra yöneticisi**.

    ![Merhaba Ambari görünümleri simgesini seçin](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Select hello **varsayılan** sırası.

    ![Merhaba varsayılan sıra seçin](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Hello için **varsayılan** kuyruk, hello değiştirme **kapasite** % 50 too25%. Hello için **thriftsvr** kuyruk, hello değiştirme **kapasite** too25%.

    ![Merhaba kapasite too25% hello sıralar için varsayılan ve thriftsvr değiştirin](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. toocreate yeni bir sıra seçin **ekleme sırası**.

    ![Select kuyruk Ekle](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Merhaba yeni kuyruk adı.

    ![Merhaba sıra Spark adı](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Merhaba bırakın **kapasite** % 50 ve ardından hello değerlerinde **Eylemler** düğmesi.

    ![Merhaba Eylemler düğmesini seçin](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Seçin **kaydedin ve yenileyin sıraları**.

    ![Kaydet'i seçin ve Kuyruklar Yenile](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Bu değişiklikler hemen hello YARN Zamanlayıcı UI'üzerinde görünür.

### <a name="additional-reading"></a>Ek kaynaklar

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Bir kümeden nasıl YARN günlüklerini karşıdan


### <a name="resolution-steps"></a>Çözüm adımları 

1. Bir güvenli Kabuk (SSH) istemcisi kullanarak toohello Hdınsight kümesine bağlanın. Daha fazla bilgi için bkz: [ek okuma](#additional-reading-2).

2. tüm uygulama kimlikleri çalışmakta olan, hello YARN uygulamaların hello toolist hello aşağıdaki komutu çalıştırın:

    ```apache
    yarn top
    ```
    Merhaba kimlikleri hello listelenen **APPLİCATİONID** sütun. Hello günlükleri indirmek **APPLİCATİONID** sütun.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. tüm uygulama yöneticileri için toodownload YARN kapsayıcı günlüklerini hello aşağıdaki komutu kullanın:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Bu komut amlogs.txt adlı bir günlük dosyası oluşturur. 

4. toodownload YARN kapsayıcı günlüklerini yalnızca hello en son uygulama Yöneticisi için komutu aşağıdaki hello kullan:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Bu komut latestamlogs.txt adlı bir günlük dosyası oluşturur. 

4. toodownload YARN kapsayıcı günlüklerini hello ilk iki uygulama yöneticileri için komutu aşağıdaki hello kullan:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Bu komut first2amlogs.txt adlı bir günlük dosyası oluşturur. 

5. Tüm YARN kapsayıcı günlükleri, toodownload kullanmak hello komutu:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Bu komut logs.txt adlı bir günlük dosyası oluşturur. 

6. belirli bir kapsayıcıya, komutu aşağıdaki kullanım hello için toodownload hello YARN kapsayıcı günlüğü:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Bu komut containerlogs.txt adlı bir günlük dosyası oluşturur.

### <a name="additional-reading-2"></a>Ek kaynaklar

- [SSH kullanarak tooHDInsight (Hadoop) bağlanma](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN kavramları ve uygulamalar](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







