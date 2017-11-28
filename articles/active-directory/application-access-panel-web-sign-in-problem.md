---
title: "Web sitesi toohello erişim paneli imzalama aaaProblem | Microsoft Docs"
description: "Erişim paneli toouse toosign çalışırken karşılaşabileceğiniz Kılavuzu tootroubleshoot sorunlar hello"
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="2653c-103">Toohello erişim paneli Web sitesinde oturum açarken bir sorunla</span><span class="sxs-lookup"><span data-stu-id="2653c-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="2653c-104">Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir.</span><span class="sxs-lookup"><span data-stu-id="2653c-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="2653c-105">Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2653c-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="2653c-106">Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="2653c-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="2653c-107">Kullanıcılar, Azure AD'de bir iş veya Okul hesabı varsa toohello erişim paneli oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="2653c-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="2653c-108">Kullanıcıların doğrudan Azure AD tarafından doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="2653c-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="2653c-109">Active Directory Federasyon Hizmetleri (AD FS) kullanarak kullanıcıların kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="2653c-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="2653c-110">Kullanıcıların Windows Server Active Directory tarafından doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="2653c-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="2653c-111">Bir kullanıcı Azure veya Office 365 için bir abonelik varsa ve hello Azure portal ya da bir Office 365 uygulaması kullanarak, mümkün toouse olacak toosign içinde yeniden gerek kalmadan erişim paneli sorunsuz bir şekilde hello.</span><span class="sxs-lookup"><span data-stu-id="2653c-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="2653c-112">Kimliği doğrulanmamış kullanıcıların kendi hesabı için Azure AD içinde hello kullanıcı adı ve parola kullanarak, istendiğinde toosign olması.</span><span class="sxs-lookup"><span data-stu-id="2653c-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="2653c-113">Merhaba kuruluş Federasyon yapılandırdıysa, hello kullanıcı adı yazmaya yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="2653c-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="2653c-114">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="2653c-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="2653c-115">Merhaba kullanıcı toohello içinde imzalama emin olun **URL'yi düzeltin**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="2653c-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="2653c-116">Merhaba kullanıcının tarayıcısının hello URL tooits eklenmiş emin **Güvenilen siteler**</span><span class="sxs-lookup"><span data-stu-id="2653c-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="2653c-117">Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.</span><span class="sxs-lookup"><span data-stu-id="2653c-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="2653c-118">Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**</span><span class="sxs-lookup"><span data-stu-id="2653c-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="2653c-119">Emin hello kullanıcının olun **parola süresi değil veya unutulursa.**</span><span class="sxs-lookup"><span data-stu-id="2653c-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="2653c-120">Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="2653c-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="2653c-121">Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="2653c-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="2653c-122">Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu.</span><span class="sxs-lookup"><span data-stu-id="2653c-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="2653c-123">Tarayıcınızın tanımlama bilgilerini temizleyip ve toosign olarak yeniden deneniyor yapma emin tooalso deneyin.</span><span class="sxs-lookup"><span data-stu-id="2653c-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="2653c-124">Merhaba erişim paneli toplantı tarayıcı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="2653c-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="2653c-125">JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="2653c-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="2653c-126">toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2653c-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="2653c-127">Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2653c-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="2653c-128">Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:</span><span class="sxs-lookup"><span data-stu-id="2653c-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="2653c-129">Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="2653c-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="2653c-130">Edge Windows 10 Anniversary Edition veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="2653c-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="2653c-131">Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde</span><span class="sxs-lookup"><span data-stu-id="2653c-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="2653c-132">Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="2653c-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="2653c-133">Merhaba kullanıcının hesabı sorunları</span><span class="sxs-lookup"><span data-stu-id="2653c-133">Problems with hello user’s account</span></span>

<span data-ttu-id="2653c-134">Erişim paneli hello kullanıcının hesabı tooa sorun nedeniyle engellenmiş toohello erişin.</span><span class="sxs-lookup"><span data-stu-id="2653c-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="2653c-135">Aşağıdaki sorun giderme ve kullanıcıların ve hesap ayarları ile sorunları bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2653c-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="2653c-136">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="2653c-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="2653c-137">Bir kullanıcının hesap durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="2653c-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="2653c-138">Bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="2653c-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="2653c-139">Self servis parola sıfırlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2653c-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="2653c-140">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="2653c-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="2653c-141">Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri</span><span class="sxs-lookup"><span data-stu-id="2653c-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="2653c-142">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="2653c-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="2653c-143">Bir kullanıcının atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="2653c-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="2653c-144">Bir kullanıcı bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="2653c-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="2653c-145">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="2653c-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="2653c-146">bir kullanıcı hesabı varsa, toocheck hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-147">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-148">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-149">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-150">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-151">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-151">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-152">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-153">Merhaba kullanıcı nesnesi toobe beklediğiniz ve hiçbir veri eksik gibi göründüğünü emin Hello özelliklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2653c-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="2653c-154">Bir kullanıcının hesap durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="2653c-154">Check a user’s account status</span></span>

<span data-ttu-id="2653c-155">toocheck bir kullanıcıya ait hesap durumu, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-156">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-157">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-158">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-159">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-160">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-160">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-161">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-162">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="2653c-162">click **Profile**.</span></span>

8.  <span data-ttu-id="2653c-163">Altında **ayarları** emin **blok oturum** çok ayarlanır**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="2653c-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="2653c-164">Bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="2653c-164">Reset a user’s password</span></span>

