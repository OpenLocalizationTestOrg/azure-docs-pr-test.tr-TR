---
title: "Azure Hdınsight kullanarak HDFS aaaTroubleshoot | Microsoft Docs"
description: "HDFS ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
keywords: "Azure Hdınsight, HDFS, SSS, sorun giderme kılavuzu, sık sorulan sorular"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 4C33828F-2982-47F0-B858-C32FFF634D9E
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: f5adec6879c947fcff82112e95d9d0303592c834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hdfs-by-using-azure-hdinsight"></a><span data-ttu-id="69850-104">HDFS Azure Hdınsight kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="69850-104">Troubleshoot HDFS by using Azure HDInsight</span></span>

<span data-ttu-id="69850-105">Apache Ambari Hadoop dağıtılmış dosya sistemi (HDFS) yükleri ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="69850-105">Learn about hello top issues and their resolutions when working with Hadoop Distributed File System (HDFS) payloads in Apache Ambari.</span></span>

## <span data-ttu-id="69850-106"><a name="how-do-i-access-local-hdfs-from-inside-a-cluster"></a>Ne erişebilirim gelen yerel HDFS bir küme içindeki hello</span><span class="sxs-lookup"><span data-stu-id="69850-106"><a name="how-do-i-access-local-hdfs-from-inside-a-cluster"></a>How do I access hello local HDFS from inside a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="69850-107">Sorun</span><span class="sxs-lookup"><span data-stu-id="69850-107">Issue</span></span>

<span data-ttu-id="69850-108">Azure Blob Depolama veya Itanium tabanlı sistemler için Azure Data Lake Deposu'ndan veri içinde kullanarak komut satırı ve uygulama kodu yerine yerel HDFS gelen hello erişim hello hello Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="69850-108">Access hello local HDFS from hello command line and application code instead of by using Azure Blob storage or Azure Data Lake Store from inside hello HDInsight cluster.</span></span>   

### <a name="resolution-steps"></a><span data-ttu-id="69850-109">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="69850-109">Resolution steps</span></span>

1. <span data-ttu-id="69850-110">Merhaba komut isteminden `hdfs dfs -D "fs.default.name=hdfs://mycluster/" ...` tam anlamıyla, komutu aşağıdaki hello olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="69850-110">At hello command prompt, use `hdfs dfs -D "fs.default.name=hdfs://mycluster/" ...` literally, as in hello following command:</span></span>

    ```apache
    hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -ls /
    Found 3 items
    drwxr-xr-x   - hdiuser hdfs          0 2017-03-24 14:12 /EventCheckpoint-30-8-24-11102016-01
    drwx-wx-wx   - hive    hdfs          0 2016-11-10 18:42 /tmp
    drwx------   - hdiuser hdfs          0 2016-11-10 22:22 /user
    ```

2. <span data-ttu-id="69850-111">Kaynak kodundan hello URI kullanmak `hdfs://mycluster/` tam anlamıyla, örnek uygulama aşağıdaki hello olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="69850-111">From source code, use hello URI `hdfs://mycluster/` literally, as in hello following sample application:</span></span>

    ```csharp
    import java.io.IOException;
    import java.net.URI;
    import org.apache.commons.io.IOUtils;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.*;

    public class JavaUnitTests {

        public static void main(String[] args) throws Exception {

            Configuration conf = new Configuration();
            String hdfsUri = "hdfs://mycluster/";
            conf.set("fs.defaultFS", hdfsUri);
            FileSystem fileSystem = FileSystem.get(URI.create(hdfsUri), conf);
            RemoteIterator<LocatedFileStatus> fileStatusIterator = fileSystem.listFiles(new Path("/tmp"), true);
            while(fileStatusIterator.hasNext()) {
                System.out.println(fileStatusIterator.next().getPath().toString());
            }
        }
    }
    ```

3. <span data-ttu-id="69850-112">Çalışma hello derlenmiş .jar dosyasına (örneğin, adında bir dosya `java-unit-tests-1.0.jar`) hello Hdınsight üzerinde komutu aşağıdaki hello ile küme:</span><span class="sxs-lookup"><span data-stu-id="69850-112">Run hello compiled .jar file (for example, a file named `java-unit-tests-1.0.jar`) on hello HDInsight cluster with hello following command:</span></span>

    ```apache
    hdiuser@hn0-spark2:~$ hadoop jar java-unit-tests-1.0.jar JavaUnitTests
    hdfs://mycluster/tmp/hive/hive/5d9cf301-2503-48c7-9963-923fb5ef79a7/inuse.info
    hdfs://mycluster/tmp/hive/hive/5d9cf301-2503-48c7-9963-923fb5ef79a7/inuse.lck
    hdfs://mycluster/tmp/hive/hive/a0be04ea-ae01-4cc4-b56d-f263baf2e314/inuse.info
    hdfs://mycluster/tmp/hive/hive/a0be04ea-ae01-4cc4-b56d-f263baf2e314/inuse.lck
    ```


## <span data-ttu-id="69850-113"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Nasıl ı zorla-küme güvenli modda HDFS devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="69850-113"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="69850-114">Sorun</span><span class="sxs-lookup"><span data-stu-id="69850-114">Issue</span></span>

<span data-ttu-id="69850-115">Merhaba yerel HDFS hello Hdınsight kümesinde güvenli modda takıldı.</span><span class="sxs-lookup"><span data-stu-id="69850-115">hello local HDFS is stuck in safe mode on hello HDInsight cluster.</span></span>   

### <a name="detailed-description"></a><span data-ttu-id="69850-116">Ayrıntılı açıklama</span><span class="sxs-lookup"><span data-stu-id="69850-116">Detailed description</span></span>

<span data-ttu-id="69850-117">HDFS komutu aşağıdaki hello çalıştırdığınızda hatası oluşur:</span><span class="sxs-lookup"><span data-stu-id="69850-117">Failure occurs when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="69850-118">Merhaba komutu çalıştırdığınızda aşağıdaki hata hello bakın:</span><span class="sxs-lookup"><span data-stu-id="69850-118">You see hello following error when you run hello command:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="69850-119">Olası neden</span><span class="sxs-lookup"><span data-stu-id="69850-119">Probable cause</span></span>

<span data-ttu-id="69850-120">Merhaba Hdınsight kümesi bırakıldı tooa çok az sayıda düğüm ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="69850-120">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="69850-121">düğüm sayısını Hello aşağıdadır veya toohello HDFS çoğaltma faktörü kapatın.</span><span class="sxs-lookup"><span data-stu-id="69850-121">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="69850-122">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="69850-122">Resolution steps</span></span> 

1. <span data-ttu-id="69850-123">HDFS Hello durumunu hello Hdınsight kümesinde hello aşağıdaki komutları kullanarak alın:</span><span class="sxs-lookup"><span data-stu-id="69850-123">Get hello status of HDFS on hello HDInsight cluster by using hello following commands:</span></span>

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

2. <span data-ttu-id="69850-124">HDFS Hello bütünlüğünü hello Hdınsight kümesinde hello aşağıdaki komutları kullanarak denetleyin:</span><span class="sxs-lookup"><span data-stu-id="69850-124">Check hello integrity of HDFS on hello HDInsight cluster by using hello following commands:</span></span>

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

3. <span data-ttu-id="69850-125">Hiçbir eksik, bozuk veya under-çoğaltılmış bloğu yok veya bu blokları yoksayılabilir karar verirseniz, komut tootake hello adı düğümünü güvenli mod dışında izleyen hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="69850-125">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

    ```apache
    hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
    ```
