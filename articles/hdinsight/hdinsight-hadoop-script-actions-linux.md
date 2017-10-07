---
title: "Linux tabanlı Hdınsight - Azure ile aaaScript eylem geliştirme | Microsoft Docs"
description: "Nasıl toocustomize Linux tabanlı Hdınsight kümeleri toouse Bash betiklerini öğrenin. Merhaba betik eylemi özelliği hdınsight sırasında veya Küme oluşturulduktan sonra toorun komut dosyaları sağlar. Komut dosyaları, küme yapılandırma ayarlarının kullanılan toochange olması veya ek yazılım yüklemesi."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Hdınsight ile betik eylemi geliştirme

Bilgi toocustomize Hdınsight küme kullanarak nasıl Bash betikleri. Betik yolu toocustomize Hdınsight sırasında veya Küme oluşturulduktan sonra eylemlerdir.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-are-script-actions"></a>Betik eylemleri nelerdir

Betik eylemleri hello küme düğümleri toomake yapılandırma değişiklikleri Azure çalışır Bash betikleridir veya yazılımı yükleyin. Betik eylemi kök olarak yürütülür ve tam erişim hakları toohello küme düğümleri sağlar.

Betik eylemleri yöntemler aşağıdaki hello uygulanabilir:

| Bu yöntem tooapply bir komut dosyası kullan... | Sırasında oluşturma küme... | Çalıştıran bir kümede... |
| --- |:---:|:---:|
| Azure portalına |✓ |✓ |
| Azure PowerShell |✓ |✓ |
| Azure CLI |&nbsp; |✓ |
| HDInsight .NET SDK'sı |✓ |✓ |
| Azure Resource Manager şablonu |✓ |&nbsp; |

Bu yöntemleri tooapply betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Komut dosyası geliştirme için en iyi yöntemler

Hdınsight kümesi için özel bir komut dosyası geliştirirken göz önünde birkaç en iyi yöntemler tookeep vardır:

