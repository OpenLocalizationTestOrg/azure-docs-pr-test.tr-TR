---
title: "Paylaşılan erişim imzaları - Azure Hdınsight kullanarak aaaRestrict erişim | Microsoft Docs"
description: "Nasıl toouse paylaşılan erişim imzaları toorestrict Hdınsight erişim Azure storage bloblarında depolanır toodata öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Azure Storage paylaşılan erişim imzaları toorestrict erişim toodata Hdınsight'ta kullanın

Hdınsight tam erişim toodata hello kümesi ile ilişkili hello Azure depolama hesapları vardır. Paylaşılan erişim imzaları hello blob kapsayıcı toorestrict erişim toohello verileri üzerinde kullanabilirsiniz. Örneğin, tooprovide salt okunur erişim toohello verileri. Paylaşılan erişim imzaları (SAS) toolimit erişim toodata sağlayan bir Azure depolama hesapları özelliğidir. Örneğin, salt okunur erişim toodata sağlama.

> [!IMPORTANT]
> Apache bırakabilmenizi kullanarak bir çözüm için etki alanına katılmış Hdınsight kullanmayı düşünün. Daha fazla bilgi için bkz: Merhaba [etki alanına katılmış Hdınsight yapılandırma](hdinsight-domain-joined-configure.md) belge.

> [!WARNING]
> Hdınsight hello kümesi için tam erişim toohello varsayılan depolama olması gerekir.

## <a name="requirements"></a>Gereksinimler

* Bir Azure aboneliği
* C# veya Python. C# kod örneği, bir Visual Studio çözümü olarak sağlanır.

  * Visual Studio 2013, 2015 veya 2017 sürümü olması gerekir
  * Python 2.7 ya da daha yüksek bir sürüm olması gerekir

