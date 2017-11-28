---
title: "StorSimple sanal dizini aaaPortal hazırlığı | Microsoft Docs"
description: "İlk öğretici toodeploy StorSimple sanal dizinin hello Azure portal hazırlanmasını içerir"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a><span data-ttu-id="2a54e-103">StorSimple sanal dizinin dağıtma - hello Azure portal hazırlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-103">Deploy StorSimple Virtual Array - Prepare hello Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="2a54e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2a54e-104">Overview</span></span>

<span data-ttu-id="2a54e-105">Gerekli dağıtım öğreticileri hello serideki makalesine ilk hello budur toocompletely sanal dizinizi bir dosya sunucusu veya hello Resource Manager modelini kullanarak bir iSCSI sunucu olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-105">This is hello first article in hello series of deployment tutorials required toocompletely deploy your virtual array as a file server or an iSCSI server using hello Resource Manager model.</span></span> <span data-ttu-id="2a54e-106">Bu makalede hello gerekli hazırlık toocreate ve, StorSimple cihaz Yöneticisi hizmeti önceki tooprovisioning sanal bir dizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-106">This article describes hello preparation required toocreate and configure your StorSimple Device Manager service prior tooprovisioning a virtual array.</span></span> <span data-ttu-id="2a54e-107">Bu makalede ayrıca tooa dağıtım yapılandırma denetim listesi ve yapılandırma önkoşulları bağlar.</span><span class="sxs-lookup"><span data-stu-id="2a54e-107">This article also links out tooa deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="2a54e-108">Kurulum ve yapılandırma yönetici ayrıcalıkları toocomplete hello işlemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-108">You need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="2a54e-109">Başlamadan önce hello dağıtım yapılandırma denetim listesini gözden geçirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="2a54e-109">We recommend that you review hello deployment configuration checklist before you begin.</span></span> <span data-ttu-id="2a54e-110">Merhaba portal hazırlık 10 dakikadan daha kısa sürer.</span><span class="sxs-lookup"><span data-stu-id="2a54e-110">hello portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="2a54e-111">Bu makalede yayımlanmış hello bilgiler, StorSimple sanal hello Azure portal dizilerde ve Microsoft Azure kamu bulut toohello dağıtımını geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-111">hello information published in this article applies toohello deployment of StorSimple Virtual Arrays in hello Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="2a54e-112">başlarken</span><span class="sxs-lookup"><span data-stu-id="2a54e-112">Get started</span></span>
<span data-ttu-id="2a54e-113">Merhaba dağıtımı iş akışı hello portal hazırlama, sanallaştırılmış ortamınızdaki sanal bir dizi sağlama ve hello Kurulumu Tamamlanıyor oluşur.</span><span class="sxs-lookup"><span data-stu-id="2a54e-113">hello deployment workflow consists of preparing hello portal, provisioning a virtual array in your virtualized environment, and completing hello setup.</span></span> <span data-ttu-id="2a54e-114">Merhaba StorSimple sanal dizinin dağıtım bir dosya sunucusu veya bir iSCSI sunucusu olarak kullanmaya tooget, aşağıdaki tabloda kaynakları toorefer toohello gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-114">tooget started with hello StorSimple Virtual Array deployment as a file server or an iSCSI server, you need toorefer toohello following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="2a54e-115">Dağıtım makaleleri</span><span class="sxs-lookup"><span data-stu-id="2a54e-115">Deployment articles</span></span>

<span data-ttu-id="2a54e-116">toodeploy, StorSimple sanal dizinin dizisi belirlenen hello makalelerinde aşağıdaki toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-116">toodeploy your StorSimple Virtual Array, refer toohello following articles in hello prescribed sequence.</span></span>

