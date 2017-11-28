---
title: "Azure Dosya paylaşımını bağlama ve Windows’da paylaşıma erişme | Microsoft Docs"
description: "Azure Dosya paylaşımını bağlayın ve Windows’da paylaşıma erişin."
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
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="687b1-103">Azure Dosya paylaşımını bağlama ve Windows’da paylaşıma erişme</span><span class="sxs-lookup"><span data-stu-id="687b1-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="687b1-104">[Azure Dosya depolama](storage-dotnet-how-to-use-files.md), Windows’un kolay kullanılan bulut dosya sistemidir.</span><span class="sxs-lookup"><span data-stu-id="687b1-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="687b1-105">Azure Dosya paylaşımları, Windows ve Windows Server’a bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="687b1-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="687b1-106">Bu makale Windows’da Azure Dosya paylaşımının üç farklı yolla bağlanmasını gösterir: Dosya Gezgini kullanıcı arabirimi ile, Powershell ve Komut İstemi aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="687b1-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="687b1-107">Bir Azure Dosya paylaşımını, barındırıldığı Azure bölgesinin dışında bağlamak için (örneğin, şirket içinde veya farklı bir Azure bölgesinde) işletim sisteminin SMB 3.0'ı desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="687b1-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="687b1-108">Azure Dosya paylaşımı, işletim sistemi sürümüne bağlı olarak şirket içindeki Windows makinesine veya Azure sanal makinesine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="687b1-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="687b1-109">Aşağıdaki tabloda şunlar gösterilir:</span><span class="sxs-lookup"><span data-stu-id="687b1-109">Below table illustrates the</span></span> 

