---
title: "aaaAccess Hadoop YARN uygulama günlüklerini Linux tabanlı Hdınsight üzerinde - Azure | Microsoft Docs"
description: "Tooaccess YARN uygulama hello komut satırı ve bir web tarayıcısı kullanarak bir Linux tabanlı Hdınsight (Hadoop) kümesinde nasıl günlüğe yazacağını öğrenin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Linux tabanlı Hdınsight üzerinde erişim YARN uygulama günlükleri

Azure Hdınsight Hadoop kümesinde YARN (henüz başka bir kaynak Uzlaştırıcı) uygulamaları için günlüklerini nasıl tooaccess hello öğrenin.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>YARN zaman çizelgesi sunucu

Merhaba [YARN zaman çizelgesi sunucu](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) tamamlanmış uygulamaların ve iki farklı arabirimleri aracılığıyla çerçeveye özel uygulama bilgilerini hakkında genel bilgiler sağlar. Bu avantajlar şunlardır:

* 3.1.1.374 sürümüyle etkin ya da daha yüksek depolama ve alma Hdınsight kümelerinde genel uygulama bilgilerinin açıldı.
* Hdınsight kümelerinde Hello çerçeveye özel uygulama bilgileri hello zaman çizelgesi sunucu bileşeninin şu anda kullanılamıyor.

Veri türü aşağıdaki hello uygulamalar hakkında genel bilgiler içerir:

* Merhaba uygulama kimliği, uygulamanın benzersiz tanıtıcısı
* Merhaba uygulaması başlatan hello kullanıcı
* Toocomplete Merhaba uygulaması denemeleri hakkında bilgi yapılan
* Belirtilen uygulama girişimleri tarafından kullanılan Merhaba kapsayıcılara

## <a name="YARNAppsAndLogs"></a>YARN uygulamalar ve günlükleri

YARN kaynak Yönetimi'nden uygulama zamanlama/izleme ayrıştırarak birden fazla programlama modeli (bunlardan biri olan MapReduce) destekler. YARN kullanan bir genel *ResourceManager* (RM) çalışan-düğüm başına *NodeManagers* (NMs) ve uygulama başına *ApplicationMasters* (AMs). Merhaba uygulama başına AM kaynakları (CPU, bellek, disk, ağ) hello RM ile uygulamanızı çalıştırmak için anlaşır Merhaba RM olarak verilen bu kaynakları NMs toogrant ile çalışır *kapsayıcıları*. Merhaba AM hello RM tarafından Merhaba kapsayıcılara atanan tooit hello ilerlemesini izlemek için sorumludur Bir uygulama Merhaba uygulaması hello doğasına bağlı olarak çok sayıda kapsayıcı gerektirebilir.

Her uygulama katları oluşabilir *uygulama denemeleri*. Bir uygulama başarısız olursa, yeni bir girişim denenen. Her girişimde bir kapsayıcıda çalışır. Bir anlamda hello bağlam YARN uygulama tarafından gerçekleştirilen çalışmanın temel birim için bir kapsayıcı sağlar. Bir kapsayıcı hello bağlamında yapılır tüm iş üzerinde hangi hello kapsayıcı ayrılan hello tek çalışan düğümünde gerçekleştirilir. Bkz: [YARN kavramları] [ YARN-concepts] daha ayrıntılı başvuru.

Uygulama (ve ilişkili hello kapsayıcı günlükleri) sorunlu Hadoop uygulamalarında hata ayıklama de önemlidir. YARN toplama, toplama ve hello ile uygulama günlükleri depolamak için iyi bir çerçeve sağlar [günlük toplama] [ log-aggregation] özelliği. Merhaba günlük toplama özellik erişimi uygulama günlüklerini daha belirleyici hale getirir. Bir alt düğüm üzerindeki tüm kapsayıcıları arasında günlükleri toplar ve çalışan düğümü başına bir toplu günlük dosyası olarak depolar. bir uygulama bittikten sonra hello günlük hello varsayılan dosya sistemi üzerinde depolanır. Uygulamanızın yüzlerce veya binlerce kapsayıcıların kullanabilir, ancak tek bir alt düğüm üzerinde çalışan tüm kapsayıcıları için her zaman toplanmış tooa tek dosyalı günlüklerin. Bu nedenle var. yalnızca uygulamanız tarafından kullanılan çalışan düğümü başına 1 günlük Günlük toplama Hdınsight kümeleri sürüm 3.0 ve üstü varsayılan olarak etkindir. Toplanan günlükleri hello kümesi için varsayılan depolama bulunur. yol aşağıdaki hello hello HDFS yol toohello günlükleri şöyledir:

    /app-logs/<user>/logs/<applicationId>

Merhaba yolundaki `user` hello Merhaba uygulaması başlatan hello kullanıcı adıdır. Merhaba `applicationId` hello YARN RM tarafından hello atanan benzersiz tanımlayıcı tooan uygulama

Bunlar yazıldığı şekilde hello toplanmış günlükleri doğrudan okunabilir olmayan bir [TFile][T-file], [ikili biçimi] [ binary-format] kapsayıcı dizini. YARN ResourceManager günlüklerini hello veya CLI araçlarını tooview Bu günlükler uygulamalar veya ilgi kapsayıcıları için düz metin olarak kullanın.

## <a name="yarn-cli-tools"></a>YARN CLI araçlarını

toouse hello YARN CLI araçlarını, SSH kullanarak Hdınsight kümesi toohello önce bağlanmanız gerekir. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

Aşağıdaki komutları hello birini çalıştırarak düz metin olarak bu günlükleri görüntüleyebilirsiniz:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Merhaba belirtin &lt;ApplicationId >, &lt;kullanıcı-kim-başlatıldı--uygulama >, &lt;Containerıd >, ve &lt;alt düğüm adresi > Bu komutlar çalıştırıldığında, bilgi.

## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager kullanıcı Arabirimi

Merhaba YARN ResourceManager UI hello küme headnode üzerinde çalışır. Merhaba Ambari web kullanıcı Arabirimi erişilir. Aşağıdaki adımları tooview hello YARN kullanım hello kaydeder:

1. Web tarayıcınızda toohttps://CLUSTERNAME.azurehdinsight.net gidin. CLUSTERNAME hello Hdınsight kümenizin adıyla değiştirin.
2. Merhaba hello soldaki hizmetlerin listesinden **YARN**.

    ![Seçili yarn hizmeti](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. Merhaba gelen **hızlı bağlantılar** açılan listesinde, hello küme baş düğümler birini seçin ve ardından **ResourceManager günlük**.

    ![Yarn hızlı bağlantılar](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Bağlantılar tooYARN günlükleri bir listesi sunulur.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
