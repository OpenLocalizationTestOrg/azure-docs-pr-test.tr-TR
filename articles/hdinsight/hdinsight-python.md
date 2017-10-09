---
title: "Apache Hive veya Pig - Azure Hdınsight ile UDF aaaPython | Microsoft Docs"
description: "Azure üzerinde toouse Python kullanıcı tanımlı işlevler (UDF) Hive ve hdınsight'ta Hadoop teknoloji hello Pig yığın nasıl öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Hdınsight'ta kullanım Python kullanıcı tanımlı işlevler (UDF) Hive veya Pig ile

Bilgi nasıl toouse Python kullanıcı tanımlı işlevler (UDF) Apache Hive veya Pig içinde Azure hdınsight'ta Hadoop ile.

## <a name="python"></a>Hdınsight üzerinde Python

Python2.7 Hdınsight 3.0 ve sonraki sürümlerinde varsayılan olarak yüklenir. Apache Hive Python bu sürümü ile akış işleme için kullanılabilir. Akış işleme Hive ve hello UDF arasında STDOUT ve STDIN toopass verileri kullanır.

Hdınsight, ayrıca Java'da yazılmış bir Python uygulaması Jython içerir. Jython doğrudan hello Java sanal makinesi'üzerinde çalışır ve akış kullanmaz. Jython hello Python yorumlayıcı Python ile Pig kullanırken önerilen ' dir.

