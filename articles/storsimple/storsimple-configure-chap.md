---
title: "StorSimple 8000 serisi cihaz için CHAP aaaConfigure | Microsoft Docs"
description: "Nasıl tooconfigure hello karşılıklı kimlik doğrulama protokolü (CHAP) StorSimple cihazında açıklar."
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
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="52e8a-103">StorSimple cihazınız için CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52e8a-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="52e8a-104">Bu öğretici nasıl tooconfigure StorSimple cihazınız için CHAP açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="52e8a-105">Bu makalede ayrıntılı hello yordam StorSimple 1200 aygıtların yanı sıra tooStorSimple 8000 serisi geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="52e8a-106">CHAP karşılıklı kimlik doğrulama protokolü için anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="52e8a-107">Itanium tabanlı sistemler için sunucuları toovalidate hello kimliği uzak istemci tarafından kullanılan bir kimlik doğrulama düzeni değil.</span><span class="sxs-lookup"><span data-stu-id="52e8a-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="52e8a-108">Merhaba doğrulama bir paylaşılan parola veya gizli temel alır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="52e8a-109">CHAP tek yönlü olabilir (tek yönlü) veya karşılıklı (çift yönlü).</span><span class="sxs-lookup"><span data-stu-id="52e8a-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="52e8a-110">Merhaba hedef Başlatıcı doğruladığında tek yönlü CHAP türüdür.</span><span class="sxs-lookup"><span data-stu-id="52e8a-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="52e8a-111">Karşılıklı veya ters CHAP hello diğer yandan hello hedef hello Başlatıcı kimlik doğrulaması ve hello Başlatıcı hello hedef kimlik doğrulaması yapmak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="52e8a-112">Başlatıcı kimlik doğrulaması olmadan hedef kimlik doğrulaması uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="52e8a-113">Ancak, yalnızca başlatıcı kimlik doğrulaması aynı zamanda uygulanırsa, hedef kimlik doğrulama uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="52e8a-114">En iyi uygulama, CHAP tooenhance iSCSI güvenlik kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="52e8a-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="52e8a-115">IPSec StorSimple cihazlarda şu anda desteklenmiyor aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="52e8a-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="52e8a-116">Merhaba StorSimple cihazı Hello CHAP ayarları yolları aşağıdaki hello yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="52e8a-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="52e8a-117">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="52e8a-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="52e8a-118">Çift yönlü veya karşılıklı veya ters kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="52e8a-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="52e8a-119">Her durumda, hello portal hello cihaz ve hello sunucu iSCSI Initiator yazılımı için yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="52e8a-120">Merhaba bu yapılandırma için ayrıntılı adımlar öğreticiyi izleyerek hello açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="52e8a-121">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="52e8a-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="52e8a-122">Tek yönlü kimlik doğrulamada hello hedef hello Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="52e8a-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="52e8a-123">Bu kimlik doğrulama hello StorSimple cihaz ve hello iSCSI Initiator yazılımı hello konaktaki hello CHAP Başlatıcı ayarları yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="52e8a-124">StorSimple cihazınız için ayrıntılı yordamlar hello ve Windows ana bilgisayar sonraki açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="52e8a-125">tooconfigure cihazınız için tek yönlü kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="52e8a-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="52e8a-126">Merhaba hello üzerinde Klasik Azure portalı içinde **aygıtları** hello sayfasında, **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP Başlatıcı](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="52e8a-128">Aşağı kaydırın, bu sayfada ve hello **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="52e8a-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="52e8a-129">CHAP başlatıcı için bir kullanıcı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="52e8a-130">CHAP başlatıcı için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="52e8a-131">Merhaba CHAP kullanıcı adı 233'den az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="52e8a-132">Merhaba CHAP parolası 12 ile 16 arasında karakter olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="52e8a-133">Uzun bir kullanıcı adı ve parola kimlik doğrulama hatası hello Windows ana bilgisayarda sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="52e8a-134">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-134">Confirm hello password.</span></span>
3. <span data-ttu-id="52e8a-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-135">Click **Save**.</span></span> <span data-ttu-id="52e8a-136">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="52e8a-137">Tıklatın **Tamam** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="52e8a-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="52e8a-138">tooconfigure tek yönlü kimlik doğrulama hello Windows ana bilgisayar sunucusu</span><span class="sxs-lookup"><span data-stu-id="52e8a-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="52e8a-139">Merhaba Windows ana bilgisayar sunucusunda hello iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="52e8a-140">Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="52e8a-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="52e8a-141">Merhaba tıklatın **bulma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-141">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI başlatıcısı özellikleri](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="52e8a-143">Tıklatın **Portal Bul**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="52e8a-144">Merhaba, **Hedef Portal Bul** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="52e8a-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="52e8a-145">Cihazınızı Hello IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="52e8a-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="52e8a-146">Tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-146">Click **Advanced**.</span></span>
      
       ![Hedef portalı Bul](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="52e8a-148">Merhaba, **Gelişmiş ayarları** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="52e8a-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="52e8a-149">Select hello **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="52e8a-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="52e8a-150">Merhaba, **adı** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="52e8a-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="52e8a-151">Merhaba, **hedef gizli** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello parola.</span><span class="sxs-lookup"><span data-stu-id="52e8a-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="52e8a-152">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-152">Click **OK**.</span></span>
      
       ![Gelişmiş ayarlar genel](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="52e8a-154">Merhaba üzerinde **hedefleri** hello sekmesinde **iSCSI başlatıcısı özellikleri** penceresinde hello Aygıt durumu olarak görünmelidir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="52e8a-155">Bir StorSimple 1200 cihaz kullanıyorsanız, ardından her birim bir iSCSI hedefi olarak aşağıda gösterildiği gibi bağlanır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="52e8a-156">Bu nedenle, 3-4 arası adımlar, her birim için yinelenen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Ayrı hedefleri olarak takılı birimleri](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="52e8a-158">Merhaba iSCSI adını değiştirirseniz, hello yeni ad yeni iSCSI oturumları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="52e8a-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="52e8a-159">Yeni ayarları oturumunuzu kapattığınızda kadar oturumlar var ve oturum açma için tekrar kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="52e8a-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="52e8a-160">Merhaba Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için çok Git[ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="52e8a-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="52e8a-161">Çift yönlü veya karşılıklı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="52e8a-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="52e8a-162">Çift yönlü kimlik doğrulama, hello hedef hello Başlatıcı kimliğini doğrular ve hello hedef hello Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="52e8a-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="52e8a-163">Bu, hello kullanıcı tooconfigure hello CHAP Başlatıcı ayarları gibi hello hello cihaz ve iSCSI Initiator yazılımı hello konaktaki CHAP ayarları ters gerektirir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="52e8a-164">Merhaba aşağıdaki yordamlar hello adımları tooconfigure karşılıklı kimlik doğrulaması hello cihazda ve hello Windows ana bilgisayarda açıklar.</span><span class="sxs-lookup"><span data-stu-id="52e8a-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="52e8a-165">tooconfigure cihazınız karşılıklı kimlik doğrulaması için</span><span class="sxs-lookup"><span data-stu-id="52e8a-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="52e8a-166">Merhaba hello üzerinde Klasik Azure portalı içinde **aygıtları** hello sayfasında, **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP hedefi](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="52e8a-168">Aşağı kaydırın, bu sayfada ve hello **CHAP hedefi** bölümü:</span><span class="sxs-lookup"><span data-stu-id="52e8a-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="52e8a-169">Sağlayan bir **ters CHAP kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="52e8a-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="52e8a-170">Tedarik bir **ters CHAP parolası** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="52e8a-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="52e8a-171">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-171">Confirm hello password.</span></span>
3. <span data-ttu-id="52e8a-172">Merhaba, **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="52e8a-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="52e8a-173">Sağlayan bir **kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="52e8a-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="52e8a-174">Sağlayan bir **parola** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="52e8a-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="52e8a-175">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-175">Confirm hello password.</span></span>
4. <span data-ttu-id="52e8a-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-176">Click **Save**.</span></span> <span data-ttu-id="52e8a-177">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="52e8a-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="52e8a-178">Tıklatın **Tamam** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="52e8a-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="52e8a-179">Merhaba Windows tooconfigure çift yönlü kimlik doğrulamasını ana bilgisayar sunucusu</span><span class="sxs-lookup"><span data-stu-id="52e8a-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="52e8a-180">Merhaba Windows ana bilgisayar sunucusunda hello iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="52e8a-181">Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="52e8a-182">Tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="52e8a-183">Merhaba, **iSCSI Başlatıcı Karşılıklı CHAP parolası** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="52e8a-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="52e8a-184">Türü hello **ters CHAP parolası** hello Klasik Azure portalı yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="52e8a-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="52e8a-185">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52e8a-185">Click **OK**.</span></span>
      
       ![iSCSI Başlatıcı Karşılıklı CHAP parolası](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="52e8a-187">Merhaba tıklatın **hedefleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="52e8a-188">Merhaba tıklatın **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="52e8a-189">Merhaba, **tooTarget bağlanmak** iletişim kutusu, tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="52e8a-190">Merhaba, **Gelişmiş Özellikler** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="52e8a-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="52e8a-191">Select hello **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="52e8a-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="52e8a-192">Merhaba, **adı** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="52e8a-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="52e8a-193">Merhaba, **hedef gizli** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello parola.</span><span class="sxs-lookup"><span data-stu-id="52e8a-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="52e8a-194">Select hello **gerçekleştirme karşılıklı kimlik doğrulaması** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="52e8a-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Gelişmiş ayarlar karşılıklı kimlik doğrulaması](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="52e8a-196">Tıklatın **Tamam** toocomplete hello CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52e8a-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="52e8a-197">Merhaba Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için çok Git[ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="52e8a-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="52e8a-198">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="52e8a-198">Additional considerations</span></span>
<span data-ttu-id="52e8a-199">Merhaba **Hızlı Bağlan** özelliği etkinleştirilmiş CHAP sahip bağlantıları desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="52e8a-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="52e8a-200">CHAP etkin olduğunda, hello kullandığınızdan emin olun **Bağlan** hello üzerinde kullanılabilir düğmesi **hedefleri** sekmesini tooconnect tooa hedef.</span><span class="sxs-lookup"><span data-stu-id="52e8a-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Tootarget Bağlan](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="52e8a-202">Merhaba, **tooTarget bağlanmak** sunulan, select hello iletişim kutusuna **bu sık kullanılan hedefler bağlantı toohello listesine eklemek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="52e8a-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="52e8a-203">Bu, her zaman hello bilgisayarı yeniden başlatır, girişiminde toorestore hello bağlantı toohello iSCSI sık kullanılan hedefler yapılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="52e8a-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="52e8a-204">Yapılandırma sırasında hatalar</span><span class="sxs-lookup"><span data-stu-id="52e8a-204">Errors during configuration</span></span>
<span data-ttu-id="52e8a-205">CHAP yapılandırması doğru değil sonra büyük olasılıkla toosee olduğunuz bir **kimlik doğrulama hatası** hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="52e8a-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="52e8a-206">Doğrulama CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52e8a-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="52e8a-207">CHAP hello aşağıdaki adımları tamamlayarak kullanılmakta olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52e8a-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="52e8a-208">tooverify CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52e8a-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="52e8a-209">Tıklatın **sık kullanılan hedefler**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="52e8a-210">Kimlik doğrulamasının etkin hello hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="52e8a-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="52e8a-211">Tıklatın **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-211">Click **Details**.</span></span>
   
    ![iSCSI Başlatıcı özellikleri sık kullanılan hedefler](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="52e8a-213">Merhaba, **sık kullanılan hedef ayrıntıları** iletişim kutusu, Not hello hello girişi **kimlik doğrulaması** alan.</span><span class="sxs-lookup"><span data-stu-id="52e8a-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="52e8a-214">Merhaba yapılandırma başarılı olup olmadığını, yazması gerekir **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="52e8a-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Sık kullanılan hedef ayrıntıları](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="52e8a-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52e8a-216">Next steps</span></span>
* <span data-ttu-id="52e8a-217">Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="52e8a-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="52e8a-218">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="52e8a-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

