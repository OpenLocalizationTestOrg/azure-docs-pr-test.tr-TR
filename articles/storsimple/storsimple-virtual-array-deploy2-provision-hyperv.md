---
title: "Hyper-V sanal dizisinde StorSimple sağlama | Microsoft Docs"
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
ms.openlocfilehash: bad431c8958f7d381bb9c0410caa3a57c6e75c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="bfbf1-103">StorSimple sanal dizinin - sağlama Hyper-v dağıtma</span><span class="sxs-lookup"><span data-stu-id="bfbf1-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="bfbf1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bfbf1-104">Overview</span></span>
<span data-ttu-id="bfbf1-105">Bu öğretici, bir StorSimple sanal dizisi Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde sağlayacak açıklar.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="bfbf1-106">Bu makale, Azure portalı ve Microsoft Azure kamu bulut StorSimple sanal diziler dağıtımda için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="bfbf1-107">Sanal bir dizi yapılandırmak ve sağlamak için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-107">You need administrator privileges to provision and configure a virtual array.</span></span> <span data-ttu-id="bfbf1-108">Sağlama ve ilk kurulumu tamamlamak için yaklaşık 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="bfbf1-109">Sağlama önkoşulları</span><span class="sxs-lookup"><span data-stu-id="bfbf1-109">Provisioning prerequisites</span></span>
<span data-ttu-id="bfbf1-110">Burada, Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde sanal bir dizi sağlamak için gereken önkoşullar bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="bfbf1-111">StorSimple Cihaz Yöneticisi hizmeti için</span><span class="sxs-lookup"><span data-stu-id="bfbf1-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="bfbf1-112">Başlamadan önce aşağıdakilerden emin olun:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="bfbf1-113">Tüm adımları tamamladınız [StorSimple sanal dizisi için portal hazırlama](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="bfbf1-114">Hyper-V için sanal dizinin görüntüyü Azure portalından yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="bfbf1-115">Daha fazla bilgi için bkz: **3. adım: sanal dizinin görüntüyü indirmeyi** , [StorSimple sanal dizinin kılavuzu için portal hazırlamak](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="bfbf1-116">StorSimple sanal dizi çalışan yazılımın yalnızca StorSimple cihaz Yöneticisi hizmeti ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="bfbf1-117">StorSimple sanal dizi için</span><span class="sxs-lookup"><span data-stu-id="bfbf1-117">For the StorSimple Virtual Array</span></span>
<span data-ttu-id="bfbf1-118">Sanal bir dizi dağıtmadan önce emin olun:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="bfbf1-119">Hyper-olabilecek V Windows Server 2008 R2 veya üstü çalıştıran bir ana bilgisayar sistemine erişimi sağlamak için kullanılan bir cihaz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="bfbf1-120">Ana bilgisayar sistemi sanal dizinizi sağlamak için aşağıdaki kaynaklara ayrılması yapabiliyor:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-120">The host system is able to dedicate the following resources to provision your virtual array:</span></span>

  * <span data-ttu-id="bfbf1-121">4 çekirdek en az.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="bfbf1-122">En az 8 GB RAM.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="bfbf1-123">Dosya sunucusu olarak sanal dizinin yapılandırmayı planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="bfbf1-124">16 GB RAM, 2-4 milyon dosyaları desteklemek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-124">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="bfbf1-125">Bir ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-125">One network interface.</span></span>
  * <span data-ttu-id="bfbf1-126">Veri için 500 GB sanal disk.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="bfbf1-127">Veri merkezindeki ağ için</span><span class="sxs-lookup"><span data-stu-id="bfbf1-127">For the network in the datacenter</span></span>
