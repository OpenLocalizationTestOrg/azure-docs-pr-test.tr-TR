---
title: "Python bileşenleri - Azure Hdınsight ile aaaApache Storm | Microsoft Docs"
description: "Bilgi nasıl toocreate Python bileşenleri kullanan bir Apache Storm topolojisini."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: Apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="3dfde-104">Python kullanarak Hdınsight üzerinde Apache Storm topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="3dfde-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="3dfde-105">Bilgi nasıl toocreate Python bileşenleri kullanan bir Apache Storm topolojisini.</span><span class="sxs-lookup"><span data-stu-id="3dfde-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="3dfde-106">Apache Storm, bir topoloji çeşitli dillerde toocombine bileşenlerini izin verme bile birden çok dili destekler.</span><span class="sxs-lookup"><span data-stu-id="3dfde-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="3dfde-107">Merhaba (0.10.0 Storm ile sunulan) Flux framework sağlar tooeasily Python bileşenleri kullanan çözümler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3dfde-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dfde-108">Bu belgedeki bilgiler Hello Hdınsight 3.6 üzerinde Storm kullanılarak test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="3dfde-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3dfde-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3dfde-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="3dfde-111">Bu proje için Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="3dfde-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dfde-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3dfde-112">Prerequisites</span></span>

* <span data-ttu-id="3dfde-113">Python 2.7 ya da daha yüksek</span><span class="sxs-lookup"><span data-stu-id="3dfde-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="3dfde-114">Java JDK 1.8 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="3dfde-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="3dfde-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="3dfde-115">Maven 3</span></span>

* <span data-ttu-id="3dfde-116">(İsteğe bağlı) Yerel bir Storm geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="3dfde-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="3dfde-117">Yerel olarak toorun hello topoloji isterseniz, yerel bir Storm ortam yalnızca gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="3dfde-118">Daha fazla bilgi için bkz: [bir geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="3dfde-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="3dfde-119">Storm çoklu dil desteği</span><span class="sxs-lookup"><span data-stu-id="3dfde-119">Storm multi-language support</span></span>

