---
title: "hdınsight'ta Hadoop işleri için aaaUpload verileri | Microsoft Docs"
description: "Azure CLI, Azure Storage Gezgini, Azure PowerShell, hello Hadoop komut satırı veya Sqoop kullanarak Hdınsight'ta Hadoop işleri için tooupload ve erişim verileri nasıl hello öğrenin."
keywords: "etl hadoop alma verileri hadoop, hadoop veri yükleme"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>HDInsight'ta Hadoop işleri için veri yükleme
Azure Hdınsight tam özellikli Hadoop dağıtılmış dosya sistemi (HDFS) üzerinden Azure Blob Depolama sağlar. Bunun tasarlandığından toocustomers bir HDFS uzantısı tooprovide sorunsuz bir deneyim. Merhaba Hadoop ekosistemi toooperate doğrudan yönettiği hello verileri bileşenlerinde hello kümesini sağlar. Azure Blob Depolama ve HDFS depolama verilerinin ve bu verileri hesaplamalar için iyileştirilmiş farklı dosya sistemleridir. Azure Blob storage kullanma hello yararları hakkında bilgi için [Azure Blob storage kullanma Hdınsight ile][hdinsight-storage].

**Önkoşullar**

Başlamadan önce aşağıdaki gereksinim hello dikkat edin:

* Azure Hdınsight kümesi. Yönergeler için bkz: [Azure Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision].

## <a name="why-blob-storage"></a>Neden blob depolama?
Azure Hdınsight kümeleri genellikle olan toorun MapReduce işleri dağıtılır ve bu işlemler tamamlandıktan sonra hello kümeleri bırakılır. Hesaplamalar tamamlandıktan sonra hello HDFS kümelerde hello veri tutma pahalı yolu toostore bu verileri olacaktır. Azure Blob Depolama, yüksek oranda kullanılabilir, yüksek düzeyde ölçeklenebilir, yüksek kapasite, Hdınsight kullanarak işlenen toobe veriler için düşük maliyetli ve paylaşılabilir depolama seçeneği değil. Bir blob verileri depolamak verilerini kaybetmeden güvenle yayımlanan hesaplama toobe için kullanılan hello Hdınsight kümeleri sağlar.

### <a name="directories"></a>Dizinler
Azure Blob storage kapsayıcıları verileri anahtar/değer çiftleri olarak depolar ve dizin hiyerarşisi yok. Ancak hello "/" karakteri görünür bir dosyayı dizin yapısında depolanmış gibi hello anahtar adı toomake içinde kullanılabilir. Gerçek dizinleri varsa gibi Hdınsight bu görür.

Örneğin, bir blob'un anahtarı *input/log1.txt* şeklinde olabilir. Hiçbir gerçek "Giriş" dizini var, ancak hello toohello varlığını son "/" karakterini hello anahtar adı, bir dosya yolu hello görünümünü içeriyor.

Azure Explorer Araçları kullanırsanız, bu nedenle, bazı 0 bayt dosyaları fark edebilirsiniz. Bu dosyaları iki amaca hizmet eder:

* Boş klasörleri varsa, bunlar hello klasörü hello varlığını işaretleyin. Azure Blob Depolama birimi olan foo/çubuğu adlı bir blob varsa adlı bir klasör yok akıllı tooknow **foo**. Ancak boş bir klasör olarak adlandırılan tek yolu toosignify hello **foo** yerinde bu özel 0 bayt dosya sağlayarak değil.
* Bunlar, özel meta verileri Hadoop hello tarafından özellikle hello izinleri ve sahiplerine hello klasörler için dosya sistemi basılı tutun.

## <a name="command-line-utilities"></a>Komut satırı yardımcı programları
Microsoft Azure Blob storage ile yardımcı programları toowork aşağıdaki hello sağlar:

