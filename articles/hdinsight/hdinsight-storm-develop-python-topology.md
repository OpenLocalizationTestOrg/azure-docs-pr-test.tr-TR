---
title: "Apache Storm Python bileşenleri - Azure Hdınsight ile | Microsoft Docs"
description: "Python bileşenleri kullanan bir Apache Storm topolojisini oluşturmayı öğrenin."
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
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="d93b9-104">Python kullanarak Hdınsight üzerinde Apache Storm topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="d93b9-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="d93b9-105">Python bileşenleri kullanan bir Apache Storm topolojisini oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d93b9-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="d93b9-106">Apache Storm, bile, bir topoloji çeşitli dillerde bileşenlerini birleştirmenize izin vererek birden çok dili destekler.</span><span class="sxs-lookup"><span data-stu-id="d93b9-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="d93b9-107">(0.10.0 Storm ile sunulan) Flux framework Python bileşenleri kullanan çözümler kolayca oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d93b9-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d93b9-108">Bu belgedeki bilgiler Hdınsight 3.6 üzerinde Storm kullanılarak test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d93b9-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="d93b9-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="d93b9-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d93b9-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d93b9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d93b9-111">Bu proje için kod şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="d93b9-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d93b9-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d93b9-112">Prerequisites</span></span>

* <span data-ttu-id="d93b9-113">Python 2.7 ya da daha yüksek</span><span class="sxs-lookup"><span data-stu-id="d93b9-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="d93b9-114">Java JDK 1.8 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="d93b9-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="d93b9-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="d93b9-115">Maven 3</span></span>

* <span data-ttu-id="d93b9-116">(İsteğe bağlı) Yerel bir Storm geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="d93b9-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="d93b9-117">Yerel bir Storm ortam yalnızca topoloji yerel olarak çalıştırmak istiyorsanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d93b9-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="d93b9-118">Daha fazla bilgi için bkz: [bir geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="d93b9-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="d93b9-119">Storm çoklu dil desteği</span><span class="sxs-lookup"><span data-stu-id="d93b9-119">Storm multi-language support</span></span>

