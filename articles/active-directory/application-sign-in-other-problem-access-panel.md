---
title: "Merhaba erişim paneli tooan uygulamadan imzalama aaaProblems | Microsoft Docs"
description: "Bir uygulama erişiminde tootroubleshoot sorun myapps.microsoft.com adresindeki Microsoft Azure AD erişim paneli nasıl hello"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="27178-103">Merhaba erişim panelinden tooan uygulamada oturum sorunları</span><span class="sxs-lookup"><span data-stu-id="27178-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="27178-104">Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni.</span><span class="sxs-lookup"><span data-stu-id="27178-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="27178-105">Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="27178-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="27178-106">Merhaba uygulaması düzgün şekilde yapılandırılmalıdır ve atanan toohello kullanıcı veya grup hello kullanıcı toosee hello hello erişim paneli uygulamada üyesidir.</span><span class="sxs-lookup"><span data-stu-id="27178-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="27178-107">bir kullanıcı için görüyor olabilirsiniz uygulamalarının Hello türü kategorileri aşağıdaki hello ayrılır:</span><span class="sxs-lookup"><span data-stu-id="27178-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="27178-108">Office 365 uygulamaları</span><span class="sxs-lookup"><span data-stu-id="27178-108">Office 365 Applications</span></span>

-   <span data-ttu-id="27178-109">Federasyon tabanlı SSO ile yapılandırılan Microsoft ve üçüncü taraf uygulamalar</span><span class="sxs-lookup"><span data-stu-id="27178-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="27178-110">Parola tabanlı SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="27178-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="27178-111">Varolan SSO çözümleriyle uygulamaları</span><span class="sxs-lookup"><span data-stu-id="27178-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="27178-112">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="27178-112">General issues toocheck first</span></span>

