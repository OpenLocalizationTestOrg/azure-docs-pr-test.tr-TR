---
title: "bir Microsoft Azure StorSimple sanal dizisinde aaaInstall güncelleştirmeleri | Microsoft Docs"
description: "Toouse hello StorSimple sanal dizinin web kullanıcı Arabirimi tooapply hello portal ve düzeltme yöntemi kullanılarak nasıl güncelleştirdiği açıklar"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7424abc7e46d4f08b4eae1194642b263f32c4318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="ca5d2-103">StorSimple sanal dizinizi üzerinde - Azure portalında güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="ca5d2-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="ca5d2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ca5d2-104">Overview</span></span>

<span data-ttu-id="ca5d2-105">Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Azure portal aracılığıyla hello adımları gerekli tooinstall güncelleştirmeleri açıklanır.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="ca5d2-106">Tooapply yazılım güncelleştirmeleri veya düzeltmeleri tookeep StorSimple sanal dizinizi güncel gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="ca5d2-107">Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="ca5d2-108">Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="ca5d2-109">Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="ca5d2-110">Bu veri bozulması olasılığını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca5d2-111">Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0.3 yöntemiyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="ca5d2-112">Güncelleştirme 0.2 çalıştırıyorsanız, hello Klasik Azure Portalı aracılığıyla hello güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="ca5d2-113">Merhaba yerel web kullanıcı arabirimini kullanın</span><span class="sxs-lookup"><span data-stu-id="ca5d2-113">Use hello local web UI</span></span>

<span data-ttu-id="ca5d2-114">Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="ca5d2-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="ca5d2-115">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="ca5d2-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="ca5d2-116">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="ca5d2-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="ca5d2-117">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="ca5d2-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="ca5d2-118">Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="ca5d2-119">toodownload hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="ca5d2-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="ca5d2-120">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ca5d2-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="ca5d2-121">Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="ca5d2-122">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="ca5d2-123">Girin **3182061** Update 0.3 ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="ca5d2-124">Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0.3**.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="ca5d2-126">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-126">Click **Add**.</span></span> <span data-ttu-id="ca5d2-127">Merhaba güncelleştirme toohello Sepeti eklenir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="ca5d2-128">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="ca5d2-129">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-129">Click **Download**.</span></span> <span data-ttu-id="ca5d2-130">Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="ca5d2-131">Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="ca5d2-132">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="ca5d2-133">Açık hello kopyaladığınız klasörü, Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="ca5d2-134">Bu, kullanılan tooinstall hello güncelleştirme veya düzeltme dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="ca5d2-135">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="ca5d2-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="ca5d2-136">Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="ca5d2-137">Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="ca5d2-138">Bu yordamı 2 dakika toocomplete değerinden alır.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="ca5d2-139">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="ca5d2-140">tooinstall hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="ca5d2-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="ca5d2-141">Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="ca5d2-143">İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="ca5d2-144">Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="ca5d2-145">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-145">Click **Apply**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="ca5d2-147">Bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-147">A warning is displayed.</span></span> <span data-ttu-id="ca5d2-148">Bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi budur.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="ca5d2-149">Merhaba onay simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-149">Click hello check icon.</span></span>
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="ca5d2-151">Merhaba güncelleştirme başlatır.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-151">hello update starts.</span></span> <span data-ttu-id="ca5d2-152">Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="ca5d2-153">Merhaba yerel UI bu süre içinde erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-153">hello local UI is not accessible in this duration.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="ca5d2-155">Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="ca5d2-156">Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="ca5d2-157">Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10288.0** güncelleştirme 0.3 için.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ca5d2-158">Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="ca5d2-159">Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10288** ve Azure portal raporları hello **10.0.10288.0** hello için aynı sürüm.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure portal reports **10.0.10288.0** for hello same version.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="ca5d2-161">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="ca5d2-161">Use hello Azure portal</span></span>

<span data-ttu-id="ca5d2-162">Güncelleştirme 0.2 çalıştırılıyorsa hello Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-162">If running Update 0.2, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="ca5d2-163">Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="ca5d2-164">Bu yordamı yaklaşık 7 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="ca5d2-165">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="ca5d2-166">Merhaba sonra yükleme (olarak belirttiği % 100 İş durumu), tam gidin tooyour StorSimple cihaz Yöneticisi hizmeti değildir.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ca5d2-167">Seçin **aygıtları** seçin ve tooupdate aygıtlar bağlı toothis hizmeti hello listesinden istediğiniz hello aygıtı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="ca5d2-168">Merhaba, **ayarları** dikey penceresinde çok Git**Yönet** bölümünde ve seçin **aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="ca5d2-169">Görüntülenen hello yazılım sürüm olmalıdır **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="ca5d2-169">hello displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ca5d2-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca5d2-170">Next steps</span></span>

<span data-ttu-id="ca5d2-171">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="ca5d2-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

