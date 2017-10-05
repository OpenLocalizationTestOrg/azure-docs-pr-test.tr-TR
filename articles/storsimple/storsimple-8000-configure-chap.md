---
title: "StorSimple 8000 serisi aygıt için CHAP yapılandırma | Microsoft Docs"
description: "Karşılıklı Kimlik Doğrulama Protokolü (CHAP) StorSimple cihazında yapılandırılması açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 61e0877187759d76b6f7efcef0a5ed8bec8500fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="fbf3a-103">StorSimple cihazınız için CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbf3a-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="fbf3a-104">Bu öğretici, StorSimple cihazınız için CHAP yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="fbf3a-105">Bu makalede ayrıntılı yordam StorSimple 8000 serisi cihazlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-105">The procedure detailed in this article applies to StorSimple 8000 series devices.</span></span>

<span data-ttu-id="fbf3a-106">CHAP karşılıklı kimlik doğrulama protokolü için anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="fbf3a-107">Bu sunucuları tarafından uzak istemcilerin kimliğini doğrulamak için kullanılan bir kimlik doğrulama düzeni olur.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="fbf3a-108">Doğrulama bir paylaşılan parola veya gizli temel alır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="fbf3a-109">CHAP (tek yönlü) bir yolu olabilir veya karşılıklı (çift yönlü).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="fbf3a-110">Hedef Başlatıcı doğruladığında bir CHAP yoludur.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-110">One way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="fbf3a-111">Karşılıklı veya ters CHAP Başlatıcı Hedef doğrular ve hedef Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-111">In mutual or reverse CHAP, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="fbf3a-112">Başlatıcı kimlik doğrulaması olmadan hedef kimlik doğrulaması uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="fbf3a-113">Ancak, yalnızca başlatıcı kimlik doğrulaması aynı zamanda uygulanırsa, hedef kimlik doğrulama uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="fbf3a-114">En iyi uygulama, iSCSI güvenliğini artırmak için CHAP kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="fbf3a-115">IPSec StorSimple cihazlarda şu anda desteklenmiyor aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="fbf3a-116">StorSimple cihazında CHAP ayarları aşağıdaki yollarla yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="fbf3a-117">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fbf3a-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="fbf3a-118">Çift yönlü veya karşılıklı veya ters kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fbf3a-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="fbf3a-119">Her durumda, cihaz ve sunucu iSCSI Initiator yazılımı için portal yapılandırılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="fbf3a-120">Bu yapılandırma için ayrıntılı adımlar aşağıdaki öğreticide açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="fbf3a-121">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fbf3a-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="fbf3a-122">Tek yönlü kimlik doğrulamada hedef Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="fbf3a-123">Bu kimlik doğrulama StorSimple cihazı ve iSCSI başlatıcısı yazılımı CHAP Başlatıcı ayarları yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="fbf3a-124">StorSimple cihazı ve Windows ana bilgisayar için ayrıntılı yordamlar sonraki açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="fbf3a-125">Tek yönlü kimlik doğrulama için Cihazınızı yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="fbf3a-125">To configure your device for one-way authentication</span></span>

