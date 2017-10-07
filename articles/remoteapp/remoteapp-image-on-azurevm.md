---
title: "Azure RemoteApp görüntüsü dayalı bir Azure VM aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate bir Azure sanal makinesi ile başlatarak Azure RemoteApp için görüntü."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="3e51c-103">Bir Azure sanal makineye dayalı bir Azure RemoteApp görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e51c-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3e51c-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e51c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3e51c-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="3e51c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3e51c-106">Bir Azure sanal makineden (hangi koleksiyonunuzda paylaşmak hello uygulamaları barındıracak) Azure RemoteApp görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e51c-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="3e51c-107">Toouse tüm hello Azure RemoteApp görüntü gereksinimleri karşılayan toohello Azure VM görüntü Galerisi eklediğimiz sanal makine görüntüsü seçebilir - isterseniz kendi VM için bu VM görüntüsü bir başlangıç noktası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e51c-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="3e51c-108">Yalnızca hello "Windows Server Uzak Masaüstü oturumu ana bilgisayarı" görüntü hello Kitaplığı'nda arayın.</span><span class="sxs-lookup"><span data-stu-id="3e51c-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="3e51c-109">Azure VM temelinde kendi görüntünüzü tabanlı iki adımları toocreate vardır - hello görüntü oluşturma ve hello Azure VM kitaplık tooAzure RemoteApp karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3e51c-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="3e51c-110">Bir Azure VM temelinde özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="3e51c-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="3e51c-111">Bu adımları toocreate bir Azure VM temelinde görüntü kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e51c-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="3e51c-112">Bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e51c-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="3e51c-113">Hello Azure sanal makine görüntüsü Galerisi'nden hello "Windows Server Uzak Masaüstü oturumu ana bilgisayarı" veya "Windows Server Uzak Masaüstü oturumu ana bilgisayarı ile Microsoft Office 365 ProPlus" Merhaba görüntüsü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e51c-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="3e51c-114">Bu görüntü tüm hello Azure RemoteApp şablon görüntüsü gereksinimlerini karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="3e51c-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="3e51c-115">Ayrıntılar için bkz [Windows çalıştıran bir VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e51c-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="3e51c-116">Toohello VM bağlanmak ve yükleyin ve RemoteApp aracılığıyla tooshare istediğiniz hello uygulamalar yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3e51c-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="3e51c-117">Emin tooperform uygulamalarınız tarafından gerekli ek Windows yapılandırmalara olun.</span><span class="sxs-lookup"><span data-stu-id="3e51c-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="3e51c-118">Ayrıntılar için bkz [nasıl tooLog tooa sanal makine çalıştıran Windows Server üzerinde](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e51c-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="3e51c-119">Merhaba Windows Server Uzak Masaüstü oturumu ana bilgisayarı görüntülerden birini kullanıyorsanız, VM hello RemoteApp pre-reqs. karşılayan sağlayacak bir dahil doğrulama komut dosyası yok</span><span class="sxs-lookup"><span data-stu-id="3e51c-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="3e51c-120">toorun komut dosyasını çift tıklatın **Validateremoteappımage** hello masaüstünde.</span><span class="sxs-lookup"><span data-stu-id="3e51c-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="3e51c-121">Merhaba betik tarafından raporlanan tüm hataları toohello sonraki adıma devam etmeden önce düzeltilen emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e51c-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="3e51c-122">SYSPREP generalize ve hello görüntüsünü yakalayın.</span><span class="sxs-lookup"><span data-stu-id="3e51c-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="3e51c-123">Bkz: [nasıl tooCapture bir şablon olarak Windows sanal makine tooUse](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="3e51c-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="3e51c-124">Hello Azure RemoteApp görüntüsü kitaplığa Hello görüntüsü Aktar</span><span class="sxs-lookup"><span data-stu-id="3e51c-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="3e51c-125">Bu adımları tooimport hello yeni görüntüyü Azure RemoteApp kullanın:</span><span class="sxs-lookup"><span data-stu-id="3e51c-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="3e51c-126">Merhaba, **şablon görüntüleri** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="3e51c-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="3e51c-127">Hiçbir mevcut görüntü varsa, tıklatın **karşıya yükleyebilir veya bir şablon görüntüsü içe**.</span><span class="sxs-lookup"><span data-stu-id="3e51c-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="3e51c-128">En az bir görüntü zaten varsa, tıklatın  **+**  tooadd yeni bir görüntü.</span><span class="sxs-lookup"><span data-stu-id="3e51c-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="3e51c-129">Seçin **sanal makinelerden bir görüntü alma** kitaplığı ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3e51c-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="3e51c-130">Merhaba sonraki sayfada özel görüntünüzü hello listeden seçin ve görüntünüzü oluşturduğunuzda listelenen hello adımları uyguladığınız onaylayın.</span><span class="sxs-lookup"><span data-stu-id="3e51c-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="3e51c-131">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e51c-131">Click **Next**.</span></span>
4. <span data-ttu-id="3e51c-132">Merhaba yeni RemoteApp görüntüsü için bir ad girin ve hello konum seçin ve ardından hello onay işareti toostart hello içeri aktarma işlemi.</span><span class="sxs-lookup"><span data-stu-id="3e51c-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="3e51c-133">Azure sanal makineleri tooany Azure RemoteApp tarafından desteklenen Azure konumu tarafından desteklenen tüm Azure konumdan görüntüleri içe aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e51c-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="3e51c-134">Merhaba konumlara bağlı olarak hello alma too25 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3e51c-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="3e51c-135">Artık toocreate yeni koleksiyonunuzu ya da hazır bir [bulut](remoteapp-create-cloud-deployment.md) koleksiyonu veya [karma](remoteapp-create-hybrid-deployment.md)gereksinimlerinize bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="3e51c-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

