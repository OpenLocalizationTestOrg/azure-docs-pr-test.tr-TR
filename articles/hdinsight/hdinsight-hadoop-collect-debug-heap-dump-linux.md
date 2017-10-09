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
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="3d97a-103">Linux tabanlı hdınsight'ta Hadoop Hizmetleri için yığın dökümleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3d97a-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="3d97a-104">Yığın dökümleri hello döküm oluşturuldu hello zamanında değişkenlerin hello değerleri dahil olmak üzere hello uygulamanın belleğin anlık görüntüsünü içerir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="3d97a-105">Bu nedenle bunlar çalışma zamanında oluşan sorunları tanılamak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="3d97a-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d97a-106">Merhaba bu belgedeki adımlar yalnızca Linux kullanmak Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="3d97a-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="3d97a-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3d97a-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3d97a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3d97a-109"><a name="whichServices"></a>Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="3d97a-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="3d97a-110">Yığın dökümleri Hizmetleri aşağıdaki hello için etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3d97a-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="3d97a-111">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="3d97a-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="3d97a-112">**Hive** -hiveserver2, meta depo, derbyserver</span><span class="sxs-lookup"><span data-stu-id="3d97a-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="3d97a-113">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="3d97a-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="3d97a-114">**yarn** -resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="3d97a-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="3d97a-115">**hdfs** -datanode, secondarynamenode, iş</span><span class="sxs-lookup"><span data-stu-id="3d97a-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="3d97a-116">Ayrıca hello eşlemesi için yığın dökümleri etkinleştirmek ve azaltmak işlemleri Hdınsight tarafından çalıştırılan.</span><span class="sxs-lookup"><span data-stu-id="3d97a-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="3d97a-117"><a name="configuration"></a>Anlama yığın dökümü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3d97a-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="3d97a-118">Yığın dökümleri seçenekleri geçirerek etkin (bazen çevrilir olarak bilinen veya parametrelerini) toohello bir hizmeti başlatıldığında JVM.</span><span class="sxs-lookup"><span data-stu-id="3d97a-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="3d97a-119">Çoğu Hadoop Hizmetleri için bu seçenekleri hello Kabuk kullanılan komut dosyası toostart hello hizmet toopass değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d97a-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="3d97a-120">Her komut dosyasında bir dışarı aktarma için yoktur  **\* \_OPTS**, hello seçenekleri içeren toohello JVM geçirildi.</span><span class="sxs-lookup"><span data-stu-id="3d97a-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="3d97a-121">Merhaba, örneğin, **hadoop env.sh** komut dosyası, ile başlayan hello satır `export HADOOP_NAMENODE_OPTS=` hello iş hizmeti hello seçeneklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="3d97a-122">Eşleme ve azaltma hello MapReduce hizmeti bir alt işlemi bu işlemleri olduğu gibi işlemleri biraz farklı.</span><span class="sxs-lookup"><span data-stu-id="3d97a-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="3d97a-123">Her eşleme ya da azaltmak işlem bir alt kapsayıcıda çalışır ve hello JVM seçenekleri içeren iki girdi vardır.</span><span class="sxs-lookup"><span data-stu-id="3d97a-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="3d97a-124">İçinde yer alan her ikisi de **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="3d97a-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="3d97a-125">**mapreduce.Admin.Map.Child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="3d97a-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="3d97a-126">**mapreduce.Admin.reduce.Child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="3d97a-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="3d97a-127">Ambari kullanarak toomodify hem hello komut dosyaları ve hello kümedeki düğümler arasında değişiklikleri çoğaltmaya Ambari mapred-site.xml ayarları işlemek öneririz.</span><span class="sxs-lookup"><span data-stu-id="3d97a-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="3d97a-128">Merhaba bkz [Ambari kullanarak](#using-ambari) belirli adımlar için bölüm.</span><span class="sxs-lookup"><span data-stu-id="3d97a-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="3d97a-129">Yığın dökümlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3d97a-129">Enable heap dumps</span></span>

<span data-ttu-id="3d97a-130">bir OutOfMemoryError oluştuğunda hello aşağıdaki seçenek yığın dökümleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="3d97a-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="3d97a-131">Merhaba  **+**  bu seçeneği etkin olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="3d97a-132">Merhaba varsayılan devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="3d97a-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="3d97a-133">Merhaba döküm dosyaları büyük olabileceğinden yığın dökümleri hdınsight'ta Hadoop Hizmetleri için varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="3d97a-134">Bunları gidermek için etkinleştirirseniz, bunları yeniden oluşturduktan sonra sorun ve toplanan hello döküm dosyalarını hello toodisable unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3d97a-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="3d97a-135">Konum dökümü</span><span class="sxs-lookup"><span data-stu-id="3d97a-135">Dump location</span></span>

<span data-ttu-id="3d97a-136">Merhaba varsayılan hello döküm dosyası hello geçerli çalışma dizini konumudur.</span><span class="sxs-lookup"><span data-stu-id="3d97a-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="3d97a-137">Merhaba burada denetleyebilirsiniz seçenekten hello kullanarak saklanır:</span><span class="sxs-lookup"><span data-stu-id="3d97a-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="3d97a-138">Örneğin, kullanarak `-XX:HeapDumpPath=/tmp` hello tmp dizininde depolanan hello dökümleri toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="3d97a-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="3d97a-139">Betikler</span><span class="sxs-lookup"><span data-stu-id="3d97a-139">Scripts</span></span>

