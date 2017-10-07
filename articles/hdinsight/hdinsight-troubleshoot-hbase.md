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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Azure Hdınsight kullanarak HBase sorun giderme

Apache Ambari, Apache HBase yükü ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Birden çok atanmamış bölgeleri ile nasıl hbck komutu raporları çalıştırılsın mı

Merhaba çalıştırdığınızda görebilirsiniz genel bir hata iletisi `hbase hbck` komuttur "birden çok atanmamış bölgeler veya Delik bölgelerinin hello zincirindeki."

Hello HBase ana UI'da, tüm bölge sunuculara dengesini bölgeler hello sayısını görebilirsiniz. Daha sonra çalıştırabilirsiniz `hbase hbck` toosee delik hello bölge zincirindeki komutu.

Delik hello çevrimdışı bölgeleri, bunu düzeltme hello atamaları ilk kaynaklanıyor olabilir. 

toobring atanmamış bölgeleri arka tooa normal durum Merhaba, hello aşağıdaki adımları tamamlayın:

1. SSH kullanarak Hdınsight HBase kümesi içinde toohello imzalayın.
2. Merhaba çalıştırmak hello ZooKeeper kabuğu ile tooconnect `hbase zkcli` komutu.
3. Merhaba çalıştırmak `rmr /hbase/regions-in-transition` komut veya hello `rmr /hbase-unsecure/regions-in-transition` komutu.
4. Merhaba gelen tooexit `hbase zkcli` Kabuk, hello kullan `exit` komutu.
5. Merhaba Apache Ambari UI açın ve ardından hello etkin HBase ana hizmetini yeniden başlatın.
6. Merhaba çalıştırmak `hbase hbck` komutunu yeniden (seçenekleri olmadan). Tüm bölgeler atanan bu komut tooensure Hello çıktısını denetleyin.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Zaman aşımı sorunları nasıl hbck komutlarını bölge atamaları kullanırken düzeltme

### <a name="issue"></a>Sorun

Merhaba kullandığınızda zaman aşımı sorunlarıyla ilgili olası bir nedeni `hbck` komutu, birkaç bölgeler hello "geçiş" olduğundan emin olabilir uzun bir süre için durum. Bu bölgeler hello HBase ana UI çevrimdışı olarak görebilirsiniz. Çok sayıda bölgeleri tootransition denediğinizden HBase ana zaman aşımı olabilir ve bu bölgeler tekrar çevrimiçi oluşturulamıyor toobring olmalıdır.

### <a name="resolution-steps"></a>Çözüm adımları

1. SSH kullanarak Hdınsight HBase kümesi içinde toohello imzalayın.
2. Merhaba çalıştırmak hello ZooKeeper kabuğu ile tooconnect `hbase zkcli` komutu.
3. Merhaba çalıştırmak `rmr /hbase/regions-in-transition` veya hello `rmr /hbase-unsecure/regions-in-transition` komutu.
4. tooexit hello `hbase zkcli` Kabuk, hello kullan `exit` komutu.
5. Hello Ambari UI, hello etkin HBase ana hizmetini yeniden başlatın.
6. Merhaba çalıştırmak `hbase hbck -fixAssignments` yeniden komutu.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Nasıl ı zorla-küme güvenli modda HDFS devre dışı bırak

### <a name="issue"></a>Sorun

Merhaba yerel Hadoop dağıtılmış dosya sistemi (HDFS) hello Hdınsight kümesinde güvenli modda takıldı.

### <a name="detailed-description"></a>Ayrıntılı açıklama

HDFS komutu aşağıdaki hello çalıştırdığınızda bu hata bir hatadan kaynaklanıyor:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

Merhaba hata toorun hello komutu çalıştığınızda görebilirsiniz şöyle görünür:

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

### <a name="probable-cause"></a>Olası neden

Merhaba Hdınsight kümesi bırakıldı tooa çok az sayıda düğüm ölçeklendirilebilir. düğüm sayısını Hello aşağıdadır veya toohello HDFS çoğaltma faktörü kapatın.

### <a name="resolution-steps"></a>Çözüm adımları 

1. Merhaba Hdınsight üzerinde HDFS hello aşağıdaki komutları çalıştırarak küme hello Hello durumunu alın:

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
2. HDFS hello Hdınsight üzerinde aşağıdaki komutları hello kullanarak küme hello hello bütünlüğünü de denetleyebilirsiniz:

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

3. Hiçbir eksik, bozuk veya under-çoğaltılmış bloğu yok veya bu blokları yoksayılabilir karar verirseniz, komut tootake hello adı düğümünü güvenli mod dışında izleyen hello çalıştırın:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Nasıl JDBC veya SQLLine bağlantısı düzeltirim Apache Phoenix ile ilgili sorunları

### <a name="resolution-steps"></a>Çözüm adımları

