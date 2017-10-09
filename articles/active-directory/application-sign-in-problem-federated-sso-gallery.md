---
title: "Federasyon için yapılandırılan tooa galeri uygulamada imzalama aaaProblems çoklu oturum açma | Microsoft Docs"
description: "Yönergeler için yapılandırdığınız bir uygulamaya SAML tabanlı Federasyon tek oturum açma için Azure AD ile imzalarken hello belirli hataları"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="43579-103">Federasyon çoklu oturum açma için yapılandırılmış tooa galeri uygulamada oturum sorunları</span><span class="sxs-lookup"><span data-stu-id="43579-103">Problems signing in tooa gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="43579-104">tootroubleshoot, sorun izleme olarak Azure AD'de tooverify hello uygulama yapılandırması gerekir:</span><span class="sxs-lookup"><span data-stu-id="43579-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="43579-105">Hello Azure AD galeri uygulama için tüm hello yapılandırma adımları izlediğinizi.</span><span class="sxs-lookup"><span data-stu-id="43579-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="43579-106">Merhaba tanımlayıcısı ve yanıt AAD'de yapılandırılmış URL'si eşleşen bunlar hello uygulamada beklenen değerler</span><span class="sxs-lookup"><span data-stu-id="43579-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="43579-107">Toohello uygulama veya atanan kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="43579-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="43579-108">Uygulama dizinde bulunamadı</span><span class="sxs-lookup"><span data-stu-id="43579-108">Application not found in directory</span></span>

<span data-ttu-id="43579-109">*Hata AADSTS70001: Uygulama, tanımlayıcısı 'https://contoso.com' hello dizininde bulunamadı*.</span><span class="sxs-lookup"><span data-stu-id="43579-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="43579-110">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="43579-110">**Possible cause**</span></span>

<span data-ttu-id="43579-111">Merhaba veren özniteliği hello SAML isteğinde AD hello uygulama Azure AD yapılandırılmış hello tanımlayıcı değeri eşleşmiyor hello uygulama tooAzure gönderir.</span><span class="sxs-lookup"><span data-stu-id="43579-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="43579-112">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="43579-112">**Resolution**</span></span>

<span data-ttu-id="43579-113">Bu hello veren öznitelik hello Azure AD içinde yapılandırılmış tanımlayıcı değeri eşleşen hello SAML isteğinde emin olun:</span><span class="sxs-lookup"><span data-stu-id="43579-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="43579-114">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="43579-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="43579-115">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="43579-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43579-116">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="43579-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43579-117">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43579-118">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-118">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="43579-119">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="43579-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="43579-120">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="43579-120">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="43579-121">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43579-122">Çok Git**etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="43579-122">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="43579-123">Merhaba textbox hello değeri hello hata görüntülenen hello tanımlayıcı değeri için eşleştirme tanımlayıcı hello değeri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="43579-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="43579-124">Azure AD'de veya güncelleştirilen hello tanımlayıcı değerine ve hello SAML isteğinde hello uygulama tarafından eşleşen hello değeri gönderir sonra toohello uygulamada mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43579-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="43579-125">Merhaba yanıt adresi hello uygulama için yapılandırılan hello yanıt adresleri eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="43579-125">hello reply address does not match hello reply addresses configured for hello application.</span></span>

<span data-ttu-id="43579-126">*Hata AADSTS50011: hello yanıt adresini 'https://contoso.com' hello uygulama için yapılandırılan hello yanıt adresleri eşleşmiyor.*</span><span class="sxs-lookup"><span data-stu-id="43579-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span>

<span data-ttu-id="43579-127">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="43579-127">**Possible cause**</span></span>

<span data-ttu-id="43579-128">Merhaba hello SAML istekteki AssertionConsumerServiceURL değeri hello yanıt URL'si değer veya desen Azure AD içinde yapılandırılmış eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="43579-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="43579-129">Merhaba hello SAML istekteki AssertionConsumerServiceURL değeri hello hata gördüğünüz hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="43579-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span>

<span data-ttu-id="43579-130">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="43579-130">**Resolution**</span></span>

<span data-ttu-id="43579-131">Azure AD'de cihazın eşleşen hello yanıt URL'si değeri yapılandırılmış hello SAML isteğinde hello AssertionConsumerServiceURL değeri emin olun.</span><span class="sxs-lookup"><span data-stu-id="43579-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="43579-132">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="43579-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="43579-133">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="43579-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43579-134">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="43579-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43579-135">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43579-136">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-136">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="43579-137">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="43579-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="43579-138">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="43579-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="43579-139">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43579-140">Çok Git**etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="43579-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="43579-141">Doğrulamak veya hello yanıt URL'si metin kutusuna toomatch hello hello SAML istekteki AssertionConsumerServiceURL değeri hello değeri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="43579-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>  
    * <span data-ttu-id="43579-142">Merhaba yanıt URL'si textbox görmüyorsanız, hello seçin **Göster Gelişmiş URL ayarları** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="43579-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="43579-143">Azure AD'de veya güncelleştirilen hello yanıt URL'si değerine ve onu sonra hello değerle eşleşen hello uygulama tarafından hello SAML isteği gönderir, toohello uygulamada mümkün toosign olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="43579-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="43579-144">Kullanıcı bir role atanmış olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="43579-144">User not assigned a role</span></span>