* Linux tabanlı Hdınsight kümesi veya [Azure PowerShell] [ powershell] -mevcut bir Linux tabanlı kümeniz varsa, Ambari tooadd bir paylaşılan erişim imzası toohello küme kullanabilirsiniz. Aksi durumda, Azure PowerShell toocreate bir küme kullanın ve küme oluşturma sırasında bir paylaşılan erişim imzası ekleyin.

    > [!IMPORTANT]
    > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Örnek dosyalarından hello [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Bu depo hello aşağıdaki öğeleri içerir:

  * Hdınsight ile kullanmak için bir depolama kapsayıcısı, depolanan ilke ve SAS oluşturabilirsiniz bir Visual Studio projesi
  * Hdınsight ile kullanmak için bir depolama kapsayıcısı, depolanan ilke ve SAS oluşturabilirsiniz bir Python komut dosyası
  * Bir Hdınsight oluşturabilmeniz için bir PowerShell Betiği küme ve toouse hello SAS yapılandırın.

## <a name="shared-access-signatures"></a>Paylaşılan erişim imzaları

Paylaşılan erişim imzaları iki tür vardır:

* Geçici: hello başlangıç saati, sona erme saati ve SAS tüm belirtilen SAS URI'sini hello üzerinde hello izinlerini.

* Erişim ilkesinde saklanan: depolanmış erişim ilkesi, bir blob kapsayıcısını gibi bir kaynak kapsayıcısı üzerinde tanımlanır. Bir ilke bir veya daha fazla paylaşılan erişim imzalar için kullanılan toomanage kısıtlamaları olabilir. Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, hello SAS hello kısıtlamaları devralır - hello başlangıç saati, sona erme saati ve izinleri - depolanan hello erişim ilkesi için tanımlı.

Merhaba fark hello iki formlar arasında önemli bir senaryo için önemlidir: iptal. Merhaba SAS edinir herkes, kimin istenen bağımsız olarak toobegin ile kullanabilmesi için bir SAS bir URL ' dir. Bir SAS yayımlandığını, hello world herkes tarafından kullanılabilir. Dağıtılan bir SAS dört özelliklerinden biri işlem yapılana kadar geçerlidir:

1. SAS ulaşıldığında hello üzerinde belirtilen hello bitiş saati.

2. SAS ulaşıldığında hello tarafından başvurulan depolanan hello erişim ilkesinde belirtilen hello bitiş saati. Merhaba aşağıdaki senaryolara neden hello sona erme saati toobe ulaştı:

    * Merhaba süre geçti.
    * depolanan hello erişim ilkesi değiştirilmiş toohave bir sona erme hello geçmiş saattir. Merhaba sona erme saati değiştirme tek yönlü toorevoke hello SAS olur.

3. Merhaba, başka bir şekilde toorevoke hello SAS SAS silinir, hello tarafından başvurulan erişim ilkesi depolanır. Depolanan hello erişim ilkesi ile aynı adı, için tüm SAS belirteci hello yeniden yapıyorsanız hello önceki ilke (Merhaba sona erme saati hello üzerinde SAS değil geçtiyse) geçerli olur. Toorevoke hello SAS düşünüyorsanız, hello erişim ilkesi hello gelecekteki içinde bir sona erme saati ile yeniden farklı bir ad emin toouse olması.

4. kullanılan toocreate hello SAS olduğu hello hesap anahtarını yeniden oluşturur. Başlangıç anahtarı yeniden oluşturuluyor hello önceki anahtar toofail kimlik doğrulaması kullanan tüm uygulamalar neden olur. Tüm bileşenleri toohello yeni anahtarı güncelleştirin.

> [!IMPORTANT]
> Paylaşılan erişim imzası URI hello hesabı anahtar kullanılan toocreate hello imza ile ilişkili ve hello depolanmış erişim ilkesi (varsa) ilişkili. Hiçbir depolanmış erişim ilkesi belirtilirse, hello yalnızca yolu toorevoke paylaşılan erişim imzası toochange hello hesap anahtardır.

Her zaman depolanmış erişim ilkeleri kullanmanızı öneririz. Depolanan ilkelerde kullanırken imzaları iptal etmek veya gerektiği gibi hello sona erme tarihini uzatmak. Bu belgedeki Hello adımları depolanmış erişim ilkeleri toogenerate SAS kullanın.

Paylaşılan erişim imzaları ile ilgili daha fazla bilgi için bkz: [anlama hello SAS modelini](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Depolanan ilke ve C kullanarak SAS oluşturma\#

1. Merhaba çözümü Visual Studio'da açın.

2. Çözüm Gezgini'nde hello üzerinde sağ **SASToken** proje ve seçin **özellikleri**.

3. Seçin **ayarları** ve girişleri aşağıdaki hello değerlerini ekleyin:

   * StorageConnectionString: hello bağlantı dizesi toocreate istediğiniz hello depolama hesabı için depolanan ilke ve SAS için. Hello biçiminde olmalıdır `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` nerede `myaccount` depolama hesabınız hello adıdır ve `mykey` hello depolama hesabı için hello anahtarıdır.

   * ContainerName: toorestrict erişmek istediğiniz hello depolama hesabındaki hello kapsayıcı.

   * SASPolicyName: hello adı toouse hello için ilke toocreate depolanır.

   * FileToUpload: karşıya yüklenen toohello kapsayıcı hello yolu tooa dosya.

4. Merhaba projesini çalıştırın. Merhaba SAS oluşturulduktan sonra metin aşağıdaki bilgileri benzer toohello görüntülenir:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Merhaba SAS İlkesi belirteci, depolama hesabı adı ve kapsayıcı adını kaydedin. Hdınsight kümenizle hello depolama hesabını ilişkilendirerek bu değerler kullanılır.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Depolanan ilke ve Python kullanarak SAS oluşturma

1. Merhaba SASToken.py dosyasını açın ve aşağıdaki değerleri hello değiştirin:

   * İlke\_ad: hello adı toouse hello için depolanan ilke toocreate.

   * Depolama\_hesap\_ad: hello depolama hesabınızın adını.

   * Depolama\_hesap\_anahtarı: hello depolama hesabının hello anahtarı.

   * Depolama\_kapsayıcı\_ad: toorestrict erişmek istediğiniz hello depolama hesabındaki hello kapsayıcı.

   * örnek\_dosya\_yol: karşıya yüklenen toohello kapsayıcıdır hello yol tooa dosyası.

2. Merhaba komut dosyasını çalıştırın. Metin hello betik tamamlandığında aşağıdaki hello SAS belirteci benzer toohello görüntüler:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Merhaba SAS İlkesi belirteci, depolama hesabı adı ve kapsayıcı adını kaydedin. Hdınsight kümenizle hello depolama hesabını ilişkilendirerek bu değerler kullanılır.

## <a name="use-hello-sas-with-hdinsight"></a>Hdınsight ile Merhaba SAS kullanma

Bir Hdınsight kümesi oluştururken, bir birincil depolama hesabı belirtmeniz gerekir ve isteğe bağlı olarak ek depolama hesapları belirtebilirsiniz. Depolama ekleme bu yöntemlerin her ikisi de tam erişim toohello depolama hesapları ve kullanılan kapsayıcıları gerektirir.

toouse bir paylaşılan erişim imzası toolimit erişim tooa kapsayıcı ekleme özel giriş toohello **çekirdek site** hello küme yapılandırması.

* İçin **Windows tabanlı** veya **Linux tabanlı** Hdınsight kümeleri, PowerShell kullanarak küme oluşturma sırasında hello giriş ekleyebilirsiniz.
* İçin **Linux tabanlı** Hdınsight kümeleri, Ambari kullanarak küme oluşturulduktan sonra başlangıç yapılandırmasını değiştirin.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Merhaba SAS kullanan bir küme oluşturun

SAS hello dahil bu kullanımları hello Hdınsight kümesi oluşturma örneği `CreateCluster` hello havuzun dizin. Bunu, aşağıdaki kullanım hello adımları toouse:

1. Açık hello `CreateCluster\HDInsightSAS.ps1` dosyasını bir metin düzenleyicisinde ve değerleri hello belge hello başında aşağıdaki hello değiştirin.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Örneğin, değiştirme `'mycluster'` toohello adı hello kümesinin toocreate istiyor. Merhaba SAS değerleri, bir depolama hesabı ve SAS belirteci oluştururken hello önceki adımlardan hello değerler eşleşmelidir.

    Merhaba değerlerinin değiştiğini sonra hello dosyasını kaydedin.

2. Yeni bir Azure PowerShell komut istemini açın. Azure PowerShell ile ilgili bilginiz veya yüklemediyseniz, bkz: [yükleyin ve Azure PowerShell yapılandırma][powershell].

1. Merhaba isteminden komutu tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullan:

    ```powershell
    Login-AzureRmAccount
    ```

    İstendiğinde, Azure aboneliğinizin hello hesapla oturum açın.

    Hesabınızın birden çok Azure aboneliği ile ilişkili ise, toouse gerekebilir `Select-AzureRmSubscription` tooselect hello abonelik toouse istiyor.

4. Dizinleri toohello Hello satırından değiştirmek `CreateCluster` hello HDInsightSAS.ps1 dosyasını içeren dizini. Toorun hello komut aşağıdaki hello kullanın

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Merhaba kaynak grubu ve depolama hesapları oluşturur gibi hello komut dosyası çalışırken Çıktı toohello PowerShell istemi kaydeder. İstendiğinde tooenter hello HTTP kullanıcı hello Hdınsight kümesi için var. Kullanılan toosecure HTTP/s erişimini toohello küme hesabıdır.

    Linux tabanlı bir küme oluşturuyorsanız, bir SSH kullanıcı hesabı adı ve parola istenir. Bu hesap, toohello kümedeki kullanılan tooremotely günlüktür.

   > [!IMPORTANT]
   > Merhaba HTTP/s veya SSH kullanıcı adı ve parola istendiğinde, hello aşağıdaki ölçütleri karşılayan bir parola sağlamanız gerekir:
   >
   > * En az 10 karakter uzunluğunda olmalıdır
   > * En az bir rakam içermelidir
   > * En az bir alfasayısal olmayan karakter içermelidir
   > * En az bir büyük veya küçük harf içermelidir

Bir süre bu komut dosyası toocomplete genellikle yaklaşık 15 dakika sürer. Herhangi bir hata olmadan Hello betik tamamlandığında, hello küme oluşturuldu.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Merhaba SAS ile var olan bir küme kullanın

Varolan bir Linux tabanlı kümeniz varsa, hello SAS toohello ekleyebilirsiniz **çekirdek site** hello aşağıdaki adımları kullanarak yapılandırma:

1. Kümeniz için Hello Ambari web kullanıcı arabirimini açın. Hello için bu sayfayı https://YOURCLUSTERNAME.azurehdinsight.net adresidir. İstendiğinde, toohello küme hello yönetici adı (Yönetici) kullanarak kimlik doğrulaması ve ne zaman kullanılan parola hello küme oluşturma.

2. Sol hello Ambari web kullanıcı Arabirimi tarafı hello seçin **HDFS** seçip hello **yapılandırmalar** hello sayfasının hello ortasında sekmesi.

3. Select hello **Gelişmiş** sekmesini tıklatın ve ardından hello bulana kadar kaydırın **özel çekirdek site** bölümü.

4. Merhaba genişletin **özel çekirdek site** bölümünde, sonra kaydırma toohello uç ve select hello **Özellik Ekle...**  bağlantı. Kullanım hello aşağıdaki değerleri Merhaba **anahtar** ve **değeri** alanlar:

   * **Anahtar**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Değer**: hello önceden çalıştırdığınız C# veya Python uygulama tarafından döndürülen SAS hello

     Değiştir **CONTAINERNAME** hello kapsayıcı adı ile Merhaba C# veya SAS uygulaması ile kullanılır. Değiştir **STORAGEACCOUNTNAME** , kullandığınız hello depolama hesabı adı ile.

5. Hello tıklatın **Ekle** toosave bu anahtar ve değer düğmesine tıklayın ve ardından hello **kaydetmek** düğmesini toosave hello yapılandırma değişiklikleri. İstendiğinde, ("SAS depolama erişim örneğin ekleme") hello değişiklik açıklamasını ekleyin ve ardından **kaydetmek**.

    Tıklatın **Tamam** zaman hello değişiklikleri tamamlanmıştır.

   > [!IMPORTANT]
   > Merhaba değişiklik uygulanmadan önce birkaç hizmeti yeniden başlatmanız gerekir.

6. Merhaba Ambari web kullanıcı Arabirimi, seçin **HDFS** sol hello ve ardından hello listeden **yeniden tüm** hello gelen **hizmet eylemleri** hello sağdaki listede aşağı açılır. İstendiğinde, seçin **bakım Modu'nu** ve select yeniden tüm __Conform ".

    MapReduce2 ve YARN için bu işlemi yineleyin.

7. Merhaba hizmetleri yeniden başlattıktan sonra her birini seçin ve hello bakım modundan devre dışı bırakma **hizmet eylemleri** açılır.

## <a name="test-restricted-access"></a>Kısıtlı erişim test

sınırlı tooverify erişim, aşağıdaki yöntemleri kullanın hello:

* İçin **Windows tabanlı** Hdınsight kümeleri, Uzak Masaüstü tooconnect toohello küme kullanın. Daha fazla bilgi için bkz: [bağlanmak, RDP kullanarak tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Bağlantı kurulduktan sonra hello kullan **Hadoop komut satırı** hello Masaüstü tooopen bir komut istemi simgesi.

* İçin **Linux tabanlı** Hdınsight kümeleri, SSH tooconnect toohello küme kullanın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

Toohello küme bağlandıktan sonra yalnızca okuma ve liste öğeleri hello SAS depolama hesabındaki yapabilecekleriniz adımları tooverify aşağıdaki hello kullan:

1. Merhaba kapsayıcısının toolist hello içeriği hello isteminden komutu aşağıdaki hello kullanın: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Değiştir **SASCONTAINER** hello SAS depolama hesabı için oluşturulan hello kapsayıcı hello adı. Değiştir **SASACCOUNTNAME** SAS hello için kullanılan hello depolama hesabının hello ada sahip.

    Merhaba listesi hello kapsayıcı ve SAS oluşturulduğunda karşıya hello dosyası içerir.

2. Kullanım hello aşağıdaki hello hello dosyasının içeriğini okuyabilirsiniz tooverify komutu. Hello yerine **SASCONTAINER** ve **SASACCOUNTNAME** hello önceki adımda olduğu gibi. Değiştir **FILENAME** hello önceki komutta gösterilen hello dosyasının hello adıyla:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Bu komut hello hello dosyasının içeriğini listeler.

3. Komut toodownload hello dosya toohello yerel dosya sistemi aşağıdaki hello kullan:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    İndirmeler hello adlı tooa yerel dosyası bu komut **testdosyası.txt**.

4. Kullanım hello aşağıdaki adlı tooupload hello yerel dosya tooa yeni dosya komutu **testupload.txt** hello SAS depolama üzerinde:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Metin aşağıdaki ileti benzer toohello alırsınız:

        put: java.io.IOException

    Merhaba depolama konumu okuma + liste yalnızca olduğundan bu hata oluşur. Merhaba varsayılan depolama yazılabilir olduğundan hello kümesi için komut tooput hello verileri aşağıdaki hello kullan:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    Bu süre, hello işlemi başarıyla tamamlanmış olmalıdır.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="a-task-was-canceled"></a>Bir görev iptal edildi

**Belirtiler**: hello PowerShell Betiği kullanılarak bir küme oluştururken, hello aşağıdaki hata iletisini alabilirsiniz:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Neden**: Merhaba yönetici/HTTP kullanıcı hello küme veya (Linux tabanlı kümelerde) için bir parola kullanıyorsanız, bu hata oluşabilir hello SSH kullanıcı.

**Çözümleme**: hello aşağıdaki ölçütleri karşılayan bir parola kullanın:

* En az 10 karakter uzunluğunda olmalıdır
* En az bir rakam içermelidir
* En az bir alfasayısal olmayan karakter içermelidir
* En az bir büyük veya küçük harf içermelidir

## <a name="next-steps"></a>Sonraki adımlar

Sizin için artık öğrendiğinize tooadd sınırlı erişimli depolama tooyour Hdınsight kümesi diğer yolları toowork kümenizdeki veri ile nasıl bilgi edinin:

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
