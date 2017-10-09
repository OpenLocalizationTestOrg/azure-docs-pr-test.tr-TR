---
title: "Windows tabanlı hdınsight'tan aaaMigrate tooLinux tabanlı Hdınsight - Azure | Microsoft Docs"
description: "Windows tabanlı bir hdınsight'tan toomigrate küme tooa Linux tabanlı Hdınsight kümesi nasıl öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Bir Windows tabanlı Hdınsight küme tooa Linux tabanlı kümeden geçirme

Bu belge, Windows ve Linux Hdınsight'ta nasıl hakkında yönergeler arasındaki hello farklar hakkında ayrıntılar sağlar. toomigrate var olan iş yükleri tooa Linux tabanlı küme.

Windows tabanlı Hdınsight kolay bir yolu toouse hello bulutta Hadoop sağlarken toomigrate tooa Linux tabanlı küme gerekebilir. Örneğin, tootake avantajlarından Linux tabanlı araçlar ve çözümünüz için gerekli olan teknolojiler. Pek çok hello Hadoop ekosistemindeki Linux tabanlı sistemlerde geliştirilmiş ve Windows tabanlı Hdınsight ile kullanılmak üzere müsait olmayabilir. Ayrıca, birçok defterleri, videolar ve diğer eğitim malzemesi Hadoop ile çalışırken, Linux sistemi kullandığınız varsayılır.

> [!NOTE]
> Hdınsight kümeleri hello küme hello düğümler için hello işletim sistemi olarak Ubuntu uzun süreli destek (LTS) kullanın. Diğer bileşen sürümü oluşturma bilgilerle birlikte, Hdınsight ile Ubuntu hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Geçiş görevleri

Merhaba, geçiş için genel iş akışı aşağıdaki gibidir.

![Geçiş iş akışı diyagramı](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Bu belgenin her bölüm geçirirken, var olan iş akışı, işleri, vb. tooa Linux tabanlı küme gerekli olabilecek toounderstand değişiklikleri okuyun.

2. Linux tabanlı bir küme bir test/kalite güvence ortamı oluşturun. Linux tabanlı bir küme oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-provision-linux-clusters.md).

3. İşleri, veri kaynakları ve havuzlarını toohello yeni ortam varolan kopyalayın.

4. Toomake işleriniz hello yeni kümede beklendiği gibi çalıştığından emin sınama doğrulaması gerçekleştirir.

Her şeyin beklendiği gibi çalıştığını doğruladıktan sonra hello geçiş için kapalı kalma süresi zamanlayın. Bu kesinti sırasında hello aşağıdaki eylemleri gerçekleştirin:

1. Merhaba küme düğümlerinde yerel olarak depolanan tüm geçici verileri yedekleyin. Örneğin, doğrudan bir baş düğüm üzerinde depolanan verileri varsa.

2. Merhaba Windows tabanlı küme silin.

3. Aynı Windows tabanlı küme kullanılan hello veri deposu varsayılan hello kullanarak Linux tabanlı bir küme oluşturun. Merhaba Linux tabanlı küme var olan üretim verilerinizi karşı çalışmaya devam edebilirsiniz.

4. Yedeklediğiniz herhangi bir geçici veri içeri aktarın.

5. Başlangıç işleri/hello yeni küme kullanarak işlemeye devam et.

### <a name="copy-data-toohello-test-environment"></a>Kopya veri toohello test ortamı

Birçok yöntemleri toocopy hello veri ve işleri vardır, ancak hello iki Bu bölümde açıklanan hello en basit yöntem toodirectly taşıma dosyaları tooa test kümesi.

#### <a name="hdfs-copy"></a>HDFS kopyalama

Adımları toocopy veri hello üretim küme toohello test kümeden aşağıdaki hello kullanın. Bu adımları hello kullanın `hdfs dfs` Hdınsight ile birlikte yardımcı programı.

