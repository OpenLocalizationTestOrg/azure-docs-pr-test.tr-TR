---
title: "Azure MFA uygulama parolaları kullanmak üzere nasıl? | Microsoft Belgeleri"
description: "Bu sayfa, kullanıcıların uygulama parolaları nedir ve ne için ile kullanıldıkları Azure MFA Algıla anlamasına yardımcı olur."
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
ms.openlocfilehash: 1ecc2bdef5ff7ef8ed8dded7dc12428ce9657821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="99dbc-104">Azure çok faktörlü kimlik doğrulaması'ndaki uygulama parolaları nedir?</span><span class="sxs-lookup"><span data-stu-id="99dbc-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="99dbc-105">Exchange Active Sync kullanan Apple yerel e-posta istemcisi gibi belirli bir tarayıcı olmayan uygulamaları, şu anda çok faktörlü kimlik doğrulamasını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="99dbc-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="99dbc-106">Çok faktörlü kimlik doğrulaması kullanıcı başına etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="99dbc-107">Başka bir deyişle, bir kullanıcı, çok faktörlü kimlik doğrulamasını kullanamaz:</span><span class="sxs-lookup"><span data-stu-id="99dbc-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="99dbc-108">Kullanıcı için multi-Factor authentication etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="99dbc-108">The user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="99dbc-109">Kullanıcı, bir tarayıcı olmayan uygulama kullanmaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="99dbc-109">The user is trying to use a non-browser app.</span></span>

<span data-ttu-id="99dbc-110">Bir uygulama parolası kullanıcının uygulamayı kullanmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-110">An app password allows the user to use the app.</span></span>

<span data-ttu-id="99dbc-111">Bir uygulama parolası sahip olduktan sonra özgün parolanızı bu tarayıcı olmayan uygulamaları ile yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="99dbc-112">İki aşamalı doğrulama için kaydolduğunuzda, herkesin ikinci doğrulama de gerçekleştiremezsiniz parolanızla oturum oturum vermez Microsoft'a söyleyen.</span><span class="sxs-lookup"><span data-stu-id="99dbc-112">When you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="99dbc-113">İki aşamalı doğrulama için istenemez çünkü telefonunuzda Apple yerel e-posta istemcisi olarak oturum açamaz.</span><span class="sxs-lookup"><span data-stu-id="99dbc-113">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="99dbc-114">Bu sorun için çözüm kullanmadığınız daha güvenli bir uygulama parolası günlük oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="99dbc-114">The solution to this problem is to create a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="99dbc-115">Uygulama parolaları, iki aşamalı doğrulamayı destekleyemez yalnızca bu uygulamalar içindir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="99dbc-116">Uygulamalar çok faktörlü kimlik doğrulamasını atlamak ve çalışmaya devam uygulama parolasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-116">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>


