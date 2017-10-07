---
title: "aaaMigrate tooAzure kaynak yöneticisi için Hdınsight araçları | Microsoft Docs"
description: "Hdınsight kümeleri için nasıl toomigrate tooAzure Resource Manager geliştirme araçları"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Hdınsight kümeleri geçirme tooAzure Resource Manager tabanlı geliştirme araçları

Hdınsight, Hdınsight için Azure Service Manager ASM tabanlı araçlar kaldırmaktadır. Azure PowerShell, Azure CLI veya hello Hdınsight .NET SDK'sı toowork Hdınsight kümeleri ile kullanıyorsanız, Azure Resource Manager ARM tabanlı kullanmaları toouse hello sürümleri PowerShell'i, CLI ve .NET SDK'sı ileride. Bu makalede işaretçiler hakkında yönergeler sağlar. toomigrate toohello yeni ARM tabanlı yaklaşım. Uygun olduğunda, bu makalede hello ASM ve ARM yaklaşımlar Hdınsight için hello farklarını çıkışı da işaret eder.

> [!IMPORTANT]
> ASM Hello desteği PowerShell'i, CLI, temel ve .NET SDK'yı Durdur **1 Ocak 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Geçirme Azure CLI tooAzure Kaynak Yöneticisi
önceki bir yükleme Yükseltmekte olduğunuz sürece hello Azure CLI şimdi tooAzure Resource Manager (ARM) mod, varsayılan olarak; Bu durumda, toouse hello gerekebilir `azure config mode arm` komut tooswitch tooARM modu.

Merhaba temel komutları o hello toowork Azure Hizmet Yönetimi (ASM) kullanılarak Hdınsight ile sağlanan Azure CLI olan hello aynı ARM kullanırken; Ancak bazı parametreler ve anahtarları yeni adlara sahip ve çok sayıda yeni parametreler kullanılabilir ARM kullanırken yoktur. Örneğin, artık kullanabilirsiniz `azure hdinsight cluster create` toospecify hello Azure sanal bir küme içinde oluşturulmalıdır veya Hive ağ ve Oozie meta depo bilgileri.

Hdınsight ile Azure Resource Manager ile çalışmak için temel komutlar şunlardır:

* `azure hdinsight cluster create`-Yeni bir Hdınsight kümesi oluşturur
* `azure hdinsight cluster delete`-Mevcut bir Hdınsight kümesine siler
* `azure hdinsight cluster show`-Varolan bir kümeye hakkındaki bilgileri görüntüleme
* `azure hdinsight cluster list`-Azure aboneliğiniz için Hdınsight kümeleri listeler

Kullanım hello `-h` tooinspect hello parametreleri ve her komut için kullanılabilen anahtarlar geçin.

### <a name="new-commands"></a>Yeni komutları
Azure Resource Manager ile kullanılabilen yeni komutlar şunlardır:

* `azure hdinsight cluster resize`-değişiklikleri hello kümedeki çalışan düğümü sayısını dinamik olarak hello
* `azure hdinsight cluster enable-http-access`-HTTPs erişim toohello küme sağlar (üzerinde varsayılan olarak)
* `azure hdinsight cluster disable-http-access`-HTTPs erişim toohello küme devre dışı bırakır
* `azure hdinsight script-action`-oluşturma/betik eylemleri bir kümede yönetmek için komutlar sağlar
* `azure hdinsight config`-için bir yapılandırma dosyası oluşturma ile Merhaba kullanılabilir komutlar sağlar `hdinsight cluster create` tooprovide yapılandırma bilgilerini komutu.

### <a name="deprecated-commands"></a>Kullanım dışı komutları
Merhaba kullanırsanız `azure hdinsight job` komutları toosubmit işleri tooyour Hdınsight kümesi, bunlar hello ARM komutlarını kullanılabilir değildir. Tooprogrammatically gönderme işleri tooHDInsight komut dosyalarından gerekiyorsa, bunun yerine hello Hdınsight tarafından sağlanan REST API'lerini kullanmanız gerekir. REST API'lerini kullanarak işlerini göndermenin daha fazla bilgi için aşağıdaki belgeleri hello bakın.

