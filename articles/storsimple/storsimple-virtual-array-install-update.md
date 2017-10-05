---
title: "Bir Microsoft Azure StorSimple sanal dizinin güncelleştirmeleri yükle | Microsoft Docs"
description: "StorSimple sanal dizinin web kullanıcı Arabirimi portal ve düzeltme yöntemini kullanarak güncelleştirmeleri uygulamak için nasıl kullanılacağını açıklar"
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
ms.openlocfilehash: c2d081604c0ca01f47c3ff2aab7477859d280963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="13146-103">StorSimple sanal dizinizi üzerinde - Azure portalında güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="13146-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="13146-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="13146-104">Overview</span></span>

<span data-ttu-id="13146-105">Bu makalede, StorSimple sanal dizinin yerel web kullanıcı Arabirimi aracılığıyla ve Azure Portalı aracılığıyla güncelleştirmeleri yüklemek için gereken adımlar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="13146-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="13146-106">Yazılım güncelleştirmelerini veya düzeltmeleri StorSimple sanal dizinizi güncel tutmak için uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13146-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="13146-107">Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="13146-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="13146-108">Bir tek düğümlü cihaz StorSimple sanal dizinin olması koşuluyla, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="13146-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="13146-109">Bir güncelleştirmeyi uygulamadan önce birimler veya paylaşımlar çevrimdışı konakta ilk almanızı öneririz ve ardından cihaz.</span><span class="sxs-lookup"><span data-stu-id="13146-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="13146-110">Bu veri bozulması olasılığını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="13146-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13146-111">Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, update 0.3 yüklemek için yerel web kullanıcı Arabirimi aracılığıyla düzeltme yöntemini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13146-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="13146-112">Güncelleştirme 0.2 çalıştırıyorsanız, Klasik Azure Portalı aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="13146-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="13146-113">Yerel web kullanıcı arabirimini kullanın</span><span class="sxs-lookup"><span data-stu-id="13146-113">Use the local web UI</span></span>

<span data-ttu-id="13146-114">Yerel web kullanıcı arabirimini kullanırken iki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="13146-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="13146-115">Güncelleştirmeyi veya düzeltmeyi indirin</span><span class="sxs-lookup"><span data-stu-id="13146-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="13146-116">Güncelleştirmeyi veya düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="13146-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="13146-117">Güncelleştirmeyi veya düzeltmeyi indirin</span><span class="sxs-lookup"><span data-stu-id="13146-117">Download the update or the hotfix</span></span>

<span data-ttu-id="13146-118">Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="13146-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="13146-119">Güncelleştirmeyi veya düzeltmeyi indirmek için</span><span class="sxs-lookup"><span data-stu-id="13146-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="13146-120">Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="13146-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="13146-121">Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="13146-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="13146-122">Microsoft Update Kataloğu arama kutusuna, yüklemek istediğiniz düzeltme Bilgi Bankası (KB) sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="13146-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="13146-123">Girin **3182061** Update 0.3 ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="13146-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="13146-124">Düzeltme listesi göründüğünde, örneğin, **StorSimple sanal dizinin güncelleştirme 0.3**.</span><span class="sxs-lookup"><span data-stu-id="13146-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="13146-126">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13146-126">Click **Add**.</span></span> <span data-ttu-id="13146-127">Güncelleştirme sepete eklenir.</span><span class="sxs-lookup"><span data-stu-id="13146-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="13146-128">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13146-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="13146-129">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13146-129">Click **Download**.</span></span> <span data-ttu-id="13146-130">İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun.</span><span class="sxs-lookup"><span data-stu-id="13146-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="13146-131">Güncelleştirmeler belirtilen konuma indirilir ve güncelleştirme ile aynı adı taşıyan alt klasöre yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="13146-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="13146-132">Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="13146-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="13146-133">Kopyalanan klasörünü açın, bir Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="13146-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="13146-134">Bu dosya, güncelleştirme veya düzeltme yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="13146-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="13146-135">Güncelleştirmeyi veya düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="13146-135">Install the update or the hotfix</span></span>

