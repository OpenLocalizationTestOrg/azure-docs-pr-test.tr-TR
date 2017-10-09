---
title: "Apache Sqoop aaaRun işleri Azure Hdınsight (Hadoop) ile | Microsoft Docs"
description: "Nasıl toouse Azure PowerShell bir iş istasyonu toorun Sqoop gelen içe ve dışa aktarma Hadoop kümesi ve bir Azure SQL veritabanı arasında bilgi edinin."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Hdınsight'ta Hadoop ile Sqoop kullanma
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Bilgi nasıl toouse Sqoop Hdınsight tooimport ve Hdınsight kümesi ve Azure SQL database veya SQL Server veritabanı arasında verme.

Hadoop günlükleri ve dosyaları gibi yapılandırılmamış ve yarı yapılandırılmış veri işleme için doğal bir seçim olsa da olabilir ilişkisel veritabanlarında depolanan bir gereksinim tooprocess yapılandırılmış veri.

[Sqoop] [ sqoop-user-guide-1.4.4] tasarlanmış aracı tootransfer Hadoop kümeleri ve ilişkisel veritabanları arasında verilerdir. SQL Server, MySQL veya Oracle hello Hadoop dağıtılmış dosya sistemi (HDFS) içine dönüştürme hello verileri Hadoop ile MapReduce veya Hive ve uygulamasına geri hello verileri dışarı aktarma gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) tooimport verilerden kullanabilirsiniz bir RDBMS. Bu öğreticide, ilişkisel veritabanı için SQL Server veritabanını kullanıyorsunuz.

Hdınsight kümelerinde desteklenir Sqoop sürümleri için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler nelerdir?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Merhaba senaryo anlama

Hdınsight kümesi bazı örnek verilerle birlikte gelir. Aşağıdaki iki örnek hello kullan:

* Konumda bulunan bir log4j günlük dosyası */example/data/sample.log*. günlükleri aşağıdaki hello hello dosyasından ayıklanan:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Adlı bir Hive tablosu *hivesampletable*, hangi başvuruları hello veri dosyası konumunda bulunan */hive/warehouse/hivesampletable*. Merhaba tablo bazı mobil cihaz verileri içerir. 
  
  | Alan | Veri türü |
  | --- | --- |
  | istemci kimliği |Dize |
  | querytime |Dize |
  | Pazar |Dize |
  | deviceplatform |Dize |
  | devicemake |Dize |
  | devicemodel |Dize |
  | durum |Dize |
  | Ülke |Dize |
  | querydwelltime |Çift |
  | SessionID |bigint |
  | sessionpagevieworder |bigint |

