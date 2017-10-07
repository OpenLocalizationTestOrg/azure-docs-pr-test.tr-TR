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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Caffe Azure Hdınsight Spark üzerinde dağıtılmış derin learning için kullanın.


## <a name="introduction"></a>Giriş

Derin öğrenme, her şeyi sağlık tootransportation toomanufacturing ve daha fazlasını etkileyen. Şirketler gibi toosolve sabit sorunları, öğrenme toodeep kapatma [görüntü sınıflandırma](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [konuşma tanıma](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)nesne tanıma ve makine çevirisi. 

Vardır [birçok popüler uygulamayı](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)dahil [Microsoft Bilişsel Araç Seti](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, vs. Caffe hello En ünlü simgesel olmayan (kesinlik temelli) sinir ağı çerçeveleri biridir ve yaygın olarak bilgisayar görme dahil birçok alanda kullanılır. Ayrıca, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) birleştirir; bu durumda derin öğrenme Apache Spark Caffe var olan bir Hadoop'ta kolayca da kullanılabilir küme Spark ETL işlem hatları ile birlikte sistem karmaşıklığı ve uçtan uca öğrenme için gecikme süresini azaltır.

[Hdınsight](https://azure.microsoft.com/en-us/services/hdinsight/) sağlayan tam olarak yönetilen bulut Hadoop teklifi açık kaynak analitik kümeler Spark, Hive, MapReduce, HBase, Storm, Kafka ve % 99,9 SLA tarafından yedeklenen R Server için en iyi duruma getirilmiş yalnızca hello değil. Bu Büyük Veri teknolojilerinin tümünün yanı sıra ISV uygulamaları da yönetilen kümeler olarak, kurumsal düzeyde güvenlik ve izleme seçenekleriyle kolayca dağıtılabilir.

Bazı kullanıcılar bize hakkında kaydolmasını toouse Microsoft'un PaaS Hadoop ürün Hdınsight'ta öğrenme derin. Daha fazla tooshare hello gelecekteki olacaktır, ancak bugün toosummarize nasıl teknik blogunda istiyoruz toouse Caffe Hdınsight Spark üzerinde.

Caffe önce yüklediyseniz, bu framework yükleme biraz zor olduğunu fark edeceksiniz. Bu Web Günlüğü'ndeki biz öncelikle gösterecektir nasıl tooinstall [Caffe Spark üzerinde](https://github.com/yahoo/CaffeOnSpark) bir Hdınsight kümesi için sonra hello yerleşik MNIST demo toodemostrate kullanma toouse CPU'larda Hdınsight Spark kullanarak dağıtılmış derin öğrenme.

Hdınsight üzerinde çalışması dört ana adım tooget vardır.

1. Merhaba gerekli bağımlılıkları tüm hello düğümlere yükleyin
2. Hdınsight için Spark üzerinde hello baş düğümünde Caffe derleme
3. Merhaba gerekli kitaplıkları tooall hello çalışan düğümleri Dağıt
4. Caffe model oluşturmak ve distributely çalıştırın

Hdınsight bir PaaS çözümü olduğundan, oldukça kolay tooperform olması için bazı görevler harika platform özellikleri - sunar. Bu blog gönderisinde yoğun olarak kullandığımız hello özelliklerden birini çağrılır [betik eylemi](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), hangi yürütebilirsiniz ile Kabuk komutları toocustomize küme düğümleri (baş düğüm, alt düğüm veya kenar düğümüne).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>1. adım: hello gerekli bağımlılıkları tüm hello düğümlere yükleyin.

başlatılan tooget ihtiyacımız tooinstall hello bağımlılıkları gerekir. Merhaba Caffe site ve [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) hello bağımlılıkları için Spark (Hdınsight Spark hello moddur) YARN modunda üzerinde yüklemek için bazı çok kullanışlı wiki sunar ancak biz tooadd birkaç daha fazla bağımlılıkları Hdınsight platformu için gerekir. Biz hello betik eylemi aşağıdaki gibi kullanın ve tüm hello baş düğümler ve çalışan düğümleri üzerinde çalıştırın. Bu bağımlılıkların ayrıca diğer paketlere bağımlı gibi bu betik eylemi yaklaşık 20 dakika sürer. Erişilebilir tooyour GitHub konumu veya hello varsayılan BLOB storage hesabı gibi Hdınsight kümesi olan bazı konumda girmelisiniz.

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


Merhaba betik eylemine Yukarıdaki iki adımı vardır. Merhaba ilk adımdır tooinstall tüm gerekli kitaplıklar hello. Bu kitaplıklar hem Caffe (gflags aracına gibi glog) derleme ve Caffe (numpy gibi) çalıştırmak için gerekli kitaplıkları hello içerir. CPU en iyi duruma getirme libatlas kullanıyoruz ancak MKL veya (GPU için) CUDA gibi diğer en iyi duruma getirme kitaplıkları yükleme hello CaffeOnSpark wiki her zaman izleyebilirsiniz.

Merhaba ikinci toodownload adımdır, derleme ve çalışma zamanı sırasında protobuf 2.5.0 Caffe için yükleyin. Protobuf 2.5.0 [gereklidir](https://github.com/yahoo/CaffeOnSpark/issues/87), toocompile ihtiyacımız şekilde bu sürümü Ubuntu 16 üzerinde bir paketi olarak kullanılabilir değil ancak hello kaynak kodu ondan. Ayrıca birkaç kaynak yok nasıl hello Internet üzerinde toocompile, gibi [bu](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply Başlarken, yalnızca bu betik eylemini, küme tooall hello çalışan karşı düğümler ve baş düğümler (Hdınsight 3.5 için) çalıştırabilirsiniz. Merhaba küme sağlama süre boyunca hello betik eylemleri de çalıştırabilirsiniz veya hello betik eylemleri çalıştıran küme için ya da çalıştırabilirsiniz. Merhaba betik eylemleri hakkında daha fazla ayrıntı için lütfen hello belgelerine bakın [burada](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Betik eylemleri tooInstall bağımlılıkları](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>2. adım: Caffe Hdınsight için Spark hello baş düğümünde oluşturmak

Hello ikinci adımı toobuild Caffe hello headnode üzerinde ve derlenmiş hello kitaplıkları tooall hello çalışan düğümleri dağıtın. Bu adımda, çok gerekir[ssh, headnode içine](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), yalnızca hello izleyin [CaffeOnSpark yapı işlemi](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), ve aşağıda hello betik toobuild CaffeOnSpark birkaç ek adım ile kullanabilirsiniz. 

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

Toodo gerekebilir CaffeOnSpark hangi hello belgelerine diyor'den fazla. Merhaba değişiklikler şunlardır:
- Yalnızca tooCPU değiştirin ve belirli bu amaç için libatlas kullanın.
- Daha sonra kullanmak için erişilebilir tooall çalışan düğümüne olan paylaşılan bir konuma olan hello veri kümeleri toohello BLOB storage yerleştirin.
- PUT hello Caffe kitaplıkları tooBLOB depolama derlenmiş ve daha sonra betik eylemleri tooavoid ek derleme süresi kullanarak kitaplıkları tooall hello düğümleri kopyalayacak.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Sorun giderme: Ant BuildException oluştu: döndürülen exec: 2

Bazen önce toobuild CaffeOnSpark çalışırken sorar

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Yalnızca temiz hello kod deposu "temiz yapma" olarak ve "yapı çalışma yapma" Merhaba doğru bağımlılıklara sahip olduğu sürece bu sorunu çözmek için.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Sorun giderme: Maven depo bağlantısı zaman aşımına uğradı

Bazen maven bana hello bağlantı zaman aşımı hatası, benzer toobelow sağlar:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Bu birkaç dakika bekledikten sonra Tamam olması ve yalnızca toorebuild hello kod deneyin, şekilde sınırları belirli bir IP adresi trafiğinden hello Maven kalmış olabilir.


### <a name="troubleshooting-test-failure-for-caffe"></a>Sorun giderme: hata Caffe için test etme

Bir sınama hatası CaffeOnSpark, aşağıda ile benzer son denetleme hello yaparken büyük olasılıkla görürsünüz. Bu prabably UTF-8 kodlaması ile ilgili olan ancak Caffe hello kullanımını etkileyen değil

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>3. adım: hello gerekli kitaplıkları tooall hello çalışan düğümleri Dağıt

Merhaba sonraki adımdır toodistribute hello kitaplıkları (temel, CaffeOnSpark/caffe-genel/dağıtmak/lib kitaplıklarında hello/ve CaffeOnSpark/caffe-atandığında/dağıtmak/lib /) tooall hello düğümleri. Adım 2'de, biz bu kitaplıkları BLOB Depolama alanında koyun ve bu adımda, betik eylemleri toocopy kullanacağız onu tooall hello baş düğümler ve çalışan düğümleri.

toodo Bu, basit bir betik eylemi aşağıdaki gibi çalıştırın (toopoint toohello doğru konuma belirli tooyour küme gerekir):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

2. adımda biz bunu erişilebilir tooall hello düğümler BLOB Depolama hello put olduğundan, bu adımda biz yalnızca yalnızca tooall hello düğümleri kopyalayın.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>4. adım: bir Caffe model oluşturmak ve distributely çalıştırın

Yukarıdaki adımları hello çalıştırdıktan sonra Caffe eşlenmeye hello headnode üzerinde yüklü olduğundan ve iyi toogo duyuyoruz. Merhaba sonraki toowrite Caffe modeli adımdır. 

Caffe oluşturmak için bir model, yalnızca size gereken yere toodefine bir yapılandırma dosyası ve hiç (çoğu durumda) kodlama olmadan bir "açıklayıcı mimarisi" kullanıyor. Bu nedenle gelin var. bir göz atalım. 

Biz bugün eğitmek hello MNIST eğitim için bir örnek modeli modelidir. el yazısı basamak Hello MNIST veritabanı 60.000 örnekler Eğitim kümesi ve bir sınama kümesi 10.000 örnekler vardır. NIST kullanılabilir daha büyük bir alt kümesidir. Merhaba basamak boyutu normalleştirilmiş ve sabit boyutlu bir resmi ortalanmış olmuştur. CaffeOnSpark bazı komut dosyaları toodownload hello veri kümesine sahiptir ve hello doğru biçime dönüştür.

CaffeOnSpark MNIST eğitim için bazı ağ topolojileri örnek sağlar. Merhaba ağ mimarisi (Merhaba ağ hello topolojisini) ve en iyi duruma getirme bölme iyi bir tasarıma sahiptir. Bu durumda, gerekli iki dosya vardır: 

Merhaba "Solver" dosyası (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) hello iyileştirme gözlemledikten ve parametre güncelleştirmeleri oluşturmak için kullanılır. Örneğin, CPU veya GPU, kaç yineleme olacaktır, hello satışlarının nedir kullanılıp kullanılmayacağını tanımlar vs. Ayrıca, hangi neuron ağ topolojisi (Merhaba ikinci dosyası ihtiyacımız olan) programı kullanım hello tanımlar. Çözücü hakkında daha fazla bilgi için lütfen çok başvurun[Caffe belgelerine](http://caffe.berkeleyvision.org/tutorial/solver.html).

GPU yerine CPU kullanıyoruz beri bu örnekte, biz hello son satırına değiştirmeniz gerekir:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe yapılandırma](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

Diğer satırlar gerektiği gibi değiştirebilirsiniz.

Merhaba ikinci dosyası (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) hello neuron ağ gibi nasıl göründüğünü ve hello ilgili girdi ve çıktı dosyası tanımlar. Ayrıca tooupdate hello dosya tooreflect hello eğitim veri konumu ihtiyacımız var. Merhaba lenet_memory_train_test.prototxt (toopoint toohello doğru konuma belirli tooyour küme gerekir) bölümünde aşağıdaki gibi değiştirin:

- Merhaba "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" çok değiştirme "wasb: / / / projeleri/machine_learning/image_dataset/mnist_train_lmdb"
- "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" çok değiştirme "wasb: / / / projeleri/machine_learning/image_dataset/mnist_test_lmdb"

![Caffe yapılandırma](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Nasıl toodefine hello ağ ile ilgili daha fazla bilgi için lütfen hello denetleyin [MNIST veri kümesi üzerinde Caffe belgeleri](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

Bu blog Hello amaçla biz yalnızca bu basit MNIST örneği kullanın. Hello baş düğümünden aşağıdaki hello komutunu çalıştırmanız gerekir:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

Gerekli hello temel olarak IT (lenet_memory_solver.prototxt ve lenet_memory_train_test.prototxt) tooeach YARN kapsayıcı ve ayrıca dosyaları hello hello tanımlanan her Spark sürücü/Yürütücü tooLD_LIBRARY_PATH ilgili yolu CaffeOnSpark kitaplıkları sahip önceki kod parçacığını ve noktaları toohello konumu. 

## <a name="monitoring-and-troubleshooting"></a>İzleme ve sorun giderme

YARN küme modu kullanıyoruz beri hello Spark sürücüsü zamanlanmış tooan rasgele kapsayıcı (ve rasgele çalışan düğümüne); Bu durumda olacaktır yalnızca hello konsol çıktısı şuna benzer olarak görmeniz gerekir:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Ne tooknow istiyorsanız, genellikle daha fazla bilgiye sahip tooget hello Spark sürücünün günlük gerekir. Bu durumda, toogo toohello YARN kullanıcı Arabiriminde toofind hello ilgili YARN günlüklerini gerekir. Merhaba YARN kullanıcı Arabirimi tarafından bu URL'yi elde edebilirsiniz: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN KULLANICI ARABİRİMİ](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

Bu belirli bir uygulama için kaç tane kaynaklar bir göz atalım. Merhaba "Zamanlayıcı" bağlantısını tıklatın ve sonra bu uygulama için olduğunu çalıştıran 9 kapsayıcıları görürsünüz. Biz YARN tooprovide 8 yürütücüler isteyin ve sürücü işlemi için başka bir kapsayıcıdır. 

![YARN Zamanlayıcı](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Hata varsa, toocheck hello sürücüsü günlükleri veya kapsayıcı günlükleri isteyebilirsiniz. Sürücü günlüklerinde YARN kullanıcı arabiriminde hello uygulama kimliği'ni tıklatın, sonra hello "Logs" düğmesini tıklatın. Merhaba sürücüsü günlükleri stderr yazılır.

![YARN KULLANICI ARABİRİMİNDE 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Örneğin, bazı hello hatadan hello sürücü günlükleri, çok fazla yürütücüler tahsis belirten görebilirsiniz.

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

Bazı durumlarda, hello sorunu sürücüleri yerine yürütücüler oluşabilir. Bu durumda, toocheck hello kapsayıcı günlükleri gerekir. Her zaman hello kapsayıcı günlükleri alın ve hello başarısız kapsayıcı alın. Örneğin, Caffe çalıştırırken bu hatayı karşılamayabilir.

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

Bu durumda, tooget başarısız hello kapsayıcı kimliği gerekir (hello çalışması üstüne, bu, container_1485916338528_0008_05_000005'dir). Yeniden toorun gerekiyor 

    yarn logs -containerId container_1485916338528_0008_03_000005

Merhaba headnode. Kapsayıcı hatası denetledikten sonra (burada, CPU modunu kullanmanız) GPU modunu kullanarak içinde lenet_memory_solver.prototxt neden olur.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Sonuçlar alınıyor

Biz 8 yürütücüler ayırma ve hello ağ topolojisi basit olduğundan yalnızca yaklaşık 30 dakika toorun hello sonuç almanız gerekir. Merhaba komut satırından biz hello modeli toowasb:///mnist.model yerleştirin ve wasb adlı hello sonuçları tooa klasör put görebilirsiniz: / / / mnist_features_result.

Çalıştırarak hello sonuçlar alabilirsiniz

    hadoop fs -cat hdfs:///mnist_features_result/*

ve hello sonuç aşağıdaki gibi görünür:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Merhaba SampleID hello MNIST kümesindeki hello Kimliğini temsil eder ve model hello hello numarasını tanımlayan hello etiketidir.


## <a name="conclusion"></a>Sonuç

Bu belgede, basit bir örnek çalıştıran ile tooinstall CaffeOnSpark çalıştınız. Hdınsight tam yönetilen bir bulut dağıtılmış bir işlem platformudur ve makine öğrenme ve Gelişmiş analitik iş yükleri, büyük veri kümesi üzerinde çalıştırmak için hello en iyi yerdir ve dağıtılmış derin öğrenme için Hdınsight Spark tooperform derin öğrenmeyi Caffe kullanabilirsiniz görevler.


## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)