| **#** | <span data-ttu-id="2a54e-117">**Bu adımda**</span><span class="sxs-lookup"><span data-stu-id="2a54e-117">**In this step**</span></span> | <span data-ttu-id="2a54e-118">**Bunu...**</span><span class="sxs-lookup"><span data-stu-id="2a54e-118">**You do this …**</span></span> | <span data-ttu-id="2a54e-119">**Ve bu belgeleri kullanın.**</span><span class="sxs-lookup"><span data-stu-id="2a54e-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2a54e-120">1.</span><span class="sxs-lookup"><span data-stu-id="2a54e-120">1.</span></span> |<span data-ttu-id="2a54e-121">**Azure portal Hello ayarlayın**</span><span class="sxs-lookup"><span data-stu-id="2a54e-121">**Set up hello Azure portal**</span></span> |<span data-ttu-id="2a54e-122">Oluşturun ve, StorSimple cihaz Yöneticisi hizmeti önceki tooprovisioning StorSimple sanal dizinin yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-122">Create and configure your StorSimple Device Manager service prior tooprovisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="2a54e-123">Merhaba portal hazırlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-123">Prepare hello portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="2a54e-124">2.</span><span class="sxs-lookup"><span data-stu-id="2a54e-124">2.</span></span> |<span data-ttu-id="2a54e-125">**Merhaba sanal dizinin sağlama**</span><span class="sxs-lookup"><span data-stu-id="2a54e-125">**Provision hello Virtual Array**</span></span> |<span data-ttu-id="2a54e-126">Hyper-v, sağlama ve Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde tooa StorSimple sanal dizinin bağlanın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-126">For Hyper-V, provision and connect tooa StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="2a54e-127">VMware, sağlamak ve tooa StorSimple sanal dizinin VMware ESXi 5.5 çalıştıran bir konak sistemi ve üstü bağlanın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-127">For VMware, provision and connect tooa StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="2a54e-128">Hyper-V sanal bir dizide sağlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="2a54e-129">VMware sanal bir dizide sağlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="2a54e-130">3.</span><span class="sxs-lookup"><span data-stu-id="2a54e-130">3.</span></span> |<span data-ttu-id="2a54e-131">**Sanal dizinin Hello ayarlayın**</span><span class="sxs-lookup"><span data-stu-id="2a54e-131">**Set up hello Virtual Array**</span></span> |<span data-ttu-id="2a54e-132">Dosya sunucunuz için ilk kurulum gerçekleştirmek, StorSimple dosya sunucunuzu kaydetmek ve hello cihaz kurulumunu tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-132">For your file server, perform initial setup, register your StorSimple file server, and complete hello device setup.</span></span> <span data-ttu-id="2a54e-133">Ardından, SMB paylaşımları sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a54e-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="2a54e-134">İSCSI sunucunuz için ilk kurulum gerçekleştirmek, StorSimple iSCSI sunucuyu kaydetmek ve hello cihaz kurulumunu tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete hello device setup.</span></span> <span data-ttu-id="2a54e-135">Ardından, iSCSI birimleri sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a54e-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="2a54e-136">Sanal dizinin Kurulumu dosya sunucusu olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2a54e-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="2a54e-137">Sanal dizinin Kurulumu iSCSI sunucusu olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="2a54e-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="2a54e-138">Hello Azure portal yukarı tooset şimdi başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a54e-138">You can now begin tooset up hello Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="2a54e-139">Yapılandırma denetim listesi</span><span class="sxs-lookup"><span data-stu-id="2a54e-139">Configuration checklist</span></span>

<span data-ttu-id="2a54e-140">Merhaba yapılandırma denetim listesi, StorSimple sanal dizisinde hello yazılım yapılandırmadan önce toocollect gereksinim hello bilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="2a54e-140">hello configuration checklist describes hello information that you need toocollect before you configure hello software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="2a54e-141">Zaman yardımcı öncesinde bu bilgiler, ortamınızdaki hello StorSimple cihazı dağıtma daha verimli hale hello işlemi hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="2a54e-141">Preparing this information ahead of time helps streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="2a54e-142">StorSimple sanal dizinizi bir dosya sunucusu veya bir iSCSI sunucu olarak dağıtılan bağlı bağlı olarak, denetim listeleri aşağıdaki hello biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of hello following checklists.</span></span>

