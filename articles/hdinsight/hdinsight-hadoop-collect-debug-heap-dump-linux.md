---
title: "aaaEnable yığın dökümleri hdınsight'ta - Azure Hadoop Hizmetleri için | Microsoft Docs"
description: "Hata ayıklama ve çözümleme için Hadoop Linux tabanlı Hdınsight kümeleri Hizmetleri'nden yığın dökümleri etkinleştirin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Linux tabanlı hdınsight'ta Hadoop Hizmetleri için yığın dökümleri etkinleştir

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Yığın dökümleri hello döküm oluşturuldu hello zamanında değişkenlerin hello değerleri dahil olmak üzere hello uygulamanın belleğin anlık görüntüsünü içerir. Bu nedenle bunlar çalışma zamanında oluşan sorunları tanılamak için kullanışlıdır.

> [!IMPORTANT]
> Merhaba bu belgedeki adımlar yalnızca Linux kullanmak Hdınsight kümeleri ile çalışır. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whichServices"></a>Hizmetleri

Yığın dökümleri Hizmetleri aşağıdaki hello için etkinleştirebilirsiniz:

* **hcatalog** -tempelton
* **Hive** -hiveserver2, meta depo, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager, nodemanager, timelineserver
* **hdfs** -datanode, secondarynamenode, iş

Ayrıca hello eşlemesi için yığın dökümleri etkinleştirmek ve azaltmak işlemleri Hdınsight tarafından çalıştırılan.

## <a name="configuration"></a>Anlama yığın dökümü yapılandırma

Yığın dökümleri seçenekleri geçirerek etkin (bazen çevrilir olarak bilinen veya parametrelerini) toohello bir hizmeti başlatıldığında JVM. Çoğu Hadoop Hizmetleri için bu seçenekleri hello Kabuk kullanılan komut dosyası toostart hello hizmet toopass değiştirebilirsiniz.

Her komut dosyasında bir dışarı aktarma için yoktur  **\* \_OPTS**, hello seçenekleri içeren toohello JVM geçirildi. Merhaba, örneğin, **hadoop env.sh** komut dosyası, ile başlayan hello satır `export HADOOP_NAMENODE_OPTS=` hello iş hizmeti hello seçeneklerini içerir.

Eşleme ve azaltma hello MapReduce hizmeti bir alt işlemi bu işlemleri olduğu gibi işlemleri biraz farklı. Her eşleme ya da azaltmak işlem bir alt kapsayıcıda çalışır ve hello JVM seçenekleri içeren iki girdi vardır. İçinde yer alan her ikisi de **mapred-site.xml**:

* **mapreduce.Admin.Map.Child.Java.opts**
* **mapreduce.Admin.reduce.Child.Java.opts**

