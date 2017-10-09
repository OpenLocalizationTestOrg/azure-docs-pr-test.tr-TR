---
title: "aaaCreate destek bileti veya servis talebi için StorSimple 8000 serisi | Microsoft Docs"
description: "Nasıl toolog destek isteği bilgi edinin ve StorSimple 8000 serisi aygıtınızda bir destek oturumu başlatın."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 832e3ac739dafa6dd8c24aaea38aef9c6f1b27b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="d780f-103">Microsoft Destek'e Başvur</span><span class="sxs-lookup"><span data-stu-id="d780f-103">Contact Microsoft Support</span></span>

<span data-ttu-id="d780f-104">Merhaba StorSimple Aygıt Yöneticisi'ni sağlar hello yetenek çok**yeni bir destek isteği oturum** hello hizmet Özet dikey.</span><span class="sxs-lookup"><span data-stu-id="d780f-104">hello StorSimple Device Manager provides hello capability too**log a new support request** within hello service summary blade.</span></span> <span data-ttu-id="d780f-105">StorSimple çözümünüzle birlikte herhangi bir sorunla karşılaşırsanız, teknik destek için bir hizmet isteği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d780f-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="d780f-106">Destek mühendisinize ile çevrimiçi oturumda destek oturumu toostart StorSimple Cihazınızda gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d780f-106">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="d780f-107">Bu makalede, izlenecek yol:</span><span class="sxs-lookup"><span data-stu-id="d780f-107">This article walks you through:</span></span>

