---
title: "oturum açtıktan sonra bir uygulamanın sayfasında aaaError | Microsoft Docs"
description: "Bir hata Hello uygulama kendisini yayar zaman nasıl tooresolve sorunları Azure AD ile oturum açın"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="d2ffc-103">Oturum açtıktan sonra bir uygulamanın sayfada hata</span><span class="sxs-lookup"><span data-stu-id="d2ffc-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="d2ffc-104">Bu senaryoda, Azure AD hello kullanıcı oturumu, ancak Merhaba uygulaması hello kullanıcı toosuccessfully bitiş hello oturum akışı sağlanmıyor hata görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="d2ffc-105">Bu senaryoda, Merhaba uygulaması hello yanıt sorunu Azure AD tarafından kabul etmiyor.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="d2ffc-106">Merhaba uygulaması Azure AD'den hello yanıt neden kabul etmediğiniz bazı olası nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="d2ffc-107">Merhaba uygulamasında Hello hatası yeterince Temizle tooknow değilse ne sonra hello yanıtta eksik:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="d2ffc-108">Merhaba uygulaması hello Azure AD Galerisi, hello makaledeki tüm hello adımları takip doğrulayıp [nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="d2ffc-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="d2ffc-109">Gibi bir araç kullanın [Fiddler](http://www.telerik.com/fiddler) toocapture SAML istek, SAML yanıtını ve SAML belirteci.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="d2ffc-110">Merhaba SAML yanıtını, eksik olana hello uygulama satıcı tooknow ile paylaşır.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="d2ffc-111">Merhaba SAML yanıtını eksik öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="d2ffc-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="d2ffc-112">tooadd hello Azure AD yapılandırma toobe hello Azure AD yanıt olarak gönderilen bir öznitelikte hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2ffc-113">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d2ffc-114">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2ffc-115">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2ffc-116">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2ffc-117">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d2ffc-118">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2ffc-119">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d2ffc-120">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2ffc-121">tıklatın **görüntüleme ve düzenleme diğer tüm kullanıcı özniteliklerini altında** hello **kullanıcı öznitelikleri** bölüm tooedit hello kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d2ffc-122">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="d2ffc-123">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-123">click **Add attribute**.</span></span> <span data-ttu-id="d2ffc-124">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="d2ffc-125">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-125">Click **Save.**</span></span> <span data-ttu-id="d2ffc-126">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="d2ffc-127">Merhaba yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-127">Save hello configuration.</span></span>

<span data-ttu-id="d2ffc-128">Bir sonraki defa Hello toohello uygulamada oturum açtığında Azure AD hello yeni öznitelik hello SAML yanıtını gönderir.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="d2ffc-129">Merhaba uygulaması farklı kullanıcı tanımlayıcısı value veya format bekliyor</span><span class="sxs-lookup"><span data-stu-id="d2ffc-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="d2ffc-130">Merhaba oturum açma toohello uygulama hello SAML yanıtını rolleri gibi öznitelikleri eksik veya Merhaba uygulaması hello Entityıd özniteliği için farklı bir biçim bekleniyordu nedeniyle başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="d2ffc-131">Bir öznitelik hello Azure AD uygulama yapılandırmasında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="d2ffc-132">toochange hello kullanıcı tanımlayıcısı değeri hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2ffc-133">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d2ffc-134">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2ffc-135">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2ffc-136">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2ffc-137">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d2ffc-138">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2ffc-139">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d2ffc-140">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2ffc-141">Merhaba altında **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="d2ffc-142">Entityıd (kullanıcı tanımlayıcısı) biçimini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d2ffc-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="d2ffc-143">Merhaba uygulaması hello Entityıd özniteliği için başka bir biçime görüyorsa.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="d2ffc-144">Ardından, Azure AD hello yanıtta toohello uygulama kullanıcı kimlik doğrulamasından sonra gönderir mümkün tooselect hello Entityıd (kullanıcı tanımlayıcısı) biçimi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="d2ffc-145">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="d2ffc-146">Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="d2ffc-147">Merhaba uygulaması farklı imza yöntemi hello SAML yanıtını için bekliyor</span><span class="sxs-lookup"><span data-stu-id="d2ffc-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="d2ffc-148">Merhaba SAML belirtecine hangi kısımlarının Azure Active Directory tarafından dijital olarak imzalanmış toochange.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="d2ffc-149">Merhaba adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="d2ffc-150">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d2ffc-151">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2ffc-152">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2ffc-153">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2ffc-154">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d2ffc-155">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2ffc-156">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d2ffc-157">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2ffc-158">tıklatın **Göster gelişmiş sertifika imzalama ayarları** hello altında **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="d2ffc-159">Select hello uygun **imzalama seçeneği** hello uygulama tarafından beklenen:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="d2ffc-160">Oturum SAML yanıtını</span><span class="sxs-lookup"><span data-stu-id="d2ffc-160">Sign SAML response</span></span>

  * <span data-ttu-id="d2ffc-161">Oturum açma SAML yanıtını ve onaylama</span><span class="sxs-lookup"><span data-stu-id="d2ffc-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="d2ffc-162">Oturum SAML onayı</span><span class="sxs-lookup"><span data-stu-id="d2ffc-162">Sign SAML assertion</span></span>

<span data-ttu-id="d2ffc-163">Bir sonraki defa Hello toohello uygulamada oturum açtığında, Azure AD oturum seçili hello SAML yanıtını parçası hello.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="d2ffc-164">Merhaba uygulaması algoritması toobe SHA-1 imzalama hello bekliyor</span><span class="sxs-lookup"><span data-stu-id="d2ffc-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="d2ffc-165">Varsayılan olarak, Azure AD çoğu güvenlik algoritması hello kullanarak hello SAML belirteci imzalar.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="d2ffc-166">Merhaba oturum algoritma tooSHA-1 değiştirme hello uygulama tarafından gerekli kılınmadıkça hiçbir önerilmez.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="d2ffc-167">toochange imzalama algoritmasını Merhaba, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2ffc-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2ffc-168">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d2ffc-169">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2ffc-170">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2ffc-171">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2ffc-172">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d2ffc-173">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2ffc-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2ffc-174">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d2ffc-175">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2ffc-176">tıklatın **Göster gelişmiş sertifika imzalama ayarları** hello altında **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="d2ffc-177">SHA-1, hello seçin **imzalama algoritması**.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="d2ffc-178">Sonraki kullanıcı işaretlerini toohello uygulamada Merhaba, SAML belirteci SHA-1 algoritmasını kullanarak Azure AD oturum hello.</span><span class="sxs-lookup"><span data-stu-id="d2ffc-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2ffc-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2ffc-179">Next steps</span></span>
[<span data-ttu-id="d2ffc-180">Nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de</span><span class="sxs-lookup"><span data-stu-id="d2ffc-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
