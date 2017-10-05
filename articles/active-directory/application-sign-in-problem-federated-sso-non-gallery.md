---
title: "Federasyon için yapılandırılan bir galeri olmayan uygulamaya oturumu açmada sorun çoklu oturum açma | Microsoft Docs"
description: "SAML tabanlı Federasyon tek oturum açma için Azure AD ile yapılandırılmış bir uygulama için oturum açarken karşılaşabilecekleri belirli sorunları için yönergeler"
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
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="08eea-103">Federasyon çoklu oturum açma için yapılandırılmış bir galeri olmayan uygulama oturum açma sorunları</span><span class="sxs-lookup"><span data-stu-id="08eea-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="08eea-104">Sorunu gidermek için izleme olarak Azure AD uygulama yapılandırmasını doğrulayın gerekir:</span><span class="sxs-lookup"><span data-stu-id="08eea-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="08eea-105">Azure AD galeri uygulama için tüm yapılandırma adımları izlediğinizi.</span><span class="sxs-lookup"><span data-stu-id="08eea-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="08eea-106">Kimlik ve yanıt AAD'de yapılandırılmış URL'yi eşleşen bunlar uygulamadaki beklenen değerler</span><span class="sxs-lookup"><span data-stu-id="08eea-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="08eea-107">Uygulamayı kullanıcılara atanan</span><span class="sxs-lookup"><span data-stu-id="08eea-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="08eea-108">Uygulama dizinde bulunamadı</span><span class="sxs-lookup"><span data-stu-id="08eea-108">Application not found in directory</span></span>

<span data-ttu-id="08eea-109">*Hata AADSTS70001: Uygulama, tanımlayıcısı 'https://contoso.com' dizininde bulunamadı*.</span><span class="sxs-lookup"><span data-stu-id="08eea-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="08eea-110">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="08eea-110">**Possible cause**</span></span>

<span data-ttu-id="08eea-111">Azure ad SAML isteğinde uygulamadan özniteliği gönderir veren Azure AD uygulamada yapılandırılan tanımlayıcı değeri eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="08eea-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="08eea-112">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="08eea-112">**Resolution**</span></span>

<span data-ttu-id="08eea-113">Bu tanımlayıcı eşleştirme SAML isteğinde veren özniteliğinde emin Azure AD içinde yapılandırılan değeri:</span><span class="sxs-lookup"><span data-stu-id="08eea-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="08eea-114">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="08eea-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="08eea-115">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08eea-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08eea-116">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08eea-117">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08eea-118">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="08eea-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="08eea-119">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="08eea-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08eea-120">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="08eea-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="08eea-121">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08eea-122"><span id="_Hlk477190042" class="anchor"></span>Git **etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="08eea-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="08eea-123">Tanımlayıcı metin değerinde hata görüntülenen tanımlayıcı değeri değeri eşleşen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="08eea-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="08eea-124">Azure AD'de veya güncelleştirilen tanımlayıcı değerine ve bu değeri gönderir SAML isteğinde uygulama tarafından eşleşen sonra uygulamaya oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="08eea-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="08eea-125">Yanıt adresini uygulama için yapılandırılan yanıt adresleri eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="08eea-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="08eea-126">*Hata AADSTS50011: Yanıt adresini 'https://contoso.com' uygulaması için yapılandırılmış yanıt adresleri eşleşmiyor.*</span><span class="sxs-lookup"><span data-stu-id="08eea-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="08eea-127">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="08eea-127">**Possible cause**</span></span> 

<span data-ttu-id="08eea-128">SAML isteğinde AssertionConsumerServiceURL değerinde yanıt URL'si değer veya desen Azure AD içinde yapılandırılmış eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="08eea-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="08eea-129">Hatayı görmek URL SAML isteğinde AssertionConsumerServiceURL değerdir.</span><span class="sxs-lookup"><span data-stu-id="08eea-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="08eea-130">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="08eea-130">**Resolution**</span></span> 

