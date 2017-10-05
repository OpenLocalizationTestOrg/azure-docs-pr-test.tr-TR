---
title: "Federasyon için yapılandırılan bir galeri uygulamaya oturumu açmada sorun çoklu oturum açma | Microsoft Docs"
description: "Yönergeler için yapılandırdığınız bir uygulamaya SAML tabanlı Federasyon tek oturum açma için Azure AD ile imzalarken belirli hataları"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0fc5a8eb3d033d60bf6082d61bf1698924ab91c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="814b6-103">Federasyon çoklu oturum açma için yapılandırılmış bir galeri uygulaması için oturum açma sorunları</span><span class="sxs-lookup"><span data-stu-id="814b6-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="814b6-104">Sorunu gidermek için izleme olarak Azure AD uygulama yapılandırmasını doğrulayın gerekir:</span><span class="sxs-lookup"><span data-stu-id="814b6-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="814b6-105">Azure AD galeri uygulama için tüm yapılandırma adımları izlediğinizi.</span><span class="sxs-lookup"><span data-stu-id="814b6-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="814b6-106">Kimlik ve yanıt AAD'de yapılandırılmış URL'yi eşleşen bunlar uygulamadaki beklenen değerler</span><span class="sxs-lookup"><span data-stu-id="814b6-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="814b6-107">Uygulamayı kullanıcılara atanan</span><span class="sxs-lookup"><span data-stu-id="814b6-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="814b6-108">Uygulama dizinde bulunamadı</span><span class="sxs-lookup"><span data-stu-id="814b6-108">Application not found in directory</span></span>

<span data-ttu-id="814b6-109">*Hata AADSTS70001: Uygulama, tanımlayıcısı 'https://contoso.com' dizininde bulunamadı*.</span><span class="sxs-lookup"><span data-stu-id="814b6-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="814b6-110">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="814b6-110">**Possible cause**</span></span>

<span data-ttu-id="814b6-111">Azure ad SAML isteğinde uygulamadan özniteliği gönderir veren Azure AD uygulamada yapılandırılan tanımlayıcı değeri eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="814b6-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="814b6-112">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="814b6-112">**Resolution**</span></span>

<span data-ttu-id="814b6-113">Bu tanımlayıcı eşleştirme SAML isteğinde veren özniteliğinde emin Azure AD içinde yapılandırılan değeri:</span><span class="sxs-lookup"><span data-stu-id="814b6-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="814b6-114">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="814b6-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="814b6-115">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="814b6-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="814b6-116">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="814b6-117">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="814b6-118">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="814b6-119">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="814b6-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="814b6-120">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="814b6-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="814b6-121">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="814b6-122">Git **etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="814b6-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="814b6-123">Tanımlayıcı metin değerinde hata görüntülenen tanımlayıcı değeri değeri eşleşen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="814b6-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="814b6-124">Azure AD'de veya güncelleştirilen tanımlayıcı değerine ve bu değeri gönderir SAML isteğinde uygulama tarafından eşleşen sonra uygulamaya oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="814b6-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="814b6-125">Yanıt adresini uygulama için yapılandırılan yanıt adresleri eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="814b6-125">The reply address does not match the reply addresses configured for the application.</span></span>

<span data-ttu-id="814b6-126">*Hata AADSTS50011: Yanıt adresini 'https://contoso.com' uygulaması için yapılandırılmış yanıt adresleri eşleşmiyor.*</span><span class="sxs-lookup"><span data-stu-id="814b6-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span>

<span data-ttu-id="814b6-127">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="814b6-127">**Possible cause**</span></span>

<span data-ttu-id="814b6-128">SAML isteğinde AssertionConsumerServiceURL değerinde yanıt URL'si değer veya desen Azure AD içinde yapılandırılmış eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="814b6-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="814b6-129">Hatayı görmek URL SAML isteğinde AssertionConsumerServiceURL değerdir.</span><span class="sxs-lookup"><span data-stu-id="814b6-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span>

<span data-ttu-id="814b6-130">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="814b6-130">**Resolution**</span></span>

<span data-ttu-id="814b6-131">Bu yanıt URL'si eşleşen SAML isteğinde AssertionConsumerServiceURL değerinde emin Azure AD içinde yapılandırılan değeri.</span><span class="sxs-lookup"><span data-stu-id="814b6-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="814b6-132">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="814b6-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="814b6-133">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="814b6-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="814b6-134">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="814b6-135">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="814b6-136">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-136">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="814b6-137">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="814b6-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="814b6-138">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="814b6-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="814b6-139">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="814b6-140">Git **etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="814b6-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="814b6-141">Doğrulamak veya SAML isteğinde AssertionConsumerServiceURL değerle eşleşecek şekilde yanıt URL'si textbox değeri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="814b6-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>  
    * <span data-ttu-id="814b6-142">Yanıt URL'si metin kutusuna görmüyorsanız seçin **Göster Gelişmiş URL ayarları** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="814b6-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="814b6-143">Azure AD'de veya güncelleştirilen yanıt URL'si değerine ve bu değeri gönderir SAML isteğinde uygulama tarafından eşleşen sonra uygulamaya oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="814b6-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="814b6-144">Kullanıcı bir role atanmış olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="814b6-144">User not assigned a role</span></span>

