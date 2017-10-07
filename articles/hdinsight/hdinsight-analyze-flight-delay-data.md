---
title: "hdınsight'ta - Azure Hadoop ile aaaAnalyze uçuş gecikme veri | Microsoft Docs"
description: "Merhaba kümesini silmek ve Sqoop iş Hive işini çalıştır toouse bir Windows PowerShell komut dosyası toocreate bir Hdınsight kümesi çalışma şeklini öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme
Hive sağlar Hadoop MapReduce işleri adlı bir SQL benzeri komut dosyası dili ile çalışan bir  *[HiveQL][hadoop-hiveql]*, hangi uygulanabilir özetlemeye doğrultusunda, sorgulama, ve büyük miktarda veriyi analiz etme.

> [!IMPORTANT]
> Merhaba bu belgedeki adımlar Windows tabanlı Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Linux tabanlı bir küme ile çalışma adımları için bkz: [(Linux) hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümlemek](hdinsight-analyze-flight-delay-data-linux.md).

Merhaba önemli yararlarından biri Azure Hdınsight hello veri depolama ve işlem ayrılmasıdır. Hdınsight Azure Blob Depolama, veri depolaması için kullanır. Tipik bir işi üç bölümden oluşur:

1. **Verileri Azure Blob Depolama alanında depolar.**  Örneğin, verileri, algılayıcı verilerini, web günlükleri hava durumu ve bu durumda, uçuş gecikme verileri Azure Blob depolama alanına kaydedilir.
2. **İşlerini çalıştırın.** Zaman tooprocess hello veriler olduğunda, bir Windows PowerShell komut dosyası (veya bir istemci uygulaması) çalıştırmak toocreate bir Hdınsight kümesi işleri çalıştırma ve hello küme silin. Çıktı veri tooAzure Blob Depolama kaydetme Hello işler. hatta hello kümesi silindikten sonra hello çıktı verileri korunur. Bu şekilde, yalnızca ne, tüketilen için ücret ödersiniz.
3. **Azure Blob depolama alanından Hello çıkış almak**, veya Bu öğreticide, hello veri tooan Azure SQL veritabanını dışa aktarın.

Merhaba Aşağıdaki diyagramda hello senaryo ve bu öğreticinin hello yapısı gösterilmektedir:

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

Merhaba diyagramı Hello numaraları toohello bölüm başlıkları karşılık unutmayın. **M** hello ana işlem için anlamına gelir. **A** hello ek hello içeriği anlamına gelir.

Merhaba ana bölümü hello öğreticinin nasıl toouse bir Windows PowerShell komut dosyası tooperform hello aşağıdaki görevleri gösterir:

* Hdınsight kümesi oluşturun.
* Bir Hive işi hello küme toocalculate ortalama gecikme üzerinde havaalanları çalıştırın. Merhaba uçuş gecikme veriler bir Azure Blob Depolama hesabında depolanır.
* Sqoop iş tooexport hello Hive işi çıkış tooan Azure SQL veritabanı çalıştırın.
* Merhaba Hdınsight kümesi silin.

Merhaba çok içinde uçuş gecikme veri yüklemek, Hive sorgu dizesi oluşturma/yükleme ve hello Azure SQL veritabanı için hello Sqoop işi hazırlama hello yönergelerini bulabilirsiniz.