<span data-ttu-id="d93b9-120">Apache Storm, herhangi bir programlama dili kullanılarak yazılmış bileşenleriyle çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d93b9-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="d93b9-121">Bileşenleri ile nasıl çalışılacağını anlamalısınız [Thrift tanımıdır Storm için](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="d93b9-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="d93b9-122">Python için bir modül Storm ile kolayca arabirim sayesinde Apache Storm projenin bir parçası olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d93b9-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="d93b9-123">Bu modülü bulabilirsiniz [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="d93b9-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="d93b9-124">Storm Java sanal makine (JVM) üzerinde çalışan Java bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d93b9-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="d93b9-125">Diğer dillerde yazılmış bileşenleri alt yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d93b9-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="d93b9-126">Storm stdin/stdout gönderilen JSON iletileri kullanarak bu alt iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="d93b9-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="d93b9-127">Bileşenleri arasındaki iletişim hakkında daha fazla ayrıntı bulunabilir [çoklu dil Protokolü](https://storm.apache.org/documentation/Multilang-protocol.html) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="d93b9-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="d93b9-128">Python Flux framework ile</span><span class="sxs-lookup"><span data-stu-id="d93b9-128">Python with the Flux framework</span></span>

<span data-ttu-id="d93b9-129">Flux framework Storm topolojilerini Bileşenler'den ayrı olarak tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d93b9-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="d93b9-130">Flux framework YAML Storm topolojisini tanımlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d93b9-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="d93b9-131">Aşağıdaki metni YAML belge Python bileşeninde başvurmak nasıl örneğidir:</span><span class="sxs-lookup"><span data-stu-id="d93b9-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

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

<span data-ttu-id="d93b9-132">Sınıf `FluxShellSpout` başlatmak için kullanılan `sentencespout.py` spout uygulayan komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="d93b9-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="d93b9-133">Flux bekliyor olması için Python komut dosyaları `/resources` topoloji içeren jar dosyasını içinde dizin.</span><span class="sxs-lookup"><span data-stu-id="d93b9-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="d93b9-134">Bu örnek Python komut dosyalarında depolamasının `/multilang/resources` dizin.</span><span class="sxs-lookup"><span data-stu-id="d93b9-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="d93b9-135">`pom.xml` Bu dosyayı aşağıdaki XML kullanarak içerir:</span><span class="sxs-lookup"><span data-stu-id="d93b9-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="d93b9-136">Daha önce belirtildiği gibi bir `storm.py` Storm Thrift tanımıdır uygulayan dosyası.</span><span class="sxs-lookup"><span data-stu-id="d93b9-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="d93b9-137">Flux framework içerir `storm.py` otomatik olarak zaman projesi yapılandırıldığında, böylece dahil hakkında endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d93b9-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="d93b9-138">Projeyi derleme</span><span class="sxs-lookup"><span data-stu-id="d93b9-138">Build the project</span></span>

<span data-ttu-id="d93b9-139">Proje kökünden aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d93b9-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="d93b9-140">Bu komut oluşturur bir `target/WordCount-1.0-SNAPSHOT.jar` derlenmiş topoloji içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="d93b9-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="d93b9-141">Topoloji yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d93b9-141">Run the topology locally</span></span>

<span data-ttu-id="d93b9-142">Topoloji yerel olarak çalıştırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d93b9-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="d93b9-143">Bu komut, bir yerel Storm geliştirme ortamını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d93b9-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="d93b9-144">Daha fazla bilgi için bkz: [bir geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="d93b9-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="d93b9-145">Bir kez topolojisini başlatır aşağıdakine benzer yerel konsol bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="d93b9-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="d93b9-146">Topoloji durdurmak için kullanma __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="d93b9-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="d93b9-147">Hdınsight üzerinde Storm topolojisini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d93b9-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="d93b9-148">Kopyalamak için aşağıdaki komutu kullanın `WordCount-1.0-SNAPSHOT.jar` Hdınsight kümesi üzerinde storm'a dosyası:</span><span class="sxs-lookup"><span data-stu-id="d93b9-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d93b9-149">Değiştir `sshuser` kümeniz için SSH kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="d93b9-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="d93b9-150">Değiştir `mycluster` küme adı ile.</span><span class="sxs-lookup"><span data-stu-id="d93b9-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="d93b9-151">SSH kullanıcı için parola girin istenebilir.</span><span class="sxs-lookup"><span data-stu-id="d93b9-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="d93b9-152">SSH ve SCP kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d93b9-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d93b9-153">Dosya karşıya sonra SSH kullanarak kümeye bağlanın:</span><span class="sxs-lookup"><span data-stu-id="d93b9-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="d93b9-154">SSH oturumundan kümede topoloji başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d93b9-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="d93b9-155">Kümede topolojisini görüntülemek için Storm kullanıcı Arabirimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d93b9-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="d93b9-156">Storm kullanıcı Arabirimi https://mycluster.azurehdinsight.net/stormui bulunur.</span><span class="sxs-lookup"><span data-stu-id="d93b9-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="d93b9-157">Değiştir `mycluster` küme adıyla.</span><span class="sxs-lookup"><span data-stu-id="d93b9-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="d93b9-158">Başladıktan sonra Storm topolojisini durdurulana kadar çalışır.</span><span class="sxs-lookup"><span data-stu-id="d93b9-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="d93b9-159">Topoloji durdurmak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="d93b9-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="d93b9-160">`storm kill TOPOLOGYNAME` Komut satırından komutu</span><span class="sxs-lookup"><span data-stu-id="d93b9-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="d93b9-161">**KILL** düğmesini Storm kullanıcı Arabirimi.</span><span class="sxs-lookup"><span data-stu-id="d93b9-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d93b9-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d93b9-162">Next steps</span></span>

<span data-ttu-id="d93b9-163">Diğer yolları Python Hdınsight ile kullanmak için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="d93b9-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="d93b9-164">MapReduce işleri akış için Python kullanma</span><span class="sxs-lookup"><span data-stu-id="d93b9-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="d93b9-165">Python kullanıcı tanımlı işlevler (UDF), Pig ve Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="d93b9-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
