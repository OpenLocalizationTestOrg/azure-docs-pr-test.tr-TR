---
title: "StorSimple 8000 serisi aygıt için CHAP yapılandırma | Microsoft Docs"
description: "Karşılıklı Kimlik Doğrulama Protokolü (CHAP) StorSimple cihazında yapılandırılması açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 36b4e73d0336deb9560d44163fc5330d1c9d775c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="831de-103">StorSimple cihazınız için CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="831de-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="831de-104">Bu öğretici, StorSimple cihazınız için CHAP yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="831de-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="831de-105">Bu makalede ayrıntılı yordam StorSimple 1200 aygıtların yanı sıra StorSimple 8000 serisi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="831de-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="831de-106">CHAP karşılıklı kimlik doğrulama protokolü için anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="831de-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="831de-107">Bu sunucuları tarafından uzak istemcilerin kimliğini doğrulamak için kullanılan bir kimlik doğrulama düzeni olur.</span><span class="sxs-lookup"><span data-stu-id="831de-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="831de-108">Doğrulama bir paylaşılan parola veya gizli temel alır.</span><span class="sxs-lookup"><span data-stu-id="831de-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="831de-109">CHAP tek yönlü olabilir (tek yönlü) veya karşılıklı (çift yönlü).</span><span class="sxs-lookup"><span data-stu-id="831de-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="831de-110">Hedef Başlatıcı doğruladığında tek yönlü CHAP türüdür.</span><span class="sxs-lookup"><span data-stu-id="831de-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="831de-111">Karşılıklı veya ters CHAP, diğer yandan, hedef, başlatıcı kimlik doğrulaması yapmak ve Başlatıcı Hedef kimlik doğrulaması yapmak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="831de-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="831de-112">Başlatıcı kimlik doğrulaması olmadan hedef kimlik doğrulaması uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="831de-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="831de-113">Ancak, yalnızca başlatıcı kimlik doğrulaması aynı zamanda uygulanırsa, hedef kimlik doğrulama uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="831de-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="831de-114">En iyi uygulama, iSCSI güvenliğini artırmak için CHAP kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="831de-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="831de-115">IPSec StorSimple cihazlarda şu anda desteklenmiyor aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="831de-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="831de-116">StorSimple cihazında CHAP ayarları aşağıdaki yollarla yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="831de-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="831de-117">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="831de-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="831de-118">Çift yönlü veya karşılıklı veya ters kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="831de-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="831de-119">Her durumda, cihaz ve sunucu iSCSI Initiator yazılımı için portal yapılandırılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="831de-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="831de-120">Bu yapılandırma için ayrıntılı adımlar aşağıdaki öğreticide açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="831de-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="831de-121">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="831de-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="831de-122">Tek yönlü kimlik doğrulamada hedef Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="831de-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="831de-123">Bu kimlik doğrulama StorSimple cihazı ve iSCSI başlatıcısı yazılımı CHAP Başlatıcı ayarları yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="831de-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="831de-124">StorSimple cihazı ve Windows ana bilgisayar için ayrıntılı yordamlar sonraki açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="831de-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="831de-125">Tek yönlü kimlik doğrulama için Cihazınızı yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="831de-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="831de-126">Azure Klasik portalında üzerinde **aygıtları** sayfasında, **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="831de-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP Başlatıcı](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="831de-128">Bu sayfada ve buna aşağı kaydırın **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="831de-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="831de-129">CHAP başlatıcı için bir kullanıcı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="831de-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="831de-130">CHAP başlatıcı için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="831de-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="831de-131">CHAP kullanıcı adı 233'den az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="831de-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="831de-132">CHAP parolası 12 ile 16 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="831de-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="831de-133">Uzun bir kullanıcı adı ve parola kimlik doğrulama hatası Windows ana bilgisayardaki sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="831de-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="831de-134">Parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="831de-134">Confirm the password.</span></span>
3. <span data-ttu-id="831de-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="831de-135">Click **Save**.</span></span> <span data-ttu-id="831de-136">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="831de-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="831de-137">Değişiklikleri kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="831de-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="831de-138">Windows ana bilgisayar sunucusunda tek yönlü kimlik doğrulamasını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="831de-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="831de-139">Windows ana bilgisayarı sunucusunda, iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="831de-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="831de-140">İçinde **iSCSI başlatıcısı özellikleri** penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="831de-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="831de-141">Tıklatın **bulma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="831de-141">Click the **Discovery** tab.</span></span>
      
       ![iSCSI başlatıcısı özellikleri](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="831de-143">Tıklatın **Portal Bul**.</span><span class="sxs-lookup"><span data-stu-id="831de-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="831de-144">İçinde **Hedef Portal Bul** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="831de-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="831de-145">Cihazınızı IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="831de-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="831de-146">Tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="831de-146">Click **Advanced**.</span></span>
      
       ![Hedef portalı Bul](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="831de-148">İçinde **Gelişmiş ayarları** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="831de-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="831de-149">Seçin **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="831de-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="831de-150">İçinde **adı** alanında, Klasik portalda CHAP başlatıcı için belirtilen kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="831de-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="831de-151">İçinde **hedef gizli** alan, Klasik portalda CHAP başlatıcı için belirtilen parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="831de-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="831de-152">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="831de-152">Click **OK**.</span></span>
      
       ![Gelişmiş ayarlar genel](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="831de-154">Üzerinde **hedefleri** sekmesinde **iSCSI başlatıcısı özellikleri** penceresinde, cihaz durumu olarak görünmelidir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="831de-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="831de-155">Bir StorSimple 1200 cihaz kullanıyorsanız, ardından her birim bir iSCSI hedefi olarak aşağıda gösterildiği gibi bağlanır.</span><span class="sxs-lookup"><span data-stu-id="831de-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="831de-156">Bu nedenle, 3-4 arası adımlar, her birim için yinelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="831de-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![Ayrı hedefleri olarak takılı birimleri](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="831de-158">İSCSI adını değiştirirseniz, yeni ad yeni iSCSI oturumları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="831de-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="831de-159">Yeni ayarları oturumunuzu kapattığınızda kadar oturumlar var ve oturum açma için tekrar kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="831de-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="831de-160">Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için Git [ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="831de-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="831de-161">Çift yönlü veya karşılıklı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="831de-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="831de-162">Çift yönlü kimlik doğrulama, hedef Başlatıcı kimliğini doğrular ve hedef Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="831de-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="831de-163">Bu cihaz ve iSCSI Initiator yazılımı konaktaki CHAP Başlatıcı Ayarları yanı sıra ters CHAP ayarlarını yapılandırmak kullanıcının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="831de-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="831de-164">Aşağıdaki yordamlar, Windows ana bilgisayar ve aygıt üzerinde karşılıklı kimlik doğrulaması yapılandırmak için gereken adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="831de-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="831de-165">Karşılıklı kimlik doğrulama için Cihazınızı yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="831de-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="831de-166">Azure Klasik portalında üzerinde **aygıtları** sayfasında, **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="831de-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP hedefi](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="831de-168">Bu sayfada ve buna aşağı kaydırın **CHAP hedefi** bölümü:</span><span class="sxs-lookup"><span data-stu-id="831de-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="831de-169">Sağlayan bir **ters CHAP kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="831de-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="831de-170">Tedarik bir **ters CHAP parolası** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="831de-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="831de-171">Parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="831de-171">Confirm the password.</span></span>
3. <span data-ttu-id="831de-172">İçinde **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="831de-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="831de-173">Sağlayan bir **kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="831de-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="831de-174">Sağlayan bir **parola** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="831de-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="831de-175">Parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="831de-175">Confirm the password.</span></span>
4. <span data-ttu-id="831de-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="831de-176">Click **Save**.</span></span> <span data-ttu-id="831de-177">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="831de-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="831de-178">Değişiklikleri kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="831de-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="831de-179">Windows ana bilgisayar sunucusunda çift yönlü kimlik doğrulamasını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="831de-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="831de-180">Windows ana bilgisayarı sunucusunda, iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="831de-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="831de-181">İçinde **iSCSI başlatıcısı özellikleri** penceresinde tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="831de-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="831de-182">Tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="831de-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="831de-183">İçinde **iSCSI Başlatıcı Karşılıklı CHAP parolası** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="831de-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="831de-184">Tür **ters CHAP parolası** Azure Klasik Portalı'nda yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="831de-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="831de-185">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="831de-185">Click **OK**.</span></span>
      
       ![iSCSI Başlatıcı Karşılıklı CHAP parolası](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="831de-187">Tıklatın **hedefleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="831de-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="831de-188">Tıklatın **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="831de-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="831de-189">İçinde **bağlanmak için hedef** iletişim kutusu, tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="831de-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="831de-190">İçinde **Gelişmiş Özellikler** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="831de-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="831de-191">Seçin **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="831de-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="831de-192">İçinde **adı** alanında, Klasik portalda CHAP başlatıcı için belirtilen kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="831de-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="831de-193">İçinde **hedef gizli** alan, Klasik portalda CHAP başlatıcı için belirtilen parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="831de-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="831de-194">Seçin **gerçekleştirme karşılıklı kimlik doğrulaması** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="831de-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Gelişmiş ayarlar karşılıklı kimlik doğrulaması](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="831de-196">Tıklatın **Tamam** CHAP yapılandırmasını tamamlamak için</span><span class="sxs-lookup"><span data-stu-id="831de-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="831de-197">Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için Git [ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="831de-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="831de-198">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="831de-198">Additional considerations</span></span>
<span data-ttu-id="831de-199">**Hızlı Bağlan** özelliği etkinleştirilmiş CHAP sahip bağlantıları desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="831de-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="831de-200">CHAP etkinleştirildiğinde kullandığınızdan emin olun **Bağlan** kullanılabilir düğmesi **hedefleri** sekmesinde bir hedef bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="831de-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Hedefe Bağlan](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="831de-202">İçinde **hedef Bağlan** sunulur, iletişim kutusu seç **Bu bağlantı sık kullanılan hedefler listesine eklemek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="831de-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="831de-203">Bu bilgisayar yeniden başlatıldığında her girişiminde bağlantı iSCSI sık kullanılan hedefler geri yüklemek için yapılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="831de-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="831de-204">Yapılandırma sırasında hatalar</span><span class="sxs-lookup"><span data-stu-id="831de-204">Errors during configuration</span></span>
<span data-ttu-id="831de-205">CHAP yapılandırması doğru değil sonra görmek büyük olasılıkla bir **kimlik doğrulama hatası** hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="831de-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="831de-206">Doğrulama CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="831de-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="831de-207">Aşağıdaki adımları tamamlayarak CHAP kullanılmakta olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="831de-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="831de-208">CHAP yapılandırmasını doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="831de-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="831de-209">Tıklatın **sık kullanılan hedefler**.</span><span class="sxs-lookup"><span data-stu-id="831de-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="831de-210">Kimlik doğrulamasının etkin hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="831de-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="831de-211">Tıklatın **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="831de-211">Click **Details**.</span></span>
   
    ![iSCSI Başlatıcı özellikleri sık kullanılan hedefler](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="831de-213">İçinde **sık kullanılan hedef ayrıntıları** iletişim kutusunda, giriş Not **kimlik doğrulaması** alan.</span><span class="sxs-lookup"><span data-stu-id="831de-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="831de-214">Yapılandırma başarılı olup olmadığını, yazması gerekir **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="831de-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Sık kullanılan hedef ayrıntıları](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="831de-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="831de-216">Next steps</span></span>
* <span data-ttu-id="831de-217">Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="831de-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="831de-218">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="831de-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

