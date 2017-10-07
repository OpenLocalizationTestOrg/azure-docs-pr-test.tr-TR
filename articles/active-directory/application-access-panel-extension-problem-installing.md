---
title: "Merhaba uygulama erişim paneli tarayıcı uzantısı yükleme aaaProblem | Microsoft Docs"
description: "Hello erişim paneli tarayıcı uzantısı yüklerken toofix sık karşılaşılan hataların nasıl karşılaştı"
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
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a><span data-ttu-id="816f0-103">Merhaba uygulama erişim paneli tarayıcı uzantısı yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="816f0-103">Problem installing hello application access panel browser extension</span></span>

<span data-ttu-id="816f0-104">Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir.</span><span class="sxs-lookup"><span data-stu-id="816f0-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="816f0-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="816f0-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="816f0-106">Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="816f0-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="816f0-107">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="816f0-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="816f0-108">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="816f0-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="816f0-109">Merhaba erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="816f0-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="816f0-110">JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="816f0-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="816f0-111">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="816f0-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="816f0-112">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="816f0-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="816f0-113">Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="816f0-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="816f0-114">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="816f0-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="816f0-115">Edge Windows 10 Anniversary Edition veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="816f0-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="816f0-116">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="816f0-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="816f0-117">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="816f0-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="816f0-118">Nasıl tooinstall hello erişim paneli tarayıcı uzantısı</span><span class="sxs-lookup"><span data-stu-id="816f0-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="816f0-119">tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="816f0-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="816f0-120">Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="816f0-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="816f0-121">Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.</span><span class="sxs-lookup"><span data-stu-id="816f0-121">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="816f0-122">Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="816f0-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="816f0-123">Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="816f0-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="816f0-124">**Ekleme** hello uzantısı tooyour tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="816f0-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="816f0-125">Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="816f0-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="816f0-126">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="816f0-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="816f0-127">Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="816f0-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="816f0-128">Ayrıca hello uzantısı Chrome ve kenar hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="816f0-128">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="816f0-129">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="816f0-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="816f0-130">Edge erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="816f0-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="816f0-131">Internet Explorer için Grup İlkesi ayarı</span><span class="sxs-lookup"><span data-stu-id="816f0-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="816f0-132">Kullanıcılarınızın makinelerde Internet Explorer için tooremotely yükleme hello erişim paneli uzantısına izin ver Grup İlkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="816f0-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="816f0-133">Merhaba Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="816f0-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="816f0-134">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.</span><span class="sxs-lookup"><span data-stu-id="816f0-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="816f0-135">Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="816f0-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="816f0-136">Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="816f0-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="816f0-137">[Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="816f0-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="816f0-138">Merhaba öğreticisini izleyin [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](active-directory-saas-ie-group-policy.md) ilişkin adım adım yönergeler nasıl tooconfigure hello Grup İlkesi ve toousers dağıtın.</span><span class="sxs-lookup"><span data-stu-id="816f0-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="816f0-139">Merhaba erişim paneli Internet Explorer'da sorun giderme</span><span class="sxs-lookup"><span data-stu-id="816f0-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="816f0-140">Merhaba izleyin [sorun giderme hello Internet Explorer için erişim paneli uzantısı](active-directory-saas-ie-troubleshooting.md) hello uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="816f0-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="816f0-141">Bu sorun giderme adımları hello sorunu çözmezse</span><span class="sxs-lookup"><span data-stu-id="816f0-141">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="816f0-142">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="816f0-142">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="816f0-143">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="816f0-143">Correlation error ID</span></span>

-   <span data-ttu-id="816f0-144">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="816f0-144">UPN (user email address)</span></span>

-   <span data-ttu-id="816f0-145">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="816f0-145">TenantID</span></span>

-   <span data-ttu-id="816f0-146">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="816f0-146">Browser type</span></span>

-   <span data-ttu-id="816f0-147">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="816f0-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="816f0-148">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="816f0-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="816f0-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="816f0-149">Next steps</span></span>
[<span data-ttu-id="816f0-150">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="816f0-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