tooconnect Phoenix ile başlangıç IP adresi etkin ZooKeeper düğümün sağlamanız gerekir. Bu hello ZooKeeper hizmet toowhich sqlline.py çalışıyor olun tooconnect olan hazır ve çalışır.
1. İçinde toohello, SSH kullanarak Hdınsight kümesi oturum açın.
2. Merhaba aşağıdaki komutu girin:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Başlangıç IP adresi hello etkin ZooKeeper düğümünün hello Ambari UI ' alabilirsiniz. Çok Git**HBase** > **hızlı bağlantılar** > **ZK\* (etkin)** > **Zookeeper bilgisi**. 

3. Merhaba sqlline.py tooPhoenix bağlanır ve zaman aşımına yapar, çalışma hello aşağıdaki toovalidate hello kullanılabilirlik ve Phoenix durumunu komutu:

   ```apache
           !tables
           !quit
   ```      
4. Bu komut çalışırsa, sorun yoktur. Merhaba kullanıcı tarafından sağlanan başlangıç IP adresi yanlış olabilir. Merhaba komut uzun bir süre duraklar ve aşağıdaki hata hello görüntüler, ancak toostep 5 devam edin.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Merhaba baş düğümü (hn0) toodiagnose hello durumundan hello Phoenix sistem, komutları aşağıdaki hello çalıştırın. KATALOG tablosu:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   Merhaba komutu bir hata benzer toohello aşağıdaki döndürmesi gerekir: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Hello Ambari UI'da, tüm ZooKeeper düğümleri üzerindeki adımları toorestart hello HMaster hizmeti aşağıdaki hello tamamlayın:

    1. Merhaba, **Özet** bölüm HBase çok Git**HBase** > **etkin HBase ana**. 
    2. Merhaba, **bileşenleri** bölümünde, hello HBase ana hizmetini yeniden başlatın.
    3. Tüm kalan için bu adımları yineleyin **bekleme HBase ana** Hizmetleri. 

Bu hello HBase ana hizmet toostabilize toofive dakika kaplayan ve hello kurtarma işlemini tamamlayın. Birkaç dakika sonra o hello sistem hello sqlline.py komutları tooconfirm yineleyin. Yedekleme KATALOĞU tablodur ve onun sorgulanabilir. 

Ne zaman sistem hello. KATALOG tablo geri toonormal, hello bağlantı sorunu tooPhoenix otomatik olarak çözülmesi gerekir.


## <a name="what-causes-a-master-server-toofail-toostart"></a>Ana sunucu toofail toostart nedeni nedir

### <a name="error"></a>Hata 

Atomik yeniden adlandırılırken bir hata oluşur.

### <a name="detailed-description"></a>Ayrıntılı açıklama

Merhaba başlatma işlemi sırasında birçok başlatma adımları HMaster tamamlar. Veri taşıma (.tmp) hello sıfırdan bunlar toohello veri klasörü. HMaster yanıt vermeyen bölge sunucuları, varsa hello yazma tamamlanan günlükleri (WALs) klasör toosee da bakar ve benzeri. 

Başlatma sırasında temel bir HMaster mu `list` bu klasörlerde komutu. Herhangi bir zamanda bu klasörlerden herhangi biri beklenmeyen bir dosyada HMaster görürse, bir özel durum oluşturur ve başlamıyor.  

### <a name="probable-cause"></a>Olası neden

Hello bölge sunucu günlüklerindeki hello dosya oluşturma tooidentify hello zaman çizelgesi deneyin ve hello saat hello dosya geçici bir işlem kilitlenme oluşturulduğu varsa bakın. (HBase destek tooassist başvurun size bunu.) Bu yardımcı olur; böylece basarsa bu hatayı önlemek ve normal işlem kapatmalar olun bize daha sağlam mekanizmaları sağlar.

### <a name="resolution-steps"></a>Çözüm adımları

Merhaba çağrı yığını denetleyin ve hangi klasörün hello sorunu neden toodetermine deneyin (örneğin, hello WALs veya hello .tmp klasörünü olabilir). Cloud Explorer'da ya da HDFS komutlarını kullanarak toolocate hello sorun dosya deneyin. Genellikle, bu olan bir \*-renamePending.json dosya. (Merhaba \*-renamePending.json dosyasıdır tooimplement hello Atomik yeniden adlandırma işlemi hello WASB driver'ın kullandığı bir günlük dosyası. Son toobugs bu uygulamada, bu dosyaları bırakılabilir işlem çökmesi ve benzeri sonra.) Bu dosya Cloud Explorer'da veya HDFS komutlarını kullanarak zorla silme. 

