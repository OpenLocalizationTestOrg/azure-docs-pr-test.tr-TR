---
title: Hyper-V sanal dizisinde StorSimple aaaProvision | Microsoft Docs
description: "StorSimple sanal dizinin dağıtım ikinci Bu öğreticide, Hyper-V sanal bir dizide sağlama içerir."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="092a8-103">StorSimple sanal dizinin - sağlama Hyper-v dağıtma</span><span class="sxs-lookup"><span data-stu-id="092a8-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="092a8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="092a8-104">Overview</span></span>
<span data-ttu-id="092a8-105">Bu öğretici, StorSimple sanal nasıl tooprovision dizisi Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde açıklar.</span><span class="sxs-lookup"><span data-stu-id="092a8-105">This tutorial describes how tooprovision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="092a8-106">Bu makale, Azure portalında ve Microsoft Azure kamu bulut toohello dağıtım StorSimple sanal dizi geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="092a8-106">This article applies toohello deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="092a8-107">Sanal bir dizi yapılandırma ve yönetici ayrıcalıkları tooprovision gerekir.</span><span class="sxs-lookup"><span data-stu-id="092a8-107">You need administrator privileges tooprovision and configure a virtual array.</span></span> <span data-ttu-id="092a8-108">Merhaba sağlama ve ilk kurulum yaklaşık 10 dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-108">hello provisioning and initial setup can take around 10 minutes toocomplete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="092a8-109">Sağlama önkoşulları</span><span class="sxs-lookup"><span data-stu-id="092a8-109">Provisioning prerequisites</span></span>
<span data-ttu-id="092a8-110">Burada Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde, sanal bir dizi hello Önkoşullar tooprovision bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="092a8-110">Here you will find hello prerequisites tooprovision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="092a8-111">Merhaba StorSimple cihaz Yöneticisi hizmeti</span><span class="sxs-lookup"><span data-stu-id="092a8-111">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="092a8-112">Başlamadan önce aşağıdakilerden emin olun:</span><span class="sxs-lookup"><span data-stu-id="092a8-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="092a8-113">Tüm hello adımları tamamlamış [hazırlama hello portal StorSimple sanal dizini](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="092a8-113">You have completed all hello steps in [Prepare hello portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="092a8-114">Hyper-V için Azure portal hello hello sanal dizinin görüntü yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="092a8-114">You have downloaded hello virtual array image for Hyper-V from hello Azure portal.</span></span> <span data-ttu-id="092a8-115">Daha fazla bilgi için bkz: **adım 3: indirme hello sanal dizinin resmi** , [StorSimple sanal dizinin kılavuzu için hazırlama hello portalı](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="092a8-115">For more information, see **Step 3: Download hello virtual array image** of [Prepare hello portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="092a8-116">StorSimple sanal dizinin Hello üzerinde çalışan hello yazılımı yalnızca StorSimple cihaz Yöneticisi hizmeti hello ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-116">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="092a8-117">StorSimple sanal dizinin Hello için</span><span class="sxs-lookup"><span data-stu-id="092a8-117">For hello StorSimple Virtual Array</span></span>
<span data-ttu-id="092a8-118">Sanal bir dizi dağıtmadan önce emin olun:</span><span class="sxs-lookup"><span data-stu-id="092a8-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="092a8-119">Olması kullanılan tooa hazırlayabilirsiniz, bir cihaz Hyper-V Windows Server 2008 R2 veya sonraki sürümlerde çalışan erişim tooa ana bilgisayar sistemine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="092a8-119">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later that can be used tooa provision a device.</span></span>
* <span data-ttu-id="092a8-120">Merhaba ana bilgisayar sistemidir mümkün toodedicate kaynakları tooprovision sanal dizinizi hello:</span><span class="sxs-lookup"><span data-stu-id="092a8-120">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>

  * <span data-ttu-id="092a8-121">4 çekirdek en az.</span><span class="sxs-lookup"><span data-stu-id="092a8-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="092a8-122">En az 8 GB RAM.</span><span class="sxs-lookup"><span data-stu-id="092a8-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="092a8-123">Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="092a8-123">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="092a8-124">16 GB RAM toosupport 2-4 milyon dosyaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="092a8-124">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="092a8-125">Bir ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="092a8-125">One network interface.</span></span>
  * <span data-ttu-id="092a8-126">Veri için 500 GB sanal disk.</span><span class="sxs-lookup"><span data-stu-id="092a8-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="092a8-127">Merhaba veri merkezinde Hello ağ için</span><span class="sxs-lookup"><span data-stu-id="092a8-127">For hello network in hello datacenter</span></span>