> [!NOTE]
> Merhaba bu belgedeki belirli tooWindows tabanlı Hdınsight kümeleri adımlardır. Linux tabanlı bir küme ile çalışma adımları için bkz: [(Linux) hdınsight'ta Hive kullanarak uçuş gecikme verileri analiz](hdinsight-analyze-flight-delay-data-linux.md)

### <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure PowerShell içeren bir iş istasyonu**.

    > [!IMPORTANT]
    > Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır. Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.
    >
    > Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü. Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.

**Bu öğreticide kullanılan dosyaları**

Bu öğretici hello zamanında performans uçak uçuş verilerini kullanır [araştırma ve yenilikçi teknoloji yönetim, taşıma İstatistik Enstitüsü veya RITA][rita-website].
Veriler hello kopyasını tooan Azure Blob Depolama kapsayıcısını hello ortak Blob erişim iznine sahip karşıya yüklendi.
PowerShell Betiği parçası hello ortak blob kapsayıcısı toohello varsayılan blob kapsayıcısından kümenizin hello verileri kopyalar. Merhaba betiğidir de HiveQL kopyalanan toohello aynı Blob kapsayıcısı.
Toolearn istiyorsanız tooget/karşıya yükleme hello veri tooyour nasıl kendi depolama hesabı ve nasıl toocreate/karşıya yükleme hello HiveQL komut dosyası, bkz: [ek A](#appendix-a) ve [ek B](#appendix-b).

Merhaba aşağıdaki tabloda Bu öğreticide kullanılan hello dosyaları listeler:

<table border="1">
<tr><th>Dosyalar</th><th>Açıklama</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>Merhaba HiveQL komut dosyası tarafından hello Hive işi kullanılır. Bu komut dosyasını karşıya yüklenen tooan hello genel erişim ile Azure Blob Depolama hesabı olmuştur. <a href="#appendix-b">Ek B</a> hazırlama ve bu dosyayı tooyour kendi Azure Blob Depolama hesabı karşıya yükleme hakkında yönergeler vardır.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Merhaba Hive işi için giriş verileri. Merhaba verileri karşıya yüklenen tooan hello genel erişim ile Azure Blob Depolama hesabı olmuştur. <a href="#appendix-a">Ek A</a> hello verileri almak ve hello veri tooyour kendi Azure Blob Depolama hesabı karşıya yükleme yönergeleri açmıştır.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>Merhaba Hive işi Hello çıkış yolu. Merhaba varsayılan kapsayıcı hello çıktı verilerini depolamak için kullanılır.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>Merhaba Hive işi durumu klasör hello varsayılan kapsayıcı.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Küme oluşturma ve Hive/Sqoop işleri çalıştırma
Hadoop MapReduce toplu işlemesidir. Merhaba en uygun maliyetli şekilde toorun Hive işi toocreate hello işi için bir kümedir ve hello iş tamamlandıktan sonra hello işi silin. Merhaba aşağıdaki betiği hello tüm işlem kapsar.
Hdınsight kümesi oluşturma ve Hive işleri çalıştırma hakkında daha fazla bilgi için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri] [ hdinsight-provision] ve [Hdınsight ile Hive kullanma] [hdinsight-use-hive].

**Azure PowerShell toorun hello Hive sorguları**

1. Merhaba yönergeleri kullanarak hello Sqoop iş çıktısı için bir Azure SQL veritabanı ve hello tablo oluşturma [ek C](#appendix-c).
2. Windows PowerShell ISE açın ve komut dosyası izleyen hello çalıştırın:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. Tooyour SQL veritabanına bağlanmak ve hello AvgDelays tablo şehirde ortalama uçuş gecikmelerinden bakın:

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Ek A - karşıya yükleme uçuş gecikme veri tooAzure Blob Depolama
Merhaba veri dosyası ve hello HiveQL komut dosyaları karşıya yükleme (bkz [ek B](#appendix-b)) bazı planlama gerektirir. Merhaba toostore hello veri dosyaları ve Hdınsight kümesi oluşturma ve hello Hive işi çalıştırma önce hello HiveQL dosya olur. İki seçeneğiniz vardır:

* **Kullanım hello aynı hello Hdınsight küme tarafından hello varsayılan dosya sistemi olarak kullanılacak Azure depolama hesabı.** Merhaba Hdınsight kümesi hello depolama hesabının erişim anahtarı olacağı için ek değişiklikler toomake gerekmez.
* **Merhaba Hdınsight küme varsayılan dosya sistemi farklı bir Azure Storage hesabını kullanın.** Merhaba Durum buysa, hello oluşturma hello Windows PowerShell komut dosyası bulundu parçası değiştirmelisiniz [oluşturma Hdınsight kümesi ve çalışma Hive/Sqoop işleri](#runjob) toolink hello ek depolama alanı hesabı olarak depolama hesabı. Yönergeler için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri][hdinsight-provision]. Merhaba Hdınsight kümesi sonra hello hello depolama hesabı için erişim anahtarı bilir.

> [!NOTE]
> Merhaba Blob Depolama yolu hello veri dosyası için sabit kodlanmış içinde hello HiveQL komut dosyasıdır. Buna uygun şekilde güncelleştirmeniz gerekir.

**toodownload hello uçuş veri**

1. Çok Gözat[araştırma ve yenilikçi teknoloji yönetim, taşıma İstatistik Enstitüsü][rita-website].
2. Başlangıç sayfasında, aşağıdaki değerleri hello seçin:

    <table border="1">
    <tr><th>Ad</th><th>Değer</th></tr>
    <tr><td>Filtre yıl</td><td>2013 </td></tr>
    <tr><td>Dönem filtre</td><td>Ocak</td></tr>
    <tr><td>Alanları</td><td>*Yıl*, *FlightDate*, *UniqueCarrier*, *taşıyıcı*, *FlightNum*, *OriginAirportID* , *Kaynak*, *OriginCityName*, *OriginState*, *DestAirportID*, *hedef* , *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*,  *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*,  *LateAircraftDelay* (diğer tüm alanlar Temizle)</td></tr>
    </table>
3.Tıklatın **karşıdan**.
4. Merhaba dosya toohello sıkıştırmasını **C:\Tutorials\FlightDelay\2013Data** klasör. Her dosya, bir CSV dosyası ve yaklaşık 60 GB boyutunda.
5. Merhaba toohello verilerini içeren hello ayın yeniden adlandırın. Örneğin, hello dosya hello Ocak verileri içeren adlandırılmış *January.csv*.
6. Adım 2 ve 5 toodownload bir dosyayı her hello için 12 ay 2013'te yineleyin. En az bir dosya toorun hello öğreticinin gerekir.

**tooupload hello uçuş gecikme veri tooAzure Blob Depolama**

1. Merhaba parametreleri hazırlayın:

    <table border="1">
    <tr><th>Değişken adı</th><th>Notlar</th></tr>
    <tr><td>$storageAccountName</td><td>Merhaba tooupload hello verilerin istediğiniz Azure depolama hesabı.</td></tr>
    <tr><td>$blobContainerName</td><td>Blob kapsayıcısı tooupload hello verilerin istediğiniz hello.</td></tr>
    </table>
2. Azure PowerShell ISE açın.
3. Komut dosyası hello betik bölmesine aşağıdaki hello yapıştırın:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Tuşuna **F5** toorun hello komut dosyası.

Lütfen hello dosyaları karşıya yükleme için farklı bir yöntem toouse seçerseniz, flightdelay/öğreticileri/veri hello dosya yolu olduğundan emin olun. Merhaba dosyalara erişmek için hello sözdizimi aşağıdaki gibidir:

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

Merhaba yolu öğreticileri/flightdelay/verilerini hello dosyaları karşıya yüklediğiniz sırada oluşturulan hello sanal klasörüdür. 12 dosyaları, her ay için bir tane olduğundan emin olun.

> [!NOTE]
> Merhaba Hive sorgusu tooread hello yeni konumdan güncelleştirmeniz gerekir.
>
> Merhaba kapsayıcı erişim izni toobe ortak yapılandırmak veya hello depolama hesabı toohello Hdınsight kümesine bağlayın. Aksi takdirde hello Hive sorgu dizesi mümkün tooaccess hello veri dosyalarını olmaz.

- - -

## <a id="appendix-b"></a>Ek B - oluşturun ve HiveQL betiğini yükleyin
Azure PowerShell kullanarak, birden çok HiveQL ifadelerini tek bir saat veya paket hello HiveQL deyimi bir komut dosyasına çalıştırabilirsiniz. Bu bölümde, nasıl toocreate HiveQL betiğini ve karşıya yükleme hello tooAzure Blob Depolama Azure PowerShell kullanarak komut dosyası gösterir. Hive Azure Blob depolamada depolanan hello HiveQL betikleri toobe gerektirir.

Merhaba HiveQL betiğini hello aşağıdakileri gerçekleştirir:

1. **Merhaba delays_raw tablo bırakma**, hello tablo zaten mevcut durumda.
2. **Merhaba delays_raw dış Hive tablosu oluşturmak** hello uçuş gecikme dosyalarıyla toohello Blob depolama konumuna işaret eden. Bu sorgu alanları tarafından sınırlandırılır belirtir "," ve "tarafından \n" satırları sonlandırılır. Alan değerleri virgül içerdiğinde Hive alan sınırlayıcı virgül ve alan değeri parçası olan bir tane arasında ayrım çünkü bu bir sorun oluşturur (kaynak için alan değerlerini hello durumda olduğu\_ŞEHİR\_adı ve hedef\_ ŞEHİR\_adı). tooaddress Bu, hello sorgu sütunlara yanlış bölme toohold veri TEMP sütunları oluşturur.
3. **Başlangıç gecikmeleri tablo bırakma**, hello tablo zaten mevcut durumda.
4. **Merhaba gecikmeler tablosu oluşturma**. Merhaba verileri yararlı tooclean başka bir işleme önce yoktur. Bu sorgu yeni bir tablo oluşturur *gecikmeler*, hello delays_raw tablosundan. (Daha önce belirtildiği gibi) hello TEMP sütunları kopyalanmadı Not ve o hello **substring** kullanılan tooremove tırnak işaretleri hello verilerden işlevdir.
5. **Merhaba ortalama hava durumu gecikme ve grupları hello sonuçları Şehir ada göre işlem.** Ayrıca hello sonuçları tooBlob depolama çıktı. Hello sorgulayan kesme hello verilerden kaldıracak ve burada hello değeri için satır dışladığı Not **weather_delay** null. Daha sonra Bu öğreticide kullanılan Sqoop, bu değerler varsayılan olarak işleyebilmesini değil çünkü bu gereklidir.

Merhaba HiveQL komutları tam bir listesi için bkz: [Hive veri tanımlama dili][hadoop-hiveql]. Noktalı virgül Sonlandır her HiveQL komutu gerekir.

**toocreate HiveQL komut dosyası**

1. Merhaba parametreleri hazırlayın:

    <table border="1">
    <tr><th>Değişken adı</th><th>Notlar</th></tr>
    <tr><td>$storageAccountName</td><td>Merhaba tooupload hello HiveQL betiğini istediğiniz Azure depolama hesabı.</td></tr>
    <tr><td>$blobContainerName</td><td>Blob kapsayıcısı tooupload hello HiveQL betiğini istediğiniz hello.</td></tr>
    </table>
2. Azure PowerShell ISE açın.
3. Kopyalama ve yapıştırma hello betik bölmesine komut dosyası izleyen hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Merhaba komut dosyasında kullanılan hello değişkenleri şunlardır:

   * **$hqlLocalFileName** -hello betik kaydeder hello HiveQL komut dosyası yerel olarak yüklemeden önce tooBlob depolama. Merhaba dosya adı değil. Merhaba varsayılan değer <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** -hello Azure Blob Depolama kullanılan hello HiveQL komut dosyası blob adı budur. tutorials/flightdelay/flightdelays.hql Hello varsayılan değerdir. Merhaba dosyasını doğrudan tooAzure Blob depolama alanına yazılır, var olmadığından bir "/" Merhaba başında hello blob adı. Blob depolama biriminden tooaccess hello dosyanın istiyorsanız, tooadd gerekir bir "/" Merhaba başında hello dosya adı.
   * **$srcDataFolder** ve **$dstDataFolder** -"flightdelay/öğreticileri/data" = "flightdelay/öğreticileri/çıktı" =

- - -
## <a id="appendix-c"></a>Ek C - hello Sqoop iş çıktısı için bir Azure SQL veritabanı hazırlama
**tooprepare hello SQL veritabanı (Merhaba Sqoop betik ile Birleştir)**

1. Merhaba parametreleri hazırlayın:

    <table border="1">
    <tr><th>Değişken adı</th><th>Notlar</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>hello Azure SQL veritabanı sunucusunun adını Hello. Hiçbir şey girin toocreate yeni bir sunucu.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>hello Azure SQL veritabanı sunucusu için Hello oturum açma adı. $SqlDatabaseServerName var olan bir sunucu varsa hello oturum açma ve oturum açma parolası hello sunucusuyla kullanılan tooauthenticate edilir. Aksi takdirde kullanılan toocreate yeni bir sunucu oldukları.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>hello Azure SQL veritabanı sunucusuna Hello oturum açma parolası.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Yalnızca yeni bir Azure veritabanı sunucusu oluştururken bu değeri kullanılır.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>Merhaba SQL veritabanı toocreate hello AvgDelays tablo hello Sqoop işi için kullanılır. Boş bırakarak HDISqoop adlı bir veritabanı oluşturur. Merhaba tablo hello Sqoop iş çıktısı AvgDelays adıdır. </td></tr>
    </table>
2. Azure PowerShell ISE açın.
3. Kopyalama ve yapıştırma hello betik bölmesine komut dosyası izleyen hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Merhaba komut dosyası kullanan bir temsili durum aktarımı (REST) hizmeti, http://bot.whatismyipaddress.com, tooretrieve dış IP adresi. Başlangıç IP adresi, SQL veritabanı sunucunuz için bir güvenlik duvarı kuralı oluşturmak için kullanılır.

    Merhaba komut dosyasında kullanılan bazı değişkenler şunlardır:

   * **$ipAddressRestService** -hello varsayılan değerdir http://bot.whatismyipaddress.com. Bir ortak IP adresi, dış IP adresi almak için REST hizmeti değil. İsterseniz diğer hizmetler kullanabilirsiniz. (bir Windows PowerShell komut dosyası kullanarak) istasyonunuzdan hello veritabanı erişebilmeniz hello hizmeti aracılığıyla alınan hello dış IP adresi kullanılan toocreate Azure SQL veritabanı sunucunuz için bir güvenlik duvarı kuralı olacaktır.
   * **$fireWallRuleName** -bu hello hello güvenlik duvarı kuralı hello Azure SQL veritabanı sunucusunun adıdır. Merhaba varsayılan ad <u>FlightDelay</u>. İstiyorsanız, onu yeniden adlandırabilirsiniz.
   * **$sqlDatabaseMaxSizeGB** -yalnızca yeni bir Azure SQL veritabanı sunucusu oluştururken bu değer kullanılır. Merhaba varsayılan değer 10 GB'tır. Bu öğretici için 10GB yeterlidir.
   * **$sqlDatabaseName** -yalnızca yeni bir Azure SQL veritabanı oluştururken bu değer kullanılır. HDISqoop Hello varsayılan değerdir. Adlandırırsanız, hello Sqoop Windows PowerShell Betiği uygun şekilde güncelleştirmeniz gerekir.
4. Tuşuna **F5** toorun hello komut dosyası.
5. Merhaba komut dosyası çıkışını doğrulayın. Merhaba komut dosyası başarıyla çalıştırıldığını doğrulayın.

## <a id="nextsteps"></a> Sonraki adımlar
Anladığınızdan artık nasıl tooupload dosya tooAzure Blob storage, toopopulate bir Hive tablosu nasıl hello verileri Azure Blob depolama biriminden kullanarak nasıl toorun Hive sorguları ve nasıl toouse HDFS tooan Azure SQL veritabanından Sqoop tooexport veri. toolearn daha makaleler hello bakın:

* [Hdınsight kullanmaya başlama][hdinsight-get-started]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [Oozie Hdınsight ile kullanma][hdinsight-use-oozie]
* [Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