1. Varolan kümenizin Hello depolama hesabı ve varsayılan kapsayıcı bilgilerini bulun. Aşağıdaki örnek hello PowerShell tooretrieve bu bilgileri kullanır:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. bir test ortamı toocreate Hdınsight belgedeki hello oluşturma Linux tabanlı kümelerde hello adımları izleyin. Merhaba küme oluşturmadan önce durdurun ve bunun yerine seçin **isteğe bağlı yapılandırma**.

3. Merhaba isteğe bağlı yapılandırma dikey penceresinden seçin **bağlantılı depolama hesapları**.

4. Seçin **depolama anahtarı eklemek**ve istendiğinde, hello adım 1'de PowerShell komut dosyası tarafından döndürülen hello depolama hesabı seçin. Tıklatın **seçin** her dikey. Son olarak, hello kümesi oluşturun.

5. Merhaba Küme oluşturulduktan sonra tooit kullanarak bağlan **SSH.** Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

6. Merhaba SSH oturumunda, aşağıdaki komut toocopy dosyaları hello bağlantılı depolama hesabı toohello yeni varsayılan depolama hesabından hello kullanın. KAPSAYICI, PowerShell tarafından döndürülen hello kapsayıcı bilgileri ile değiştirin. Değiştir __hesap__ hello hesap adına sahip. Merhaba yolu toodata hello yolu tooa veri dosyası ile değiştirin.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Merhaba verileri içeren hello dizin yapısını hello sınama ortamında mevcut değilse, komutu aşağıdaki hello kullanarak oluşturabilirsiniz:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Merhaba `-p` anahtar hello yoldaki tüm dizinler hello oluşturulmasını etkinleştirir.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Azure Storage blobları arasında doğrudan kopyalama

