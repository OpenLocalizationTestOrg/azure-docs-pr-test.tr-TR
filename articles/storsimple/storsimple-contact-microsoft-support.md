---
title: "StorSimple 8000 serisi için destek bileti oturum | Microsoft Docs"
description: "Bir destek isteği oluşturun ve StorSimple Cihazınızda destek oturum başlatma hakkında bilgi edinin."
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
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="d16f8-103">StorSimple için Microsoft Destek'e başvurun</span><span class="sxs-lookup"><span data-stu-id="d16f8-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="d16f8-104">Microsoft Azure StorSimple çözümünüzle birlikte herhangi bir sorunla karşılaşırsanız, teknik destek için bir hizmet isteği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d16f8-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="d16f8-105">Destek mühendisinize ile çevrimiçi oturumda StorSimple Cihazınızda bir destek oturumu başlatmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d16f8-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="d16f8-106">Bu makalede, izlenecek yol:</span><span class="sxs-lookup"><span data-stu-id="d16f8-106">This article walks you through:</span></span>

* <span data-ttu-id="d16f8-107">Bir destek isteği oluşturma</span><span class="sxs-lookup"><span data-stu-id="d16f8-107">How to create a support request.</span></span>
* <span data-ttu-id="d16f8-108">StorSimple Cihazınızı Windows PowerShell arabiriminde bir destek oturumu başlatmak nasıl.</span><span class="sxs-lookup"><span data-stu-id="d16f8-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="d16f8-109">Gözden geçirme [StorSimple 8000 serisi destek SLA'ları ve bilgileri](https://msdn.microsoft.com/library/mt433077.aspx) önce bir destek isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d16f8-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="d16f8-110">Destek isteği oluşturun</span><span class="sxs-lookup"><span data-stu-id="d16f8-110">Create a support request</span></span>
<span data-ttu-id="d16f8-111">Bir destek isteği oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d16f8-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="d16f8-112">Bir destek isteği oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="d16f8-112">To create a support request</span></span>
1. <span data-ttu-id="d16f8-113">İçinde [Klasik Azure portalı](https://manage.windowsazure.com/), sağ üst köşedeki hesap adınızı tıklatın ve ardından **Microsoft Destek birimine başvurun**.</span><span class="sxs-lookup"><span data-stu-id="d16f8-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![ManagementPortal üzerinden kişi MS desteği](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="d16f8-115">Yeni Azure portalına (portal.azure.com) yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d16f8-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="d16f8-116">Tıklatın **yeni destek isteği** döşeme.</span><span class="sxs-lookup"><span data-stu-id="d16f8-116">Click the **New support request** tile.</span></span>
   
    ![Yeni portal aracılığıyla kişinin MS desteği](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="d16f8-118">Ekranın sağ taraftaki **yeni destek isteği** bölmesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="d16f8-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Yeni destek isteği bölmesi](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="d16f8-120">İçinde **Temelleri** iletişim kutusunda, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d16f8-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="d16f8-121">Gelen **sorun türü** aşağı açılan listesinden, **teknik**.</span><span class="sxs-lookup"><span data-stu-id="d16f8-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="d16f8-122">Seçin bir **abonelik** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d16f8-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="d16f8-123">Gelen **hizmet** aşağı açılan listesinden, **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="d16f8-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="d16f8-124">Seçin bir **destek planı** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d16f8-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="d16f8-125">Teknik Destek etkinleştirmek için ücretli bir destek planı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="d16f8-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="d16f8-126">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d16f8-126">Click **Next**.</span></span> <span data-ttu-id="d16f8-127">**Sorun** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d16f8-127">The **Problem** dialog box appears.</span></span>
   
    ![Yeni destek isteği bölmesi](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="d16f8-129">İçinde **sorun** iletişim kutusunda, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d16f8-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="d16f8-130">Seçin bir **önem** aşağı açılan listeden düzeyi.</span><span class="sxs-lookup"><span data-stu-id="d16f8-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="d16f8-131">Seçin bir **sorun türü** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d16f8-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="d16f8-132">Seçin bir **kategori** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d16f8-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="d16f8-133">İçinde **ayrıntıları** kutusunda, sorununuzu kısaca anlatın.</span><span class="sxs-lookup"><span data-stu-id="d16f8-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="d16f8-134">İçinde **zaman çerçevesi** kutusunda, tarih, saat ve sorunu en son görüldüğü için karşılık gelen saat dilimini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d16f8-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="d16f8-135">Altında **karşıya dosya yükleme**, destek paketinizi göz atmak için klasör simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d16f8-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="d16f8-136">Seçin **tanılama bilgileri paylaşabilir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d16f8-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="d16f8-137">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d16f8-137">Click **Next**.</span></span> <span data-ttu-id="d16f8-138">**Kişi bilgileri** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d16f8-138">The **Contact information** dialog box appears.</span></span>
   
    ![Yeni destek isteği bölmesi](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="d16f8-140">İletişim bilgilerinizi girin ve bir kişi bir yöntem (telefon veya e-posta) seçin.</span><span class="sxs-lookup"><span data-stu-id="d16f8-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="d16f8-141">Seçin **Kaydet kişi değişikliklerini gelecekteki destek istekleri** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d16f8-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="d16f8-142">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d16f8-142">Click **Create**.</span></span>

<span data-ttu-id="d16f8-143">İsteğinizi gönderdikten sonra destek mühendisi, mümkün olan en kısa sürede isteğinize devam etmek için sizinle iletişim kuracaktır.</span><span class="sxs-lookup"><span data-stu-id="d16f8-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="d16f8-144">StorSimple için Windows PowerShell içinde bir destek oturumu Başlat</span><span class="sxs-lookup"><span data-stu-id="d16f8-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d16f8-145">StorSimple cihazı karşılaşabileceğiniz sorunları gidermek için Microsoft Support ekibinin sağlayacağı gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="d16f8-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="d16f8-146">Microsoft Support aygıtınıza oturum açmak için bir destek oturumu kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d16f8-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="d16f8-147">Bir destek oturumu başlatmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d16f8-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="d16f8-148">Bir destek oturumu başlatmak için</span><span class="sxs-lookup"><span data-stu-id="d16f8-148">To start a support session</span></span>
1. <span data-ttu-id="d16f8-149">Cihaz seri Konsolu kullanarak doğrudan veya uzak bir bilgisayardan telnet oturumu aracılığıyla erişin.</span><span class="sxs-lookup"><span data-stu-id="d16f8-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="d16f8-150">Bunu yapmak için adımları izleyin [kullan cihaz seri konsoluna bağlanmak için PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d16f8-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d16f8-151">Açılan oturumda basın **Enter** bir komut istemi almak için anahtar.</span><span class="sxs-lookup"><span data-stu-id="d16f8-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="d16f8-152">Seri konsol menüsünde seçeneğini 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="d16f8-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="d16f8-153">İsteminde aşağıdaki parolasını yazın:</span><span class="sxs-lookup"><span data-stu-id="d16f8-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="d16f8-154">İsteminde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d16f8-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="d16f8-155">Şifreli bir dize size sunulur.</span><span class="sxs-lookup"><span data-stu-id="d16f8-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="d16f8-156">Bu dize, Not Defteri gibi bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d16f8-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="d16f8-157">Bu dizeyi kaydedin ve Microsoft Support bir e-posta iletisi gönderin.</span><span class="sxs-lookup"><span data-stu-id="d16f8-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d16f8-158">Çalıştırarak destek erişim devre dışı bırakabilirsiniz `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="d16f8-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="d16f8-159">StorSimple cihazı da 8 saat oturumu başlatıldı sonra destek erişimini devre dışı bırakma dener.</span><span class="sxs-lookup"><span data-stu-id="d16f8-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="d16f8-160">Bir destek oturum başlatıldıktan sonra StorSimple cihaz kimlik bilgilerinizi değiştirmek için en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="d16f8-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

