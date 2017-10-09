---
title: "aaaLog StorSimple 8000 serisi için destek bileti | Microsoft Docs"
description: "Nasıl toocreate bir destek isteği öğrenin ve StorSimple Cihazınızda bir destek oturumu başlatın."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="d8512-103">StorSimple için Microsoft Destek'e başvurun</span><span class="sxs-lookup"><span data-stu-id="d8512-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="d8512-104">Microsoft Azure StorSimple çözümünüzle birlikte herhangi bir sorunla karşılaşırsanız, teknik destek için bir hizmet isteği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8512-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="d8512-105">Destek mühendisinize ile çevrimiçi oturumda destek oturumu toostart StorSimple Cihazınızda gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d8512-105">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="d8512-106">Bu makalede, izlenecek yol:</span><span class="sxs-lookup"><span data-stu-id="d8512-106">This article walks you through:</span></span>

* <span data-ttu-id="d8512-107">Nasıl toocreate bir destek isteği.</span><span class="sxs-lookup"><span data-stu-id="d8512-107">How toocreate a support request.</span></span>
* <span data-ttu-id="d8512-108">Nasıl toostart destek oturumunda bir Windows PowerShell arabirimi StorSimple cihazınızın hello.</span><span class="sxs-lookup"><span data-stu-id="d8512-108">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="d8512-109">Gözden geçirme hello [StorSimple 8000 serisi destek SLA'ları ve bilgileri](https://msdn.microsoft.com/library/mt433077.aspx) önce bir destek isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d8512-109">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="d8512-110">Destek isteği oluşturun</span><span class="sxs-lookup"><span data-stu-id="d8512-110">Create a support request</span></span>
<span data-ttu-id="d8512-111">Aşağıdaki adımları toocreate bir destek isteği hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8512-111">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="d8512-112">toocreate bir destek isteği</span><span class="sxs-lookup"><span data-stu-id="d8512-112">toocreate a support request</span></span>
1. <span data-ttu-id="d8512-113">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), hello sağ üst köşedeki, hesap adınızı tıklatın ve ardından **Microsoft Destek birimine başvurun**.</span><span class="sxs-lookup"><span data-stu-id="d8512-113">In hello [Azure classic portal](https://manage.windowsazure.com/), in hello upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![ManagementPortal üzerinden kişi MS desteği](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="d8512-115">Yeniden yönlendirilen toohello yeni Azure portalına (portal.azure.com) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d8512-115">You will be redirected toohello new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="d8512-116">Merhaba tıklatın **yeni destek isteği** döşeme.</span><span class="sxs-lookup"><span data-stu-id="d8512-116">Click hello **New support request** tile.</span></span>
   
    ![Yeni portal aracılığıyla kişinin MS desteği](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="d8512-118">Merhaba sağ tarafında Merhaba ekranında, hello **yeni destek isteği** bölmesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="d8512-118">On hello right side of hello screen, hello **New support request** pane appears.</span></span> 
   
    ![Yeni destek isteği bölmesi](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="d8512-120">Merhaba, **Temelleri** iletişim kutusunda, aşağıdaki tam hello:</span><span class="sxs-lookup"><span data-stu-id="d8512-120">In hello **Basics** dialog box, complete hello following:</span></span>                                
   
   1. <span data-ttu-id="d8512-121">Merhaba gelen **sorun türü** aşağı açılan listesinden, **teknik**.</span><span class="sxs-lookup"><span data-stu-id="d8512-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="d8512-122">Seçin bir **abonelik** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d8512-122">Select a **Subscription** from hello drop-down list.</span></span>
   3. <span data-ttu-id="d8512-123">Merhaba gelen **hizmet** aşağı açılan listesinden, **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="d8512-123">From hello **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="d8512-124">Seçin bir **destek planı** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d8512-124">Select a **Support plan** from hello drop-down list.</span></span> <span data-ttu-id="d8512-125">Bir Ücretli destek planı tooenable teknik destek gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8512-125">You need a paid support plan tooenable Technical Support.</span></span>
4. <span data-ttu-id="d8512-126">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8512-126">Click **Next**.</span></span> <span data-ttu-id="d8512-127">Merhaba **sorun** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d8512-127">hello **Problem** dialog box appears.</span></span>
   
    ![Yeni destek isteği bölmesi](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="d8512-129">Merhaba, **sorun** iletişim kutusunda, aşağıdaki tam hello:</span><span class="sxs-lookup"><span data-stu-id="d8512-129">In hello **Problem** dialog box, complete hello following:</span></span>
   
   1. <span data-ttu-id="d8512-130">Seçin bir **önem** hello aşağı açılan listeden düzeyi.</span><span class="sxs-lookup"><span data-stu-id="d8512-130">Select a **Severity** level from hello drop-down list.</span></span>
   2. <span data-ttu-id="d8512-131">Seçin bir **sorun türü** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d8512-131">Select a **Problem type** from hello drop-down list.</span></span>
   3. <span data-ttu-id="d8512-132">Seçin bir **kategori** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d8512-132">Select a **Category** from hello drop-down list.</span></span> 
   4. <span data-ttu-id="d8512-133">Merhaba, **ayrıntıları** kutusunda, sorununuzu kısaca anlatın.</span><span class="sxs-lookup"><span data-stu-id="d8512-133">In hello **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="d8512-134">Merhaba, **zaman çerçevesi** kutusunda, hello tarih, saat ve sorununuzun en son görüldüğü toohello karşılık gelen saat dilimini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d8512-134">In hello **Time frame** box, indicate hello date, time, and time zone that corresponds toohello most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="d8512-135">Altında **karşıya dosya yükleme**, hello klasör simgesine toobrowse tooyour destek paketi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8512-135">Under **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
   7. <span data-ttu-id="d8512-136">Select hello **tanılama bilgileri paylaşabilir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d8512-136">Select hello **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="d8512-137">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8512-137">Click **Next**.</span></span> <span data-ttu-id="d8512-138">Merhaba **kişi bilgileri** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d8512-138">hello **Contact information** dialog box appears.</span></span>
   
    ![Yeni destek isteği bölmesi](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="d8512-140">İletişim bilgilerinizi girin ve bir kişi bir yöntem (telefon veya e-posta) seçin.</span><span class="sxs-lookup"><span data-stu-id="d8512-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="d8512-141">Select hello **Kaydet kişi değişikliklerini gelecekteki destek istekleri** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d8512-141">Select hello **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="d8512-142">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8512-142">Click **Create**.</span></span>

<span data-ttu-id="d8512-143">Bir destek mühendisine isteğinizi gönderdikten sonra tooproceed isteğiniz ile mümkün olan en kısa sürede başvururlar.</span><span class="sxs-lookup"><span data-stu-id="d8512-143">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="d8512-144">StorSimple için Windows PowerShell içinde bir destek oturumu Başlat</span><span class="sxs-lookup"><span data-stu-id="d8512-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d8512-145">tüm sorunları, tootroubleshoot hello StorSimple cihazı ile karşılaşabilirsiniz, hello Microsoft Support ekibi ile tooengage gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8512-145">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="d8512-146">Microsoft Support toouse destek oturum toolog tooyour aygıtta gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d8512-146">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span> 

<span data-ttu-id="d8512-147">Hello aşağıdaki gerçekleştirme adımları toostart destek oturumu:</span><span class="sxs-lookup"><span data-stu-id="d8512-147">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="d8512-148">bir destek oturumu toostart</span><span class="sxs-lookup"><span data-stu-id="d8512-148">toostart a support session</span></span>
1. <span data-ttu-id="d8512-149">Erişim hello aygıtı hello seri Konsolu kullanarak doğrudan veya uzak bir bilgisayardan telnet oturumu aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="d8512-149">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="d8512-150">toodo Bu, başlangıç adımları içinde [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d8512-150">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d8512-151">Merhaba açar hello oturumunda basın **Enter** anahtar tooget bir komut istemi.</span><span class="sxs-lookup"><span data-stu-id="d8512-151">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="d8512-152">Merhaba seri konsol menüsünde seçeneğini 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="d8512-152">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="d8512-153">Merhaba isteminde parola aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="d8512-153">At hello prompt, type hello following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="d8512-154">Merhaba isteminde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d8512-154">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="d8512-155">Şifreli bir dize tooyou sunulur.</span><span class="sxs-lookup"><span data-stu-id="d8512-155">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="d8512-156">Bu dize, Not Defteri gibi bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d8512-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="d8512-157">Bu dizeyi kaydedin ve bir e-posta iletisi tooMicrosoft destek gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8512-157">Save this string and send it in an email message tooMicrosoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d8512-158">Çalıştırarak destek erişim devre dışı bırakabilirsiniz `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="d8512-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="d8512-159">Hello StorSimple cihazı 8 saat hello oturumu başlatıldı sonra toodisable destek erişim girişiminde.</span><span class="sxs-lookup"><span data-stu-id="d8512-159">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="d8512-160">Bir destek oturum başlatıldıktan sonra StorSimple Cihazınızı kimlik iyi bir yöntem toochange olur.</span><span class="sxs-lookup"><span data-stu-id="d8512-160">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

