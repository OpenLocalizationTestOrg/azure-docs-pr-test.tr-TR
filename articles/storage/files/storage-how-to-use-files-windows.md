---
title: "aaaMount bir Azure dosya paylaşımı ve erişim hello paylaşmak Windows | Microsoft Docs"
description: "Bir Azure dosya paylaşımı ve Windows hello paylaşımına erişim bağlayın."
services: storage
documentationcenter: na
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
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="6fa3d-103">Bir Azure dosya paylaşımı ve Windows hello paylaşımına erişim bağlama</span><span class="sxs-lookup"><span data-stu-id="6fa3d-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="6fa3d-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) Microsoft'un kolay toouse bulut dosya sistemidir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="6fa3d-105">Azure Dosya paylaşımları, Windows ve Windows Server’a bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="6fa3d-106">Bu makalede üç farklı şekilde toomount bir Azure dosya paylaşımı Windows gösterilmektedir: hello dosya Gezgini kullanıcı Arabirimi, PowerShell aracılığıyla ve hello komut istemi aracılığıyla ile.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="6fa3d-107">Bir Azure dosya paylaşımı dışında hello içinde şirket içi gibi veya farklı bir Azure bölgesindeki barındırıldığı Azure bölgesi sipariş toomount içinde SMB 3.0 hello OS desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="6fa3d-108">Azure Dosya paylaşımı, işletim sistemi sürümüne bağlı olarak şirket içindeki Windows makinesine veya Azure sanal makinesine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="6fa3d-109">Aşağıdaki tablo hello gösterir</span><span class="sxs-lookup"><span data-stu-id="6fa3d-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="6fa3d-110">Windows Sürümü</span><span class="sxs-lookup"><span data-stu-id="6fa3d-110">Windows Version</span></span>        | <span data-ttu-id="6fa3d-111">SMB Sürümü</span><span class="sxs-lookup"><span data-stu-id="6fa3d-111">SMB Version</span></span> |<span data-ttu-id="6fa3d-112">Azure VM'ye Bağlanabilir</span><span class="sxs-lookup"><span data-stu-id="6fa3d-112">Mountable On Azure VM</span></span>|<span data-ttu-id="6fa3d-113">Şirket İçine Bağlanabilir</span><span class="sxs-lookup"><span data-stu-id="6fa3d-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="6fa3d-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="6fa3d-114">Windows 7</span></span>              | <span data-ttu-id="6fa3d-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="6fa3d-115">SMB 2.1</span></span>     | <span data-ttu-id="6fa3d-116">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-116">Yes</span></span>                 | <span data-ttu-id="6fa3d-117">Hayır</span><span class="sxs-lookup"><span data-stu-id="6fa3d-117">No</span></span>                  |
| <span data-ttu-id="6fa3d-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="6fa3d-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="6fa3d-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="6fa3d-119">SMB 2.1</span></span>     | <span data-ttu-id="6fa3d-120">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-120">Yes</span></span>                 | <span data-ttu-id="6fa3d-121">Hayır</span><span class="sxs-lookup"><span data-stu-id="6fa3d-121">No</span></span>                  |
| <span data-ttu-id="6fa3d-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="6fa3d-122">Windows 8</span></span>              | <span data-ttu-id="6fa3d-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="6fa3d-123">SMB 3.0</span></span>     | <span data-ttu-id="6fa3d-124">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-124">Yes</span></span>                 | <span data-ttu-id="6fa3d-125">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-125">Yes</span></span>                 |
| <span data-ttu-id="6fa3d-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6fa3d-126">Windows Server 2012</span></span>    | <span data-ttu-id="6fa3d-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="6fa3d-127">SMB 3.0</span></span>     | <span data-ttu-id="6fa3d-128">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-128">Yes</span></span>                 | <span data-ttu-id="6fa3d-129">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-129">Yes</span></span>                 |
| <span data-ttu-id="6fa3d-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6fa3d-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="6fa3d-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="6fa3d-131">SMB 3.0</span></span>     | <span data-ttu-id="6fa3d-132">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-132">Yes</span></span>                 | <span data-ttu-id="6fa3d-133">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-133">Yes</span></span>                 |
| <span data-ttu-id="6fa3d-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="6fa3d-134">Windows 10</span></span>             | <span data-ttu-id="6fa3d-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="6fa3d-135">SMB 3.0</span></span>     | <span data-ttu-id="6fa3d-136">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-136">Yes</span></span>                 | <span data-ttu-id="6fa3d-137">Evet</span><span class="sxs-lookup"><span data-stu-id="6fa3d-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="6fa3d-138">Her zaman alma öneririz Windows sürümünüz için en son KB hello.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="6fa3d-139"></a>Windows ile Azure Dosya Paylaşımını bağlama önkoşulları</span><span class="sxs-lookup"><span data-stu-id="6fa3d-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="6fa3d-140">**Depolama hesabı adı**: toomount bir Azure dosya paylaşımı, hello depolama hesabının adını hello.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="6fa3d-141">**Depolama hesabı anahtarı**: toomount bir Azure dosya paylaşımı, birincil (veya ikincil) depolama anahtarı hello.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="6fa3d-142">SAS anahtarları şu an bağlama için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="6fa3d-143">**Bağlantı noktası 445’in açık olduğundan emin olun**: Azure Dosya depolama SMB protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="6fa3d-144">Güvenlik duvarınızın istemci makineden 445 numaralı TCP bağlantı noktaları engellemediğinden SMB 445 - TCP bağlantı noktası üzerinden iletişim kurar toosee kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="6fa3d-145">Dosya Gezgini ile Hello Azure dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="6fa3d-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="6fa3d-146">Yönergeleri izleyerek hello Not üzerinde Windows 10 gösterilir ve eski sürümleri üzerinde biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="6fa3d-147">**Dosya Gezgini'ni açın**: Bu hello Başlat menüsü açmasının tarafından ya da Win + E kısayol tuşuna basarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="6fa3d-148">**Merhaba penceresinin hello sol taraftaki toohello "Bu bilgisayar" öğesini gidin. Bu hello menüleri hello Şeritte kullanılabilir değiştirir. "Ağ sürücüsüne" Merhaba bilgisayar menüsünün altında tıklatın**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Merhaba "Harita ağ sürücüsü" açılan menüden bir ekran görüntüsü](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="6fa3d-150">**Merhaba "Bağlan" Merhaba Azure portal bölmesinde Kopyala hello UNC yolundan**: toofind bu bilgileri nasıl bulunabilir ayrıntılı bir açıklama [burada](storage-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="6fa3d-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Merhaba UNC yolundan hello Azure dosya depolama Bağlan bölmesi](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="6fa3d-152">**Merhaba sürücü harfi seçin ve hello UNC yolunu girin.**</span><span class="sxs-lookup"><span data-stu-id="6fa3d-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    !["Ağ sürücüsüne" Merhaba iletişim kutusunun ekran görüntüsü](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="6fa3d-154">**Kullanım hello depolama hesabı adı ile $a `Azure\` hello kullanıcı adı ve bir depolama hesabı anahtarı hello parola olarak olarak.**</span><span class="sxs-lookup"><span data-stu-id="6fa3d-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Merhaba ağ kimlik bilgisi iletişim kutusunun ekran görüntüsü](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="6fa3d-156">**Azure Dosya paylaşımını istediğiniz gibi kullanın**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-156">**Use Azure File share as desired**.</span></span>
    
    ![Azure Dosya paylaşımı artık bağlanmıştır](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="6fa3d-158">**Hazır toodismount olan (veya kesin olduğunda) hello Azure dosya paylaşımı, hello girişinde hello "ağ konumlarını" dosya Gezgini'nde altında hello paylaşımı için sağ tıklayarak ve "Bağlantıyı Kes"'yi seçerek bunu yapabilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="6fa3d-159">PowerShell ile Hello Azure dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="6fa3d-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="6fa3d-160">**Kullanım hello şu komutu toomount hello Azure dosya paylaşımı**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello uygun bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="6fa3d-161">**Kullanım hello Azure dosya paylaşımı istediğiniz gibi**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="6fa3d-162">**İşiniz bittiğinde, komutu aşağıdaki hello kullanarak hello Azure dosya paylaşımı kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="6fa3d-163">Merhaba kullanabilir `-Persist` parametresini `New-PSDrive` toomake hello Azure dosya paylaşımı görünür toohello hello takılı sırasında işletim sistemi geri kalanı.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="6fa3d-164">Komut İstemi ile Hello Azure dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="6fa3d-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="6fa3d-165">**Kullanım hello şu komutu toomount hello Azure dosya paylaşımı**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello uygun bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="6fa3d-166">**Kullanım hello Azure dosya paylaşımı istediğiniz gibi**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="6fa3d-167">**İşiniz bittiğinde, komutu aşağıdaki hello kullanarak hello Azure dosya paylaşımı kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="6fa3d-168">Kalıcı hello kimlik bilgileri Windows tarafından yeniden başlatmada hello Azure dosya paylaşımı tooautomatically yeniden yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="6fa3d-169">komutu aşağıdaki hello hello kimlik kalıcı:</span><span class="sxs-lookup"><span data-stu-id="6fa3d-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="6fa3d-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6fa3d-170">Next steps</span></span>
<span data-ttu-id="6fa3d-171">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="6fa3d-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="6fa3d-172">SSS</span><span class="sxs-lookup"><span data-stu-id="6fa3d-172">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="6fa3d-173">Windows’da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="6fa3d-173">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="6fa3d-174">Kavramsal makaleler ve videolar</span><span class="sxs-lookup"><span data-stu-id="6fa3d-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="6fa3d-175">Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi</span><span class="sxs-lookup"><span data-stu-id="6fa3d-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="6fa3d-176">Nasıl toouse Linux Azure File storage</span><span class="sxs-lookup"><span data-stu-id="6fa3d-176">How toouse Azure File storage with Linux</span></span>](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="6fa3d-177">Azure Dosya depolama için araç desteği</span><span class="sxs-lookup"><span data-stu-id="6fa3d-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="6fa3d-178">Nasıl toouse Microsoft Azure Storage ile AzCopy</span><span class="sxs-lookup"><span data-stu-id="6fa3d-178">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="6fa3d-179">Azure Storage ile Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="6fa3d-179">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="6fa3d-180">Azure Dosya depolama sorunlarını giderme - Windows</span><span class="sxs-lookup"><span data-stu-id="6fa3d-180">Troubleshooting Azure File storage problems - Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)
* [<span data-ttu-id="6fa3d-181">Azure Dosya depolama sorunlarını giderme - Linux</span><span class="sxs-lookup"><span data-stu-id="6fa3d-181">Troubleshooting Azure File storage problems - Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="6fa3d-182">Blog yazıları</span><span class="sxs-lookup"><span data-stu-id="6fa3d-182">Blog posts</span></span>
* [<span data-ttu-id="6fa3d-183">Azure Dosya Depolama genel kullanıma sunulmuştur</span><span class="sxs-lookup"><span data-stu-id="6fa3d-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="6fa3d-184">Azure Dosya depolama incelemesi</span><span class="sxs-lookup"><span data-stu-id="6fa3d-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="6fa3d-185">Microsoft Azure Dosya Hizmeti’ne Giriş</span><span class="sxs-lookup"><span data-stu-id="6fa3d-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="6fa3d-186">Geçirme verilerini tooAzure dosyası</span><span class="sxs-lookup"><span data-stu-id="6fa3d-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="6fa3d-187">Başvuru</span><span class="sxs-lookup"><span data-stu-id="6fa3d-187">Reference</span></span>
* [<span data-ttu-id="6fa3d-188">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="6fa3d-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="6fa3d-189">Dosya Hizmeti REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="6fa3d-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
