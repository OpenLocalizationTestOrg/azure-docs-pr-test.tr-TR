---
title: aaaUsing hello Azure Storage ile Azure CLI 1.0 | Microsoft Docs
description: "Nasıl toouse Azure komut satırı arabirimi (Azure CLI) 1.0 ile Azure depolama toocreate hello ve depolama hesaplarını yönetme ve Azure BLOB'ları ve dosyalar ile çalışırken öğrenin. platformlar arası aracı Hello Azure CLI değil"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Hello Azure CLI 1.0 Azure Storage ile kullanma

## <a name="overview"></a>Genel Bakış

Hello Azure CLI açık kaynak, bir dizi hello Azure platformu ile çalışmak için platformlar arası komutları sağlar. Aynı işlevselliği bulunan hello hello çoğunu sağlayan [Azure portal](https://portal.azure.com) de gibi zengin veri erişim işlevselliği.

Bu kılavuzda, biz ele alacağız nasıl toouse [Azure komut satırı arabirimi (Azure CLI)](../../cli-install-nodejs.md) tooperform çeşitli Azure Storage ile geliştirme ve yönetim görevleri. İndirin ve yükleyin veya yükseltme toohello öneririz bu kılavuzu kullanmadan önce en son Azure CLI.

Bu kılavuz, Azure Storage hello temel kavramlarını anladığınızı varsayar. Merhaba Kılavuzu bir dizi betiği hello Azure Storage ile Azure CLI toodemonstrate hello kullanımı sağlar. Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre hello betik değişkenlerini emin tooupdate olması.

> [!NOTE]
> Başlangıç Kılavuzu, Klasik depolama hesapları için hello Azure CLI komut ve komut dosyası örnekler verilmektedir. Bkz: [kullanma hello Mac, Linux ve Windows Azure kaynak yönetimi için Azure CLI](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) Resource Manager depolama hesapları için Azure CLI komutları için.
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>5 dakika içinde Azure Storage ve hello Azure CLI kullanmaya başlama
Bu kılavuzda Ubuntu örnekler için kullanılır, ancak diğer işletim sistemi platformlarını benzer şekilde gerçekleştirmeniz gerekir.

**Yeni tooAzure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın. Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).

Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.

**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**

1. Azure CLI hello yönergeleri izleyerek özetlenen hello yükleyip [yükleme hello Azure CLI](../../cli-install-nodejs.md).
2. Hello Azure CLI yüklendikten sonra mümkün toouse olacaktır Merhaba, komut satırı arabirimi (Bash, Terminal, komut istemi) tooaccess hello Azure CLI komutlarının azure komutu. Türü hello _azure_ komut ve çıktı aşağıdaki hello görmeniz gerekir.

    ![Azure komut çıktısı](./media/storage-azure-cli/azure_command.png)   
3. Merhaba komut satırı arabiriminde yazın `azure storage` tüm toolist hello azure depolama komutları ve hello işlevler hello Azure CLI'nin sağladığı bir ilk izlenim alın. Komut adı ile yazabilirsiniz **-h** parametresi (örneğin, `azure storage share create -h`) komut sözdizimi toosee ayrıntıları.
4. Şimdi, biz temel Azure CLI komutları tooaccess Azure Storage gösteren basit bir komut dosyası size. Merhaba komut dosyası ilk tooset iki değişken depolama hesabı ve anahtarı için istenir. Ardından, hello betik bu yeni depolama hesabı yeni bir kapsayıcı oluşturur ve var olan bir görüntü dosyası (blob) toothat kapsayıcıyı karşıya yükleme. Bu kapsayıcıdaki tüm blob'lara Hello komut dosyasını listeler sonra hello yerel bilgisayarda var olan hello görüntü dosyası toohello hedef dizini indirir.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. Yerel bilgisayarınızda, tercih edilen metin düzenleyicisi (örneğin VIM) açın. Betik yukarıdaki Merhaba, metin düzenleyicisi yazın.
6. Şimdi, yapılandırma ayarlarınızı temel alan tooupdate hello komut dosyası değişkenleri gerekir.

   * **< Storage_account_name >** hello komut dosyasında adı verilen hello kullanın veya depolama hesabınız için yeni bir ad girin. **Önemli:** hello depolama hesabının adını hello Azure içinde benzersiz olmalıdır. Çok küçük olmalıdır!
   * **< storage_account_key >** hello erişim anahtarını depolama hesabınızın.
   * **< Container_name >** hello komut dosyasında adı verilen hello kullanın veya, kapsayıcı için yeni bir ad girin.
   * **< İmage_to_upload >** yolu tooa resim, yerel bilgisayarınızda gibi girin: "~ / images/HelloWorld.png".
   * **< Destination_folder >** bir yolu tooa yerel dizin toostore dosyaları Azure Storage'dan gibi indirilen girin: "~/downloadImages".
