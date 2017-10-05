---
title: "Parola için yapılandırılmış bir Azure AD galeri uygulaması oturumu açmada sorun çoklu oturum açma | Microsoft Docs"
description: "Parola çoklu oturum açma için yapılandırılmış Azure AD galeri uygulamaları için oturum açma ile ilgili sorunları gidermek için kılavuzluk sorunlu alanları açıklanır"
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="fa003-103">Parola çoklu oturum açma için yapılandırılmış bir Azure AD galeri uygulaması için oturum açma sorunları</span><span class="sxs-lookup"><span data-stu-id="fa003-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="fa003-104">Erişim paneli, Azure AD Yöneticisi erişim verildi görünümü ve başlatma bulut tabanlı uygulamalar Azure Active Directory (Azure AD) bir iş veya Okul hesabı olan bir kullanıcının sağlayan bir web tabanlı portal olmaktır.</span><span class="sxs-lookup"><span data-stu-id="fa003-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="fa003-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa003-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="fa003-106">Erişim paneli Azure Portalı'ndan ayrıdır ve kullanıcıların bir Azure aboneliğine sahip olmasını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="fa003-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="fa003-107">Parola tabanlı çoklu oturum açma (SSO) erişimi Masası'nda kullanmak için erişim paneli uzantısı kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa003-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="fa003-108">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fa003-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="fa003-109">Erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="fa003-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="fa003-110">Erişim paneli JavaScript destekleyen bir tarayıcı gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="fa003-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="fa003-111">Parola tabanlı çoklu oturum açma (SSO) erişimi Masası'nda kullanmak için erişim paneli uzantısı kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa003-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="fa003-112">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fa003-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="fa003-113">Parola tabanlı, SSO için son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="fa003-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="fa003-114">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="fa003-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="fa003-115">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="fa003-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="fa003-116">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="fa003-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="fa003-117">Tarayıcı uzantıları köşesi desteklendiğinde hale kenar Windows 10 için kullanılabilir hale parola tabanlı SSO uzantısı.</span><span class="sxs-lookup"><span data-stu-id="fa003-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="fa003-118">Erişim paneli tarayıcı uzantısı yükleme</span><span class="sxs-lookup"><span data-stu-id="fa003-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="fa003-119">Erişim paneli tarayıcı uzantısı yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fa003-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="fa003-120">Açık [erişim paneli](https://myapps.microsoft.com) olarak oturum açın ve desteklenen tarayıcılar birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="fa003-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="fa003-121">tıklatın bir **parola SSO uygulaması** erişim panelinde.</span><span class="sxs-lookup"><span data-stu-id="fa003-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="fa003-122">Yazılımı yüklemek soran istem içinde seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="fa003-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="fa003-123">Tarayıcınıza bağlı için karşıdan yükleme bağlantısı yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="fa003-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="fa003-124">**Ekleme** tarayıcınız uzantısı.</span><span class="sxs-lookup"><span data-stu-id="fa003-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="fa003-125">Tarayıcınız isterse, ya da seçin **etkinleştirmek** veya **izin** uzantısı.</span><span class="sxs-lookup"><span data-stu-id="fa003-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="fa003-126">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="fa003-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="fa003-127">Erişim paneline oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fa003-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="fa003-128">Ayrıca uzantısı Chrome ve Firefox için aşağıya doğrudan bağlantılarından yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fa003-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="fa003-129">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="fa003-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="fa003-130">Firefox erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="fa003-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="fa003-131">Internet Explorer için Grup İlkesi ayarı</span><span class="sxs-lookup"><span data-stu-id="fa003-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="fa003-132">Uzaktan erişim paneli uzantısı Internet Explorer için kullanıcılarınızın makinelere yüklemeniz olanak tanıyan Grup İlkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa003-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="fa003-133">Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fa003-133">The prerequisites include:</span></span>

-   <span data-ttu-id="fa003-134">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler, etki alanına.</span><span class="sxs-lookup"><span data-stu-id="fa003-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="fa003-135">Grup İlkesi nesnesi (GPO) düzenlemek için "Ayarları düzenleme" izni olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa003-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="fa003-136">Varsayılan olarak, aşağıdaki güvenlik gruplarının üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="fa003-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="fa003-137">[Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa003-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="fa003-138">Öğreticiyi izleyin [Grup İlkesi'ni kullanarak Internet Explorer için erişim paneli uzantısı dağıtma](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) adım adım yönergeler için Grup İlkesi yapılandırmak ve kullanıcılara dağıtma.</span><span class="sxs-lookup"><span data-stu-id="fa003-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="fa003-139">Internet Explorer erişim panelinde sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fa003-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="fa003-140">İzleyin [erişim paneli uzantısı Internet Explorer için sorun giderme](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="fa003-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="fa003-141">Parola çoklu oturum açma galeri olmayan uygulama için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa003-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="fa003-142">Bir uygulama için gereken Azure AD galerisinden yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="fa003-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="fa003-143">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="fa003-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="fa003-144">Uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa003-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="fa003-145">Uygulamaya kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="fa003-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="fa003-146">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="fa003-146">Add a non-gallery application</span></span>

<span data-ttu-id="fa003-147">Azure AD Galeriden bir uygulama eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fa003-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="fa003-148">Açık [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="fa003-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="fa003-149">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="fa003-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fa003-150">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="fa003-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fa003-151">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="fa003-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fa003-152">tıklatın **Ekle** düğmesine sağ üst köşede **kurumsal uygulamalar** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="fa003-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="fa003-153">tıklatın **olmayan galeri uygulaması.**</span><span class="sxs-lookup"><span data-stu-id="fa003-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="fa003-154">Uygulamanızda adını girin **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="fa003-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="fa003-155">Seçin **ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="fa003-155">Select **Add.**</span></span>

<span data-ttu-id="fa003-156">Kısa bir süre sonra uygulamanın yapılandırma dikey görüyor.</span><span class="sxs-lookup"><span data-stu-id="fa003-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="fa003-157">Uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa003-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="fa003-158">Bir uygulama için çoklu oturum açmayı yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fa003-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="fa003-159">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="fa003-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fa003-160">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="fa003-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fa003-161">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="fa003-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fa003-162">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="fa003-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fa003-163">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fa003-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fa003-164">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="fa003-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fa003-165">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="fa003-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="fa003-166">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="fa003-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fa003-167">Modunu seçin **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="fa003-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="fa003-168">Girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="fa003-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="fa003-169">Bu kullanıcılar, kullanıcı adını ve oturum açmak için parola girdiğiniz yere URL'dir.</span><span class="sxs-lookup"><span data-stu-id="fa003-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="fa003-170">Oturum açma alanları URL'de göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fa003-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="fa003-171">Kullanıcılar uygulamayı atayın.</span><span class="sxs-lookup"><span data-stu-id="fa003-171">Assign users to the application.</span></span>

11. <span data-ttu-id="fa003-172">Ayrıca, kullanıcı adına kimlik bilgilerini kullanıcıları satırlarını seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve kullanıcılar adına kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="fa003-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="fa003-173">Aksi takdirde, kullanıcılar başlatma sırasında kimlik kendilerini girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="fa003-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="fa003-174">Uygulamaya kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="fa003-174">Assign users to the application</span></span>

<span data-ttu-id="fa003-175">Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fa003-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="fa003-176">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="fa003-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fa003-177">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="fa003-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fa003-178">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="fa003-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fa003-179">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="fa003-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fa003-180">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fa003-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fa003-181">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="fa003-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fa003-182">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="fa003-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="fa003-183">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="fa003-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fa003-184">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="fa003-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="fa003-185">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="fa003-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="fa003-186">Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="fa003-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="fa003-187">Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="fa003-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="fa003-188">Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="fa003-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="fa003-189">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="fa003-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="fa003-190">Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="fa003-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="fa003-191">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="fa003-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="fa003-192">Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fa003-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="fa003-193">Kısa bir süre sonra seçtiğiniz kullanıcıların erişim panelinde bu uygulamaları başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="fa003-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="fa003-194">Bu sorun giderme adımları sorunu çözümleme yaparsanız</span><span class="sxs-lookup"><span data-stu-id="fa003-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="fa003-195">bir destek bileti aşağıdaki bilgilerle varsa açın:</span><span class="sxs-lookup"><span data-stu-id="fa003-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="fa003-196">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="fa003-196">Correlation error ID</span></span>

-   <span data-ttu-id="fa003-197">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="fa003-197">UPN (user email address)</span></span>

-   <span data-ttu-id="fa003-198">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="fa003-198">TenantID</span></span>

-   <span data-ttu-id="fa003-199">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="fa003-199">Browser type</span></span>

-   <span data-ttu-id="fa003-200">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="fa003-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="fa003-201">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="fa003-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa003-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa003-202">Next steps</span></span>
[<span data-ttu-id="fa003-203">Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fa003-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

