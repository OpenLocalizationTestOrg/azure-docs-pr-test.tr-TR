---
title: "Erişim paneli Web sitesine oturum açma sorunu | Microsoft Docs"
description: "Erişim paneli kullanmak için kaydolun çalışılırken karşılaşabileceğiniz sorunları gidermek için yönergeler"
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
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="c7f8a-103">Erişim paneli Web sitesine oturum açma sorunu</span><span class="sxs-lookup"><span data-stu-id="c7f8a-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="c7f8a-104">Erişim paneli, Azure AD Yöneticisi erişim verildi görünümü ve başlatma bulut tabanlı uygulamalar Azure Active Directory (Azure AD) bir iş veya Okul hesabı olan bir kullanıcının sağlayan bir web tabanlı portal olmaktır.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c7f8a-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="c7f8a-106">Erişim paneli Azure Portalı'ndan ayrıdır ve kullanıcıların bir Azure aboneliğine sahip olmasını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="c7f8a-107">Azure AD'de bir iş veya Okul hesabı varsa kullanıcıların erişim panelinde oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="c7f8a-108">Kullanıcıların doğrudan Azure AD tarafından doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="c7f8a-109">Active Directory Federasyon Hizmetleri (AD FS) kullanarak kullanıcıların kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="c7f8a-110">Kullanıcıların Windows Server Active Directory tarafından doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="c7f8a-111">Bir kullanıcı Azure veya Office 365 için bir abonelik varsa ve Azure portal ya da bir Office 365 uygulaması kullanarak, erişim paneli sorunsuz bir şekilde gerek kalmadan yeniden oturum açmak için kullandığınız mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="c7f8a-112">Kimliği doğrulanmamış kullanıcılar kendi hesabı için Azure AD'de kullanıcı adı ve parola kullanarak oturum açın istenir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="c7f8a-113">Kuruluşun Federasyon yapılandırdıysa, kullanıcı adı yazmaya yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="c7f8a-114">İlk denetlemek için genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="c7f8a-114">General issues to check first</span></span> 

-   <span data-ttu-id="c7f8a-115">Emin olun kullanıcı olduğundan oturum açma için **URL'yi düzeltin**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="c7f8a-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="c7f8a-116">Kullanıcının tarayıcısının URL ekledi emin olun, **Güvenilen siteler**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="c7f8a-117">Kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="c7f8a-118">Kullanıcının hesabı olduğundan emin olun **kilitli değil.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="c7f8a-119">Kullanıcının emin olun **parola süresi değil veya unutulursa.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="c7f8a-120">Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="c7f8a-121">Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="c7f8a-122">Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** yürütülebilmesi çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri izin güncel değil.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="c7f8a-123">Tarayıcınızın tanımlama bilgilerini temizleyip ve yeniden oturum açmaya de deneyin emin olun.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="c7f8a-124">Erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="c7f8a-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="c7f8a-125">Erişim paneli JavaScript destekleyen bir tarayıcı gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="c7f8a-126">Parola tabanlı çoklu oturum açma (SSO) erişimi Masası'nda kullanmak için erişim paneli uzantısı kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="c7f8a-127">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="c7f8a-128">Parola tabanlı, SSO için son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="c7f8a-129">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="c7f8a-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="c7f8a-130">Edge Windows 10 Anniversary Edition veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="c7f8a-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="c7f8a-131">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="c7f8a-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="c7f8a-132">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="c7f8a-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="c7f8a-133">Kullanıcı hesabının sorunları</span><span class="sxs-lookup"><span data-stu-id="c7f8a-133">Problems with the user’s account</span></span>

<span data-ttu-id="c7f8a-134">Kullanıcı hesabında bir sorun nedeniyle erişim Paneli'ne erişim engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="c7f8a-135">Aşağıdaki sorun giderme ve kullanıcıların ve hesap ayarları ile sorunları bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="c7f8a-136">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="c7f8a-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="c7f8a-137">Bir kullanıcının hesap durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="c7f8a-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="c7f8a-138">Bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c7f8a-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="c7f8a-139">Self servis parola sıfırlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7f8a-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="c7f8a-140">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="c7f8a-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="c7f8a-141">Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri</span><span class="sxs-lookup"><span data-stu-id="c7f8a-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="c7f8a-142">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="c7f8a-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="c7f8a-143">Bir kullanıcının atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="c7f8a-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="c7f8a-144">Bir kullanıcı bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="c7f8a-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="c7f8a-145">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="c7f8a-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="c7f8a-146">Bir kullanıcı hesabının mevcut olup olmadığını denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-147">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-148">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-149">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-150">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-151">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-151">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-152">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-153">Beklediğiniz ve hiçbir veri eksik gibi göründüğünü emin olmak için kullanıcı nesnesinin özelliklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="c7f8a-154">Bir kullanıcının hesap durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="c7f8a-154">Check a user’s account status</span></span>

<span data-ttu-id="c7f8a-155">Bir kullanıcı hesabı durumunu denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-156">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-157">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-158">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-159">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-160">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-160">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-161">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-162">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-162">click **Profile**.</span></span>

8.  <span data-ttu-id="c7f8a-163">Altında **ayarları** emin **blok oturum** ayarlanır **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="c7f8a-164">Bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c7f8a-164">Reset a user’s password</span></span>

