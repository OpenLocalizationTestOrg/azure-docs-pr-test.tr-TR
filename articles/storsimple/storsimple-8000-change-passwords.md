---
title: "aaaChange StorSimple parolalarınızı | Microsoft Docs"
description: "Nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti toochange StorSimple Snapshot Manager ve cihaz Yöneticisi parolalarınızı açıklar."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="bcd2b-103">StorSimple parolalarınızı Hello StorSimple cihaz Yöneticisi hizmeti toochange kullanın</span><span class="sxs-lookup"><span data-stu-id="bcd2b-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="bcd2b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bcd2b-104">Overview</span></span>
<span data-ttu-id="bcd2b-105">Azure portal hello **aygıt ayarları** seçeneği StorSimple cihaz Yöneticisi hizmeti tarafından yönetilen bir StorSimple cihazda yapılandırabilirsiniz tüm hello aygıt parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="bcd2b-106">Bu öğretici hello nasıl kullanabileceğinizi açıklar **güvenlik** altında seçeneği **aygıt ayarları** toochange aygıt yöneticinize veya StorSimple Snapshot Manager parolası.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="bcd2b-107">Değişiklik hello cihaz Yöneticisi parolası</span><span class="sxs-lookup"><span data-stu-id="bcd2b-107">Change hello device administrator password</span></span>
<span data-ttu-id="bcd2b-108">Windows PowerShell arabirimi tooaccess hello StorSimple cihazı kullanmak için gerekli tooenter bir cihaz Yöneticisi parolası olur.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="bcd2b-109">Bir hizmetle Hello ilk StorSimple cihaz kaydedildiğinde hello varsayılan bu arabirimin paroladır *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="bcd2b-110">Verilerinizin Hello güvenlik için bu parolayı gerekli toochange olan hello kayıt işleminin hello sonuna.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="bcd2b-111">Bu parolayı değiştirmeden hello kayıt işleminden çıkmak olamaz.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="bcd2b-112">Daha fazla bilgi için bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="bcd2b-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="bcd2b-113">Merhaba Windows PowerShell arabirimi üzerinden kayıt sırasında ilk ayarlandı hello parola hello Azure portal daha sonra değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="bcd2b-114">Aşağıdaki adımları toochange hello cihaz Yöneticisi parolası hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="bcd2b-115">toochange hello cihaz Yöneticisi parolası</span><span class="sxs-lookup"><span data-stu-id="bcd2b-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="bcd2b-116">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="bcd2b-117">Merhaba Tablo listesi aygıtları gelen, seçin ve hello cihaz parolasını tıklatın toochange düşündüğünüz.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="bcd2b-118">Merhaba, **ayarları** dikey penceresinde çok Git**Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="bcd2b-119">Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **parola** toochange hello cihaz Yöneticisi parolası.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="bcd2b-120">Merhaba, **parola** dikey penceresinde 8 too15 karakterler içeren bir yönetici parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="bcd2b-121">Merhaba parola 3 veya daha çok büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="bcd2b-122">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="bcd2b-123">Tıklatın **kaydetmek** tıklatıp onaylamanız istendiğinde, **Evet**.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="bcd2b-124">Merhaba cihaz Yöneticisi parolası şimdi güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="bcd2b-125">Bu değiştirilmiş parola tooaccess hello Windows PowerShell arabirimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="bcd2b-126">Merhaba StorSimple Snapshot Manager parolasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="bcd2b-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="bcd2b-127">StorSimple Snapshot Manager yazılımı Windows ana bilgisayarınıza bulunur ve StorSimple Cihazınızı hello form yerel ve bulut anlık görüntüleri toomanage yedeklerini yöneticilerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="bcd2b-128">StorSimple anlık görüntü Yöneticisi'nde bir aygıt yapılandırma sırasında sizden istenir tooprovide hello aygıt IP adresi ve parola tooauthenticate depolama cihazı.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="bcd2b-129">Ayarlayabilir veya hello parola için StorSimple Snapshot Manager hello Azure portal değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="bcd2b-130">Aşağıdaki adımları tooset hello gerçekleştirmek veya hello StorSimple Snapshot Manager parolasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="bcd2b-131">tooset hello StorSimple Snapshot Manager parolası</span><span class="sxs-lookup"><span data-stu-id="bcd2b-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="bcd2b-132">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="bcd2b-133">Merhaba Tablo listesi aygıtları gelen, seçin ve hello aygıtı tıklatın StorSimple Snapshot Manager parolasını tooset düşündüğünüz veya değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="bcd2b-134">Merhaba, **ayarları** dikey penceresinde çok Git**Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="bcd2b-135">Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **parola** tooset ya da değişiklik hello StorSimple Snapshot Manager parolası.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="bcd2b-136">Merhaba, **parola** dikey penceresinde, 14 veya 15 karakter olan bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="bcd2b-137">3 veya daha çok büyük harf, küçük harfler, sayısal ve özel karakter bir bileşimi hello parola içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="bcd2b-138">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="bcd2b-139">Tıklatın **kaydetmek** tıklatıp onaylamanız istendiğinde, **Evet**.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="bcd2b-140">Merhaba StorSimple Snapshot Manager parolası şimdi güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcd2b-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd2b-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bcd2b-141">Next steps</span></span>
* <span data-ttu-id="bcd2b-142">Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2b-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="bcd2b-143">Daha fazla bilgi edinmek [cihaz yapılandırmanızı değiştirme](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2b-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="bcd2b-144">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2b-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