* <span data-ttu-id="d780f-108">Nasıl toocreate bir destek isteği.</span><span class="sxs-lookup"><span data-stu-id="d780f-108">How toocreate a support request.</span></span>
* <span data-ttu-id="d780f-109">Nasıl toomanage destek yaşam döngüsü hello portalındaki isteyin.</span><span class="sxs-lookup"><span data-stu-id="d780f-109">How toomanage a support request lifecycle from within hello portal.</span></span>
* <span data-ttu-id="d780f-110">Nasıl toostart destek oturumunda bir Windows PowerShell arabirimi StorSimple cihazınızın hello.</span><span class="sxs-lookup"><span data-stu-id="d780f-110">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="d780f-111">Gözden geçirme hello [StorSimple 8000 serisi destek SLA'ları ve bilgileri](https://msdn.microsoft.com/library/mt433077.aspx) önce bir destek isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d780f-111">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="d780f-112">Destek isteği oluşturun</span><span class="sxs-lookup"><span data-stu-id="d780f-112">Create a support request</span></span>

<span data-ttu-id="d780f-113">Bağlı olarak, [destek planı](https://azure.microsoft.com/support/plans/), doğrudan hello StorSimple cihaz Yöneticisi hizmeti Özet dikey penceresinden, StorSimple Cihazınızda bir sorun destek bileti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d780f-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from hello StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="d780f-114">Aşağıdaki adımları toocreate bir destek isteği hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d780f-114">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="d780f-115">toocreate bir destek isteği</span><span class="sxs-lookup"><span data-stu-id="d780f-115">toocreate a support request</span></span>

1. <span data-ttu-id="d780f-116">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="d780f-116">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="d780f-117">Merhaba hizmet Özet dikey ayarlarında çok Git**destek + sorun giderme** bölümünde ve ardından **yeni destek isteği**.</span><span class="sxs-lookup"><span data-stu-id="d780f-117">In hello service summary blade settings, go too**SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![Yeni portal aracılığıyla kişinin MS desteği](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="d780f-119">Merhaba, **yeni destek isteği** dikey penceresinde, select **Temelleri**.</span><span class="sxs-lookup"><span data-stu-id="d780f-119">In hello **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="d780f-120">Merhaba, **Temelleri** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="d780f-120">In hello **Basics** blade, do hello following steps:</span></span>
   1. <span data-ttu-id="d780f-121">Merhaba gelen **sorun türü** aşağı açılan listesinden, **teknik**.</span><span class="sxs-lookup"><span data-stu-id="d780f-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="d780f-122">Merhaba geçerli **abonelik**, **hizmet** türü ve hello **kaynak** (StorSimple cihaz Yöneticisi hizmeti) otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="d780f-122">hello current **Subscription**, **Service** type, and hello **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="d780f-123">Seçin bir **destek planı** aboneliğinizle ilişkili birden çok planları varsa hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d780f-123">Select a **Support plan** from hello drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="d780f-124">Bir Ücretli destek planı tooenable teknik destek gerekir.</span><span class="sxs-lookup"><span data-stu-id="d780f-124">You need a paid support plan tooenable Technical Support.</span></span>
   4. <span data-ttu-id="d780f-125">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d780f-125">Click **Next**.</span></span>

       ![Yeni portal aracılığıyla kişinin MS desteği](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="d780f-127">Merhaba, **yeni destek isteği** dikey penceresinde, select **adım 2 sorun**.</span><span class="sxs-lookup"><span data-stu-id="d780f-127">In hello **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="d780f-128">Merhaba, **sorun** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="d780f-128">In hello **Problem** blade, do hello following steps:</span></span>
    
    1. <span data-ttu-id="d780f-129">Merhaba seçin **önem**.</span><span class="sxs-lookup"><span data-stu-id="d780f-129">Choose hello **Severity**.</span></span>
    2. <span data-ttu-id="d780f-130">Merhaba sorunu ilgili toohello gereç ya da hello StorSimple cihaz Yöneticisi hizmeti olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d780f-130">Specify if hello issue is related toohello appliance or hello StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="d780f-131">Seçin bir **kategori** bu vermek ve daha fazlasını sağlamak **ayrıntıları** hello sorun hakkında.</span><span class="sxs-lookup"><span data-stu-id="d780f-131">Choose a **Category** for this issue and provide more **Details** about hello issue.</span></span>
    4. <span data-ttu-id="d780f-132">Merhaba başlangıç tarihini ve saatini hello soruna yönelik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d780f-132">Provide hello start date and time for hello problem.</span></span>
    5. <span data-ttu-id="d780f-133">Merhaba, **karşıya dosya yükleme**, hello klasör simgesine toobrowse tooyour destek paketi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d780f-133">In hello **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
    6. <span data-ttu-id="d780f-134">Denetleme **tanılama bilgileri paylaşabilir**.</span><span class="sxs-lookup"><span data-stu-id="d780f-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="d780f-135">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d780f-135">Click **Next**.</span></span>

       ![Yeni portal aracılığıyla kişinin MS desteği](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="d780f-137">Merhaba, **yeni destek isteği** dikey penceresinde tıklatın **adım 3 irtibat bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="d780f-137">In hello **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="d780f-138">Merhaba, **kişi bilgileri** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="d780f-138">In hello **Contact information** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="d780f-139">Merhaba, **başvurun seçenekleri**, tercih edilen iletişim yönteminiz (telefon veya e-posta) sağlamak ve hello dili.</span><span class="sxs-lookup"><span data-stu-id="d780f-139">In hello **Contact options**, provide your preferred contact method (phone or email) and hello language.</span></span> <span data-ttu-id="d780f-140">Merhaba yanıt süresi, abonelik plana göre otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="d780f-140">hello response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="d780f-141">Adı, e-posta, isteğe bağlı kişi, ülke Hello kişi bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d780f-141">In hello Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="d780f-142">Select hello **Kaydet kişi değişikliklerini gelecekteki destek istekleri** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d780f-142">Select hello **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="d780f-143">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d780f-143">Click **Create**.</span></span>
   
        ![Yeni portal aracılığıyla kişinin MS desteği](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="d780f-145">Microsoft Support bu bilgileri tooreach tooyou çıkışı daha fazla bilgi, tanılama ve çözümleme için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d780f-145">Microsoft Support will use this information tooreach out tooyou for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="d780f-146">Bir destek mühendisine isteğinizi gönderdikten sonra tooproceed isteğiniz ile mümkün olan en kısa sürede başvururlar.</span><span class="sxs-lookup"><span data-stu-id="d780f-146">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="d780f-147">Bir destek isteği yönetme</span><span class="sxs-lookup"><span data-stu-id="d780f-147">Manage a support request</span></span>

<span data-ttu-id="d780f-148">Bir destek bileti oluşturduktan sonra hello üzerinden bu biletin hello portal hello yaşam döngüsü yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d780f-148">After creating a support ticket, you can manage hello lifecycle of hello ticket from within hello portal.</span></span>

#### <a name="toomanage-your-support-requests"></a><span data-ttu-id="d780f-149">toomanage destek istekleri</span><span class="sxs-lookup"><span data-stu-id="d780f-149">toomanage your support requests</span></span>

1. <span data-ttu-id="d780f-150">tooget toohello Yardım ve Destek sayfası, çok gidin**Gözat > Yardım + Destek**.</span><span class="sxs-lookup"><span data-stu-id="d780f-150">tooget toohello help and support page, navigate too**Browse > Help + support**.</span></span>

    ![Destek isteklerini yönet](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="d780f-152">Tablo listesini tüm hello destek istekleri hello görüntülenir **Yardım + Destek** dikey.</span><span class="sxs-lookup"><span data-stu-id="d780f-152">A tabular listing of All hello support requests is displayed in hello **Help + support** blade.</span></span>

    ![Destek isteklerini yönet](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="d780f-154">Seçin ve bir destek isteği'ni tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d780f-154">Select and click a support request.</span></span> <span data-ttu-id="d780f-155">Merhaba durumu ve bu istek için hello ayrıntıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d780f-155">You can view hello status and hello details for this request.</span></span> <span data-ttu-id="d780f-156">Tıklatın **+ yeni ileti** toofollow yukarı bu istekte istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d780f-156">Click **+ New message** if you want toofollow up on this request.</span></span>

    ![Destek isteklerini yönet](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="d780f-158">StorSimple için Windows PowerShell içinde bir destek oturumu Başlat</span><span class="sxs-lookup"><span data-stu-id="d780f-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="d780f-159">tüm sorunları, tootroubleshoot hello StorSimple cihazı ile karşılaşabilirsiniz, hello Microsoft Support ekibi ile tooengage gerekir.</span><span class="sxs-lookup"><span data-stu-id="d780f-159">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="d780f-160">Microsoft Support toouse destek oturum toolog tooyour aygıtta gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d780f-160">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span>

<span data-ttu-id="d780f-161">Hello aşağıdaki gerçekleştirme adımları toostart destek oturumu:</span><span class="sxs-lookup"><span data-stu-id="d780f-161">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="d780f-162">bir destek oturumu toostart</span><span class="sxs-lookup"><span data-stu-id="d780f-162">toostart a support session</span></span>

1. <span data-ttu-id="d780f-163">Erişim hello aygıtı hello seri Konsolu kullanarak doğrudan veya uzak bir bilgisayardan telnet oturumu aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="d780f-163">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="d780f-164">toodo Bu, başlangıç adımları içinde [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d780f-164">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d780f-165">Merhaba açar hello oturumunda basın **Enter** anahtar tooget bir komut istemi.</span><span class="sxs-lookup"><span data-stu-id="d780f-165">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="d780f-166">Merhaba seri konsol menüsünde seçeneğini 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="d780f-166">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="d780f-167">Merhaba isteminde parola aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="d780f-167">At hello prompt, type hello following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="d780f-168">Merhaba isteminde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d780f-168">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="d780f-169">Şifreli bir dize tooyou sunulur.</span><span class="sxs-lookup"><span data-stu-id="d780f-169">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="d780f-170">Bu dize, Not Defteri gibi bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d780f-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="d780f-171">Bu dizeyi kaydedin ve bir e-posta iletisi tooMicrosoft destek gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d780f-171">Save this string and send it in an email message tooMicrosoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d780f-172">Çalıştırarak destek erişim devre dışı bırakabilirsiniz `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="d780f-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="d780f-173">Hello StorSimple cihazı 8 saat hello oturumu başlatıldı sonra toodisable destek erişim girişiminde.</span><span class="sxs-lookup"><span data-stu-id="d780f-173">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="d780f-174">Bir destek oturum başlatıldıktan sonra StorSimple Cihazınızı kimlik iyi bir yöntem toochange olur.</span><span class="sxs-lookup"><span data-stu-id="d780f-174">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d780f-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d780f-175">Next steps</span></span>

<span data-ttu-id="d780f-176">Nasıl çok öğrenin[tanılamada ve sorunları ilgili tooyour StorSimple 8000 serisi cihaz](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="d780f-176">Learn how too[diagnose and solve problems related tooyour StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
