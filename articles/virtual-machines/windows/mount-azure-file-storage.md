---
title: Azure dosya depolama biriminden bir Azure Windows VM aaaMount | Microsoft Docs
description: "Azure dosya depolama ile Merhaba bulutta dosya depolamak ve bir Azure sanal makineden (VM) bulut dosya paylaşımına bağlayın."
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
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="fc6a4-103">Azure dosya paylaşımları Windows VM ile birlikte kullanmak</span><span class="sxs-lookup"><span data-stu-id="fc6a4-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="fc6a4-104">Azure dosya paylaşımları, VM'den bir şekilde toostore ve erişim dosyaları olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="fc6a4-105">Örneğin, bir komut dosyası veya tüm sanal makineleri tooshare istediğiniz uygulama yapılandırma dosyası depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="fc6a4-106">Bu konuda, dosya paylaşımı toocreate ve bağlama Azure nasıl ve ne gösteriyoruz tooupload ve yükleme dosyaları.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="fc6a4-107">Bir sanal makineden tooa dosya paylaşımına bağlanmak</span><span class="sxs-lookup"><span data-stu-id="fc6a4-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="fc6a4-108">Bu bölümde, zaten bir dosya paylaşımı için tooconnect istediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="fc6a4-109">Bir toocreate gerekirse bkz [bir dosya paylaşımı oluşturmak](#create-a-file-share) bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="fc6a4-110">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc6a4-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fc6a4-111">Merhaba sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fc6a4-112">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-112">Choose your storage account.</span></span>
4. <span data-ttu-id="fc6a4-113">Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fc6a4-114">Bir dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-114">Select a file share.</span></span>
6. <span data-ttu-id="fc6a4-115">Tıklatın **Bağlan** tooopen hello bağlama hello dosya paylaşımından Windows veya Linux için komut satırı söz dizimi görülmektedir bir sayfa.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="fc6a4-116">Merhaba komutun Hello sözdizimi vurgulayın ve Not Defteri veya nedenini bildirmeden bir yerde başka kolayca erişebilirsiniz bir yere yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="fc6a4-117">Merhaba sözdizimi tooremove hello başında Düzenle ** > ** ve değiştirme *[sürücü harfi]* hello sürücü harfine sahip (örneğin, **Y:**) burada istediğinizi toomount hello dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="fc6a4-118">Tooyour VM bağlanabilir ve bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="fc6a4-119">Merhaba yapıştırma seçeneğiyle bağlantı sözdizimi düzenlenmesi ve isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="fc6a4-120">Merhaba bağlantıyı oluştururken hello iletisi alıyorum **hello komutu başarıyla tamamlandı.**</span><span class="sxs-lookup"><span data-stu-id="fc6a4-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="fc6a4-121">Merhaba sürücü harfi tooswitch toothat sürücüye yazarak Hello bağlantısını denetleyin ve ardından **dir** toosee Merhaba içeriğine hello dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="fc6a4-122">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc6a4-122">Create a file share</span></span> 
1. <span data-ttu-id="fc6a4-123">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc6a4-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fc6a4-124">Merhaba sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fc6a4-125">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-125">Choose your storage account.</span></span>
4. <span data-ttu-id="fc6a4-126">Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fc6a4-127">Merhaba dosya hizmeti sayfasında tıklatın **+ dosya paylaşımı** ilk dosya paylaşımı toocreate. \\</span><span class="sxs-lookup"><span data-stu-id="fc6a4-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="fc6a4-128">Merhaba dosya paylaşımı adı girin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-128">Fill in hello file share name.</span></span> <span data-ttu-id="fc6a4-129">Dosya Paylaşımı adları küçük harf, rakam ve tek tire kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="fc6a4-130">Merhaba adı bir tire ile başlatamıyor ve birden çok kullanamazsınız art arda kısa çizgi.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="fc6a4-131">Bir sınırı ne kadar büyük hello dosya doldurun, too5120 GB olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="fc6a4-132">Tıklatın **Tamam** toodeploy hello dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="fc6a4-133">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="fc6a4-133">Upload files</span></span>
1. <span data-ttu-id="fc6a4-134">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc6a4-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fc6a4-135">Merhaba sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fc6a4-136">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-136">Choose your storage account.</span></span>
4. <span data-ttu-id="fc6a4-137">Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fc6a4-138">Bir dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-138">Select a file share.</span></span>
6. <span data-ttu-id="fc6a4-139">Tıklatın **karşıya** tooopen hello **dosyaları karşıya yükleme** sayfası.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="fc6a4-140">Başlangıç klasörü simgesi toobrowse üzerinde yerel dosya sistemine dosya tooupload için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="fc6a4-141">Tıklatın **karşıya** tooupload hello dosya toohello dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="fc6a4-142">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="fc6a4-142">Download files</span></span>
1. <span data-ttu-id="fc6a4-143">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc6a4-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fc6a4-144">Merhaba sol menüsünde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fc6a4-145">Depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-145">Choose your storage account.</span></span>
4. <span data-ttu-id="fc6a4-146">Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fc6a4-147">Bir dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-147">Select a file share.</span></span>
6. <span data-ttu-id="fc6a4-148">Merhaba dosyasını sağ tıklatın ve seçin **karşıdan** toodownload, tooyour yerel makine.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="fc6a4-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc6a4-149">Next steps</span></span>

<span data-ttu-id="fc6a4-150">Ayrıca, oluşturun ve PowerShell kullanarak dosya paylaşımlarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="fc6a4-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="fc6a4-151">Daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="fc6a4-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