<span data-ttu-id="08eea-131">Bu yanıt URL'si eşleşen SAML isteğinde AssertionConsumerServiceURL değerinde emin Azure AD içinde yapılandırılan değeri.</span><span class="sxs-lookup"><span data-stu-id="08eea-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="08eea-132">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="08eea-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="08eea-133">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08eea-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="08eea-134">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="08eea-135">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="08eea-136">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="08eea-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="08eea-137">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm Uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="08eea-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="08eea-138">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="08eea-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="08eea-139">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08eea-140">Git **etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="08eea-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="08eea-141">Doğrulamak veya SAML isteğinde AssertionConsumerServiceURL değerle eşleşecek şekilde yanıt URL'si textbox değeri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="08eea-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="08eea-142">Yanıt URL'si metin kutusuna görmüyorsanız seçin **Göster Gelişmiş URL ayarları** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="08eea-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="08eea-143">Azure AD'de veya güncelleştirilen yanıt URL'si değerine ve bu değeri gönderir SAML isteğinde uygulama tarafından eşleşen sonra uygulamaya oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="08eea-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="08eea-144">Kullanıcı bir role atanmış olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="08eea-144">User not assigned a role</span></span>

<span data-ttu-id="08eea-145">*Hata AADSTS50105: Oturum açmış olan kullanıcının 'brian@contoso.com' uygulama için bir role atanmış olmamalıdır*</span><span class="sxs-lookup"><span data-stu-id="08eea-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="08eea-146">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="08eea-146">**Possible cause**</span></span>

<span data-ttu-id="08eea-147">Kullanıcı Azure AD'de uygulama erişim izni yok.</span><span class="sxs-lookup"><span data-stu-id="08eea-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="08eea-148">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="08eea-148">**Resolution**</span></span>

<span data-ttu-id="08eea-149">Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08eea-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="08eea-150">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08eea-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08eea-151">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08eea-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08eea-152">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08eea-153">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08eea-154">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="08eea-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="08eea-155">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="08eea-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08eea-156">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="08eea-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="08eea-157">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08eea-158">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="08eea-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="08eea-159">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="08eea-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="08eea-160">Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="08eea-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="08eea-161">Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="08eea-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="08eea-162">Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="08eea-163">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="08eea-164">Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="08eea-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="08eea-165">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="08eea-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="08eea-166">Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="08eea-167">Bir kısa süre sonra seçtiğiniz kullanıcıların çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="08eea-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="08eea-168">Bir geçerli SAML istekte</span><span class="sxs-lookup"><span data-stu-id="08eea-168">Not a valid SAML Request</span></span>

<span data-ttu-id="08eea-169">*Hata AADSTS75005: İstek bir geçerli Saml2 protokol iletisi değil.*</span><span class="sxs-lookup"><span data-stu-id="08eea-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="08eea-170">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="08eea-170">**Possible cause**</span></span>

<span data-ttu-id="08eea-171">Azure AD çoklu oturum açma için uygulama tarafından gönderilen isteği SAML desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="08eea-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="08eea-172">Bazı yaygın sorunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08eea-172">Some common issues are:</span></span>

-   <span data-ttu-id="08eea-173">SAML isteğinde gerekli alanlar eksik</span><span class="sxs-lookup"><span data-stu-id="08eea-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="08eea-174">SAML kodlanmış isteği yöntemi</span><span class="sxs-lookup"><span data-stu-id="08eea-174">SAML request encoded method</span></span>

<span data-ttu-id="08eea-175">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="08eea-175">**Resolution**</span></span>

