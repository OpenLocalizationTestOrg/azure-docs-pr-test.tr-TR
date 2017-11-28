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
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="cbf7a-103">Azure Dosya depolamada bir Dosya Paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbf7a-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="cbf7a-104">Kullanarak Azure dosya paylaşımları oluşturabilirsiniz [Azure portal](https://portal.azure.com/), Azure Storage PowerShell cmdlet'lerini Merhaba, hello Azure Storage istemcisi kitaplıklarını veya Azure Storage REST API'sini hello. Bu öğreticide şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="cbf7a-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="cbf7a-105">Nasıl toocreate bir Azure dosya paylaşımı hello Azure portal kullanarak</span><span class="sxs-lookup"><span data-stu-id="cbf7a-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="cbf7a-106">Nasıl toocreate bir Azure dosya paylaşımı PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="cbf7a-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="cbf7a-107">Nasıl toocreate bir Azure dosya paylaşımı CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="cbf7a-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="cbf7a-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cbf7a-108">Prerequisites</span></span>
<span data-ttu-id="cbf7a-109">bir Azure dosya paylaşımı toocreate, zaten varolan bir depolama hesabı kullanabilir veya [yeni bir Azure depolama hesabı oluşturma](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbf7a-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="cbf7a-110">toocreate PowerShell ile Azure dosya paylaşımı, hello hesap anahtarı ve depolama hesabınızın adını gerekir...</span><span class="sxs-lookup"><span data-stu-id="cbf7a-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="cbf7a-111">Powershell veya CLI toouse düşünüyorsanız, depolama hesabı anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="cbf7a-112">Merhaba Portal aracılığıyla dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbf7a-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="cbf7a-113">**Azure Portal gidin tooStorage hesabı dikey penceresinde**:</span><span class="sxs-lookup"><span data-stu-id="cbf7a-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="cbf7a-114">![Depolama Hesabı Dikey Penceresi](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="cbf7a-115">**Dosya Paylaşımı ekleme düğmesine tıklayın**:</span><span class="sxs-lookup"><span data-stu-id="cbf7a-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="cbf7a-116">![Merhaba tıklatın dosya paylaşım düğmesi ekleme](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="cbf7a-117">**Ad ve Kota belirtin. Kota şu an en çok 5 TB olabilir**:</span><span class="sxs-lookup"><span data-stu-id="cbf7a-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="cbf7a-118">![Merhaba yeni dosya paylaşımı için bir ad ve istenen bir kota belirtin](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="cbf7a-119">**Yeni dosya paylaşımınızı görüntüleyin**: ![Yeni dosya paylaşımınızı görüntüleyin](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="cbf7a-120">**Dosyayı karşıya yükleyin**: ![Dosyayı karşıya yükleyin](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="cbf7a-121">**Dosya paylaşımınıza göz atın ve dizinlerinizle dosyalarınız yönetin**: ![Dosya paylaşımına göz atın](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="cbf7a-122">PowerShell üzerinden dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbf7a-122">Create file share through PowerShell</span></span>
<span data-ttu-id="cbf7a-123">tooprepare toouse PowerShell, indirin ve hello Azure PowerShell cmdlet'lerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="cbf7a-124">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) noktası ve yükleme yönergeleri için hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="cbf7a-125">Bu, indirin ve yükleyin veya toohello en son Azure PowerShell modülü yükseltme önerilir.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="cbf7a-126">**Depolama hesabı ve anahtarı için bir bağlam oluşturma** hello bağlam Merhaba, depolama hesabı adı ve hesap anahtarını kapsar.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="cbf7a-127">Hesap anahtarını [Azure portalından](https://portal.azure.com/) kopyalama yönergeleri için bkz. [Depolama erişim anahtarlarını görüntüleme ve kopyalama](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cbf7a-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="cbf7a-128">**Yeni dosya paylaşımını oluşturun**:</span><span class="sxs-lookup"><span data-stu-id="cbf7a-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="cbf7a-129">Merhaba, dosya paylaşımının adını tamamen küçük harfli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="cbf7a-130">Dosya paylaşımlarının ve dosyaların adlandırılması hakkında tüm ayrıntılara ulaşmak için bkz. [Paylaşımları, Dizinleri, Dosyaları ve Meta Verileri Adlandırma ve Bunlara Başvuruda Bulunma](https://msdn.microsoft.com/library/azure/dn167011.aspx)</span><span class="sxs-lookup"><span data-stu-id="cbf7a-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="cbf7a-131">Komut Satırı Arabirimi (CLI) üzerinden dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbf7a-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="cbf7a-132">**tooprepare toouse bir komut satırı arabirimi (CLI), indirin ve hello Azure CLI yükleyin.**</span><span class="sxs-lookup"><span data-stu-id="cbf7a-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="cbf7a-133">Bkz. [Azure CLI 2.0’ı yükleme](/cli/azure/install-az-cli2.md) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cbf7a-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="cbf7a-134">**Toocreate hello paylaşımı istediğiniz bir bağlantı dizesi toohello depolama hesabı oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="cbf7a-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="cbf7a-135">Değiştir ```<storage-account>``` ve ```<resource_group>``` depolama hesabı adı ve kaynak grubunuzdaki hello aşağıdaki örneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="cbf7a-136">**Dosya paylaşımı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="cbf7a-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="cbf7a-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbf7a-137">Next steps</span></span>
* [<span data-ttu-id="cbf7a-138">Dosya Paylaşımını Bağlama - Windows</span><span class="sxs-lookup"><span data-stu-id="cbf7a-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="cbf7a-139">Dosya Paylaşımını Bağlama - Linux</span><span class="sxs-lookup"><span data-stu-id="cbf7a-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="cbf7a-140">Dosya Paylaşımını Bağlama - macOS</span><span class="sxs-lookup"><span data-stu-id="cbf7a-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="cbf7a-141">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="cbf7a-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="cbf7a-142">SSS</span><span class="sxs-lookup"><span data-stu-id="cbf7a-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="cbf7a-143">Windows’da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="cbf7a-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="cbf7a-144">Linux’ta sorun giderme</span><span class="sxs-lookup"><span data-stu-id="cbf7a-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   