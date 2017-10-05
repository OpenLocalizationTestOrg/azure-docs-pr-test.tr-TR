---
title: "Bağlama Azure dosya depolama biriminden bir Azure Windows VM | Microsoft Docs"
description: "Azure dosya depolama ile bulutta dosya depolamak ve bir Azure sanal makineden (VM) bulut dosya paylaşımına bağlayın."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="d5d3c-103">Azure dosya paylaşımları Windows VM ile birlikte kullanmak</span><span class="sxs-lookup"><span data-stu-id="d5d3c-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="d5d3c-104">Azure dosya paylaşımları, depolama ve sanal makineden dosyalara erişmek için bir yol olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="d5d3c-105">Örneğin, bir komut dosyası veya paylaşmak için tüm VM'ler istediğiniz uygulama yapılandırma dosyası depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="d5d3c-106">Bu konuda, nasıl oluşturulacağı ve bir Azure dosya paylaşımını bağlama ve dosyaları yükleme ve indirme nasıl gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="d5d3c-107">Bir sanal makineden bir dosya paylaşımına bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d5d3c-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="d5d3c-108">Bu bölümde, bağlanmak istediğiniz bir dosya paylaşımı zaten olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="d5d3c-109">Bir oluşturmanız gerekiyorsa, bkz: [bir dosya paylaşımı oluşturmak](#create-a-file-share) bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="d5d3c-110">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5d3c-111">Sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="d5d3c-112">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-112">Choose your storage account.</span></span>
4. <span data-ttu-id="d5d3c-113">İçinde **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="d5d3c-114">Bir dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-114">Select a file share.</span></span>
6. <span data-ttu-id="d5d3c-115">Tıklatın **Bağlan** Windows veya Linux dosya paylaşımına bağlanması için komut satırı sözdizimi gösterilmektedir sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="d5d3c-116">Komutun sözdizimi vurgulayın ve Not Defteri veya nedenini bildirmeden bir yerde başka kolayca erişebilirsiniz bir yere yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="d5d3c-117">Başında kaldırmak için söz dizimi Düzenle ** > ** ve değiştirme *[sürücü harfi]* sürücü harfiyle (örneğin, **Y:**) burada istediğiniz dosya paylaşımını bağlama.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="d5d3c-118">VM'nize bağlanmak ve bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="d5d3c-119">Düzenlenen bağlantı sözdiziminde yapıştırın ve isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="d5d3c-120">Bağlantı oluşturulduğunda, ileti almak **komutu başarıyla tamamlandı.**</span><span class="sxs-lookup"><span data-stu-id="d5d3c-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="d5d3c-121">Bu sürücüye geçin ve yazın için sürücü harfini yazarak bağlantıyı denetleyin **dir** dosya paylaşımı içeriğini görmek için.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="d5d3c-122">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5d3c-122">Create a file share</span></span> 
1. <span data-ttu-id="d5d3c-123">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5d3c-124">Sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="d5d3c-125">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-125">Choose your storage account.</span></span>
4. <span data-ttu-id="d5d3c-126">İçinde **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="d5d3c-127">Dosya hizmeti sayfasında tıklatın **+ dosya paylaşımı** ilk dosya paylaşımınızı oluşturmak üzere. \\</span><span class="sxs-lookup"><span data-stu-id="d5d3c-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="d5d3c-128">Dosya Paylaşımı adı girin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-128">Fill in the file share name.</span></span> <span data-ttu-id="d5d3c-129">Dosya Paylaşımı adları küçük harf, rakam ve tek tire kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="d5d3c-130">Adı bir tire ile başlayamaz ve birden çok kullanamazsınız art arda kısa çizgi.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="d5d3c-131">Ne kadar büyük olabilir, en fazla 5120 GB üzerinde bir sınır doldurun.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="d5d3c-132">Tıklatın **Tamam** dosya paylaşımı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="d5d3c-133">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d5d3c-133">Upload files</span></span>
1. <span data-ttu-id="d5d3c-134">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5d3c-135">Sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="d5d3c-136">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-136">Choose your storage account.</span></span>
4. <span data-ttu-id="d5d3c-137">İçinde **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="d5d3c-138">Bir dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-138">Select a file share.</span></span>
6. <span data-ttu-id="d5d3c-139">Tıklatın **karşıya** açmak için **dosyaları karşıya yükleme** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="d5d3c-140">Yerel dosya sisteminizi karşıya yüklenecek dosyayı göz atmak için klasör simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="d5d3c-141">Tıklatın **karşıya** dosya dosya paylaşımına karşıya.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="d5d3c-142">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="d5d3c-142">Download files</span></span>
1. <span data-ttu-id="d5d3c-143">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5d3c-144">Sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="d5d3c-145">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-145">Choose your storage account.</span></span>
4. <span data-ttu-id="d5d3c-146">İçinde **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="d5d3c-147">Bir dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-147">Select a file share.</span></span>
6. <span data-ttu-id="d5d3c-148">Dosyayı sağ tıklayın ve seçin **karşıdan** yerel makinenize indirmek için.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="d5d3c-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5d3c-149">Next steps</span></span>

<span data-ttu-id="d5d3c-150">Ayrıca, oluşturun ve PowerShell kullanarak dosya paylaşımlarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="d5d3c-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="d5d3c-151">Daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="d5d3c-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
