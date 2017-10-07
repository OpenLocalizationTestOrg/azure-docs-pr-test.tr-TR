---
title: "bir Azure dosya paylaşımı aaaHow toocreate | Microsoft Docs"
description: "Nasıl toocreate bir Azure dosya paylaşımı Azure dosya depolama hello Azure portal, PowerShell ve hello Azure CLI kullanma."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Azure Dosya depolamada bir Dosya Paylaşımı oluşturma
Kullanarak Azure dosya paylaşımları oluşturabilirsiniz [Azure portal](https://portal.azure.com/), Azure Storage PowerShell cmdlet'lerini Merhaba, hello Azure Storage istemcisi kitaplıklarını veya Azure Storage REST API'sini hello. Bu öğreticide şunları öğreneceksiniz:
* [Nasıl toocreate bir Azure dosya paylaşımı hello Azure portal kullanarak](#Create file share through hello Portal)
* [Nasıl toocreate bir Azure dosya paylaşımı PowerShell'i kullanma](#Create file share using PowerShell)
* [Nasıl toocreate bir Azure dosya paylaşımı CLI kullanma](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Ön koşullar
bir Azure dosya paylaşımı toocreate, zaten varolan bir depolama hesabı kullanabilir veya [yeni bir Azure depolama hesabı oluşturma](storage-create-storage-account.md). toocreate PowerShell ile Azure dosya paylaşımı, hello hesap anahtarı ve depolama hesabınızın adını gerekir... Powershell veya CLI toouse düşünüyorsanız, depolama hesabı anahtarı gerekir.

## <a name="create-file-share-through-hello-portal"></a>Merhaba Portal aracılığıyla dosya paylaşımı oluşturma
1. **Azure Portal gidin tooStorage hesabı dikey penceresinde**:    
    ![Depolama Hesabı Dikey Penceresi](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **Dosya Paylaşımı ekleme düğmesine tıklayın**:    
    ![Merhaba tıklatın dosya paylaşım düğmesi ekleme](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **Ad ve Kota belirtin. Kota şu an en çok 5 TB olabilir**:    
    ![Merhaba yeni dosya paylaşımı için bir ad ve istenen bir kota belirtin](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **Yeni dosya paylaşımınızı görüntüleyin**: ![Yeni dosya paylaşımınızı görüntüleyin](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **Dosyayı karşıya yükleyin**: ![Dosyayı karşıya yükleyin](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **Dosya paylaşımınıza göz atın ve dizinlerinizle dosyalarınız yönetin**: ![Dosya paylaşımına göz atın](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>PowerShell üzerinden dosya paylaşımı oluşturma
tooprepare toouse PowerShell, indirin ve hello Azure PowerShell cmdlet'lerini yükleyin. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) noktası ve yükleme yönergeleri için hello yükleyin.

> [!Note]  
> Bu, indirin ve yükleyin veya toohello en son Azure PowerShell modülü yükseltme önerilir.

1. **Depolama hesabı ve anahtarı için bir bağlam oluşturma** hello bağlam Merhaba, depolama hesabı adı ve hesap anahtarını kapsar. Hesap anahtarını [Azure portalından](https://portal.azure.com/) kopyalama yönergeleri için bkz. [Depolama erişim anahtarlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Yeni dosya paylaşımını oluşturun**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> Merhaba, dosya paylaşımının adını tamamen küçük harfli olması gerekir. Dosya paylaşımlarının ve dosyaların adlandırılması hakkında tüm ayrıntılara ulaşmak için bkz. [Paylaşımları, Dizinleri, Dosyaları ve Meta Verileri Adlandırma ve Bunlara Başvuruda Bulunma](https://msdn.microsoft.com/library/azure/dn167011.aspx)

## <a name="create-file-share-through-command-line-interface-cli"></a>Komut Satırı Arabirimi (CLI) üzerinden dosya paylaşımı oluşturma
1. **tooprepare toouse bir komut satırı arabirimi (CLI), indirin ve hello Azure CLI yükleyin.**  
    Bkz. [Azure CLI 2.0’ı yükleme](/cli/azure/install-az-cli2.md) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md).

2. **Toocreate hello paylaşımı istediğiniz bir bağlantı dizesi toohello depolama hesabı oluşturun.**  
    Değiştir ```<storage-account>``` ve ```<resource_group>``` depolama hesabı adı ve kaynak grubunuzdaki hello aşağıdaki örneğine sahip.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Dosya paylaşımı oluşturma**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Sonraki adımlar
* [Dosya Paylaşımını Bağlama - Windows](storage-file-how-to-use-files-windows.md)
* [Dosya Paylaşımını Bağlama - Linux](storage-how-to-use-files-linux.md)
* [Dosya Paylaşımını Bağlama - macOS](storage-file-how-to-use-files-mac.md)

Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

* [SSS](storage-files-faq.md)
* [Sorun giderme](storage-troubleshoot-file-connection-problems.md)