<span data-ttu-id="3d97a-140">Bir komut dosyası ayrıca tetikleyebilir olduğunda bir **OutOfMemoryError** oluşur.</span><span class="sxs-lookup"><span data-stu-id="3d97a-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="3d97a-141">Örneğin, bir bildirim hello hata bilmesi tetikleme oluştu.</span><span class="sxs-lookup"><span data-stu-id="3d97a-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="3d97a-142">Kullanım hello aşağıdaki üzerinde bir komut dosyası tootrigger seçeneği bir __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="3d97a-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="3d97a-143">Hadoop dağıtılmış bir sistemde olduğundan, kullanılan herhangi bir komut dosyası hello hizmetinin çalıştığı hello kümedeki tüm düğümlerde yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="3d97a-144">Merhaba betik gerekir ayrıca olması hello hesap Merhaba hizmeti çalışırken tarafından erişilebilir olduğundan ve sağlamalısınız bir konumda Yürütme izinleri.</span><span class="sxs-lookup"><span data-stu-id="3d97a-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="3d97a-145">Örneğin, toostore komut dosyalarında isteyebilir `/usr/local/bin` ve `chmod go+rx /usr/local/bin/filename.sh` toogrant okuma ve Yürütme izinleri.</span><span class="sxs-lookup"><span data-stu-id="3d97a-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="3d97a-146">Ambari kullanarak</span><span class="sxs-lookup"><span data-stu-id="3d97a-146">Using Ambari</span></span>

<span data-ttu-id="3d97a-147">hizmet için aşağıdaki adımları kullanın hello toomodify hello yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="3d97a-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="3d97a-148">Kümeniz için Hello Ambari web kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="3d97a-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="3d97a-149">Merhaba, https://YOURCLUSTERNAME.azurehdinsight.net URL'dir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="3d97a-150">İstendiğinde, toohello site hello HTTP hesap adını kullanarak kimlik doğrulaması (varsayılan: Yönetici) ve parola kümeniz için.</span><span class="sxs-lookup"><span data-stu-id="3d97a-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3d97a-151">İkinci kez Ambari tarafından hello kullanıcı adı ve parola istenebilir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="3d97a-152">Bu durumda, girin aynı hesap adı ve parola hello</span><span class="sxs-lookup"><span data-stu-id="3d97a-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="3d97a-153">Hello solda Hello listesini kullanarak toomodify istediğiniz hello hizmet alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="3d97a-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="3d97a-154">Örneğin, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="3d97a-154">For example, **HDFS**.</span></span> <span data-ttu-id="3d97a-155">Merhaba Hello merkezi bölmesinde seçin **yapılandırmalar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3d97a-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Ambari web HDFS yapılandırmalar sekmesi seçili görüntüsü](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="3d97a-157">Hello kullanarak **filtre...**  girişi girin **çevrilir**.</span><span class="sxs-lookup"><span data-stu-id="3d97a-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="3d97a-158">Yalnızca bu metni içeren öğeleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-158">Only items containing this text are displayed.</span></span>

    ![Filtrelenmiş liste](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="3d97a-160">Hello bulur  **\* \_OPTS** tooenable yığın dökümleri için istediğiniz ve hello seçenekleri eklemek hello hizmeti için giriş tooenable istiyor.</span><span class="sxs-lookup"><span data-stu-id="3d97a-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="3d97a-161">Görüntü aşağıdaki hello ekledim `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_iş\_OPTS** girişi:</span><span class="sxs-lookup"><span data-stu-id="3d97a-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![-XX ile HADOOP_NAMENODE_OPTS: + HeapDumpOnOutOfMemoryError - XX: = HeapDumpPath/tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="3d97a-163">Etkinleştirme yığın dökümleri hello için harita ya da alt işlem azaltmak adlı hello alanları için Ara **mapreduce.admin.map.child.java.opts** ve **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="3d97a-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="3d97a-164">Kullanım hello **kaydetmek** düğmesini toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="3d97a-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="3d97a-165">Merhaba değişiklikleri açıklayan kısa bir not girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d97a-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="3d97a-166">Merhaba değişiklikler uygulandıktan sonra hello **yeniden başlatma gerekli** simge bir veya daha fazla hizmet görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![gerekli simgesini ve düğmesi yeniden başlatın](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="3d97a-168">Yeniden başlatma gerektiren her hizmeti seçin ve hello kullanın **hizmet eylemleri** çok düğmesini**kapatma üzerinde Bakım modu**.</span><span class="sxs-lookup"><span data-stu-id="3d97a-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="3d97a-169">Bakım modu hello hizmetinden oluşturulmasını, yeniden başlattığınızda önler uyarıları engeller.</span><span class="sxs-lookup"><span data-stu-id="3d97a-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Bakım modu menüsünde Aç](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="3d97a-171">Bakım modu etkinleştirildiğinde, hello kullan **yeniden** hello hizmeti için çok düğmesini**tüm parametreden yeniden başlatın**</span><span class="sxs-lookup"><span data-stu-id="3d97a-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Tüm etkilenen giriş yeniden başlatın](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="3d97a-173">Merhaba hello girişlerinde **yeniden** düğmesi diğer hizmetler için farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d97a-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="3d97a-174">Merhaba hizmetleri yeniden başlattıktan sonra hello kullan **hizmet eylemleri** çok düğmesini**Bakım modu devre dışı bırakma**.</span><span class="sxs-lookup"><span data-stu-id="3d97a-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="3d97a-175">Merhaba hizmeti için uyarılar için izleme bu Ambari tooresume.</span><span class="sxs-lookup"><span data-stu-id="3d97a-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