<span data-ttu-id="bfbf1-128">Başlamadan önce StorSimple sanal dizinin dağıtmak ve veri merkezi ağ uygun şekilde yapılandırmak için ağ gereksinimlerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span></span> <span data-ttu-id="bfbf1-129">Daha fazla bilgi için bkz: [StorSimple sanal ağ gereksinimleri dizi](storsimple-ova-system-requirements.md#networking-requirements).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="bfbf1-130">Adım adım sağlama</span><span class="sxs-lookup"><span data-stu-id="bfbf1-130">Step-by-step provisioning</span></span>
<span data-ttu-id="bfbf1-131">Sağlamak ve sanal bir dizi bağlanmak için aşağıdaki adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-131">To provision and connect to a virtual array, you need to perform the following steps:</span></span>

1. <span data-ttu-id="bfbf1-132">Ana bilgisayar sistemi minimum sanal dizinin gereksinimlerini karşılamak için yeterli kaynaklara sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span></span>
2. <span data-ttu-id="bfbf1-133">Hiper yönetici sanal bir dizide sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="bfbf1-134">Sanal dizinin başlatın ve IP adresi alın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-134">Start the virtual array and get the IP address.</span></span>

<span data-ttu-id="bfbf1-135">Bu adımların her biri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-135">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="bfbf1-136">1. adım: ana bilgisayar sistemi minimum sanal dizinin gereksinimleri karşıladığından emin olun</span><span class="sxs-lookup"><span data-stu-id="bfbf1-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="bfbf1-137">Sanal bir dizi oluşturmak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-137">To create a virtual array, you need:</span></span>

* <span data-ttu-id="bfbf1-138">Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 SP1 yüklü Hyper-V rolü.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="bfbf1-139">Microsoft Windows İstemcisi üzerindeki Microsoft Hyper-V Yöneticisi ana bilgisayara bağlı.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="bfbf1-140">Sanal dizinin oluşturmakta olduğunuz temel alınan donanım (ana bilgisayar sistemi) aşağıdaki kaynaklar sanal dizinizi ayrılması mümkün olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span></span>

* <span data-ttu-id="bfbf1-141">4 çekirdek en az.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="bfbf1-142">En az 8 GB RAM.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="bfbf1-143">Dosya sunucusu olarak sanal dizinin yapılandırmayı planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="bfbf1-144">16 GB RAM, 2-4 milyon dosyaları desteklemek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-144">You need 16 GB RAM to support 2 - 4 million files.</span></span>
* <span data-ttu-id="bfbf1-145">Bir ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-145">One network interface.</span></span>
* <span data-ttu-id="bfbf1-146">Sistem verileri için 500 GB sanal disk.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="bfbf1-147">2. adım: hiper yönetici sanal bir dizide sağlama</span><span class="sxs-lookup"><span data-stu-id="bfbf1-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="bfbf1-148">Bir aygıt, hiper yönetici sağlamak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-148">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-array"></a><span data-ttu-id="bfbf1-149">Sanal bir dizi sağlamak için</span><span class="sxs-lookup"><span data-stu-id="bfbf1-149">To provision a virtual array</span></span>
1. <span data-ttu-id="bfbf1-150">Windows Server ana bilgisayarında sanal dizinin görüntüyü bir yerel sürücüye kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-150">On your Windows Server host, copy the virtual array image to a local drive.</span></span> <span data-ttu-id="bfbf1-151">Bu görüntü (VHD veya VHDX) Azure portalı üzerinden yüklenen.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span></span> <span data-ttu-id="bfbf1-152">Sonraki yordamda bu görüntüyü kullanma gibi görüntü kopyaladığınız konumunu not edin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>
2. <span data-ttu-id="bfbf1-153">Açık **Sunucu Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-153">Open **Server Manager**.</span></span> <span data-ttu-id="bfbf1-154">Sağ alt köşesinde üst tıklatın **Araçları** seçip **Hyper-V Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="bfbf1-155">Windows Server 2008 R2 çalıştırıyorsanız, Hyper-V Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="bfbf1-156">Sunucu Yöneticisi'nde **rolleri > Hyper-V > Hyper-V Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="bfbf1-157">İçinde **Hyper-V Yöneticisi'ni**, kapsam bölmesinde bağlam menüsünü açmak için sistem düğümünü sağ tıklatın ve ardından **yeni** > **sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="bfbf1-158">Üzerinde **başlamadan önce** sayfasında yeni sanal makine Sihirbazı'nın, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="bfbf1-159">Üzerinde **ad ve konum belirtin** sayfasında, sağlayan bir **adı** sanal dizini.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="bfbf1-160">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="bfbf1-161">Üzerinde **nesil** sayfasında, cihaz resim türünü seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span></span> <span data-ttu-id="bfbf1-162">Windows Server 2008 R2 kullanıyorsanız, bu sayfa görünmez.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="bfbf1-163">Seçin **2. nesil** Windows Server 2012 veya sonraki bir .vhdx görüntüsü yüklediyseniz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="bfbf1-164">Seçin **1. nesil** Windows Server 2008 R2 veya sonraki bir .vhd görüntüsü yüklediyseniz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="bfbf1-165">Üzerinde **atamak bellek** sayfasında, belirtin bir **başlangıç belleği** , en az **8192 MB**olmayan dinamik belleği etkinleştirme ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="bfbf1-166">Üzerinde **ağ yapılandırma** sayfasında, Internet'e bağlı bir sanal anahtar belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="bfbf1-167">Üzerinde **sanal sabit diski bağlayın** sayfasında, **varolan bir sanal sabit diski kullanmak**(.vhdx veya .vhd) sanal dizinin görüntü konumunu belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="bfbf1-168">Gözden geçirme **Özet** ve ardından **son** sanal makine oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="bfbf1-169">En düşük gereksinimleri karşılamak için 4 çekirdek gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-169">To meet the minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="bfbf1-170">4 sanal işlemci eklemek için ana bilgisayar sisteminizin seçin **Hyper-V Yöneticisi'ni** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span></span> <span data-ttu-id="bfbf1-171">Listesini bölümündeki sağ bölmede **sanal makineleri**, az önce oluşturduğunuz sanal makine bulun.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="bfbf1-172">Seçin ve makine adını sağ tıklatın ve seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-172">Select and right-click the machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="bfbf1-173">Üzerinde **ayarları** sol bölmedeki sayfasını tıklatın **İşlemci**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-173">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="bfbf1-174">Sağ bölmede, ayarlayın **sanal işlemcilerin sayısı** 4 (veya daha fazla).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="bfbf1-175">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="bfbf1-176">En düşük gereksinimleri karşılamak için de bir 500 GB sanal veri diski eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="bfbf1-177">İçinde **ayarları** sayfa:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-177">In the **Settings** page:</span></span>

    1. <span data-ttu-id="bfbf1-178">Sol bölmede seçin **SCSI denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-178">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="bfbf1-179">Sağ bölmede seçin **sabit sürücü** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-179">In the right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="bfbf1-180">Üzerinde **sabit sürücü** sayfasında, **sanal sabit disk** seçeneğini ve tıklayın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="bfbf1-181">**Yeni Sanal Sabit Disk Sihirbazı** başlatır.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-181">The **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="bfbf1-182">Üzerinde **başlamadan önce** sayfasında yeni sanal sabit Disk Sihirbazı'nın tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="bfbf1-183">Üzerinde **Disk biçimi seçin sayfasında**, varsayılan seçeneği kabul **VHDX** biçimi.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="bfbf1-184">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-184">Click **Next**.</span></span> <span data-ttu-id="bfbf1-185">Bu ekran, Windows Server 2008 R2 çalıştıran, sunulan değil.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="bfbf1-186">Üzerinde **Disk türünü seçin sayfasında**, sanal sabit disk türü olarak ayarlamak **dinamik olarak genişletilen** (önerilen).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="bfbf1-187">**Boyutu sabit** disk çalışır ancak uzun bir süre beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-187">**Fixed size** disk would work but you may need to wait a long time.</span></span> <span data-ttu-id="bfbf1-188">Değil kullanmanız önerilir **Differencing** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-188">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="bfbf1-189">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-189">Click **Next**.</span></span> <span data-ttu-id="bfbf1-190">Windows Server 2012 R2 ve Windows Server 2012'de, **dinamik olarak genişletilen** Windows Server 2008 R2'de varsayılan iken varsayılan seçenektir **boyutu sabit**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="bfbf1-191">Üzerinde **ad ve konum belirtin** sayfasında, sağlayan bir **adı** yanı **konumu** (birine gözatabilirsiniz) veri diski için.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="bfbf1-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="bfbf1-193">Üzerinde **Disk yapılandırma** sayfasında, seçeneğini **bir yeni boş sanal sabit disk Oluştur** ve boyutu olarak belirtin **500 GB** (veya daha fazla).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="bfbf1-194">500 GB en düşük gereksinim olsa da, her zaman daha büyük bir disk sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="bfbf1-195">Olamaz genişletmek veya bir kez sağlanan diski küçültmeye unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-195">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="bfbf1-196">Sağlamak için disk boyutu hakkında daha fazla bilgi için boyutlandırma bölümünde gözden [en iyi yöntemler belge](storsimple-ova-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="bfbf1-197">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="bfbf1-198">Üzerinde **Özet** sayfasında, sanal veri diskinizi ayrıntılarını gözden geçirin ve memnun tıklatmak **son** disk oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="bfbf1-199">Sihirbaz kapanır ve bir sanal sabit disk makinenize eklenir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-199">The wizard closes and a virtual hard disk is added to your machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="bfbf1-200">Geri dönüp **ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-200">Return to the **Settings** page.</span></span> <span data-ttu-id="bfbf1-201">Tıklatın **Tamam** kapatmak için **ayarları** sayfasında ve Hyper-V Yöneticisi'ni penceresine dönün.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-array-and-get-the-ip"></a><span data-ttu-id="bfbf1-202">3. adım: sanal dizinin başlatın ve IP Al</span><span class="sxs-lookup"><span data-stu-id="bfbf1-202">Step 3: Start the virtual array and get the IP</span></span>
<span data-ttu-id="bfbf1-203">Sanal dizinizi başlatmak ve buna bağlanmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-203">Perform the following steps to start your virtual array and connect to it.</span></span>

#### <a name="to-start-the-virtual-array"></a><span data-ttu-id="bfbf1-204">Sanal dizinin başlatmak için</span><span class="sxs-lookup"><span data-stu-id="bfbf1-204">To start the virtual array</span></span>
1. <span data-ttu-id="bfbf1-205">Sanal dizinin başlatın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-205">Start the virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="bfbf1-206">Cihaz çalıştırdıktan sonra cihazı seçin, sağ tıklatın ve seçin **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-206">After the device is running, select the device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="bfbf1-207">Cihazın hazır olması 5-10 dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-207">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="bfbf1-208">Bir durum iletisi ilerlemeyi göstermek için konsolda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-208">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="bfbf1-209">Cihaz hazır olduktan sonra Git **eylem**.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-209">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="bfbf1-210">Tuşuna `Ctrl + Alt + Delete` sanal diziye oturum açmak için.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span></span> <span data-ttu-id="bfbf1-211">Varsayılan kullanıcı *StorSimpleAdmin* ve varsayılan parola *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="bfbf1-212">Güvenlik nedenleriyle ilk oturum açmada cihaz Yönetici parolasının süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-212">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="bfbf1-213">Parolayı değiştirmek için istenir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-213">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="bfbf1-214">En az 8 karakter içeren bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="bfbf1-215">Parola en az 3 dışında aşağıdaki 4 gereksinimleri karşılaması gerekir: büyük harf, küçük harfler, sayısal ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="bfbf1-216">Onaylamak için parolayı yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-216">Reenter the password to confirm it.</span></span> <span data-ttu-id="bfbf1-217">Parolanın değiştirilmesi bildirilir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-217">You are notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="bfbf1-218">Parola başarıyla değiştirildikten sonra sanal dizinin yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-218">After the password is successfully changed, the virtual array may restart.</span></span> <span data-ttu-id="bfbf1-219">Cihazın başlatmak için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-219">Wait for the device to start.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="bfbf1-220">Cihazın Windows PowerShell konsolu ile birlikte bir ilerleme çubuğu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="bfbf1-221">Adım 6-8 yalnızca yukarı DHCP olmayan ortamda önyüklemesi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="bfbf1-222">Bir DHCP ortamında varsa, bu adımları atlayın ve 9. adıma gidin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="bfbf1-223">Cihazınızı DHCP olmayan ortamda yukarı önyüklendiğinde aşağıdaki ekranı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="bfbf1-224">Ardından, ağ yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-224">Next, configure the network.</span></span>
7. <span data-ttu-id="bfbf1-225">Kullanım `Get-HcsIpAddress` sanal dizinizi etkin ağ arabirimleri listelemek için komutu.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="bfbf1-226">Cihazınızı etkin tek bir ağ arabirimi varsa, bu arabirime atanmış varsayılan addır `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="bfbf1-227">Kullanım `Set-HcsIpAddress` ağı yapılandırmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="bfbf1-228">Aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-228">See the following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="bfbf1-229">İlk kurulumu tamamlandıktan ve cihaz yukarı önyüklendikten sonra aygıt başlık metni görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="bfbf1-230">IP adresi ve cihaz yönetmek için başlık metni görüntülenen URL not edin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="bfbf1-231">Web kullanıcı Arabirimine sanal dizinin bağlanmak ve yerel kurulumunu ve kaydını tamamlamak için bu IP adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="bfbf1-232">(İsteğe bağlı) Yalnızca Cihazınızı kamu bulutta dağıtıyorsanız bu adımı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="bfbf1-233">Şimdi Cihazınızda Amerika Birleşik Devletleri Federal Bilgi İşleme Standardı (FIPS) mod olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="bfbf1-234">FIPS 140 standardı, önemli verilerin korunması için BİZE Federal hükümeti bilgisayar sistemleri tarafından kullanım için onaylanan şifreleme algoritmalarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="bfbf1-235">FIPS modunda etkinleştirmek için aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-235">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="bfbf1-236">Böylece şifreleme doğrulama etkili FIPS modunda etkinleştirdikten sonra Cihazınızı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="bfbf1-237">Etkinleştirmek veya FIPS modundayken, Cihazınızda devre dışı.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="bfbf1-238">Cihaz FIPS ve FIPS olmayan mod arasında geçiş yapma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="bfbf1-239">Cihazınızı minimum yapılandırma gereksinimlerini karşılamıyorsa, (aşağıda gösterilen) başlık metni aşağıdaki hatayı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span></span> <span data-ttu-id="bfbf1-240">Böylece makine en düşük gereksinimleri karşılamak için yeterli kaynaklara sahip aygıt yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="bfbf1-241">Ardından, yeniden başlatın ve cihaza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="bfbf1-241">You can then restart and connect to the device.</span></span> <span data-ttu-id="bfbf1-242">Minimum yapılandırma gereksinimlerini başvurmak [1. adım: ana bilgisayar sistemi minimum sanal dizinin gereksinimlerini karşıladığından emin olmak](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="bfbf1-243">Yerel web kullanıcı Arabirimi kullanılarak yapılan başlangıç yapılandırması sırasında başka bir hata yüz, aşağıdaki iş akışları için başvurun:</span><span class="sxs-lookup"><span data-stu-id="bfbf1-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="bfbf1-244">Tanılama testleri [web kullanıcı Arabirimi Kurulumu sorunlarını giderme](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="bfbf1-245">[Günlük paketi oluşturmak ve günlük dosyalarını görüntülemek](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="bfbf1-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfbf1-246">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bfbf1-246">Next steps</span></span>
* [<span data-ttu-id="bfbf1-247">Dosya sunucusu olarak StorSimple sanal dizinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="bfbf1-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="bfbf1-248">StorSimple sanal dizinizi bir iSCSI sunucusu olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="bfbf1-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