> [!WARNING]
> Bu belgedeki Hello adımlar varsayımlar aşağıdaki hello olun: 
>
> * Merhaba yerel geliştirme ortamınızı Python komut dosyaları oluşturun.
> * Merhaba betikleri tooHDInsight ya da hello kullanarak karşıya `scp` yerel Bash oturumu veya PowerShell komut dosyası sağlanan hello komutu.
>
> Toouse hello istiyorsanız [Azure bulut Kabuğu (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) gerekir sonra Hdınsight ile toowork önizleme:
>
> * Merhaba bulut Kabuk ortamı içindeki Hello betikleri oluşturun.
> * Kullanım `scp` tooupload hello hello dosyalarından Kabuk tooHDInsight bulut.
> * Kullanım `ssh` hello bulut Kabuk tooconnect tooHDInsight ve çalışma hello örnekleri.

## <a name="hivepython"></a>UDF yığını

Python olarak kullanılabilir bir UDF Hive gelen HiveQL hello `TRANSFORM` deyimi. Örneğin, aşağıdaki HiveQL hello hello çağırır `hiveudf.py` hello kümesi için hello varsayılan Azure depolama hesabına depolanan dosya.

**Linux tabanlı Hdınsight**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**Windows tabanlı Hdınsight**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> Windows tabanlı Hdınsight kümelerinde hello `USING` yan tümcesi hello tam yolu toopython.exe belirtmeniz gerekir.

Bu örnek yaptığı aşağıda verilmiştir:

1. Merhaba `add file` hello dosya hello başında deyiminin ekler hello `hiveudf.py` dosya toohello hello kümedeki tüm düğümler tarafından erişilebilir olması için önbellek, dağıtılmış.
2. Merhaba `SELECT TRANSFORM ... USING` deyimi hello veri seçer `hivesampletable`. Merhaba ClientID, devicemake ve devicemodel değerleri toohello de geçirir `hiveudf.py` komut dosyası.
3. Merhaba `AS` yan tümcesi açıklar döndürülen hello alanları `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Merhaba hiveudf.py dosyası oluşturma


Geliştirme ortamınızı adlı bir metin dosyası oluşturun `hiveudf.py`. Merhaba dosyasının Merhaba içeriğine koddan hello kullan:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Bu komut dosyası hello aşağıdaki eylemleri gerçekleştirir:

1. Veri satırı STDIN okuyun.
2. Yeni satır karakteri sondaki hello kullanarak kaldırılır `string.strip(line, "\n ")`.
3. Akış işleme yaparken, tek bir satırı her değer arasında bir sekme karakteri ile tüm hello değerlerini içerir. Bu nedenle `string.split(line, "\t")` giriş yalnızca hello alanları dönmeden her sekmesi sırasında kullanılan toosplit hello olabilir.
4. İşlem tamamlandığında, hello çıktı sekmesi her alanı arasında tek bir satır olarak tooSTDOUT yazılmış olmalıdır. Örneğin, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Merhaba `while` döngü Hayır kadar yinelenir `line` okunur.

Merhaba komut çıktısı şöyledir hello giriş değerleri için bir birleşimini `devicemake` ve `devicemodel`, ve hello karmasını birleştirilmiş değer.

Bkz: [hello örnekleri çalıştırma](#running) nasıl toorun Hdınsight kümenizdeki Bu örnek.

## <a name="pigpython"></a>Pig UDF

Bir Python komut dosyası olarak bir UDF Pig gelen hello kullanılabilir `GENERATE` deyimi. Jython veya C Python kullanarak hello komut dosyası çalıştırabilirsiniz.

* Jython JVM hello üzerinde çalışır ve yerel olarak Pig çağrılabilir.
* C Python bir dış işlem olduğundan, Pig Hello verileri hello üzerinde bir Python işlemde çalışan toohello betik çıkışı JVM gönderilir. Merhaba hello Python komut dosyası çıkışını Pig'ya geri gönderilir.

toospecify hello Python Yorumlayıcı, kullanım `register` hello Python betiği başvururken. Merhaba Aşağıdaki örnekler komut dosyaları ile Pig kaydetmeye `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Jython kullanırken hello yol toohello pig_jython dosya yerel bir yol ya da bir WASB olabilir: / / yolu. Ancak, C Python kullanırken, bir dosya toosubmit hello Pig işi kullandığınız hello düğümünün hello yerel dosya sisteminde başvurmalıdır.

Kaydı, bu örnek için Pig Latin hello olduğunda aynı her ikisi için hello:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Bu örnek yaptığı aşağıda verilmiştir:

1. Merhaba ilk satırı yükler hello örnek veri dosyası, `sample.log` içine `LOGS`. Ayrıca her kayıt olarak tanımlayan bir `chararray`.
2. hello işleminin hello sonucu depolamak herhangi bir null değeri filtreleyen Hello sonraki satıra `LOG`.
3. Ardından, hello kayıtlarında üzerinden tekrarlanan `LOG` ve kullandığı `GENERATE` tooinvoke hello `create_structure` hello Python/Jython komut dosyasında yer alan yöntemi yüklü olarak `myfuncs`. `LINE`kullanılan toopass hello geçerli kayıt toohello işlevdir.
4. Son olarak, hello çıkışları hello kullanarak Dökümü alınan tooSTDOUT olan `DUMP` komutu. Merhaba işlemi tamamlandıktan sonra bu komut hello sonuçları görüntüler.

### <a name="create-hello-pigudfpy-file"></a>Merhaba pigudf.py dosyası oluşturma

Geliştirme ortamınızı adlı bir metin dosyası oluşturun `pigudf.py`. Merhaba dosyasının Merhaba içeriğine koddan hello kullan:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

Merhaba Pig Latin örnekte biz hello tanımlanan `LINE` hello girişi için tutarlı bir şemayı olduğundan chararray girin. Merhaba Python betiği hello veri çıkışı için tutarlı bir şema dönüştürür.

1. Merhaba `@outputSchema` deyimi tooPig döndürülen hello verilerin hello biçimini tanımlar. Bu durumda olan bir **veri paketi**, Pig veri türü. Merhaba paketi chararray (dize) tümü alanları izleyen hello içerir:

   * -Başlangıç tarihi hello günlük girişinin oluşturulduğu tarih
   * saati - hello günlük girişinin oluşturulduğu hello
   * ClassName - için hello sınıf adı hello girdisi oluşturuldu
   * Level - hello günlük düzeyi
   * Ayrıntı - verbose ayrıntılarını hello günlüğü girişi

2. Ardından, hello `def create_structure(input)` Pig çizgi öğelerine geçirir hello işlevi tanımlar.

3. Merhaba örnek veri `sample.log`, çoğunlukla toohello tarih, saat, classname düzeyi, uyumlu ve ayrıntı şema tooreturn istiyoruz. Ancak, ile başlayan birkaç satırları içeren `*java.lang.Exception*`. Bu satırlar değiştirilmiş toomatch hello şema olmalıdır. Merhaba `if` deyimi için olanlar denetler ve ardından massages hello giriş verisi toomove hello `*java.lang.Exception*` hello veri satır içi bizim beklenen çıkış şemasıyla getiren dize toohello son.

4. Ardından, hello `split` hello ilk dört boşluk karakterleri kullanılan toosplit hello veri komuttur. Merhaba çıkış içine atandığı `date`, `time`, `classname`, `level`, ve `detail`.

5. Son olarak, hello değerleri tooPig döndürülür.

Merhaba veri tooPig döndürüldüğünde, onu tutarlı bir şemayı hello tanımlanan sahip `@outputSchema` deyimi.

## <a name="running"></a>Karşıya yükleme ve başlangıç örnekleri çalıştırın

> [!IMPORTANT]
> Merhaba **SSH** adımlar, yalnızca Linux tabanlı Hdınsight kümesi ile çalışır. Merhaba **PowerShell** adımları bir Linux veya Windows tabanlı Hdınsight kümesi ile çalışır, ancak bir Windows istemci gerektirir.

### <a name="ssh"></a>SSH

SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Kullanım `scp` toocopy hello dosyaları tooyour Hdınsight kümesi. Örneğin, kopya hello adlı dosyaları tooa küme komutu aşağıdaki hello **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. SSH tooconnect toohello küme kullanın.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Merhaba SSH oturumundan hello python dosyaları toohello WASB depolama hello küme için daha önce karşıya ekleyin.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Merhaba dosyalarını karşıya yükledikten sonra toorun hello Hive ve Pig işleri kullanım hello aşağıdaki adımları.

#### <a name="use-hello-hive-udf"></a>Merhaba Hive UDF kullanın

1. Kullanım hello `hive` toostart hello hive kabuğunu komutu. Görmeniz gerekir bir `hive>` hello Kabuk yüklendikten sonra ister.

2. Merhaba sorgusu aşağıdaki hello girin `hive>` istemi:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Merhaba son satırı girdikten sonra hello iş başlamanız gerekir. Merhaba işi tamamlandıktan sonra aşağıdaki örnek çıkış benzer toohello döndürür:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Merhaba Pig UDF kullanın

1. Kullanım hello `pig` toostart hello Kabuk komutu. Gördüğünüz bir `grunt>` hello Kabuk yüklendikten sonra ister.

2. Merhaba deyimlerini aşağıdaki hello girin `grunt>` istemi:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Satır aşağıdaki hello girdikten sonra hello iş başlamanız gerekir. Merhaba işi tamamlandığında, çıkış benzer toohello veri aşağıdaki döndürür:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Kullanmak `quit` tooexit Grunt Kabuk hello ve aşağıdaki tooedit hello pigudf.py dosyasına hello yerel dosya sisteminde hello kullanın:

    ```bash
    nano pigudf.py
    ```

5. Bir kez hello Düzenleyicisi'nde hello kaldırarak satır aşağıdaki hello açıklamadan çıkarın `#` hello satırının hello başından karakteri:

    ```bash
    #from pig_util import outputSchema
    ```

    Merhaba değişiklik yapıldıktan sonra Ctrl + X tooexit hello Düzenleyicisi'ni kullanın. Y seçin ve ardından toosave hello değişiklikleri girin.

6. Kullanım hello `pig` toostart hello Kabuğu komutunu yeniden. Hello olduğunuzda `grunt>` isteminde, hello C Python yorumlayıcı kullanılarak toorun hello Python komut aşağıdaki hello kullanın.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Bu iş tamamlandığında, ne zaman, daha önce Jython kullanılarak hello komut çalıştırıldığı aynı çıktı hello görmeniz gerekir.

### <a name="powershell-upload-hello-files"></a>PowerShell: Karşıya yükleme hello dosyaları

PowerShell tooupload hello dosyaları toohello Hdınsight sunucusuna kullanabilirsiniz. Aşağıdaki komut dosyası tooupload hello Python dosyaları hello kullan:

> [!IMPORTANT] 
> Bu bölümdeki adımları Hello Azure PowerShell kullanın. Azure PowerShell kullanma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Değişiklik hello `C:\path\to` toohello yolu toohello geliştirme ortamınızı dosyalarda değeri.

Bu betiği Hdınsight kümenizle ilgili bilgileri alır ve ardından hello hesabı ve anahtarı hello varsayılan depolama hesabı için ayıklar ve karşıya dosya toohello kök hello kapsayıcısının hello.

> [!NOTE]
> Dosyaları karşıya yükleme ile ilgili daha fazla bilgi için bkz: hello [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md) belge.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: hello Hive UDF kullanın

PowerShell çalıştırma kullanılan tooremotely Hive sorguları da olabilir. PowerShell komut dosyası toorun kullanan bir Hive sorgusu aşağıdaki kullanım hello **hiveudf.py** komut dosyası:

> [!IMPORTANT]
> Çalıştırmadan önce hello betik hello Hdınsight kümeniz için HTTPs/Admin hesap bilgilerini ister.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Merhaba hello için çıktı **Hive** işi aşağıdaki örneğine benzer toohello görünmelidir:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell kullanılan toorun Pig Latin işleri de olabilir. toorun hello kullanan bir Pig Latin iş **pigudf.py** komut dosyası, PowerShell Betiği aşağıdaki hello kullanın:

> [!NOTE]
> PowerShell kullanarak işi uzaktan gönderirken, olası toouse C Python hello yorumlayıcı değil.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Merhaba hello için çıktı **Pig** işi veri aşağıdaki benzer toohello görünmelidir:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Sorun giderme

### <a name="errors-when-running-jobs"></a>İşlerini çalışırken hataları

Merhaba hive işi çalıştırırken metnini izleyen bir hata benzer toohello karşılaşabilirsiniz:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Bu sorunun nedeni hello satır sonları hello Python dosyasında. Çok sayıda Windows düzenleyicileri toousing CRLF varsayılan bitiş hello çizgi ancak Linux uygulamalar genellikle LF bekler.

Merhaba dosya tooHDInsight karşıya yüklemeden önce aşağıdaki PowerShell deyimleri tooremove hello CR karakterleri hello kullanabilirsiniz:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>PowerShell komut dosyaları

Merhaba örnek PowerShell komut dosyalarını toorun hello örneklerde kullanılan her ikisi de hello işi için hata çıktısını görüntüler açıklamalı bir satır içerir. Merhaba beklenen çıktı hello işi için görüyorsanız değil, hello aşağıdaki satır ve hello hata bilgileri bir sorun olduğunu gösteriyor varsa bkz açıklamadan çıkarın.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Ayrıca Hello hata bilgileri (STDERR) ve hello işi (STDOUT) hello sonucunu oturum tooyour Hdınsight depolama değildir.

| Bu iş için... | Bu dosyalar hello blob kapsayıcısında bakın |
| --- | --- |
| Hive |/ HivePython/stderr<p>/ HivePython/stdout |
| Pig |/ PigPython/stderr<p>/ PigPython/stdout |

## <a name="next"></a>Sonraki adımlar

Varsayılan olarak sağlanmayan tooload Python modülleri gerekirse bkz [nasıl toodeploy modülü tooAzure Hdınsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Diğer yolları toouse Pig, Hive ve MapReduce kullanma hakkında toolearn için belgeler aşağıdaki hello bakın:

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)
