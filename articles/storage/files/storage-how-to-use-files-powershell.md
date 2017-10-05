---
title: "PowerShell kullanarak Azure Dosya depolamayı yönetme | Microsoft Docs"
description: "PowerShell kullanarak Azure Dosya depolamayı yönetmeyi öğrenin."
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
ms.openlocfilehash: ce62d4423ce711a6902aed7b8174ff4e827f6083
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="fe745-103">PowerShell kullanarak Azure Dosya depolamayı yönetme</span><span class="sxs-lookup"><span data-stu-id="fe745-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="fe745-104">Dosya paylaşımları oluşturmak ve yönetmek için Azure PowerShell’i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe745-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="fe745-105">Azure Storage için PowerShell cmdlet’leri yükleme</span><span class="sxs-lookup"><span data-stu-id="fe745-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="fe745-106">PowerShell’i kullanmaya hazırlamak için Azure PowerShell cmdlet’lerini indirin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fe745-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="fe745-107">Yükleme noktası ve yükleme yönergeleri için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="fe745-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="fe745-108">En güncel Azure PowerShell modülünü indirmeniz ve yüklemeniz veya yükseltmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="fe745-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="fe745-109">**Başlat**’a tıklayıp **Windows PowerShell** yazarak Azure PowerShell penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="fe745-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="fe745-110">PowerShell penceresi sizin için Azure Powershell modülünü yükler.</span><span class="sxs-lookup"><span data-stu-id="fe745-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="fe745-111">Depolama hesabınız ve anahtarı için bir bağlam oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe745-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="fe745-112">Depolama hesabı bağlamını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe745-112">Create the storage account context.</span></span> <span data-ttu-id="fe745-113">Bağlam, depolama hesabı adını ve hesap anahtarını kapsar.</span><span class="sxs-lookup"><span data-stu-id="fe745-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="fe745-114">Hesap anahtarını [Azure portalından](https://portal.azure.com) kopyalama yönergeleri için bkz. [Depolama erişim anahtarlarını görüntüleme ve kopyalama](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="fe745-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="fe745-115">`storage-account-name` ve `storage-account-key` değerlerini aşağıdaki örnekte olduğu gibi depolama hesabı adı ve anahtarınız ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe745-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="fe745-116">Yeni dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe745-116">Create a new file share</span></span>
<span data-ttu-id="fe745-117">`logs` adında yeni bir paylaşım oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe745-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="fe745-118">Artık, File Storage’da bir dosya paylaşımınız bulunur.</span><span class="sxs-lookup"><span data-stu-id="fe745-118">You now have a file share in File storage.</span></span> <span data-ttu-id="fe745-119">Şimdi, bir dizin ve dosya ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="fe745-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe745-120">Dosya paylaşımınızın adı küçük harflerden oluşmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe745-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="fe745-121">Dosya paylaşımlarının ve dosyaların adlandırılması hakkında tüm ayrıntılara ulaşmak için bkz. [Paylaşımları, Dizinleri, Dosyaları ve Meta Verileri Adlandırma ve Bunlara Başvuruda Bulunma](https://msdn.microsoft.com/library/azure/dn167011.aspx)</span><span class="sxs-lookup"><span data-stu-id="fe745-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="fe745-122">Dosya paylaşımında bir dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe745-122">Create a directory in the file share</span></span>
<span data-ttu-id="fe745-123">Paylaşımda bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe745-123">Create a directory in the share.</span></span> <span data-ttu-id="fe745-124">Aşağıdaki örnekte, dizin `CustomLogs` olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="fe745-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="fe745-125">Dizine yerel bir dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="fe745-125">Upload a local file to the directory</span></span>
<span data-ttu-id="fe745-126">Şimdi, dizine yerel bir doya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fe745-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="fe745-127">Aşağıdaki örnekte `C:\temp\Log1.txt` konumundan bir dosya yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fe745-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="fe745-128">Dosya yolunu yerel makinenizdeki geçerli bir dosyaya işaret edecek şekilde düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="fe745-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="fe745-129">Dizindeki dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="fe745-129">List the files in the directory</span></span>
<span data-ttu-id="fe745-130">Dizindeki dosyaları görmek üzere tüm dizin dosyalarını listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe745-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="fe745-131">Bu komut, CustomLogs dizinindeki dosyaları ve alt dizinleri (varsa) döndürür.</span><span class="sxs-lookup"><span data-stu-id="fe745-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="fe745-132">Get-AzureStorageFile, hangi dizin nesnesi geçiriliyorsa, onun için dosyaların ve dizinlerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fe745-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="fe745-133">"Get-AzureStorageFile -Share $s" kök dizindeki dosyaların ve dizinlerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fe745-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="fe745-134">Alt dizindeki dosyaların bir listesini almak için alt dizini Get-AzureStorageFile dizinine geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe745-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="fe745-135">Böylece şu işlemleri gerçekleştirmiş olursunuz; komutun kanala kadar olan ilk parçası CustomLogs alt dizininin dizin örneğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fe745-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="fe745-136">Daha sonra, CustomLogs alt dizinindeki dosyaları ve dizinleri döndüren Get-AzureStorageFile dizinine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="fe745-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="fe745-137">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="fe745-137">Copy files</span></span>
<span data-ttu-id="fe745-138">Azure PowerShell’in 0.9.7 sürümünden başlayarak, bir dosyayı başka bir dosyaya, bir dosyayı başka bir bloba veya bir blobu bir dosyaya kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe745-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="fe745-139">Bu kopyalama işlemlerinin PowerShell cmdlet'leri kullanılarak nasıl yapılacağı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fe745-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="fe745-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe745-140">Next steps</span></span>
<span data-ttu-id="fe745-141">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="fe745-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="fe745-142">SSS</span><span class="sxs-lookup"><span data-stu-id="fe745-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="fe745-143">Windows’da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fe745-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="fe745-144">Linux’ta sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fe745-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    