| Aracı | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Azure komut satırı arabirimi][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Hadoop komutu](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Hello Azure CLI, Azure PowerShell ve AzCopy tüm edebilirsiniz dış azure'dan hello komutu yalnızca hello Hdınsight kümesinde kullanılabilir ve yalnızca Azure Blob depolama alanına hello yerel dosya sisteminden verileri yüklenirken verir Hadoop kullanılabilir.
>
>

### <a id="xplatcli"></a>Azure CLI
Hello Azure CLI toomanage Azure sağlayan bir araçtır platformlar arası Hizmetleri. Aşağıdaki adımları tooupload veri tooAzure Blob Depolama hello kullan:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Yükleme ve Mac, Linux ve Windows hello Azure CLI yapılandırma](../cli-install-nodejs.md).
2. Bir komut istemi, bash ya da diğer kabuğunu açın ve tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullanın.

        azure login

    İstendiğinde, aboneliğiniz için hello kullanıcı adı ve parola girin.
3. Komut toolist hello depolama hesapları, aboneliğiniz için aşağıdaki hello girin:

        azure storage account list
4. Merhaba blob ile toowork istediğiniz içeren hello depolama hesabını seçin, sonra komutu tooretrieve hello anahtarı bu hesap için aşağıdaki hello kullanın:

        azure storage account keys list <storage-account-name>

    Bu döndürmelidir **birincil** ve **ikincil** anahtarları. Kopya hello **birincil** hello sonraki adımlarda kullanılacak çünkü anahtar değeri.
5. Komut tooretrieve hello depolama hesabındaki blob kapsayıcılar listesi aşağıdaki hello kullan:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Dosyaları toohello blob indirmek ve aşağıdaki komutları tooupload hello kullanın:

   * bir dosya tooupload:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * bir dosya toodownload:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Her zaman hello ile aynı çalışacaksınız, depolama hesabı ayarlama hello hesabı belirtme yerine ortam değişkenleri aşağıdaki hello ve anahtar her komut için:
>
> * **AZURE\_depolama\_hesap**: hello depolama hesabı adı
> * **AZURE\_depolama\_erişim\_anahtar**: hello depolama hesabı anahtarı
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell toocontrol kullanın ve hello dağıtımı ve Yönetimi azure'da iş yüklerinizin otomatikleştirmek bir komut dosyası ortamıdır. İş istasyonu toorun Azure PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload bir yerel dosya tooAzure Blob Depolama**

1. Belirtildiği gibi açık hello Azure PowerShell konsolunda [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).
2. Merhaba hello ilk beş değişkenleri komut dosyası izleyen hello ayarlayın:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Yapıştır hello komut dosyası hello Azure PowerShell konsol toorun onu toocopy hello dosya.