7. Merhaba gerekli VIM değişkenlerde güncelleştirdikten sonra tuş bileşimlerini basın `ESC`, `:`, `wq!` toosave hello komut dosyası.
8. toorun bu komut, komut dosyası dosya adı hello bash konsolunda türü hello yeterlidir. Bu betik çalıştıktan sonra indirilen hello görüntü dosyasını içeren bir yerel hedef klasör olmalıdır. Merhaba ekran aşağıdaki örnek çıkış şunları gösterir:

Merhaba betik çalıştıktan sonra indirilen hello görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Depolama hesapları hello Azure CLI ile yönetme
### <a name="connect-tooyour-azure-subscription"></a>Tooyour Azure aboneliğine bağlanma
Merhaba depolama komutların çoğu Azure aboneliği çalışır ancak tooconnect tooyour hello Azure CLI abonelikten öneririz. Aboneliğinize tooconfigure hello Azure CLI toowork izleyin hello adımlarda [tooan Azure aboneliği hello Azure CLI ' bağlanma](../../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Yeni depolama hesabı oluşturma
toouse Azure depolama, depolama hesabı gerekir. Bilgisayar tooconnect tooyour aboneliğinizi yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.

```azurecli
azure storage account create <account_name>
```

Depolama hesabınızın adını Hello uzunluğu 3 ile 24 karakter arasında olmalı ve sayı ve yalnızca küçük harf kullanmanız gerekir.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Ortam değişkenleri varsayılan bir Azure depolama hesabı ayarlama
Aboneliğinizde birden çok depolama hesabı olabilir. Bunlardan birini seçin ve tüm hello depolama hello aynı komutları için ortam değişkenlerini hello ayarlama oturumu. Bu komutlar hello depolama belirtmeden hesap ve açıkça anahtar toorun hello Azure CLI depolama sağlar.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Başka bir şekilde tooset varsayılan depolama hesabı bağlantı dizesi kullanıyor. İlk olarak hello bağlantı dizesini komutla alın:

```azurecli
azure storage account connectionstring show <account_name>
```

Merhaba çıkış bağlantı dizesini kopyalayın ve tooenvironment değişkeni ayarlayın:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Oluşturma ve BLOB'ları yönetme
Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir. Bu bölümde, zaten hello Azure Blob Depolama kavramlarına alışık olduğunuz varsayılır. Ayrıntılı bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Bir kapsayıcı oluşturma
Azure depolama her blob bir kapsayıcıda olmalıdır. Hello kullanarak özel bir kapsayıcı oluşturabilirsiniz `azure storage container create` komutu:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**. tooprevent anonim erişim tooblobs, kümesi hello izni parametresi çok**devre dışı**. Varsayılan olarak, hello yeni kapsayıcı özeldir ve yalnızca hello hesap sahibi tarafından erişilebilir. tooallow anonim ortak okuma erişimine tooblob, ancak değil toocontainer meta veriler veya toohello listesi hello kapsayıcıdaki blobları, hello izni çok parametre**Blob**. tooallow tam ortak okuma tooblob kaynaklara erişmesine, kapsayıcı meta verileri ve hello kapsayıcıdaki blobları hello listesi, hello izni çok parametre**kapsayıcı**. Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../blobs/storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
Azure Blob Storage blok blobları ve sayfa bloblarını destekler. Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooa kapsayıcıdaki blobları tooupload, kullanabileceğiniz hello `azure storage blob upload`. Varsayılan olarak, bu komut hello yerel dosyaları tooa blok blobu yükler. toospecify hello türü hello blob için kullanabileceğiniz hello `--blobtype` parametresi.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Kapsayıcıdan BLOB indirmek
Aşağıdaki örnek hello nasıl toodownload kapsayıcıdan BLOB'ların gösterir.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>BLOB kopyalama
Blobları, depolama hesaplarıyla bölgeler içinde veya bunların arasında zaman uyumsuz olarak kopyalayabilirsiniz.

Merhaba aşağıdaki örnekte nasıl tooanother toocopy bloblarından bir depolama hesabı gösterilmiştir. Bu örnekte BLOB'lar nerede genel olarak, bir kapsayıcı oluşturuyoruz anonim olarak erişilebilir.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

Bu örnek bir zaman uyumsuz kopya gerçekleştirir. Merhaba çalıştırarak her kopyalama işlemi hello durumunu izleyebilirsiniz `azure storage blob copy show` işlemi.

Merhaba kopyalama işlemi için sağlanan hello kaynak URL gerekir ya da genel olarak erişilebilir veya bir SAS (paylaşılan erişim imzası) belirteci dahil unutmayın.

### <a name="delete-a-blob"></a>Blob silme
toodelete bir blob hello aşağıdaki komutu kullanın:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Oluşturun ve dosya paylaşımlarını yönetmek
Azure File storage hello standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar. Microsoft Azure sanal makineler ve bulut Hizmetleri yanı sıra, şirket içi uygulamalara bağlı paylaşımlar üzerinden dosya verileri paylaşabilir. Dosya paylaşımları ve dosya verilerini hello Azure CLI aracılığıyla yönetebilirsiniz. Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md) veya [nasıl toouse Linux Azure File storage](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Dosya paylaşımı oluşturma
Bir Azure dosya paylaşımı azure'da SMB dosya paylaşımı değil. Tüm dizin ve dosyaların bir dosya paylaşımı oluşturulmalıdır. Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, toohello kapasite limitlerini hello depolama hesabının sınırsız sayıda depolayabilirsiniz. Merhaba aşağıdaki örnek adlı bir dosya paylaşımı oluşturur **paylaşımım**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Dizin oluşturma
Bir dizin, bir Azure dosya paylaşımı için isteğe bağlı hiyerarşik bir yapı sağlar. Merhaba aşağıdaki örnek adlı bir dizin oluşturur **Dizinim** hello dosya paylaşımında.

```azurecli
azure storage directory create myshare myDir
```

Bu dizin yolu, birden çok düzeyi içerebilir Not *örneğin*, **bir / b**. Ancak, tüm üst dizinleri var olduğundan emin olmalısınız. Örneğin, yol **bir / b**, dizin oluşturmanız gerekir **bir** ilk olarak, ardından dizin oluşturma **b**.

### <a name="upload-a-local-file-toodirectory"></a>Yerel dosya toodirectory karşıya yükle
Merhaba aşağıdaki örnek dosya karşıya yükleme **~/temp/samplefile.txt** toohello **Dizinim** dizin. Merhaba dosya yolu geçerli bir dosya tooa yerel makinenizde işaret şekilde düzenleyin:

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Merhaba paylaşımda bir dosya boyutu too1 TB yukarı olabilir unutmayın.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Merhaba paylaşım kök veya dizinde hello dosyaları listeleme
Merhaba dosyaları ve alt dizinleri paylaşım kök ya da komut aşağıdaki hello kullanarak dizin listeleyebilirsiniz:

```azurecli
azure storage file list myshare myDir
```

Bu hello dizin adı işlemi listeleme hello için isteğe bağlı olduğunu unutmayın. Atlanırsa, hello komutu hello hello paylaşımının hello kök dizinin içeriğini listeler.

### <a name="copy-files"></a>Dosyaları kopyalama
Azure CLI 0.9.8 sürümü ile başlayarak, tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz. Aşağıda nasıl tooperform bu kopyalama göstermek CLI komutları kullanarak işlemleri. toocopy dosya toohello yeni bir dizin:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy bir blob tooa dosyası dizini:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Sonraki Adımlar

Burada depolama kaynaklarla çalışmak için Azure CLI 1.0 komut başvurusu bulabilirsiniz:

* [Kaynak Yöneticisi modunda Azure CLI komutları](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Azure Hizmet Yönetimi modunda Azure CLI komutları](../../cli-install-nodejs.md)

Tootry hello istiyor [Azure CLI 2.0](../storage-azure-cli.md), hello Resource Manager dağıtım modeli ile kullanmak için Python içinde yazılmış bizim nesil CLI.
