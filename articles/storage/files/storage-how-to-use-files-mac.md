---
title: "macOS’da SMB üzerinden Azure Dosya paylaşımını bağlama | Microsoft Docs"
description: "macOS’da SMB üzerinden Azure Dosya paylaşımını bağlamayı öğrenin."
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
ms.openlocfilehash: bc3d67745afb8bbffe7ec3462e995104daff9632
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="85d6e-103">macOS’da SMB üzerinden Azure Dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="85d6e-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="85d6e-104">[Azure Dosya depolama](../storage-dotnet-how-to-use-files.md), endüstri standardı kullanılarak Azure’da ağ dosya paylaşımları oluşturmanızı ve bunları kullanmanızı sağlayan bir Microsoft hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="85d6e-105">Azure Dosya paylaşımları macOS Sierra (10.12) ve El Capitan’da (10.11) bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="85d6e-106">Bu makalede, macOS’ta Bulucu kullanıcı arabirimiyle ve Terminal kullanarak Azure Dosya paylaşımını bağlamanın iki farklı yolu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="85d6e-107">SMB üzerinden Azure Dosya paylaşımını bağlamadan önce, SMB paket imzalamasını devre dışı bırakmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="85d6e-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="85d6e-108">Bunu yapmazsanız, macOS’tan Azure Dosya paylaşımına erişirken performansta düşüş olabilir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="85d6e-109">SMB bağlantınız şifrelenir, bu sayede bağlantınızın güvenliği etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="85d6e-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="85d6e-110">Terminalde, aşağıdaki komutlar [SMB paket imzalamasını devre dışı bırakma üzerine Apple destek makalesinde](https://support.apple.com/HT205926) anlatıldığı gibi SMB paket imzalamasını devre dışı bırakır:</span><span class="sxs-lookup"><span data-stu-id="85d6e-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="85d6e-111">macOS’ta Azure Dosya paylaşımını bağlama önkoşulları</span><span class="sxs-lookup"><span data-stu-id="85d6e-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="85d6e-112">**Depolama hesabı adı**: Azure Dosya paylaşımını bağlayabilmeniz için depolama hesabınızın adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="85d6e-113">**Depolama hesabı anahtarı**: Azure Dosya paylaşımını bağlayabilmeniz için birincil (veya ikincil) depolama anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="85d6e-114">SAS anahtarları şu an bağlama için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="85d6e-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="85d6e-115">**Bağlantı noktası 445’in açık olduğundan emin olun**: SMB, TCP bağlantı noktası 445 üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="85d6e-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="85d6e-116">İstemci makinenizde (Mac) güvenlik duvarının TCP bağlantı noktası 445’i engellemediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="85d6e-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="85d6e-117">Bulucu yoluyla Azure Dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="85d6e-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="85d6e-118">**Bulucu’yu açın**: Bulucu varsayılan olarak macOS’ta açıktır, ancak bunun seçili durumdaki uygulama olduğundan emin olmak için dock’taki “macOS yüz simgesine” tıklayın:</span><span class="sxs-lookup"><span data-stu-id="85d6e-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="85d6e-119">![macOS yüz simgesi](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="85d6e-119">![The macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="85d6e-120">**”Git” menüsünden “Sunucuya Bağlan”ı seçin**: [Önkoşullar](#preq)’dan UNC adını kullanarak başlangıç çift eğik çizgisini (`\\`) `smb://` ile ve diğer tüm ters eğik çizgileri (`\`) eğik çizgiyle (`/`) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85d6e-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="85d6e-121">Bağlantınız şu şekilde görünmelidir: ![“Sunucuya Bağlan” iletişim kutusu](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="85d6e-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="85d6e-122">**Kullanıcı adı ve parola istendiğinde paylaşım adını ve depolama hesabı anahtarını kullanın**: “Sunucuya Bağlan” iletişim kutusunda “Bağlan”a tıkladığınızda kullanıcı adı ve parola istenir (Bu alan otomatik olarak macOS kullanıcı adınızla doldurulur).</span><span class="sxs-lookup"><span data-stu-id="85d6e-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="85d6e-123">macOS Anahtarlığınıza paylaşım adı/depolama hesabı anahtarı yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85d6e-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="85d6e-124">**Azure Dosya paylaşımını istediğiniz gibi kullanın**: Kullanıcı adı ve parola yerine paylaşım adını ve depolama hesabı anahtarını koyduktan sonra paylaşım bağlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="85d6e-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="85d6e-125">Bunu, yerel klasör/dosya paylaşımını normalde kullandığınız gibi kullanabilirsiniz. Örneğin, dosyaları dosya paylaşımına sürükleyip bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="85d6e-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Bağlı bir Azure Dosya paylaşımının anlık görüntüsü](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="85d6e-127">Terminal yoluyla Azure Dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="85d6e-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="85d6e-128">`<storage-account-name>` değerini depolama hesabınızın adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85d6e-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="85d6e-129">İstendiğinde parola olarak Depolama Hesabı Anahtarı’nı girin.</span><span class="sxs-lookup"><span data-stu-id="85d6e-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="85d6e-130">**Azure Dosya paylaşımını istediğiniz gibi kullanın**: Azure Dosya paylaşımı, önceki komutta belirtilmiş olan bağlama noktasına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="85d6e-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Bağlı Azure Dosya paylaşımının anlık görüntüsü](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="85d6e-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85d6e-132">Next steps</span></span>
<span data-ttu-id="85d6e-133">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="85d6e-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="85d6e-134">Apple Destek Makalesi - Mac’inizde Dosya Paylaşımı ile bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="85d6e-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="85d6e-135">SSS</span><span class="sxs-lookup"><span data-stu-id="85d6e-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="85d6e-136">Windows’da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="85d6e-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="85d6e-137">Linux’ta sorun giderme</span><span class="sxs-lookup"><span data-stu-id="85d6e-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    