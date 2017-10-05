---
title: "Azure Dosya Paylaşımı oluşturma | Microsoft Docs"
description: "Azure portal, PowerShell ve Azure CLI kullanarak Azure Dosya depolamada bir Azure dosya paylaşımı nasıl oluşturulur?"
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
ms.openlocfilehash: 10da4d903eaab290a6cca2c4f674548a43a70c53
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="1cebd-103">Azure Dosya depolamada bir Dosya Paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="1cebd-104">[Azure portalını](https://portal.azure.com/), Azure Depolama PowerShell cmdlet’lerini, Azure Depolama istemci kitaplıklarını veya Azure Depolama REST API’sini kullanarak Azure dosya paylaşımları oluşturabilirsiniz. Bu öğreticide şunlar gösterilecek:</span><span class="sxs-lookup"><span data-stu-id="1cebd-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="1cebd-105">Azure portalını kullanarak Azure Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-105">How to create an Azure File share using the Azure portal</span></span>](#Create file share through the Portal)
* [<span data-ttu-id="1cebd-106">PowerShell kullanarak Azure Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-106">How to create an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="1cebd-107">CLI kullanarak Azure Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-107">How to create an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="1cebd-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1cebd-108">Prerequisites</span></span>
<span data-ttu-id="1cebd-109">Azure Dosya paylaşımı oluşturmak için zaten var olan bir depolama hesabı kullanabilir veya [yeni bir Azure depolama hesabı oluşturabilirsiniz](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1cebd-109">To create an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="1cebd-110">PowerShell ile Azure Dosya paylaşımı oluşturmak için depolama hesabınızın hesap anahtarı ve adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cebd-110">To create an Azure File share with PowerShell, you will need the account key and name of your storage account..</span></span> <span data-ttu-id="1cebd-111">PowerShell veya CLI kullanmayı planlıyorsanız Depolama hesabının anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cebd-111">You will need Storage account key if you plan to use Powershell or CLI.</span></span>

## <a name="create-file-share-through-the-portal"></a><span data-ttu-id="1cebd-112">Portal üzerinden dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-112">Create file share through the Portal</span></span>
1. <span data-ttu-id="1cebd-113">**Azure Portal’ındaki Depolama Hesabı dikey penceresine gidin**:</span><span class="sxs-lookup"><span data-stu-id="1cebd-113">**Go to Storage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="1cebd-114">![Depolama Hesabı Dikey Penceresi](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="1cebd-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="1cebd-115">**Dosya Paylaşımı ekleme düğmesine tıklayın**:</span><span class="sxs-lookup"><span data-stu-id="1cebd-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="1cebd-116">![Dosya Paylaşımı ekleme düğmesine tıklayın](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="1cebd-116">![Click the add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="1cebd-117">**Ad ve Kota belirtin. Kota şu an en çok 5 TB olabilir**:</span><span class="sxs-lookup"><span data-stu-id="1cebd-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="1cebd-118">![Yeni dosya paylaşımı için ad ve istenen kotayı sağlayın](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="1cebd-118">![Provide a name and a desired quota for the new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="1cebd-119">**Yeni dosya paylaşımınızı görüntüleyin**: ![Yeni dosya paylaşımınızı görüntüleyin](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="1cebd-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="1cebd-120">**Dosyayı karşıya yükleyin**: ![Dosyayı karşıya yükleyin](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="1cebd-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="1cebd-121">**Dosya paylaşımınıza göz atın ve dizinlerinizle dosyalarınız yönetin**: ![Dosya paylaşımına göz atın](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="1cebd-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="1cebd-122">PowerShell üzerinden dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-122">Create file share through PowerShell</span></span>
<span data-ttu-id="1cebd-123">PowerShell’i kullanmaya hazırlamak için Azure PowerShell cmdlet’lerini indirin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1cebd-123">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="1cebd-124">Yükleme noktası ve yükleme yönergeleri için bkz. [Azure PowerShell’i yükleme ve yapılandırma](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="1cebd-124">See [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for the install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="1cebd-125">En güncel Azure PowerShell modülünü indirmeniz ve yüklemeniz veya yükseltmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="1cebd-125">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="1cebd-126">**Depolama hesabınız ve anahtarınız için bir bağlam oluşturun** Bağlam, depolama hesabı adını ve hesap anahtarını kapsar.</span><span class="sxs-lookup"><span data-stu-id="1cebd-126">**Create a context for your storage account and key** The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="1cebd-127">Hesap anahtarını [Azure portalından](https://portal.azure.com/) kopyalama yönergeleri için bkz. [Depolama erişim anahtarlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="1cebd-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="1cebd-128">**Yeni dosya paylaşımını oluşturun**:</span><span class="sxs-lookup"><span data-stu-id="1cebd-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="1cebd-129">Dosya paylaşımınızın adı küçük harflerden oluşmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1cebd-129">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="1cebd-130">Dosya paylaşımlarının ve dosyaların adlandırılması hakkında tüm ayrıntılara ulaşmak için bkz. [Paylaşımları, Dizinleri, Dosyaları ve Meta Verileri Adlandırma ve Bunlara Başvuruda Bulunma](https://msdn.microsoft.com/library/azure/dn167011.aspx)</span><span class="sxs-lookup"><span data-stu-id="1cebd-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="1cebd-131">Komut Satırı Arabirimi (CLI) üzerinden dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cebd-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="1cebd-132">**Komut Satırı Arabirimi (CLI) kullanmaya hazırlanmak için Azure CLI’yi indirin ve yükleyin.**</span><span class="sxs-lookup"><span data-stu-id="1cebd-132">**To prepare to use a Command Line Interface (CLI), download and install the Azure CLI.**</span></span>  
    <span data-ttu-id="1cebd-133">Bkz. [Azure CLI 2.0’ı yükleme](/cli/azure/install-az-cli2.md) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1cebd-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="1cebd-134">**Paylaşımı oluşturmak istediğiniz depolama hesabına bir bağlantı dizesi oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="1cebd-134">**Create a connection string to the storage account where you want to create the share.**</span></span>  
    <span data-ttu-id="1cebd-135">```<storage-account>``` ve ```<resource_group>``` değerlerini aşağıdaki örnekte olduğu gibi depolama hesabı adı ve kaynak grubuyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1cebd-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in the following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. <span data-ttu-id="1cebd-136">**Dosya paylaşımı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="1cebd-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="1cebd-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1cebd-137">Next steps</span></span>
* [<span data-ttu-id="1cebd-138">Dosya Paylaşımını Bağlama - Windows</span><span class="sxs-lookup"><span data-stu-id="1cebd-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="1cebd-139">Dosya Paylaşımını Bağlama - Linux</span><span class="sxs-lookup"><span data-stu-id="1cebd-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="1cebd-140">Dosya Paylaşımını Bağlama - macOS</span><span class="sxs-lookup"><span data-stu-id="1cebd-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="1cebd-141">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="1cebd-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="1cebd-142">SSS</span><span class="sxs-lookup"><span data-stu-id="1cebd-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="1cebd-143">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="1cebd-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)