<span data-ttu-id="814b6-145">*Hata AADSTS50105: Oturum açmış olan kullanıcının 'brian@contoso.com' uygulaması için bir rol atanmamış*.</span><span class="sxs-lookup"><span data-stu-id="814b6-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="814b6-146">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="814b6-146">**Possible cause**</span></span>

<span data-ttu-id="814b6-147">Kullanıcı Azure AD'de uygulama erişim izni yok.</span><span class="sxs-lookup"><span data-stu-id="814b6-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="814b6-148">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="814b6-148">**Resolution**</span></span>

<span data-ttu-id="814b6-149">Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="814b6-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="814b6-150">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="814b6-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="814b6-151">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="814b6-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="814b6-152">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="814b6-153">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="814b6-154">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="814b6-155">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="814b6-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="814b6-156">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="814b6-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="814b6-157">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="814b6-158">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="814b6-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="814b6-159">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="814b6-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="814b6-160">Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="814b6-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="814b6-161">Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="814b6-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="814b6-162">Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="814b6-163">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="814b6-164">Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="814b6-165">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="814b6-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="814b6-166">Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="814b6-167">Bir kısa süre sonra seçtiğiniz kullanıcıların çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="814b6-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="814b6-168">Bir geçerli SAML istekte</span><span class="sxs-lookup"><span data-stu-id="814b6-168">Not a valid SAML Request</span></span>

<span data-ttu-id="814b6-169">*Hata AADSTS75005: İstek bir geçerli Saml2 protokol iletisi değil.*</span><span class="sxs-lookup"><span data-stu-id="814b6-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="814b6-170">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="814b6-170">**Possible cause**</span></span>

<span data-ttu-id="814b6-171">Azure AD çoklu oturum açma için uygulama tarafından gönderilen isteği SAML desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="814b6-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="814b6-172">Bazı yaygın sorunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="814b6-172">Some common issues are:</span></span>

-   <span data-ttu-id="814b6-173">SAML isteğinde gerekli alanlar eksik</span><span class="sxs-lookup"><span data-stu-id="814b6-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="814b6-174">SAML kodlanmış isteği yöntemi</span><span class="sxs-lookup"><span data-stu-id="814b6-174">SAML request encoded method</span></span>

<span data-ttu-id="814b6-175">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="814b6-175">**Resolution**</span></span>

