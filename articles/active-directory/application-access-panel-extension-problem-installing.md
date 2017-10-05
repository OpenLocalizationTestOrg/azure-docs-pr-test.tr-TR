---
title: "Uygulama erişimi yükleme sorunu panel tarayıcı uzantısı | Microsoft Docs"
description: "Erişim paneli tarayıcı uzantısı yüklenirken karşılaşılan yaygın hataları gidermek nasıl"
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
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="b06de-103">Uygulama erişimi yükleme sorun tarayıcı uzantısı paneli</span><span class="sxs-lookup"><span data-stu-id="b06de-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="b06de-104">Erişim paneli, Azure AD Yöneticisi erişim verildi görünümü ve başlatma bulut tabanlı uygulamalar Azure Active Directory (Azure AD) bir iş veya Okul hesabı olan bir kullanıcının sağlayan bir web tabanlı portal olmaktır.</span><span class="sxs-lookup"><span data-stu-id="b06de-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="b06de-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b06de-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="b06de-106">Erişim paneli Azure Portalı'ndan ayrıdır ve kullanıcıların bir Azure aboneliğine sahip olmasını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="b06de-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="b06de-107">Parola tabanlı çoklu oturum açma (SSO) erişimi Masası'nda kullanmak için erişim paneli uzantısı kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b06de-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="b06de-108">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b06de-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="b06de-109">Erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="b06de-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="b06de-110">Erişim paneli JavaScript destekleyen bir tarayıcı gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="b06de-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="b06de-111">Parola tabanlı çoklu oturum açma (SSO) erişimi Masası'nda kullanmak için erişim paneli uzantısı kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b06de-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="b06de-112">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b06de-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="b06de-113">Parola tabanlı, SSO için son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="b06de-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="b06de-114">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="b06de-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="b06de-115">Edge Windows 10 Anniversary Edition veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="b06de-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="b06de-116">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="b06de-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="b06de-117">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="b06de-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="b06de-118">Erişim paneli tarayıcı uzantısı yükleme</span><span class="sxs-lookup"><span data-stu-id="b06de-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="b06de-119">Erişim paneli tarayıcı uzantısı yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b06de-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="b06de-120">Açık [erişim paneli](https://myapps.microsoft.com) olarak oturum açın ve desteklenen tarayıcılar birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="b06de-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="b06de-121">tıklatın bir **parola SSO uygulaması** erişim panelinde.</span><span class="sxs-lookup"><span data-stu-id="b06de-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="b06de-122">Yazılımı yüklemek soran istem içinde seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="b06de-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="b06de-123">Tarayıcınıza bağlı için karşıdan yükleme bağlantısı yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="b06de-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="b06de-124">**Ekleme** tarayıcınız uzantısı.</span><span class="sxs-lookup"><span data-stu-id="b06de-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="b06de-125">Tarayıcınız isterse, ya da seçin **etkinleştirmek** veya **izin** uzantısı.</span><span class="sxs-lookup"><span data-stu-id="b06de-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="b06de-126">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="b06de-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="b06de-127">Erişim paneline oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b06de-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="b06de-128">Ayrıca uzantısı Chrome ve kenar için aşağıdaki doğrudan bağlantılarından yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b06de-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="b06de-129">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="b06de-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="b06de-130">Edge erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="b06de-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="b06de-131">Internet Explorer için Grup İlkesi ayarı</span><span class="sxs-lookup"><span data-stu-id="b06de-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="b06de-132">Uzaktan erişim paneli uzantısı Internet Explorer için kullanıcılarınızın makinelere yüklemeniz olanak tanıyan Grup İlkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b06de-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="b06de-133">Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b06de-133">The prerequisites include:</span></span>

-   <span data-ttu-id="b06de-134">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler, etki alanına.</span><span class="sxs-lookup"><span data-stu-id="b06de-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="b06de-135">Grup İlkesi nesnesi (GPO) düzenlemek için "Ayarları düzenleme" izni olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b06de-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="b06de-136">Varsayılan olarak, aşağıdaki güvenlik gruplarının üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="b06de-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="b06de-137">[Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b06de-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="b06de-138">Öğreticiyi izleyin [Grup İlkesi'ni kullanarak Internet Explorer için erişim paneli uzantısı dağıtma](active-directory-saas-ie-group-policy.md) adım adım yönergeler için Grup İlkesi yapılandırmak ve kullanıcılara dağıtma.</span><span class="sxs-lookup"><span data-stu-id="b06de-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="b06de-139">Internet Explorer erişim panelinde sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b06de-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="b06de-140">İzleyin [erişim paneli uzantısı Internet Explorer için sorun giderme](active-directory-saas-ie-troubleshooting.md) uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="b06de-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="b06de-141">Bu sorun giderme adımları sorunu çözmezse</span><span class="sxs-lookup"><span data-stu-id="b06de-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="b06de-142">bir destek bileti aşağıdaki bilgilerle varsa açın:</span><span class="sxs-lookup"><span data-stu-id="b06de-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="b06de-143">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="b06de-143">Correlation error ID</span></span>

-   <span data-ttu-id="b06de-144">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="b06de-144">UPN (user email address)</span></span>

-   <span data-ttu-id="b06de-145">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="b06de-145">TenantID</span></span>

-   <span data-ttu-id="b06de-146">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="b06de-146">Browser type</span></span>

-   <span data-ttu-id="b06de-147">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="b06de-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b06de-148">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="b06de-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b06de-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b06de-149">Next steps</span></span>
[<span data-ttu-id="b06de-150">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b06de-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