<span data-ttu-id="c7f8a-165">Bir kullanıcının parolasını sıfırlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-166">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-167">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-168">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-169">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-170">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-170">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-171">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-172">tıklatın **parola sıfırlama** kullanıcı dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="c7f8a-173">tıklatın **parola sıfırlama** düğmesini **parola sıfırlama** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="c7f8a-174">Kopya **geçici parola** veya **yeni bir parola girin** kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="c7f8a-175">Bu yeni parolayı kullanıcıya iletişim, Azure Active Directory'ye sonraki oturum açma sırasında bu parolayı değiştirmeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="c7f8a-176">Self Servis parola sıfırlama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7f8a-176">Enable self-service password reset</span></span>

<span data-ttu-id="c7f8a-177">Self Servis parola sıfırlamayı etkinleştirmek için dağıtım adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="c7f8a-178">Azure Active Directory parolalarını sıfırlamalarına olanak tanıma</span><span class="sxs-lookup"><span data-stu-id="c7f8a-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="c7f8a-179">Sıfırlama veya Active Directory şirket içi parolalarını değiştirmek kullanıcıları etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7f8a-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="c7f8a-180">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="c7f8a-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="c7f8a-181">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-182">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-183">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-184">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-185">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-186">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-186">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-187">tıklatın **çok faktörlü kimlik doğrulaması** dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="c7f8a-188">Bir kez **multi-Factor Authentication Yönetim Portalı** yüklendiğinde emin olduğunuz üzerinde **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="c7f8a-189">Kullanıcı, arama, filtreleme veya sıralama kullanıcı listesinde bulun.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="c7f8a-190">Kullanıcı kullanıcılar listesinden seçin ve **etkinleştirmek**, **devre dışı**, veya **zorla** istediğiniz gibi çok faktörlü kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="c7f8a-191">Bir kullanıcı ise bir **zorlanmış** durumunda, ayarlayın bunları **devre dışı** geçici olarak kendi hesaba geri izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="c7f8a-192">Daha sonra geri oldukları sonra durumlarına değiştirebilirsiniz **etkin** yeniden sonraki oturum açma sırasında kişi bilgileri yeniden kaydetmek için bunları gerektirecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="c7f8a-193">Alternatif olarak, içindeki adımları takip edebilirsiniz [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info) doğrulamak veya onlar için bu veri kümesi için.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="c7f8a-194">Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri</span><span class="sxs-lookup"><span data-stu-id="c7f8a-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="c7f8a-195">Çok faktörlü kimlik doğrulaması, koşullu erişim, kimlik koruması ve parola sıfırlama için kullanılan kullanıcı kimlik doğrulaması kişi bilgilerini denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-196">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-197">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-198">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-199">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-200">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-200">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-201">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-202">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-202">click **Profile**.</span></span>

8.  <span data-ttu-id="c7f8a-203">Ekranı aşağı kaydırarak **kimlik doğrulaması kişi bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="c7f8a-204">**Gözden geçirme** veri, güncelleştirme ve kullanıcı için gerektiği şekilde kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="c7f8a-205">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="c7f8a-205">Check a user’s group memberships</span></span>

<span data-ttu-id="c7f8a-206">Bir kullanıcı grup üyeliklerini denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-207">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-208">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-209">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-210">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-211">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-211">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-212">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-213">tıklatın **grupları** olduğu kullanıcı grupları görmek için bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="c7f8a-214">Bir kullanıcının atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="c7f8a-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="c7f8a-215">Bir kullanıcının atanan lisansları denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-216">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-217">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-218">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-219">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-220">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-220">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-221">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-222">tıklatın **lisansları** , şu anda kullanıcı lisansları görmek üzere atanır.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="c7f8a-223">Bir kullanıcı bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="c7f8a-223">Assign a user a license</span></span> 

<span data-ttu-id="c7f8a-224">Bir kullanıcıya bir lisans atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="c7f8a-225">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c7f8a-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c7f8a-226">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7f8a-227">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7f8a-228">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="c7f8a-229">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-229">click **All users**.</span></span>

6.  <span data-ttu-id="c7f8a-230">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="c7f8a-231">tıklatın **lisansları** , şu anda kullanıcı lisansları görmek üzere atanır.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="c7f8a-232">tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="c7f8a-233">Seçin **bir veya daha fazla ürün** mevcut ürünler listesinden.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="c7f8a-234">**İsteğe bağlı** tıklatın **atama seçenekleri** ürünleri granularly atanacak öğe.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="c7f8a-235">Tıklatın **Tamam** ne zaman bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="c7f8a-236">Tıklatın **atamak** bu lisans bu kullanıcıya atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="c7f8a-237">Bu sorun giderme adımları sorunu çözmezse</span><span class="sxs-lookup"><span data-stu-id="c7f8a-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="c7f8a-238">bir destek bileti aşağıdaki bilgilerle varsa açın:</span><span class="sxs-lookup"><span data-stu-id="c7f8a-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="c7f8a-239">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="c7f8a-239">Correlation error ID</span></span>

-   <span data-ttu-id="c7f8a-240">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="c7f8a-240">UPN (user email address)</span></span>

-   <span data-ttu-id="c7f8a-241">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="c7f8a-241">Tenant ID</span></span>

-   <span data-ttu-id="c7f8a-242">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="c7f8a-242">Browser type</span></span>

-   <span data-ttu-id="c7f8a-243">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="c7f8a-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="c7f8a-244">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="c7f8a-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7f8a-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7f8a-245">Next steps</span></span>
[<span data-ttu-id="c7f8a-246">Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c7f8a-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
