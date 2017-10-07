---
title: "aaaHow toouse Azure MFA uygulama parolaları? | Microsoft Belgeleri"
description: "Bu sayfayı kullanıcıların uygulama parolaları nedir ve ne olduklarını anlamasına yardımcı olacak şekilde tooAzure MFA ile kullanılır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="036c6-104">Azure çok faktörlü kimlik doğrulaması'ndaki uygulama parolaları nedir?</span><span class="sxs-lookup"><span data-stu-id="036c6-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="036c6-105">Exchange Active Sync kullanan hello Apple yerel e-posta istemcisi gibi belirli bir tarayıcı olmayan uygulamaları, şu anda çok faktörlü kimlik doğrulamasını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="036c6-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="036c6-106">Çok faktörlü kimlik doğrulaması kullanıcı başına etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="036c6-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="036c6-107">Başka bir deyişle, bir kullanıcı, çok faktörlü kimlik doğrulamasını kullanamaz:</span><span class="sxs-lookup"><span data-stu-id="036c6-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="036c6-108">Merhaba kullanıcı çok faktörlü kimlik doğrulaması için etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="036c6-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="036c6-109">Merhaba kullanıcı toouse bir tarayıcı olmayan uygulaması çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="036c6-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="036c6-110">Bir uygulama parolası hello kullanıcı toouse hello uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="036c6-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="036c6-111">Bir uygulama parolası sahip olduktan sonra özgün parolanızı bu tarayıcı olmayan uygulamaları ile yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="036c6-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="036c6-112">İki aşamalı doğrulama için kaydolduğunuzda, hello ikinci doğrulama de gerçekleştirilemiyor, Microsoft olmayan herhangi bir kişi oturum toolet parolanızla oturum söyleyen.</span><span class="sxs-lookup"><span data-stu-id="036c6-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="036c6-113">iki aşamalı doğrulama için istenemez olduğundan telefonunuzda hello Apple yerel e-posta istemcisi olarak oturum açamaz.</span><span class="sxs-lookup"><span data-stu-id="036c6-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="036c6-114">Merhaba çözüm toothis toocreate kullanmadığınız daha güvenli bir uygulama parolası sorunudur günlük.</span><span class="sxs-lookup"><span data-stu-id="036c6-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="036c6-115">Uygulama parolaları, iki aşamalı doğrulamayı destekleyemez yalnızca bu uygulamalar içindir.</span><span class="sxs-lookup"><span data-stu-id="036c6-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="036c6-116">Uygulamalar çok faktörlü kimlik doğrulamasını atlamak ve toowork devam hello uygulama parolasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="036c6-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="036c6-117">Office 2013 istemcileri (Outlook dahil) destekleyen yeni kimlik doğrulama protokolleri ve iki aşamalı doğrulamayla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="036c6-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="036c6-118">Uygulama parolaları Office 2013 istemcilerle kullanım için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="036c6-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="036c6-119">Daha fazla bilgi için bkz: [Office 2013 modern kimlik doğrulaması genel önizlemesi Duyuruldu](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="036c6-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="036c6-120">Nasıl toouse uygulama parolaları</span><span class="sxs-lookup"><span data-stu-id="036c6-120">How toouse app passwords</span></span>
<span data-ttu-id="036c6-121">Uygulama parolaları hakkında bazı şeyleri tooknow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="036c6-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="036c6-122">Kendi uygulama parolaları oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="036c6-122">You don't create your own app passwords.</span></span> <span data-ttu-id="036c6-123">Bunlar otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="036c6-123">They are automatically generated.</span></span>
* <span data-ttu-id="036c6-124">Şu anda kullanıcı başına 40 parolalık bir sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="036c6-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="036c6-125">Merhaba sınırına ulaştınız sonra toocreate bir uygulama parolası çalışırsanız, yeni bir tane oluşturmadan önce toodelete varolan uygulama parolalarınızdan birini sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="036c6-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="036c6-126">Bir uygulama parolası aygıt başına, uygulama başına değil kullanın.</span><span class="sxs-lookup"><span data-stu-id="036c6-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="036c6-127">Örneğin, dizüstü bilgisayarınız için bir uygulama parolası oluşturmanız ve tüm Dizüstü bilgisayarınızdaki uygulamalar için bu uygulama parolasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="036c6-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="036c6-128">Ardından, tüm uygulamalarınız için ikinci bir uygulama parolası toouse masaüstünüzde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="036c6-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="036c6-129">Kaydettiğiniz ilk kez iki aşamalı doğrulama için bir uygulama parolası hello verilir.</span><span class="sxs-lookup"><span data-stu-id="036c6-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="036c6-130">Ek olanları ihtiyacınız varsa, bunları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="036c6-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="036c6-131">Oluşturma ve uygulama parolaları silme</span><span class="sxs-lookup"><span data-stu-id="036c6-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="036c6-132">İlk oturum açma işleminiz sırasında kullanabileceğiniz bir uygulama parolası verilir.</span><span class="sxs-lookup"><span data-stu-id="036c6-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="036c6-133">Ayrıca, oluşturabilir ve daha sonra uygulama parolalarını Sil.</span><span class="sxs-lookup"><span data-stu-id="036c6-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="036c6-134">Uygulama parolalarını Sil nasıl çok faktörlü kimlik doğrulaması nasıl kullandığınıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="036c6-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="036c6-135">Aşağıdaki yanıt hello toomanage uygulama parolaları nereye toodetermine sorular:</span><span class="sxs-lookup"><span data-stu-id="036c6-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="036c6-136">Kişisel Microsoft hesabınız için iki aşamalı doğrulama kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="036c6-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="036c6-137">Yanıt Evet ise, toohello başvurmalıdır [uygulama parolaları ve iki aşamalı doğrulamayı](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) Yardım makalesi.</span><span class="sxs-lookup"><span data-stu-id="036c6-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="036c6-138">Öyle değilse, iki tooquestion devam edin.</span><span class="sxs-lookup"><span data-stu-id="036c6-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="036c6-139">İş veya Okul hesabınız için iki aşamalı doğrulamayı kullanmak için Tamam.</span><span class="sxs-lookup"><span data-stu-id="036c6-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="036c6-140">Bu toosign tooOffice 365 uygulamalarında kullanıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="036c6-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="036c6-141">Yanıt Evet ise, çok başvurmalıdır[Office 365 için bir uygulama parolası oluşturmanız](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) Yardım.</span><span class="sxs-lookup"><span data-stu-id="036c6-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="036c6-142">Öyle değilse, tooquestion üç devam edin.</span><span class="sxs-lookup"><span data-stu-id="036c6-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="036c6-143">Microsoft Azure ile iki aşamalı doğrulama kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="036c6-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="036c6-144">Yanıt Evet ise, toohello devam [hello Azure portalında uygulama parolaları yönetme](#manage-app-passwords-in-the-Azure-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="036c6-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="036c6-145">Öyle değilse, tooquestion dört devam edin.</span><span class="sxs-lookup"><span data-stu-id="036c6-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="036c6-146">İki aşamalı doğrulamayı kullandığınızda emin değil misiniz?</span><span class="sxs-lookup"><span data-stu-id="036c6-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="036c6-147">Toohello devam [hello MyApps portal ile uygulama parolaları yönetme](#manage-app-passwords-with-the-myapps-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="036c6-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="036c6-148">Hello Azure portalında uygulama parolaları yönetme</span><span class="sxs-lookup"><span data-stu-id="036c6-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="036c6-149">İki aşamalı doğrulamayı Azure ile kullanırsanız, toocreate uygulama parolaları hello Azure portal aracılığıyla istiyor.</span><span class="sxs-lookup"><span data-stu-id="036c6-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="036c6-150">hello Azure portal toocreate uygulama parolaları</span><span class="sxs-lookup"><span data-stu-id="036c6-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="036c6-151">İçinde toohello Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="036c6-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="036c6-152">Merhaba üstünde, kullanıcı adını sağ tıklatın ve ek güvenlik doğrulama'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="036c6-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="036c6-153">Uygulama parolaları hello üstünde hello düzenleyebileceğinizi sayfasında seçin</span><span class="sxs-lookup"><span data-stu-id="036c6-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="036c6-154">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="036c6-154">Click **Create**.</span></span>
5. <span data-ttu-id="036c6-155">Merhaba uygulama parolası için bir ad girin ve tıklayın **sonraki**</span><span class="sxs-lookup"><span data-stu-id="036c6-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="036c6-156">Merhaba uygulama parolası toohello panoya kopyalayın ve uygulamanıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="036c6-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Bulut](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="036c6-158">hello Azure portal toodelete uygulama parolaları</span><span class="sxs-lookup"><span data-stu-id="036c6-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="036c6-159">İçinde toohello Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="036c6-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="036c6-160">Merhaba üstünde, kullanıcı adını sağ tıklatın ve ek güvenlik doğrulama'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="036c6-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="036c6-161">Merhaba üstünde, sonraki tooadditional güvenlik doğrulama seçin **uygulama parolaları.**</span><span class="sxs-lookup"><span data-stu-id="036c6-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="036c6-162">Toodelete, select istediğiniz sonraki toohello uygulama parolası **silmek**.</span><span class="sxs-lookup"><span data-stu-id="036c6-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="036c6-163">Merhaba silmeyi onaylamak **Evet**.</span><span class="sxs-lookup"><span data-stu-id="036c6-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="036c6-164">Merhaba uygulama parolası silindikten sonra tıklayabilirsiniz **kapatmak**.</span><span class="sxs-lookup"><span data-stu-id="036c6-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="036c6-165">Uygulama parolaları hello MyApps portalı ile yönetin.</span><span class="sxs-lookup"><span data-stu-id="036c6-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="036c6-166">Çok faktörlü kimlik doğrulaması kullanımını emin değilseniz, daha sonra her zaman oluşturabilir ve hello myapps portalı üzerinden uygulama parolalarını Sil.</span><span class="sxs-lookup"><span data-stu-id="036c6-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="036c6-167">kullanarak bir uygulama parolası toocreate hello Myapps portalı</span><span class="sxs-lookup"><span data-stu-id="036c6-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="036c6-168">Çok oturum[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="036c6-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="036c6-169">Adınızı hello üst sağ tıklatın ve seçin **profil**.</span><span class="sxs-lookup"><span data-stu-id="036c6-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="036c6-170">Seçin **ek güvenlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="036c6-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="036c6-171">![Ek güvenlik doğrulaması - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="036c6-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="036c6-172">Seçin **uygulama parolaları**.</span><span class="sxs-lookup"><span data-stu-id="036c6-172">Select **app passwords**.</span></span>
   <span data-ttu-id="036c6-173">![Uygulama parolaları - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="036c6-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="036c6-174">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="036c6-174">Click **Create**.</span></span>
6. <span data-ttu-id="036c6-175">Merhaba uygulama parolası için bir ad girin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="036c6-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="036c6-176">Merhaba uygulama parolası toohello panoya kopyalayın ve uygulamanıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="036c6-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="036c6-177">![Bir uygulama parolası oluşturma](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="036c6-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="036c6-178">kullanarak bir uygulama parolası toodelete hello Myapps portalı</span><span class="sxs-lookup"><span data-stu-id="036c6-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="036c6-179">Çok oturum[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="036c6-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="036c6-180">Merhaba üstünde profilini seçin.</span><span class="sxs-lookup"><span data-stu-id="036c6-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="036c6-181">Seçin **ek güvenlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="036c6-181">Select **Additional Security Verification**.</span></span>

   ![Ek güvenlik doğrulaması - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="036c6-183">Seçin **uygulama parolaları**.</span><span class="sxs-lookup"><span data-stu-id="036c6-183">Select **app passwords**.</span></span>

   ![Uygulama parolaları - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="036c6-185">Toodelete, istediğiniz sonraki toohello uygulama parolası tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="036c6-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Bir uygulama parolası Sil](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="036c6-187">Tıklayarak, bu parolayı toodelete istediğinizi onaylamak **Evet**.</span><span class="sxs-lookup"><span data-stu-id="036c6-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="036c6-188">Merhaba uygulama parolası silindikten sonra tıklayabilirsiniz **kapatmak**.</span><span class="sxs-lookup"><span data-stu-id="036c6-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="036c6-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="036c6-189">Next steps</span></span>

- [<span data-ttu-id="036c6-190">İki basamaklı doğrulama ayarlarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="036c6-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="036c6-191">Merhaba deneyin [Microsoft Authenticator uygulaması](microsoft-authenticator-app-how-to.md) tooverify oturum açma işlemleri metinleri veya aramaları almasını yerine uygulama bildirimleri ile.</span><span class="sxs-lookup"><span data-stu-id="036c6-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