1.  <span data-ttu-id="08eea-176">SAML isteğinde yakalayın.</span><span class="sxs-lookup"><span data-stu-id="08eea-176">Capture SAML request.</span></span> <span data-ttu-id="08eea-177">öğreticiyi izleyin [SAML tabanlı çoklu oturum açma uygulamaları için Azure AD içinde hata ayıklamak nasıl](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) SAML isteğinde yakalama öğrenin.</span><span class="sxs-lookup"><span data-stu-id="08eea-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="08eea-178">Paylaşım ve uygulamanın satıcısına başvurun:</span><span class="sxs-lookup"><span data-stu-id="08eea-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="08eea-179">SAML isteği</span><span class="sxs-lookup"><span data-stu-id="08eea-179">SAML request</span></span>

    -   [<span data-ttu-id="08eea-180">Azure AD çoklu oturum açma SAML protokolü gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="08eea-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="08eea-181">Bunlar doğrulamalıdır çoklu oturum açma için Azure AD SAML uygulama destekledikleri.</span><span class="sxs-lookup"><span data-stu-id="08eea-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="08eea-182">RequiredResourceAccess listesinde kaynak yok</span><span class="sxs-lookup"><span data-stu-id="08eea-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="08eea-183">*Hata AADSTS65005: İstemci uygulama kaynağa erişim isteğinde bulundu ' 00000002-0000-0000-c000-000000000000'. İstemci, kendi requiredResourceAccess listesinde bu kaynak belirtilmedi bu isteği başarısız oldu*.</span><span class="sxs-lookup"><span data-stu-id="08eea-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="08eea-184">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="08eea-184">**Possible cause**</span></span>

<span data-ttu-id="08eea-185">Uygulama nesnesi bozuk.</span><span class="sxs-lookup"><span data-stu-id="08eea-185">The application object is corrupted.</span></span>

<span data-ttu-id="08eea-186">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="08eea-186">**Resolution**</span></span>

<span data-ttu-id="08eea-187">Sorunu çözmek için uygulama dizininden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="08eea-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="08eea-188">Ardından, ekleyin ve uygulamayı yeniden yapılandırmak, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08eea-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="08eea-189">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="08eea-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="08eea-190">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08eea-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08eea-191">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08eea-192">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08eea-193">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="08eea-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="08eea-194">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="08eea-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08eea-195">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="08eea-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="08eea-196">Tıklatın **silmek** uygulamanın üst sol **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="08eea-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="08eea-197">Azure AD yenileyin ve Azure AD Galeriden uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08eea-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="08eea-198">Ardından, uygulamayı yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="08eea-198">Then, Configure the application again.</span></span>

<span data-ttu-id="08eea-199">Uygulama yeniden yapılandırmadan sonra uygulamaya oturum açabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08eea-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="08eea-200">Sertifika veya anahtar yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="08eea-200">Certificate or key not configured</span></span>

<span data-ttu-id="08eea-201">Hata AADSTS50003: yapılandırılmış hiçbir imzalama anahtarı.</span><span class="sxs-lookup"><span data-stu-id="08eea-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="08eea-202">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="08eea-202">**Possible cause**</span></span>

<span data-ttu-id="08eea-203">Uygulama nesnesi bozuk ve Azure AD uygulama için yapılandırılan sertifika tanımıyor.</span><span class="sxs-lookup"><span data-stu-id="08eea-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="08eea-204">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="08eea-204">**Resolution**</span></span>

<span data-ttu-id="08eea-205">Silin ve yeni bir sertifika oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08eea-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="08eea-206">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="08eea-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="08eea-207">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08eea-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08eea-208">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08eea-209">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08eea-210">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="08eea-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="08eea-211">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="08eea-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08eea-212">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="08eea-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="08eea-213">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08eea-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08eea-214">tıklatın **yeni sertifika oluştur** altında **imzalama sertifikası SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="08eea-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="08eea-215">Sona erme tarihini seçin.</span><span class="sxs-lookup"><span data-stu-id="08eea-215">Select Expiration date.</span></span> <span data-ttu-id="08eea-216">Ardından **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="08eea-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="08eea-217">Denetleme **yeni sertifika etkin hale getirin** etkin sertifikanın geçersiz kılmak için.</span><span class="sxs-lookup"><span data-stu-id="08eea-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="08eea-218">Ardından **kaydetmek** dikey pencerenin üstündeki ve geçiş sertifikası etkinleştirmek için kabul edin.</span><span class="sxs-lookup"><span data-stu-id="08eea-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="08eea-219">Altında **SAML imzalama sertifikası** 'yi tıklatın **kaldırmak** kaldırmak için **kullanılmayan** sertifika.</span><span class="sxs-lookup"><span data-stu-id="08eea-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="08eea-220">Uygulamaya gönderilen SAML talep özelleştirirken sorunu</span><span class="sxs-lookup"><span data-stu-id="08eea-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="08eea-221">Uygulamanıza gönderilen SAML öznitelik taleplerini özelleştirmek öğrenmek için bkz: [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="08eea-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08eea-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08eea-222">Next steps</span></span>
[<span data-ttu-id="08eea-223">Azure AD çoklu oturum açma SAML protokolü gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="08eea-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
