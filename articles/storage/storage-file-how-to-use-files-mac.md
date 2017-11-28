---
title: "macOS SMB üzerinden aaaMount Azure dosya paylaşımının | Microsoft Docs"
description: "Nasıl toomount bir Azure dosya paylaşımı üzerinden SMB macOS ile bilgi edinin."
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="30564-103">macOS’da SMB üzerinden Azure Dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="30564-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="30564-104">[Azure File storage](storage-dotnet-how-to-use-files.md) hello Azure toocreate ve kullanım ağ dosya paylaşımları sağlayan Microsoft'un hizmetini kullanarak hello endüstri standardı.</span><span class="sxs-lookup"><span data-stu-id="30564-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="30564-105">Azure Dosya paylaşımları macOS Sierra (10.12) ve El Capitan’da (10.11) bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="30564-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="30564-106">Bu makalede iki farklı şekilde toomount macOS hello Terminal kullanarak ve hello Bulucu kullanıcı Arabirimi ile bir Azure dosya paylaşımı gösterir.</span><span class="sxs-lookup"><span data-stu-id="30564-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="30564-107">SMB üzerinden Azure Dosya paylaşımını bağlamadan önce, SMB paket imzalamasını devre dışı bırakmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="30564-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="30564-108">Bunu yapmazsanız düşük performans macOS hello Azure dosya paylaşımı erişirken verim.</span><span class="sxs-lookup"><span data-stu-id="30564-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="30564-109">Merhaba güvenlik bağlantınızın etkilemesini SMB bağlantınızı şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="30564-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="30564-110">Terminal Hello hello aşağıdaki komutları SMB paket imzalama, bu tarafından açıklandığı gibi devre dışı bırakır [SMB paket imzalama devre dışı bırakma Apple destek makalesine](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="30564-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="30564-111">macOS’ta Azure Dosya paylaşımını bağlama önkoşulları</span><span class="sxs-lookup"><span data-stu-id="30564-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="30564-112">**Depolama hesabı adı**: toomount bir Azure dosya paylaşımı, hello depolama hesabının adını hello.</span><span class="sxs-lookup"><span data-stu-id="30564-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="30564-113">**Depolama hesabı anahtarı**: toomount bir Azure dosya paylaşımı, birincil (veya ikincil) depolama anahtarı hello.</span><span class="sxs-lookup"><span data-stu-id="30564-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="30564-114">SAS anahtarları şu an bağlama için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="30564-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="30564-115">**Bağlantı noktası 445’in açık olduğundan emin olun**: SMB, TCP bağlantı noktası 445 üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="30564-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="30564-116">(Merhaba Mac), istemci makinenizde toomake, güvenlik duvarının TCP bağlantı noktası 445 engellemediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="30564-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="30564-117">Bulucu yoluyla Azure Dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="30564-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="30564-118">**Bulucu açmak**: Bulucu varsayılan macOS üzerinde açık, ancak, bunu hello şu anda seçili uygulama hello "macOS yüz simgesi"'i tıklatarak hello noktasında sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30564-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="30564-119">![Merhaba macOS yüz simgesi](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="30564-119">![hello macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="30564-120">**"TooServer Bağlan" hello "Git" menü seçin**: hello hello UNC yolundan kullanarak [Önkoşullar](#preq), Dönüştür hello başına çift ters eğik çizgi (`\\`) çok`smb://` ve tüm diğer ters eğik çizgi (`\`) tooforwards eğik çizgi (`/`).</span><span class="sxs-lookup"><span data-stu-id="30564-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="30564-121">Bağlantı hello aşağıdaki gibi görünmelidir: ![hello "tooServer Bağlan" iletişim](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="30564-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="30564-122">**Bir kullanıcı adı ve parola istendiğinde hello paylaşım adı ve depolama hesabı anahtarı kullan**: "Bağlan" hello "tooServer Bağlan" iletişim kutusunda tıklattığınızda hello kullanıcı adı ve parola (Bu olacaktır, macOS ile autopopulated istenir Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="30564-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="30564-123">MacOS Anahtarlık hello paylaşım adı/depolama hesabı anahtarı yerleştirme hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="30564-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="30564-124">**Kullanım hello Azure dosya paylaşımı istediğiniz gibi**: hello paylaşım adı ve depolama hesabı anahtar hello kullanıcı adı ve parola değiştirme sonra hello paylaşımı bağlanır.</span><span class="sxs-lookup"><span data-stu-id="30564-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="30564-125">Dosyaları hello dosya paylaşım içine sürükleyip dahil olmak üzere bir yerel klasör/dosya paylaşımı, normalde kullandığınız gibi bu kullanabilir:</span><span class="sxs-lookup"><span data-stu-id="30564-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Bağlı bir Azure Dosya paylaşımının anlık görüntüsü](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="30564-127">Terminal yoluyla Azure Dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="30564-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="30564-128">Değiştir `<storage-account-name>` depolama hesabınızın hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="30564-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="30564-129">İstendiğinde parola olarak Depolama Hesabı Anahtarı’nı girin.</span><span class="sxs-lookup"><span data-stu-id="30564-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="30564-130">**Kullanım hello Azure dosya paylaşımı istediğiniz gibi**: hello Azure dosya paylaşımı takılı hello önceki komutu tarafından belirtilen hello bağlama noktasında.</span><span class="sxs-lookup"><span data-stu-id="30564-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Bir anlık görüntüsünü takılı hello Azure dosya paylaşımı](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="30564-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30564-132">Next steps</span></span>
<span data-ttu-id="30564-133">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="30564-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="30564-134">Apple destek makalesi - nasıl tooconnect dosya paylaşımı Mac</span><span class="sxs-lookup"><span data-stu-id="30564-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="30564-135">SSS</span><span class="sxs-lookup"><span data-stu-id="30564-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="30564-136">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="30564-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)