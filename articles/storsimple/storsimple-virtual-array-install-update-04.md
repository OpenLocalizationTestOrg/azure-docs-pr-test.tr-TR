---
title: "StorSimple sanal dizisindeki aaaInstall güncelleştirmeleri | Microsoft Docs"
description: "Azure portal ve düzeltme yöntemi toouse hello StorSimple sanal dizinin web kullanıcı Arabirimi tooapply güncelleştirmeleri kullanarak nasıl hello açıklar"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="51b4a-103">StorSimple sanal dizinizi üzerinde güncelleştirme 0.4 yükleyin</span><span class="sxs-lookup"><span data-stu-id="51b4a-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="51b4a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="51b4a-104">Overview</span></span>

<span data-ttu-id="51b4a-105">Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Azure portal aracılığıyla hello adımları gerekli tooinstall güncelleştirme 0.4 açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="51b4a-105">This article describes hello steps required tooinstall Update 0.4 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="51b4a-106">Tooapply yazılım güncelleştirmeleri veya düzeltmeleri tookeep StorSimple sanal dizinizi güncel gerekir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="51b4a-107">Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="51b4a-108">Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="51b4a-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="51b4a-109">Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz.</span><span class="sxs-lookup"><span data-stu-id="51b4a-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="51b4a-110">Bu veri bozulması olasılığını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51b4a-111">Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0.3 yöntemiyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="51b4a-112">Daha sonra öneririz veya güncelleştirme 0.2 çalıştırıyorsanız hello Azure portal aracılığıyla hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="51b4a-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="51b4a-113">Merhaba yerel web kullanıcı arabirimini kullanın</span><span class="sxs-lookup"><span data-stu-id="51b4a-113">Use hello local web UI</span></span>

<span data-ttu-id="51b4a-114">Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="51b4a-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="51b4a-115">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="51b4a-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="51b4a-116">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="51b4a-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="51b4a-117">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="51b4a-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="51b4a-118">Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="51b4a-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="51b4a-119">toodownload hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="51b4a-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="51b4a-120">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="51b4a-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="51b4a-121">Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="51b4a-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="51b4a-122">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor.</span><span class="sxs-lookup"><span data-stu-id="51b4a-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="51b4a-123">Girin **3216577** 0.4 güncelleştirmesi için ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="51b4a-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="51b4a-124">Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0.4**.</span><span class="sxs-lookup"><span data-stu-id="51b4a-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="51b4a-126">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-126">Click **Add**.</span></span> <span data-ttu-id="51b4a-127">Merhaba güncelleştirme toohello Sepeti eklenir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="51b4a-128">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="51b4a-129">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-129">Click **Download**.</span></span> <span data-ttu-id="51b4a-130">Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="51b4a-131">Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="51b4a-132">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="51b4a-133">Açık hello kopyaladığınız klasörü, Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="51b4a-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="51b4a-134">Bu, kullanılan tooinstall hello güncelleştirme veya düzeltme dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="51b4a-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="51b4a-135">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="51b4a-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="51b4a-136">Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun.</span><span class="sxs-lookup"><span data-stu-id="51b4a-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="51b4a-137">Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="51b4a-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="51b4a-138">Bu yordamı 2 dakika toocomplete değerinden alır.</span><span class="sxs-lookup"><span data-stu-id="51b4a-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="51b4a-139">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="51b4a-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="51b4a-140">tooinstall hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="51b4a-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="51b4a-141">Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="51b4a-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="51b4a-143">İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello.</span><span class="sxs-lookup"><span data-stu-id="51b4a-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="51b4a-144">Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51b4a-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="51b4a-145">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-145">Click **Apply**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="51b4a-147">Bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-147">A warning is displayed.</span></span> <span data-ttu-id="51b4a-148">Bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi budur.</span><span class="sxs-lookup"><span data-stu-id="51b4a-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="51b4a-149">Merhaba onay simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-149">Click hello check icon.</span></span>
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="51b4a-151">Merhaba güncelleştirme başlatır.</span><span class="sxs-lookup"><span data-stu-id="51b4a-151">hello update starts.</span></span> <span data-ttu-id="51b4a-152">Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="51b4a-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="51b4a-153">Merhaba yerel UI bu süre içinde erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="51b4a-153">hello local UI is not accessible in this duration.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="51b4a-155">Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası.</span><span class="sxs-lookup"><span data-stu-id="51b4a-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="51b4a-156">Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="51b4a-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="51b4a-157">Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10289.0** 0.4 güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="51b4a-157">hello displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="51b4a-158">Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="51b4a-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="51b4a-159">Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10289** ve Azure portal raporları hello **10.0.10289.0** hello için aynı sürüm.</span><span class="sxs-lookup"><span data-stu-id="51b4a-159">For example, hello local web UI reports **10.0.0.0.0.10289** and hello Azure portal reports **10.0.10289.0** for hello same version.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="51b4a-161">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="51b4a-161">Use hello Azure portal</span></span>

<span data-ttu-id="51b4a-162">Güncelleştirme 0.2 ve sonraki sürümleri çalışıyorsa hello Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="51b4a-162">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="51b4a-163">Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="51b4a-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="51b4a-164">Bu yordamı yaklaşık 7 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="51b4a-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="51b4a-165">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="51b4a-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="51b4a-166">Merhaba sonra yükleme (olarak belirttiği % 100 İş durumu), tam gidin tooyour StorSimple cihaz Yöneticisi hizmeti değildir.</span><span class="sxs-lookup"><span data-stu-id="51b4a-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="51b4a-167">Seçin **aygıtları** seçin ve tooupdate aygıtlar bağlı toothis hizmeti hello listesinden istediğiniz hello aygıtı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="51b4a-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="51b4a-168">Merhaba, **ayarları** dikey penceresinde çok Git**Yönet** bölümünde ve seçin **aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="51b4a-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="51b4a-169">Görüntülenen hello yazılım sürüm olmalıdır **10.0.10289.0**.</span><span class="sxs-lookup"><span data-stu-id="51b4a-169">hello displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="51b4a-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51b4a-170">Next steps</span></span>

<span data-ttu-id="51b4a-171">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="51b4a-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