Alternatif olarak, toouse hello isteyebilirsiniz `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet toocopy BLOB'lar Hdınsight dışında depolama hesapları arasında. Merhaba daha fazla bilgi için bkz. nasıl toomanage Azure PowerShell kullanarak Azure Storage ile Azure BLOB'ları bölümü.

## <a name="client-side-technologies"></a>İstemci-tarafı teknolojileri

İstemci-tarafı teknolojileri gibi [Azure PowerShell cmdlet'lerini](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), veya hello [Hadoop için .NET SDK'sı](https://hadoopsdk.codeplex.com/) toowork Linux tabanlı kümelerde devam edin. Bu teknolojiler KALAN aynı her iki küme işletim sistemi türleri arasında hello API'lerini kullanır.

## <a name="server-side-technologies"></a>Sunucu tarafı teknolojileri

Aşağıdaki tablonun hello Windows'a özgü olan geçirme sunucu tarafı bileşenlerini rehberlik sağlar.

| Bu teknoloji kullanıyorsanız... | Bu eyleme... |
| --- | --- |
| **PowerShell** (sunucu tarafı kodlar betik küme oluşturma sırasında kullanılan eylemleri de dahil olmak üzere,) |Bash betiklerini yeniden yazın. Betik eylemleri için bkz: [özelleştirme Linux tabanlı Hdınsight ile betik eylemleri](hdinsight-hadoop-customize-cluster-linux.md) ve [betik eylemi geliştirme Linux tabanlı Hdınsight için](hdinsight-hadoop-script-actions-linux.md). |
| **Azure CLI** (sunucu tarafı komut dosyaları) |Hello Azure CLI Linux'ta kullanılabilir olsa da, bunu hello Hdınsight küme baş düğümler üzerinde önceden yüklenmiş gelmez. Hello Azure CLI yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **.NET bileşenleri** |.NET Linux tabanlı Hdınsight desteklenir [Mono](https://mono-project.com). Daha fazla bilgi için bkz: [geçirmek .NET çözümleri tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Win32 bileşenlerini veya diğer yalnızca Windows teknolojisi** |Kılavuzu hello bileşeni veya teknoloji bağlıdır. Mümkün toofind Linux ile uyumlu bir sürümü olabilir veya toofind alternatif bir çözüm ihtiyaç duyabileceğiniz veya bu bileşeni yeniden yazın. |

> [!IMPORTANT]
> Merhaba Hdınsight Yönetim SDK Mono ile tamamen uyumlu değil. Çözümleri parçası toohello Hdınsight kümesi şu anda dağıtılmış olarak kullanılmamalıdır.

## <a name="cluster-creation"></a>Küme oluşturma

Bu bölümde, küme oluşturma farklılıkları hakkında bilgiler sağlar.

### <a name="ssh-user"></a>SSH kullanıcı

Linux tabanlı Hdınsight kümeleri kullanmak hello **güvenli Kabuk (SSH)** protokol tooprovide uzaktan erişim toohello küme düğümleri. Uzak Masaüstü için Windows tabanlı kümeler farklı olarak, çoğu SSH istemcisi bir grafik kullanıcı deneyimi sağlamaz. Bunun yerine, SSH istemcilerini hello kümede toorun komutları sağlayan bir komut satırı belirtin. Bazı istemciler (gibi [MobaXterm](http://mobaxterm.mobatek.net/)) toplama tooa uzaktan komut satırı grafik dosya sistemi tarayıcıda sağlayın.

Küme oluşturma sırasında bir SSH kullanıcısı ve ya da sağlamanız gereken bir **parola** veya **ortak anahtar sertifikası** kimlik doğrulaması için.

Parola kullanmaktan daha güvenli olduğu gibi ortak anahtar sertifikası kullanmanızı öneririz. Sertifika kimlik doğrulaması, imzalanmış bir genel/özel anahtar çifti oluşturma, ardından hello kümesi oluştururken hello ortak anahtarı sağlayarak çalışır. SSH kullanarak toohello sunucusuna bağlanırken hello özel anahtarı hello istemcide hello bağlantı için kimlik doğrulaması sağlar.

Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Küme özelleştirme

**Betik eylemleri** ile kullanılan Linux tabanlı kümelerde Bash komut dosyasında yazılması gerekir. Betik eylemleri küme oluşturma sırasında Linux tabanlı kümelerde bir küme yukarı sonra bunlar kullanılan tooperform özelleştirme da olabilir ve çalışması için kullanılabilse de. Daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight ile betik eylemleri](hdinsight-hadoop-customize-cluster-linux.md) ve [betik eylemi geliştirme Linux tabanlı Hdınsight için](hdinsight-hadoop-script-actions-linux.md).

Başka bir özelleştirme özelliği **önyükleme**. Bu özellik Windows kümeleri için toospecify hello Hive ile kullanmak için ek kitaplıkları konumunu sağlar. Küme oluşturulduktan sonra Bu kitaplıklar otomatik olarak Hive sorguları hello gerek toouse olmadan kullanılabilir `ADD JAR`.

Linux tabanlı kümeler için önyükleme özelliği Hello bu işlevleri sağlamaz. Bunun yerine, kısmında belgelenen betik eylemi kullanın [eklemek Hive kitaplıkları küme oluşturma sırasında](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Sanal Ağlar

Linux tabanlı Hdınsight kümeleri Resource Manager sanal ağlar gerektirirken Klasik sanal ağlar, yalnızca çalışmak Windows tabanlı Hdınsight kümeleri. Kaynaklarınız varsa bir Klasik sanal Linux Hdınsight kümesi hello ağ yüklemelisiniz bağlanmak bkz [Klasik sanal ağı tooa Resource Manager sanal ağ bağlanma](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Hdınsight ile Azure sanal ağları kullanarak yapılandırma gereksinimleri hakkında daha fazla bilgi için bkz: [kullanarak bir sanal ağ genişletme Hdınsight yetenekleri](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Yönetim ve izleme

Birçok hello web Uı'lar iş geçmişi veya Yarn kullanıcı Arabiriminde, gibi Windows tabanlı Hdınsight ile kullanmış olabilirsiniz, Ambari kullanılabilir. Ayrıca, hello Ambari Hive görünümü web tarayıcınızı kullanarak Hive sorguları bir şekilde toorun sağlar. Merhaba Ambari Web kullanıcı Arabirimi, Linux tabanlı kümelerde https://CLUSTERNAME.azurehdinsight.net adresindeki kullanılabilir.

Ambari ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Ambari Web](hdinsight-hadoop-manage-ambari.md)
* [Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Ambari uyarıları

Ambari hello kümesi ile ilgili olası sorunları size bildiren bir uyarı sistem sahiptir. Görüntüleri de hello REST API alabilir ancak uyarılar hello Ambari Web kullanıcı ARABİRİMİ'nde, sarı veya kırmızı girişleri olarak görünür.

> [!IMPORTANT]
> Ambari uyarılar belirtir, var. *olabilir* bir sorun, burada *olan* bir sorun. Örneğin, normal olarak erişebilir olsa da HiveServer2 erişilemeyeceğini bir uyarı alabilirsiniz.
>
> Birçok uyarılar aralık-temelli sorguları bir hizmet olarak uygulanır ve belirli bir zaman çerçevesi içinde bir yanıt bekler. Şekilde hello uyarı mutlaka hello hizmetinin kapalı olduğunu anlamına gelmez, yalnızca hello beklenen zaman çerçevesinde sonuç döndürmedi.

Bir uyarı için uzun bir süre gerçekleşen ya da eylemi gerçekleştirmeden önce bildirilen kullanıcı sorunları yansıtan değerlendirmelisiniz.

## <a name="file-system-locations"></a>Dosya sistemi konumları

Linux küme dosya sistemi Hello Windows tabanlı Hdınsight kümeleri farklı yerleştirilir. Aşağıdaki tablo toofind sık kullanılan dosyalar hello kullanın.

| Toofind ihtiyacım... | Bulunuyor... |
| --- | --- |
| Yapılandırma |`/etc`. Örneğin, `/etc/hadoop/conf/core-site.xml` |
| Günlük dosyaları |`/var/logs` |
| Hortonworks veri Platformu (HDP) |`/usr/hdp`. İki dizini bulunan burada hello geçerli HDP sürümü olan bir vardır ve `current`. Merhaba `current` sembolik bağlantılar toofiles ve hello sürüm numarası dizininde bulunan dizinler dizini içerir. Merhaba `current` dizindir sağlanan sürüm HDP hello gibi hello sürüm numarası sonrasındaki değişiklikler HDP dosyalara erişmek için kolay bir yol olarak güncelleştirilir. |
| hadoop streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

Genel olarak, hello hello dosyasının adını biliyorsanız, bir SSH oturumu toofind hello dosya yolundan komutu aşağıdaki hello kullanabilirsiniz:

    find / -name FILENAME 2>/dev/null

Joker karakterler hello dosya adı ile de kullanabilirsiniz. Örneğin, `find / -name *streaming*.jar 2>/dev/null` 'hello dosya adının bir parçası olarak akış' hello sözcüğünü içeren jar dosyalarını hello yolu tooany döndürür.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig ve MapReduce

Pig ve MapReduce iş yükleri, Linux tabanlı kümelerde benzerdir. Ancak, Linux tabanlı Hdınsight kümeleri Hadoop, Hive veya Pig daha yeni sürümleri kullanılarak oluşturulabilir. Bu sürüm farklılıklar nasıl değişiklikleri çıkarabilir, varolan çözümleri işlevi. Hdınsight ile dahil bileşenlerin hello sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).

Linux tabanlı Hdınsight Uzak Masaüstü işlevselliği sağlamaz. Bunun yerine, SSH kullanabilirsiniz tooremotely toohello küme baş düğümler bağlanın. Daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [SSH ile Hive kullanma](hdinsight-hadoop-use-hive-ssh.md)
* [SSH ile pig kullanma](hdinsight-hadoop-use-pig-ssh.md)
* [SSH ile MapReduce kullanma](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Bir dış Hive meta depo kullanırsanız, Linux tabanlı Hdınsight ile kullanmadan önce hello meta depo yedeklemeniz gerekir. Linux tabanlı Hdınsight uyumsuzlukları olabilir Hive daha yeni sürümleriyle kullanılabilir önceki sürümleri tarafından oluşturulan meta deponuz ile.

Grafik aşağıdaki hello Hive iş yüklerinizi geçirme hakkında rehberlik sağlar.

| Üzerinde Windows tabanlı kullanmam... | Linux tabanlı... |
| --- | --- |
| **Hive düzenleyicisinin** |[Ambari Hive görünümünü](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez Linux tabanlı kümeler için hello varsayılan yürütme altyapısı, hello set deyimi için artık gerekli değildir. |
| C# kullanıcı tanımlı işlevler | C# Linux tabanlı Hdınsight bileşenleriyle doğrulama hakkında daha fazla bilgi için bkz: [geçirmek .NET çözümleri tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD dosyaları veya bir Hive işi bir parçası olarak çağrılan hello sunucuda komut dosyaları |Bash betiklerini kullanın |
| `hive`komut Uzak Masaüstü |Kullanım [Beeline](hdinsight-hadoop-use-hive-beeline.md) veya [Hive bir SSH oturumunda](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| Üzerinde Windows tabanlı kullanmam... | Linux tabanlı... |
| --- | --- |
| C# kullanıcı tanımlı işlevler | C# Linux tabanlı Hdınsight bileşenleriyle doğrulama hakkında daha fazla bilgi için bkz: [geçirmek .NET çözümleri tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD dosyaları veya Pig işi bir parçası olarak çağrılan hello sunucuda komut dosyaları |Bash betiklerini kullanın |

### <a name="mapreduce"></a>MapReduce

| Üzerinde Windows tabanlı kullanmam... | Linux tabanlı... |
| --- | --- |
| C# Eşleyici ve reducer bileşenleri | C# Linux tabanlı Hdınsight bileşenleriyle doğrulama hakkında daha fazla bilgi için bkz: [geçirmek .NET çözümleri tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD dosyaları veya bir Hive işi bir parçası olarak çağrılan hello sunucuda komut dosyaları |Bash betiklerini kullanın |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Bir dış Oozie meta depo kullanırsanız, Linux tabanlı Hdınsight ile kullanmadan önce hello meta depo yedeklemeniz gerekir. Linux tabanlı Hdınsight uyumsuzlukları olabilir Oozie daha yeni sürümleriyle kullanılabilir önceki sürümleri tarafından oluşturulan meta deponuz ile.

Oozie iş akışları Kabuk eylemlerin sağlar. Kabuk eylemlerini hello varsayılan kabuğunu hello işletim sistemi toorun için komut satırı komutlarını kullanın. Windows Kabuğu hello üzerinde kullanan Oozie iş akışları varsa, hello iş akışları toorely hello Linux Kabuk ortamda (Bash) yeniden gerekir. Kabuk Eylemler Oozie ile kullanma hakkında daha fazla bilgi için bkz: [Oozie Kabuk eylem uzantısı](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).

Kabuk Eylemler çağrılan C# uygulamalarının Bel Oozie iş akışları varsa, bu uygulamalar Linux ortamında doğrulamanız gerekir. Daha fazla bilgi için bkz: [geçirmek .NET çözümleri tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| Üzerinde Windows tabanlı kullanmam... | Linux tabanlı... |
| --- | --- |
| Storm Panosu |Merhaba Storm Panosu kullanılabilir değil. Bkz: [dağıtma ve yönetme Storm topolojileri Linux tabanlı Hdınsight üzerinde](hdinsight-storm-deploy-monitor-topology-linux.md) yolları toosubmit topolojiler için |
| Storm kullanıcı Arabirimi |https://CLUSTERNAME.azurehdinsight.net/stormui Hello Storm kullanıcı Arabirimi kullanılabilir |
| Visual Studio toocreate, dağıtma ve C# veya karma topolojiler yönetme |Visual Studio kullanılan toocreate olması, dağıtmak ve C# (SCP.NET) veya karma topolojiler 28/10/2016 sonrasında oluşturulan Hdınsight kümelerinde Linux tabanlı Storm üzerinde yönetebilirsiniz. |

## <a name="hbase"></a>HBase

Linux tabanlı kümelerde hello znode üst HBase için olan `/hbase-unsecure`. Merhaba yapılandırmasında yerel HBase Java API kullanan herhangi bir Java istemci uygulaması için bu değeri ayarlayın.

Bkz: [bir Java tabanlı HBase uygulaması derleme](hdinsight-hbase-build-java-maven.md) bu değeri ayarlayan bir örnek istemcisi için.

## <a name="spark"></a>Spark

Spark kümeleri Önizleme sırasında Windows kümelerinde kullanılabilir. Spark GA yalnızca Linux tabanlı kümelerde ile kullanılabilir. Bir Windows tabanlı Spark Önizleme küme tooa yayın Spark Linux tabanlı kümeden geçiş yol yoktur.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="azure-data-factory-custom-net-activities"></a>Azure Data Factory özel .NET etkinlikler

Azure Data Factory özel .NET etkinlikler Linux tabanlı Hdınsight kümelerinde şu anda desteklenmemektedir. Bunun yerine, yöntemleri tooimplement özel etkinlikler ADF hattınızı bir parçası olarak aşağıdaki hello birini kullanmanız gerekir.

* .NET etkinliklerini Azure Batch havuzunda yürütün. Hello kullan Azure bağlı Batch hizmeti bölümüne bakın [bir Azure Data Factory ardışık düzeninde özel etkinlikleri kullanmak](../data-factory/data-factory-use-custom-activities.md)
* MapReduce etkinliği gibi Hello etkinlik uygulayın. Daha fazla bilgi için bkz: [MapReduce programlardan çağırma Data Factory](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Satır sonları

Genel olarak, Linux tabanlı sistemler LF kullanırken CRLF, satır sonları Windows tabanlı sistemlerde kullanın. Üretmek ya da, veri CRLF satır sonları ile beklediğiniz hello LF satır bitiş ile toomodify hello üreticileri ya da tüketicilere toowork gerekebilir.

Örneğin, Azure PowerShell tooquery kullanarak Windows tabanlı bir küme Hdınsight'ta CRLF verilerle döndürür. Merhaba Linux tabanlı bir küme ile aynı sorgu LF döndürür. Merhaba satır bitiş geçirmeden önce solutuion ile ilgili bir sorun neden olursa toosee sınamalısınız tooa Linux tabanlı küme.

Doğrudan hello Linux küme düğümlerinde yürütülen komut dosyalarınız varsa, her zaman LF hello satır bitiş olarak kullanmanız gerekir. CRLF kullanırsanız, hello betikleri Linux tabanlı bir kümede çalışırken hatalar görebilirsiniz.

Katıştırılmış CR karakterler dizelerle içermemesi hello betikleri biliyorsanız, yöntemler aşağıdaki hello birini kullanarak değişiklik hello satır sonları toplu düzenleyebilirsiniz:

* **Toohello küme karşıya yüklemeden önce**: PowerShell deyimleri toochange hello satır sonları CRLF tooLF hello betik toohello küme karşıya yüklemeden önce aşağıdaki kullanım hello.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Toohello küme karşıya sonra**: kullanım hello şu bir SSH oturumu toohello Linux tabanlı küme toomodify hello betik komutu.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Sonraki Adımlar

* [Nasıl toocreate Linux tabanlı Hdınsight kümeleri öğrenin](hdinsight-hadoop-provision-linux-clusters.md)
* [SSH tooconnect tooHDInsight kullanın](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Ambari kullanarak Linux tabanlı bir kümeyi yönetmek](hdinsight-hadoop-manage-ambari.md)