<span data-ttu-id="43579-145">*Hata AADSTS50105: hello imzalı kullanıcı 'brian@contoso.com' hello uygulama için tooa rolü atanmamış*.</span><span class="sxs-lookup"><span data-stu-id="43579-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*.</span></span>

<span data-ttu-id="43579-146">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="43579-146">**Possible cause**</span></span>

<span data-ttu-id="43579-147">Azure AD erişim toohello uygulamada Hello kullanıcı verilmedi.</span><span class="sxs-lookup"><span data-stu-id="43579-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="43579-148">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="43579-148">**Resolution**</span></span>

<span data-ttu-id="43579-149">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="43579-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="43579-150">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="43579-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="43579-151">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="43579-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43579-152">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="43579-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43579-153">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43579-154">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="43579-155">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="43579-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="43579-156">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="43579-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="43579-157">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43579-158">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="43579-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="43579-159">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="43579-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="43579-160">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="43579-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="43579-161">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="43579-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="43579-162">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="43579-163">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="43579-164">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="43579-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="43579-165">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="43579-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="43579-166">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="43579-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="43579-167">Bir kısa süre sonra seçtiğiniz hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması.</span><span class="sxs-lookup"><span data-stu-id="43579-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="43579-168">Bir geçerli SAML istekte</span><span class="sxs-lookup"><span data-stu-id="43579-168">Not a valid SAML Request</span></span>

<span data-ttu-id="43579-169">*Hata AADSTS75005: hello isteği, geçerli bir Saml2 protokol iletisi değil.*</span><span class="sxs-lookup"><span data-stu-id="43579-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="43579-170">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="43579-170">**Possible cause**</span></span>

<span data-ttu-id="43579-171">Azure AD hello SAML çoklu oturum açma için Merhaba uygulaması tarafından gönderilen isteği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="43579-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="43579-172">Bazı yaygın sorunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="43579-172">Some common issues are:</span></span>

-   <span data-ttu-id="43579-173">Merhaba SAML isteğinde gerekli alanlar eksik</span><span class="sxs-lookup"><span data-stu-id="43579-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="43579-174">SAML kodlanmış isteği yöntemi</span><span class="sxs-lookup"><span data-stu-id="43579-174">SAML request encoded method</span></span>

<span data-ttu-id="43579-175">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="43579-175">**Resolution**</span></span>

