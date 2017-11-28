---
title: "Dağıtılmış derin öğrenme için Azure Hdınsight Spark üzerinde Caffe aaaUse | Microsoft Docs"
description: "Caffe Azure Hdınsight Spark üzerinde dağıtılmış derin learning için kullanın."
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="0885f-103">Caffe Azure Hdınsight Spark üzerinde dağıtılmış derin learning için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0885f-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="0885f-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="0885f-104">Introduction</span></span>

<span data-ttu-id="0885f-105">Derin öğrenme, her şeyi sağlık tootransportation toomanufacturing ve daha fazlasını etkileyen.</span><span class="sxs-lookup"><span data-stu-id="0885f-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="0885f-106">Şirketler gibi toosolve sabit sorunları, öğrenme toodeep kapatma [görüntü sınıflandırma](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [konuşma tanıma](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)nesne tanıma ve makine çevirisi.</span><span class="sxs-lookup"><span data-stu-id="0885f-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="0885f-107">Vardır [birçok popüler uygulamayı](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)dahil [Microsoft Bilişsel Araç Seti](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, vs. Caffe hello En ünlü simgesel olmayan (kesinlik temelli) sinir ağı çerçeveleri biridir ve yaygın olarak bilgisayar görme dahil birçok alanda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0885f-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="0885f-108">Ayrıca, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) birleştirir; bu durumda derin öğrenme Apache Spark Caffe var olan bir Hadoop'ta kolayca da kullanılabilir küme Spark ETL işlem hatları ile birlikte sistem karmaşıklığı ve uçtan uca öğrenme için gecikme süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="0885f-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="0885f-109">[Hdınsight](https://azure.microsoft.com/en-us/services/hdinsight/) sağlayan tam olarak yönetilen bulut Hadoop teklifi açık kaynak analitik kümeler Spark, Hive, MapReduce, HBase, Storm, Kafka ve % 99,9 SLA tarafından yedeklenen R Server için en iyi duruma getirilmiş yalnızca hello değil.</span><span class="sxs-lookup"><span data-stu-id="0885f-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="0885f-110">Bu Büyük Veri teknolojilerinin tümünün yanı sıra ISV uygulamaları da yönetilen kümeler olarak, kurumsal düzeyde güvenlik ve izleme seçenekleriyle kolayca dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="0885f-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="0885f-111">Bazı kullanıcılar bize hakkında kaydolmasını toouse Microsoft'un PaaS Hadoop ürün Hdınsight'ta öğrenme derin.</span><span class="sxs-lookup"><span data-stu-id="0885f-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="0885f-112">Daha fazla tooshare hello gelecekteki olacaktır, ancak bugün toosummarize nasıl teknik blogunda istiyoruz toouse Caffe Hdınsight Spark üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0885f-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="0885f-113">Caffe önce yüklediyseniz, bu framework yükleme biraz zor olduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="0885f-114">Bu Web Günlüğü'ndeki biz öncelikle gösterecektir nasıl tooinstall [Caffe Spark üzerinde](https://github.com/yahoo/CaffeOnSpark) bir Hdınsight kümesi için sonra hello yerleşik MNIST demo toodemostrate kullanma toouse CPU'larda Hdınsight Spark kullanarak dağıtılmış derin öğrenme.</span><span class="sxs-lookup"><span data-stu-id="0885f-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="0885f-115">Hdınsight üzerinde çalışması dört ana adım tooget vardır.</span><span class="sxs-lookup"><span data-stu-id="0885f-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="0885f-116">Merhaba gerekli bağımlılıkları tüm hello düğümlere yükleyin</span><span class="sxs-lookup"><span data-stu-id="0885f-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="0885f-117">Hdınsight için Spark üzerinde hello baş düğümünde Caffe derleme</span><span class="sxs-lookup"><span data-stu-id="0885f-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="0885f-118">Merhaba gerekli kitaplıkları tooall hello çalışan düğümleri Dağıt</span><span class="sxs-lookup"><span data-stu-id="0885f-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="0885f-119">Caffe model oluşturmak ve distributely çalıştırın</span><span class="sxs-lookup"><span data-stu-id="0885f-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="0885f-120">Hdınsight bir PaaS çözümü olduğundan, oldukça kolay tooperform olması için bazı görevler harika platform özellikleri - sunar.</span><span class="sxs-lookup"><span data-stu-id="0885f-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="0885f-121">Bu blog gönderisinde yoğun olarak kullandığımız hello özelliklerden birini çağrılır [betik eylemi](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), hangi yürütebilirsiniz ile Kabuk komutları toocustomize küme düğümleri (baş düğüm, alt düğüm veya kenar düğümüne).</span><span class="sxs-lookup"><span data-stu-id="0885f-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="0885f-122">1. adım: hello gerekli bağımlılıkları tüm hello düğümlere yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0885f-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="0885f-123">başlatılan tooget ihtiyacımız tooinstall hello bağımlılıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0885f-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="0885f-124">Merhaba Caffe site ve [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) hello bağımlılıkları için Spark (Hdınsight Spark hello moddur) YARN modunda üzerinde yüklemek için bazı çok kullanışlı wiki sunar ancak biz tooadd birkaç daha fazla bağımlılıkları Hdınsight platformu için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0885f-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="0885f-125">Biz hello betik eylemi aşağıdaki gibi kullanın ve tüm hello baş düğümler ve çalışan düğümleri üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0885f-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="0885f-126">Bu bağımlılıkların ayrıca diğer paketlere bağımlı gibi bu betik eylemi yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0885f-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="0885f-127">Erişilebilir tooyour GitHub konumu veya hello varsayılan BLOB storage hesabı gibi Hdınsight kümesi olan bazı konumda girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


<span data-ttu-id="0885f-128">Merhaba betik eylemine Yukarıdaki iki adımı vardır.</span><span class="sxs-lookup"><span data-stu-id="0885f-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="0885f-129">Merhaba ilk adımdır tooinstall tüm gerekli kitaplıklar hello.</span><span class="sxs-lookup"><span data-stu-id="0885f-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="0885f-130">Bu kitaplıklar hem Caffe (gflags aracına gibi glog) derleme ve Caffe (numpy gibi) çalıştırmak için gerekli kitaplıkları hello içerir.</span><span class="sxs-lookup"><span data-stu-id="0885f-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="0885f-131">CPU en iyi duruma getirme libatlas kullanıyoruz ancak MKL veya (GPU için) CUDA gibi diğer en iyi duruma getirme kitaplıkları yükleme hello CaffeOnSpark wiki her zaman izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="0885f-132">Merhaba ikinci toodownload adımdır, derleme ve çalışma zamanı sırasında protobuf 2.5.0 Caffe için yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0885f-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="0885f-133">Protobuf 2.5.0 [gereklidir](https://github.com/yahoo/CaffeOnSpark/issues/87), toocompile ihtiyacımız şekilde bu sürümü Ubuntu 16 üzerinde bir paketi olarak kullanılabilir değil ancak hello kaynak kodu ondan.</span><span class="sxs-lookup"><span data-stu-id="0885f-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="0885f-134">Ayrıca birkaç kaynak yok nasıl hello Internet üzerinde toocompile, gibi [bu](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="0885f-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="0885f-135">toosimply Başlarken, yalnızca bu betik eylemini, küme tooall hello çalışan karşı düğümler ve baş düğümler (Hdınsight 3.5 için) çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="0885f-136">Merhaba küme sağlama süre boyunca hello betik eylemleri de çalıştırabilirsiniz veya hello betik eylemleri çalıştıran küme için ya da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="0885f-137">Merhaba betik eylemleri hakkında daha fazla ayrıntı için lütfen hello belgelerine bakın [burada](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="0885f-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Betik eylemleri tooInstall bağımlılıkları](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="0885f-139">2. adım: Caffe Hdınsight için Spark hello baş düğümünde oluşturmak</span><span class="sxs-lookup"><span data-stu-id="0885f-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="0885f-140">Hello ikinci adımı toobuild Caffe hello headnode üzerinde ve derlenmiş hello kitaplıkları tooall hello çalışan düğümleri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0885f-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="0885f-141">Bu adımda, çok gerekir[ssh, headnode içine](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), yalnızca hello izleyin [CaffeOnSpark yapı işlemi](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), ve aşağıda hello betik toobuild CaffeOnSpark birkaç ek adım ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="0885f-142">Toodo gerekebilir CaffeOnSpark hangi hello belgelerine diyor'den fazla.</span><span class="sxs-lookup"><span data-stu-id="0885f-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="0885f-143">Merhaba değişiklikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0885f-143">hello changes are:</span></span>
- <span data-ttu-id="0885f-144">Yalnızca tooCPU değiştirin ve belirli bu amaç için libatlas kullanın.</span><span class="sxs-lookup"><span data-stu-id="0885f-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="0885f-145">Daha sonra kullanmak için erişilebilir tooall çalışan düğümüne olan paylaşılan bir konuma olan hello veri kümeleri toohello BLOB storage yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0885f-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="0885f-146">PUT hello Caffe kitaplıkları tooBLOB depolama derlenmiş ve daha sonra betik eylemleri tooavoid ek derleme süresi kullanarak kitaplıkları tooall hello düğümleri kopyalayacak.</span><span class="sxs-lookup"><span data-stu-id="0885f-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="0885f-147">Sorun giderme: Ant BuildException oluştu: döndürülen exec: 2</span><span class="sxs-lookup"><span data-stu-id="0885f-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="0885f-148">Bazen önce toobuild CaffeOnSpark çalışırken sorar</span><span class="sxs-lookup"><span data-stu-id="0885f-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="0885f-149">Yalnızca temiz hello kod deposu "temiz yapma" olarak ve "yapı çalışma yapma" Merhaba doğru bağımlılıklara sahip olduğu sürece bu sorunu çözmek için.</span><span class="sxs-lookup"><span data-stu-id="0885f-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="0885f-150">Sorun giderme: Maven depo bağlantısı zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="0885f-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="0885f-151">Bazen maven bana hello bağlantı zaman aşımı hatası, benzer toobelow sağlar:</span><span class="sxs-lookup"><span data-stu-id="0885f-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="0885f-152">Bu birkaç dakika bekledikten sonra Tamam olması ve yalnızca toorebuild hello kod deneyin, şekilde sınırları belirli bir IP adresi trafiğinden hello Maven kalmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="0885f-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="0885f-153">Sorun giderme: hata Caffe için test etme</span><span class="sxs-lookup"><span data-stu-id="0885f-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="0885f-154">Bir sınama hatası CaffeOnSpark, aşağıda ile benzer son denetleme hello yaparken büyük olasılıkla görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0885f-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="0885f-155">Bu prabably UTF-8 kodlaması ile ilgili olan ancak Caffe hello kullanımını etkileyen değil</span><span class="sxs-lookup"><span data-stu-id="0885f-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="0885f-156">3. adım: hello gerekli kitaplıkları tooall hello çalışan düğümleri Dağıt</span><span class="sxs-lookup"><span data-stu-id="0885f-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="0885f-157">Merhaba sonraki adımdır toodistribute hello kitaplıkları (temel, CaffeOnSpark/caffe-genel/dağıtmak/lib kitaplıklarında hello/ve CaffeOnSpark/caffe-atandığında/dağıtmak/lib /) tooall hello düğümleri.</span><span class="sxs-lookup"><span data-stu-id="0885f-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="0885f-158">Adım 2'de, biz bu kitaplıkları BLOB Depolama alanında koyun ve bu adımda, betik eylemleri toocopy kullanacağız onu tooall hello baş düğümler ve çalışan düğümleri.</span><span class="sxs-lookup"><span data-stu-id="0885f-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="0885f-159">toodo Bu, basit bir betik eylemi aşağıdaki gibi çalıştırın (toopoint toohello doğru konuma belirli tooyour küme gerekir):</span><span class="sxs-lookup"><span data-stu-id="0885f-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="0885f-160">2. adımda biz bunu erişilebilir tooall hello düğümler BLOB Depolama hello put olduğundan, bu adımda biz yalnızca yalnızca tooall hello düğümleri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0885f-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="0885f-161">4. adım: bir Caffe model oluşturmak ve distributely çalıştırın</span><span class="sxs-lookup"><span data-stu-id="0885f-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="0885f-162">Yukarıdaki adımları hello çalıştırdıktan sonra Caffe eşlenmeye hello headnode üzerinde yüklü olduğundan ve iyi toogo duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="0885f-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="0885f-163">Merhaba sonraki toowrite Caffe modeli adımdır.</span><span class="sxs-lookup"><span data-stu-id="0885f-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="0885f-164">Caffe oluşturmak için bir model, yalnızca size gereken yere toodefine bir yapılandırma dosyası ve hiç (çoğu durumda) kodlama olmadan bir "açıklayıcı mimarisi" kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="0885f-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="0885f-165">Bu nedenle gelin var. bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="0885f-165">So let's take a look there.</span></span> 

<span data-ttu-id="0885f-166">Biz bugün eğitmek hello MNIST eğitim için bir örnek modeli modelidir.</span><span class="sxs-lookup"><span data-stu-id="0885f-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="0885f-167">el yazısı basamak Hello MNIST veritabanı 60.000 örnekler Eğitim kümesi ve bir sınama kümesi 10.000 örnekler vardır.</span><span class="sxs-lookup"><span data-stu-id="0885f-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="0885f-168">NIST kullanılabilir daha büyük bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="0885f-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="0885f-169">Merhaba basamak boyutu normalleştirilmiş ve sabit boyutlu bir resmi ortalanmış olmuştur.</span><span class="sxs-lookup"><span data-stu-id="0885f-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="0885f-170">CaffeOnSpark bazı komut dosyaları toodownload hello veri kümesine sahiptir ve hello doğru biçime dönüştür.</span><span class="sxs-lookup"><span data-stu-id="0885f-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="0885f-171">CaffeOnSpark MNIST eğitim için bazı ağ topolojileri örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="0885f-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="0885f-172">Merhaba ağ mimarisi (Merhaba ağ hello topolojisini) ve en iyi duruma getirme bölme iyi bir tasarıma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0885f-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="0885f-173">Bu durumda, gerekli iki dosya vardır:</span><span class="sxs-lookup"><span data-stu-id="0885f-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="0885f-174">Merhaba "Solver" dosyası (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) hello iyileştirme gözlemledikten ve parametre güncelleştirmeleri oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0885f-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="0885f-175">Örneğin, CPU veya GPU, kaç yineleme olacaktır, hello satışlarının nedir kullanılıp kullanılmayacağını tanımlar vs. Ayrıca, hangi neuron ağ topolojisi (Merhaba ikinci dosyası ihtiyacımız olan) programı kullanım hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0885f-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="0885f-176">Çözücü hakkında daha fazla bilgi için lütfen çok başvurun[Caffe belgelerine](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="0885f-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="0885f-177">GPU yerine CPU kullanıyoruz beri bu örnekte, biz hello son satırına değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0885f-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe yapılandırma](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="0885f-179">Diğer satırlar gerektiği gibi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-179">You can change other lines as needed.</span></span>

<span data-ttu-id="0885f-180">Merhaba ikinci dosyası (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) hello neuron ağ gibi nasıl göründüğünü ve hello ilgili girdi ve çıktı dosyası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0885f-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="0885f-181">Ayrıca tooupdate hello dosya tooreflect hello eğitim veri konumu ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="0885f-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="0885f-182">Merhaba lenet_memory_train_test.prototxt (toopoint toohello doğru konuma belirli tooyour küme gerekir) bölümünde aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0885f-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="0885f-183">Merhaba "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" çok değiştirme "wasb: / / / projeleri/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="0885f-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="0885f-184">"file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" çok değiştirme "wasb: / / / projeleri/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="0885f-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe yapılandırma](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="0885f-186">Nasıl toodefine hello ağ ile ilgili daha fazla bilgi için lütfen hello denetleyin [MNIST veri kümesi üzerinde Caffe belgeleri](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="0885f-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="0885f-187">Bu blog Hello amaçla biz yalnızca bu basit MNIST örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="0885f-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="0885f-188">Hello baş düğümünden aşağıdaki hello komutunu çalıştırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0885f-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="0885f-189">Gerekli hello temel olarak IT (lenet_memory_solver.prototxt ve lenet_memory_train_test.prototxt) tooeach YARN kapsayıcı ve ayrıca dosyaları hello hello tanımlanan her Spark sürücü/Yürütücü tooLD_LIBRARY_PATH ilgili yolu CaffeOnSpark kitaplıkları sahip önceki kod parçacığını ve noktaları toohello konumu.</span><span class="sxs-lookup"><span data-stu-id="0885f-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="0885f-190">İzleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0885f-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="0885f-191">YARN küme modu kullanıyoruz beri hello Spark sürücüsü zamanlanmış tooan rasgele kapsayıcı (ve rasgele çalışan düğümüne); Bu durumda olacaktır yalnızca hello konsol çıktısı şuna benzer olarak görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0885f-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="0885f-192">Ne tooknow istiyorsanız, genellikle daha fazla bilgiye sahip tooget hello Spark sürücünün günlük gerekir.</span><span class="sxs-lookup"><span data-stu-id="0885f-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="0885f-193">Bu durumda, toogo toohello YARN kullanıcı Arabiriminde toofind hello ilgili YARN günlüklerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="0885f-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="0885f-194">Merhaba YARN kullanıcı Arabirimi tarafından bu URL'yi elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0885f-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN KULLANICI ARABİRİMİ](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="0885f-196">Bu belirli bir uygulama için kaç tane kaynaklar bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="0885f-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="0885f-197">Merhaba "Zamanlayıcı" bağlantısını tıklatın ve sonra bu uygulama için olduğunu çalıştıran 9 kapsayıcıları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0885f-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="0885f-198">Biz YARN tooprovide 8 yürütücüler isteyin ve sürücü işlemi için başka bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="0885f-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![YARN Zamanlayıcı](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="0885f-200">Hata varsa, toocheck hello sürücüsü günlükleri veya kapsayıcı günlükleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="0885f-201">Sürücü günlüklerinde YARN kullanıcı arabiriminde hello uygulama kimliği'ni tıklatın, sonra hello "Logs" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0885f-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="0885f-202">Merhaba sürücüsü günlükleri stderr yazılır.</span><span class="sxs-lookup"><span data-stu-id="0885f-202">hello driver logs are written into stderr.</span></span>

![YARN KULLANICI ARABİRİMİNDE 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="0885f-204">Örneğin, bazı hello hatadan hello sürücü günlükleri, çok fazla yürütücüler tahsis belirten görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0885f-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

<span data-ttu-id="0885f-205">Bazı durumlarda, hello sorunu sürücüleri yerine yürütücüler oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="0885f-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="0885f-206">Bu durumda, toocheck hello kapsayıcı günlükleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="0885f-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="0885f-207">Her zaman hello kapsayıcı günlükleri alın ve hello başarısız kapsayıcı alın.</span><span class="sxs-lookup"><span data-stu-id="0885f-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="0885f-208">Örneğin, Caffe çalıştırırken bu hatayı karşılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="0885f-208">For example, you might meet this failure when running Caffe.</span></span>

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

<span data-ttu-id="0885f-209">Bu durumda, tooget başarısız hello kapsayıcı kimliği gerekir (hello çalışması üstüne, bu, container_1485916338528_0008_05_000005'dir).</span><span class="sxs-lookup"><span data-stu-id="0885f-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="0885f-210">Yeniden toorun gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0885f-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="0885f-211">Merhaba headnode.</span><span class="sxs-lookup"><span data-stu-id="0885f-211">from hello headnode.</span></span> <span data-ttu-id="0885f-212">Kapsayıcı hatası denetledikten sonra (burada, CPU modunu kullanmanız) GPU modunu kullanarak içinde lenet_memory_solver.prototxt neden olur.</span><span class="sxs-lookup"><span data-stu-id="0885f-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="0885f-213">Sonuçlar alınıyor</span><span class="sxs-lookup"><span data-stu-id="0885f-213">Getting results</span></span>

<span data-ttu-id="0885f-214">Biz 8 yürütücüler ayırma ve hello ağ topolojisi basit olduğundan yalnızca yaklaşık 30 dakika toorun hello sonuç almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0885f-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="0885f-215">Merhaba komut satırından biz hello modeli toowasb:///mnist.model yerleştirin ve wasb adlı hello sonuçları tooa klasör put görebilirsiniz: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="0885f-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="0885f-216">Çalıştırarak hello sonuçlar alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0885f-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="0885f-217">ve hello sonuç aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="0885f-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="0885f-218">Merhaba SampleID hello MNIST kümesindeki hello Kimliğini temsil eder ve model hello hello numarasını tanımlayan hello etiketidir.</span><span class="sxs-lookup"><span data-stu-id="0885f-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="0885f-219">Sonuç</span><span class="sxs-lookup"><span data-stu-id="0885f-219">Conclusion</span></span>

<span data-ttu-id="0885f-220">Bu belgede, basit bir örnek çalıştıran ile tooinstall CaffeOnSpark çalıştınız.</span><span class="sxs-lookup"><span data-stu-id="0885f-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="0885f-221">Hdınsight tam yönetilen bir bulut dağıtılmış bir işlem platformudur ve makine öğrenme ve Gelişmiş analitik iş yükleri, büyük veri kümesi üzerinde çalıştırmak için hello en iyi yerdir ve dağıtılmış derin öğrenme için Hdınsight Spark tooperform derin öğrenmeyi Caffe kullanabilirsiniz görevler.</span><span class="sxs-lookup"><span data-stu-id="0885f-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="0885f-222"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0885f-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0885f-223">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="0885f-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0885f-224">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="0885f-224">Scenarios</span></span>
* [<span data-ttu-id="0885f-225">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="0885f-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0885f-226">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="0885f-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="0885f-227">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="0885f-227">Manage resources</span></span>
* [<span data-ttu-id="0885f-228">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="0885f-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

