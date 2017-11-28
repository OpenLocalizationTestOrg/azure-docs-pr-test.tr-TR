---
title: "Azure Hdınsight kullanarak HBase aaaTroubleshoot | Microsoft Docs"
description: "HBase ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="0de4b-103">Azure Hdınsight kullanarak HBase sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0de4b-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="0de4b-104">Apache Ambari, Apache HBase yükü ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0de4b-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="0de4b-105">Birden çok atanmamış bölgeleri ile nasıl hbck komutu raporları çalıştırılsın mı</span><span class="sxs-lookup"><span data-stu-id="0de4b-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="0de4b-106">Merhaba çalıştırdığınızda görebilirsiniz genel bir hata iletisi `hbase hbck` komuttur "birden çok atanmamış bölgeler veya Delik bölgelerinin hello zincirindeki."</span><span class="sxs-lookup"><span data-stu-id="0de4b-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="0de4b-107">Hello HBase ana UI'da, tüm bölge sunuculara dengesini bölgeler hello sayısını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="0de4b-108">Daha sonra çalıştırabilirsiniz `hbase hbck` toosee delik hello bölge zincirindeki komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="0de4b-109">Delik hello çevrimdışı bölgeleri, bunu düzeltme hello atamaları ilk kaynaklanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="0de4b-110">toobring atanmamış bölgeleri arka tooa normal durum Merhaba, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="0de4b-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="0de4b-111">SSH kullanarak Hdınsight HBase kümesi içinde toohello imzalayın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="0de4b-112">Merhaba çalıştırmak hello ZooKeeper kabuğu ile tooconnect `hbase zkcli` komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="0de4b-113">Merhaba çalıştırmak `rmr /hbase/regions-in-transition` komut veya hello `rmr /hbase-unsecure/regions-in-transition` komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="0de4b-114">Merhaba gelen tooexit `hbase zkcli` Kabuk, hello kullan `exit` komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="0de4b-115">Merhaba Apache Ambari UI açın ve ardından hello etkin HBase ana hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="0de4b-116">Merhaba çalıştırmak `hbase hbck` komutunu yeniden (seçenekleri olmadan).</span><span class="sxs-lookup"><span data-stu-id="0de4b-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="0de4b-117">Tüm bölgeler atanan bu komut tooensure Hello çıktısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0de4b-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="0de4b-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Zaman aşımı sorunları nasıl hbck komutlarını bölge atamaları kullanırken düzeltme</span><span class="sxs-lookup"><span data-stu-id="0de4b-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="0de4b-119">Sorun</span><span class="sxs-lookup"><span data-stu-id="0de4b-119">Issue</span></span>

<span data-ttu-id="0de4b-120">Merhaba kullandığınızda zaman aşımı sorunlarıyla ilgili olası bir nedeni `hbck` komutu, birkaç bölgeler hello "geçiş" olduğundan emin olabilir uzun bir süre için durum.</span><span class="sxs-lookup"><span data-stu-id="0de4b-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="0de4b-121">Bu bölgeler hello HBase ana UI çevrimdışı olarak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="0de4b-122">Çok sayıda bölgeleri tootransition denediğinizden HBase ana zaman aşımı olabilir ve bu bölgeler tekrar çevrimiçi oluşturulamıyor toobring olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0de4b-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0de4b-123">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-123">Resolution steps</span></span>

1. <span data-ttu-id="0de4b-124">SSH kullanarak Hdınsight HBase kümesi içinde toohello imzalayın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="0de4b-125">Merhaba çalıştırmak hello ZooKeeper kabuğu ile tooconnect `hbase zkcli` komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="0de4b-126">Merhaba çalıştırmak `rmr /hbase/regions-in-transition` veya hello `rmr /hbase-unsecure/regions-in-transition` komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="0de4b-127">tooexit hello `hbase zkcli` Kabuk, hello kullan `exit` komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="0de4b-128">Hello Ambari UI, hello etkin HBase ana hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="0de4b-129">Merhaba çalıştırmak `hbase hbck -fixAssignments` yeniden komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="0de4b-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Nasıl ı zorla-küme güvenli modda HDFS devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="0de4b-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="0de4b-131">Sorun</span><span class="sxs-lookup"><span data-stu-id="0de4b-131">Issue</span></span>

