---
title: "StorSimple cihaz Yöneticisi hizmeti aaaDeploy | Microsoft Docs"
description: "Nasıl toocreate ve delete hello Azure portal StorSimple Aygıt Yöneticisi'ni hizmetinde hello açıklar ve nasıl toomanage hello hizmet kayıt anahtarını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="c67dd-103">StorSimple sanal dizini Hello StorSimple cihaz Yöneticisi hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="c67dd-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="c67dd-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c67dd-104">Overview</span></span>

<span data-ttu-id="c67dd-105">Merhaba StorSimple cihaz Yöneticisi hizmeti Microsoft Azure üzerinde çalışır ve toomultiple StorSimple cihazları bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c67dd-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="c67dd-106">Merhaba hizmeti oluşturduktan sonra hello Microsoft Azure portal tarayıcıda çalışıyor toomanage hello cihazların kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dd-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="c67dd-107">Bu, böylece yönetici yükünü en aza bir tek, merkezi konumdan bağlı toohello StorSimple Aygıt Yöneticisi'ni tüm hello cihazlar hizmet toomonitor sağlar.</span><span class="sxs-lookup"><span data-stu-id="c67dd-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="c67dd-108">Merhaba, ortak görevler, ilgili, tooa StorSimple cihaz Yöneticisi hizmeti şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c67dd-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="c67dd-109">Hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="c67dd-109">Create a service</span></span>
* <span data-ttu-id="c67dd-110">Bir hizmeti silin</span><span class="sxs-lookup"><span data-stu-id="c67dd-110">Delete a service</span></span>
* <span data-ttu-id="c67dd-111">Merhaba hizmet kayıt anahtarını alın</span><span class="sxs-lookup"><span data-stu-id="c67dd-111">Get hello service registration key</span></span>
* <span data-ttu-id="c67dd-112">Merhaba hizmet kayıt anahtarını yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="c67dd-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="c67dd-113">Bu öğretici nasıl tooperform her birini hello önceki görevleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="c67dd-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="c67dd-114">Bu makalede bulunan hello yalnızca geçerli tooStorSimple sanal diziler bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="c67dd-115">StorSimple 8000 serisi hakkında daha fazla bilgi için çok Git[StorSimple Yöneticisi hizmet dağıtma](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="c67dd-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="c67dd-116">Hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="c67dd-116">Create a service</span></span>

<span data-ttu-id="c67dd-117">bir hizmet toocreate, toohave gerekir:</span><span class="sxs-lookup"><span data-stu-id="c67dd-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="c67dd-118">Bir aboneliği bir kurumsal anlaşma ile</span><span class="sxs-lookup"><span data-stu-id="c67dd-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="c67dd-119">Etkin bir Microsoft Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="c67dd-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="c67dd-120">Merhaba, erişim yönetimi için kullanılan bilgileri faturalama</span><span class="sxs-lookup"><span data-stu-id="c67dd-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="c67dd-121">Merhaba hizmeti oluşturduğunuzda, toogenerate bir depolama hesabı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dd-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="c67dd-122">Tek bir hizmet birden çok cihazları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dd-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="c67dd-123">Ancak, bir aygıt birden fazla hizmet yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="c67dd-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="c67dd-124">Büyük bir kuruluş birden çok hizmet örnekleri toowork farklı Aboneliklerde, kuruluşlar veya bile dağıtım konumlarında olabilir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="c67dd-125">StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple 8000 serisi cihazlar ve StorSimple sanal diziler ayrı örnekleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="c67dd-126">Aşağıdaki adımları toocreate hizmet hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c67dd-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="c67dd-127">Bir hizmeti silin</span><span class="sxs-lookup"><span data-stu-id="c67dd-127">Delete a service</span></span>

<span data-ttu-id="c67dd-128">Bir hizmet silmeden önce hiçbir bağlı aygıtlar, kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c67dd-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="c67dd-129">Merhaba hizmet kullanımdaysa hello bağlı aygıtları devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="c67dd-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="c67dd-130">Merhaba, işlemi devre dışı bırakma hello bağlantı hello hizmeti ile Merhaba aygıt arasında sever ancak hello bulutta hello aygıt verilerini korumak.</span><span class="sxs-lookup"><span data-stu-id="c67dd-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c67dd-131">Hizmet silindikten sonra hello işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="c67dd-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="c67dd-132">Merhaba hizmeti tarafından kullanılan herhangi bir aygıt toobe ihtiyacınız olacak başka bir hizmetle kullanılabilmesi için önce Fabrika.</span><span class="sxs-lookup"><span data-stu-id="c67dd-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="c67dd-133">Bu senaryoda, hello yapılandırma yanı sıra hello aygıt hello yerel veriler kaybolacak.</span><span class="sxs-lookup"><span data-stu-id="c67dd-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="c67dd-134">Aşağıdaki adımları toodelete hizmet hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c67dd-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="c67dd-135">toodelete bir hizmeti</span><span class="sxs-lookup"><span data-stu-id="c67dd-135">toodelete a service</span></span>

1. <span data-ttu-id="c67dd-136">Çok Git**tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="c67dd-136">Go too**All resources**.</span></span> <span data-ttu-id="c67dd-137">StorSimple cihaz Yöneticisi hizmetiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="c67dd-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="c67dd-138">Toodelete istediğiniz hello hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="c67dd-138">Select hello service that you wish toodelete.</span></span>
   
    ![Hizmet toodelete seçin](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="c67dd-140">Tooyour hizmet Pano tooensure vardır Git hiçbir aygıt bağlı toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="c67dd-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="c67dd-141">Bu hizmetle kaydedilen hiçbir cihaz varsa bir başlık iletisi toohello etkisi de görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c67dd-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="c67dd-142">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c67dd-142">Click **Delete**.</span></span>
   
    ![Hizmet silme](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="c67dd-144">Onayınız istendiğinde tıklatın **Evet** hello onay bildirim.</span><span class="sxs-lookup"><span data-stu-id="c67dd-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Hizmet Silmeyi Onayla](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="c67dd-146">Silinen hello hizmet toobe birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="c67dd-147">Merhaba sonra hizmeti başarıyla, size bildirilecek silinir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Başarılı hizmet silme](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="c67dd-149">hizmetlerin Hello listesi yenilenecektir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-149">hello list of services will be refreshed.</span></span>

 ![Güncelleştirilmiş hizmetlerin listesi](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="c67dd-151">Merhaba hizmet kayıt anahtarını alın</span><span class="sxs-lookup"><span data-stu-id="c67dd-151">Get hello service registration key</span></span>
<span data-ttu-id="c67dd-152">Bir hizmeti başarıyla oluşturduktan sonra StorSimple cihazınızla hello hizmet tooregister gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="c67dd-153">tooregister ilk StorSimple Cihazınızı hizmet kayıt anahtarını hello.</span><span class="sxs-lookup"><span data-stu-id="c67dd-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="c67dd-154">tooregister ek cihazların mevcut bir StorSimple hizmeti ile Merhaba kayıt anahtarını ve (Merhaba ilk cihazda kayıt sırasında oluşturulan) hello hizmet verileri şifreleme anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="c67dd-155">Merhaba hizmet verileri şifreleme anahtarı hakkında daha fazla bilgi için bkz: [StorSimple güvenlik](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="c67dd-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="c67dd-156">Merhaba erişerek hello kayıt anahtarını elde edebilirsiniz **anahtarları** dikey hizmetiniz için.</span><span class="sxs-lookup"><span data-stu-id="c67dd-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="c67dd-157">Aşağıdaki adımları tooget hello hizmet kayıt anahtarını hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c67dd-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="c67dd-158">tooget hello hizmet kayıt anahtarı</span><span class="sxs-lookup"><span data-stu-id="c67dd-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="c67dd-159">Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde çok Git**Yönetim &gt;**  **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="c67dd-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Anahtarlar dikey penceresi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="c67dd-161">Merhaba, **anahtarları** hizmet kayıt anahtarını dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="c67dd-162">Merhaba kopyalama simgesini kullanarak hello kayıt anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c67dd-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="c67dd-163">Merhaba hizmet kayıt anahtarı güvenli bir yerde tutun.</span><span class="sxs-lookup"><span data-stu-id="c67dd-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="c67dd-164">Bu anahtar, yanı sıra hello hizmet verileri şifreleme anahtarı, bu hizmetiyle ek cihazlar tooregister gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="c67dd-165">Merhaba hizmet kayıt anahtarı aldıktan sonra StorSimple arabirimi hello Windows PowerShell aracılığıyla cihazınızın tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="c67dd-166">Merhaba hizmet kayıt anahtarını yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="c67dd-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="c67dd-167">Gerekli tooperform anahtar döndürme veya hizmet yöneticilerinin listesini hello değişip değişmediğini varsa tooregenerate hizmet kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="c67dd-168">Başlangıç anahtarı yeniden oluşturmak zaman hello yeni anahtar yalnızca sonraki cihazları kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c67dd-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="c67dd-169">Bu işlem tarafından zaten kayıtlı olan hello aygıtları etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="c67dd-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="c67dd-170">Aşağıdaki adımları tooregenerate hizmet kayıt anahtarını hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c67dd-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="c67dd-171">tooregenerate hello hizmet kayıt anahtarı</span><span class="sxs-lookup"><span data-stu-id="c67dd-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="c67dd-172">Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde çok Git**Yönetim &gt;**  **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="c67dd-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Anahtarlar dikey penceresi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="c67dd-174">Merhaba, **anahtarları** dikey penceresinde tıklatın **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="c67dd-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Yeniden tıklatın](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="c67dd-176">Merhaba, **üretme hizmet kayıt anahtarını** dikey penceresinde, gözden geçirme hello eylem gerekli hello zaman anahtarları yeniden oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c67dd-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="c67dd-177">Bu hizmetle kaydedilen tüm hello sonraki cihazlar hello yeni kayıt anahtarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c67dd-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="c67dd-178">Tıklatın **yeniden** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="c67dd-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="c67dd-179">Merhaba kayıt tamamlandıktan sonra size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="c67dd-179">You will be notified after hello registration is complete.</span></span>
   
   ![Yeniden oluşturma anahtarını doğrulayın](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="c67dd-181">Yeni bir hizmet kayıt anahtarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c67dd-181">A new service registration key will appear.</span></span>
   
    ![Yeniden oluşturma anahtarını doğrulayın](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="c67dd-183">Bu anahtarı kopyalayın ve bu hizmeti ile yeni aygıtları kaydetme için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c67dd-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c67dd-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c67dd-184">Next steps</span></span>
* <span data-ttu-id="c67dd-185">Nasıl çok öğrenin[başlama](storsimple-virtual-array-deploy1-portal-prep.md) bir StorSimple sanal diziye sahip.</span><span class="sxs-lookup"><span data-stu-id="c67dd-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="c67dd-186">Nasıl çok öğrenin[StorSimple Cihazınızı yönetmek](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="c67dd-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

