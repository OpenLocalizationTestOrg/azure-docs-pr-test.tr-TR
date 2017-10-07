---
title: "aaaCreate Hdınsight kümeleri Data Lake Store ile varsayılan depolama alanı olarak PowerShell kullanarak | Microsoft Docs"
description: "Azure PowerShell toocreate kullanın ve Hdınsight kümeleri Azure Data Lake Store ile kullanma"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Varsayılan depolama alanı olarak Data Lake Store ile PowerShell kullanarak Hdınsight kümeleri oluşturma
> [!div class="op_single_selector"]
> * [Hello Azure portalını kullanın](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [(Varsayılan depolama için) PowerShell kullanma](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell (için ek depolama alanı) kullanın](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Kaynak Yöneticisi'ni kullanın](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Varsayılan depolama alanı olarak Azure Data Lake Store ile nasıl toouse Azure PowerShell tooconfigure Azure Hdınsight kümeleri hakkında bilgi edinin. Ek depolama alanı olarak Data Lake Store ile bir Hdınsight kümesi oluşturma ile ilgili yönergeler için bkz: [ek depolama alanı olarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-powershell.md).

Hdınsight Data Lake Store ile kullanmak için bazı önemli noktalar şunlardır:

* Merhaba seçeneği toocreate Hdınsight kümeleri erişimi olan Hdınsight sürüm 3.5 ve 3.6 tooData Lake deposu varsayılan depolama olarak kullanılabilir.

* Hdınsight kümeleri ile Merhaba seçeneği toocreate erişim tooData Lake deposu varsayılan depolama olarak *kullanılamaz* Hdınsight Premium kümeleri için.

PowerShell kullanarak Data Lake Store ile tooconfigure Hdınsight toowork hello sonraki beş bölümlerdeki hello yönergeleri izleyin.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello aşağıdaki gereksinimleri karşıladığından emin olun:

* **Bir Azure aboneliği**: çok Git[alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 veya büyük**: bkz [nasıl tooinstall ve PowerShell yapılandırma](/powershell/azure/overview).
* **Windows Yazılım Geliştirme Seti (SDK)**: tooinstall Windows SDK'sı Git çok[indirir ve Windows 10 için Araçlar](https://dev.windows.com/en-us/downloads). Merhaba SDK kullanılan toocreate bir güvenlik sertifikası ' dir.
* **Azure Active Directory hizmet asıl**: Bu öğreticide açıklar nasıl toocreate Azure Active Directory'de (Azure AD) bir hizmet sorumlusu. Ancak, bir hizmet sorumlusu toocreate olmalıdır Azure AD yönetici. Bir yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.

    >[!NOTE]
    >Yalnızca, Azure AD yöneticisiyseniz, bir hizmet asıl oluşturabilirsiniz. Azure AD yöneticinizin Data Lake Store ile Hdınsight kümesi oluşturmadan önce bir hizmet asıl oluşturmanız gerekir. Merhaba hizmet sorumlusu bir sertifikayla açıklandığı şekilde oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Data Lake Store hesabı oluşturma
bir Data Lake Store hesabı toocreate hello aşağıdaki:

1. Masaüstünüzde bir PowerShell penceresi açın ve aşağıdaki hello kod parçacıkları girin. İçinde oturum açma hello abonelik yöneticileri veya sahipleri biri olarak istendiğinde toosign olduğunda. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Merhaba Data Lake Store kaynak sağlayıcısı kaydetme ve çok benzer bir hata alırsanız`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, aboneliğinizin Data Lake Store için Güvenilenler listesine olmayabilir. tooenable hello Data Lake Store genel önizlemesi, Azure aboneliğinizin hello yönergeleri izleyin [hello Azure portal kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).
    >

2. Bir Azure kaynak grubu ile ilişkili bir Data Lake Store hesabıdır. Bir kaynak grubu oluşturarak başlayın.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Bu gibi bir çıktı görmeniz gerekir:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Bir Data Lake Store hesabı oluşturun. Merhaba hesabı, belirttiğiniz ad yalnızca küçük harf ve sayı içermelidir.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. Data Lake Store varsayılan depolama alanı olarak kullanarak küme oluşturma sırasında bir kök yolu toowhich hello kümeye özgü dosyalar kopyalanır toospecify gerektirir. toocreate olan bir kök yolu **/kümeleri/hdiadlcluster** hello parçacığında, hello aşağıdaki cmdlet'leri kullanın:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Rol tabanlı kimlik doğrulaması için ayarlama tooData Lake deposuna erişim
Her Azure aboneliği bir Azure AD varlıkla ilişkilidir. İlk kullanıcılar ve kullanarak abonelik kaynaklarına erişim Azure portalı hello veya Azure Kaynak Yöneticisi API'si hello hizmetler Azure AD ile kimlik doğrulaması gerekir. Erişim tooAzure abonelikleri ve Hizmetleri Azure kaynak üzerinde hello uygun rol atama tarafından verilir. Hizmetler için bir hizmet sorumlusu Azure AD'de hello hizmeti tanımlar.

Bu bölümde, nasıl toogrant bir uygulama hizmeti, Hdınsight gibi erişim tooan Azure kaynak (Merhaba daha önce oluşturduğunuz Data Lake Store hesabı) gösterir. Bir hizmet asıl hello uygulaması oluşturma ve PowerShell aracılığıyla rolleri tooit atayarak bunu.

Active Directory kimlik doğrulaması için Azure Data Lake yukarı tooset iki bölüm şu hello hello görevleri gerçekleştirir.

### <a name="create-a-self-signed-certificate"></a>Otomatik olarak imzalanan sertifika oluşturma
Olduğundan emin olun [Windows SDK](https://dev.windows.com/en-us/downloads) hello işlemine devam etmeden bu bölümdeki adımları önce yüklü. Ayrıca bir dizin gibi oluşturduğunuz gerekir *C:\mycertdir*burada hello sertifika oluşturun.

1. Merhaba PowerShell penceresinden Windows SDK'yı yüklediğiniz toohello konumuna gidin (genellikle *C:\Program Files (x86) \Windows Kits\10\bin\x86*) ve hello [MakeCert] [ makecert] yardımcı programı toocreate otomatik olarak imzalanan bir sertifika ve özel anahtarı. Merhaba aşağıdaki komutları kullanın:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    İstendiğinde tooenter hello özel anahtar parolası olacaktır. Merhaba komutu başarıyla yürütüldükten sonra görmelisiniz **CertFile.cer** ve **mykey.pvk** belirttiğiniz hello sertifika dizininde.
2. Kullanım hello [Pvk2Pfx] [ pvk2pfx] yardımcı programı tooconvert hello .pvk ve .cer dosya o MakeCert oluşturulan tooa .pfx dosyası. Merhaba aşağıdaki komutu çalıştırın:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    İstendiğinde, daha önce belirttiğiniz hello özel anahtar parolası girin. Merhaba hello için belirttiğiniz değere **-SAS** parametredir hello .pfx dosyasıyla ilişkili hello parola. Merhaba komutu başarıyla tamamlandıktan sonra da görmeniz gerekir bir **CertFile.pfx** belirttiğiniz hello sertifika dizininde.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Azure AD oluşturmak ve bir hizmet sorumlusu
Bu bölümde, Azure AD uygulaması için bir hizmet sorumlusu oluşturmak, bir rol toohello hizmet sorumlusu atamak ve bir sertifika sağlayarak hello hizmet sorumlusu kimlik doğrulaması. toocreate uygulamanın Azure AD'de hello aşağıdaki komutları çalıştırın:

1. Cmdlet'leri hello PowerShell konsol penceresinde aşağıdaki hello yapıştırın. Merhaba belirttiğiniz hello değeri emin olun **- DisplayName** özelliği benzersizdir. Merhaba değerlerini **- giriş sayfası** ve **- IdentiferUris** yer tutucu değerlerini olan ve olmayan doğrulanır.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Merhaba uygulama kimliğini kullanarak bir hizmet sorumlusu oluşturma

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Merhaba hizmet asıl erişim toohello Data Lake Store kök ve daha önce belirtilen hello kök yolu tüm hello klasörlerde verin. Hello aşağıdaki cmdlet'leri kullanın:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Hdınsight Linux kümesi Data Lake Store ile Merhaba varsayılan depolama alanı olarak oluşturun.

Bu bölümde, bir Hdınsight Hadoop Linux kümesi hello varsayılan depolama alanı olarak Data Lake Store ile oluşturun. Bu sürüm için Hdınsight kümesi hello ve Data Lake Store hello olmalıdır aynı konumu.

1. Merhaba abonelik Kiracı Kimliği almak ve daha sonra toouse saklayın.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Merhaba Hdınsight kümesi cmdlet'leri aşağıdaki hello kullanarak oluşturun:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Merhaba cmdlet'i başarıyla tamamlandıktan sonra hello küme ayrıntılarını listeler bir çıktı görmeniz gerekir.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Merhaba Hdınsight küme toouse Data Lake Store üzerinde test işleri çalıştırma
Hdınsight kümesi yapılandırdıktan sonra Data Lake Store erişebildiğinizi tooensure üzerinde test işleri çalıştırabilirsiniz. toodo Data Lake Store'da kullanılabilir zaten hello örnek verileri kullanan bir tablo, bir örnek Hive işi toocreate çalıştırmak  *<cluster root>/example/data/sample.log*.

Bu bölümdeki hello oluşturduğunuz Hdınsight Linux kümesi içine güvenli Kabuk (SSH) bağlantısı ve sonra bir örnek Hive sorgusunu çalıştırın.

* Bir Windows istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Linux istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Merhaba bağlantı yaptıktan sonra komutu aşağıdaki hello kullanarak hello Hive komut satırı arabirimi (CLI) başlatın:

        hive
2. Kullanım hello CLI tooenter hello deyimleri toocreate adlı yeni bir tablo aşağıdaki **taşıtlardan** Data Lake Store'da hello örnek verileri kullanarak:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Merhaba SSH konsolda hello sorgu çıktı görmeniz gerekir.

    >[!NOTE]
    >Merhaba yolu toohello örnek CREATE TABLE komutu önceki hello verisinde `adl:///example/data/`, burada `adl:///` hello küme köküdür. Bu öğreticide belirtilen hello küme kök Hello örneği hello komuttur `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Merhaba kısa alternatif kullanın veya hello tam yolunu toohello küme kök sağlayın.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>HDFS komutlarını kullanarak Data Lake Store'a erişme
Merhaba Hdınsight küme toouse Data Lake Store yapılandırdıktan sonra Hadoop dağıtılmış dosya sistemi (HDFS) Kabuk komutları tooaccess hello deposu kullanabilirsiniz.

Bu bölümdeki hello oluşturduğunuz Hdınsight Linux kümesi içine bir SSH bağlantısı ve ardından hello HDFS komutları çalıştırın.

* Bir Windows istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Linux istemci toomake hello kümesine bir SSH bağlantısı kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Merhaba bağlantı yaptıktan sonra HDFS dosya sistemi komutu aşağıdaki hello kullanarak Data Lake Store hello dosyalarında listeleyin.

    hdfs dfs -ls adl:///

Merhaba de kullanabilirsiniz `hdfs dfs -put` tooupload bazı dosyaları tooData Lake Store komutunu ve ardından `hdfs dfs -ls` tooverify hello dosyaları başarıyla karşıya yüklendi.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure portal: Hdınsight küme toouse Data Lake Store oluşturma](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