<span data-ttu-id="3dfde-120">Apache Storm bileşenleri herhangi bir programlama dili kullanılarak yazılmış ile tasarlanmış toowork oluştu.</span><span class="sxs-lookup"><span data-stu-id="3dfde-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="3dfde-121">gereken Hello bileşenlerini anlama nasıl hello ile toowork [Thrift tanımıdır Storm için](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="3dfde-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="3dfde-122">Python için bir modül Storm tooeasily arabirim sağlayan hello Apache Storm projesinin bir parçası olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3dfde-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="3dfde-123">Bu modülü bulabilirsiniz [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="3dfde-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="3dfde-124">Storm Java sanal makine (JVM) hello üzerinde çalışan Java bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="3dfde-125">Diğer dillerde yazılmış bileşenleri alt yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3dfde-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="3dfde-126">Merhaba Storm stdin/stdout gönderilen JSON iletileri kullanarak bu alt iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="3dfde-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="3dfde-127">Hello bileşenleri arasındaki iletişim hakkında daha fazla ayrıntı bulunabilir [çoklu dil Protokolü](https://storm.apache.org/documentation/Multilang-protocol.html) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="3dfde-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="3dfde-128">Python hello Flux framework ile</span><span class="sxs-lookup"><span data-stu-id="3dfde-128">Python with hello Flux framework</span></span>

<span data-ttu-id="3dfde-129">Merhaba Flux framework toodefine Storm topolojilerini hello bileşenlerinden ayrı olarak verir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="3dfde-130">Merhaba Flux framework YAML toodefine hello Storm topolojisini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3dfde-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="3dfde-131">Merhaba aşağıdaki nasıl bir örnek metindir tooreference hello YAML belge Python bileşeninde:</span><span class="sxs-lookup"><span data-stu-id="3dfde-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="3dfde-132">Merhaba sınıfı `FluxShellSpout` kullanılan toostart hello olduğu `sentencespout.py` hello spout uygulayan komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="3dfde-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="3dfde-133">Flux bekliyor hello Python komut dosyaları toobe hello `/resources` hello topoloji içeren hello jar dosyasını içinde dizin.</span><span class="sxs-lookup"><span data-stu-id="3dfde-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="3dfde-134">Bu örnek hello hello Python betiklerini depolamasının `/multilang/resources` dizin.</span><span class="sxs-lookup"><span data-stu-id="3dfde-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="3dfde-135">Merhaba `pom.xml` XML aşağıdaki hello kullanarak bu dosyayı içerir:</span><span class="sxs-lookup"><span data-stu-id="3dfde-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="3dfde-136">Daha önce belirtildiği gibi bir `storm.py` hello Thrift tanımıdır Storm için uygulayan dosyası.</span><span class="sxs-lookup"><span data-stu-id="3dfde-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="3dfde-137">Merhaba Flux framework içerir `storm.py` otomatik olarak zaman hello projesi yapılandırıldığında, bunu dahil olmak üzere ilgili tooworry gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3dfde-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="3dfde-138">Merhaba projeyi derleme</span><span class="sxs-lookup"><span data-stu-id="3dfde-138">Build hello project</span></span>

<span data-ttu-id="3dfde-139">Merhaba proje Hello kökünden hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3dfde-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="3dfde-140">Bu komut oluşturur bir `target/WordCount-1.0-SNAPSHOT.jar` hello içeren dosya derlenmiş topolojisi.</span><span class="sxs-lookup"><span data-stu-id="3dfde-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="3dfde-141">Merhaba topoloji yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3dfde-141">Run hello topology locally</span></span>

<span data-ttu-id="3dfde-142">toorun hello yerel olarak topoloji hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3dfde-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="3dfde-143">Bu komut, bir yerel Storm geliştirme ortamını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="3dfde-144">Daha fazla bilgi için bkz: [bir geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="3dfde-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="3dfde-145">Bir kez hello topolojisini başlatır, bilgi toohello yerel konsol benzer toohello metin aşağıdaki gösterir:</span><span class="sxs-lookup"><span data-stu-id="3dfde-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="3dfde-146">toostop hello topoloji, kullanım __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="3dfde-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="3dfde-147">Hdınsight üzerinde Hello Storm topolojisini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3dfde-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="3dfde-148">Kullanım hello şu komutu toocopy hello `WordCount-1.0-SNAPSHOT.jar` Hdınsight kümesinde Storm tooyour dosya:</span><span class="sxs-lookup"><span data-stu-id="3dfde-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3dfde-149">Değiştir `sshuser` kümenizin hello SSH kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="3dfde-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="3dfde-150">Değiştir `mycluster` hello küme adı ile.</span><span class="sxs-lookup"><span data-stu-id="3dfde-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="3dfde-151">İstendiğinde tooenter hello hello SSH kullanıcı parolasını olabilir.</span><span class="sxs-lookup"><span data-stu-id="3dfde-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="3dfde-152">SSH ve SCP kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3dfde-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3dfde-153">Hello dosya karşıya yüklendikten sonra SSH kullanarak toohello kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="3dfde-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="3dfde-154">Merhaba SSH oturumundan komutu toostart hello topoloji hello kümede aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3dfde-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="3dfde-155">Merhaba kümede hello Storm kullanıcı Arabirimi tooview hello topoloji kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3dfde-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="3dfde-156">Merhaba Storm kullanıcı Arabirimi https://mycluster.azurehdinsight.net/stormui bulunur.</span><span class="sxs-lookup"><span data-stu-id="3dfde-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="3dfde-157">Değiştir `mycluster` küme adıyla.</span><span class="sxs-lookup"><span data-stu-id="3dfde-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="3dfde-158">Başladıktan sonra Storm topolojisini durdurulana kadar çalışır.</span><span class="sxs-lookup"><span data-stu-id="3dfde-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="3dfde-159">toostop topoloji Merhaba, yöntemler aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="3dfde-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="3dfde-160">Merhaba `storm kill TOPOLOGYNAME` hello komut satırından komutu</span><span class="sxs-lookup"><span data-stu-id="3dfde-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="3dfde-161">Merhaba **KILL** düğmesini hello Storm kullanıcı Arabirimi.</span><span class="sxs-lookup"><span data-stu-id="3dfde-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3dfde-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3dfde-162">Next steps</span></span>

<span data-ttu-id="3dfde-163">Belgeleri diğer yolları toouse Hdınsight ile Python için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="3dfde-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="3dfde-164">Nasıl MapReduce işleri akış için Python toouse</span><span class="sxs-lookup"><span data-stu-id="3dfde-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="3dfde-165">Nasıl toouse Python kullanıcı tanımlı işlevler (UDF), Pig ve Hive</span><span class="sxs-lookup"><span data-stu-id="3dfde-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
