---
title: aaaUsing hello Azure Storage ile Azure CLI 2.0 | Microsoft Docs
description: "Nasıl toouse Azure komut satırı arabirimi (Azure CLI) 2.0 ile Azure depolama toocreate hello ve depolama hesaplarını yönetme ve Azure BLOB'ları ve dosyalar ile çalışırken öğrenin. Hello Azure CLI 2.0 Python içinde yazılmış platformlar arası bir araçtır."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Hello Azure CLI 2.0 Azure Storage ile kullanma

Merhaba açık kaynak, platformlar arası Azure CLI 2.0 hello Azure platformu ile çalışmak için bir komut kümesi sağlar. Aynı işlevselliği bulunan hello hello çoğunu sağlayan [Azure portal](https://portal.azure.com), zengin veri erişimi de dahil olmak üzere.

Bu kılavuzda, nasıl gösteriyoruz toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform çeşitli görevleri Azure depolama hesabınızdaki kaynaklara ile çalışma. İndirin ve yükleyin veya bu kılavuzu kullanmadan önce hello CLI 2.0 toohello en son sürümüne yükseltmenizi öneririz.

Başlangıç Kılavuzu'nda Hello örnekler hello Bash kabuğunda Ubuntu üzerinde hello kullanımını varsayar ancak diğer platformlar benzer şekilde gerçekleştirmeniz gerekir. 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuz, Azure Storage hello temel kavramlarını anladığınızı varsayar. Aşağıda Azure ve hello depolama hizmeti için belirtilen mümkün toosatisfy hello hesap oluşturma gerekliliklerini olduğunuzu varsayar.

### <a name="accounts"></a>Hesaplar
* **Azure hesabı**: zaten bir Azure aboneliğiniz yoksa [ücretsiz bir Azure hesabı oluşturma](https://azure.microsoft.com/free/).
* **Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](storage-create-storage-account.md#create-a-storage-account) bölümü.

### <a name="install-hello-azure-cli-20"></a>Hello Azure CLI 2.0 yükleyin

Karşıdan yükleyip hello Azure CLI 2.0 özetlenen hello yönergeleri izleyerek [Azure CLI 2.0 yükleme](/cli/azure/install-az-cli2).

> [!TIP]
> Merhaba yüklemesiyle konusunda sorun yaşıyorsanız, hello denetleyin [yükleme sorunlarını giderme](/cli/azure/install-az-cli2#installation-troubleshooting) hello makale ve hello bölümünü [yükleme sorun giderme](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) github'da Kılavuzu.
>

## <a name="working-with-hello-cli"></a>CLI Hello ile çalışma

Hello CLI yükledikten sonra hello kullanarak `az` , komut satırı arabirimi (Bash, Terminal, komut istemi) tooaccess hello Azure CLI komutlarda komutu. Türü hello `az` komutu toosee hello temel komutları (örnek çıktı aşağıdaki hello kesildi) tam listesi:

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

Komut satırı arabirimi hello bağlamını `az storage --help` toolist hello `storage` alt grupları komutu. Merhaba alt grupları Hello açıklamalarını depolama kaynaklarla çalışmak için Azure CLI sağlar hello işlevselliği hello genel bir bakış sağlar.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Merhaba CLI tooyour Azure aboneliğine bağlanma

toowork hello kaynaklarla, Azure aboneliğinizin ilk oturum açmalısınız tooyour içinde Azure hesabı `az login`. Oturum açabilir birkaç yolu vardır:

* **Etkileşimli oturum açma**:`az login`
* **Kullanıcı adı ve parolayla oturum**:`az login -u johndoe@contoso.com -p VerySecret`
  * Bu, Microsoft hesapları veya çok faktörlü kimlik doğrulamasını kullanan ile çalışmaz.
* **Bir hizmet sorumlusu oturum oturum**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Azure CLI 2.0 örnek komut dosyası

Ardından, biz ile Azure Storage kaynaklarını birkaç temel Azure CLI 2.0 komutları toointeract sorunları küçük Kabuk betiği çalışmak. Merhaba komut dosyası ilk depolama hesabınızı yeni bir kapsayıcı oluşturur ve sonra var olan bir dosya (blob) olarak toothat kapsayıcı yükler. Merhaba kapsayıcıdaki tüm blob'lara listeler ve son olarak, yerel bilgisayarınızda belirttiğiniz hello dosya tooa hedef indirir.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Yapılandırma ve hello komut dosyası çalıştırma**

1. Sık kullandığınız metin düzenleyicisinde açın, sonra kopyalayın ve komut dosyası hello düzenleyicisine önceki hello yapıştırın.

2. Ardından, hello komut dosyanızın değişken tooreflect yapılandırma ayarlarınızı güncelleştirin. Belirtilen değerler aşağıdaki hello değiştirin:

   * **\<storage_account_name\>**  hello depolama hesabınızın adını.
   * **\<storage_account_key\>**  hello birincil veya ikincil erişim anahtarını depolama hesabınız için.
   * **\<container_name\>**  bir ad hello "azure-CLI-örnek-container" gibi yeni kapsayıcı toocreate.
   * **\<blob_name\>**  hello kapsayıcısında hello hedef blob için bir ad.
   * **\<file_to_upload\>**  yol toosmall dosyası yerel bilgisayarınızda gibi hello "~ / images/HelloWorld.png".
   * **\<destination_file\>**  hedef dosya yolu gibi hello "~ / downloadedImage.png".

3. Merhaba gerekli değişkenleri güncelleştirdikten sonra hello komut dosyasını kaydedin ve düzenleyicinizi çıkın. Merhaba sonraki adımlar varsayın kodunuzu adlı **my_storage_sample.sh**.

4. Merhaba komut dosyası yürütülebilir, olarak gerekiyorsa işaretleyin:`chmod +x my_storage_sample.sh`

5. Merhaba betiğini yürütün. Örneğin, Bash içinde:`./my_storage_sample.sh`

Çıktı benzer toohello aşağıdakilere bakın ve hello gerekir  **\<destination_file\>**  hello belirtilen komut dosyası yerel bilgisayarınızda görünmelidir.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Merhaba önceki çıktı olarak **tablo** biçimi. Hangi hello belirterek biçimi toouse çıktı belirtebilirsiniz `--output` CLI komutlarınızı değişkeninde veya genel kullanarak ayarlayın `az configure`.
>

## <a name="manage-storage-accounts"></a>Depolama hesaplarını yönetme

### <a name="create-a-new-storage-account"></a>Yeni depolama hesabı oluşturma
toouse Azure depolama, depolama hesabınızın olması gerekir. Bilgisayarınızı çok yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz[tooyour abonelik bağlanmak](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location`[Gerekli]: konum. Örneğin, "Batı ABD".
* `--name`[Gerekli]: hello depolama hesabı adı. Merhaba adı 3 too24 karakterden oluşmalı ve yalnızca küçük harf alfasayısal karakterler kullanın.
* `--resource-group`[Gerekli]: kaynak grubunun adı.
* `--sku`[Gerekli]: depolama hesabı SKU hello. İzin verilen değerler:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Varsayılan Azure depolama hesabı ortam değişkenlerini ayarlama
Azure aboneliğinizde birden çok depolama hesabı olabilir. bunlardan birini tooselect tüm sonraki depolama toouse komutlar, bu ortam değişkenleri ayarlayabilirsiniz:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Başka bir şekilde tooset varsayılan depolama hesabı bağlantı dizesi kullanmaktır. İlk olarak, hello hello bağlantı dizesi alma `show-connection-string` komutu:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Ardından kopya hello çıkış bağlantı dizesi ve ayarlama hello `AZURE_STORAGE_CONNECTION_STRING` ortam değişkeni (tooenclose hello bağlantı dizesi tırnak gerekebilir):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Aşağıdaki bölümlerde, bu makalenin hello tüm örneklerde hello ayarladığınızdan varsayın `AZURE_STORAGE_ACCOUNT` ve `AZURE_STORAGE_ACCESS_KEY` ortam değişkenleri.
>

## <a name="create-and-manage-blobs"></a>Oluşturma ve BLOB'ları yönetme
Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir. Bu bölümde, zaten Azure Blob Depolama kavramlarına alışık olduğunuz varsayılır. Ayrıntılı bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Bir kapsayıcı oluşturma
Azure depolama her blob bir kapsayıcıda olmalıdır. Hello kullanarak bir kapsayıcı oluşturabilirsiniz `az storage container create` komutu:

```azurecli
az storage container create --name <container_name>
```

İsteğe bağlı hello belirterek üç düzeyinden birini okuma erişimi için yeni bir kapsayıcı ayarlayabilirsiniz `--public-access` bağımsız değişkeni:

* `off`(varsayılan): kapsayıcı verileri, özel toohello hesap sahibi.
* `blob`: BLOB'lar ortak okuma erişimi.
* `container`: Ortak okuma ve liste toohello tüm kapsayıcı erişin.

Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../blobs/storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Bir blob tooa kapsayıcı karşıya yükle
Azure Blob storage blok destekler, ekleme ve sayfa BLOB'ları. Karşıya yükleme BLOB'ların tooa kapsayıcı hello kullanarak `blob upload` komutu:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Varsayılan olarak, hello `blob upload` komutu *.vhd dosyaları toopage BLOB veya blok blobları aksi yükler. toospecify başka türü bir blob karşıya yükleme, hello kullanabilirsiniz `--type` izin verilen değerler bağımsız değişken-- `append`, `block`, ve `page`.

 Merhaba farklı blob türleri hakkında daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Kapsayıcıdan blob indirme
Bu örnekte gösterilmiştir nasıl toodownload bir kapsayıcı blobundan:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda

Liste hello BLOB'ları bir kapsayıcıda hello ile [az depolama blob listesi](/cli/azure/storage/blob#list) komutu.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>BLOB kopyalama
Blobları, depolama hesaplarıyla bölgeler içinde veya bunların arasında zaman uyumsuz olarak kopyalayabilirsiniz.

Merhaba aşağıdaki örnekte nasıl tooanother toocopy bloblarından bir depolama hesabı gösterilmiştir. İlk olarak bir kapsayıcı hello kaynak depolama hesabında kendi BLOB'lar için herkese okuma erişimi belirtme oluşturuyoruz. Ardından, biz bir dosya toohello kapsayıcısı ve son olarak, bu kapsayıcısından kopyalama hello blob bir kapsayıcıda hello hedef depolama hesabının içine karşıya yükleyin.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

Yukarıdaki örnek Hello hello Hedef kapsayıcıyı hello hedef depolama hesabındaki hello kopyalama işlemi toosucceed için varolmalıdır. Ayrıca, hello kaynak blob Hello belirtilen `--source-uri` bağımsız değişkeni bir paylaşılan erişim imzası (SAS) belirteci eklemek veya bu örnekte olduğu gibi genel olarak erişilebilir.

### <a name="delete-a-blob"></a>Blob silme
toodelete bir blob kullanmak hello `blob delete` komutu:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Oluşturun ve dosya paylaşımlarını yönetmek
Azure File storage hello sunucu ileti bloğu (SMB) protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar. Microsoft Azure sanal makineler ve bulut Hizmetleri yanı sıra, şirket içi uygulamalara bağlı paylaşımlar üzerinden dosya verileri paylaşabilir. Dosya paylaşımları ve dosya verilerini hello Azure CLI aracılığıyla yönetebilirsiniz. Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md) veya [nasıl toouse Linux Azure File storage](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Dosya paylaşımı oluşturma
Bir Azure dosya paylaşımı azure'da SMB dosya paylaşımı değil. Tüm dizin ve dosyaların bir dosya paylaşımı oluşturulmalıdır. Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, toohello kapasite limitlerini hello depolama hesabının sınırsız sayıda depolayabilirsiniz. Merhaba aşağıdaki örnek adlı bir dosya paylaşımı oluşturur **paylaşımım**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Dizin oluşturma
Bir dizin Azure dosya paylaşımının hiyerarşik yapıda sağlar. Merhaba aşağıdaki örnek adlı bir dizin oluşturur **Dizinim** hello dosya paylaşımında.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Bir dizin yolu birden çok düzeyi, örneğin içerebilir **dizin1/dir2**. Ancak, tüm üst dizinleri bir alt dizin oluşturmadan önce mevcut olduğundan emin olmalısınız. Örneğin, yol **dizin1/dir2**, dizin oluşturmak **dizin1**, dizin oluşturma **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Bir yerel dosya tooa paylaşımı karşıya yükle
Merhaba aşağıdaki örnek dosya karşıya yükleme **~/temp/samplefile.txt** hello tooroot **paylaşımım** dosya paylaşımı. Merhaba `--source` bağımsız değişkeni hello var olan yerel dosya tooupload belirtir.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Dizin oluşturma gibi ile Merhaba paylaşımı tooupload hello dosya tooan var olan dizini içindeki hello paylaşımı içinde bir dizin yolu belirtebilirsiniz:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Merhaba paylaşımda bir dosya boyutu too1 TB yukarı olabilir.

### <a name="list-hello-files-in-a-share"></a>Bir paylaşımda hello dosyaları listeleme
Hello kullanarak dosyaları ve dizinleri bir paylaşımda listeleyebilirsiniz `az storage file list` komutu:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Dosyaları kopyalama      
Tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz. Örneğin, farklı bir paylaşım dosya tooa dizininde toocopy:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Sonraki adımlar
Azure CLI 2.0 hello ile çalışma hakkında daha fazla bilgi edinmek için bazı ek kaynaklar aşağıda verilmiştir.

* [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure CLI 2.0 komut başvurusu](/cli/azure)
* [Github'daki Azure CLI 2.0](https://github.com/Azure/azure-cli)