-   <span data-ttu-id="27178-113">Kullanarak emin bir **tarayıcı** hello hello erişim paneli için minimum gereksinimleri karşılayan.</span><span class="sxs-lookup"><span data-stu-id="27178-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="27178-114">Merhaba kullanıcının tarayıcısının hello uygulama tooits hello URL'sini ekledi emin olun **Güvenilen siteler**.</span><span class="sxs-lookup"><span data-stu-id="27178-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="27178-115">Toocheck Merhaba uygulaması olduğundan emin olun **yapılandırılmış** doğru.</span><span class="sxs-lookup"><span data-stu-id="27178-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="27178-116">Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.</span><span class="sxs-lookup"><span data-stu-id="27178-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="27178-117">Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**</span><span class="sxs-lookup"><span data-stu-id="27178-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="27178-118">Emin hello kullanıcının olun **parola süresi değil veya unutulursa.**</span><span class="sxs-lookup"><span data-stu-id="27178-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="27178-119">Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="27178-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="27178-120">Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="27178-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="27178-121">Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu.</span><span class="sxs-lookup"><span data-stu-id="27178-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="27178-122">Tarayıcınızın tanımlama bilgilerini temizleyip ve toosign olarak yeniden deneniyor yapma emin tooalso deneyin.</span><span class="sxs-lookup"><span data-stu-id="27178-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="27178-123">Merhaba erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="27178-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="27178-124">JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="27178-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="27178-125">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="27178-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="27178-126">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="27178-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="27178-127">Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="27178-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="27178-128">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="27178-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="27178-129">Edge Windows 10 Anniversary Edition veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="27178-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="27178-130">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="27178-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="27178-131">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="27178-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="27178-132">Nasıl tooinstall hello erişim paneli tarayıcı uzantısı</span><span class="sxs-lookup"><span data-stu-id="27178-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="27178-133">tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-134">Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="27178-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="27178-135">Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.</span><span class="sxs-lookup"><span data-stu-id="27178-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="27178-136">Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="27178-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="27178-137">Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="27178-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="27178-138">**Ekleme** hello uzantısı tooyour tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="27178-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="27178-139">Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="27178-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="27178-140">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="27178-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="27178-141">Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="27178-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="27178-142">Ayrıca hello uzantısı Chrome ve kenar hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="27178-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="27178-143">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="27178-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="27178-144">Edge erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="27178-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="27178-145">Azure AD galeri uygulaması için çoklu oturum açmayı tooconfigure nasıl Federasyon</span><span class="sxs-lookup"><span data-stu-id="27178-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="27178-146">Kurumsal çoklu oturum açma özelliğine sahip etkin hello Azure AD galerisinde tüm uygulama kullanılabilir bir adım adım öğretici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="27178-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="27178-147">Merhaba erişebilirsiniz [nasıl öğreticiler listesi toointegrate SaaS uygulamaları Azure Active Directory ile](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) ayrıntılı adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="27178-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="27178-148">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="27178-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="27178-149">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="27178-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="27178-150">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27178-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="27178-151">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="27178-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="27178-152">Azure AD meta verileri ve sertifika alma</span><span class="sxs-lookup"><span data-stu-id="27178-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="27178-153">Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27178-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="27178-154">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="27178-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="27178-155">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="27178-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="27178-156">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-157">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="27178-158">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-159">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-160">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-161">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="27178-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="27178-162">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="27178-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="27178-163">Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="27178-164">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="27178-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="27178-165">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="27178-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="27178-166">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="27178-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="27178-167">Hello Azure AD Galeriden bir uygulama için çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27178-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="27178-168">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-170">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-171">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-172">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-173">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="27178-174">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-175">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="27178-176">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-177">Seçin **SAML tabanlı oturum açma** hello gelen **modu** açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="27178-178">Merhaba gerekli değerleri girin **etki alanı ve URL'ler.**</span><span class="sxs-lookup"><span data-stu-id="27178-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="27178-179">Bu değerleri hello uygulama satıcısından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27178-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="27178-180">SP tarafından başlatılan SSO'yu olarak tooconfigure Merhaba uygulaması hello oturum URL'yi, gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="27178-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="27178-181">Bazı uygulamalar için hello tanımlayıcısı da gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="27178-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="27178-182">IDP tarafından başlatılan SSO'yu olarak tooconfigure Merhaba uygulaması hello yanıt URL'si gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="27178-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="27178-183">Bazı uygulamalar için hello tanımlayıcısı da gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="27178-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="27178-184">**İsteğe bağlı:** tıklatın **Göster Gelişmiş URL ayarları** toosee hello gerekli olmayan değer istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="27178-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="27178-185">Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="27178-186">**İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="27178-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="27178-187">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="27178-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="27178-188">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="27178-188">click **Add attribute**.</span></span> <span data-ttu-id="27178-189">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="27178-190">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="27178-190">Click **Save.**</span></span> <span data-ttu-id="27178-191">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="27178-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="27178-192">tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="27178-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="27178-193">Ayrıca, hello meta verileri URL'leri ve gerekli sertifika toosetup SSO hello uygulamayla sahiptir.</span><span class="sxs-lookup"><span data-stu-id="27178-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="27178-194">tıklatın **kaydetmek** toosave hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="27178-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="27178-195">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="27178-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="27178-196">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="27178-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="27178-197">tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-198">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-199">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-200">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-201">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-202">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="27178-203">Merhaba uygulaması tooshow burada yedeklemek istediğiniz görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-204">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="27178-205">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-206">Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="27178-207">Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="27178-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="27178-208">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="27178-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="27178-209">Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.</span><span class="sxs-lookup"><span data-stu-id="27178-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="27178-210">tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="27178-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="27178-211">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="27178-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="27178-212">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="27178-212">click **Add attribute**.</span></span> <span data-ttu-id="27178-213">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="27178-214">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="27178-214">Click **Save.**</span></span> <span data-ttu-id="27178-215">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="27178-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="27178-216">Hello Azure AD meta verileri veya sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="27178-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="27178-217">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-218">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-219">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-220">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-221">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-222">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="27178-223">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-224">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="27178-225">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-226">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="27178-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="27178-227">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="27178-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="27178-228">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="27178-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="27178-229">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="27178-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="27178-230">Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon</span><span class="sxs-lookup"><span data-stu-id="27178-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="27178-231">Galeri olmayan uygulama tooconfigure toohave Azure AD premium gerekir ve Merhaba uygulaması SAML 2.0 destekler.</span><span class="sxs-lookup"><span data-stu-id="27178-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="27178-232">Azure AD sürümleri hakkında daha fazla bilgi için ziyaret [Azure AD fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="27178-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="27178-233">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27178-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="27178-234">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="27178-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="27178-235">Azure AD meta verileri ve sertifika alma</span><span class="sxs-lookup"><span data-stu-id="27178-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="27178-236">Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27178-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="27178-237">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27178-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="27178-238">tooconfigure çoklu oturum açma hello Azure AD Galerisi'nde olmayan bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-239">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-240">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-241">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-242">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-243">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="27178-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="27178-244">tıklatın **olmayan galeri uygulama** hello içinde **kendi uygulama Ekle** bölümü</span><span class="sxs-lookup"><span data-stu-id="27178-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="27178-245">Merhaba Merhaba uygulaması hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="27178-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="27178-246">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="27178-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="27178-247">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="27178-248">Seçin **SAML tabanlı oturum açma** hello içinde **modu** açılır</span><span class="sxs-lookup"><span data-stu-id="27178-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="27178-249">Merhaba gerekli değerleri girin **etki alanı ve URL'ler.**</span><span class="sxs-lookup"><span data-stu-id="27178-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="27178-250">Bu değerleri hello uygulama satıcısından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27178-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="27178-251">IDP tarafından başlatılan SSO'yu olarak tooconfigure hello uygulama hello yanıt URL'si ve hello tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="27178-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="27178-252">**İsteğe bağlı:** tooconfigure hello uygulama SP tarafından başlatılan SSO'yu olarak hello oturum URL'yi, gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="27178-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="27178-253">Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="27178-254">**İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="27178-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="27178-255">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="27178-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="27178-256">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="27178-256">click **Add attribute**.</span></span> <span data-ttu-id="27178-257">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="27178-258">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="27178-258">Click **Save.**</span></span> <span data-ttu-id="27178-259">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="27178-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="27178-260">tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="27178-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="27178-261">Ayrıca, Azure AD URL'leri ve hello uygulama için gerekli sertifika sahiptir.</span><span class="sxs-lookup"><span data-stu-id="27178-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="27178-262">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="27178-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="27178-263">tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-264">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-265">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-266">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-267">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-268">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="27178-269">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-270">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="27178-271">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-272">Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="27178-273">Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="27178-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="27178-274">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="27178-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="27178-275">Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.</span><span class="sxs-lookup"><span data-stu-id="27178-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="27178-276">tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="27178-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="27178-277">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="27178-277">tooadd an attribute:</span></span>

   <span data-ttu-id="27178-278">1'ı **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="27178-278">1.click **Add attribute**.</span></span> <span data-ttu-id="27178-279">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="27178-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="27178-280">2 tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="27178-280">2 Click **Save.**</span></span> <span data-ttu-id="27178-281">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="27178-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="27178-282">Hello Azure AD meta verileri veya sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="27178-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="27178-283">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-284">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-285">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-286">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-287">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-288">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="27178-289">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-290">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="27178-291">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-292">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="27178-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="27178-293">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="27178-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="27178-294">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="27178-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="27178-295">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="27178-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="27178-296">Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması</span><span class="sxs-lookup"><span data-stu-id="27178-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="27178-297">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="27178-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="27178-298">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="27178-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="27178-299">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27178-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="27178-300">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="27178-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="27178-301">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-302">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="27178-303">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-304">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-305">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-306">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="27178-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="27178-307">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı</span><span class="sxs-lookup"><span data-stu-id="27178-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="27178-308">Tooconfigure için çoklu oturum açmayı hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="27178-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="27178-309">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="27178-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="27178-310">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="27178-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="27178-311">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="27178-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="27178-312">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27178-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="27178-313">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-314">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-315">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-316">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-317">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-318">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="27178-319">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-320">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="27178-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="27178-321">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-322">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="27178-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="27178-323">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="27178-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="27178-324">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="27178-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="27178-325">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="27178-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="27178-326">Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma</span><span class="sxs-lookup"><span data-stu-id="27178-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="27178-327">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="27178-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="27178-328">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="27178-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="27178-329">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27178-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="27178-330">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="27178-330">Add a non-gallery application</span></span>

