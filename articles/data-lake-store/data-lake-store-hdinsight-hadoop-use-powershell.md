---
Başlık: aaa "PowerShell: Azure Hdınsight kümesini Data Lake Store eklenti depolama ile | Microsoft Docs"Hizmetleri: data lake-deposu, hdınsight documentationcenter: '' Yazar: nitinme Yöneticisi: jhubbard Düzenleyicisi: cgronlun

MS.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data lake store ms.devlang: na ms.topic: ms.tgt_pltfrm makale: na ms.workload: büyük veri ms.date: 06/08/2017 ms.author: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>(Azure PowerShell toocreate Hdınsight kümesi Data Lake Store ile ek depolama alanı olarak) kullanın
> [!div class="op_single_selector"]
> * [Portalı kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [(Varsayılan depolama için) PowerShell'i kullanma](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell kullanarak (için ek depolama alanı)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Kaynak Yöneticisi'ni kullanma](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Azure Data Lake Store ile toouse Azure PowerShell tooconfigure bir Hdınsight kümesi nasıl öğrenin **ek depolama alanı olarak**. Azure Data Lake Store varsayılan depolama toocreate bir Hdınsight nasıl kümesi ile ilgili yönergeler için bkz: [varsayılan depolama olarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Hdınsight kümesi için ek depolama alanı olarak toouse Azure Data Lake Store kullanacaksanız, bu makalede anlatıldığı gibi hello küme oluştururken bunu yapmanızı öneririz. Ek depolama alanı tooan Azure Data Lake Store ekleme olan bir Hdınsight kümesine bir karmaşık bir işlem yatkın tooerrors ise.
>

Desteklenen küme türleri için Data Lake Store varsayılan depolama veya ek depolama alanı hesabı olarak kullanılabilir. Data Lake Store ek depolama alanı olarak kullanıldığında, hello varsayılan depolama hesabı hello kümeleri için Azure Storage Blobları (WASB) çıkarılsın ve hello küme ilgili dosyalar (örneğin, günlükleri, vb.) hello veriler toohello varsayılan depolama yazılmış, bir Data Lake Store hesabında tooprocess depolanabilir istiyor. Data Lake Store ek depolama alanı hesabı olarak kullanarak performans veya hello özelliği tooread/yazma toohello depolama hello kümeden etkilemez.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Hdınsight küme depolaması için Data Lake Store kullanma

Hdınsight Data Lake Store ile kullanmak için bazı önemli noktalar şunlardır:

* Seçenek toocreate Hdınsight kümeleri erişimi olan tooData Lake deposu ek depolama alanı olarak Hdınsight sürüm 3.2, 3.4, 3.5 ve 3.6 için kullanılabilir.

Hdınsight yapılandırma PowerShell kullanarak Data Lake Store ile toowork hello aşağıdaki adımları içerir:

* Bir Azure Data Lake deposu oluşturma
* Rol tabanlı kimlik doğrulaması için ayarlama tooData Lake deposuna erişim
* Kimlik doğrulama tooData Lake Store ile Hdınsight kümesi oluşturma
* Test işi hello kümede çalışan

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 veya üstü**. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* **Windows SDK**. Şuradan yükleyebilirsiniz [burada](https://dev.windows.com/en-us/downloads). Bu toocreate bir güvenlik sertifikası kullanın.
* **Azure Active Directory hizmet asıl**. Bu öğreticideki adımlardan hakkında yönergeler sağlayan bir hizmet sorumlusu Azure AD'de toocreate. Ancak, bir Azure AD yönetici toobe mümkün toocreate bir hizmet sorumlusu olması gerekir. Azure AD Yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.

    **Azure AD Yönetici değilseniz**, mümkün tooperform hello adımları gerekli toocreate bir hizmet sorumlusu olmaz. Data Lake Store ile Hdınsight kümesi oluşturmadan önce böyle bir durumda, Azure AD yöneticinizin önce bir hizmet sorumlusu oluşturmanız gerekir. Ayrıca, hello hizmet sorumlusu bir sertifika kullanılarak konusunda açıklandığı gibi oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Bir Azure Data Lake deposu oluşturma
Bu adımları toocreate bir Data Lake Store izleyin.

1. Masaüstünüzde yeni bir Azure PowerShell penceresi açın ve aşağıdaki kod parçacığında hello girin. ' De, istendiğinde toolog emin yaptığınızda, bir hello Abonelik Yöneticisi/sahibi oturum açın:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Çok benzer bir hata alırsanız,`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` hello Data Lake Store kaynak sağlayıcısı kaydedilirken aboneliğinizi Azure Data Lake Store için Güvenilenler listesine değil mümkündür. Bunlar izleyerek, Azure aboneliğinizin Data Lake Store genel önizlemesi için etkinleştirdiğinizden emin olun [yönergeleri](data-lake-store-get-started-portal.md).
   >
   >
2. Azure Data Lake Store hesabı, bir Azure Kaynak Grubu ile ilişkilidir. Azure Kaynak Grubu oluşturma işlemiyle başlayın.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Bu gibi bir çıktı görmeniz gerekir:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Bir Azure Data Lake Store hesabı oluşturun. Merhaba hesabı, belirttiğiniz ad yalnızca küçük harf ve sayı içermesi gerekir.

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

5. Bazı örnek veri tooAzure Data Lake karşıya yükleyin. Bu, daha sonra hello veri bir Hdınsight kümeden erişilebilir olduğunu Bu makale tooverify kullanacağız. Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Rol tabanlı kimlik doğrulaması için ayarlama tooData Lake deposuna erişim
Her Azure aboneliği bir Azure Active Directory ile ilişkilidir. İlk kullanıcı ve hello Azure Klasik portalında veya Azure Kaynak Yöneticisi API'si kullanılarak hello aboneliğin kaynaklara services, Azure Active Directory ile kimliğini doğrulaması gerekir. Erişim tooAzure abonelikleri ve Hizmetleri Azure kaynak üzerinde hello uygun rol atama tarafından verilir.  Hizmetler için bir hizmet sorumlusu hello Azure Active Directory (AAD) hello hizmetinde tanımlar. Bu bölümde nasıl toogrant bir uygulama hizmeti, Azure kaynak (Merhaba daha önce oluşturduğunuz Azure Data Lake Store hesabı) erişim tooan Hdınsight gibi anlatılacaktır Merhaba uygulaması için bir hizmet sorumlusu oluşturma ve Azure aracılığıyla rolleri toothat atayarak PowerShell.

tooset Active Directory kimlik doğrulaması için Azure Data Lake yukarı hello aşağıdaki görevleri gerçekleştirmeniz gerekir.

* Otomatik olarak imzalanan sertifika oluşturma
* Uygulama Azure Active Directory ve bir hizmet sorumlusu oluşturma

### <a name="create-a-self-signed-certificate"></a>Otomatik olarak imzalanan sertifika oluşturma
Olduğundan emin olun [Windows SDK](https://dev.windows.com/en-us/downloads) hello işlemine devam etmeden bu bölümdeki adımları önce yüklü. Ayrıca bir dizin gibi oluşturduğunuz gerekir **C:\mycertdir**, hello sertifika oluşturulacağı.

1. Merhaba PowerShell penceresinden Windows SDK'yı yüklediğiniz toohello konumuna gidin (genellikle `C:\Program Files (x86)\Windows Kits\10\bin\x86` ve hello [MakeCert] [ makecert] yardımcı programı toocreate otomatik olarak imzalanan bir sertifika ve bir özel anahtarı. Merhaba aşağıdaki komutları kullanın.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    İstendiğinde tooenter hello özel anahtar parolası olacaktır. Merhaba komutu başarıyla, görmeniz gerekir yürütüldükten sonra bir **CertFile.cer** ve **mykey.pvk** , belirtilen hello sertifika dizininde.
2. Kullanım hello [Pvk2Pfx] [ pvk2pfx] yardımcı programı tooconvert hello .pvk ve .cer dosya o MakeCert oluşturulan tooa .pfx dosyası. Merhaba aşağıdaki komutu çalıştırın.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    İstendiğinde daha önce belirttiğiniz hello özel anahtar parolası girin. Merhaba hello için belirttiğiniz değere **-SAS** parametredir hello .pfx dosyasıyla ilişkili hello parola. Merhaba komutu başarıyla tamamlandıktan sonra belirtilen hello sertifika dizininde CertFile.pfx görmeniz gerekir.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Bir Azure Active Directory ve bir hizmet sorumlusu oluşturma
Bu bölümde, bir Azure Active Directory uygulaması için başlangıç adımları toocreate bir hizmet sorumlusu gerçekleştirmek, bir rol toohello hizmet sorumlusu atayın ve bir sertifika sağlayarak hello hizmet sorumlusu kimlik doğrulaması. Aşağıdaki komutları toocreate hello Azure Active Directory'de bir uygulamayı çalıştırın.

1. Cmdlet'leri hello PowerShell konsol penceresinde aşağıdaki hello yapıştırın. Merhaba belirttiğiniz emin hello değeri **- DisplayName** özelliği benzersizdir. Ayrıca, değerlerini hello **- giriş sayfası** ve **- IdentiferUris** yer tutucu değerlerini olan ve olmayan doğrulanır.

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
3. Merhaba hizmet asıl erişim toohello Data Lake Store klasörü ve hello Hdınsight kümeden erişecek hello dosya verin. Aşağıdaki Hello parçacığı Data Lake Store (Merhaba örnek veri dosyasını kopyaladığınız) hesap ve dosyasının kendisini hello hello toohello kökündeki erişim sağlar.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Hdınsight Linux kümesi Data Lake Store ile ek depolama alanı olarak oluşturun.

Bu bölümde, bir Hdınsight Hadoop Linux kümesi Data Lake Store ile ek depolama alanı olarak oluşturuyoruz. Bu sürüm için hello hello Hdınsight kümesi ve hello Data Lake Store olmalıdır aynı konumu.

1. Merhaba abonelik Kiracı kimliği alma Başlat Daha sonra ihtiyacınız olacak.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. Bu sürüm için Hadoop kümesi için Data Lake Store yalnızca ek depolama alanı hello küme için kullanılabilir. Merhaba varsayılan depolama hello Azure storage bloblarında (WASB) olmaya devam eder. Bu nedenle, ilk hello depolama hesabı ve depolama kapsayıcılarına hello kümesi için gerekli oluşturacağız.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Merhaba Hdınsight kümesi oluşturur. Cmdlet aşağıdaki hello kullanın.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Merhaba cmdlet'i başarıyla tamamlandıktan sonra hello küme ayrıntıları listeleyen bir çıktı görmeniz gerekir.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Merhaba Hdınsight küme toouse hello Data Lake Store üzerinde test işleri çalıştırma
Hdınsight kümesi yapılandırdıktan sonra o hello Hdınsight test işleri hello küme tootest üzerinde çalıştırabilirsiniz küme, Data Lake Store erişebilir. toodo bu nedenle, biz önceki tooyour Data Lake Store karşıya hello örnek verileri kullanarak bir tablo oluşturur bir örnek Hive işi çalışır.

Bu bölümde Hdınsight Linux küme oluşturduğunuz ve hello örnek Hive sorgusu çalıştırma hello SSH olur.

* Bir Windows istemci tooSSH hello kümesine kullanıyorsanız bkz [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Merhaba kümesine Linux istemci tooSSH kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Bağlandıktan sonra komutu aşağıdaki hello kullanarak hello Hive CLI başlatın:

        hive
2. Merhaba, CLI kullanarak girin deyimleri toocreate adlı yeni bir tablo aşağıdaki hello **taşıtlardan** hello Data Lake Store hello örnek verileri kullanarak:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>HDFS komutları kullanarak erişim Data Lake Store
Merhaba Hdınsight küme toouse Data Lake Store yapılandırdıktan sonra hello HDFS Kabuk komutları tooaccess hello deposu kullanabilirsiniz.

Bu bölümde Hdınsight Linux küme oluşturduğunuz ve hello HDFS komutları çalıştırmak hello SSH olur.

* Bir Windows istemci tooSSH hello kümesine kullanıyorsanız bkz [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Merhaba kümesine Linux istemci tooSSH kullanıyorsanız, bkz: [Linux Hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Bağlantı kurulduktan sonra aşağıdaki hello Data Lake Store, HDFS filesystem komutu toolist hello dosyaları hello kullanın.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Bu, önceki toohello Data Lake Store karşıya hello dosya listelenmelidir.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

Merhaba de kullanabilirsiniz `hdfs dfs -put` tooupload bazı dosyaları toohello Data Lake Store komutunu ve ardından `hdfs dfs -ls` tooverify hello dosyaları başarıyla karşıya yüklendi.

## <a name="see-also"></a>Ayrıca Bkz.
* [Portal: Hdınsight küme toouse Data Lake Store oluşturma](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