1.  <span data-ttu-id="814b6-176">SAML isteğinde yakalayın.</span><span class="sxs-lookup"><span data-stu-id="814b6-176">Capture SAML request.</span></span> <span data-ttu-id="814b6-177">öğreticiyi izleyin [SAML tabanlı çoklu oturum açma uygulamaları için Azure AD içinde hata ayıklamak nasıl](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) SAML isteğinde yakalama öğrenin.</span><span class="sxs-lookup"><span data-stu-id="814b6-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="814b6-178">Paylaşım ve uygulamanın satıcısına başvurun:</span><span class="sxs-lookup"><span data-stu-id="814b6-178">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="814b6-179">SAML isteği</span><span class="sxs-lookup"><span data-stu-id="814b6-179">SAML request</span></span>

   -   [<span data-ttu-id="814b6-180">Azure AD çoklu oturum açma SAML protokolü gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="814b6-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="814b6-181">Bunlar doğrulamalıdır çoklu oturum açma için Azure AD SAML uygulama destekledikleri.</span><span class="sxs-lookup"><span data-stu-id="814b6-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="814b6-182">RequiredResourceAccess listesinde kaynak yok</span><span class="sxs-lookup"><span data-stu-id="814b6-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="814b6-183">*Hata AADSTS65005: istemci uygulama kaynağa erişim isteğinde bulundu ' 00000002-0000-0000-c000-000000000000'. İstemci, kendi requiredResourceAccess listesinde bu kaynak belirtilmedi bu isteği başarısız oldu*.</span><span class="sxs-lookup"><span data-stu-id="814b6-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="814b6-184">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="814b6-184">**Possible cause**</span></span>

<span data-ttu-id="814b6-185">Uygulama nesnesi bozuk.</span><span class="sxs-lookup"><span data-stu-id="814b6-185">The application object is corrupted.</span></span>

<span data-ttu-id="814b6-186">**Çözüm: seçeneği 1**</span><span class="sxs-lookup"><span data-stu-id="814b6-186">**Resolution: option 1**</span></span>

<span data-ttu-id="814b6-187">Sorunu çözmek için Azure AD yapılandırmasında benzersiz tanımlayıcısı değeri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="814b6-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span></span> <span data-ttu-id="814b6-188">Tanımlayıcı değeri eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="814b6-188">To add a Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="814b6-189">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="814b6-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="814b6-190">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="814b6-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="814b6-191">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="814b6-192">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="814b6-193">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="814b6-194">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="814b6-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="814b6-195">Çoklu oturum açma yapılandırdığınız uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="814b6-195">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="814b6-196">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde</span><span class="sxs-lookup"><span data-stu-id="814b6-196">Once the application loads, click on the **Single sign-on** from the application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="814b6-197">Altında **etki alanı ve URL** bölümünde, denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="814b6-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="814b6-198">içinde **tanımlayıcısı** metin kutusuna uygulama için benzersiz bir tanımlayıcı yazın.</span><span class="sxs-lookup"><span data-stu-id="814b6-198">in the **Identifier** textbox type a unique identifier for the application.</span></span>

10. <span data-ttu-id="814b6-199">**Kaydet** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="814b6-199">**Save** the configuration.</span></span>


<span data-ttu-id="814b6-200">**Çözüm seçeneği 2**</span><span class="sxs-lookup"><span data-stu-id="814b6-200">**Resolution option 2**</span></span>

<span data-ttu-id="814b6-201">Yukarıdaki 1. seçenek sizin için olmadıysa dizinden uygulamayı kaldırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="814b6-201">If option 1 above did not work for you, try removing the application from the directory.</span></span> <span data-ttu-id="814b6-202">Ardından, ekleyin ve uygulamayı yeniden yapılandırmak, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="814b6-202">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="814b6-203">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="814b6-203">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="814b6-204">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="814b6-204">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="814b6-205">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="814b6-206">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-206">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="814b6-207">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-207">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="814b6-208">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="814b6-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="814b6-209">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="814b6-209">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="814b6-210">Tıklatın **silmek** uygulamanın üst sol **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="814b6-210">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="814b6-211">Azure AD yenileyin ve Azure AD Galeriden uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="814b6-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="814b6-212">Ardından, uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="814b6-212">Then, Configure the application</span></span>

<span data-ttu-id="814b6-213"><span id="_Hlk477190176" class="anchor"></span>Uygulama yeniden yapılandırmadan sonra uygulamaya oturum açabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="814b6-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="814b6-214">Sertifika veya anahtar yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="814b6-214">Certificate or key not configured</span></span>

<span data-ttu-id="814b6-215">*Hata AADSTS50003: yapılandırılmış hiçbir imzalama anahtarı.*</span><span class="sxs-lookup"><span data-stu-id="814b6-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="814b6-216">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="814b6-216">**Possible cause**</span></span>

<span data-ttu-id="814b6-217">Uygulama nesnesi bozuk ve Azure AD uygulama için yapılandırılan sertifika tanımıyor.</span><span class="sxs-lookup"><span data-stu-id="814b6-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="814b6-218">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="814b6-218">**Resolution**</span></span>

<span data-ttu-id="814b6-219">Silin ve yeni bir sertifika oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="814b6-219">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="814b6-220">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="814b6-220">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="814b6-221">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="814b6-221">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="814b6-222">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="814b6-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="814b6-223">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-223">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="814b6-224">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="814b6-224">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="814b6-225">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="814b6-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="814b6-226">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="814b6-226">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="814b6-227">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="814b6-227">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="814b6-228">tıklatın **yeni sertifika oluştur** altında **imzalama sertifikası SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="814b6-228">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="814b6-229">Sona erme tarihini seçin.</span><span class="sxs-lookup"><span data-stu-id="814b6-229">Select Expiration date.</span></span> <span data-ttu-id="814b6-230">Ardından **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="814b6-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="814b6-231">Denetleme **yeni sertifika etkin hale getirin** etkin sertifikanın geçersiz kılmak için.</span><span class="sxs-lookup"><span data-stu-id="814b6-231">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="814b6-232">Ardından **kaydetmek** dikey pencerenin üstündeki ve geçiş sertifikası etkinleştirmek için kabul edin.</span><span class="sxs-lookup"><span data-stu-id="814b6-232">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="814b6-233">Altında **SAML imzalama sertifikası** 'yi tıklatın **kaldırmak** kaldırmak için **kullanılmayan** sertifika.</span><span class="sxs-lookup"><span data-stu-id="814b6-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="814b6-234">Uygulamaya gönderilen SAML talep özelleştirirken sorunu</span><span class="sxs-lookup"><span data-stu-id="814b6-234">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="814b6-235">Uygulamanıza gönderilen SAML öznitelik taleplerini özelleştirmek öğrenmek için bkz: [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="814b6-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="814b6-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="814b6-236">Next steps</span></span>
[<span data-ttu-id="814b6-237">SAML tabanlı çoklu oturum açma Azure AD uygulamalarında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="814b6-237">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