> [!NOTE]
> Ambari kullanarak toomodify hem hello komut dosyaları ve hello kümedeki düğümler arasında değişiklikleri çoğaltmaya Ambari mapred-site.xml ayarları işlemek öneririz. Merhaba bkz [Ambari kullanarak](#using-ambari) belirli adımlar için bölüm.

### <a name="enable-heap-dumps"></a>Yığın dökümlerini etkinleştirme

bir OutOfMemoryError oluştuğunda hello aşağıdaki seçenek yığın dökümleri sağlar:

    -XX:+HeapDumpOnOutOfMemoryError

Merhaba  **+**  bu seçeneği etkin olduğunu gösterir. Merhaba varsayılan devre dışıdır.

> [!WARNING]
> Merhaba döküm dosyaları büyük olabileceğinden yığın dökümleri hdınsight'ta Hadoop Hizmetleri için varsayılan olarak etkin değildir. Bunları gidermek için etkinleştirirseniz, bunları yeniden oluşturduktan sonra sorun ve toplanan hello döküm dosyalarını hello toodisable unutmayın.

### <a name="dump-location"></a>Konum dökümü

Merhaba varsayılan hello döküm dosyası hello geçerli çalışma dizini konumudur. Merhaba burada denetleyebilirsiniz seçenekten hello kullanarak saklanır:

    -XX:HeapDumpPath=/path

Örneğin, kullanarak `-XX:HeapDumpPath=/tmp` hello tmp dizininde depolanan hello dökümleri toobe neden olur.

### <a name="scripts"></a>Betikler

Bir komut dosyası ayrıca tetikleyebilir olduğunda bir **OutOfMemoryError** oluşur. Örneğin, bir bildirim hello hata bilmesi tetikleme oluştu. Kullanım hello aşağıdaki üzerinde bir komut dosyası tootrigger seçeneği bir __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Hadoop dağıtılmış bir sistemde olduğundan, kullanılan herhangi bir komut dosyası hello hizmetinin çalıştığı hello kümedeki tüm düğümlerde yerleştirilmelidir.
> 
> Merhaba betik gerekir ayrıca olması hello hesap Merhaba hizmeti çalışırken tarafından erişilebilir olduğundan ve sağlamalısınız bir konumda Yürütme izinleri. Örneğin, toostore komut dosyalarında isteyebilir `/usr/local/bin` ve `chmod go+rx /usr/local/bin/filename.sh` toogrant okuma ve Yürütme izinleri.

## <a name="using-ambari"></a>Ambari kullanarak

hizmet için aşağıdaki adımları kullanın hello toomodify hello yapılandırması:

1. Kümeniz için Hello Ambari web kullanıcı arabirimini açın. Merhaba, https://YOURCLUSTERNAME.azurehdinsight.net URL'dir.

    İstendiğinde, toohello site hello HTTP hesap adını kullanarak kimlik doğrulaması (varsayılan: Yönetici) ve parola kümeniz için.

   > [!NOTE]
   > İkinci kez Ambari tarafından hello kullanıcı adı ve parola istenebilir. Bu durumda, girin aynı hesap adı ve parola hello

2. Hello solda Hello listesini kullanarak toomodify istediğiniz hello hizmet alanı seçin. Örneğin, **HDFS**. Merhaba Hello merkezi bölmesinde seçin **yapılandırmalar** sekmesi.

    ![Ambari web HDFS yapılandırmalar sekmesi seçili görüntüsü](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. Hello kullanarak **filtre...**  girişi girin **çevrilir**. Yalnızca bu metni içeren öğeleri görüntülenir.

    ![Filtrelenmiş liste](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Hello bulur  **\* \_OPTS** tooenable yığın dökümleri için istediğiniz ve hello seçenekleri eklemek hello hizmeti için giriş tooenable istiyor. Görüntü aşağıdaki hello ekledim `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_iş\_OPTS** girişi:

    ![-XX ile HADOOP_NAMENODE_OPTS: + HeapDumpOnOutOfMemoryError - XX: = HeapDumpPath/tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Etkinleştirme yığın dökümleri hello için harita ya da alt işlem azaltmak adlı hello alanları için Ara **mapreduce.admin.map.child.java.opts** ve **mapreduce.admin.reduce.child.java.opts**.

    Kullanım hello **kaydetmek** düğmesini toosave hello değişiklikleri. Merhaba değişiklikleri açıklayan kısa bir not girebilirsiniz.

5. Merhaba değişiklikler uygulandıktan sonra hello **yeniden başlatma gerekli** simge bir veya daha fazla hizmet görüntülenir.

    ![gerekli simgesini ve düğmesi yeniden başlatın](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Yeniden başlatma gerektiren her hizmeti seçin ve hello kullanın **hizmet eylemleri** çok düğmesini**kapatma üzerinde Bakım modu**. Bakım modu hello hizmetinden oluşturulmasını, yeniden başlattığınızda önler uyarıları engeller.

    ![Bakım modu menüsünde Aç](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Bakım modu etkinleştirildiğinde, hello kullan **yeniden** hello hizmeti için çok düğmesini**tüm parametreden yeniden başlatın**

    ![Tüm etkilenen giriş yeniden başlatın](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > Merhaba hello girişlerinde **yeniden** düğmesi diğer hizmetler için farklı olabilir.

8. Merhaba hizmetleri yeniden başlattıktan sonra hello kullan **hizmet eylemleri** çok düğmesini**Bakım modu devre dışı bırakma**. Merhaba hizmeti için uyarılar için izleme bu Ambari tooresume.

