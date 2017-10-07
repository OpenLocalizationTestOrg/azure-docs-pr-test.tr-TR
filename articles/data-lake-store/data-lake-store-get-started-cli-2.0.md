---
title: "Azure komut satırı 2.0 aaaUse arabirimi tooget Azure Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Temel işlemleri gerçekleştirmek ve Azure platformlar arası komut satırı 2.0 toocreate bir Data Lake Store hesabı kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Azure CLI 2.0 kullanarak Azure Data Lake Store ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Bir Azure Data Lake toouse Azure CLI 2.0 toocreate nasıl depolamak öğrenin hesap ve gibi klasör oluşturma karşıya yükleme ve veri dosyalarını indirme temel işlemleri gerçekleştirmek, vb., hesabınızı silme. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).

Hello Azure CLI 2.0 Azure kaynaklarını yönetmek için Azure'nın yeni komut satırı deneyimidir. MacOS, Linux ve Windows’da kullanılabilir. Daha fazla bilgi edinmek için bkz. [Azure CLI 2.0 aracına genel bakış](https://docs.microsoft.com/cli/azure/overview). Hello de bakabilirsiniz [Azure Data Lake deposu CLI 2.0 başvurusu](https://docs.microsoft.com/cli/azure/dls) komutlar ve söz dizimi tam bir listesi.


## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

* **Azure CLI 2.0** - Yönergeler için kz. [Azure CLI 2.0 aracını yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="authentication"></a>Kimlik Doğrulaması

Bu makalede Data Lake Store için son kullanıcı olarak oturum açtığınız daha basit bir kimlik doğrulama yaklaşımı kullanılmaktadır. Merhaba erişim düzeyi tooData Lake Store hesabı ve dosya sistemi, kullanıcı oturum hello hello erişim düzeyi sonra tabidir. Ancak, diğer yaklaşım vardır Data Lake Store ile iyi tooauthenticate olarak olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Azure aboneliği tooyour oturum

1. Azure aboneliğinizde oturum açın.

    ```azurecli
    az login
    ```

    Kod toouse hello sonraki adımda alın. Bir web tarayıcısı tooopen hello sayfa https://aka.ms/devicelogin kullanın ve hello kod tooauthenticate girin. Kimlik bilgilerinizi kullanarak istendiğinde toolog var.

2. Oturum açtığında hello pencere listeleri tüm hesabınızla ilişkilendirilen Azure aboneliklerinin hello. Komut toouse belirli bir aboneliği aşağıdaki hello kullanın.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Azure Data Lake Store hesabı oluşturma

1. Yeni bir kaynak grubu oluşturun. Komutu aşağıdaki hello hello toouse istediğiniz parametre değerlerini sağlayın. Merhaba konum adı boşluk içeriyorsa, tırnak işaretleri içine alın. Örneğin, "Doğu ABD 2". 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Merhaba Data Lake Store hesabı oluşturun.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Data Lake Store hesabında klasör oluşturma

Azure Data Lake Store hesabı toomanage altında klasörleri oluşturun ve veri depolayın. Adlı bir klasör komutu toocreate aşağıdaki kullanım hello **mynewfolder** hello Data Lake Store hello kökü.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Merhaba `--folder` parametre sağlar hello komutu bir klasör oluşturur. Bu parametre mevcut değilse hello komut hello hello Data Lake Store hesabı kökünde mynewfolder adlı boş bir dosya oluşturur.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Veri tooa Data Lake Store hesabı karşıya yükle

Veri tooData Lake deposu hello hesap içinde oluşturduğunuz doğrudan hello kök düzeyinde veya tooa klasöründe karşıya yükleyebilirsiniz. Merhaba parçacıkları göstermek nasıl tooupload bazı örnek veri toohello klasörü (**mynewfolder**) hello önceki bölümde oluşturduğunuz.

Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Merhaba dosyasını indirin ve C:\sampledata\ gibi bilgisayarınızdaki yerel bir klasörde saklayın.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Merhaba hedef için hello dosya adını içeren hello tam yolunu belirtmeniz gerekir.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Data Lake Store hesabındaki dosyaları listeleme

Aşağıdaki komut toolist hello dosyaları bir Data Lake Store hesabındaki hello kullanın.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

Merhaba çıktısını benzer toohello aşağıdaki gibi olmalıdır:

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Data Lake Store hesabındaki verileri yeniden adlandırma, indirme ve silme 

* **bir dosya toorename**, komutu aşağıdaki hello kullanın:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **bir dosya toodownload**, komutu aşağıdaki hello kullanın. Önceden belirttiğiniz hello hedef yolu var olduğundan emin olun.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > henüz yoksa hello komut hello hedef klasörü oluşturur.
    > 
    >

* **bir dosya toodelete**, komutu aşağıdaki hello kullanın:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Toodelete hello klasörünün istiyorsanız **mynewfolder** ve hello dosya **vehicle1_09142014_copy.csv** birlikte bir komut kullanın hello--parametre recurse

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Data Lake Store hesabı için izin ve ACL’ler ile çalışma

Bu bölümde hakkında bilgi edinin toomanage ACL'ler Azure CLI 2.0 kullanarak ve izinleri. Azure Data Lake Store’da ACL’lerin nasıl uygulandığıyla ilgili ayrıntılı bir tartışma için bkz. [Azure Data Lake Store’da erişim denetimi](data-lake-store-access-control.md).

* **bir dosya/klasör tooupdate hello sahibi**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **tooupdate hello dosya/klasör izinlerini**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **belirli bir yol için tooget hello ACL'ler**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    Merhaba çıkış benzer toohello aşağıdaki gibi olmalıdır:

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **tooset bir ACL için bir giriş**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **tooremove bir ACL için bir giriş**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **tooremove tüm bir varsayılan ACL**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **Tüm varsayılan olmayan ACL tooremove**, komutu aşağıdaki hello kullanın:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Data Lake Store hesabını silme
Komut toodelete bir Data Lake Store hesabı aşağıdaki hello kullanın.

```azurecli
az dls account delete --account mydatalakestore
```

İstendiğinde, girin **Y** toodelete hello hesabı.

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Data Lake Store CLI 2.0 başvurusu](https://docs.microsoft.com/cli/azure/dls)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
