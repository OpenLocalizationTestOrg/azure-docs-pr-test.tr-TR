---
title: "aaaScript Hdınsight - Azure ile eylemi geliştirme | Microsoft Docs"
description: "Betik eylemi ile nasıl toocustomize Hadoop kümeleri hakkında bilgi edinin. Betik eylemi bir kümeye yüklü uygulamaların Hadoop küme veya toochange hello yapılandırması üzerinde çalışan kullanılan tooinstall ek yazılım olabilir."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Hdınsight Windows tabanlı kümeler için betik eylemi betikleri geliştirme
Hdınsight için nasıl toowrite betik eylemi komutlar hakkında bilgi edinin. Betik eylemi komut dosyalarını kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md). Linux tabanlı Hdınsight kümeleri için yazılmış aynı makalenin Merhaba bkz [Hdınsight betik eylemi geliştirme betikleri](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Bu belge yalnızca iş için Windows tabanlı Hdınsight kümeleri Hello adımları. Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Betik eylemleri Linux tabanlı kümelerde ile kullanma hakkında daha fazla bilgi için bkz: [(Linux) Hdınsight ile betik eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).
>
>



Betik eylemi bir kümeye yüklü uygulamaların Hadoop küme veya toochange hello yapılandırması üzerinde çalışan kullanılan tooinstall ek yazılım olabilir. Betik eylemleri Hdınsight kümeleri dağıtıldığında hello küme düğümleri üzerinde çalışan bir komut dosyası olan ve hello kümedeki düğümler Hdınsight yapılandırmasını tamamladıktan sonra yürütülür. Betik eylemi sistem yönetici hesabı ayrıcalıklarıyla yürütülür ve tam erişim hakları toohello küme düğümleri sağlar. Her küme, belirtilen hello sırayla yürütülen betik eylemleri toobe listesiyle sağlanabilir.

> [!NOTE]
> Aşağıdaki hata iletisini hello karşılaşırsanız:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello terim 'Kaydet-HDIFile' hello adı cmdlet, işlev, komut dosyası veya çalıştırılabilir program olarak tanınmıyor. Merhaba hello adının yazımını denetleyin veya bir yol birlikte verildiyse, o hello yolun doğru olduğunu doğrulayın ve yeniden deneyin.
> Merhaba yardımcı yöntemler eklemediniz olmasıdır.  Bkz: [özel komut dosyaları için yardımcı yöntemleri](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Örnek komut dosyaları
Windows işletim sisteminde Hdınsight kümeleri oluşturmak için hello betik eylemi Azure PowerShell komut dosyasıdır. Merhaba aşağıdaki betiği hello site yapılandırma dosyalarını yapılandırmaya ilişkin bir örnek gösterilmektedir:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

Merhaba betiği dört parametreleri, hello yapılandırma dosyasının adını, toomodify, tooset ve bir açıklama istediğiniz hello değeri istediğiniz hello özelliği alır. Örneğin:

    hive-site.xml hive.metastore.client.socket.timeout 90

Bu parametreler hello hive-site.xml dosyasında hello hive.metastore.client.socket.timeout değeri too90 ayarlar.  Merhaba varsayılan değer 60 saniyedir.

Bu örnek komut dosyası ayrıca bulunabilir [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

Hdınsight birkaç betikler Hdınsight kümelerinde tooinstall ek bileşenleri sağlar:

| Ad | Betik |
| --- | --- |
| **Spark yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-installer-v03.ps1. Bkz: [yükleme ve kullanma hdınsight'ta Spark kümeleri][hdinsight-install-spark]. |
| **R yükleme** |https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-installer-v02.ps1. Bkz: [yükleme ve kullanma R Hdınsight kümelerinde][hdinsight-r-scripts]. |
| **Solr yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-installer-v01.ps1. Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install.md). |
| - **Giraph yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-installer-v01.ps1. Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install.md). |

Betik eylemi hello Azure portal, Azure PowerShell dağıtılabilir veya Hdınsight .NET SDK kullanarak hello.  Daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak][hdinsight-cluster-customize].

> [!NOTE]
> Merhaba örnek betikler yalnızca Hdınsight kümesi sürüm 3.1 veya üzeri çalışır. Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Özel komut dosyaları için yardımcı yöntemleri
Betik eylem Yardımcısı yöntemleri özel komut dosyaları yazılırken kullanabileceğiniz yardımcı programları ' dir. Bu yöntemler tanımlanan [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), komut dosyalarınızı örnek aşağıdaki hello kullanarak eklenebilir:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Bu komut dosyası tarafından sağlanan hello yardımcı yöntemler şunlardır:

| Yardımcı yöntemi | Açıklama |
| --- | --- |
| **Kaydet-HDIFile** |İndirme hello dosyasından Tekdüzen Kaynak Tanımlayıcısı (URI) tooa konumu hello Azure VM düğümü atanan toohello kümesi ile ilişkili hello yerel diskte belirtilmiş. |
| **Genişletme HDIZippedFile** |Sıkıştırılmış bir dosya sıkıştırmasını açın. |
| **Çağırma HDICmdScript** |Bir komut dosyası cmd.exe çalıştırın. |
| **Yazma HDILog** |Bir komut dosyası eylemi için kullanılan hello özel komut dosyasından çıkış yazma. |
| **Get-Services** |Burada hello betiği yürüten hello makine üzerinde çalışan hizmetlerin listesini alın. |
| **Get-Service** |Giriş olarak Hello belirli hizmet adı ile belirli bir hizmet için ayrıntılı bilgi almak (hizmet adı, işlem kimliği, durum, vb.) hello makinede burada hello betik yürütür. |
| **Get-HDIServices** |Burada hello betiği yürüten hello bilgisayarda çalışan Hdınsight hizmetlerin listesini alın. |
| **Get-HDIService** |Merhaba belirli Hdınsight hizmet adı ile giriş olarak, belirli bir hizmet için ayrıntılı bilgi almak (hizmet adı, işlem kimliği, durum, vb.) hello makinede burada hello betik yürütür. |
| **Get-ServicesRunning** |Burada hello betiği yürüten hello bilgisayarda çalışan hizmetlerin listesini alın. |
| **Get-ServiceRunning** |Burada hello betiği yürüten (adına göre) belirli bir hizmet hello bilgisayarda çalışıp çalışmadığını denetleyin. |
| **Get-HDIServicesRunning** |Burada hello betiği yürüten hello bilgisayarda çalışan Hdınsight hizmetlerin listesini alın. |
| **Get-HDIServiceRunning** |Burada hello betiği yürüten (adına göre) belirli bir Hdınsight hizmet hello bilgisayarda çalışıp çalışmadığını denetleyin. |
| **Get-HDIHadoopVersion** |Burada hello betiği yürüten hello bilgisayarda yüklü Hadoop Hello sürümünü alır. |
| **Test-IsHDIHeadNode** |Merhaba bilgisayar burada hello betiği yürüten bir baş düğüm olup olmadığını denetleyin. |
| **Test-IsActiveHDIHeadNode** |Burada hello betiği yürüten hello bilgisayar etkin bir baş düğüm olup olmadığını denetleyin. |
| **Test-IsHDIDataNode** |Burada hello betiği yürüten hello bilgisayar veri düğümü olup olmadığını denetleyin. |
| **Düzen HDIConfigFile** |Merhaba yapılandırma dosyaları hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml veya yarn-site.xml düzenleyin. |

## <a name="best-practices-for-script-development"></a>Komut dosyası geliştirme için en iyi yöntemler
Hdınsight kümesi için özel bir komut dosyası geliştirirken göz önünde birkaç en iyi yöntemler tookeep vardır:

* Merhaba Hadoop sürüm denetimi

    Yalnızca Hdınsight sürüm 3.1 (Hadoop 2.4) ve betik eylemi tooinstall özel bileşenleri kullanan bir kümede desteği üstünde. Özel betiğinizde hello kullanmalısınız **Get-HDIHadoopVersion** yardımcı yöntem toocheck hello Hadoop sürüm hello komut dosyasında diğer görevleri gerçekleştirme ile devam etmeden önce.
* Kararlı tooscript kaynaklara bağlantılar sağlar

    Kullanıcılar tüm hello betikler ve bir küme hello özelleştirmesinde kullanılan diğer yapıları hello küme hello ömrü kullanılabilir kalmasını ve bu dosyaların sürümleri hello hello süresince değiştirmeyin emin olmanız gerekir. Merhaba kümedeki düğümlerin Hello yeniden görüntüsünü oluşturuyor gerekliyse, bu kaynakları gereklidir. Merhaba en iyi uygulama toodownload olduğunu ve kullanıcı denetimleri hello depolama hesabındaki her şeyi arşivleyin. Bu hello varsayılan depolama hesabı ya da herhangi bir anda hello dağıtımının özelleştirilmiş bir küme için belirtilen hello ek depolama hesapları olabilir.
    Merhaba belgelerinde, örneğin, biz hello kaynakları yerel bir kopyasını bu depolama hesabında yapmış olduğunuz sağlanan hello Spark ve R küme örnekleri özelleştirilmiş: https://hdiconfigactions.blob.core.windows.net/.
* Komut dosyasını Hello kümede özelleştirme ıdempotent olduğundan emin olun

    Hdınsight kümesi hello düğümlerinin hello küme ömrü boyunca yeniden olduğunu beklediğiniz gerekir. bir küme yeniden her hello küme özelleştirme betiği çalıştırılır. Bu komut dosyası tasarlanmış toobe ıdempotent yeniden görüntüsünü oluşturuyor bağlı hello betik bu hello küme aynı yalnızca hello betik Merhaba zaman hello küme başlangıçta olan ilk kez çalıştırdıktan sonra durumla durumu özelleştirilmiş toohello döndürülür emin olması hello herkese açık olması gerekir oluşturulur. Örneğin, özel bir komut dosyası D:\AppLocation uygulama yüklerseniz, ilk çalıştırın, sonra yeniden görüntüsünü oluşturuyor, bağlı her sonraki çalıştırmada hello betik Merhaba uygulaması hello D:\AppLocation konumu diğer işlemine devam etmeden önce mevcut olup olmadığını denetlemeniz gerekir Merhaba betik adımları.
* Merhaba en iyi konumda özel bileşenlerini yükle

    Küme düğümleri yeniden zaman hello C:\ kaynak sürücüde ve D:\ sistem sürücüsünde, hello veri kaybına ve bu sürücülerde yüklemiş olduğu uygulamalar sonuçta yeniden biçimlendirilebileceği. Merhaba kümesinin parçası olan bir Azure sanal makine (VM) düğüm arıza ve yeni bir düğüm tarafından değiştirilirse bu de olabilir. Merhaba D:\ sürücüsüne veya hello C:\apps konumda hello küme bileşenleri yükleyebilirsiniz. Diğer tüm konumlara hello C:\ sürücüsü üzerindeki ayrılmıştır. Uygulamaları veya kitaplıkları toobe komut dosyasını hello kümede özelleştirme yüklü olduğu hello konumu belirtin.
* Yüksek kullanılabilirlik hello küme mimarisinin emin olun

    Yüksek kullanılabilirlik için bir Aktif-Pasif mimari Hdınsight sahipse, hangi bir baş düğüm (Merhaba Hdınsight Hizmetleri çalıştırdığınız) etkin modda hello diğer olup baş düğüm (hangi Hdınsight'ta Hizmetleri çalışmıyor) bekleme modunda olur. Hdınsight Hizmetleri kesilirse hello düğümleri etkin ve Pasif modları. Betik eylemi yüksek kullanılabilirlik için iki baş düğümler üzerinde kullanılan tooinstall Hizmetleri ise, o hello Hdınsight yük devretme mekanizması mümkün tooautomatically başarısız bu kullanıcı tarafından yüklenen hizmetleri olup olmadığını unutmayın. Bu nedenle kullanıcı yüklü hizmetler beklenen toobe yüksek oranda kullanılabilir olan Hdınsight baş düğümler üzerinde kendi Aktif-Pasif modu, yük devretme yönteminde sahip veya etkin-etkin modunda olması.

    Merhaba baş düğüm rolünü hello değer olarak belirtildiğinde bir Hdınsight betik eylemi komutu her iki baş düğümler üzerinde çalışır *ClusterRoleCollection* parametresi. Bu nedenle özel bir komut dosyası tasarlarken, kodunuzu bu kurulumu farkında olduğundan emin olun. Burada hello aynı hizmetleri yüklenir ve her iki hello baş düğümü üzerinde başlatıldı ve birbirleri ile rekabet bitiş sorunlar çalışmamalıdır. Betik eylemi yüklenen yazılım toobe dayanıklı toosuch olayları nedenle Ayrıca, yeniden görüntüleme sırasında veri kaybı olmamasına dikkat edin. Uygulamaları birçok düğümüne dağıtılmış yüksek oranda kullanılabilir verilerle tasarlanmış toowork olmalıdır. Hello kadar 1/5 bir kümede hello düğümlerinin yeniden olduğunu unutmayın aynı anda.
* Merhaba özel bileşenler toouse Azure Blob depolama alanını yapılandırma

    Merhaba küme düğümlerine yükleyin hello özel bileşenler varsayılan yapılandırma toouse Hadoop dağıtılmış dosya sistemi (HDFS) depolama olabilir. Bunun yerine hello yapılandırma toouse Azure Blob Depolama değiştirmeniz gerekir. Bir küme yeniden görüntü oluşturma, hello HDFS dosya sistemi ile biçimlendirilmiş ve orada depolanan tüm verileri kaybedersiniz. Azure Blob storage kullanarak, bunun yerine, verilerinizi tutulur sağlar.

## <a name="common-usage-patterns"></a>Genel kullanım desenleri
Bu bölümde, kendi özel bir komut dosyası yazılırken içine çalışabilecek hello ortak kullanım desenlerini bazıları uygulama yönergeler sağlanmaktadır.

### <a name="configure-environment-variables"></a>Ortam değişkenleri yapılandırın
Genellikle betik eylemi geliştirme tooset ortam değişkenleri gereksinim hello düşündüğünüz. Bir ikili dış sitesinden, hello kümede yüklemek ve yüklü tooyour 'PATH' ortam değişkeni olduğu, hello konumu eklediğinizde örneği için en olası senaryodur. Aşağıdaki kod parçacığında hello nasıl özel bir komut dosyası tooset ortam değişkenleri hello gösterir.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Bu bildirimi hello ortam değişkenini ayarlar **MDS_RUNNER_CUSTOM_CLUSTER** toohello değeri 'true' ve ayrıca kümeleri hello Bu değişken toobe makine genelinde kapsamı. Zaman zaman ortam değişkenleri hello uygun kapsamda – makine ya da kullanıcı ayarlanır önemlidir. Başvuru [burada] [ 1] ortam değişkenlerini ayarlama hakkında daha fazla bilgi.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Merhaba özel komut dosyalarının depolandığı toolocations erişim
Kullanılan komut toocustomize küme gereksinimlerini tooeither hello küme için hello varsayılan depolama hesabı veya başka bir depolama hesabı üzerinde genel bir salt okunur kapsayıcı olabilir. Kodunuzu başka bir yerde bulunan kaynaklara erişirse bu genel olarak erişilebilir içinde toobe gerekir (en az genel salt okunur). Örneği için bir dosya tooaccess istediğiniz ve hello SaveFile HDI komutunu kullanarak kaydedin.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

Bu örnekte, bu hello kapsayıcı 'somestorageaccount' depolama hesabındaki ' somecontainer' genel olarak erişilebilir olduğundan emin olmalısınız. Aksi takdirde hello betik 'Bulunamadı' bir özel durum oluşturur ve başarısız.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Parametreleri toohello Ekle-AzureRmHDInsightScriptAction cmdlet'i geçirin
toopass birden çok parametre toohello Ekle-AzureRmHDInsightScriptAction cmdlet'i hello komut dosyası için tüm parametreleri tooformat hello dize değeri toocontain gerekir. Örneğin:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

or

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Başarısız Küme dağıtımı için özel durum
Tooget doğru şekilde hello olgu bildirim istiyorsanız o küme özelleştirme beklendiği gibi başarılı olmadı, önemli toothrow bir işlemdir ve hello küme oluşturma işlemi başarısız. Örneğin, tooprocess bir dosya varsa istediğiniz ve burada hello dosya yok hello hata durumu işlemek. Bu, başlangıç komut dosyası düzgün biçimde çıkar ve hello kümenin hello durumunu doğru şekilde bilinen emin olun. Merhaba aşağıdaki kod parçacığında verir nasıl bir örnek tooachieve bu:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

Merhaba dosya olmasaydı, bu parçacığında, bunu burada hello komut gerçekte düzgün biçimde hello hata iletisini yazdırdıktan sonra çıkar ve hello küme "başarılı" Küme özelleştirme işlemi tamamlandı varsayılarak çalışır duruma ulaştığında tooa durumu yol açar. Toobe doğru şekilde hello olgu bildirim istiyorsanız, o küme özelleştirme temelde eksik dosya nedeniyle beklendiği gibi başarılı olmadı, daha uygun toothrow bir işlemdir ve hello küme özelleştirme adımı başarısız. tooachieve Bu örnek kod parçacığını bunun yerine aşağıdaki hello kullanmanız gerekir.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Betik eylemi dağıtma denetim listesi
Biz toodeploy bu komut dosyalarını hazırlanırken sürdü hello adımlar şunlardır:

1. Merhaba, dağıtım sırasında hello küme düğümleri tarafından erişilebilen bir yerde özel komut dosyaları içeren hello dosyaları yerleştirin. Bu hello varsayılan veya Küme dağıtımı ya da başka bir genel olarak erişilebilir depolama kapsayıcısı hello sırasında belirtilen ek depolama hesapları olabilir.
2. Komut dosyaları toomake idempotently, yürütme emin içine denetimleri ekleyebilirsiniz, böylece Hello betik hello üzerinde birden çok kez çalıştırılabilir aynı düğüm.
3. Kullanım hello **Write-Output** STDERR yanı sıra Azure PowerShell cmdlet tooprint tooSTDOUT. Kullanmayın **Write-Host**.
4. $Env gibi bir geçici dosya klasörünü kullanabilirsiniz: TEMP tookeep hello hello komut dosyaları tarafından kullanılan indirilen dosya ve komut dosyaları çalıştırdıktan sonra sonra bunları Temizle.
5. Özel yazılım D:\ veya C:\apps yalnızca yükleyin. Ayrılmış olarak hello C: sürücüsündeki başka konumlarda kullanılmamalıdır. Merhaba C:\apps klasörü dışında hello C: sürücüsündeki dosyaları yükleme kurulum hataları sırasında hello düğümünün reimages neden olabileceğini unutmayın.
6. Böylece hello ortam değişkenleri hello komut dosyalarında ayarlama gibi herhangi bir işletim sistemi düzeyinde ayarlarını seçebilirsiniz, işletim sistemi düzeyinde ayarları veya Hadoop hizmeti yapılandırma dosyaları değiştirilmiş hello olayda toorestart Hdınsight Hizmetleri isteyebilirsiniz.

## <a name="debug-custom-scripts"></a>Özel komut dosyaları hata ayıklama
Merhaba komut dosyası hata günlüklerini diğer çıktısında hello küme oluşturma sırasında belirtilen hello varsayılan depolama hesabı ile birlikte saklanır. Merhaba günlükleri hello adı olan bir tabloda depolanır *u < \cluster-name-fragment >< \time-stamp > setuplog*. Tüm düğümlerinin üzerinde hangi hello hello kümede komut dosyasını çalıştırır hello (baş düğüm ve çalışan düğümleri) kayıtları toplanmış günlükleri şunlardır.
Toocheck hello günlükleri olan toouse kolay bir yolu, Visual Studio için Hdınsight araçları. Merhaba araçları yüklemek için bkz: [Visual Studio Hadoop araçlarını için Hdınsight kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**Visual Studio kullanarak toocheck hello günlük**

1. Visual Studio'yu açın.
2. Tıklatın **Görünüm**ve ardından **Sunucu Gezgini**.
3. "Azure" sağ tıklayın, çok Bağlan**Microsoft Azure abonelikleri**ve ardından kimlik bilgilerinizi girin.
4. Genişletme **depolama**, hello varsayılan dosya sistemi olarak kullanılan hello Azure depolama hesabı genişletin, **tabloları**ve hello tablo adına çift tıklayın.

Merhaba küme düğümleri toosee yapabilecekleriniz Ayrıca uzak STDOUT ve STDERR özel komut dosyaları için. Merhaba günlükleri her düğümde belirli yalnızca toothat düğümü ve oturum açtığınız **C:\HDInsightLogs\DeploymentAgent.log**. Bu günlük dosyaları hello özel komut dosyasından tüm çıkış kaydedin. Spark betik eylemi için bir örnek günlük parçacığı şöyle görünür:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


Bu günlük, Temizle hello Spark betik eylemi hello HEADNODE0 adlı VM üzerinde yürütüldüğü ve hiçbir özel hello yürütme sırasında durum oluştu.

Bir yürütme hatası oluşursa hello olayda, onu açıklayan hello çıkış de bu günlük dosyasında yer alır. Bu günlükler sağlanan hello bilgilerin kaynaklanabilecek betik sorunları hata ayıklamaya yardımcı olması gerekir.

## <a name="see-also"></a>Ayrıca bkz.
* [Betik eylemi kullanarak Hdınsight kümelerini özelleştirme][hdinsight-cluster-customize]
* [Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]
* [Yükleme ve Hdınsight kümelerinde R kullanma][hdinsight-r-scripts]
* [Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install.md).
* [Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