* [CURL kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma](hdinsight-hadoop-use-mapreduce-curl.md)
* [CURL kullanarak Hdınsight'ta Hadoop ile Hive sorguları çalıştırma](hdinsight-hadoop-use-hive-curl.md)
* [CURL kullanarak Hdınsight'ta Hadoop ile pig işleri çalıştırma](hdinsight-hadoop-use-pig-curl.md)

Diğer yolları toorun MapReduce hakkında bilgi için Hive ve etkileşimli olarak Pig bkz [hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md), [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md), ve [Hadoop ile Pig kullanma Hdınsight](hdinsight-use-pig.md).

### <a name="examples"></a>Örnekler
**Küme oluşturma**

* Eski komutu (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Yeni komutu (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Küme silme**

* Eski komutu (ASM)-`azure hdinsight cluster delete myhdicluster`
* Yeni komutu (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`

**Liste kümeleri**

* Eski komutu (ASM)-`azure hdinsight cluster list`
* Yeni komutu (ARM)-`azure hdinsight cluster list`

> [!NOTE]
> Merhaba Listele komutu için kaynak grubunu kullanarak hello belirtme `-g` yalnızca hello kümeler hello belirtilen kaynak grubunda döndürür.
> 
> 

**Küme bilgilerini göster**

* Eski komutu (ASM)-`azure hdinsight cluster show myhdicluster`
* Yeni komutu (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Geçirme Azure PowerShell tooAzure Kaynak Yöneticisi
Merhaba hello Azure Resource Manager (ARM) modunda Azure PowerShell hakkında genel bilgiler bulunabilir [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).

Hello Azure PowerShell ARM cmdlet'leri yüklü yan yana hello ASM cmdlet'leri ile olabilir. Merhaba iki moddan Hello cmdlet'leri, adlarına göre ayırt edilebilir.  Merhaba ARM modu *AzureRmHDInsight* çok karşılaştırma hello cmdlet'in adlarındaki*AzureHDInsight* hello ASM modunda.  Örneğin, *yeni AzureRmHDInsightCluster* vs. *AzureHDInsightCluster yeni*. Parametreleri ve anahtarları haber adlara sahip ve çok sayıda yeni parametreler kullanılabilir ARM kullanırken yoktur.  Örneğin, birkaç cmdlet'leri adlı yeni bir anahtar gerektiren *- ResourceGroupName*. 

Merhaba Hdınsight cmdlet'lerini kullanmadan önce tooyour Azure hesabı bağlanmak ve yeni bir kaynak grubu oluşturmanız gerekir:

* Login-AzureRmAccount veya [seçin AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx). Bkz: [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Yeni-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Yeniden adlandırılmış cmdlet'leri
toolist hello Hdınsight ASM cmdlet'lerini Windows PowerShell konsolunda:

    help *azurermhdinsight*

Merhaba aşağıdaki tabloda hello ASM cmdlet'leri ve hello ARM modunda adları listelenmektedir:

| ASM cmdlet'leri | ARM cmdlet'leri |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Ekleme AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Ekleme AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Ekleme AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Ekleme AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[GRANT-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[GRANT-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Çağırma AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[AzureRmHDInsightCluster yeni](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[AzureRmHDInsightClusterConfig yeni](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[AzureRmHDInsightHiveJobDefinition yeni](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[AzureRmHDInsightMapReduceJobDefinition yeni](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[AzureRmHDInsightPigJobDefinition yeni](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[AzureRmHDInsightSqoopJobDefinition yeni](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[AzureRmHDInsightStreamingMapReduceJobDefinition yeni](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[REVOKE-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[REVOKE-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Kullanım AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Bekleme AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Yeni cmdlet’ler
Merhaba, yalnızca hello ARM modunda kullanılabilir hello yeni cmdlet'ler şunlardır. 

**Betik eylemi cmdlet'leri ilgili:**

* **Get-AzureRmHDInsightPersistedScriptAction**: alır hello bir küme için betik eylemleri kalıcı kronolojik sırayla listelenir ve Ayrıntılar için belirtilen kalıcı betik eylemi alır. 
* **Get-AzureRmHDInsightScriptActionHistory**: hello betik eylemi geçmişi bir küme için alır ve geriye doğru kronolojik sırayla listelenir ya da daha önce yürütülen betik eylemi ayrıntılarını alır. 
* **Remove-AzureRmHDInsightPersistedScriptAction**: kalıcı betik eylemi bir Hdınsight kümeden kaldırır.
* **Set-AzureRmHDInsightPersistedScriptAction**: daha önce yürütülen betik eylemi toobe kalıcı betik eylemi ayarlar.
* **Gönderme AzureRmHDInsightScriptAction**: yeni bir komut dosyası eylemi tooan Azure Hdınsight kümesi gönderir. 

Ek kullanım bilgileri için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).

**Clsuter kimlik cmdlet'leri ilgili:**

* **Ekleme AzureRmHDInsightClusterIdentity**: Merhaba Hdınsight kümesi Azure Data Lake depoları erişebilmesi için bir küme kimlik tooa küme yapılandırma nesnesi ekler. Bkz: [Azure PowerShell kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>Örnekler
**Küme oluşturma**

Eski komutu (ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Yeni komut (ARM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Küme silme**

Eski komutu (ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

Yeni komut (ARM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Liste küme**

Eski komutu (ASM):

    Get-AzureHDInsightCluster

Yeni komut (ARM):

    Get-AzureRmHDInsightCluster 

**Küme Göster**

Eski komutu (ASM):

    Get-AzureHDInsightCluster -Name $clusterName

Yeni komut (ARM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Diğer örnekleri
* [Hdınsight kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Hive işlerini gönderme](hdinsight-hadoop-use-hive-powershell.md)
* [Pig işleri gönderme](hdinsight-hadoop-use-pig-powershell.md)
* [Sqoop işleri gönderme](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Geçirme toohello ARM tabanlı Hdınsight .NET SDK'sı
Azure Hizmet Yönetimi-based hello [(ASM) Hdınsight .NET SDK'sı](https://msdn.microsoft.com/library/azure/mt416619.aspx) artık kullanım dışı bırakılmıştır. Kullanmaları toouse olan Azure kaynak yönetimi tabanlı hello [(ARM) Hdınsight .NET SDK'sı](https://msdn.microsoft.com/library/azure/mt271028.aspx). Merhaba aşağıdaki ASM tabanlı Hdınsight paketleri itibaren kullanımdan kalkacaktır.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

Bu bölümde işaretçileri toomore ilgili bilgiler verilmektedir tooperform kullanarak görevleri hello ARM tabanlı SDK belirli.

| Nasıl yapılır... hello ARM tabanlı Hdınsight SDK kullanarak | Bağlantılar |
| --- | --- |
| .NET SDK kullanarak Hdınsight kümeleri oluşturma |Bkz: [Hdınsight kümeleri oluşturma .NET SDK kullanarak](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| .NET SDK'sı ile betik eylemi kullanarak bir küme özelleştirme |Bkz: [özelleştirme Hdınsight Linux kümeleri betik eylemi kullanarak](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| .NET SDK'sı ile etkileşimli olarak Azure Active Directory kullanarak uygulamaları kimlik doğrulaması |Bkz: [.NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md). Bu makalede Hello kod parçacığını hello etkileşimli kimlik doğrulaması yaklaşımı kullanır. |
| Uygulamaları etkileşimsiz .NET SDK ile Azure Active Directory'yi kullanarak kimlik doğrulaması |Bkz: [Hdınsight için etkileşimli olmayan uygulamalar oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| .NET SDK kullanarak Hive işi Gönder |Bkz: [gönderme Hive işleri](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| .NET SDK kullanarak bir Pig işi gönderin |Bkz: [gönderme Pig işleri](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| .NET SDK kullanarak Sqoop işi Gönder |Bkz: [gönderme Sqoop işleri](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| .NET SDK kullanarak Hdınsight kümeleri listesi |Bkz: [listesi Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| .NET SDK kullanarak Hdınsight kümelerini ölçeklendirme |Bkz: [ölçek Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| .NET SDK kullanarak Grant/revoke erişim tooHDInsight kümeleri |Bkz: [Grant/revoke erişim tooHDInsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| HTTP kullanıcı kimlik bilgilerini .NET SDK kullanarak Hdınsight kümelerini güncelleştirme |Bkz: [Hdınsight kümeleri için güncelleştirme HTTP kullanıcı kimlik bilgileri](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| .NET SDK kullanarak Hdınsight kümeleri için Hello varsayılan depolama hesabı bulunamadı |Bkz: [Hdınsight kümeleri için hello varsayılan depolama hesabı bulunamadı](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| .NET SDK kullanarak Hdınsight kümelerini Sil |Bkz: [silmek Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>Örnekler
Nasıl bir işlem olduğunu ilişkin bazı örnekler şunlardır hello ASM tabanlı SDK ve hello eşdeğer kod parçacığını Merhaba ARM tabanlı SDK kullanılarak gerçekleştirilir.

**Bir küme CRUD istemcisi oluşturma**

* Eski komutu (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Yeni komutu (ARM) (hizmet sorumlusu yetkilendirme)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Yeni komutu (ARM) (kullanıcı kimlik doğrulaması)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Küme oluşturma**

* Eski komutu (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Yeni komutu (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**HTTP erişimini etkinleştirme**

* Eski komutu (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Yeni komutu (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Küme silme**

* Eski komutu (ASM)
  
        client.DeleteCluster(dnsName);
* Yeni komutu (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

