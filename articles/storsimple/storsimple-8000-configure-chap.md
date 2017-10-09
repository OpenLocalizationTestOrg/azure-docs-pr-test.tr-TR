---
title: "StorSimple 8000 serisi cihaz için CHAP aaaConfigure | Microsoft Docs"
description: "Nasıl tooconfigure hello karşılıklı kimlik doğrulama protokolü (CHAP) StorSimple cihazında açıklar."
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
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="ade96-103">StorSimple cihazınız için CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ade96-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="ade96-104">Bu öğretici nasıl tooconfigure StorSimple cihazınız için CHAP açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ade96-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="ade96-105">Bu makalede ayrıntılı hello yordam tooStorSimple 8000 serisi cihazlar geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ade96-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="ade96-106">CHAP karşılıklı kimlik doğrulama protokolü için anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ade96-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="ade96-107">Itanium tabanlı sistemler için sunucuları toovalidate hello kimliği uzak istemci tarafından kullanılan bir kimlik doğrulama düzeni değil.</span><span class="sxs-lookup"><span data-stu-id="ade96-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="ade96-108">Merhaba doğrulama bir paylaşılan parola veya gizli temel alır.</span><span class="sxs-lookup"><span data-stu-id="ade96-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="ade96-109">CHAP (tek yönlü) bir yolu olabilir veya karşılıklı (çift yönlü).</span><span class="sxs-lookup"><span data-stu-id="ade96-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="ade96-110">Merhaba hedef Başlatıcı doğruladığında bir CHAP yoludur.</span><span class="sxs-lookup"><span data-stu-id="ade96-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="ade96-111">Karşılıklı veya ters CHAP hello hedef hello Başlatıcı kimliğini doğrular ve hello hedef hello Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="ade96-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="ade96-112">Başlatıcı kimlik doğrulaması olmadan hedef kimlik doğrulaması uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="ade96-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="ade96-113">Ancak, yalnızca başlatıcı kimlik doğrulaması aynı zamanda uygulanırsa, hedef kimlik doğrulama uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="ade96-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="ade96-114">En iyi uygulama, CHAP tooenhance iSCSI güvenlik kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ade96-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="ade96-115">IPSec StorSimple cihazlarda şu anda desteklenmiyor aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ade96-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="ade96-116">Merhaba StorSimple cihazı Hello CHAP ayarları yolları aşağıdaki hello yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="ade96-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="ade96-117">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ade96-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="ade96-118">Çift yönlü veya karşılıklı veya ters kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ade96-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="ade96-119">Her durumda, hello portal hello cihaz ve hello sunucu iSCSI Initiator yazılımı için yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade96-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="ade96-120">Merhaba bu yapılandırma için ayrıntılı adımlar öğreticiyi izleyerek hello açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ade96-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="ade96-121">Tek yönlü veya tek yönlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ade96-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="ade96-122">Tek yönlü kimlik doğrulamada hello hedef hello Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="ade96-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="ade96-123">Bu kimlik doğrulama hello StorSimple cihaz ve hello iSCSI Initiator yazılımı hello konaktaki hello CHAP Başlatıcı ayarları yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade96-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="ade96-124">StorSimple cihazınız için ayrıntılı yordamlar hello ve Windows ana bilgisayar sonraki açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ade96-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="ade96-125">tooconfigure cihazınız için tek yönlü kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="ade96-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="ade96-126">Hello Azure portal, tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="ade96-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ade96-127">Tıklatın **aygıtları** seçin ve tooconfigure CHAP istediğiniz bir cihaza tıklayın için.</span><span class="sxs-lookup"><span data-stu-id="ade96-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="ade96-128">Çok Git**Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="ade96-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="ade96-129">Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="ade96-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP Başlatıcı](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="ade96-131">Merhaba, **CHAP** dikey penceresinde ve hello **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="ade96-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="ade96-132">CHAP başlatıcı için bir kullanıcı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="ade96-133">CHAP başlatıcı için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="ade96-134">Merhaba CHAP kullanıcı adı 233'den az karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ade96-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="ade96-135">Merhaba CHAP parolası 12 ile 16 arasında karakter olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade96-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="ade96-136">Uzun bir kullanıcı adı ve parola kimlik doğrulama hatası hello Windows ana bilgisayarda sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ade96-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="ade96-137">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-137">Confirm hello password.</span></span>

       ![CHAP Başlatıcı](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="ade96-139">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-139">Click **Save**.</span></span> <span data-ttu-id="ade96-140">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ade96-140">A confirmation message is displayed.</span></span> <span data-ttu-id="ade96-141">Tıklatın **Tamam** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="ade96-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="ade96-142">tooconfigure tek yönlü kimlik doğrulama hello Windows ana bilgisayar sunucusu</span><span class="sxs-lookup"><span data-stu-id="ade96-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="ade96-143">Merhaba Windows ana bilgisayar sunucusunda hello iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="ade96-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="ade96-144">Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ade96-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="ade96-145">Merhaba tıklatın **bulma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ade96-145">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI başlatıcısı özellikleri](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="ade96-147">Tıklatın **Portal Bul**.</span><span class="sxs-lookup"><span data-stu-id="ade96-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="ade96-148">Merhaba, **Hedef Portal Bul** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="ade96-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="ade96-149">Cihazınızı Hello IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ade96-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="ade96-150">Tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="ade96-150">Click **Advanced**.</span></span>
      
       ![Hedef portalı Bul](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="ade96-152">Merhaba, **Gelişmiş ayarları** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="ade96-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="ade96-153">Select hello **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ade96-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="ade96-154">Merhaba, **adı** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="ade96-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="ade96-155">Merhaba, **hedef gizli** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello parola.</span><span class="sxs-lookup"><span data-stu-id="ade96-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="ade96-156">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-156">Click **OK**.</span></span>
      
       ![Gelişmiş ayarlar genel](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="ade96-158">Merhaba üzerinde **hedefleri** hello sekmesinde **iSCSI başlatıcısı özellikleri** penceresinde hello Aygıt durumu olarak görünmelidir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="ade96-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="ade96-159">Bir StorSimple 1200 cihaz kullanıyorsanız, her birimin bir iSCSI hedefi olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="ade96-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="ade96-160">Bu nedenle, 3-4 arası adımlar, her birim için yinelenen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade96-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Ayrı hedefleri olarak takılı birimleri](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="ade96-162">Merhaba iSCSI adını değiştirirseniz, hello yeni ad yeni iSCSI oturumları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ade96-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="ade96-163">Yeni ayarları oturumunuzu kapattığınızda kadar oturumlar var ve oturum açma için tekrar kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ade96-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="ade96-164">Merhaba Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için çok Git[ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="ade96-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="ade96-165">Çift yönlü veya karşılıklı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ade96-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="ade96-166">Çift yönlü kimlik doğrulama, hello hedef hello Başlatıcı kimliğini doğrular ve hello hedef hello Başlatıcı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="ade96-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="ade96-167">Bu yordamı hello kullanıcı tooconfigure hello CHAP Başlatıcı Ayarları gerektirir, hello cihaz ve iSCSI Initiator yazılımı hello ana bilgisayarda ters CHAP ayarları.</span><span class="sxs-lookup"><span data-stu-id="ade96-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="ade96-168">Merhaba aşağıdaki yordamlar hello adımları tooconfigure karşılıklı kimlik doğrulaması hello cihazda ve hello Windows ana bilgisayarda açıklar.</span><span class="sxs-lookup"><span data-stu-id="ade96-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="ade96-169">tooconfigure cihazınız karşılıklı kimlik doğrulaması için</span><span class="sxs-lookup"><span data-stu-id="ade96-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="ade96-170">Hello Azure portal, tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="ade96-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ade96-171">Tıklatın **aygıtları** seçin ve tooconfigure CHAP istediğiniz bir cihaza tıklayın için.</span><span class="sxs-lookup"><span data-stu-id="ade96-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="ade96-172">Çok Git**Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="ade96-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="ade96-173">Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="ade96-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP hedefi](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="ade96-175">Aşağı kaydırın, bu sayfada ve hello **CHAP hedefi** bölümü:</span><span class="sxs-lookup"><span data-stu-id="ade96-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="ade96-176">Sağlayan bir **ters CHAP kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="ade96-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="ade96-177">Tedarik bir **ters CHAP parolası** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="ade96-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="ade96-178">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-178">Confirm hello password.</span></span>
3. <span data-ttu-id="ade96-179">Merhaba, **CHAP Başlatıcı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="ade96-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="ade96-180">Sağlayan bir **kullanıcı adı** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="ade96-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="ade96-181">Sağlayan bir **parola** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="ade96-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="ade96-182">Merhaba parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-182">Confirm hello password.</span></span>

       ![CHAP Başlatıcı](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="ade96-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-184">Click **Save**.</span></span> <span data-ttu-id="ade96-185">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ade96-185">A confirmation message is displayed.</span></span> <span data-ttu-id="ade96-186">Tıklatın **Tamam** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="ade96-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="ade96-187">Merhaba Windows tooconfigure çift yönlü kimlik doğrulamasını ana bilgisayar sunucusu</span><span class="sxs-lookup"><span data-stu-id="ade96-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="ade96-188">Merhaba Windows ana bilgisayar sunucusunda hello iSCSI başlatıcısı başlatın.</span><span class="sxs-lookup"><span data-stu-id="ade96-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="ade96-189">Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ade96-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="ade96-190">Tıklatın **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="ade96-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="ade96-191">Merhaba, **iSCSI Başlatıcı Karşılıklı CHAP parolası** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="ade96-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="ade96-192">Türü hello **ters CHAP parolası** hello Azure portal yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="ade96-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="ade96-193">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ade96-193">Click **OK**.</span></span>
      
       ![iSCSI Başlatıcı Karşılıklı CHAP parolası](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="ade96-195">Merhaba tıklatın **hedefleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ade96-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="ade96-196">Merhaba tıklatın **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ade96-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="ade96-197">Merhaba, **tooTarget bağlanmak** iletişim kutusu, tıklatın **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="ade96-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="ade96-198">Merhaba, **Gelişmiş Özellikler** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="ade96-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="ade96-199">Select hello **CHAP'yi etkinleştir oturum** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ade96-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="ade96-200">Merhaba, **adı** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="ade96-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="ade96-201">Merhaba, **hedef gizli** alan, hello CHAP Başlatıcı hello Klasik Portalı'nda için belirtilen kaynağı hello parola.</span><span class="sxs-lookup"><span data-stu-id="ade96-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="ade96-202">Select hello **gerçekleştirme karşılıklı kimlik doğrulaması** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ade96-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Gelişmiş ayarlar karşılıklı kimlik doğrulaması](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="ade96-204">Tıklatın **Tamam** toocomplete hello CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ade96-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="ade96-205">Merhaba Windows ana bilgisayar sunucusunda CHAP yapılandırma hakkında daha fazla bilgi için çok Git[ek hususlar](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="ade96-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="ade96-206">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="ade96-206">Additional considerations</span></span>

<span data-ttu-id="ade96-207">Merhaba **Hızlı Bağlan** özelliği etkinleştirilmiş CHAP sahip bağlantıları desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ade96-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="ade96-208">CHAP etkin olduğunda, hello kullandığınızdan emin olun **Bağlan** hello üzerinde kullanılabilir düğmesi **hedefleri** sekmesini tooconnect tooa hedef.</span><span class="sxs-lookup"><span data-stu-id="ade96-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Tootarget Bağlan](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="ade96-210">Merhaba, **tooTarget bağlanmak** sunulan, select hello iletişim kutusuna **bu sık kullanılan hedefler bağlantı toohello listesine eklemek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ade96-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="ade96-211">Bu seçim, her zaman hello bilgisayarı yeniden başlatır, girişiminde toorestore hello bağlantı toohello iSCSI sık kullanılan hedefler yapılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ade96-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="ade96-212">Yapılandırma sırasında hatalar</span><span class="sxs-lookup"><span data-stu-id="ade96-212">Errors during configuration</span></span>

<span data-ttu-id="ade96-213">CHAP yapılandırması doğru değil sonra büyük olasılıkla toosee olduğunuz bir **kimlik doğrulama hatası** hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="ade96-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="ade96-214">Doğrulama CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ade96-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="ade96-215">CHAP hello aşağıdaki adımları tamamlayarak kullanılmakta olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ade96-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="ade96-216">tooverify CHAP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ade96-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="ade96-217">Tıklatın **sık kullanılan hedefler**.</span><span class="sxs-lookup"><span data-stu-id="ade96-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="ade96-218">Kimlik doğrulamasının etkin hello hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="ade96-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="ade96-219">Tıklatın **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="ade96-219">Click **Details**.</span></span>
   
    ![iSCSI Başlatıcı özellikleri sık kullanılan hedefler](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="ade96-221">Merhaba, **sık kullanılan hedef ayrıntıları** iletişim kutusu, Not hello hello girişi **kimlik doğrulaması** alan.</span><span class="sxs-lookup"><span data-stu-id="ade96-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="ade96-222">Merhaba yapılandırma başarılı olup olmadığını, yazması gerekir **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="ade96-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Sık kullanılan hedef ayrıntıları](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="ade96-224">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ade96-224">Next steps</span></span>

* <span data-ttu-id="ade96-225">Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="ade96-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="ade96-226">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ade96-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