* <span data-ttu-id="2a54e-143">Merhaba karşıdan [StorSimple sanal dizinin dosya sunucusu yapılandırma denetim listesi](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="2a54e-143">Download hello [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="2a54e-144">Merhaba karşıdan [StorSimple sanal dizinin iSCSI sunucu yapılandırma denetim listesi](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="2a54e-144">Download hello [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a54e-145">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2a54e-145">Prerequisites</span></span>

<span data-ttu-id="2a54e-146">Burada, StorSimple cihaz Yöneticisi hizmetiniz, StorSimple sanal dizinin ve hello veri merkezi ağ için hello yapılandırma önkoşulları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2a54e-146">Here you find hello configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and hello datacenter network.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="2a54e-147">Merhaba StorSimple cihaz Yöneticisi hizmeti</span><span class="sxs-lookup"><span data-stu-id="2a54e-147">For hello StorSimple Device Manager service</span></span>

<span data-ttu-id="2a54e-148">Başlamadan önce aşağıdakilerden emin olun:</span><span class="sxs-lookup"><span data-stu-id="2a54e-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2a54e-149">Erişim kimlik bilgilerine sahip bir Microsoft hesabınız var.</span><span class="sxs-lookup"><span data-stu-id="2a54e-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="2a54e-150">Erişim kimlik bilgilerine sahip bir Microsoft Azure Storage hesabınız var.</span><span class="sxs-lookup"><span data-stu-id="2a54e-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="2a54e-151">Microsoft Azure aboneliğiniz StorSimple cihaz Yöneticisi hizmeti için etkinleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a54e-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="2a54e-152">StorSimple sanal dizinin Hello için</span><span class="sxs-lookup"><span data-stu-id="2a54e-152">For hello StorSimple Virtual Array</span></span>

<span data-ttu-id="2a54e-153">Sanal bir dizi dağıtmadan önce emin olun:</span><span class="sxs-lookup"><span data-stu-id="2a54e-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="2a54e-154">Hyper-V Windows Server 2008 R2 veya sonraki sürümlerde çalışan erişim tooa ana bilgisayar sistemi sahip veya kullanılan tooa olabilir (ESXi 5.5 veya sonraki) VMware bir aygıtı sağlamak.</span><span class="sxs-lookup"><span data-stu-id="2a54e-154">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used tooa provision a device.</span></span>
* <span data-ttu-id="2a54e-155">Merhaba ana bilgisayar sistemidir mümkün toodedicate kaynakları tooprovision sanal dizinizi hello:</span><span class="sxs-lookup"><span data-stu-id="2a54e-155">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>
  
  * <span data-ttu-id="2a54e-156">4 çekirdek en az.</span><span class="sxs-lookup"><span data-stu-id="2a54e-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="2a54e-157">En az 8 GB RAM.</span><span class="sxs-lookup"><span data-stu-id="2a54e-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="2a54e-158">Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyon dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="2a54e-158">If you plan tooconfigure hello virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="2a54e-159">16 GB RAM toosupport 2-4 milyon dosyaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-159">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="2a54e-160">Bir ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="2a54e-160">One network interface.</span></span>
  * <span data-ttu-id="2a54e-161">Sistem verileri için 500 GB sanal disk.</span><span class="sxs-lookup"><span data-stu-id="2a54e-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-hello-datacenter-network"></a><span data-ttu-id="2a54e-162">Merhaba veri merkezi ağ için</span><span class="sxs-lookup"><span data-stu-id="2a54e-162">For hello datacenter network</span></span>

<span data-ttu-id="2a54e-163">Başlamadan önce aşağıdakilerden emin olun:</span><span class="sxs-lookup"><span data-stu-id="2a54e-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2a54e-164">Merhaba ağ, veri merkezinizdeki hello StorSimple cihazınız için ağ gereksinimlerine uygun yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="2a54e-164">hello network in your datacenter is configured as per hello networking requirements for your StorSimple device.</span></span> <span data-ttu-id="2a54e-165">Daha fazla bilgi için bkz: Merhaba [StorSimple sanal dizinin sistem gereksinimleri](storsimple-ova-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2a54e-165">For more information, see hello [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="2a54e-166">StorSimple sanal dizinizi ayrılmış 5 MB/sn Internet bant genişliği (veya daha fazla) olduğundan her zaman kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="2a54e-167">Bu bant genişliği herhangi bir uygulama ile Paylaşılmaması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2a54e-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="2a54e-168">Adım adım hazırlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-168">Step-by-step preparation</span></span>

<span data-ttu-id="2a54e-169">Adım adım yönergeler tooprepare aşağıdaki hello portalınızı hello StorSimple cihaz Yöneticisi hizmeti için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-169">Use hello following step-by-step instructions tooprepare your portal for hello StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="2a54e-170">1. Adım: Yeni bir hizmet oluşturun</span><span class="sxs-lookup"><span data-stu-id="2a54e-170">Step 1: Create a new service</span></span>

<span data-ttu-id="2a54e-171">Merhaba StorSimple cihaz Yöneticisi hizmeti tek bir örneği birden çok StorSimple sanal diziler yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a54e-171">A single instance of hello StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="2a54e-172">Adımları toocreate hello StorSimple cihaz Yöneticisi hizmetinin bir örneği aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2a54e-172">Perform hello following steps toocreate an instance of hello StorSimple Device Manager service.</span></span> <span data-ttu-id="2a54e-173">Mevcut bir StorSimple cihaz Yöneticisi hizmeti toomanage sanal dizileriniz varsa, bu adımı atlayın ve çok gidin[2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="2a54e-173">If you have an existing StorSimple Device Manager service toomanage your virtual arrays, skip this step and go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="2a54e-174">Hizmetiniz ile Merhaba otomatik bir depolama hesabının oluşturulmasını etkinleştirmediyseniz toocreate ihtiyacınız olacak bir hizmeti başarıyla oluşturduktan sonra en az bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="2a54e-174">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="2a54e-175">Otomatik olarak bir depolama hesabı oluşturmadıysanız, çok Git[hello hizmet için yeni bir depolama hesabı yapılandırma](#optional-step-configure-a-new-storage-account-for-the-service) ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="2a54e-175">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="2a54e-176">Depolama hesabı hello otomatik oluşturma etkinleştirilirse, çok Git[2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="2a54e-176">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="2a54e-177">2. adım: hello hizmet kayıt anahtarını alın</span><span class="sxs-lookup"><span data-stu-id="2a54e-177">Step 2: Get hello service registration key</span></span>

<span data-ttu-id="2a54e-178">Merhaba StorSimple cihaz Yöneticisi hizmeti çalışır durumda sonra tooget hello hizmet kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-178">After hello StorSimple Device Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="2a54e-179">Bu anahtar kullanılan tooregister ve StorSimple Cihazınızı hello hizmetiyle bağlama.</span><span class="sxs-lookup"><span data-stu-id="2a54e-179">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="2a54e-180">Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a54e-180">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="2a54e-181">Merhaba hizmet kayıt anahtarı olan kullanılan tooregister tüm StorSimple Aygıt Yöneticisi'ni hizmetinizle tooregister gereken StorSimple Aygıt Yöneticisi'ni cihazların Merhaba.</span><span class="sxs-lookup"><span data-stu-id="2a54e-181">hello service registration key is used tooregister all hello StorSimple Device Manager devices that need tooregister with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a><span data-ttu-id="2a54e-182">Adım 3: hello sanal dizinin görüntü indirin</span><span class="sxs-lookup"><span data-stu-id="2a54e-182">Step 3: Download hello virtual array image</span></span>

<span data-ttu-id="2a54e-183">Merhaba hizmet kayıt anahtarını oluşturduktan sonra ana bilgisayar sisteminde toodownload hello uygun sanal dizinin görüntü tooprovision sanal bir dizi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-183">After you have hello service registration key, you will need toodownload hello appropriate virtual array image tooprovision a virtual array on your host system.</span></span> <span data-ttu-id="2a54e-184">Merhaba sanal dizinin görüntüleri, işletim sisteminin belirli ve hello Azure Portalı'nda hello hızlı başlangıç sayfasından indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-184">hello virtual array images are operating system specific and can be downloaded from hello Quick Start page in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a54e-185">StorSimple sanal dizinin Hello üzerinde çalışan hello yazılımı yalnızca StorSimple cihaz Yöneticisi hizmeti hello ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-185">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="2a54e-186">Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a54e-186">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="tooget-hello-virtual-array-image"></a><span data-ttu-id="2a54e-187">tooget hello sanal dizinin görüntüsü</span><span class="sxs-lookup"><span data-stu-id="2a54e-187">tooget hello virtual array image</span></span>

1. <span data-ttu-id="2a54e-188">Merhaba içine oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a54e-188">Sign into hello [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="2a54e-189">Hello Azure portal'ı tıklatın **Gözat > StorSimple cihaz yöneticileri**.</span><span class="sxs-lookup"><span data-stu-id="2a54e-189">In hello Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="2a54e-190">Var olan bir StorSimple cihaz Yöneticisi hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="2a54e-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="2a54e-191">Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde tıklatın **Hızlı Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="2a54e-191">In hello **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="2a54e-192">Merhaba Microsoft Download Center gelen toodownload istediğiniz hello bağlantı karşılık gelen toohello görüntüsünü tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-192">Click hello link corresponding toohello image that you want toodownload from hello Microsoft Download Center.</span></span> <span data-ttu-id="2a54e-193">yaklaşık 4.8 GB Hello görüntü dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="2a54e-193">hello image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="2a54e-194">Hyper-V Windows Server 2012 ve sonraki sürümler için VHDX</span><span class="sxs-lookup"><span data-stu-id="2a54e-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="2a54e-195">VHD için Hyper-V Windows Server 2008 R2 ve sonraki sürümler</span><span class="sxs-lookup"><span data-stu-id="2a54e-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="2a54e-196">VMDK VMWare ESXi 5.5 ve sonraki sürümleri</span><span class="sxs-lookup"><span data-stu-id="2a54e-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="2a54e-197">Karşıdan yükle ve hello sıkıştırması açılmış dosyasının bulunduğu bir not yapmadan hello dosya tooa yerel sürücü, sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-197">Download and unzip hello file tooa local drive, making a note of where hello unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="2a54e-198">İsteğe bağlı adım: yeni bir depolama hesabı hello hizmeti için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2a54e-198">Optional step: Configure a new storage account for hello service</span></span>

<span data-ttu-id="2a54e-199">Bu adım isteğe bağlıdır ve yalnızca, bir depolama hesabının otomatik oluşturulmasını hello hizmetiniz ile etkinleştirmediyseniz gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-199">This step is optional and should be performed only if you did not enable hello automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="2a54e-200">Azure storage hesabı farklı bir bölgede toocreate gerekirse bkz [nasıl toocreate bir depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="2a54e-200">If you need toocreate an Azure storage account in a different region, see [How toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="2a54e-201">Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://ms.portal.azure.com/) hello StorSimple cihaz Yöneticisi hizmet sayfası tooadd var olan bir Microsoft Azure depolama hesabı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2a54e-201">Perform hello following steps in hello [Azure portal](https://ms.portal.azure.com/) on hello StorSimple Device Manager service page tooadd an existing Microsoft Azure storage account.</span></span>

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a><span data-ttu-id="2a54e-202">tooadd sahip bir depolama hesabı kimlik bilgilerini hello hello Aygıt Yöneticisi hizmeti aynı Azure abonelik</span><span class="sxs-lookup"><span data-stu-id="2a54e-202">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>

1. <span data-ttu-id="2a54e-203">Aygıt Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-203">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="2a54e-204">Merhaba açılır **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="2a54e-204">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="2a54e-205">Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2a54e-205">Select **Storage account credentials** within hello **Configuration** section.</span></span>
3. <span data-ttu-id="2a54e-206">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-206">Click **Add**.</span></span>
4. <span data-ttu-id="2a54e-207">Merhaba, **depolama hesabı ekleme** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="2a54e-207">In hello **Add a storage account** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="2a54e-208">İçin **abonelik**seçin **geçerli**.</span><span class="sxs-lookup"><span data-stu-id="2a54e-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="2a54e-209">Hello Azure depolama hesabınızın adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-209">Provide hello name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="2a54e-210">Seçin **etkinleştirmek** toocreate StorSimple cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal.</span><span class="sxs-lookup"><span data-stu-id="2a54e-210">Select **Enable** toocreate a secure channel for network communication between your StorSimple device and hello cloud.</span></span> <span data-ttu-id="2a54e-211">Seçin **devre dışı** yalnızca özel bir bulutta işlem yapıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="2a54e-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="2a54e-212">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a54e-212">Click **Add**.</span></span> <span data-ttu-id="2a54e-213">Merhaba depolama hesabı başarıyla oluşturulduktan sonra size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="2a54e-213">You are notified after hello storage account is successfully created.</span></span><br></br>
   
     ![Varolan bir depolama hesabı kimlik bilgileri Ekle](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="2a54e-215">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="2a54e-215">Next step</span></span>

<span data-ttu-id="2a54e-216">Merhaba sonraki tooprovision, StorSimple sanal dizi için bir sanal makine adımdır.</span><span class="sxs-lookup"><span data-stu-id="2a54e-216">hello next step is tooprovision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="2a54e-217">Ana bilgisayar işletim sistemine bağlı olarak bkz hello ayrıntılı yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="2a54e-217">Depending on your host operating system, see hello detailed instructions in:</span></span>

* [<span data-ttu-id="2a54e-218">Hyper-V StorSimple sanal dizisinde sağlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="2a54e-219">VMware StorSimple sanal dizisinde sağlama</span><span class="sxs-lookup"><span data-stu-id="2a54e-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