Örneğin, Hdınsight ile PowerShell oluşturulan komut dosyalarını toowork bkz [Hdınsight Araçları](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy, bir komut satırı aracını içine ve dışına bir Azure Storage hesabı veri aktarma toosimplify hello görev tasarlanmış ' dir. Ayrı bir araç olarak kullanabilir veya varolan bir uygulama bu aracı içerecek. [AzCopy karşıdan][azure-azcopy-download].

Merhaba AzCopy söz dizimi aşağıdaki gibidir:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Daha fazla bilgi için bkz: [dosyaları Azure BLOB'ları için karşıya yükleme/indirme AzCopy -][azure-azcopy].

### <a id="commandline"></a>Hadoop komut satırı
Merhaba Hadoop komut satırı, yalnızca hello veri hello küme baş düğümünde zaten geldiğinde, verileri blob depolama alanına depolamak için yararlıdır.

Sipariş toouse hello Hadoop komutu, yöntemler aşağıdaki hello birini kullanarak toohello headnode önce bağlanmanız gerekir:

* **Windows tabanlı Hdınsight**: [Uzak Masaüstü kullanarak bağlan](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **Linux tabanlı Hdınsight**: SSH kullanarak bağlan ([SSH komutu hello](hdinsight-hadoop-linux-use-ssh-unix.md) veya [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Bağlantı kurulduktan sonra aşağıdaki sözdizimi tooupload dosya toostorage hello kullanabilirsiniz.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Örneğin, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Merhaba varsayılan dosya sistemi Hdınsight için Azure Blob depolama alanına olduğundan, /example/data.txt gerçekte Azure Blob depolama alanına değildir. Toohello dosyası olarak da başvurabilir:

    wasb:///example/data/data.txt

or

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Diğer Hadoop listesini dosyalarıyla çalışan komutlar için bkz: [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> Veri yazma 256 KB HBase kümelerinde hello varsayılan blok boyutu kullanılır. Merhaba kullanırken bu HBase API'lerini veya REST API'leri kullanırken düzgün çalışır, `hadoop` veya `hdfs dfs` komutları toowrite veri ~ 12 GB'den büyük hatayla sonuçlanır. Merhaba bkz [blob yazma için depolama özel durumu](#storageexception) daha fazla bilgi için bölüm aşağıda.
>
>

## <a name="graphical-clients"></a>Grafik istemcileri
Azure Storage ile çalışmak için bir grafik arabirim sağlayan birkaç uygulamalar vardır. Merhaba, bu uygulamaları birkaç listesi aşağıdadır:

| İstemci | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Hdınsight için Microsoft Visual Studio Araçları](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure Depolama Gezgini](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Bulut depolama Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Gezgini](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Hdınsight için Visual Studio Araçları
Daha fazla bilgi için bkz: [Bul hello bağlı kaynakları](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Azure Storage Gezgini
*Azure Storage Gezgini* inceleme ve BLOB'lar hello verileri değiştirme için yararlı bir araçtır. Bu, yüklenebilir bir ücretsiz, açık kaynak aracıdır [http://storageexplorer.com/](http://storageexplorer.com/). Merhaba kaynak kodu, bu bağlantıdan kullanılabilir.

Merhaba aracını kullanmadan önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir. Hello bu bilgileri alma hakkında yönergeler için bkz "nasıl yapılır: erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama" bölümünü [oluşturma, yönetme veya bir depolama hesabı silme][azure-create-storage-account].

1. Azure Storage Gezgini çalıştırın. Bu ilk kez hello ise hello Depolama Gezgini'ni çalıştırmak, Merhaba istenir **_vm hesap adı** ve **depolama hesabı anahtarı**. Daha önce çalıştırdıysanız, hello kullan **Ekle** düğmesini tooadd yeni depolama hesabı adı ve anahtar.

    Merhaba adını ve Hdınsight küme tarafından kullanılan hello depolama hesabı için anahtar ve seçip girin **Aç & Kaydet**.

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. Kapsayıcıları toohello hello arabirimi solundaki Hello listesinde Hdınsight kümenizle ilişkilendirilmiş hello kapsayıcı hello adına tıklayın. Varsayılan olarak, bu hello hello Hdınsight kümenizin adıdır, ancak belirli bir ad hello kümesi oluştururken girdiyseniz farklı olabilir.
3. Merhaba araç çubuğundan hello karşıya yükleme simgesini seçin.

    ![Araç çubuğu vurgulanmış karşıya yükleme simgesi](./media/hdinsight-upload-data/toolbar.png)
4. Bir dosya tooupload belirtin ve ardından **açık**. İstendiğinde, seçin **karşıya** tooupload hello dosya toohello kök hello depolama kapsayıcısı. Tooupload hello dosya tooa belirli yolu istiyorsanız hello hello yolu girin **hedef** alan ve ardından **karşıya**.

    ![Dosya yükleme iletişim kutusu](./media/hdinsight-upload-data/fileupload.png)

    Merhaba dosya karşıya yükleme tamamlandıktan sonra hello Hdınsight kümesinde işleri kullanabilirsiniz.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Azure Blob Depolama Birimi yerel sürücü olarak bağlama
Bkz: [bağlama Azure Blob Storage yerel sürücü olarak](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Hizmetler
### <a name="azure-data-factory"></a>Azure Data Factory
Hello Azure Data Factory hizmetine kolaylaştırılmış, ölçeklenebilir ve güvenilir veri üretim ardışık düzenlerle veri depolama, veri işleme ve veri taşıma hizmetleri oluşturmak için tam olarak yönetilen bir hizmettir.

Azure Data Factory kullanılan toomove veriler Azure Blob depolama alanına olabilir veya doğrudan Hdınsight gibi özelliklerine toocreate veri ardışık Hive veya Pig.

Daha fazla bilgi için bkz: Merhaba [Azure Data Factory belgelerine](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop, Hadoop ve ilişkisel veritabanları arasında tasarlanmış aracı tootransfer verilerdir. SQL Server, MySQL veya Oracle hello Hadoop dağıtılmış dosya sistemi (HDFS) içine dönüştürme hello verileri Hadoop ile MapReduce veya Hive ve uygulamasına geri hello verileri dışarı aktarma gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) tooimport verilerden kullanabilirsiniz bir RDBMS.

Daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop].

## <a name="development-sdks"></a>Geliştirme SDK'ları
Azure Blob Depolama, programlama dilleri aşağıdaki hello bir Azure SDK kullanarak da erişilebilir:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Hello Azure SDK'ları yükleme hakkında daha fazla bilgi için bkz: [Azure indirir](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Sorun giderme
### <a id="storageexception"></a>Blob yazma için depolama özel durumu
**Belirtiler**: hello kullanırken `hadoop` veya `hdfs dfs` toowrite dosyaları ~ 12 GB komutlardır veya daha büyük bir HBase kümesi üzerinde aşağıdaki hata hello karşılaşabilirsiniz:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Neden**: hdınsight'ta HBase kümeleri varsayılan tooa blok boyutu 256 KB tooAzure depolama yazılırken. Bu HBase API'lerini veya REST API'leri için çalışırken, onu bir hatayla hello kullanırken sonuçlanır `hadoop` veya `hdfs dfs` komut satırı yardımcı programları.

**Çözümleme**: kullanım `fs.azure.write.request.size` toospecify daha büyük bir blok boyutu. Bir kullanım başına temelinde hello kullanarak bunu yapabilirsiniz `-D` parametresi. Merhaba hello ile bu parametresini kullanarak bir örnek verilmiştir `hadoop` komutu:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Merhaba değerini de artırabilirsiniz `fs.azure.write.request.size` Ambari kullanarak genel. Merhaba aşağıdaki adımları olabilir hello Ambari Web kullanıcı arabirimini toochange hello değeri kullanılır:

1. Tarayıcınızda, kümeniz için Ambari Web kullanıcı arabirimini toohello gidin. Https://CLUSTERNAME.azurehdinsight.net, budur nerede **CLUSTERNAME** hello kümenizin adıdır.

    İstendiğinde, hello küme için hello yönetici adı ve parola girin.
2. Yan hello ekranın sol hello seçin **HDFS**ve ardından hello **yapılandırmalar** sekmesi.
3. Merhaba, **filtre... ** alanına, `fs.azure.write.request.size`. Bu hello alan ve geçerli değer hello sayfa hello ortadaki görüntüler.
4. Merhaba değer 262144 (256 KB) toohello yeni değerini değiştirin. Örneğin, 4194304 (4MB).

![Ambari Web kullanıcı Arabirimi aracılığıyla hello değeri değiştirme resmi](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Ambari kullanarak daha fazla bilgi için bkz: [hello Ambari Web kullanıcı arabirimini kullanarak yönetin Hdınsight kümelerini](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Sonraki adımlar
Anladığınıza göre Hdınsight tooget verisine nasıl okuma makaleleri toolearn nasıl aşağıdaki hello tooperform analiz:

* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]
* [Hadoop işlerini programlı olarak gönderme][hdinsight-submit-jobs]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