<span data-ttu-id="0de4b-132">Merhaba yerel Hadoop dağıtılmış dosya sistemi (HDFS) hello Hdınsight kümesinde güvenli modda takıldı.</span><span class="sxs-lookup"><span data-stu-id="0de4b-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0de4b-133">Ayrıntılı açıklama</span><span class="sxs-lookup"><span data-stu-id="0de4b-133">Detailed description</span></span>

<span data-ttu-id="0de4b-134">HDFS komutu aşağıdaki hello çalıştırdığınızda bu hata bir hatadan kaynaklanıyor:</span><span class="sxs-lookup"><span data-stu-id="0de4b-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="0de4b-135">Merhaba hata toorun hello komutu çalıştığınızda görebilirsiniz şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="0de4b-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="0de4b-136">Olası neden</span><span class="sxs-lookup"><span data-stu-id="0de4b-136">Probable cause</span></span>

<span data-ttu-id="0de4b-137">Merhaba Hdınsight kümesi bırakıldı tooa çok az sayıda düğüm ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="0de4b-138">düğüm sayısını Hello aşağıdadır veya toohello HDFS çoğaltma faktörü kapatın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0de4b-139">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-139">Resolution steps</span></span> 

1. <span data-ttu-id="0de4b-140">Merhaba Hdınsight üzerinde HDFS hello aşağıdaki komutları çalıştırarak küme hello Hello durumunu alın:</span><span class="sxs-lookup"><span data-stu-id="0de4b-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="0de4b-141">HDFS hello Hdınsight üzerinde aşağıdaki komutları hello kullanarak küme hello hello bütünlüğünü de denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0de4b-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="0de4b-142">Hiçbir eksik, bozuk veya under-çoğaltılmış bloğu yok veya bu blokları yoksayılabilir karar verirseniz, komut tootake hello adı düğümünü güvenli mod dışında izleyen hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0de4b-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="0de4b-143">Nasıl JDBC veya SQLLine bağlantısı düzeltirim Apache Phoenix ile ilgili sorunları</span><span class="sxs-lookup"><span data-stu-id="0de4b-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0de4b-144">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-144">Resolution steps</span></span>

<span data-ttu-id="0de4b-145">tooconnect Phoenix ile başlangıç IP adresi etkin ZooKeeper düğümün sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="0de4b-146">Bu hello ZooKeeper hizmet toowhich sqlline.py çalışıyor olun tooconnect olan hazır ve çalışır.</span><span class="sxs-lookup"><span data-stu-id="0de4b-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="0de4b-147">İçinde toohello, SSH kullanarak Hdınsight kümesi oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="0de4b-148">Merhaba aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="0de4b-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="0de4b-149">Başlangıç IP adresi hello etkin ZooKeeper düğümünün hello Ambari UI ' alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="0de4b-150">Çok Git**HBase** > **hızlı bağlantılar** > **ZK\* (etkin)** > **Zookeeper bilgisi**.</span><span class="sxs-lookup"><span data-stu-id="0de4b-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="0de4b-151">Merhaba sqlline.py tooPhoenix bağlanır ve zaman aşımına yapar, çalışma hello aşağıdaki toovalidate hello kullanılabilirlik ve Phoenix durumunu komutu:</span><span class="sxs-lookup"><span data-stu-id="0de4b-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="0de4b-152">Bu komut çalışırsa, sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="0de4b-152">If this command works, there is no issue.</span></span> <span data-ttu-id="0de4b-153">Merhaba kullanıcı tarafından sağlanan başlangıç IP adresi yanlış olabilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="0de4b-154">Merhaba komut uzun bir süre duraklar ve aşağıdaki hata hello görüntüler, ancak toostep 5 devam edin.</span><span class="sxs-lookup"><span data-stu-id="0de4b-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="0de4b-155">Merhaba baş düğümü (hn0) toodiagnose hello durumundan hello Phoenix sistem, komutları aşağıdaki hello çalıştırın. KATALOG tablosu:</span><span class="sxs-lookup"><span data-stu-id="0de4b-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="0de4b-156">Merhaba komutu bir hata benzer toohello aşağıdaki döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0de4b-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="0de4b-157">Hello Ambari UI'da, tüm ZooKeeper düğümleri üzerindeki adımları toorestart hello HMaster hizmeti aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="0de4b-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="0de4b-158">Merhaba, **Özet** bölüm HBase çok Git**HBase** > **etkin HBase ana**.</span><span class="sxs-lookup"><span data-stu-id="0de4b-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="0de4b-159">Merhaba, **bileşenleri** bölümünde, hello HBase ana hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="0de4b-160">Tüm kalan için bu adımları yineleyin **bekleme HBase ana** Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="0de4b-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="0de4b-161">Bu hello HBase ana hizmet toostabilize toofive dakika kaplayan ve hello kurtarma işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="0de4b-162">Birkaç dakika sonra o hello sistem hello sqlline.py komutları tooconfirm yineleyin. Yedekleme KATALOĞU tablodur ve onun sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="0de4b-163">Ne zaman sistem hello. KATALOG tablo geri toonormal, hello bağlantı sorunu tooPhoenix otomatik olarak çözülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="0de4b-164">Ana sunucu toofail toostart nedeni nedir</span><span class="sxs-lookup"><span data-stu-id="0de4b-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="0de4b-165">Hata</span><span class="sxs-lookup"><span data-stu-id="0de4b-165">Error</span></span> 

