---
title: "aaaChange StorSimple sanal dizinin cihaz Yönetici parolasının | Microsoft Docs"
description: "Nasıl toouse ya da hello Azure portal veya StorSimple sanal dizinin web kullanıcı Arabirimi toochange hello cihaz Yöneticisi parolası açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="52707-103">Merhaba StorSimple sanal dizinin cihaz Yöneticisi parolasını StorSimple cihaz Yöneticisi aracılığıyla değiştirme</span><span class="sxs-lookup"><span data-stu-id="52707-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="52707-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="52707-104">Overview</span></span>

<span data-ttu-id="52707-105">Kullandığınızda hello Windows PowerShell arabirimi tooaccess StorSimple sanal dizinin Merhaba, gerekli tooenter bir cihaz Yöneticisi parolası olur.</span><span class="sxs-lookup"><span data-stu-id="52707-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="52707-106">Merhaba StorSimple cihazı ilk sağlandığında ve başlatılan hello varsayılan paroladır *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="52707-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="52707-107">Verilerinizin Hello güvenlik için hello oturum ilk kez ve hello varsayılan parola süre sonu bu parola gerekli toochange olur.</span><span class="sxs-lookup"><span data-stu-id="52707-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="52707-108">Merhaba aygıt, üretim ortamınızda dağıtıldıktan sonra herhangi bir zamanda ya da hello yerel web kullanıcı Arabirimi veya hello Azure portal toochange hello cihaz Yöneticisi parolası de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52707-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="52707-109">Bu makalede bu yordamların her biri açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="52707-109">Each of these procedures is described in this article.</span></span>

 ![Aygıtları dikey penceresi](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="52707-111">Hello Azure portal toochange hello parolayı kullanın</span><span class="sxs-lookup"><span data-stu-id="52707-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="52707-112">Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello Azure portal aracılığıyla hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="52707-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="52707-113">hello Azure portal aracılığıyla toochange hello cihaz Yöneticisi parolası</span><span class="sxs-lookup"><span data-stu-id="52707-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="52707-114">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **Yönetim** 'yi tıklatın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="52707-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="52707-115">Merhaba açılır **aygıtları** tüm StorSimple sanal dizinin aygıtlarını listeler dikey.</span><span class="sxs-lookup"><span data-stu-id="52707-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="52707-116">Merhaba, **aygıtları** dikey penceresinde parola değişikliği gerektirir hello aygıtı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="52707-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="52707-117">Merhaba, **ayarları** , cihazınız için dikey tıklayın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="52707-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="52707-118">Merhaba, **güvenlik ayarları** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="52707-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="52707-119">Toohello aşağı **cihaz Yöneticisi parolasını** bölümü.</span><span class="sxs-lookup"><span data-stu-id="52707-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="52707-120">8 too15 karakterler içeren bir yönetici parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="52707-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="52707-121">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="52707-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="52707-122">Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="52707-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="52707-123">Merhaba cihaz Yöneticisi parolası şimdi güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="52707-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="52707-124">Bu değiştirilmiş parola tooaccess hello aygıt yerel olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52707-124">You can use this modified password tooaccess hello device locally.</span></span>

![Güvenlik ayarları dikey penceresi](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="52707-126">Merhaba yerel web kullanıcı Arabirimi toochange hello parolayı kullanın</span><span class="sxs-lookup"><span data-stu-id="52707-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="52707-127">Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello yerel web kullanıcı Arabirimi aracılığıyla hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="52707-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="52707-128">Merhaba yerel web kullanıcı Arabirimi aracılığıyla toochange hello cihaz Yöneticisi parolası</span><span class="sxs-lookup"><span data-stu-id="52707-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="52707-129">Merhaba yerel web kullanıcı Arabirimi, tıklatın **Bakım** > **parola değişikliği** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="52707-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![Parola1 değiştirme](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="52707-131">Merhaba girin **geçerli parola**.</span><span class="sxs-lookup"><span data-stu-id="52707-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="52707-132">Sağlayan bir **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="52707-132">Provide a **New Password**.</span></span> <span data-ttu-id="52707-133">Merhaba parola en az 8 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="52707-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="52707-134">3'hello aşağıdaki 4'ün içermelidir: büyük harf, küçük harfler, sayısal ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="52707-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="52707-135">Parolanız olamaz Not hello son 24 parola hello aynıdır.</span><span class="sxs-lookup"><span data-stu-id="52707-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="52707-136">Merhaba parola tooconfirm yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="52707-136">Reenter hello password tooconfirm it.</span></span>
   
    ![Parola2 değiştirme](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="52707-138">Merhaba sayfasının Hello altında tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="52707-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="52707-139">Merhaba yeni parola şimdi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="52707-139">hello new password is now applied.</span></span> <span data-ttu-id="52707-140">Merhaba parola değiştirme başarısız olursa, aşağıdaki hata hello bakın:</span><span class="sxs-lookup"><span data-stu-id="52707-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![parola hatası](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="52707-142">Merhaba parola başarıyla güncelleştirildikten sonra size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="52707-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="52707-143">Daha sonra bu değiştirilmiş parola tooaccess hello aygıt yerel olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52707-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="52707-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52707-144">Next steps</span></span>
<span data-ttu-id="52707-145">Nasıl çok öğrenin[StorSimple sanal dizinizi yönetmek](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="52707-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

