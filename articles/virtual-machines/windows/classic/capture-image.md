---
title: "bir Azure Windows VM görüntüsünü aaaCapture | Microsoft Docs"
description: "Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalayın."
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
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="b4ed2-103">Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalayın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-103">Capture an image of an Azure Windows virtual machine created with hello classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b4ed2-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b4ed2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b4ed2-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b4ed2-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b4ed2-107">Resource Manager modeli için bilgi [genelleştirilmiş VM Azure ile yönetilen bir görüntüsünü yakalama](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b4ed2-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="b4ed2-108">Bu makale size nasıl gösterir toocapture bir görüntü toocreate kullanabilmeniz için diğer sanal makineler Windows çalıştıran bir Azure sanal makine.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-108">This article shows you how toocapture an Azure virtual machine running Windows so you can use it as an image toocreate other virtual machines.</span></span> <span data-ttu-id="b4ed2-109">Tüm veri disklerinin toohello sanal makineye bağlı ve bu görüntüyü hello işletim sistemi diski içerir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-109">This image includes hello operating system disk and any data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="b4ed2-110">Merhaba görüntü kullanan diğer sanal makineleri hello oluşturduğunuzda, ağ yapılandırmaları yukarı tooset gerekir böylece ağ yapılandırmaları içermez.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-110">It doesn't include networking configurations, so you'll need tooset up network configurations when you create hello other virtual machines that use hello image.</span></span>

<span data-ttu-id="b4ed2-111">Azure depoları hello altındaki görüntüyü **VM görüntüleri (Klasik)**, **işlem** tüm görüntülediğinizde listelenen hizmet hello Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-111">Azure stores hello image under **VM images (classic)**, a **Compute** service that is listed when you view all hello Azure services.</span></span> <span data-ttu-id="b4ed2-112">Merhaba budur karşıya görüntülerin depolandığı aynı yerde.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-112">This is hello same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="b4ed2-113">Görüntüleri hakkında daha fazla ayrıntı için bkz: [sanal makineler için görüntüleri hakkında](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4ed2-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b4ed2-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b4ed2-114">Before you begin</span></span>
<span data-ttu-id="b4ed2-115">Bu adımlarda, bir Azure sanal makinesi oluşturulur ve hello işletim sistemi, tüm veri diskleri ekleme de dahil olmak üzere yapılandırılmış varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-115">These steps assume that you've already created an Azure virtual machine and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="b4ed2-116">Bunu henüz yapmadıysanız hello sanal makine hazırlanıyor ve oluşturma hakkındaki bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b4ed2-116">If you haven't done this yet, see hello following articles for information on creating and preparing hello virtual machine:</span></span>

* [<span data-ttu-id="b4ed2-117">Bir görüntüden sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4ed2-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="b4ed2-118">Nasıl tooattach bir veri diski tooa sanal makine</span><span class="sxs-lookup"><span data-stu-id="b4ed2-118">How tooattach a data disk tooa virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="b4ed2-119">Merhaba sunucu rolleri Sysprep ile desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-119">Make sure hello server roles are supported with Sysprep.</span></span> <span data-ttu-id="b4ed2-120">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="b4ed2-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="b4ed2-121">Bu işlem, yakalandıktan sonra hello özgün sanal makine siler.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-121">This process deletes hello original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="b4ed2-122">Önceki toocapturing bir Azure sanal makinesi görüntüsünü bir önerilir hello hedef sanal makine yedeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-122">Prior toocapturing an image of an Azure virtual machine, it is recommended hello target virtual machine be backed up.</span></span> <span data-ttu-id="b4ed2-123">Azure sanal makineleri Azure Yedekleme kullanılarak yedeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="b4ed2-124">Ayrıntılar için bkz. [Azure sanal makinelerini yedekleme](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="b4ed2-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="b4ed2-125">Sertifikalı iş ortaklarının sunduğu başka çözümler vardır.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="b4ed2-126">şu anda kullanılabilir nedir çıkışı toofind hello Azure Marketi arayın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-126">toofind out what’s currently available, search hello Azure Marketplace.</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="b4ed2-127">Merhaba sanal makinesi yakalama</span><span class="sxs-lookup"><span data-stu-id="b4ed2-127">Capture hello virtual machine</span></span>
1. <span data-ttu-id="b4ed2-128">Merhaba, [Azure portal](http://portal.azure.com), **Bağlan** toohello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-128">In hello [Azure portal](http://portal.azure.com), **Connect** toohello virtual machine.</span></span> <span data-ttu-id="b4ed2-129">Yönergeler için bkz: [nasıl tooa sanal Windows Server çalıştıran makinede toosign][How toosign in tooa virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="b4ed2-129">For instructions, see [How toosign in tooa virtual machine running Windows Server][How toosign in tooa virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="b4ed2-130">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="b4ed2-131">Merhaba dizini çok değiştirmek`%windir%\system32\sysprep`, ve ardından sysprep.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-131">Change hello directory too`%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="b4ed2-132">Merhaba **Sistem Hazırlama aracı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-132">hello **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="b4ed2-133">Aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="b4ed2-133">Do hello following:</span></span>

   * <span data-ttu-id="b4ed2-134">İçinde **sistem temizleme eylemi**seçin **girin sistem Out-of-Box deneyimi (OOBE)** emin olun **Generalize** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="b4ed2-135">Sysprep kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse Sysprep: Giriş][How tooUse Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="b4ed2-135">For more information about using Sysprep, see [How tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="b4ed2-136">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="b4ed2-137">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-137">Click **OK**.</span></span>

   ![Sysprep'i çalıştırın](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="b4ed2-139">Sysprep kapatır hello sanal çok hello Azure portal hello sanal makinede hello durumunu Değişeni makineyi,**durduruldu**.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-139">Sysprep shuts down hello virtual machine, which changes hello status of hello virtual machine in hello Azure portal too**Stopped**.</span></span>
6. <span data-ttu-id="b4ed2-140">Hello Azure portal'ı tıklatın **sanal makineleri (Klasik)** ve hello toocapture istediğiniz sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-140">In hello Azure portal, click **Virtual Machines (classic)** and select hello virtual machine you want toocapture.</span></span> <span data-ttu-id="b4ed2-141">Merhaba **VM görüntüleri (Klasik)** grubu altında listelenen **işlem** görüntülediğinizde **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-141">hello **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="b4ed2-142">Merhaba komut çubuğunda **yakalama**.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-142">On hello command bar, click **Capture**.</span></span>

   ![Sanal makine yakalama](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="b4ed2-144">Merhaba **yakalama hello sanal makine** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-144">hello **Capture hello Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="b4ed2-145">İçinde **görüntü adı**, hello yeni görüntüsü için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-145">In **Image name**, type a name for hello new image.</span></span> <span data-ttu-id="b4ed2-146">İçinde **görüntü etiketi**, hello yeni görüntüsü için bir etiket yazın.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-146">In **Image label**, type a label for hello new image.</span></span>

9. <span data-ttu-id="b4ed2-147">Tıklatın **hello sanal makinede Sysprep çalıştırdım**.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-147">Click **I've run Sysprep on hello virtual machine**.</span></span> <span data-ttu-id="b4ed2-148">Bu onay kutusunu toohello eylemlerinde Sysprep ile 3-5 adımlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-148">This checkbox refers toohello actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="b4ed2-149">Bir görüntü _gerekir_ genelleştirilmiş bir Windows sunucusu eklemeden önce özel görüntü görüntü tooyour kümesi Sysprep çalıştırarak.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image tooyour set of custom images.</span></span>

10. <span data-ttu-id="b4ed2-150">Merhaba yakalama işlemi tamamlandıktan sonra hello yeni görüntüsü hello kullanılabilir **Market**, hello içinde **işlem**, **VM görüntüleri (Klasik)** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-150">Once hello capture completes, hello new image becomes available in hello **Marketplace**, in hello **Compute**, **VM images (classic)** container.</span></span>

    ![Görüntü yakalama başarılı](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="b4ed2-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4ed2-152">Next steps</span></span>
<span data-ttu-id="b4ed2-153">Merhaba, kullanılan hazır toobe toocreate sanal makineleri görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-153">hello image is ready toobe used toocreate virtual machines.</span></span> <span data-ttu-id="b4ed2-154">toodo bunu hello seçerek bir sanal makine oluşturacaksınız **daha fazla hizmet** menü öğesi hello Hizmetleri menüsü, ardından hello sonundaki **VM görüntüleri (Klasik)** hello içinde **işlem**grubu.</span><span class="sxs-lookup"><span data-stu-id="b4ed2-154">toodo this, you'll create a virtual machine by selecting hello **More services** menu item at hello bottom of hello services menu, then **VM images (classic)** in hello **Compute** group.</span></span> <span data-ttu-id="b4ed2-155">Yönergeler için bkz: [bir görüntüden sanal makine oluşturma](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="b4ed2-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
