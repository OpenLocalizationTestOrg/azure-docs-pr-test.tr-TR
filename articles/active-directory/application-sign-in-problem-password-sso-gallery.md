---
title: "tooan içinde Federasyon için yapılandırılan Azure AD galerisinde uygulamanızı imzalama aaaProblems çoklu oturum açma | Microsoft Docs"
description: "Parola çoklu oturum açma için yapılandırılmış bir Azure AD galeri uygulama tootroubleshoot nasıl sorunlar"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="49c92-103">Tooan Federasyon çoklu oturum açma için yapılandırılmış bir Azure AD galeri uygulama imzalama sorunları</span><span class="sxs-lookup"><span data-stu-id="49c92-103">Problems signing in tooan Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="49c92-104">Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir.</span><span class="sxs-lookup"><span data-stu-id="49c92-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="49c92-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49c92-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="49c92-106">Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="49c92-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="49c92-107">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="49c92-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="49c92-108">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="49c92-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="49c92-109">Merhaba erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="49c92-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="49c92-110">JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="49c92-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="49c92-111">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="49c92-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="49c92-112">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="49c92-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="49c92-113">Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="49c92-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="49c92-114">Internet Explorer 8, 9, 10, 11 - Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="49c92-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="49c92-115">Chrome - Windows 7 ve daha sonra ve MacOS x veya sonrası</span><span class="sxs-lookup"><span data-stu-id="49c92-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="49c92-116">Firefox 26,0 veya daha sonra - Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="49c92-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="49c92-117">tarayıcı uzantıları köşesi desteklendiğinde hale kenar Windows 10 için kullanılabilir hale hello parola tabanlı SSO uzantısı.</span><span class="sxs-lookup"><span data-stu-id="49c92-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="49c92-118">Nasıl tooinstall hello erişim paneli tarayıcı uzantısı</span><span class="sxs-lookup"><span data-stu-id="49c92-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="49c92-119">tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="49c92-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="49c92-120">Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="49c92-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="49c92-121">Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.</span><span class="sxs-lookup"><span data-stu-id="49c92-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="49c92-122">Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="49c92-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="49c92-123">Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="49c92-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="49c92-124">**Ekleme** hello uzantısı tooyour tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="49c92-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="49c92-125">Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="49c92-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="49c92-126">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="49c92-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="49c92-127">Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="49c92-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="49c92-128">Ayrıca hello uzantısı Chrome ve Firefox için hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49c92-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="49c92-129">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="49c92-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="49c92-130">Firefox erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="49c92-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="49c92-131">Internet Explorer için Grup İlkesi ayarı</span><span class="sxs-lookup"><span data-stu-id="49c92-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="49c92-132">Kullanıcılarınızın makinelerde Internet Explorer için tooremotely yükleme hello erişim paneli uzantısına izin ver Grup İlkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49c92-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="49c92-133">Merhaba Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="49c92-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="49c92-134">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.</span><span class="sxs-lookup"><span data-stu-id="49c92-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="49c92-135">Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="49c92-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="49c92-136">Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="49c92-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="49c92-137">[Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="49c92-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="49c92-138">Merhaba öğreticisini izleyin [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) ilişkin adım adım yönergeler nasıl tooconfigure hello Grup İlkesi ve toousers dağıtın.</span><span class="sxs-lookup"><span data-stu-id="49c92-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="49c92-139">Merhaba erişim paneli Internet Explorer'da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="49c92-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="49c92-140">Merhaba izleyin [sorun giderme hello Internet Explorer için erişim paneli uzantısı](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) hello uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="49c92-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="49c92-141">Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması</span><span class="sxs-lookup"><span data-stu-id="49c92-141">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="49c92-142">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="49c92-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="49c92-143">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="49c92-143">Add an application from hello Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="49c92-144">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49c92-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="49c92-145">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="49c92-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="49c92-146">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="49c92-146">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="49c92-147">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="49c92-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="49c92-148">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="49c92-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="49c92-149">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="49c92-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49c92-150">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49c92-151">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="49c92-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="49c92-152">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="49c92-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="49c92-153">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="49c92-153">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="49c92-154">Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="49c92-154">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="49c92-155">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="49c92-155">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="49c92-156">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="49c92-156">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="49c92-157">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="49c92-157">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="49c92-158">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49c92-158">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="49c92-159">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="49c92-159">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="49c92-160">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="49c92-160">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="49c92-161">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="49c92-161">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49c92-162">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-162">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49c92-163">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="49c92-163">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="49c92-164">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-164">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="49c92-165">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="49c92-165">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="49c92-166">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="49c92-166">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="49c92-167">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="49c92-167">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="49c92-168">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="49c92-168">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="49c92-169">[Kullanıcıların toohello uygulama atama](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="49c92-169">[Assign users toohello application](#_How_to_assign).</span></span>

10. <span data-ttu-id="49c92-170">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="49c92-170">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="49c92-171">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="49c92-171">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="49c92-172">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="49c92-172">Assign users toohello application</span></span>

<span data-ttu-id="49c92-173">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="49c92-173">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="49c92-174">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="49c92-174">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49c92-175">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="49c92-175">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49c92-176">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-176">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49c92-177">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="49c92-177">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="49c92-178">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-178">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="49c92-179">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="49c92-179">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="49c92-180">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="49c92-180">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="49c92-181">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="49c92-181">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="49c92-182">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="49c92-182">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="49c92-183">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="49c92-183">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="49c92-184">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="49c92-184">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="49c92-185">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="49c92-185">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="49c92-186">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-186">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="49c92-187">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="49c92-187">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="49c92-188">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="49c92-188">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="49c92-189">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="49c92-189">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="49c92-190">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="49c92-190">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="49c92-191">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="49c92-191">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a><span data-ttu-id="49c92-192">Bu sorun giderme, adımları hello sorunu çözümlemek yok</span><span class="sxs-lookup"><span data-stu-id="49c92-192">If these troubleshoot steps don't resolve hello issue</span></span> 
<span data-ttu-id="49c92-193">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="49c92-193">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="49c92-194">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="49c92-194">Correlation error ID</span></span>

-   <span data-ttu-id="49c92-195">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="49c92-195">UPN (user email address)</span></span>

-   <span data-ttu-id="49c92-196">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="49c92-196">TenantID</span></span>

-   <span data-ttu-id="49c92-197">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="49c92-197">Browser type</span></span>

-   <span data-ttu-id="49c92-198">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="49c92-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="49c92-199">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="49c92-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="49c92-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49c92-200">Next steps</span></span>
[<span data-ttu-id="49c92-201">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="49c92-201">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