1.  <span data-ttu-id="43579-176">SAML isteğinde yakalayın.</span><span class="sxs-lookup"><span data-stu-id="43579-176">Capture SAML request.</span></span> <span data-ttu-id="43579-177">Merhaba öğreticisini izleyin [nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure AD'de](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn nasıl toocapture hello SAML isteyin.</span><span class="sxs-lookup"><span data-stu-id="43579-177">follow hello tutorial [How toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="43579-178">Merhaba uygulamanın satıcısına ve Paylaşım başvurun:</span><span class="sxs-lookup"><span data-stu-id="43579-178">Contact hello application vendor and share:</span></span>

   -   <span data-ttu-id="43579-179">SAML isteği</span><span class="sxs-lookup"><span data-stu-id="43579-179">SAML request</span></span>

   -   [<span data-ttu-id="43579-180">Azure AD çoklu oturum açma SAML protokolü gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="43579-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="43579-181">Bunlar doğrulamalıdır hello Azure AD SAML uygulama için çoklu oturum açmayı destekledikleri.</span><span class="sxs-lookup"><span data-stu-id="43579-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="43579-182">RequiredResourceAccess listesinde kaynak yok</span><span class="sxs-lookup"><span data-stu-id="43579-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="43579-183">*Hata AADSTS65005:hello istemci uygulaması erişim tooresource istedi ' 00000002-0000-0000-c000-000000000000'. Merhaba istemci kendi requiredResourceAccess listesinde bu kaynak belirtilmedi bu isteği başarısız oldu*.</span><span class="sxs-lookup"><span data-stu-id="43579-183">*Error AADSTS65005:hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="43579-184">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="43579-184">**Possible cause**</span></span>

<span data-ttu-id="43579-185">Merhaba uygulama nesnesi bozuk.</span><span class="sxs-lookup"><span data-stu-id="43579-185">hello application object is corrupted.</span></span>

<span data-ttu-id="43579-186">**Çözüm: seçeneği 1**</span><span class="sxs-lookup"><span data-stu-id="43579-186">**Resolution: option 1**</span></span>

<span data-ttu-id="43579-187">toosolve hello sorun hello Azure AD yapılandırmasında hello benzersiz tanımlayıcısı değeri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="43579-187">toosolve hello problem, add hello unique Identifier value in hello Azure AD configuration.</span></span> <span data-ttu-id="43579-188">tooadd tanımlayıcı değeri hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="43579-188">tooadd a Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="43579-189">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="43579-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="43579-190">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="43579-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43579-191">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="43579-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43579-192">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43579-193">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="43579-194">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="43579-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="43579-195">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="43579-195">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="43579-196">Merhaba uygulamanın yüklediği sonra hello üzerinde tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde</span><span class="sxs-lookup"><span data-stu-id="43579-196">Once hello application loads, click on hello **Single sign-on** from hello application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="43579-197">Merhaba altında **etki alanı ve URL** bölümünde, denetleme üzerinde hello **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="43579-197">Under hello **Domain and URL** section, check on hello **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="43579-198">Merhaba, **tanımlayıcısı** metin hello uygulama için benzersiz bir tanımlayıcı yazın.</span><span class="sxs-lookup"><span data-stu-id="43579-198">in hello **Identifier** textbox type a unique identifier for hello application.</span></span>

10. <span data-ttu-id="43579-199">**Kaydet** hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="43579-199">**Save** hello configuration.</span></span>


<span data-ttu-id="43579-200">**Çözüm seçeneği 2**</span><span class="sxs-lookup"><span data-stu-id="43579-200">**Resolution option 2**</span></span>

<span data-ttu-id="43579-201">Seçenek 1 yukarıda sizin için olmadıysa Merhaba uygulaması hello dizininden kaldırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="43579-201">If option 1 above did not work for you, try removing hello application from hello directory.</span></span> <span data-ttu-id="43579-202">Ardından, ekleyin ve hello uygulamayı yeniden yapılandırmak, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="43579-202">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="43579-203">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="43579-203">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="43579-204">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="43579-204">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43579-205">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="43579-205">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43579-206">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-206">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43579-207">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-207">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="43579-208">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="43579-208">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="43579-209">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="43579-209">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="43579-210">Tıklatın **silmek** hello sol üst hello uygulamasının adresindeki **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="43579-210">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="43579-211">Azure AD yenileyin ve hello Azure AD Galerisi'nden hello uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="43579-211">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="43579-212">Ardından, Merhaba uygulaması yapılandırın</span><span class="sxs-lookup"><span data-stu-id="43579-212">Then, Configure hello application</span></span>

<span data-ttu-id="43579-213"><span id="_Hlk477190176" class="anchor"></span>Merhaba uygulaması yeniden yapılandırmadan sonra toohello uygulamada mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43579-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="43579-214">Sertifika veya anahtar yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="43579-214">Certificate or key not configured</span></span>

<span data-ttu-id="43579-215">*Hata AADSTS50003: yapılandırılmış hiçbir imzalama anahtarı.*</span><span class="sxs-lookup"><span data-stu-id="43579-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="43579-216">**Olası neden**</span><span class="sxs-lookup"><span data-stu-id="43579-216">**Possible cause**</span></span>

<span data-ttu-id="43579-217">Merhaba uygulama nesnesi bozuk ve Azure AD hello uygulama için yapılandırılan hello sertifika tanımıyor.</span><span class="sxs-lookup"><span data-stu-id="43579-217">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="43579-218">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="43579-218">**Resolution**</span></span>

<span data-ttu-id="43579-219">toodelete ve yeni bir sertifika oluşturmak, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="43579-219">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="43579-220">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="43579-220">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="43579-221">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="43579-221">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43579-222">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="43579-222">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43579-223">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-223">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43579-224">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="43579-224">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="43579-225">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="43579-225">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="43579-226">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="43579-226">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="43579-227">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="43579-227">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43579-228">tıklatın **yeni sertifika oluştur** hello altında **imzalama sertifikası SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="43579-228">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="43579-229">Sona erme tarihini seçin.</span><span class="sxs-lookup"><span data-stu-id="43579-229">Select Expiration date.</span></span> <span data-ttu-id="43579-230">Ardından **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="43579-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="43579-231">Denetleme **yeni sertifika etkin hale getirin** toooverride hello active sertifika.</span><span class="sxs-lookup"><span data-stu-id="43579-231">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="43579-232">Ardından **kaydetmek** hello dikey penceresinde hello üstündeki ve tooactivate hello geçiş sertifikası kabul edin.</span><span class="sxs-lookup"><span data-stu-id="43579-232">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="43579-233">Merhaba altında **SAML imzalama sertifikası** 'yi tıklatın **kaldırmak** tooremove hello **kullanılmayan** sertifika.</span><span class="sxs-lookup"><span data-stu-id="43579-233">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="43579-234">Merhaba SAML talep özelleştirirken sorun tooan uygulama gönderilen</span><span class="sxs-lookup"><span data-stu-id="43579-234">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="43579-235">toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="43579-235">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43579-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43579-236">Next steps</span></span>
[<span data-ttu-id="43579-237">Nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure AD'de</span><span class="sxs-lookup"><span data-stu-id="43579-237">How toodebug SAML-based single sign-on tooapplications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