İlk olarak, verdiğiniz *sample.log* ve *hivesampletable* toohello Azure SQL veritabanı veya tooSQL sunucu ve içeri aktarma hello hello mobil cihaz verileri içeren bir tabloda geri tooHDInsight hello kullanarak Aşağıdaki yolu:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Küme ve SQL veritabanı oluşturma
Bu bölümde Azure portalı ve Azure Resource Manager şablonu nasıl toocreate bir küme, bir SQL veritabanı ve çalışan hello öğreticisi kullanma hello SQL veritabanı şemalarını hello gösterir. Merhaba şablonu bulunabilir [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). Merhaba Resource Manager şablonu bir bacpac paket toodeploy hello tablo şemalarını tooSQL veritabanı çağırır.  bir ortak blob kapsayıcısında, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac bulunan Hello bacpac paket. Merhaba bacpac dosyaları için özel bir kapsayıcı toouse istiyorsanız, değerleri hello şablonda aşağıdaki hello kullanın:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Toouse Azure PowerShell toocreate hello küme ve hello SQL veritabanı tercih ederseniz, bkz. [ek A](#appendix-a---a-powershell-sample).

1. Görüntü tooopen hello Azure portalında bir Resource Manager şablonu aşağıdaki hello'ı tıklatın.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Aşağıdaki özelliklere hello girin:

    - **Abonelik**: Azure aboneliğiniz girin.
    - **Kaynak grubu**: yeni bir Azure kaynak grubu oluşturun veya varolan bir kaynak grubu seçin.  Bir kaynak grubu yönetim amaçla ' dir.  Nesneler için bir kapsayıcıdır.
    - **Konum**: bir bölge seçin.
    - **ClusterName**: Merhaba Hadoop kümesi için bir ad girin.
    - **Küme oturum açma adı ve parola**: hello varsayılan oturum açma adıdır, yönetici
    - **SSH kullanıcı adı ve parola**.
    - **SQL veritabanı sunucusu oturum açma adı ve parola**.
    - **_artifacts konumu**: kendi backpac dosyayı farklı bir konumda toouse istemediğiniz sürece hello varsayılan değeri kullanın.
    - **Konum Sas belirteci _artifacts**: boş bırakın.
    - **Bacpac dosya adı**: kendi backpac dosya toouse istemediğiniz sürece hello varsayılan değeri kullanın.
     
     değerleri aşağıdaki hello sabit kodlanmış hello değişkenler bölümünde şunlardır:
     
     | Varsayılan depolama hesabı adı | <CluterName>Depolama |
     | --- | --- |
     | Azure SQL veritabanı sunucusu adı |<ClusterName>dbserver |
     | Azure SQL veritabanı adı |<ClusterName>DB |
     
     Lütfen bu değerleri yazın.  Bunları daha sonra hello öğreticide gerekir.

3. tıklatın **Tamam** toosave hello parametreleri.

4 gelen hello **özel dağıtım** dikey penceresinde tıklatın **kaynak grubu** açılır kutusuna ve ardından **yeni** toocreate yeni bir kaynak grubu. Merhaba kaynak grubu hello küme, hello bağımlı depolama hesabı ve diğer bağlı kaynağı gruplandıran bir kapsayıcıdır.

5. **Yasal koşullar**’a ve ardından **Oluştur**’a tıklayın.

6. **Oluştur**’a tıklayın. Şablon dağıtımı için dağıtım gönderme başlıklı yeni bir kutucuk görürsünüz. Yaklaşık 20 dakika toocreate hello küme ve SQL veritabanı hakkında alır.

Toouse mevcut Azure SQL veritabanını veya Microsoft SQL Server'ı seçerseniz

* **Azure SQL veritabanı**: istasyonunuzdan hello Azure SQL veritabanı sunucusu tooallow erişimi için bir güvenlik duvarı kuralı yapılandırmanız gerekir. Bir Azure SQL veritabanı oluşturma ve hello güvenlik duvarını yapılandırma hakkında yönergeler için bkz: [Azure SQL veritabanını kullanmaya başlama][sqldatabase-get-started]. 
  
  > [!NOTE]
  > Varsayılan olarak Azure SQL veritabanını Azure Hdınsight gibi Azure hizmetlerden bağlantılara izin verir. Bu güvenlik duvarı ayarı devre dışıysa, tooenable gereken hello Azure portalı şuradan. Bir Azure SQL veritabanı oluşturma ve güvenlik duvarı kuralları yapılandırma hakkında daha fazla yönerge için bkz: [oluşturma ve yapılandırma SQL veritabanı][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: Hdınsight kümenize hello üzerinde ise, aynı sanal ağ Azure SQL sunucusu olarak, bu makale tooimport ve dışarı aktarma veri tooa SQL Server veritabanında hello adımları kullanabilirsiniz.
  
  > [!NOTE]
  > Hdınsight yalnızca konum tabanlı sanal ağları destekler ve benzeşim grubu tabanlı sanal ağlar ile şu anda çalışmıyor.
  > 
  > 
  
  * toocreate ve sanal ağ yapılandırma, bkz: [hello Azure portal kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * SQL Server, veri merkezinizde kullanırken, hello sanal ağ olarak yapılandırmalısınız *siteden siteye* veya *noktadan siteye*.
      
      > [!NOTE]
      > İçin **noktası site** sanal ağlar, SQL Server çalıştırmalıdır hello VPN istemcisi hello kullanılabilir yapılandırma uygulama **Pano** Azure sanal ağı yapılandırmanızın.
      > 
      > 
    * Bir Azure sanal makinede SQL Server kullanırken SQL Server barındırma hello sanal makine hello üyesi ise herhangi bir sanal ağ yapılandırması kullanılabilir Hdınsight aynı sanal ağ.
  * toocreate bir sanal ağ Hdınsight kümesinde bkz [özel seçenekleri kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server kimlik doğrulaması da izin vermelidir. Bir SQL Server oturum açma toocomplete hello bu makaledeki adımları kullanmanız gerekir.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Sqoop işleri çalıştırma
Hdınsight Sqoop işleri çeşitli yöntemler kullanarak çalıştırabilirsiniz. Hangi yöntemi sizin için uygun olan tablo toodecide aşağıdaki hello kullanın ve sonra kılavuz hello bağlantıyı izleyin.

| **Bu** isterseniz... | .. .an **etkileşimli** Kabuk | ... **toplu** işleme | .. hemen bu **küme işletim sistemi** | .. .from bu **istemci işletim sistemi** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, UNIX, Mac OS X veya Windows |
| [Hadoop için .NET SDK](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux veya Windows |Windows (için şimdi) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux veya Windows |Windows |

## <a name="limitations"></a>Sınırlamalar
* Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.
* -Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop gerçekleştirir hello INSERT işlemlerine toplu işleme yerine birden çok ekler.

## <a name="next-steps"></a>Sonraki adımlar
Öğrendiğiniz artık nasıl toouse Sqoop. toolearn daha bakın:

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile Oozie kullanma][hdinsight-use-oozie]: Oozie iş akışında kullanmak Sqoop eylem.
* [Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-data]: kullanmak Hive tooanalyze uçuş gecikme veri ve Sqoop tooexport veri tooan Azure SQL veritabanını kullanın.
* [Veri tooHDInsight karşıya][hdinsight-upload-data]: veri tooHDInsight/Azure Blob Depolama yüklemek için diğer yöntemler bulun.

## <a name="appendix-a---a-powershell-sample"></a>Ek A - PowerShell örnek
Merhaba PowerShell örnek hello aşağıdaki adımları gerçekleştirir:

1. TooAzure bağlanın.
2. Bir Azure kaynak grubu oluşturun. Daha fazla bilgi için bkz: [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md)
3. Bir Azure SQL veritabanı sunucusu, Azure SQL veritabanına ve iki tablo oluşturun. 
   
    Bunun yerine SQL Server kullanıyorsanız, aşağıdaki deyimleri toocreate hello tabloları hello kullanın:
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    Merhaba en kolay yolu tooexamine hello veritabanını ve tabloları toouse Visual Studio olur. Merhaba veritabanı sunucusu ve hello veritabanı hello Azure portal kullanarak incelenebilir.
4. Hdınsight kümesi oluşturun.
   
    tooexamine hello küme hello Azure portalında veya Azure PowerShell'i kullanabilirsiniz.
5. Merhaba kaynak veri dosyası önceden işleyebilir.
   
    Bu öğreticide, log4j günlük dosyası (ayrılmış bir dosya) ve bir Hive tablosu tooan Azure SQL veritabanı verin. Merhaba sınırlanmış dosya olarak adlandırılır */example/data/sample.log*. Öğreticide daha önce Merhaba, log4j günlükler bazı örnekler gördünüz. Merhaba günlük dosyasında bazı boş satırlar ve bazı satırlar benzer toothese vardır:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    Bu verileri kullanan diğer örnekler için ince budur ancak biz hello Azure SQL database veya SQL Server içeri aktarmadan önce bu özel durumlar kaldırmanız gerekir. Sqoop verme başarısız boş bir dize veya daha az sayıda satırıyla ise hello Azure SQL veritabanı tablosunda tanımlı alanları hello sayısından öğeleri. Merhaba log4jlogs Tablo 7 dize türü alan yok.
   
    Bu yordamı hello kümesinde yeni bir dosya oluşturur: tutorials/usesqoop/data/sample.log. tooexamine hello değiştirilmiş veri dosyası, hello Azure portal, Azure Storage Gezgini aracını veya Azure PowerShell kullanabilirsiniz. [Hdınsight kullanmaya başlama] [ hdinsight-get-started] hello dosya içeriği görüntülemek ve örnek Azure PowerShell toodownload bir dosyayı kullanmak için bir kod sahiptir.
6. Bir veri dosyası toohello Azure SQL veritabanına verin.
   
    Merhaba kaynak tutorials/usesqoop/data/sample.log dosyasıdır. Merhaba veri dışa aktarılan toois nerede hello tablo log4jlogs çağrılır.
   
   > [!NOTE]
   > Dışında bir bağlantı dizesi bilgisi, SQL Server veya bir Azure SQL veritabanı için bu bölümdeki hello adımları çalışması gerekir. Bu adımları yapılandırma aşağıdaki hello kullanarak test edilmiş:
   > 
   > * **Azure sanal ağı noktadan siteye Yapılandırması**: bir sanal ağa bağlı özel bir veri merkezinde hello Hdınsight küme tooa SQL Server. Bkz: [noktadan siteye VPN hello Yönetim Portalı yapılandırma](../vpn-gateway/vpn-gateway-point-to-site-create.md) daha fazla bilgi için.
   > * **Azure Hdınsight 3.1**: bkz [özel seçenekleri kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md) bir küme üzerinde bir sanal ağ oluşturma hakkında daha fazla bilgi için.
   > * **SQL Server 2014**: tooallow kimlik doğrulaması ve çalışan hello VPN istemci yapılandırma paketi tooconnect güvenli bir şekilde yapılandırılmış toohello sanal ağ.
   > 
   > 
7. Bir Hive tablosu toohello Azure SQL veritabanı dışarı aktarın.
8. Merhaba mobiledata tablo toohello Hdınsight kümesi içeri aktarın.
   
    tooexamine hello değiştirilmiş veri dosyası, hello Azure portal, Azure Storage Gezgini aracını veya Azure PowerShell kullanabilirsiniz.  [Hdınsight kullanmaya başlama] [ hdinsight-get-started] hello dosya içeriği görüntülemek ve Azure PowerShell toodownload bir dosyayı kullanma hakkında örnek koduna sahip.

### <a name="hello-powershell-sample"></a>Merhaba PowerShell örnek
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

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
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
