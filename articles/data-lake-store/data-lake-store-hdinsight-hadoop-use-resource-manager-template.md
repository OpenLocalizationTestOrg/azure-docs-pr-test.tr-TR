---
title: "aaaUse Azure şablonları toocreate Hdınsight ve Data Lake Store | Microsoft Docs"
description: "Azure Resource Manager şablonları toocreate kullanın ve Hdınsight kümeleri Azure Data Lake Store ile kullanma"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Azure Resource Manager şablonunu kullanarak Data Lake Store ile Hdınsight kümesi oluşturma
> [!div class="op_single_selector"]
> * [Portalı kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [(Varsayılan depolama için) PowerShell'i kullanma](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell kullanarak (için ek depolama alanı)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Kaynak Yöneticisi'ni kullanma](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Azure Data Lake Store ile toouse Azure PowerShell tooconfigure bir Hdınsight kümesi nasıl öğrenin **ek depolama alanı olarak**.

Desteklenen küme türleri için Data Lake Store bir varsayılan depolama veya ek depolama alanı hesabı olarak kullanılması. Data Lake Store ek depolama alanı olarak kullanıldığında, hello varsayılan depolama hesabı hello kümeleri için Azure Storage Blobları (WASB) çıkarılsın ve hello küme ilgili dosyalar (örneğin, günlükleri, vb.) hello veriler toohello varsayılan depolama yazılmış, bir Data Lake Store hesabında tooprocess depolanabilir istiyor. Data Lake Store ek depolama alanı hesabı olarak kullanarak performans veya hello özelliği tooread/yazma toohello depolama hello kümeden etkilemez.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Hdınsight küme depolaması için Data Lake Store kullanma

Hdınsight Data Lake Store ile kullanmak için bazı önemli noktalar şunlardır:

* Seçenek toocreate Hdınsight kümeleri erişimi olan Hdınsight sürüm 3.5 ve 3.6 tooData Lake deposu varsayılan depolama olarak kullanılabilir.

* Seçenek toocreate Hdınsight kümeleri erişimi olan tooData Lake deposu ek depolama alanı olarak Hdınsight sürüm 3.2, 3.4, 3.5 ve 3.6 için kullanılabilir.

Bu makalede, sizi ek depolama alanı olarak Data Lake Store ile Hadoop kümesi sağlayın. Data Lake Store varsayılan depolama toocreate bir Hadoop nasıl kümesi ile ilgili yönergeler için bkz: [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 veya üstü**. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* **Azure Active Directory hizmet asıl**. Bu öğreticideki adımlardan hakkında yönergeler sağlayan bir hizmet sorumlusu Azure AD'de toocreate. Ancak, bir Azure AD yönetici toobe mümkün toocreate bir hizmet sorumlusu olması gerekir. Azure AD Yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.

    **Azure AD Yönetici değilseniz**, mümkün tooperform hello adımları gerekli toocreate bir hizmet sorumlusu olmaz. Data Lake Store ile Hdınsight kümesi oluşturmadan önce böyle bir durumda, Azure AD yöneticinizin önce bir hizmet sorumlusu oluşturmanız gerekir. Ayrıca, hello hizmet sorumlusu bir sertifika kullanılarak konusunda açıklandığı gibi oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Azure Data Lake Store ile Hdınsight kümesi oluşturma
Merhaba Resource Manager şablonu ve hello önkoşulları hello şablonunu kullanarak github'da kullanılabilir [yeni Data Lake Store ile Hdınsight Linux kümesi dağıtma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Bu bağlantıyı toocreate Hdınsight kümesi hello ek depolama alanı olarak Azure Data Lake Store ile Merhaba yönergelerini izleyin.

Yukarıda belirtilen hello bağlantı Hello yönergeleri PowerShell gerektirir. Bu yönergeler içeren başlamadan önce tooyour Azure hesabı oturum emin olun. Masaüstünüzde yeni bir Azure PowerShell penceresi açın ve aşağıdaki kod parçacıkları hello girin. ' De, istendiğinde toolog emin yaptığınızda, bir hello Abonelik Yöneticisi/sahibi oturum açın:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Örnek veri toohello Azure Data Lake Store karşıya yükle
Merhaba Resource Manager şablonu yeni bir Data Lake Store hesabı oluşturur ve hello Hdınsight küme ile ilişkilendirir. Şimdi bazı örnek veri toohello Data Lake Store yüklemeniz gerekir. Bu veriler, daha sonra hello Data Lake Store verilerine erişmek hello öğretici toorun işlerini bir Hdınsight kümesine ait gerekir. Yönergeler için tooupload verileri, görmek [dosya tooyour Data Lake Store karşıya](data-lake-store-get-started-portal.md#uploaddata). Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>İlgili ACL'leri hello örnek verilere ayarlayın
karşıya yüklediğiniz hello örnek verileri hello Hdınsight kümeden erişilebilir olduğundan emin toomake, kullanılan tooestablish kimlik hello Hdınsight kümesi ve Data Lake Store arasında hello Azure AD uygulama erişim toohello dosya/klasör olduğunuz olduğundan emin olmalısınız tooaccess çalışıyor. toodo bunu hello aşağıdaki adımları gerçekleştirin.

1. Merhaba Hdınsight kümesi ile ilişkili Azure AD uygulaması ve hello Data Lake Store Hello adını bulun. Hello adı için tek yönlü toolook hello Resource Manager şablonu kullanılarak oluşturulan tooopen hello Hdınsight küme dikey penceresinde, hello tıklatın **kümeye özgü AAD kimliği** sekmesini tıklatın ve değeri hello Ara **hizmet sorumlusu Görünen ad**.
2. Şimdi, erişim toothis hello dosya/klasör hello Hdınsight kümeden tooaccess istediğiniz Azure AD uygulaması sağlar. tooset hello sağda ACL'ler hello dosya/klasör Data Lake Store'da görmek [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Merhaba Hdınsight küme toouse hello Data Lake Store üzerinde test işleri çalıştırma
Hdınsight kümesi yapılandırdıktan sonra o hello Hdınsight test işleri hello küme tootest üzerinde çalıştırabilirsiniz küme, Data Lake Store erişebilir. toodo bu nedenle, biz önceki tooyour Data Lake Store karşıya hello örnek verileri kullanarak bir tablo oluşturur bir örnek Hive işi çalışır.

Bu bölümde, SSH Hdınsight Linux kümesi ve çalışma hello halinde örnek Hive sorgusu olur. Windows istemcisi kullanıyorsanız, kullanmanızı öneririz **PuTTY**, hangi adresinden yüklenebilir [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

PuTTY kullanma hakkında daha fazla bilgi için bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Bağlandıktan sonra komutu aşağıdaki hello kullanarak hello Hive CLI başlatın:

   ```
   hive
   ```
2. Merhaba, CLI kullanarak girin deyimleri toocreate adlı yeni bir tablo aşağıdaki hello **taşıtlardan** hello Data Lake Store hello örnek verileri kullanarak:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:

   ```
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
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>HDFS komutları kullanarak erişim Data Lake Store
Merhaba Hdınsight küme toouse Data Lake Store yapılandırdıktan sonra hello HDFS Kabuk komutları tooaccess hello deposu kullanabilirsiniz.

Bu bölümde, SSH Hdınsight Linux kümesi ve çalışma hello halinde HDFS komutu olur. Windows istemcisi kullanıyorsanız, kullanmanızı öneririz **PuTTY**, hangi adresinden yüklenebilir [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

PuTTY kullanma hakkında daha fazla bilgi için bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Bağlantı kurulduktan sonra aşağıdaki hello Data Lake Store, HDFS filesystem komutu toolist hello dosyaları hello kullanın.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Bu, önceki toohello Data Lake Store karşıya hello dosya listelenmelidir.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

Merhaba de kullanabilirsiniz `hdfs dfs -put` tooupload bazı dosyaları toohello Data Lake Store komutunu ve ardından `hdfs dfs -ls` tooverify hello dosyaları başarıyla karşıya yüklendi.


## <a name="next-steps"></a>Sonraki adımlar
* [Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama](data-lake-store-copy-data-wasb-distcp.md)