<span data-ttu-id="092a8-128">Başlamadan önce gereksinimleri toodeploy bir StorSimple sanal dizi ağ hello gözden geçirin ve hello veri merkezi ağ uygun şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="092a8-128">Before you begin, review hello networking requirements toodeploy a StorSimple Virtual Array and configure hello datacenter network appropriately.</span></span> <span data-ttu-id="092a8-129">Daha fazla bilgi için bkz: [StorSimple sanal ağ gereksinimleri dizi](storsimple-ova-system-requirements.md#networking-requirements).</span><span class="sxs-lookup"><span data-stu-id="092a8-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="092a8-130">Adım adım sağlama</span><span class="sxs-lookup"><span data-stu-id="092a8-130">Step-by-step provisioning</span></span>
<span data-ttu-id="092a8-131">tooprovision ve tooa sanal dizinin bağlanmak, aşağıdaki adımları tooperform hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="092a8-131">tooprovision and connect tooa virtual array, you need tooperform hello following steps:</span></span>

1. <span data-ttu-id="092a8-132">Merhaba ana bilgisayar sistemi yeterli kaynakları toomeet hello minimum sanal dizinin gereksinimleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="092a8-132">Ensure that hello host system has sufficient resources toomeet hello minimum virtual array requirements.</span></span>
2. <span data-ttu-id="092a8-133">Hiper yönetici sanal bir dizide sağlayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="092a8-134">Merhaba sanal dizinin başlatın ve başlangıç IP adresi alın.</span><span class="sxs-lookup"><span data-stu-id="092a8-134">Start hello virtual array and get hello IP address.</span></span>

<span data-ttu-id="092a8-135">Bu adımların her biri aşağıdaki bölümlerde hello açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="092a8-135">Each of these steps is explained in hello following sections.</span></span>

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="092a8-136">1. adım: hello ana bilgisayar sistemi minimum sanal dizinin gereksinimleri karşıladığından emin olun</span><span class="sxs-lookup"><span data-stu-id="092a8-136">Step 1: Ensure that hello host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="092a8-137">sanal bir dizi toocreate, şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="092a8-137">toocreate a virtual array, you need:</span></span>

* <span data-ttu-id="092a8-138">Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 SP1 yüklü hello Hyper-V rolü.</span><span class="sxs-lookup"><span data-stu-id="092a8-138">hello Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="092a8-139">Bir Microsoft Windows İstemcisi üzerindeki Microsoft Hyper-V Yöneticisi'ni toohello ana bağlı.</span><span class="sxs-lookup"><span data-stu-id="092a8-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected toohello host.</span></span>

<span data-ttu-id="092a8-140">Merhaba sanal dizinin oluşturmakta olduğunuz donanım (ana bilgisayar sistemi) temel bu hello kaynakları tooyour sanal dizinin aşağıdaki mümkün toodedicate hello olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="092a8-140">Make sure that hello underlying hardware (host system) on which you are creating hello virtual array is able toodedicate hello following resources tooyour virtual array:</span></span>

* <span data-ttu-id="092a8-141">4 çekirdek en az.</span><span class="sxs-lookup"><span data-stu-id="092a8-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="092a8-142">En az 8 GB RAM.</span><span class="sxs-lookup"><span data-stu-id="092a8-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="092a8-143">Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="092a8-143">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="092a8-144">16 GB RAM toosupport 2-4 milyon dosyaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="092a8-144">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
* <span data-ttu-id="092a8-145">Bir ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="092a8-145">One network interface.</span></span>
* <span data-ttu-id="092a8-146">Sistem verileri için 500 GB sanal disk.</span><span class="sxs-lookup"><span data-stu-id="092a8-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="092a8-147">2. adım: hiper yönetici sanal bir dizide sağlama</span><span class="sxs-lookup"><span data-stu-id="092a8-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="092a8-148">Aşağıdaki adımları tooprovision bir aygıt, hiper yönetici hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="092a8-148">Perform hello following steps tooprovision a device in your hypervisor.</span></span>

#### <a name="tooprovision-a-virtual-array"></a><span data-ttu-id="092a8-149">sanal bir dizi tooprovision</span><span class="sxs-lookup"><span data-stu-id="092a8-149">tooprovision a virtual array</span></span>
1. <span data-ttu-id="092a8-150">Windows Server ana bilgisayarında hello sanal dizinin görüntü tooa yerel sürücüye kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-150">On your Windows Server host, copy hello virtual array image tooa local drive.</span></span> <span data-ttu-id="092a8-151">Bu görüntü (VHD veya VHDX) hello Azure portal indirilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-151">You downloaded this image (VHD or VHDX) through hello Azure portal.</span></span> <span data-ttu-id="092a8-152">Merhaba yordamda daha sonra bu görüntüyü kullanma gibi hello görüntü kopyaladığınız hello konumunu not edin.</span><span class="sxs-lookup"><span data-stu-id="092a8-152">Make a note of hello location where you copied hello image as you are using this image later in hello procedure.</span></span>
2. <span data-ttu-id="092a8-153">Açık **Sunucu Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="092a8-153">Open **Server Manager**.</span></span> <span data-ttu-id="092a8-154">Merhaba sağ üst köşeden, tıklatın **Araçları** seçip **Hyper-V Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="092a8-154">In hello top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="092a8-155">Windows Server 2008 R2 çalıştırıyorsanız, hello Hyper-V Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="092a8-155">If you are running Windows Server 2008 R2, open hello Hyper-V Manager.</span></span> <span data-ttu-id="092a8-156">Sunucu Yöneticisi'nde **rolleri > Hyper-V > Hyper-V Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="092a8-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="092a8-157">İçinde **Hyper-V Yöneticisi'ni**hello kapsam bölmesinde sistem düğümü tooopen hello bağlam menüsü sağ tıklayın ve ardından **yeni** > **sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="092a8-157">In **Hyper-V Manager**, in hello scope pane, right-click your system node tooopen hello context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="092a8-158">Merhaba üzerinde **başlamadan önce** hello yeni sanal makine Sihirbazı sayfasını tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="092a8-158">On hello **Before you begin** page of hello New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="092a8-159">Hello üzerinde **ad ve konum belirtin** sayfasında, sağlayan bir **adı** sanal dizini.</span><span class="sxs-lookup"><span data-stu-id="092a8-159">On hello **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="092a8-160">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="092a8-161">Merhaba üzerinde **nesil** sayfasında, hello aygıt resim türünü seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="092a8-161">On hello **Specify generation** page, choose hello device image type, and then click **Next**.</span></span> <span data-ttu-id="092a8-162">Windows Server 2008 R2 kullanıyorsanız, bu sayfa görünmez.</span><span class="sxs-lookup"><span data-stu-id="092a8-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="092a8-163">Seçin **2. nesil** Windows Server 2012 veya sonraki bir .vhdx görüntüsü yüklediyseniz.</span><span class="sxs-lookup"><span data-stu-id="092a8-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="092a8-164">Seçin **1. nesil** Windows Server 2008 R2 veya sonraki bir .vhd görüntüsü yüklediyseniz.</span><span class="sxs-lookup"><span data-stu-id="092a8-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="092a8-165">Merhaba üzerinde **atamak bellek** sayfasında, belirtin bir **başlangıç belleği** , en az **8192 MB**olmayan dinamik belleği etkinleştirme ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="092a8-165">On hello **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="092a8-166">Merhaba üzerinde **ağ yapılandırma** sayfasında, bağlı toohello Internet olan hello sanal anahtar belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="092a8-166">On hello **Configure networking** page, specify hello virtual switch that is connected toohello Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="092a8-167">Merhaba üzerinde **sanal sabit diski bağlayın** sayfasında, **varolan bir sanal sabit diski kullanmak**hello sanal dizinin görüntü (.vhdx veya .vhd) hello konumunu belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="092a8-167">On hello **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify hello location of hello virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="092a8-168">Gözden geçirme hello **Özet** ve ardından **son** toocreate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="092a8-168">Review hello **Summary** and then click **Finish** toocreate hello virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="092a8-169">toomeet hello en düşük gereksinimler, 4 çekirdek gerekir.</span><span class="sxs-lookup"><span data-stu-id="092a8-169">toomeet hello minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="092a8-170">tooadd 4 sanal işlemci, ana bilgisayar sisteminizin hello seçin **Hyper-V Yöneticisi'ni** penceresi.</span><span class="sxs-lookup"><span data-stu-id="092a8-170">tooadd 4 virtual processors, select your host system in hello **Hyper-V Manager** window.</span></span> <span data-ttu-id="092a8-171">Merhaba hello listesi bölümündeki sağ bölmede **sanal makineleri**, az önce oluşturduğunuz hello sanal makine bulun.</span><span class="sxs-lookup"><span data-stu-id="092a8-171">In hello right-pane under hello list of **Virtual Machines**, locate hello virtual machine you just created.</span></span> <span data-ttu-id="092a8-172">Seçin ve hello makine adını sağ tıklatın ve seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="092a8-172">Select and right-click hello machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="092a8-173">Merhaba üzerinde **ayarları** sayfasında hello sol bölmede, tıklatın **İşlemci**.</span><span class="sxs-lookup"><span data-stu-id="092a8-173">On hello **Settings** page, in hello left-pane, click **Processor**.</span></span> <span data-ttu-id="092a8-174">Merhaba sağ bölmede, ayarlamak **sanal işlemcilerin sayısı** too4 (veya daha fazla).</span><span class="sxs-lookup"><span data-stu-id="092a8-174">In hello right-pane, set **number of virtual processors** too4 (or more).</span></span> <span data-ttu-id="092a8-175">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="092a8-176">toomeet hello en düşük gereksinimler, tooadd 500 GB sanal veri diski de gerekir.</span><span class="sxs-lookup"><span data-stu-id="092a8-176">toomeet hello minimum requirements, you also need tooadd a 500 GB virtual data disk.</span></span> <span data-ttu-id="092a8-177">Merhaba, **ayarları** sayfa:</span><span class="sxs-lookup"><span data-stu-id="092a8-177">In hello **Settings** page:</span></span>

    1. <span data-ttu-id="092a8-178">Merhaba sol bölmesinde seçin **SCSI denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="092a8-178">In hello left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="092a8-179">Merhaba sağ bölmede seçin **sabit sürücü** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="092a8-179">In hello right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="092a8-180">Merhaba üzerinde **sabit sürücü** sayfası, select hello **sanal sabit disk** seçeneğini ve tıklayın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="092a8-180">On hello **Hard drive** page, select hello **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="092a8-181">Merhaba **Yeni Sanal Sabit Disk Sihirbazı** başlatır.</span><span class="sxs-lookup"><span data-stu-id="092a8-181">hello **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="092a8-182">Merhaba üzerinde **başlamadan önce** hello Yeni Sanal Sabit Disk Sihirbazı, sayfasını tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="092a8-182">On hello **Before you begin** page of hello New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="092a8-183">Merhaba üzerinde **Disk biçimi seçin sayfasında**, hello varsayılan seçeneği kabul **VHDX** biçimi.</span><span class="sxs-lookup"><span data-stu-id="092a8-183">On hello **Choose Disk Format page**, accept hello default option of **VHDX** format.</span></span> <span data-ttu-id="092a8-184">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-184">Click **Next**.</span></span> <span data-ttu-id="092a8-185">Bu ekran, Windows Server 2008 R2 çalıştıran, sunulan değil.</span><span class="sxs-lookup"><span data-stu-id="092a8-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="092a8-186">Merhaba üzerinde **Disk türünü seçin sayfasında**, sanal sabit disk türü olarak ayarlamak **dinamik olarak genişletilen** (önerilen).</span><span class="sxs-lookup"><span data-stu-id="092a8-186">On hello **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="092a8-187">**Boyutu sabit** disk çalışır ancak toowait uzun bir süre gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-187">**Fixed size** disk would work but you may need toowait a long time.</span></span> <span data-ttu-id="092a8-188">Merhaba kullanmamanızı öneririz **Differencing** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="092a8-188">We recommend that you do not use hello **Differencing** option.</span></span> <span data-ttu-id="092a8-189">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-189">Click **Next**.</span></span> <span data-ttu-id="092a8-190">Windows Server 2012 R2 ve Windows Server 2012'de, **dinamik olarak genişletilen** Windows Server 2008 R2'de hello varsayılan iken hello varsayılan seçenektir **boyutu sabit**.</span><span class="sxs-lookup"><span data-stu-id="092a8-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is hello default option whereas in Windows Server 2008 R2, hello default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="092a8-191">Merhaba üzerinde **ad ve konum belirtin** sayfasında, sağlayan bir **adı** yanı **konumu** (tooone göz atabilirsiniz) hello veri diski için.</span><span class="sxs-lookup"><span data-stu-id="092a8-191">On hello **Specify Name and Location** page, provide a **name** as well as **location** (you can browse tooone) for hello data disk.</span></span> <span data-ttu-id="092a8-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="092a8-193">Merhaba üzerinde **Disk yapılandırma** sayfası, select hello seçeneği **bir yeni boş sanal sabit disk Oluştur** ve hello boyutu olarak belirtin **500 GB** (veya daha fazla).</span><span class="sxs-lookup"><span data-stu-id="092a8-193">On hello **Configure Disk** page, select hello option **Create a new blank virtual hard disk** and specify hello size as **500 GB** (or more).</span></span> <span data-ttu-id="092a8-194">500 GB hello minimum gereksinim olsa da, her zaman daha büyük bir disk sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="092a8-194">While 500 GB is hello minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="092a8-195">Olamaz genişletmek veya bir kez sağlanan hello diski küçültmeye unutmayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-195">Note that you cannot expand or shrink hello disk once provisioned.</span></span> <span data-ttu-id="092a8-196">Disk tooprovision hello boyutu hakkında daha fazla bilgi için hello hello boyutlandırma bölümünde gözden [en iyi yöntemler belge](storsimple-ova-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="092a8-196">For more information on hello size of disk tooprovision, review hello sizing section in hello [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="092a8-197">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="092a8-198">Merhaba üzerinde **Özet** sayfasında, sanal veri diskinizi hello ayrıntılarını gözden geçirin ve memnun tıklatmak **son** toocreate hello disk.</span><span class="sxs-lookup"><span data-stu-id="092a8-198">On hello **Summary** page, review hello details of your virtual data disk and if satisfied, click **Finish** toocreate hello disk.</span></span> <span data-ttu-id="092a8-199">Merhaba sihirbaz kapanır ve bir sanal sabit disk tooyour makine eklenir.</span><span class="sxs-lookup"><span data-stu-id="092a8-199">hello wizard closes and a virtual hard disk is added tooyour machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="092a8-200">Toohello iade **ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="092a8-200">Return toohello **Settings** page.</span></span> <span data-ttu-id="092a8-201">Tıklatın **Tamam** tooclose hello **ayarları** sayfasında ve tooHyper-V Yöneticisi'ni penceresine dönün.</span><span class="sxs-lookup"><span data-stu-id="092a8-201">Click **OK** tooclose hello **Settings** page and return tooHyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a><span data-ttu-id="092a8-202">3. adım: hello sanal dizinin başlatın ve hello IP Al</span><span class="sxs-lookup"><span data-stu-id="092a8-202">Step 3: Start hello virtual array and get hello IP</span></span>
<span data-ttu-id="092a8-203">Aşağıdaki adımları toostart hello sanal dizinizi gerçekleştirmek ve tooit bağlanın.</span><span class="sxs-lookup"><span data-stu-id="092a8-203">Perform hello following steps toostart your virtual array and connect tooit.</span></span>

#### <a name="toostart-hello-virtual-array"></a><span data-ttu-id="092a8-204">toostart hello sanal dizinin</span><span class="sxs-lookup"><span data-stu-id="092a8-204">toostart hello virtual array</span></span>
1. <span data-ttu-id="092a8-205">Merhaba sanal dizinin başlatın.</span><span class="sxs-lookup"><span data-stu-id="092a8-205">Start hello virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="092a8-206">Hello aygıt çalıştırdıktan sonra hello cihaz seçin, sağ tıklayın ve seçin **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="092a8-206">After hello device is running, select hello device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="092a8-207">Merhaba aygıt toobe hazır 5-10 dakika toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-207">You may have toowait 5-10 minutes for hello device toobe ready.</span></span> <span data-ttu-id="092a8-208">Bir durum iletisi hello konsol tooindicate hello ilerleme görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="092a8-208">A status message is displayed on hello console tooindicate hello progress.</span></span> <span data-ttu-id="092a8-209">Merhaba cihaz hazır olduktan sonra çok Git**eylem**.</span><span class="sxs-lookup"><span data-stu-id="092a8-209">After hello device is ready, go too**Action**.</span></span> <span data-ttu-id="092a8-210">Tuşuna `Ctrl + Alt + Delete` toohello sanal dizinin toolog.</span><span class="sxs-lookup"><span data-stu-id="092a8-210">Press `Ctrl + Alt + Delete` toolog in toohello virtual array.</span></span> <span data-ttu-id="092a8-211">Merhaba varsayılan kullanıcı *StorSimpleAdmin* ve hello varsayılan parola *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="092a8-211">hello default user is *StorSimpleAdmin* and hello default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="092a8-212">Güvenlik nedenleriyle hello ilk oturum açmada hello cihaz Yönetici parolasının süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="092a8-212">For security reasons, hello device administrator password expires at hello first logon.</span></span> <span data-ttu-id="092a8-213">İstendiğinde toochange hello parola olur.</span><span class="sxs-lookup"><span data-stu-id="092a8-213">You are prompted toochange hello password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="092a8-214">En az 8 karakter içeren bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="092a8-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="092a8-215">Merhaba parola en az 3 4 gereksinimlerine hello dışında karşılaması gerekir: büyük harf, küçük harfler, sayısal ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="092a8-215">hello password must satisfy at least 3 out of hello following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="092a8-216">Merhaba parola tooconfirm yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="092a8-216">Reenter hello password tooconfirm it.</span></span> <span data-ttu-id="092a8-217">Bu hello parolanın değiştirilmesi bildirilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-217">You are notified that hello password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="092a8-218">Merhaba parola başarıyla değiştirildikten sonra hello sanal dizinin yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="092a8-218">After hello password is successfully changed, hello virtual array may restart.</span></span> <span data-ttu-id="092a8-219">Merhaba aygıt toostart bekleyin.</span><span class="sxs-lookup"><span data-stu-id="092a8-219">Wait for hello device toostart.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="092a8-220">Merhaba cihazın Hello Windows PowerShell konsolu ile birlikte bir ilerleme çubuğu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="092a8-220">hello Windows PowerShell console of hello device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="092a8-221">Adım 6-8 yalnızca yukarı DHCP olmayan ortamda önyüklemesi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="092a8-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="092a8-222">Bir DHCP ortamında varsa, bu adımları atlayın ve toostep 9 gidin.</span><span class="sxs-lookup"><span data-stu-id="092a8-222">If you are in a DHCP environment, then skip these steps and go toostep 9.</span></span> <span data-ttu-id="092a8-223">Cihazınızı DHCP olmayan ortamda yukarı önyüklendiğinde ekran aşağıdaki hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="092a8-223">If you booted up your device in non-DHCP environment, you will see hello following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="092a8-224">Ardından, hello ağ yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="092a8-224">Next, configure hello network.</span></span>
7. <span data-ttu-id="092a8-225">Kullanım hello `Get-HcsIpAddress` sanal dizinizi etkin toolist hello ağ arabirimleri komutu.</span><span class="sxs-lookup"><span data-stu-id="092a8-225">Use hello `Get-HcsIpAddress` command toolist hello network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="092a8-226">Cihazınızı etkin tek bir ağ arabirimi varsa, hello varsayılan atanan ad toothis arabirimidir `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="092a8-226">If your device has a single network interface enabled, hello default name assigned toothis interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="092a8-227">Kullanım hello `Set-HcsIpAddress` cmdlet tooconfigure hello ağ.</span><span class="sxs-lookup"><span data-stu-id="092a8-227">Use hello `Set-HcsIpAddress` cmdlet tooconfigure hello network.</span></span> <span data-ttu-id="092a8-228">Aşağıdaki örnek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="092a8-228">See hello following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="092a8-229">Merhaba ilk Kurulum tamamlandıktan ve hello aygıt yukarı önyüklendikten sonra hello aygıt başlık metni görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="092a8-229">After hello initial setup is complete and hello device has booted up, you will see hello device banner text.</span></span> <span data-ttu-id="092a8-230">Başlangıç IP adresi ve hello başlık metni toomanage hello aygıtı görüntülenen hello URL'sini not edin.</span><span class="sxs-lookup"><span data-stu-id="092a8-230">Make a note of hello IP address and hello URL displayed in hello banner text toomanage hello device.</span></span> <span data-ttu-id="092a8-231">Bu IP adresi tooconnect toohello web sanal dizinin ve tam hello yerel kurulumu ve kayıt kullanıcı arabirimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="092a8-231">Use this IP address tooconnect toohello web UI of your virtual array and complete hello local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="092a8-232">(İsteğe bağlı) Yalnızca Cihazınızı hello Bulutu dağıtıyorsanız bu adımı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="092a8-232">(Optional) Perform this step only if you are deploying your device in hello Government Cloud.</span></span> <span data-ttu-id="092a8-233">Şimdi Cihazınızda hello Amerika Birleşik Devletleri Federal Bilgi İşleme Standardı (FIPS) mod olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="092a8-233">You will now enable hello United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="092a8-234">Merhaba FIPS 140 standardı, gizli verilerin hello koruma için BİZE Federal hükümeti bilgisayar sistemleri tarafından kullanım için onaylanan şifreleme algoritmalarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="092a8-234">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span>

    1. <span data-ttu-id="092a8-235">cmdlet aşağıdaki hello çalıştırmak tooenable hello FIPS modunda:</span><span class="sxs-lookup"><span data-stu-id="092a8-235">tooenable hello FIPS mode, run hello following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="092a8-236">Böylece Hello şifreleme doğrulama etkili hello FIPS modunda etkinleştirdikten sonra Cihazınızı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="092a8-236">Reboot your device after you have enabled hello FIPS mode so that hello cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="092a8-237">Etkinleştirmek veya FIPS modundayken, Cihazınızda devre dışı.</span><span class="sxs-lookup"><span data-stu-id="092a8-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="092a8-238">FIPS ve FIPS olmayan mod arasında değişen hello aygıt desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="092a8-238">Alternating hello device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="092a8-239">Cihazınızı hello en düşük yapılandırma gereksinimlerini karşılamıyorsa, aşağıdaki hata hello Başlık metin (aşağıda gösterilen) hello bakın.</span><span class="sxs-lookup"><span data-stu-id="092a8-239">If your device does not meet hello minimum configuration requirements, you see hello following error in hello banner text (shown below).</span></span> <span data-ttu-id="092a8-240">Merhaba makine sahip en düşük gereksinimler hello yeterli kaynakları toomeet olması hello aygıt yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="092a8-240">Modify hello device configuration so that hello machine has adequate resources toomeet hello minimum requirements.</span></span> <span data-ttu-id="092a8-241">Ardından, yeniden başlatın ve toohello aygıtı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="092a8-241">You can then restart and connect toohello device.</span></span> <span data-ttu-id="092a8-242">Toohello en düşük yapılandırma gereksinimlerini başvuran [1. adım: hello ana bilgisayar sistemi minimum sanal dizinin gereksinimlerini karşıladığından emin olmak](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="092a8-242">Refer toohello minimum configuration requirements in [Step 1: Ensure that hello host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="092a8-243">Başka bir hata hello yerel web kullanıcı Arabirimi kullanılarak hello başlangıç yapılandırması sırasında yüz, iş akışları şu toohello başvurun:</span><span class="sxs-lookup"><span data-stu-id="092a8-243">If you face any other error during hello initial configuration using hello local web UI, refer toohello following workflows:</span></span>

* <span data-ttu-id="092a8-244">Tanılama çok testler[web kullanıcı Arabirimi Kurulumu sorunlarını giderme](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="092a8-244">Run diagnostic tests too[troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="092a8-245">[Günlük paketi oluşturmak ve günlük dosyalarını görüntülemek](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="092a8-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="092a8-246">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="092a8-246">Next steps</span></span>
* [<span data-ttu-id="092a8-247">Dosya sunucusu olarak StorSimple sanal dizinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="092a8-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="092a8-248">StorSimple sanal dizinizi bir iSCSI sunucusu olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="092a8-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