* [Hedef hello Hadoop sürümü](#bPS1)
* [Hedef hello işletim sistemi sürümü](#bps10)
* [Kararlı tooscript kaynaklara bağlantılar sağlar](#bPS2)
* [Önceden derlenmiş kaynakları kullanın](#bPS4)
* [Komut dosyasını Hello kümede özelleştirme ıdempotent olduğundan emin olun](#bPS3)
* [Yüksek kullanılabilirlik hello küme mimarisinin emin olun](#bPS5)
* [Merhaba özel bileşenler toouse Azure Blob depolama alanını yapılandırma](#bPS6)
* [Bilgi tooSTDOUT ve STDERR yazma](#bPS7)
* [Dosyaları ASCII olarak LF satır sonları ile kaydedin.](#bps8)
* [Geçici hataları yeniden deneme mantığı toorecover kullanın](#bps9)

> [!IMPORTANT]
> Betik eylemleri 60 dakika içinde tamamlamanız gerekir veya hello işlemi başarısız olur. Düğüm sağlama işlemi sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak hello komut dosyasını çalıştırır. CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden hello betik tootake uzun toofinish neden olabilir.

### <a name="bPS1"></a>Hedef hello Hadoop sürümü

Farklı sürümlerini Hdınsight Hadoop Hizmetleri ve bileşenleri yüklü farklı sürümlerine sahip. Komut bir hizmet veya bileşenin belirli bir sürümünü görüyorsa yalnızca hello betik hello gerekli bileşenleri içerir Hdınsight hello sürümü ile kullanmanız gerekir. Hello kullanarak Hdınsight ile dahil bileşen sürümleri hakkında bilgi bulabilirsiniz [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.

### <a name="bps10"></a>Hedef hello işletim sistemi sürümü

Linux tabanlı Hdınsight Ubuntu Linux dağıtım hello üzerinde temel alır. Hdınsight farklı sürümlerini farklı sürümlerine ilişkin kodunuzu nasıl davranacağını değişebilir Ubuntu kullanır. Örneğin, Hdınsight 3.4 ve önceki Upstart kullanmak Ubuntu sürümlerinde dayalı. Sürüm 3.5 Systemd kullanan Ubuntu 16.04 üzerinde temel alır. Kodunuzu toowork hem yazılması gereken şekilde Systemd ve Upstart farklı komutlarını kullanır.

Başka bir önemli fark Hdınsight 3.4 3.5 arasındaki `JAVA_HOME` şimdi tooJava 8 işaret eder.

Merhaba işletim sistemi sürümünü kullanarak denetleyebilirsiniz `lsb_release`. Merhaba aşağıdaki kodu toodetermine Merhaba, nasıl bir komut dosyası gösterilmektedir Ubuntu 14 ya da 16 çalıştırıyor:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Bu parçacıkları https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh adresindeki içeren hello tam komut dosyası bulabilirsiniz.

Merhaba Hdınsight tarafından kullanılan Ubuntu Hello sürümü için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md) belge.

toounderstand hello farklarını Systemd ve Upstart, bkz: [Systemd Upstart kullanıcılar için](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Kararlı tooscript kaynaklara bağlantılar sağlar

Merhaba komut dosyası ve ilişkili kaynakları hello küme hello ömrü kullanılabilir kalmalıdır. Yeni düğümler toohello küme ölçeklendirme işlemleri sırasında eklenirse, bu kaynakları gereklidir.

Merhaba en iyi uygulama toodownload olduğunu ve her şeyi aboneliğinizi Azure depolama hesabında arşivleyin.

> [!IMPORTANT]
> Itanium tabanlı sistemler için hello varsayılan depolama hesabı hello küme ya da bir ortak, salt okunur kapsayıcı için başka bir depolama hesabı üzerinde kullanılan hello depolama hesabı olmalıdır.

Örneğin, Microsoft tarafından sağlanan hello örnekleri hello depolanan [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) depolama hesabı. Bu hello Hdınsight ekibi tarafından korunan bir ortak, salt okunur kapsayıcıdır.

### <a name="bPS4"></a>Önceden derlenmiş kaynakları kullanın

tooreduce hello alır toorun hello betik süresi, kaynak kodu kaynaklardan derleme işlemlerden kaçının. Örneğin, önceden derleme kaynakları ve bunları bir Azure depolama hesabı blob hello depolamak Hdınsight olarak aynı veri merkezinde.

### <a name="bPS3"></a>Komut dosyasını Hello kümede özelleştirme ıdempotent olduğundan emin olun

Komut dosyaları ıdempotent olması gerekir. Merhaba betik birden çok kez çalıştırılıp çalıştırılmadığını döndürme zorunluluğu her zaman aynı durumu kümeyi toohello hello.

Örneğin, yapılandırma dosyalarını değiştiren bir komut dosyası yinelenen giriş varsa eklememelisiniz birden çok kez çalıştı.

### <a name="bPS5"></a>Yüksek kullanılabilirlik hello küme mimarisinin emin olun

Linux tabanlı Hdınsight kümeleri hello küme içinde etkin olan iki baş düğümler sağlar ve her iki düğümde betik eylemleri çalıştırın. Yüklediğiniz hello bileşenleri tek bir baş düğüm bekliyorsanız, hello bileşenleri her iki baş düğümler üzerinde yüklemeyin.

> [!IMPORTANT]
> Hdınsight bir parçası olarak sağlanan tasarlanmış toofail üzerinden hello iki baş düğümler arasında gerektiği gibi hizmetlerdir. Bu işlev toocustom bileşenleri betik eylemleri ile genişletilmedi. Özel bileşenler için yüksek kullanılabilirlik gerekiyorsa, kendi yük devretme mekanizması uygulamalıdır.

### <a name="bPS6"></a>Merhaba özel bileşenler toouse Azure Blob depolama alanını yapılandırma

Merhaba kümede yüklemek bileşenleri Hadoop dağıtılmış dosya sistemi (HDFS) depolama kullanan bir varsayılan yapılandırmaya sahip olabilir. Hdınsight Azure Storage veya Data Lake Store hello varsayılan depolama alanı olarak kullanır. Her iki hello küme silinse bile veri devam ederse bir HDFS uyumlu bir dosya sistemi sağlar. Tooconfigure bileşenleri toouse WASB veya HDFS yerine ADL yüklemeniz gerekebilir.

İşlemlerinin çoğu için toospecify hello dosya sistemi gerekmez. Örneğin, hello aşağıdaki hello giraph examples.jar dosya hello yerel dosya sistemi toocluster depolama biriminden kopyalar:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

Bu örnekte, hello `hdfs` komutu hello varsayılan küme depolama saydam olarak kullanır. Bazı işlemler için toospecify hello URI gerekebilir. Örneğin, `adl:///example/jars` Data Lake Store için veya `wasb:///example/jars` Azure depolama.

### <a name="bPS7"></a>Bilgi tooSTDOUT ve STDERR yazma

Hdınsight yazılı tooSTDOUT ve STDERR komut çıktısının günlüğe kaydeder. Merhaba Ambari web kullanıcı arabirimini kullanarak bu bilgileri görüntüleyebilirsiniz.

> [!NOTE]
> Ambari, yalnızca hello küme başarıyla oluşturulduysa kullanılabilir. Küme oluşturma ve oluşturma başarısız sırasında bir betik eylemi kullanın, hello sorun giderme bölümüne bakın. [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) günlüğe kaydedilen bilgileri erişme diğer yolları için.

Tooadd ek günlük isteyebilirsiniz ancak çoğu yardımcı programları ve yükleme paketleri zaten bilgi tooSTDOUT ve STDERR, yazma. toosend metin tooSTDOUT, kullanım `echo`. Örneğin:

```bash
echo "Getting ready tooinstall Foo"
```

Varsayılan olarak, `echo` hello dize tooSTDOUT gönderir. toodirect, tooSTDERR, ekleme `>&2` önce `echo`. Örneğin:

```bash
>&2 echo "An error occurred installing Foo"
```

Bunun yerine tooSTDOUT tooSTDERR (2) yazılan bilgilerin yönlendirir. G/ç yeniden yönlendirme hakkında daha fazla bilgi için bkz: [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Betik eylemleri tarafından günlüğe kaydedilen bilgi görüntüleme hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a>Dosyaları ASCII olarak LF satır sonları ile kaydedin.

Bash betiklerini ASCII biçiminde LF tarafından sonlandırıldı çizgili depolanması gerekir. UTF-8 olarak depolanır veya CRLF hello satır bitiş olarak kullanan dosyalar hello aşağıdaki hata ile başarısız:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Geçici hataları yeniden deneme mantığı toorecover kullanın

Dosyaları indirilirken alma apt ya da üzerinden veri aktaran diğer eylemler kullanarak paketleri yükleme Internet Merhaba, hello eylem tootransient ağ hataları başarısız olabilir. Örneğin, hello uzak kaynak ile iletişim kuran tooa yedekleme düğüm üzerinde başarısız hello işleminde olabilir.

toomake, komut dosyası dayanıklı tootransient hataları yeniden deneme mantığı uygulayabilirsiniz. tooimplement mantığı nasıl yeniden deneme işlevi aşağıdaki hello gösterir. Bu, üç kez başarısız olmadan önce hello işlemini yeniden dener.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Merhaba aşağıdaki örneklerde görüldüğü nasıl toouse bu işlev.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Özel komut dosyaları için yardımcı yöntemleri

Betik eylem Yardımcısı yöntemleri özel komut dosyaları yazılırken kullanabileceğiniz yardımcı programları ' dir. Bu yöntemler bulunan[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) komut dosyası. Toodownload aşağıdaki hello ve komut dosyanızı bir parçası olarak kullanın:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

komut dosyanız için kullanılabilir Yardımcıları aşağıdaki hello:

| Yardımcı kullanımı | Açıklama |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Bir dosya hello Kaynak URI toohello belirtilen dosya yolundan indirir. Varsayılan olarak, varolan bir dosyanın üzerine yazmaz. |
| `untar_file TARFILE DESTDIR` |Tar dosyasını ayıklar (kullanarak `-xf`) toohello hedef dizini. |
| `test_is_headnode` |Bir küme baş düğümünde, dönüş 1; çalışan Aksi takdirde, 0. |
| `test_is_datanode` |Merhaba geçerli düğüm (çalışan) veri düğümü ise 1 döner; Aksi takdirde, 0. |
| `test_is_first_datanode` |Merhaba geçerli düğüm hello ilk veri (çalışan) ise düğümü (adlandırılmış workernode0) 1 döner; Aksi takdirde, 0. |
| `get_headnodes` |Merhaba headnodes hello kümedeki dönüş hello tam etki alanı adı. Virgülle ayrılmış adlardır. Boş bir dize hatası döndürülür. |
| `get_primary_headnode` |Merhaba birincil headnode Hello tam etki alanı adını alır. Boş bir dize hatası döndürülür. |
| `get_secondary_headnode` |Merhaba ikincil headnode Hello tam etki alanı adını alır. Boş bir dize hatası döndürülür. |
| `get_primary_headnode_number` |Merhaba birincil headnode Hello sayısal sonekini alır. Boş bir dize hatası döndürülür. |
| `get_secondary_headnode_number` |Merhaba ikincil headnode Hello sayısal sonekini alır. Boş bir dize hatası döndürülür. |

## <a name="commonusage"></a>Genel kullanım desenleri

Bu bölümde, kendi özel bir komut dosyası yazılırken içine çalışabilecek hello ortak kullanım desenlerini bazıları uygulama yönergeler sağlanmaktadır.

### <a name="passing-parameters-tooa-script"></a>Tooa komut parametreleri geçirme

Bazı durumlarda, komut parametreleri gerektirebilir. Örneğin, hello Ambari REST API kullanırken hello küme için hello yönetici parolası gerekebilir.

Toohello betik geçirilen parametre olarak bilinen *konumsal parametreler*ve çok atanan`$1` hello ilk parametresi, `$2` hello ikinci ve böylece açma için. `$0`Merhaba komut dosyasının kendisini Hello adını içerir.

Toohello betik parametre olarak geçirilen değerleri (') tek tırnak içine. Geçirilen değer bu hello sabit değer olarak kabul edilir sağlar.

### <a name="setting-environment-variables"></a>Ortam değişkenlerini ayarlama

Bir ortam değişkeni ayarı deyiminden hello tarafından gerçekleştirilir:

    VARIABLENAME=value

Burada VARIABLENAME hello hello değişkenin adıdır. tooaccess hello değişken, kullanım `$VARIABLENAME`. Örneğin, parola tooassign adlı konumsal parametre olarak bir ortam değişkeni tarafından sağlanan bir değer, aşağıdaki ifadeyi hello kullanırsınız:

    PASSWORD=$1

Sonraki erişim toohello bilgileri daha sonra kullanabilir `$PASSWORD`.

Ortam değişkenleri Hello betik Ayarla yalnızca hello hello betik kapsamında mevcut. Bazı durumlarda, hello betik tamamlandıktan sonra korunur tooadd sistem geneli ortam değişkenleri gerekebilir. tooadd sistem geneli ortam değişkenleri eklemek hello değişkeni çok`/etc/environment`. Örneğin, aşağıdaki ifadeyi hello ekler `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Merhaba özel komut dosyalarının depolandığı toolocations erişim

Kullanılan komut toocustomize bir küme hello aşağıdaki konumlardan birinde depolanan toobe gerekir:

* Bir __Azure depolama hesabı__ hello kümeyle ilişkili.

* Bir __ek depolama alanı hesabı__ hello kümesi ile ilişkili.

* A __herkese açık şekilde okunabilir URI__. Örneğin, bir URL toodata OneDrive, Dropbox veya barındırma hizmeti başka bir dosyaya depolanan.

* Bir __Azure Data Lake Store hesabı__ hello Hdınsight kümesi ile ilişkili. Hdınsight ile Azure Data Lake Store kullanma hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Merhaba hizmet asıl Hdınsight kullandığı tooaccess Data Lake Store okuma erişimi toohello komut dosyası olması gerekir.

Merhaba komut dosyası tarafından kullanılan kaynakları da genel kullanıma açık olması gerekir.

Bir Azure depolama hesabı ya da Azure Data Lake Store Hello dosyaların depolanması hello Azure ağı içinde her ikisi olarak hızlı erişim sağlar.

> [!NOTE]
> Merhaba URI kullanılan biçimi tooreference hello betik kullanılan hello hizmete bağlı olarak farklılık gösterir. Merhaba Hdınsight kümesiyle ilişkili depolama hesapları için `wasb://` veya `wasbs://`. Genel olarak okunabilir URI'ler için kullanmak `http://` veya `https://`. Data Lake Store için kullanma `adl://`.

### <a name="checking-hello-operating-system-version"></a>Merhaba işletim sistemi sürüm denetimi

Hdınsight farklı sürümlerini Ubuntu belirli sürümlerini kullanır. Komut dosyanız için denetlemelisiniz işletim sistemi sürümleri arasındaki farklar olabilir. Örneğin, tooinstall Ubuntu bağlı toohello sürümü bir ikili gerekebilir.

toocheck hello işletim sistemi sürümü, kullanım `lsb_release`. Örneğin, komut dosyası izleyen hello nasıl işletim sistemi sürümü hello bağlı olarak dosya tooreference belirli tar gösterir:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Betik eylemi dağıtma denetim listesi

Biz toodeploy bu komut dosyalarını hazırlanırken sürdü hello adımlar şunlardır:

* Merhaba, dağıtım sırasında hello küme düğümleri tarafından erişilebilen bir yerde özel komut dosyaları içeren hello dosyaları yerleştirin. Örneğin, varsayılan depolama hello küme için hello. Dosyaları herkese açık şekilde okunabilir barındırma hizmetleri de depolanabilir.
* Merhaba betik impotent olduğunu doğrulayın. Bunun yapılması verir hello betik toobe yürütülen birden çok kez hello üzerinde aynı düğüm.
* Bir geçici dosya dizin tmp tookeep hello kullan hello komut dosyaları tarafından kullanılan dosyaları indirilir ve komut dosyaları çalıştırdıktan sonra sonra bunları Temizle.
* İşletim sistemi düzeyinde ayarlarını veya Hadoop hizmeti yapılandırma dosyalarını değiştirdiyseniz, toorestart Hdınsight Hizmetleri isteyebilirsiniz.

## <a name="runScriptAction"></a>Nasıl toorun betik eylemi

Yöntemler aşağıdaki hello kullanarak betik eylemleri toocustomize Hdınsight kümelerini kullanabilirsiniz:

* Azure portalına
* Azure PowerShell
* Azure Resource Manager şablonları
* Merhaba Hdınsight .NET SDK'sı.

Her yöntemi kullanma hakkında daha fazla bilgi için bkz: [nasıl toouse betik eylemi](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Özel kod örnekleri

Microsoft, bir Hdınsight kümesine tooinstall bileşenleri örnek komut dosyaları sağlar. Daha fazla örnek betik eylemleri için bağlantıları aşağıdaki hello bakın.

* [Yükleme ve Hdınsight kümelerinde ton kullanın](hdinsight-hadoop-hue-linux.md)
* [Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install-linux.md)
* [Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install-linux.md)
* [Yükleme veya Hdınsight kümelerinde Mono yükseltme](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Sorun giderme

Merhaba, geliştirilmiş komut dosyaları kullanırken karşılaşabileceğiniz hatalar şunlardır:

**Hata**: `$'\r': command not found`. Bazen arkasından `syntax error: unexpected end of file`.

*Neden*: CRLF ile bir betik hello satırlarında sonlandırdığınızda, bu hataya neden olur. UNIX sistemleri yalnızca LF hello satır bitiş olarak bekler.

Merhaba komut dosyası bir Windows ortamı yazılan CRLF birçok metin düzenleyicileri Windows'da için bitiş ortak bir çizgi olarak çoğunlukla oluşur.

*Çözümleme*: metin düzenleyicinizde bir seçenek ise, UNIX biçimini veya LF hello satır bitiş için seçin. Ayrıca UNIX sistem toochange hello CRLF tooan LF komutları aşağıdaki hello kullanabilirsiniz:

> [!NOTE]
> Merhaba CRLF satır sonları tooLF değiştirmeniz gerekir, hello aşağıdaki komutlar kabaca eşdeğerdir. Merhaba yardımcı programları sisteminizdeki kullanılabilir göre seçin.

| Komut | Notlar |
| --- | --- |
| `unix2dos -b INFILE` |Merhaba özgün dosya yedeklenir ile bir. BAK uzantısı |
| `tr -d '\r' < INFILE > OUTFILE` |Yalnızca LF sonları sürümüyle ÇIKIŞDOSYASI içerir |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Merhaba dosyasını doğrudan değiştirir |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |ÇIKIŞDOSYASI yalnızca LF sonları ile bir sürüm içeriyor. |

**Hata**: `line 1: #!/usr/bin/env: No such file or directory`.

*Neden*: Bu hata hello betik UTF-8 bir bayt sırası işareti (BOM) ile olarak kaydedildi oluşur.

*Çözümleme*: Kaydet hello dosya olarak ASCII veya UTF-8 bir ürün reçetesi olmadan olarak. Ayrıca, bir Linux veya UNIX sistem toocreate hello AĞACI olmadan bir dosya üzerinde komutu aşağıdaki hello kullanabilirsiniz:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Değiştir `INFILE` hello dosyasıyla AĞACI hello içeren. `OUTFILE`Merhaba AĞACI kullanmadan hello komut içeren yeni bir dosya adı olmalıdır.

## <a name="seeAlso"></a>Sonraki adımlar

* Nasıl çok öğrenin[özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)
* Kullanım hello [Hdınsight .NET SDK'sı başvurusu](https://msdn.microsoft.com/library/mt271028.aspx) toolearn Hdınsight yönetmek .NET uygulamaları oluşturma hakkında daha fazla bilgi
* Kullanım hello [Hdınsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn nasıl toouse REST tooperform yönetim eylemleri hdınsight kümeleri.
