---
title: "Azure AD galeri uygulama parolasını yapılandırılmış tooan imzalama aaaProblems çoklu oturum açma | Microsoft Docs"
description: "Kılavuzu tootroubleshoot tooAzure içinde ilgili toosigning parola çoklu oturum açma için yapılandırılmış AD galeri uygulamaları sorunları sağlamak sorunlu alanları açıklanır"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="ac6af-103">Tooan parola çoklu oturum açma için yapılandırılmış bir Azure AD galeri uygulama imzalama sorunları</span><span class="sxs-lookup"><span data-stu-id="ac6af-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="ac6af-104">Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="ac6af-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac6af-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="ac6af-106">Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ac6af-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="ac6af-107">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="ac6af-108">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="ac6af-109">Merhaba erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="ac6af-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="ac6af-110">JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="ac6af-111">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="ac6af-112">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="ac6af-113">Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="ac6af-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="ac6af-114">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="ac6af-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="ac6af-115">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="ac6af-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="ac6af-116">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="ac6af-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="ac6af-117">tarayıcı uzantıları köşesi desteklendiğinde hale kenar Windows 10 için kullanılabilir hale hello parola tabanlı SSO uzantısı.</span><span class="sxs-lookup"><span data-stu-id="ac6af-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="ac6af-118">Nasıl tooinstall hello erişim paneli tarayıcı uzantısı</span><span class="sxs-lookup"><span data-stu-id="ac6af-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="ac6af-119">tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ac6af-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="ac6af-120">Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="ac6af-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="ac6af-121">Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.</span><span class="sxs-lookup"><span data-stu-id="ac6af-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="ac6af-122">Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="ac6af-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="ac6af-123">Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="ac6af-124">**Ekleme** hello uzantısı tooyour tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="ac6af-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="ac6af-125">Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="ac6af-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="ac6af-126">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="ac6af-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="ac6af-127">Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ac6af-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="ac6af-128">Ayrıca hello uzantısı Chrome ve Firefox için hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ac6af-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="ac6af-129">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="ac6af-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="ac6af-130">Firefox erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="ac6af-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="ac6af-131">Internet Explorer için Grup İlkesi ayarı</span><span class="sxs-lookup"><span data-stu-id="ac6af-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="ac6af-132">Kullanıcılarınızın makinelerde Internet Explorer için tooremotely yükleme hello erişim paneli uzantısına izin ver Grup İlkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac6af-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="ac6af-133">Merhaba Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ac6af-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="ac6af-134">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.</span><span class="sxs-lookup"><span data-stu-id="ac6af-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="ac6af-135">Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="ac6af-136">Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="ac6af-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="ac6af-137">[Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac6af-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="ac6af-138">Merhaba öğreticisini izleyin [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) ilişkin adım adım yönergeler nasıl tooconfigure hello Grup İlkesi ve toousers dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ac6af-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="ac6af-139">Merhaba erişim paneli Internet Explorer'da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ac6af-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="ac6af-140">Merhaba izleyin [sorun giderme hello Internet Explorer için erişim paneli uzantısı](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) hello uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="ac6af-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ac6af-141">Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma</span><span class="sxs-lookup"><span data-stu-id="ac6af-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ac6af-142">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac6af-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ac6af-143">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="ac6af-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="ac6af-144">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac6af-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="ac6af-145">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="ac6af-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="ac6af-146">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="ac6af-146">Add a non-gallery application</span></span>

<span data-ttu-id="ac6af-147">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ac6af-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ac6af-148">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="ac6af-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ac6af-149">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ac6af-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ac6af-150">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ac6af-151">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ac6af-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ac6af-152">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="ac6af-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ac6af-153">tıklatın **olmayan galeri uygulaması.**</span><span class="sxs-lookup"><span data-stu-id="ac6af-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="ac6af-154">Merhaba, uygulamanızın hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ac6af-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="ac6af-155">Seçin **ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="ac6af-155">Select **Add.**</span></span>

<span data-ttu-id="ac6af-156">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ac6af-157">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac6af-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ac6af-158">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ac6af-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ac6af-159">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="ac6af-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ac6af-160">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ac6af-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ac6af-161">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ac6af-162">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ac6af-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ac6af-163">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ac6af-164">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="ac6af-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ac6af-165">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="ac6af-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="ac6af-166">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ac6af-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ac6af-167">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="ac6af-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ac6af-168">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="ac6af-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="ac6af-169">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="ac6af-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="ac6af-170">Merhaba oturum alanları hello URL'de göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ac6af-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="ac6af-171">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="ac6af-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="ac6af-172">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="ac6af-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ac6af-173">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="ac6af-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="ac6af-174">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="ac6af-174">Assign users toohello application</span></span>

<span data-ttu-id="ac6af-175">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ac6af-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ac6af-176">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="ac6af-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ac6af-177">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ac6af-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ac6af-178">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ac6af-179">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ac6af-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ac6af-180">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ac6af-181">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="ac6af-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ac6af-182">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="ac6af-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ac6af-183">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ac6af-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ac6af-184">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="ac6af-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ac6af-185">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="ac6af-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ac6af-186">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="ac6af-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ac6af-187">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="ac6af-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ac6af-188">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ac6af-189">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="ac6af-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="ac6af-190">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="ac6af-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ac6af-191">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="ac6af-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="ac6af-192">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="ac6af-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="ac6af-193">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="ac6af-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="ac6af-194">Sorun giderme adımları değil hello varsa hello sorunu çözün</span><span class="sxs-lookup"><span data-stu-id="ac6af-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="ac6af-195">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="ac6af-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="ac6af-196">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="ac6af-196">Correlation error ID</span></span>

-   <span data-ttu-id="ac6af-197">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="ac6af-197">UPN (user email address)</span></span>

-   <span data-ttu-id="ac6af-198">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="ac6af-198">TenantID</span></span>

-   <span data-ttu-id="ac6af-199">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="ac6af-199">Browser type</span></span>

-   <span data-ttu-id="ac6af-200">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="ac6af-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="ac6af-201">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="ac6af-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac6af-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac6af-202">Next steps</span></span>
[<span data-ttu-id="ac6af-203">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="ac6af-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