<span data-ttu-id="0de4b-166">Atomik yeniden adlandırılırken bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="0de4b-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0de4b-167">Ayrıntılı açıklama</span><span class="sxs-lookup"><span data-stu-id="0de4b-167">Detailed description</span></span>

<span data-ttu-id="0de4b-168">Merhaba başlatma işlemi sırasında birçok başlatma adımları HMaster tamamlar.</span><span class="sxs-lookup"><span data-stu-id="0de4b-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="0de4b-169">Veri taşıma (.tmp) hello sıfırdan bunlar toohello veri klasörü.</span><span class="sxs-lookup"><span data-stu-id="0de4b-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="0de4b-170">HMaster yanıt vermeyen bölge sunucuları, varsa hello yazma tamamlanan günlükleri (WALs) klasör toosee da bakar ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="0de4b-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="0de4b-171">Başlatma sırasında temel bir HMaster mu `list` bu klasörlerde komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="0de4b-172">Herhangi bir zamanda bu klasörlerden herhangi biri beklenmeyen bir dosyada HMaster görürse, bir özel durum oluşturur ve başlamıyor.</span><span class="sxs-lookup"><span data-stu-id="0de4b-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="0de4b-173">Olası neden</span><span class="sxs-lookup"><span data-stu-id="0de4b-173">Probable cause</span></span>

<span data-ttu-id="0de4b-174">Hello bölge sunucu günlüklerindeki hello dosya oluşturma tooidentify hello zaman çizelgesi deneyin ve hello saat hello dosya geçici bir işlem kilitlenme oluşturulduğu varsa bakın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="0de4b-175">(HBase destek tooassist başvurun size bunu.) Bu yardımcı olur; böylece basarsa bu hatayı önlemek ve normal işlem kapatmalar olun bize daha sağlam mekanizmaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="0de4b-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0de4b-176">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-176">Resolution steps</span></span>

<span data-ttu-id="0de4b-177">Merhaba çağrı yığını denetleyin ve hangi klasörün hello sorunu neden toodetermine deneyin (örneğin, hello WALs veya hello .tmp klasörünü olabilir).</span><span class="sxs-lookup"><span data-stu-id="0de4b-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="0de4b-178">Cloud Explorer'da ya da HDFS komutlarını kullanarak toolocate hello sorun dosya deneyin.</span><span class="sxs-lookup"><span data-stu-id="0de4b-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="0de4b-179">Genellikle, bu olan bir \*-renamePending.json dosya.</span><span class="sxs-lookup"><span data-stu-id="0de4b-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="0de4b-180">(Merhaba \*-renamePending.json dosyasıdır tooimplement hello Atomik yeniden adlandırma işlemi hello WASB driver'ın kullandığı bir günlük dosyası.</span><span class="sxs-lookup"><span data-stu-id="0de4b-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="0de4b-181">Son toobugs bu uygulamada, bu dosyaları bırakılabilir işlem çökmesi ve benzeri sonra.) Bu dosya Cloud Explorer'da veya HDFS komutlarını kullanarak zorla silme.</span><span class="sxs-lookup"><span data-stu-id="0de4b-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="0de4b-182">Bazen de olabilir aşağıdakine benzer adlı geçici bir dosya *$$$. $$$* bu konumda.</span><span class="sxs-lookup"><span data-stu-id="0de4b-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="0de4b-183">Toouse HDFS sahip `ls` Cloud Explorer hello dosyasında göremiyorum; bu dosya toosee komutu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="0de4b-184">toodelete bu dosya, use hello HDFS komutu `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="0de4b-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="0de4b-185">Bu komutları çalıştırdıktan sonra HMaster hemen başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="0de4b-186">Hata</span><span class="sxs-lookup"><span data-stu-id="0de4b-186">Error</span></span>

