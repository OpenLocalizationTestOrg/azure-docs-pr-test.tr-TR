---
title: "cep telefonları için aaaMicrosoft Authenticator uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooupgrade toohello en son sürümünü Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="a7de0-103">Merhaba Microsoft Authenticator uygulaması ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a7de0-103">Get started with hello Microsoft Authenticator app</span></span>
<span data-ttu-id="a7de0-104">Merhaba Microsoft Authenticator uygulaması bir ek düzeyi iş veya Okul hesabınızda güvenlik sunar (örneğin, bsimon@contoso.com) veya Microsoft hesabınızı (örneğin, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="a7de0-104">hello Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="a7de0-105">Merhaba uygulaması iki yoldan biriyle çalışır:</span><span class="sxs-lookup"><span data-stu-id="a7de0-105">hello app works in one of two ways:</span></span>

* <span data-ttu-id="a7de0-106">**Bildirim**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-106">**Notification**.</span></span> <span data-ttu-id="a7de0-107">Merhaba uygulama, yetkisiz erişim tooaccounts önlemek ve bildirim tooyour akıllı telefon veya tablet ileterek sahte işlemleri durdurun yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-107">hello app can help prevent unauthorized access tooaccounts and stop fraudulent transactions by pushing a notification tooyour smartphone or tablet.</span></span> <span data-ttu-id="a7de0-108">Yalnızca hello bildirim görüntüleyin ve işlem meşru ise seçin **doğrula**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-108">Simply view hello notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="a7de0-109">Aksi takdirde, seçebileceğiniz **reddetme**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="a7de0-110">**Doğrulama kodu**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-110">**Verification code**.</span></span> <span data-ttu-id="a7de0-111">Merhaba uygulaması bir OAuth doğrulama kodu toogenerate bir yazılım belirteci olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-111">hello app can be used as a software token toogenerate an OAuth verification code.</span></span> <span data-ttu-id="a7de0-112">Kullanıcı adınızı ve parolanızı girdikten sonra oturum açma hello ekranına hello uygulama tarafından sağlanan hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="a7de0-112">After you enter your username and password, you enter hello code provided by hello app into hello sign-in screen.</span></span> <span data-ttu-id="a7de0-113">Merhaba doğrulama kodu ikinci bir form kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7de0-113">hello verification code provides a second form of authentication.</span></span>

<span data-ttu-id="a7de0-114">Merhaba Microsoft Authenticator uygulaması hello Azure Authenticator uygulamasını yerini alır.</span><span class="sxs-lookup"><span data-stu-id="a7de0-114">hello Microsoft Authenticator app replaces hello Azure Authenticator app.</span></span> <span data-ttu-id="a7de0-115">Hello Azure Authenticator uygulamasını hala çalışıyor, ancak toomove toohello yeni Microsoft Authenticator uygulaması karar verirseniz, bu makale size yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-115">hello Azure Authenticator app still works, but if you decide toomove toohello new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="a7de0-116">İki aşamalı doğrulama için kabul</span><span class="sxs-lookup"><span data-stu-id="a7de0-116">Opt in for two-step verification</span></span>

<span data-ttu-id="a7de0-117">Merhaba Microsoft Authenticator uygulamasını kendi başına çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="a7de0-117">hello Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="a7de0-118">Her kullanıcı adı ve parola ile oturum çalıştırdıktan sonra ikinci bir doğrulama yöntemi için hesapları tooprompt yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a7de0-118">Configure each of your accounts tooprompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="a7de0-119">Bir iş veya Okul hesabı için genellikle toochoose bu özellik kendiniz elde etmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7de0-119">For a work or school account, you don't usually get toochoose this feature for yourself.</span></span> <span data-ttu-id="a7de0-120">Bunun yerine, bir güvenlik yöneticisi sizin adınıza kabul eder ve bunu tooregister doğrulama yöntemlerini hesabınız için size bildirir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-120">Instead, a security administrator opts in on your behalf and then notifies you tooregister verification methods for your account.</span></span> <span data-ttu-id="a7de0-121">Bu senaryo tooyou geçerliyse, daha fazla bilgi edinin [ne Azure çok faktörlü kimlik doğrulaması için beni anlamına gelmez](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="a7de0-121">If this scenario applies tooyou, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="a7de0-122">Kişisel bir hesap için kendiniz için iki aşamalı doğrulamayı yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-122">For a personal account, you need tooset up two-step verification for yourself.</span></span> <span data-ttu-id="a7de0-123">Bir Microsoft hesabınız varsa, bu adımları kullanılabilir olan [iki basamaklı doğrulama hakkında](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="a7de0-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="a7de0-124">Microsoft olmayan hesapların ile Merhaba Microsoft Authenticator de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7de0-124">You can also use hello Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="a7de0-125">Bunlar hello özelliği iki aşamalı doğrulama dışında bir şey çağırabilir ancak mümkün toofind olması gereken güvenlik veya oturum açma ayarları altında.</span><span class="sxs-lookup"><span data-stu-id="a7de0-125">They may call hello feature something other than two-step verification, but you should be able toofind it under security or sign-in settings.</span></span> 

## <a name="install-hello-app"></a><span data-ttu-id="a7de0-126">Merhaba uygulamasını yükleyin</span><span class="sxs-lookup"><span data-stu-id="a7de0-126">Install hello app</span></span>
<span data-ttu-id="a7de0-127">Merhaba Microsoft Authenticator uygulaması için kullanılabilir [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), ve [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="a7de0-127">hello Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-toohello-app"></a><span data-ttu-id="a7de0-128">Hesapları toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="a7de0-128">Add accounts toohello app</span></span>
<span data-ttu-id="a7de0-129">Tooadd toohello Microsoft Authenticator uygulamasını istediğiniz her hesap için aşağıdaki yordamlarını hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7de0-129">For each account that you want tooadd toohello Microsoft Authenticator app, use one of hello following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-toohello-app"></a><span data-ttu-id="a7de0-130">Kişisel bir Microsoft hesabı toohello uygulamasını ekleme</span><span class="sxs-lookup"><span data-stu-id="a7de0-130">Add a personal Microsoft account toohello app</span></span>

<span data-ttu-id="a7de0-131">Kişisel bir Microsoft hesabı (bir toosign kullanmak tooOutlook.com içinde Xbox, Skype, vb.), tüm toodo sahip olduğu hello Microsoft Authenticator uygulaması tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a7de0-131">For a personal Microsoft account (one that you use toosign in tooOutlook.com, Xbox, Skype, etc.), all you have toodo is sign in tooyour account in hello Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a><span data-ttu-id="a7de0-132">Bir iş veya Okul hesabı toohello uygulamasını hello QR kodu tarayıcı kullanarak</span><span class="sxs-lookup"><span data-stu-id="a7de0-132">Add a work or school account toohello app using hello QR code scanner</span></span>
1. <span data-ttu-id="a7de0-133">Toohello güvenlik doğrulama ayarları ekranına gidin.</span><span class="sxs-lookup"><span data-stu-id="a7de0-133">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="a7de0-134">Hakkında bilgi için tooget toothis ekran bkz [güvenlik ayarlarınızı değiştirme](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="a7de0-134">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="a7de0-135">Merhaba sonraki çok onay kutusunu**Doğrulayıcı uygulama** seçip **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-135">Check hello box next too**Authenticator app** then select **Configure**.</span></span>

    ![Merhaba Yapılandır düğmesine hello güvenlik doğrulama ayarları ekranı](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="a7de0-137">Bu bir QR kodu içeren bir ekrana getirir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-137">This brings up a screen with a QR code on it.</span></span>

    ![Merhaba QR kodu sağlar ekranı](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="a7de0-139">Açık hello Microsoft Authenticator uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a7de0-139">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="a7de0-140">Merhaba üzerinde **hesapları** ekran, select  **+** ve ardından iş veya Okul hesabı tooadd istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="a7de0-140">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>
4. <span data-ttu-id="a7de0-141">Merhaba kamera tooscan hello QR kodu kullanın ve ardından **Bitti** tooclose hello QR kodu ekran.</span><span class="sxs-lookup"><span data-stu-id="a7de0-141">Use hello camera tooscan hello QR code, and then select **Done** tooclose hello QR code screen.</span></span>

    <span data-ttu-id="a7de0-142">Kameranızı düzgün çalışmıyorsa, yapabilecekleriniz [hello QR kodu ve URL'yi elle girin](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="a7de0-142">If your camera is not working properly, you can [enter hello QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="a7de0-143">Hello uygulama hesap adınızı ile bunun altındaki altı rakamlı bir kod gösterdiğinde bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="a7de0-143">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Hesapları ekranı](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a><span data-ttu-id="a7de0-145">Bir hesabı toohello uygulamasını el ile Ekle</span><span class="sxs-lookup"><span data-stu-id="a7de0-145">Add an account toohello app manually</span></span>
1. <span data-ttu-id="a7de0-146">Toohello güvenlik doğrulama ayarları ekranına gidin.</span><span class="sxs-lookup"><span data-stu-id="a7de0-146">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="a7de0-147">Hakkında bilgi için tooget toothis ekran bkz [güvenlik ayarlarınızı değiştirme](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a7de0-147">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="a7de0-148">Seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-148">Select **Configure**.</span></span>

    ![Merhaba Yapılandır düğmesine hello güvenlik doğrulama ayarları ekranı](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="a7de0-150">Bu bir QR kodu içeren bir ekrana getirir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="a7de0-151">Merhaba kodu ve URL unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7de0-151">Note hello code and URL.</span></span>

    ![Merhaba QR kodu ve URL sağlayan ekran](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="a7de0-153">Açık hello Microsoft Authenticator uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a7de0-153">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="a7de0-154">Merhaba üzerinde **hesapları** ekran, select  **+** ve ardından iş veya Okul hesabı tooadd istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="a7de0-154">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>

4. <span data-ttu-id="a7de0-155">Merhaba tarayıcıda seçin **kodu el ile girmeniz**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-155">In hello scanner, select **enter code manually**.</span></span>

    ![QR kodu taraması için ekran](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="a7de0-157">Hello uygulama uygun kutulara hello Hello kodu ve hello URL'yi girin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-157">Enter hello code and hello URL in hello appropriate boxes in hello app, then select **Finish**.</span></span>

    ![Kod ve URL girme ekran](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="a7de0-159">Hello uygulama hesap adınızı ile bunun altındaki altı rakamlı bir kod gösterdiğinde bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="a7de0-159">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Hesapları ekranı](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a><span data-ttu-id="a7de0-161">Touch ID kullanarak bir hesap toohello uygulama ekleyin</span><span class="sxs-lookup"><span data-stu-id="a7de0-161">Add an account toohello app using Touch ID</span></span>
<span data-ttu-id="a7de0-162">Touch ID ios'ta Hello Microsoft Authenticator uygulaması destekler</span><span class="sxs-lookup"><span data-stu-id="a7de0-162">hello Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="a7de0-163">Azure çok faktörlü kimlik doğrulaması kuruluşlar toorequire cihazlar için bir PIN verir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-163">Azure Multi-Factor Authentication allows organizations toorequire a PIN for devices.</span></span> <span data-ttu-id="a7de0-164">Touch ID ile iOS kullanıcıları tooenter bir PIN gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="a7de0-164">With Touch ID, iOS users don’t need tooenter a PIN.</span></span> <span data-ttu-id="a7de0-165">Bunun yerine, bunlar parmak izini tarayabilir ve seçin **Onayla**.</span><span class="sxs-lookup"><span data-stu-id="a7de0-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="a7de0-166">Touch ID Microsoft Authenticator ile ayarlama basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="a7de0-167">Bir PIN ile normal doğrulama sınamasını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="a7de0-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="a7de0-168">Cihazınızı Touch ID destekliyorsa, Microsoft Authenticator onu otomatik olarak o hesap için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a7de0-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Touch ID kurulumunun doğrulama](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="a7de0-170">Noktasındaki İleri, bunu olduğunuzda, oturum açma, tooverify gerekli alınan hello anında iletme bildirimini seçin ve PIN'İNİZİ girmek yerine parmak izinizi tarama.</span><span class="sxs-lookup"><span data-stu-id="a7de0-170">From that point forward, when you're required tooverify your sign-in, you select hello received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Anında iletme bildirimi](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a><span data-ttu-id="a7de0-172">Oturum açtığınızda hello uygulama kullanma</span><span class="sxs-lookup"><span data-stu-id="a7de0-172">Use hello app when you sign in</span></span>

<span data-ttu-id="a7de0-173">Hesabınızı toohello uygulama eklendikten sonra istendiğinde toodo test doğrulama toomake her şeyin doğru şekilde yapılandırıldığından emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7de0-173">Once your account is added toohello app, you may be prompted toodo a test verification toomake sure everything was configured correctly.</span></span> <span data-ttu-id="a7de0-174">Bundan sonra tamamladınız!</span><span class="sxs-lookup"><span data-stu-id="a7de0-174">After that, you're done!</span></span> <span data-ttu-id="a7de0-175">Merhaba sonraki sefer oturum açtığınızda kadar toodo başka bir şey gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a7de0-175">You don't need toodo anything else until hello next time you sign in.</span></span>

<span data-ttu-id="a7de0-176">Merhaba uygulamada doğrulama kodları toouse seçerseniz, toosee Başlat hello giriş sayfasında bunları.</span><span class="sxs-lookup"><span data-stu-id="a7de0-176">If you chose toouse verification codes in hello app, you start toosee them on hello home page.</span></span> <span data-ttu-id="a7de0-177">Bir gereksinim duyduğunuzda, böylece her zaman yeni bir kod sahip oldukları her 30 saniyede değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a7de0-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="a7de0-178">Ancak oturum açın ve bir doğrulama kodu istendiğinde tooenter olduğu kadar toodo onlarla herhangi bir şey gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a7de0-178">But you don't need toodo anything with them until you sign in and are prompted tooenter a verification code.</span></span>  