1. <span data-ttu-id="fbf3a-126">Azure portalında StorSimple cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-126">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="fbf3a-127">Tıklatın **aygıtları** seçin ve istediğiniz CHAP yapılandırmak için bir cihaza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-127">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="fbf3a-128">Git **Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-128">Go to **Device settings > Security**.</span></span> <span data-ttu-id="fbf3a-129">İçinde **güvenlik ayarları** dikey penceresinde tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-129">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP Başlatıcı](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="fbf3a-131">İçinde **CHAP** dikey penceresinde ve **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-131">In the **CHAP** blade, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="fbf3a-132">CHAP başlatıcı için bir kullanıcı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="fbf3a-133">CHAP başlatıcı için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="fbf3a-134">CHAP kullanıcı adı 233'den az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-134">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="fbf3a-135">CHAP parolası 12 ile 16 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-135">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="fbf3a-136">Uzun bir kullanıcı adı ve parola kimlik doğrulama hatası Windows ana bilgisayardaki sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-136">A longer user name or password results in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="fbf3a-137">Parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-137">Confirm the password.</span></span>

       ![CHAP Başlatıcı](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="fbf3a-139">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-139">Click **Save**.</span></span> <span data-ttu-id="fbf3a-140">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-140">A confirmation message is displayed.</span></span> <span data-ttu-id="fbf3a-141">Değişiklikleri kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-141">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="fbf3a-142">Windows ana bilgisayar sunucusunda tek yönlü kimlik doğrulamasını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="fbf3a-142">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="fbf3a-143">Windows ana bilgisayarı sunucusunda, iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-143">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="fbf3a-144">İçinde **iSCSI başlatıcısı özellikleri** penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-144">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="fbf3a-145">Tıklatın **bulma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-145">Click the **Discovery** tab.</span></span>
      
       ![iSCSI başlatıcısı özellikleri](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="fbf3a-147">Tıklatın **Portal Bul**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="fbf3a-148">İçinde **Hedef Portal Bul** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-148">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="fbf3a-149">Cihazınızı IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-149">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="fbf3a-150">Tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-150">Click **Advanced**.</span></span>
      
       ![Hedef portalı Bul](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="fbf3a-152">İçinde **Gelişmiş ayarları** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-152">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="fbf3a-153">Seçin **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-153">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="fbf3a-154">İçinde **adı** alanında, Klasik portalda CHAP başlatıcı için belirtilen kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-154">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="fbf3a-155">İçinde **hedef gizli** alan, Klasik portalda CHAP başlatıcı için belirtilen parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-155">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="fbf3a-156">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-156">Click **OK**.</span></span>
      
       ![Gelişmiş ayarlar genel](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="fbf3a-158">Üzerinde **hedefleri** sekmesinde **iSCSI başlatıcısı özellikleri** penceresinde, cihaz durumu olarak görünmelidir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-158">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="fbf3a-159">Bir StorSimple 1200 cihaz kullanıyorsanız, her birimin bir iSCSI hedefi olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="fbf3a-160">Bu nedenle, 3-4 arası adımlar, her birim için yinelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-160">Hence, steps 3-4 will need to be repeated for each volume.</span></span>
   
    ![Ayrı hedefleri olarak takılı birimleri](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="fbf3a-162">İSCSI adını değiştirirseniz, yeni ad yeni iSCSI oturumları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-162">If you change the iSCSI name, the new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="fbf3a-163">Yeni ayarları oturumunuzu kapattığınızda kadar oturumlar var ve oturum açma için tekrar kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="fbf3a-164">Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için Git [ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-164">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="fbf3a-165">Çift yönlü veya karşılıklı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fbf3a-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="fbf3a-166">Çift yönlü kimlik doğrulama, hedef Başlatıcı kimliğini doğrular ve hedef Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-166">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="fbf3a-167">Bu yordam kullanıcıya CHAP Başlatıcı ayarlarını yapılandırabilir, cihaz ve iSCSI başlatıcısı yazılımı ters CHAP ayarları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-167">This procedure requires the user to configure the CHAP initiator settings, reverse CHAP settings on the device, and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="fbf3a-168">Aşağıdaki yordamlar, Windows ana bilgisayar ve aygıt üzerinde karşılıklı kimlik doğrulaması yapılandırmak için gereken adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-168">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="fbf3a-169">Karşılıklı kimlik doğrulama için Cihazınızı yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="fbf3a-169">To configure your device for mutual authentication</span></span>

1. <span data-ttu-id="fbf3a-170">Azure portalında StorSimple cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-170">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="fbf3a-171">Tıklatın **aygıtları** seçin ve istediğiniz CHAP yapılandırmak için bir cihaza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-171">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="fbf3a-172">Git **Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-172">Go to **Device settings > Security**.</span></span> <span data-ttu-id="fbf3a-173">İçinde **güvenlik ayarları** dikey penceresinde tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-173">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP hedefi](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="fbf3a-175">Bu sayfada ve buna aşağı kaydırın **CHAP hedefi** bölümü:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-175">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="fbf3a-176">Sağlayan bir **ters CHAP kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="fbf3a-177">Tedarik bir **ters CHAP parolası** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="fbf3a-178">Parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-178">Confirm the password.</span></span>
3. <span data-ttu-id="fbf3a-179">İçinde **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-179">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="fbf3a-180">Sağlayan bir **kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="fbf3a-181">Sağlayan bir **parola** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="fbf3a-182">Parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-182">Confirm the password.</span></span>

       ![CHAP Başlatıcı](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="fbf3a-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-184">Click **Save**.</span></span> <span data-ttu-id="fbf3a-185">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-185">A confirmation message is displayed.</span></span> <span data-ttu-id="fbf3a-186">Değişiklikleri kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-186">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="fbf3a-187">Windows ana bilgisayar sunucusunda çift yönlü kimlik doğrulamasını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="fbf3a-187">To configure bidirectional authentication on the Windows host server</span></span>

1. <span data-ttu-id="fbf3a-188">Windows ana bilgisayarı sunucusunda, iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-188">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="fbf3a-189">İçinde **iSCSI başlatıcısı özellikleri** penceresinde tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-189">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="fbf3a-190">Tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="fbf3a-191">İçinde **iSCSI Başlatıcı Karşılıklı CHAP parolası** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-191">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="fbf3a-192">Tür **ters CHAP parolası** Azure Portalı'nda yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-192">Type the **Reverse CHAP Password** that you configured in the Azure portal.</span></span>
   2. <span data-ttu-id="fbf3a-193">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-193">Click **OK**.</span></span>
      
       ![iSCSI Başlatıcı Karşılıklı CHAP parolası](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="fbf3a-195">Tıklatın **hedefleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-195">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="fbf3a-196">Tıklatın **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-196">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="fbf3a-197">İçinde **bağlanmak için hedef** iletişim kutusu, tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-197">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="fbf3a-198">İçinde **Gelişmiş Özellikler** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-198">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="fbf3a-199">Seçin **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-199">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="fbf3a-200">İçinde **adı** alanında, Klasik portalda CHAP başlatıcı için belirtilen kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-200">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="fbf3a-201">İçinde **hedef gizli** alan, Klasik portalda CHAP başlatıcı için belirtilen parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-201">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="fbf3a-202">Seçin **gerçekleştirme karşılıklı kimlik doğrulaması** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-202">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Gelişmiş ayarlar karşılıklı kimlik doğrulaması](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="fbf3a-204">Tıklatın **Tamam** CHAP yapılandırmasını tamamlamak için</span><span class="sxs-lookup"><span data-stu-id="fbf3a-204">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="fbf3a-205">Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için Git [ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-205">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="fbf3a-206">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="fbf3a-206">Additional considerations</span></span>

<span data-ttu-id="fbf3a-207">**Hızlı Bağlan** özelliği etkinleştirilmiş CHAP sahip bağlantıları desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-207">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="fbf3a-208">CHAP etkinleştirildiğinde kullandığınızdan emin olun **Bağlan** kullanılabilir düğmesi **hedefleri** sekmesinde bir hedef bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-208">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Hedefe Bağlan](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="fbf3a-210">İçinde **hedef Bağlan** sunulur, iletişim kutusu seç **Bu bağlantı sık kullanılan hedefler listesine eklemek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-210">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="fbf3a-211">Bu seçim, bilgisayar yeniden başlatıldığında her girişiminde bağlantı iSCSI sık kullanılan hedefler geri yüklemek için yapılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-211">This selection ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="fbf3a-212">Yapılandırma sırasında hatalar</span><span class="sxs-lookup"><span data-stu-id="fbf3a-212">Errors during configuration</span></span>

<span data-ttu-id="fbf3a-213">CHAP yapılandırması doğru değil sonra görmek büyük olasılıkla bir **kimlik doğrulama hatası** hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-213">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="fbf3a-214">Doğrulama CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbf3a-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="fbf3a-215">Aşağıdaki adımları tamamlayarak CHAP kullanılmakta olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-215">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="fbf3a-216">CHAP yapılandırmasını doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="fbf3a-216">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="fbf3a-217">Tıklatın **sık kullanılan hedefler**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="fbf3a-218">Kimlik doğrulamasının etkin hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-218">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="fbf3a-219">Tıklatın **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-219">Click **Details**.</span></span>
   
    ![iSCSI Başlatıcı özellikleri sık kullanılan hedefler](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="fbf3a-221">İçinde **sık kullanılan hedef ayrıntıları** iletişim kutusunda, giriş Not **kimlik doğrulaması** alan.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-221">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="fbf3a-222">Yapılandırma başarılı olup olmadığını, yazması gerekir **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-222">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Sık kullanılan hedef ayrıntıları](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="fbf3a-224">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fbf3a-224">Next steps</span></span>

* <span data-ttu-id="fbf3a-225">Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="fbf3a-226">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-226">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