<span data-ttu-id="0de4b-187">Hiçbir sunucu adresinin *hbase: meta* bölge xxx için.</span><span class="sxs-lookup"><span data-stu-id="0de4b-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0de4b-188">Ayrıntılı açıklama</span><span class="sxs-lookup"><span data-stu-id="0de4b-188">Detailed description</span></span>

<span data-ttu-id="0de4b-189">Linux kümenizde bu hello belirten bir ileti görebilirsiniz *hbase: meta* tablo çevrimiçi değil.</span><span class="sxs-lookup"><span data-stu-id="0de4b-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="0de4b-190">Çalışan `hbck` , bildirebilir "hbase: meta tablo ReplicaID 0 üzerinde herhangi bir bölgeyi bulunamadı."</span><span class="sxs-lookup"><span data-stu-id="0de4b-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="0de4b-191">HBase yeniden sonra HMaster başlatılamadı Hello sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="0de4b-192">Merhaba HMaster günlüklerinde selamlama iletisine görebilirsiniz: "hiçbir sunucu adresinin hbase: bölge hbase için meta: Yedekleme \<bölge adı\>".</span><span class="sxs-lookup"><span data-stu-id="0de4b-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="0de4b-193">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-193">Resolution steps</span></span>

1. <span data-ttu-id="0de4b-194">Hello HBase kabuğu, komutları (geçerli değişiklik gerçek değerler) aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="0de4b-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="0de4b-195">Merhaba silme *hbase: ad alanı* girişi.</span><span class="sxs-lookup"><span data-stu-id="0de4b-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="0de4b-196">Bu girdi olabilir hello hello zaman raporlandığını aynı hata *hbase: ad alanı* tablo taraması.</span><span class="sxs-lookup"><span data-stu-id="0de4b-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="0de4b-197">HBase hello Ambari kullanıcı Arabirimi, bir çalışan durumunda yukarı toobring hello etkin HMaster hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="0de4b-198">Merhaba HBase kabuğu, tüm çevrimdışı tablolar, Yukarı toobring içinde hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0de4b-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="0de4b-199">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0de4b-199">Additional reading</span></span>

