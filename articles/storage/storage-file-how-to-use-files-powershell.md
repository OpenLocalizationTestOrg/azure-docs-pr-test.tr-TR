---
title: aaaHow toouse PowerShell toomanage Azure File storage | Microsoft Docs
description: "Toouse PowerShell toomanage Azure File storage öğrenin."
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
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="2334e-103">Nasıl toouse PowerShell toomanage Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="2334e-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="2334e-104">Azure PowerShell toocreate ve dosya paylaşımlarını yönetmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2334e-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="2334e-105">Azure Storage için Hello PowerShell cmdlet'lerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="2334e-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="2334e-106">tooprepare toouse PowerShell, indirin ve hello Azure PowerShell cmdlet'lerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2334e-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2334e-107">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs) noktası ve yükleme yönergeleri için hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2334e-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="2334e-108">Bu, indirin ve yükleyin veya toohello en son Azure PowerShell modülü yükseltme önerilir.</span><span class="sxs-lookup"><span data-stu-id="2334e-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="2334e-109">**Başlat**’a tıklayıp **Windows PowerShell** yazarak Azure PowerShell penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="2334e-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="2334e-110">Merhaba PowerShell penceresinde hello Azure Powershell modülü sizin yerinize yükler.</span><span class="sxs-lookup"><span data-stu-id="2334e-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="2334e-111">Depolama hesabınız ve anahtarı için bir bağlam oluşturma</span><span class="sxs-lookup"><span data-stu-id="2334e-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="2334e-112">Merhaba depolama hesabı bağlamını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2334e-112">Create hello storage account context.</span></span> <span data-ttu-id="2334e-113">Merhaba bağlam Merhaba, depolama hesabı adı ve hesap anahtarını kapsar.</span><span class="sxs-lookup"><span data-stu-id="2334e-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="2334e-114">Hesap anahtarınızı hello kopyalama yönergeleri için [Azure portal](https://portal.azure.com), bkz: [depolama erişim tuşlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="2334e-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="2334e-115">Değiştir `storage-account-name` ve `storage-account-key` depolama hesabı adı ve örnek aşağıdaki hello anahtarında ile.</span><span class="sxs-lookup"><span data-stu-id="2334e-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="2334e-116">Yeni dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2334e-116">Create a new file share</span></span>
<span data-ttu-id="2334e-117">Adlı hello yeni paylaşım oluşturun `logs`.</span><span class="sxs-lookup"><span data-stu-id="2334e-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="2334e-118">Artık, File Storage’da bir dosya paylaşımınız bulunur.</span><span class="sxs-lookup"><span data-stu-id="2334e-118">You now have a file share in File storage.</span></span> <span data-ttu-id="2334e-119">Şimdi, bir dizin ve dosya ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="2334e-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2334e-120">Merhaba, dosya paylaşımının adını tamamen küçük harfli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2334e-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="2334e-121">Dosya paylaşımlarının ve dosyaların adlandırılması hakkında tüm ayrıntılara ulaşmak için bkz. [Paylaşımları, Dizinleri, Dosyaları ve Meta Verileri Adlandırma ve Bunlara Başvuruda Bulunma](https://msdn.microsoft.com/library/azure/dn167011.aspx)</span><span class="sxs-lookup"><span data-stu-id="2334e-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="2334e-122">Merhaba dosya paylaşımında bir dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="2334e-122">Create a directory in hello file share</span></span>
<span data-ttu-id="2334e-123">Merhaba paylaşımda bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2334e-123">Create a directory in hello share.</span></span> <span data-ttu-id="2334e-124">Aşağıdaki örneğine hello hello dizin adlı `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="2334e-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="2334e-125">Bir yerel dosya toohello dizin karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="2334e-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="2334e-126">Şimdi bir yerel dosya toohello dizin karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2334e-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="2334e-127">Merhaba aşağıdaki örnek dosya karşıya yükleme `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="2334e-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="2334e-128">Hello dosya yolu geçerli bir dosya tooa yerel makinenizde işaret şekilde düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="2334e-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="2334e-129">Merhaba dizininde hello dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="2334e-129">List hello files in hello directory</span></span>
<span data-ttu-id="2334e-130">toosee hello dosya hello dizinindeki tüm hello dizin dosyalarını listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2334e-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="2334e-131">(Varsa) Bu komut hello CustomLogs dizinindeki hello dosyaları ve alt dizinleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="2334e-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="2334e-132">Get-AzureStorageFile, hangi dizin nesnesi geçiriliyorsa, onun için dosyaların ve dizinlerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2334e-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="2334e-133">"Get-AzureStorageFile-Share $s" Merhaba kök dizinindeki dosyaları ve dizinleri listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2334e-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="2334e-134">tooget alt dizindeki dosyaların listesi, toopass hello alt tooGet-AzureStorageFile sahip.</span><span class="sxs-lookup"><span data-stu-id="2334e-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="2334e-135">Bu yaptığı olan--hello toohello kanal hello komutu ilk parçası CustomLogs hello alt dizininin dizin örneğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2334e-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="2334e-136">Daha sonra customlogs alt dizinindeki hello dosyaları ve dizinleri döndüren Get-AzureStorageFile içine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="2334e-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="2334e-137">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="2334e-137">Copy files</span></span>
<span data-ttu-id="2334e-138">Azure PowerShell'in 0.9.7 sürümünden başlayarak, tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2334e-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="2334e-139">Aşağıda nasıl tooperform bu kopyalama göstermek PowerShell cmdlet'lerini kullanarak işlemleri.</span><span class="sxs-lookup"><span data-stu-id="2334e-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="2334e-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2334e-140">Next steps</span></span>
<span data-ttu-id="2334e-141">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="2334e-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="2334e-142">SSS</span><span class="sxs-lookup"><span data-stu-id="2334e-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="2334e-143">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2334e-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)