<span data-ttu-id="2653c-165">tooreset bir kullanıcının parolasını, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-166">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-167">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-168">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-169">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-170">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-170">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-171">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-172">Merhaba tıklatın **parola sıfırlama** hello kullanıcı dikey penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="2653c-173">Merhaba tıklatın **parola sıfırlama** hello düğmesinde **parola sıfırlama** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="2653c-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="2653c-174">Kopya hello **geçici parola** veya **yeni bir parola girin** hello kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="2653c-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="2653c-175">Bu yeni parola toohello kullanıcı iletişim, bu parolayı sırasında bir sonraki oturum tooAzure Active Directory gerekli toochange olabilir.</span><span class="sxs-lookup"><span data-stu-id="2653c-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="2653c-176">Self Servis parola sıfırlama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2653c-176">Enable self-service password reset</span></span>

<span data-ttu-id="2653c-177">tooenable Self Servis parola sıfırlama, hello dağıtım adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="2653c-178">Azure Active Directory parolalarını kullanıcılar tooreset etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2653c-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="2653c-179">Kullanıcıların tooreset etkinleştirmek veya Active Directory şirket içi parolalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="2653c-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="2653c-180">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="2653c-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="2653c-181">toocheck kullanıcı çok faktörlü kimlik doğrulama durumu, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-182">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-183">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-184">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-185">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-186">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-186">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-187">Merhaba tıklatın **çok faktörlü kimlik doğrulaması** hello dikey penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="2653c-188">Bir kez hello **multi-Factor Authentication Yönetim Portalı** yüklendiğinde hello üzerinde olduğundan olun **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="2653c-189">Merhaba kullanıcı arama, filtreleme veya sıralama hello kullanıcı listesinde bulun.</span><span class="sxs-lookup"><span data-stu-id="2653c-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="2653c-190">Kullanıcıların hello listesinden seçim hello kullanıcı ve **etkinleştirmek**, **devre dışı**, veya **zorla** istediğiniz gibi çok faktörlü kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="2653c-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2653c-191">Bir kullanıcı ise bir **zorlanmış** durumunda, ayarladığınız bunları çok**devre dışı** geçici olarak toolet bunları kendi hesaba geri.</span><span class="sxs-lookup"><span data-stu-id="2653c-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="2653c-192">Bunlar geri olduktan sonra daha sonra durumlarına çok değiştirebilirsiniz**etkin** yeniden toorequire bunları toore kayıt sırasında bir sonraki kişi bilgileri oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2653c-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="2653c-193">Alternatif olarak, hello hello adımları takip edebilirsiniz [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info) tooverify ya da bunlar için bu veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="2653c-194">Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri</span><span class="sxs-lookup"><span data-stu-id="2653c-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="2653c-195">bir kullanıcının kimlik doğrulamasını başvurun çok faktörlü kimlik doğrulaması, koşullu erişim, kimlik koruması ve parola sıfırlamak için kullanılan bilgileri toocheck hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-196">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-197">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-198">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-199">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-200">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-200">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-201">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-202">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="2653c-202">click **Profile**.</span></span>

8.  <span data-ttu-id="2653c-203">Çok ilerleyin**kimlik doğrulaması kişi bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="2653c-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="2653c-204">**Gözden geçirme** hello veri, hello kullanıcı ve güncelleştirme için gerektiği şekilde kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="2653c-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="2653c-205">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="2653c-205">Check a user’s group memberships</span></span>

<span data-ttu-id="2653c-206">toocheck bir kullanıcıya ait grup üyeliklerini, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-207">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-208">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-209">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-210">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-211">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-211">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-212">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-213">tıklatın **grupları** hello kullanıcı grupları toosee bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="2653c-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="2653c-214">Bir kullanıcının atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="2653c-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="2653c-215">toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-216">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-217">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-218">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-219">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-220">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-220">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-221">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-222">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="2653c-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="2653c-223">Bir kullanıcı bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="2653c-223">Assign a user a license</span></span> 

<span data-ttu-id="2653c-224">tooassign lisans tooa kullanıcı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2653c-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="2653c-225">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2653c-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2653c-226">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2653c-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2653c-227">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2653c-228">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2653c-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2653c-229">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2653c-229">click **All users**.</span></span>

6.  <span data-ttu-id="2653c-230">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2653c-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2653c-231">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="2653c-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="2653c-232">Merhaba tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="2653c-233">Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="2653c-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="2653c-234">**İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın.</span><span class="sxs-lookup"><span data-stu-id="2653c-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="2653c-235">Tıklatın **Tamam** ne zaman bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="2653c-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2653c-236">Merhaba tıklatın **atamak** tooassign bu lisansları toothis kullanıcı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2653c-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="2653c-237">Bu sorun giderme adımları hello sorunu çözmezse</span><span class="sxs-lookup"><span data-stu-id="2653c-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="2653c-238">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="2653c-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="2653c-239">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="2653c-239">Correlation error ID</span></span>

-   <span data-ttu-id="2653c-240">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="2653c-240">UPN (user email address)</span></span>

-   <span data-ttu-id="2653c-241">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="2653c-241">Tenant ID</span></span>

-   <span data-ttu-id="2653c-242">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="2653c-242">Browser type</span></span>

-   <span data-ttu-id="2653c-243">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="2653c-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="2653c-244">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="2653c-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="2653c-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2653c-245">Next steps</span></span>
[<span data-ttu-id="2653c-246">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="2653c-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