[<span data-ttu-id="0de4b-200">%S tooprocess hello HBase tablo</span><span class="sxs-lookup"><span data-stu-id="0de4b-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="0de4b-201">Hata</span><span class="sxs-lookup"><span data-stu-id="0de4b-201">Error</span></span>

<span data-ttu-id="0de4b-202">HMaster zaman aşımına uğruyor önemli özel durum benzer too"java.io.IOException ile: 300000ms atanan ad alanı tablo toobe için bekleme süresi sona erdi."</span><span class="sxs-lookup"><span data-stu-id="0de4b-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0de4b-203">Ayrıntılı açıklama</span><span class="sxs-lookup"><span data-stu-id="0de4b-203">Detailed description</span></span>

<span data-ttu-id="0de4b-204">Birçok tablolar ve HMaster hizmetlerinizi yeniden başlattığınızda atılmış olan olmayan bölgeleri varsa bu sorunla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="0de4b-205">Yeniden başlatma başarısız olabilir ve hata iletisi önceki hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="0de4b-206">Olası neden</span><span class="sxs-lookup"><span data-stu-id="0de4b-206">Probable cause</span></span>

<span data-ttu-id="0de4b-207">Bu, hello HMaster hizmeti ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="0de4b-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="0de4b-208">Genel küme başlangıç görevleri uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="0de4b-209">Merhaba ad alanı tablo henüz atanmadığından HMaster kapanır.</span><span class="sxs-lookup"><span data-stu-id="0de4b-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="0de4b-210">Bu yalnızca büyük olduğu senaryolarda oluşuyor unflushed veri miktarını var ve beş dakikalık bir zaman aşımı yeterli değil.</span><span class="sxs-lookup"><span data-stu-id="0de4b-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="0de4b-211">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-211">Resolution steps</span></span>

1. <span data-ttu-id="0de4b-212">Hello Ambari UI, çok Git**HBase** > **yapılandırmalar**.</span><span class="sxs-lookup"><span data-stu-id="0de4b-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="0de4b-213">Merhaba özel hbase-site.xml dosyasında ayarı aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0de4b-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="0de4b-214">Gerekli hello Hizmetleri (HMaster ve büyük olasılıkla diğer HBase Hizmetleri) yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="0de4b-215">Bir bölge sunucu üzerinde bir yeniden başlatma hatası nedeni nedir</span><span class="sxs-lookup"><span data-stu-id="0de4b-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="0de4b-216">Sorun</span><span class="sxs-lookup"><span data-stu-id="0de4b-216">Issue</span></span>

<span data-ttu-id="0de4b-217">Bir yeniden başlatma hatası bir bölge sunucuda aşağıdaki en iyi yöntemleri tarafından engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="0de4b-218">Toorestart HBase bölge sunucuları planlarken ağır iş yükü etkinlik duraklatmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="0de4b-219">Shutdown devam ederken uygulama bölge sunucularıyla tooconnect devam ederse, hello bölge sunucu yeniden başlatma işlemi birkaç dakika daha yavaş olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0de4b-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="0de4b-220">Ayrıca, tüm tabloların hello temizleme bir fikir toofirst vardır.</span><span class="sxs-lookup"><span data-stu-id="0de4b-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="0de4b-221">Bir başvurunun nasıl tooflush tablolara bakın [Hdınsight HBase: nasıl tooimprove hello HBase kümesi yeniden zaman tabloları temizlenerek](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="0de4b-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="0de4b-222">Merhaba yeniden başlatma işlemi HBase bölge sunucularından hello Ambari UI'ı başlattığınızda, hello bölge sunucuları kapandı, ancak hemen yeniden başlatma hemen bakın.</span><span class="sxs-lookup"><span data-stu-id="0de4b-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="0de4b-223">Merhaba arka planda neler olduğunu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0de4b-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="0de4b-224">Merhaba Ambari aracı bir durdurma isteği toohello bölge sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="0de4b-225">Merhaba Ambari Aracısı düzgün bir şekilde hello bölge sunucu tooshut için 30 saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="0de4b-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="0de4b-226">Uygulamanızı hello bölge sunucusuyla tooconnect devam ederse, hello sunucu hemen kapatmak olmaz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="0de4b-227">kapatma oluşmadan önce hello 30 saniyelik zaman aşımı süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="0de4b-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="0de4b-228">30 saniye sonra hello Ambari aracı zorla KILL gönderir (`kill -9`) komutu toohello bölge sunucu.</span><span class="sxs-lookup"><span data-stu-id="0de4b-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="0de4b-229">(Dizininde hello /var/günlük/hello ilgili çalışan düğümünün) hello ambari Aracısı günlüğünde görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0de4b-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="0de4b-230">Merhaba bölge sunucu işlemi durdurulmuş olsa bile hello ani kapatma nedeniyle hello işlemle ilişkili hello bağlantı noktası, yayımlanmamış.</span><span class="sxs-lookup"><span data-stu-id="0de4b-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="0de4b-231">Merhaba bölge sunucusu başlatıldığında, bu durum tooan AddressBindException hello günlükleri aşağıdaki gösterildiği gibi yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="0de4b-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="0de4b-232">Merhaba bölge-server.log burada hello bölge sunucu toostart başarısız hello çalışan düğümleri hello /var/log/hbase dizininde içinde doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0de4b-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="0de4b-233">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="0de4b-233">Resolution steps</span></span>

1. <span data-ttu-id="0de4b-234">Yeniden başlatmadan önce tooreduce hello yük hello HBase bölge sunucularda deneyin.</span><span class="sxs-lookup"><span data-stu-id="0de4b-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="0de4b-235">Alternatif olarak (1. Adım Yardım değil ise), aşağıdaki hello çalışan düğümleri kullanarak sunucularda hello try toomanually yeniden bölge komutlar:</span><span class="sxs-lookup"><span data-stu-id="0de4b-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