<span data-ttu-id="13146-136">Güncelleştirme veya düzeltme yükleme önce bir ağ paylaşımı üzerinden erişilebilir veya güncelleştirmeye sahip veya ana bilgisayarınız yerel olarak ya da düzeltmeyi indirdiğiniz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="13146-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="13146-137">GA çalıştıran bir cihazda güncelleştirmeleri yüklemek veya 0,1 yazılım sürümleri güncelleştirmek için bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="13146-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="13146-138">Bu yordamı tamamlamak için değerinden 2 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="13146-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="13146-139">Güncelleştirme veya düzeltme yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="13146-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="13146-140">Güncelleştirme veya düzeltme yüklemek için</span><span class="sxs-lookup"><span data-stu-id="13146-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="13146-141">Yerel web kullanıcı Arabirimi, Git **Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="13146-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="13146-143">İçinde **güncelleştirme dosya yolu**, güncelleştirme veya düzeltme için dosya adı girin.</span><span class="sxs-lookup"><span data-stu-id="13146-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="13146-144">Ayrıca, bir ağ paylaşımında girdiyseniz güncelleştirme veya düzeltme yükleme dosyasına göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13146-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="13146-145">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13146-145">Click **Apply**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="13146-147">Bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="13146-147">A warning is displayed.</span></span> <span data-ttu-id="13146-148">Bir tek düğümlü aygıt güncelleştirme uygulanana, aygıt yeniden başladıktan sonra kapalı kalma süresi budur.</span><span class="sxs-lookup"><span data-stu-id="13146-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="13146-149">Onay simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13146-149">Click the check icon.</span></span>
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="13146-151">Güncelleştirme başlatır.</span><span class="sxs-lookup"><span data-stu-id="13146-151">The update starts.</span></span> <span data-ttu-id="13146-152">Cihaz başarıyla güncelleştirildikten sonra yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="13146-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="13146-153">Yerel kullanıcı arabirimini bu süre içinde erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="13146-153">The local UI is not accessible in this duration.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="13146-155">Yeniden başlatma tamamlandıktan sonra gittiğiniz **oturum** sayfası.</span><span class="sxs-lookup"><span data-stu-id="13146-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="13146-156">Aygıt yazılımı, yerel web kullanıcı Arabirimi, güncelleştirilmiş olduğunu doğrulamak için Git **Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="13146-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="13146-157">Görüntülenen yazılım sürümü olmalıdır **10.0.0.0.0.10288.0** güncelleştirme 0.3 için.</span><span class="sxs-lookup"><span data-stu-id="13146-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="13146-158">Yazılım sürümlerini yerel web kullanıcı Arabirimi biraz farklı bir şekilde hem de Azure portalında bildirin.</span><span class="sxs-lookup"><span data-stu-id="13146-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="13146-159">Örneğin, yerel web kullanıcı Arabirimi raporları **10.0.0.0.0.10288** ve Azure portal raporları **10.0.10288.0** aynı sürüm için.</span><span class="sxs-lookup"><span data-stu-id="13146-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure portal reports **10.0.10288.0** for the same version.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="13146-161">Azure portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="13146-161">Use the Azure portal</span></span>

<span data-ttu-id="13146-162">Güncelleştirme 0.2 çalıştırılıyorsa, Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="13146-162">If running Update 0.2, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="13146-163">Portal yordamı tarama, indirme ve güncelleştirmeleri yüklemek kullanıcının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="13146-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="13146-164">Bu yordamı tamamlamak için yaklaşık 7 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="13146-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="13146-165">Güncelleştirme veya düzeltme yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="13146-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="13146-166">(Olarak % 100 İş durumu tarafından gösterilen) yükleme tamamlandıktan sonra StorSimple cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="13146-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="13146-167">Seçin **aygıtları** seçin ve bu hizmete bağlı aygıtlar listesinde güncelleştirmek istediğiniz cihaza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13146-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="13146-168">İçinde **ayarları** dikey penceresinde, Git **Yönet** bölümünde ve seçin **aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="13146-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="13146-169">Görüntülenen yazılım sürümü olmalıdır **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="13146-169">The displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="13146-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13146-170">Next steps</span></span>

<span data-ttu-id="13146-171">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="13146-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