Bazen de olabilir aşağıdakine benzer adlı geçici bir dosya *$$$. $$$* bu konumda. Toouse HDFS sahip `ls` Cloud Explorer hello dosyasında göremiyorum; bu dosya toosee komutu. toodelete bu dosya, use hello HDFS komutu `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Bu komutları çalıştırdıktan sonra HMaster hemen başlamanız gerekir. 

### <a name="error"></a>Hata

Hiçbir sunucu adresinin *hbase: meta* bölge xxx için.

### <a name="detailed-description"></a>Ayrıntılı açıklama

Linux kümenizde bu hello belirten bir ileti görebilirsiniz *hbase: meta* tablo çevrimiçi değil. Çalışan `hbck` , bildirebilir "hbase: meta tablo ReplicaID 0 üzerinde herhangi bir bölgeyi bulunamadı." HBase yeniden sonra HMaster başlatılamadı Hello sorun olabilir. Merhaba HMaster günlüklerinde selamlama iletisine görebilirsiniz: "hiçbir sunucu adresinin hbase: bölge hbase için meta: Yedekleme \<bölge adı\>".  

### <a name="resolution-steps"></a>Çözüm adımları

1. Hello HBase kabuğu, komutları (geçerli değişiklik gerçek değerler) aşağıdaki hello girin:  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Merhaba silme *hbase: ad alanı* girişi. Bu girdi olabilir hello hello zaman raporlandığını aynı hata *hbase: ad alanı* tablo taraması.

3. HBase hello Ambari kullanıcı Arabirimi, bir çalışan durumunda yukarı toobring hello etkin HMaster hizmetini yeniden başlatın.  

4. Merhaba HBase kabuğu, tüm çevrimdışı tablolar, Yukarı toobring içinde hello aşağıdaki komutu çalıştırın:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Ek kaynaklar

[%S tooprocess hello HBase tablo](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Hata

HMaster zaman aşımına uğruyor önemli özel durum benzer too"java.io.IOException ile: 300000ms atanan ad alanı tablo toobe için bekleme süresi sona erdi."

### <a name="detailed-description"></a>Ayrıntılı açıklama

Birçok tablolar ve HMaster hizmetlerinizi yeniden başlattığınızda atılmış olan olmayan bölgeleri varsa bu sorunla karşılaşabilirsiniz. Yeniden başlatma başarısız olabilir ve hata iletisi önceki hello görürsünüz.  

### <a name="probable-cause"></a>Olası neden

Bu, hello HMaster hizmeti ile bilinen bir sorundur. Genel küme başlangıç görevleri uzun sürebilir. Merhaba ad alanı tablo henüz atanmadığından HMaster kapanır. Bu yalnızca büyük olduğu senaryolarda oluşuyor unflushed veri miktarını var ve beş dakikalık bir zaman aşımı yeterli değil.
  
### <a name="resolution-steps"></a>Çözüm adımları

1. Hello Ambari UI, çok Git**HBase** > **yapılandırmalar**. Merhaba özel hbase-site.xml dosyasında ayarı aşağıdaki hello ekleyin: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Gerekli hello Hizmetleri (HMaster ve büyük olasılıkla diğer HBase Hizmetleri) yeniden başlatın.  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Bir bölge sunucu üzerinde bir yeniden başlatma hatası nedeni nedir

### <a name="issue"></a>Sorun

Bir yeniden başlatma hatası bir bölge sunucuda aşağıdaki en iyi yöntemleri tarafından engellenebilir. Toorestart HBase bölge sunucuları planlarken ağır iş yükü etkinlik duraklatmak öneririz. Shutdown devam ederken uygulama bölge sunucularıyla tooconnect devam ederse, hello bölge sunucu yeniden başlatma işlemi birkaç dakika daha yavaş olacaktır. Ayrıca, tüm tabloların hello temizleme bir fikir toofirst vardır. Bir başvurunun nasıl tooflush tablolara bakın [Hdınsight HBase: nasıl tooimprove hello HBase kümesi yeniden zaman tabloları temizlenerek](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Merhaba yeniden başlatma işlemi HBase bölge sunucularından hello Ambari UI'ı başlattığınızda, hello bölge sunucuları kapandı, ancak hemen yeniden başlatma hemen bakın. 

Merhaba arka planda neler olduğunu aşağıda verilmiştir: 

1. Merhaba Ambari aracı bir durdurma isteği toohello bölge sunucusuna gönderir.
2. Merhaba Ambari Aracısı düzgün bir şekilde hello bölge sunucu tooshut için 30 saniye bekler. 
3. Uygulamanızı hello bölge sunucusuyla tooconnect devam ederse, hello sunucu hemen kapatmak olmaz. kapatma oluşmadan önce hello 30 saniyelik zaman aşımı süresi dolar. 
4. 30 saniye sonra hello Ambari aracı zorla KILL gönderir (`kill -9`) komutu toohello bölge sunucu. (Dizininde hello /var/günlük/hello ilgili çalışan düğümünün) hello ambari Aracısı günlüğünde görebilirsiniz:

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
Merhaba bölge sunucu işlemi durdurulmuş olsa bile hello ani kapatma nedeniyle hello işlemle ilişkili hello bağlantı noktası, yayımlanmamış. Merhaba bölge sunucusu başlatıldığında, bu durum tooan AddressBindException hello günlükleri aşağıdaki gösterildiği gibi yol açabilir. Merhaba bölge-server.log burada hello bölge sunucu toostart başarısız hello çalışan düğümleri hello /var/log/hbase dizininde içinde doğrulayabilirsiniz. 

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

### <a name="resolution-steps"></a>Çözüm adımları

1. Yeniden başlatmadan önce tooreduce hello yük hello HBase bölge sunucularda deneyin. 
2. Alternatif olarak (1. Adım Yardım değil ise), aşağıdaki hello çalışan düğümleri kullanarak sunucularda hello try toomanually yeniden bölge komutlar:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