> [!NOTE]
> <span data-ttu-id="99dbc-117">Office 2013 istemcileri (Outlook dahil) destekleyen yeni kimlik doğrulama protokolleri ve iki aşamalı doğrulamayla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="99dbc-118">Uygulama parolaları Office 2013 istemcilerle kullanım için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="99dbc-119">Daha fazla bilgi için bkz: [Office 2013 modern kimlik doğrulaması genel önizlemesi Duyuruldu](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="99dbc-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="99dbc-120">Uygulama parolaları kullanma</span><span class="sxs-lookup"><span data-stu-id="99dbc-120">How to use app passwords</span></span>
<span data-ttu-id="99dbc-121">Uygulama parolaları hakkında bilinmesi gereken bazı şeyler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="99dbc-121">Here are some things to know about app passwords:</span></span>

* <span data-ttu-id="99dbc-122">Kendi uygulama parolaları oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-122">You don't create your own app passwords.</span></span> <span data-ttu-id="99dbc-123">Bunlar otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="99dbc-123">They are automatically generated.</span></span>
* <span data-ttu-id="99dbc-124">Şu anda kullanıcı başına 40 parolalık bir sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="99dbc-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="99dbc-125">Sınıra ulaştıktan sonra bir uygulama parolası oluşturmak denerseniz, yeni bir tane oluşturmadan önce varolan uygulama parolalarınızdan birini silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-125">If you try to create an app password after you have reached the limit, you'll have to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="99dbc-126">Bir uygulama parolası aygıt başına, uygulama başına değil kullanın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="99dbc-127">Örneğin, dizüstü bilgisayarınız için bir uygulama parolası oluşturmanız ve tüm Dizüstü bilgisayarınızdaki uygulamalar için bu uygulama parolasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="99dbc-128">Daha sonra masaüstünüzde tüm uygulama için kullanılacak ikinci bir uygulama parolası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99dbc-128">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="99dbc-129">Bir uygulama parolası kaydettiğiniz iki aşamalı doğrulamayı ilk kez verilir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-129">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="99dbc-130">Ek olanları ihtiyacınız varsa, bunları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99dbc-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="99dbc-131">Oluşturma ve uygulama parolaları silme</span><span class="sxs-lookup"><span data-stu-id="99dbc-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="99dbc-132">İlk oturum açma işleminiz sırasında kullanabileceğiniz bir uygulama parolası verilir.</span><span class="sxs-lookup"><span data-stu-id="99dbc-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="99dbc-133">Ayrıca, oluşturabilir ve daha sonra uygulama parolalarını Sil.</span><span class="sxs-lookup"><span data-stu-id="99dbc-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="99dbc-134">Uygulama parolalarını Sil nasıl çok faktörlü kimlik doğrulaması nasıl kullandığınıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="99dbc-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="99dbc-135">Uygulama parolaları yönetmek için nereye belirlemek için aşağıdaki soruları yanıtlayın:</span><span class="sxs-lookup"><span data-stu-id="99dbc-135">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="99dbc-136">Kişisel Microsoft hesabınız için iki aşamalı doğrulama kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="99dbc-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="99dbc-137">Yanıt Evet ise, için başvurmalıdır [uygulama parolaları ve iki aşamalı doğrulamayı](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) Yardım makalesi.</span><span class="sxs-lookup"><span data-stu-id="99dbc-137">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="99dbc-138">Öyle değilse, iki soru devam edin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-138">If no, continue to question two.</span></span>

2. <span data-ttu-id="99dbc-139">İş veya Okul hesabınız için iki aşamalı doğrulamayı kullanmak için Tamam.</span><span class="sxs-lookup"><span data-stu-id="99dbc-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="99dbc-140">Bunu Office 365 uygulamalarda oturum açmak için kullandığınız?</span><span class="sxs-lookup"><span data-stu-id="99dbc-140">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="99dbc-141">Yanıt Evet ise, için başvurmalıdır [Office 365 için bir uygulama parolası oluşturmanız](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) Yardım.</span><span class="sxs-lookup"><span data-stu-id="99dbc-141">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="99dbc-142">Öyle değilse, soru üç devam edin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-142">If no, continue to question three.</span></span> 

3. <span data-ttu-id="99dbc-143">Microsoft Azure ile iki aşamalı doğrulama kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="99dbc-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="99dbc-144">Yanıt Evet ise, devam [Azure portalında uygulama parolaları yönetme](#manage-app-passwords-in-the-Azure-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-144">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="99dbc-145">Öyle değilse, dört soru devam edin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-145">If no, continue to question four.</span></span>

4. <span data-ttu-id="99dbc-146">İki aşamalı doğrulamayı kullandığınızda emin değil misiniz?</span><span class="sxs-lookup"><span data-stu-id="99dbc-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="99dbc-147">Devam [MyApps portal ile uygulama parolaları yönetme](#manage-app-passwords-with-the-myapps-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-147">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="99dbc-148">Azure portalında uygulama parolaları yönetme</span><span class="sxs-lookup"><span data-stu-id="99dbc-148">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="99dbc-149">İki aşamalı doğrulamayı Azure ile kullanırsanız, Azure portalı üzerinden uygulama parolaları oluşturmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="99dbc-149">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="99dbc-150">Azure portalında uygulama parolaları oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="99dbc-150">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="99dbc-151">Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-151">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="99dbc-152">En üstte, kullanıcı adını sağ tıklatın ve ek güvenlik doğrulama'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-152">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="99dbc-153">En üstte düzenleyebileceğinizi sayfasında uygulama parolaları seçin</span><span class="sxs-lookup"><span data-stu-id="99dbc-153">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="99dbc-154">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-154">Click **Create**.</span></span>
5. <span data-ttu-id="99dbc-155">Uygulama parolası için bir ad girin ve tıklayın **sonraki**</span><span class="sxs-lookup"><span data-stu-id="99dbc-155">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="99dbc-156">Uygulama parolasını panoya kopyalayın ve uygulamanıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-156">Copy the app password to the clipboard and paste it into your app.</span></span>
   
   ![Bulut](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="99dbc-158">Azure portalında uygulama parolaları silmek için</span><span class="sxs-lookup"><span data-stu-id="99dbc-158">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="99dbc-159">Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="99dbc-160">En üstte, kullanıcı adını sağ tıklatın ve ek güvenlik doğrulama'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-160">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="99dbc-161">Ek güvenlik doğrulaması yanındaki üst seçin **uygulama parolaları.**</span><span class="sxs-lookup"><span data-stu-id="99dbc-161">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="99dbc-162">Silmek istediğiniz uygulama parolası yanındaki seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-162">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="99dbc-163">Silme işlemini onaylamak **Evet**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-163">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="99dbc-164">Uygulama parolası silindikten sonra tıklayabilirsiniz **kapatmak**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-164">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="99dbc-165">Uygulama parolaları MyApps portalı ile yönetin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-165">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="99dbc-166">Çok faktörlü kimlik doğrulaması kullanımını emin değilseniz, daha sonra her zaman oluşturabilir ve myapps portalı üzerinden uygulama parolalarını Sil.</span><span class="sxs-lookup"><span data-stu-id="99dbc-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="99dbc-167">Myapps Portalı'nı kullanarak bir uygulama parolası oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="99dbc-167">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="99dbc-168">Oturum [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="99dbc-168">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="99dbc-169">Sağ üst köşedeki adınızın ve seçin **profil**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-169">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="99dbc-170">Seçin **ek güvenlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="99dbc-171">![Ek güvenlik doğrulaması - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="99dbc-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="99dbc-172">Seçin **uygulama parolaları**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-172">Select **app passwords**.</span></span>
   <span data-ttu-id="99dbc-173">![Uygulama parolaları - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="99dbc-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="99dbc-174">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-174">Click **Create**.</span></span>
6. <span data-ttu-id="99dbc-175">Uygulama parolası için bir ad girin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-175">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="99dbc-176">Uygulama parolasını panoya kopyalayın ve uygulamanıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-176">Copy the app password to the clipboard and paste it into your app.</span></span>
   <span data-ttu-id="99dbc-177">![Bir uygulama parolası oluşturma](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="99dbc-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="99dbc-178">Myapps Portalı'nı kullanarak bir uygulama parolası silmek için</span><span class="sxs-lookup"><span data-stu-id="99dbc-178">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="99dbc-179">Oturum [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="99dbc-179">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="99dbc-180">En üstte profilini seçin.</span><span class="sxs-lookup"><span data-stu-id="99dbc-180">At the top, select profile.</span></span>
3. <span data-ttu-id="99dbc-181">Seçin **ek güvenlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-181">Select **Additional Security Verification**.</span></span>

   ![Ek güvenlik doğrulaması - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="99dbc-183">Seçin **uygulama parolaları**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-183">Select **app passwords**.</span></span>

   ![Uygulama parolaları - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="99dbc-185">Silmek istediğiniz uygulama parolası yanındaki tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-185">Next to the app password you want to delete, click **Delete**.</span></span>

   ![Bir uygulama parolası Sil](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="99dbc-187">Parola tıklayarak silmek istediğinizi onaylamak **Evet**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-187">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="99dbc-188">Uygulama parolası silindikten sonra tıklayabilirsiniz **kapatmak**.</span><span class="sxs-lookup"><span data-stu-id="99dbc-188">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99dbc-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99dbc-189">Next steps</span></span>

- [<span data-ttu-id="99dbc-190">İki basamaklı doğrulama ayarlarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="99dbc-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="99dbc-191">Denemenin [Microsoft Authenticator uygulaması](microsoft-authenticator-app-how-to.md) oturum açma işlemleri metinleri veya aramaları almasını yerine uygulama bildirimleri ile doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="99dbc-191">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
