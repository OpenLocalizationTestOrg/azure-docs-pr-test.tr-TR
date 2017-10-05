---
title: "Bir Azure Windows VM görüntüsünü yakalama | Microsoft Docs"
description: "Klasik dağıtım modeliyle oluşturulan bir Azure Windows sanal makinesinin bir görüntüsünü yakalama"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="01388-103">Klasik dağıtım modeliyle oluşturulan bir Azure Windows sanal makinesinin bir görüntüsünü yakalama</span><span class="sxs-lookup"><span data-stu-id="01388-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="01388-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="01388-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="01388-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="01388-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="01388-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="01388-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="01388-107">Resource Manager modeli için bilgi [genelleştirilmiş VM Azure ile yönetilen bir görüntüsünü yakalama](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="01388-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="01388-108">Bu makalede, diğer sanal makineler oluşturmak için bir resim olarak kullanabilmek için Windows çalıştıran bir Azure sanal makinesi yakalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="01388-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="01388-109">Bu görüntü, işletim sistemi diski ve sanal makineye bağlı olan veri disklerinin içerir.</span><span class="sxs-lookup"><span data-stu-id="01388-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="01388-110">Diğer görüntü kullanan sanal makineleri oluşturduğunuzda ağ yapılandırmalarını ayarlamanız gerekir böylece ağ yapılandırmaları içermez.</span><span class="sxs-lookup"><span data-stu-id="01388-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="01388-111">Azure depolar altındaki görüntüyü **VM görüntüleri (Klasik)**, **işlem** tüm Azure hizmetlerini görüntülediğinizde listelenen hizmet.</span><span class="sxs-lookup"><span data-stu-id="01388-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="01388-112">Bu, yüklediğiniz tüm görüntüleri depolandığı aynı yerdir.</span><span class="sxs-lookup"><span data-stu-id="01388-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="01388-113">Görüntüleri hakkında daha fazla ayrıntı için bkz: [sanal makineler için görüntüleri hakkında](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01388-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="01388-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="01388-114">Before you begin</span></span>
<span data-ttu-id="01388-115">Bu adımlarda, bir Azure sanal makinesi oluşturulur ve yapılandırılmış olan veri disklerinin ekleme de dahil olmak üzere işletim sistemi varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="01388-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="01388-116">Bunu henüz yapmadıysanız oluşturma ve sanal makine hazırlanıyor hakkında bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="01388-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="01388-117">Bir görüntüden sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="01388-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="01388-118">Nasıl bir sanal makineye bir veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="01388-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="01388-119">Sunucu rolleri Sysprep ile desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="01388-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="01388-120">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="01388-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="01388-121">Bu işlem, yakalandıktan sonra özgün sanal makine siler.</span><span class="sxs-lookup"><span data-stu-id="01388-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="01388-122">Bir Azure sanal makinesi görüntüsünü yapılandırmadan önce hedef sanal makine yedeklenebilir önerilir.</span><span class="sxs-lookup"><span data-stu-id="01388-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="01388-123">Azure sanal makineleri Azure Yedekleme kullanılarak yedeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="01388-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="01388-124">Ayrıntılar için bkz. [Azure sanal makinelerini yedekleme](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="01388-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="01388-125">Sertifikalı iş ortaklarının sunduğu başka çözümler vardır.</span><span class="sxs-lookup"><span data-stu-id="01388-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="01388-126">Şu anda hangi çözümlerin kullanılabilir olduğunu öğrenmek için Azure Market’te arama yapın.</span><span class="sxs-lookup"><span data-stu-id="01388-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="01388-127">Sanal makine yakalanamadı</span><span class="sxs-lookup"><span data-stu-id="01388-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="01388-128">İçinde [Azure portal](http://portal.azure.com), **Bağlan** sanal makineye.</span><span class="sxs-lookup"><span data-stu-id="01388-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="01388-129">Yönergeler için bkz: [Windows Server çalıştıran bir sanal makine için oturum açma][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="01388-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="01388-130">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="01388-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="01388-131">Dizinine değiştirin `%windir%\system32\sysprep`, ve ardından sysprep.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="01388-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="01388-132">**Sistem Hazırlama aracı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="01388-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="01388-133">Şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="01388-133">Do the following:</span></span>

   * <span data-ttu-id="01388-134">İçinde **sistem temizleme eylemi**seçin **girin sistem Out-of-Box deneyimi (OOBE)** emin olun **Generalize** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="01388-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="01388-135">Sysprep kullanma hakkında daha fazla bilgi için bkz: [kullanım Sysprep nasıl: Giriş][How to Use Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="01388-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="01388-136">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="01388-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="01388-137">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01388-137">Click **OK**.</span></span>

   ![Sysprep'i çalıştırın](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="01388-139">Azure portalında sanal makinenin durumunu değiştiren sanal makine, Sysprep kapandıktan **durduruldu**.</span><span class="sxs-lookup"><span data-stu-id="01388-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="01388-140">Azure portalında tıklatın **sanal makineleri (Klasik)** ve yakalamak istediğiniz sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="01388-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="01388-141">**VM görüntüleri (Klasik)** grubu altında listelenen **işlem** görüntülediğinizde **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="01388-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="01388-142">Komut çubuğunda **yakalama**.</span><span class="sxs-lookup"><span data-stu-id="01388-142">On the command bar, click **Capture**.</span></span>

   ![Sanal makine yakalama](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="01388-144">**Sanal makine yakalanamadı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="01388-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="01388-145">İçinde **görüntü adı**, yeni görüntüsü için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="01388-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="01388-146">İçinde **görüntü etiketi**, yeni görüntüsü için bir etiket yazın.</span><span class="sxs-lookup"><span data-stu-id="01388-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="01388-147">Tıklatın **sanal makinede Sysprep çalıştırdım**.</span><span class="sxs-lookup"><span data-stu-id="01388-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="01388-148">Adım 3-5 Sysprep ile eylemler için bu onay kutusunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="01388-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="01388-149">Bir görüntü _gerekir_ genelleştirilmiş bir Windows Server görüntüsü özel resimler kümenize eklemeden önce Sysprep çalıştırarak.</span><span class="sxs-lookup"><span data-stu-id="01388-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="01388-150">Yakalama işlemi tamamlandıktan sonra yeni görüntüyü içinde etkin hale **Market**, **işlem**, **VM görüntüleri (Klasik)** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="01388-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Görüntü yakalama başarılı](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="01388-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01388-152">Next steps</span></span>
<span data-ttu-id="01388-153">Sanal makineler oluşturmak için kullanılacak görüntüyü hazırdır.</span><span class="sxs-lookup"><span data-stu-id="01388-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="01388-154">Bunu yapmak için bir sanal makine seçerek oluşturacaksınız **daha fazla hizmet** Hizmetleri menüsünün alt menü öğesi **VM görüntüleri (Klasik)** içinde **işlem** grubu.</span><span class="sxs-lookup"><span data-stu-id="01388-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="01388-155">Yönergeler için bkz: [bir görüntüden sanal makine oluşturma](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="01388-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