<span data-ttu-id="27178-331">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-332">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="27178-333">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-334">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-335">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-336">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="27178-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="27178-337">tıklatın **olmayan galeri uygulaması.**</span><span class="sxs-lookup"><span data-stu-id="27178-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="27178-338">Merhaba, uygulamanızın hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="27178-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="27178-339">Seçin **ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="27178-339">Select **Add.**</span></span>

<span data-ttu-id="27178-340">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="27178-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="27178-341">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27178-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="27178-342">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-343">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="27178-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="27178-344">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-345">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-346">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-347">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="27178-348">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-349">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="27178-350">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-351">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="27178-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="27178-352">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="27178-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="27178-353">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="27178-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="27178-354">Merhaba oturum alanları hello URL'de göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="27178-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="27178-355">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="27178-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="27178-356">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="27178-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="27178-357">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="27178-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="27178-358">Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan</span><span class="sxs-lookup"><span data-stu-id="27178-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="27178-359">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="27178-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="27178-360">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="27178-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="27178-361">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="27178-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="27178-362">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="27178-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="27178-363">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="27178-364">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="27178-365">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="27178-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="27178-366">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="27178-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="27178-367">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="27178-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="27178-368">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="27178-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="27178-369">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="27178-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="27178-370">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="27178-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="27178-371">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="27178-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="27178-372">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="27178-373">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="27178-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="27178-374">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="27178-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="27178-375">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="27178-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="27178-376">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="27178-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="27178-377">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="27178-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="27178-378">Sorun giderme adımları değil hello varsa hello sorunu çözün</span><span class="sxs-lookup"><span data-stu-id="27178-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="27178-379">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="27178-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="27178-380">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="27178-380">Correlation error ID</span></span>

-   <span data-ttu-id="27178-381">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="27178-381">UPN (user email address)</span></span>

-   <span data-ttu-id="27178-382">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="27178-382">TenantID</span></span>

-   <span data-ttu-id="27178-383">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="27178-383">Browser type</span></span>

-   <span data-ttu-id="27178-384">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="27178-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="27178-385">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="27178-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="27178-386">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27178-386">Next steps</span></span>
[<span data-ttu-id="27178-387">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="27178-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