| <span data-ttu-id="687b1-110">Windows Sürümü</span><span class="sxs-lookup"><span data-stu-id="687b1-110">Windows Version</span></span>        | <span data-ttu-id="687b1-111">SMB Sürümü</span><span class="sxs-lookup"><span data-stu-id="687b1-111">SMB Version</span></span> |<span data-ttu-id="687b1-112">Azure VM'ye Bağlanabilir</span><span class="sxs-lookup"><span data-stu-id="687b1-112">Mountable On Azure VM</span></span>|<span data-ttu-id="687b1-113">Şirket İçine Bağlanabilir</span><span class="sxs-lookup"><span data-stu-id="687b1-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="687b1-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="687b1-114">Windows 7</span></span>              | <span data-ttu-id="687b1-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="687b1-115">SMB 2.1</span></span>     | <span data-ttu-id="687b1-116">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-116">Yes</span></span>                 | <span data-ttu-id="687b1-117">Hayır</span><span class="sxs-lookup"><span data-stu-id="687b1-117">No</span></span>                  |
| <span data-ttu-id="687b1-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="687b1-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="687b1-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="687b1-119">SMB 2.1</span></span>     | <span data-ttu-id="687b1-120">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-120">Yes</span></span>                 | <span data-ttu-id="687b1-121">Hayır</span><span class="sxs-lookup"><span data-stu-id="687b1-121">No</span></span>                  |
| <span data-ttu-id="687b1-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="687b1-122">Windows 8</span></span>              | <span data-ttu-id="687b1-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="687b1-123">SMB 3.0</span></span>     | <span data-ttu-id="687b1-124">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-124">Yes</span></span>                 | <span data-ttu-id="687b1-125">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-125">Yes</span></span>                 |
| <span data-ttu-id="687b1-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="687b1-126">Windows Server 2012</span></span>    | <span data-ttu-id="687b1-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="687b1-127">SMB 3.0</span></span>     | <span data-ttu-id="687b1-128">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-128">Yes</span></span>                 | <span data-ttu-id="687b1-129">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-129">Yes</span></span>                 |
| <span data-ttu-id="687b1-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="687b1-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="687b1-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="687b1-131">SMB 3.0</span></span>     | <span data-ttu-id="687b1-132">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-132">Yes</span></span>                 | <span data-ttu-id="687b1-133">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-133">Yes</span></span>                 |
| <span data-ttu-id="687b1-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="687b1-134">Windows 10</span></span>             | <span data-ttu-id="687b1-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="687b1-135">SMB 3.0</span></span>     | <span data-ttu-id="687b1-136">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-136">Yes</span></span>                 | <span data-ttu-id="687b1-137">Evet</span><span class="sxs-lookup"><span data-stu-id="687b1-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="687b1-138">Her zaman Windows sürümünüz için en yeni KB’yi almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="687b1-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="687b1-139"></a>Windows ile Azure Dosya Paylaşımını bağlama önkoşulları</span><span class="sxs-lookup"><span data-stu-id="687b1-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="687b1-140">**Depolama Hesabı Adı**: Azure Dosya paylaşımını bağlayabilmeniz için depolama hesabınızın adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="687b1-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="687b1-141">**Depolama Hesabı Anahtarı**: Azure Dosya paylaşımını bağlayabilmeniz için birincil (veya ikincil) depolama anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="687b1-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="687b1-142">SAS anahtarları şu an bağlama için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="687b1-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="687b1-143">**Bağlantı noktası 445’in açık olduğundan emin olun**: Azure Dosya depolama SMB protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="687b1-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="687b1-144">SMB, TCP bağlantı noktası 445 üstünden iletişim kurar. İstemci makinenizde güvenlik duvarının TCP bağlantı noktaları 445’i engellemediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="687b1-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="687b1-145">Azure Dosya paylaşımını Dosya Gezgini ile bağlama</span><span class="sxs-lookup"><span data-stu-id="687b1-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="687b1-146">Aşağıdaki yönergelerin Windows 10’da gösterildiğini ve eski sürümlerde biraz değişiklik gösterebileceğini aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="687b1-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="687b1-147">**Dosya Gezgini’ni açın**: Başlat Menüsünden veya Win+E kısayoluna basarak açılabilir.</span><span class="sxs-lookup"><span data-stu-id="687b1-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="687b1-148">**Pencerenin sol tarafındaki “Bu Bilgisayar” öğesine gidin. Bu, şeritteki kullanılabilir menüleri değiştirir. Bilgisayar menüsünün altındaki “Ağ Sürücüsüne Bağlan”ı** seçin.</span><span class="sxs-lookup"><span data-stu-id="687b1-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![“Ağ Sürücüsüne Bağlan” açılan menüsünün ekran görüntüsü](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="687b1-150">**Azure portalının “Bağlan” bölmesindeki UNC adını kopyalayın**: Bu bilgiyi nasıl bulacağınıza ilişkin ayrıntılı açıklamayı [burada](storage-file-how-to-use-files-portal.md#connect-to-file-share) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="687b1-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Azure Dosya depolamanın Bağlan bölmesinden UNC adı](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="687b1-152">**Sürücü harfini seçin ve UNC adını girin.**</span><span class="sxs-lookup"><span data-stu-id="687b1-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![“Ağ Sürücüsüne Bağlan” iletişim kutusunun ekran görüntüsü](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="687b1-154">**Kullanıcı adı olarak, başına `Azure\` ekleyip Depolama Hesabı Adını ve parola olarak Depolama Hesabı Anahtarını kullanın.**</span><span class="sxs-lookup"><span data-stu-id="687b1-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![Ağ kimlik bilgileri iletişim kutusunun ekran görüntüsü](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="687b1-156">**Azure Dosya paylaşımını istediğiniz gibi kullanın**.</span><span class="sxs-lookup"><span data-stu-id="687b1-156">**Use Azure File share as desired**.</span></span>
    
    ![Azure Dosya paylaşımı artık bağlanmıştır](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="687b1-158">**Azure Dosya paylaşımını çıkarmaya (veya bağlantısını kesmeye) hazır olduğunuzda, Dosya Gezgini’ndeki “Ağ konumları”nın altında bulunan girdiye sağ tıklayıp “Bağlantıyı Kes”i seçerek bunu yapabilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="687b1-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="687b1-159">Azure Dosya paylaşımı PowerShell ile bağlama</span><span class="sxs-lookup"><span data-stu-id="687b1-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="687b1-160">**Azure Dosya paylaşımını bağlamak için aşağıdaki komutları kullanın**: `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` öğelerini uygun bilgilerle değiştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="687b1-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="687b1-161">**Azure Dosya paylaşımını istediğiniz gibi kullanın**.</span><span class="sxs-lookup"><span data-stu-id="687b1-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="687b1-162">**İşiniz bittiğinde, aşağıdaki komutu kullanarak Azure Dosya paylaşımını çıkarabilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="687b1-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="687b1-163">`New-PSDrive` üzerinde `-Persist` parametresini kullanarak, Azure Dosya paylaşımını bağlıyken işletim sisteminin geri kalanında görünür duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="687b1-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="687b1-164">Azure Dosya paylaşımı Komut İstemi ile bağlama</span><span class="sxs-lookup"><span data-stu-id="687b1-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="687b1-165">**Azure Dosya paylaşımını bağlamak için aşağıdaki komutları kullanın**: `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` öğelerini uygun bilgilerle değiştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="687b1-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="687b1-166">**Azure Dosya paylaşımını istediğiniz gibi kullanın**.</span><span class="sxs-lookup"><span data-stu-id="687b1-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="687b1-167">**İşiniz bittiğinde, aşağıdaki komutu kullanarak Azure Dosya paylaşımını çıkarabilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="687b1-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="687b1-168">Windows’daki kimlik bilgilerini kalıcı hale getirerek Azure Dosya paylaşımını yeniden başlatıldığında otomatik olarak yeniden bağlanacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="687b1-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="687b1-169">Aşağıdaki komut, kimlik bilgilerini kalıcı hale getirir:</span><span class="sxs-lookup"><span data-stu-id="687b1-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="687b1-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="687b1-170">Next steps</span></span>
<span data-ttu-id="687b1-171">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="687b1-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="687b1-172">SSS</span><span class="sxs-lookup"><span data-stu-id="687b1-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="687b1-173">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="687b1-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="687b1-174">Kavramsal makaleler ve videolar</span><span class="sxs-lookup"><span data-stu-id="687b1-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="687b1-175">Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi</span><span class="sxs-lookup"><span data-stu-id="687b1-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="687b1-176">Azure Dosya depolamayı Linux ile kullanma</span><span class="sxs-lookup"><span data-stu-id="687b1-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="687b1-177">Azure Dosya depolama için araç desteği</span><span class="sxs-lookup"><span data-stu-id="687b1-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="687b1-178">Azure Depolama ile Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="687b1-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="687b1-179">Microsoft Azure Depolama ile AzCopy kullanma</span><span class="sxs-lookup"><span data-stu-id="687b1-179">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="687b1-180">Azure Depolama ile Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="687b1-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="687b1-181">Azure Dosya depolama sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="687b1-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="687b1-182">Blog yazıları</span><span class="sxs-lookup"><span data-stu-id="687b1-182">Blog posts</span></span>
* [<span data-ttu-id="687b1-183">Azure Dosya Depolama genel kullanıma sunulmuştur</span><span class="sxs-lookup"><span data-stu-id="687b1-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="687b1-184">Azure Dosya depolama incelemesi</span><span class="sxs-lookup"><span data-stu-id="687b1-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="687b1-185">Microsoft Azure Dosya Hizmeti’ne Giriş</span><span class="sxs-lookup"><span data-stu-id="687b1-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="687b1-186">Azure Dosya Hizmeti’ne verileri geçirme </span><span class="sxs-lookup"><span data-stu-id="687b1-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="687b1-187">Başvuru</span><span class="sxs-lookup"><span data-stu-id="687b1-187">Reference</span></span>
* [<span data-ttu-id="687b1-188">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="687b1-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="687b1-189">Dosya Hizmeti REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="687b1-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
