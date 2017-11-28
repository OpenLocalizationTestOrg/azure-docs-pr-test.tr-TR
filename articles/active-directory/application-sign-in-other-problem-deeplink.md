---
title: "bir ayrıntılı bağlantı kullanarak tooan uygulamada imzalama aaaProblems | Microsoft Docs"
description: "Nasıl bir uygulamaya Azure AD kullanarak bir ayrıntılı bağlantı URL'den erişmeyi tootroubleshoot sorunları"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="616c6-103">Bir ayrıntılı bağlantı kullanarak tooan uygulamada oturum sorunları</span><span class="sxs-lookup"><span data-stu-id="616c6-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="616c6-104">Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni.</span><span class="sxs-lookup"><span data-stu-id="616c6-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="616c6-105">Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="616c6-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="616c6-106">Merhaba uygulaması düzgün şekilde yapılandırılmalıdır ve atanan toohello kullanıcı veya grup hello kullanıcı toosee hello hello erişim paneli uygulamada üyesidir.</span><span class="sxs-lookup"><span data-stu-id="616c6-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="616c6-107">Ayrıntılı bağlantılar veya kullanıcı erişimi URL'leri kullanıcılarınızın parola SSO uygulamalarını doğrudan kendi tarayıcılar URL'den çubuklarını tooaccess kullanabilir bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="616c6-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="616c6-108">Toothis bağlantı giderek kullanıcıların olması otomatik olarak toogo toohello erişim paneli ilk gerek kalmadan hello uygulamaya imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="616c6-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="616c6-109">Merhaba budur aynı bağlantı kullanıcılar bu uygulamalardan hello Office 365 uygulama Başlatıcı tooaccess kullanın.</span><span class="sxs-lookup"><span data-stu-id="616c6-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="616c6-110">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="616c6-110">General issues toocheck first</span></span>

-   <span data-ttu-id="616c6-111">Kullanarak emin bir **tarayıcı** hello hello erişim paneli için minimum gereksinimleri karşılayan.</span><span class="sxs-lookup"><span data-stu-id="616c6-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="616c6-112">Merhaba kullanıcının tarayıcısının hello uygulama tooits hello URL'sini ekledi emin olun **Güvenilen siteler**.</span><span class="sxs-lookup"><span data-stu-id="616c6-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="616c6-113">Toocheck Merhaba uygulaması olduğundan emin olun **yapılandırılmış** doğru.</span><span class="sxs-lookup"><span data-stu-id="616c6-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="616c6-114">Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.</span><span class="sxs-lookup"><span data-stu-id="616c6-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="616c6-115">Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**</span><span class="sxs-lookup"><span data-stu-id="616c6-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="616c6-116">Emin hello kullanıcının olun **parola süresi değil veya unutulursa.**</span><span class="sxs-lookup"><span data-stu-id="616c6-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="616c6-117">Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="616c6-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="616c6-118">Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="616c6-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="616c6-119">Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu.</span><span class="sxs-lookup"><span data-stu-id="616c6-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="616c6-120">Tarayıcınızın tanımlama bilgilerini temizleyip ve toosign olarak yeniden deneniyor yapma emin tooalso deneyin.</span><span class="sxs-lookup"><span data-stu-id="616c6-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="616c6-121">Merhaba ayrıntılı bağlantı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="616c6-121">Checking hello deeplink</span></span>

<span data-ttu-id="616c6-122">Merhaba doğru ayrıntılı bağlantı varsa toocheck hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-123">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="616c6-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="616c6-124">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="616c6-125">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="616c6-126">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="616c6-127">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="616c6-128">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="616c6-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="616c6-129">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="616c6-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="616c6-130">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="616c6-131">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="616c6-132">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="616c6-133">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="616c6-134">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="616c6-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="616c6-135">Merhaba onay hello için ayrıntılı bağlantı hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="616c6-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="616c6-136">Merhaba etiketi bulmak **kullanıcı erişim URL'si**.</span><span class="sxs-lookup"><span data-stu-id="616c6-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="616c6-137">Bu URL, ayrıntılı bağlantı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="616c6-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="616c6-138">Nasıl tooinstall hello erişim paneli tarayıcı uzantısı</span><span class="sxs-lookup"><span data-stu-id="616c6-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="616c6-139">tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-140">Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="616c6-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="616c6-141">Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.</span><span class="sxs-lookup"><span data-stu-id="616c6-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="616c6-142">Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="616c6-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="616c6-143">Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="616c6-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="616c6-144">**Ekleme** hello uzantısı tooyour tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="616c6-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="616c6-145">Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="616c6-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="616c6-146">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="616c6-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="616c6-147">Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="616c6-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="616c6-148">Ayrıca hello uzantısı Chrome ve Firefox için hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="616c6-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="616c6-149">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="616c6-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="616c6-150">Firefox erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="616c6-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="616c6-151">Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması</span><span class="sxs-lookup"><span data-stu-id="616c6-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="616c6-152">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="616c6-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="616c6-153">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="616c6-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="616c6-154">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="616c6-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="616c6-155">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="616c6-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="616c6-156">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-157">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**.</span><span class="sxs-lookup"><span data-stu-id="616c6-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="616c6-158">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="616c6-159">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="616c6-160">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="616c6-161">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="616c6-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="616c6-162">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="616c6-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="616c6-163">Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="616c6-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="616c6-164">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="616c6-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="616c6-165">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="616c6-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="616c6-166">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="616c6-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="616c6-167">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="616c6-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="616c6-168">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-169">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="616c6-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="616c6-170">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="616c6-171">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="616c6-172">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="616c6-173">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="616c6-174">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="616c6-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="616c6-175">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="616c6-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="616c6-176">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="616c6-177">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="616c6-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="616c6-178">[Kullanıcıların toohello uygulama atama](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="616c6-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="616c6-179">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="616c6-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="616c6-180">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="616c6-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="616c6-181">Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma</span><span class="sxs-lookup"><span data-stu-id="616c6-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="616c6-182">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="616c6-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="616c6-183">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="616c6-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="616c6-184">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="616c6-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="616c6-185">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="616c6-185">Add a non-gallery application</span></span>

<span data-ttu-id="616c6-186">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-187">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**.</span><span class="sxs-lookup"><span data-stu-id="616c6-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="616c6-188">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="616c6-189">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="616c6-190">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="616c6-191">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="616c6-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="616c6-192">tıklatın **olmayan galeri uygulaması.**</span><span class="sxs-lookup"><span data-stu-id="616c6-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="616c6-193">Merhaba, uygulamanızın hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="616c6-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="616c6-194">Seçin **ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="616c6-194">Select **Add.**</span></span>

<span data-ttu-id="616c6-195">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="616c6-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="616c6-196">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="616c6-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="616c6-197">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-198">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="616c6-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="616c6-199">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="616c6-200">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="616c6-201">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="616c6-202">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="616c6-203">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="616c6-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="616c6-204">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="616c6-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="616c6-205">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="616c6-206">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="616c6-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="616c6-207">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="616c6-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="616c6-208">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="616c6-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="616c6-209">Merhaba oturum alanları hello URL'de göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="616c6-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="616c6-210">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="616c6-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="616c6-211">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="616c6-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="616c6-212">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="616c6-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="616c6-213">Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan</span><span class="sxs-lookup"><span data-stu-id="616c6-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="616c6-214">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="616c6-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="616c6-215">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="616c6-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="616c6-216">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="616c6-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="616c6-217">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="616c6-218">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="616c6-219">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="616c6-220">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="616c6-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="616c6-221">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="616c6-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="616c6-222">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="616c6-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="616c6-223">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="616c6-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="616c6-224">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="616c6-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="616c6-225">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="616c6-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="616c6-226">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="616c6-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="616c6-227">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="616c6-228">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="616c6-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="616c6-229">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="616c6-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="616c6-230">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="616c6-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="616c6-231">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="616c6-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="616c6-232">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="616c6-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="616c6-233">Sorun giderme adımları değil hello varsa hello sorunu çözün.</span><span class="sxs-lookup"><span data-stu-id="616c6-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="616c6-234">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="616c6-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="616c6-235">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="616c6-235">Correlation error ID</span></span>

-   <span data-ttu-id="616c6-236">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="616c6-236">UPN (user email address)</span></span>

-   <span data-ttu-id="616c6-237">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="616c6-237">TenantID</span></span>

-   <span data-ttu-id="616c6-238">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="616c6-238">Browser type</span></span>

-   <span data-ttu-id="616c6-239">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="616c6-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="616c6-240">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="616c6-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="616c6-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="616c6-241">Next steps</span></span>
[<span data-ttu-id="616c6-242">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="616c6-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
