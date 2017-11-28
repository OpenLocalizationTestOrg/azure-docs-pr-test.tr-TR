---
title: "tooa Microsoft uygulaması imzalama aaaProblems | Microsoft Docs"
description: "Toofirst taraf Microsoft Azure AD (örneğin, Office 365) kullanarak Applications imzalarken karşılaştığı yaygın sorunlarını giderme"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="08809-103">Tooa Microsoft uygulaması imzalama sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="08809-104">Microsoft Applications (örneğin, Office 365 Exchange, SharePoint, Yammer, vb.) atanan ve biraz farklı 3 taraf SaaS uygulamaları veya diğer uygulamalar üzerinde çoklu oturum açma için Azure AD ile tümleştirmek yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="08809-105">Kullanıcı erişim tooa Microsoft yayımlanan uygulama alabilirsiniz üç ana yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="08809-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="08809-106">Merhaba Office 365 veya diğer Ücretli paketlerini uygulamalar için erişim aracılığıyla kullanıcılara verilen **lisans atama** ya da doğrudan tootheir kullanıcı hesabı veya bizim grup tabanlı lisans atama özelliği kullanarak bir grup.</span><span class="sxs-lookup"><span data-stu-id="08809-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="08809-107">Microsoft veya üçüncü taraf yazılımınızla herkes için toouse yayımlar, uygulamalar için kullanıcılara üzerinden erişim izni **kullanıcı izni**.</span><span class="sxs-lookup"><span data-stu-id="08809-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="08809-108">This0 toohello uygulamada Azure AD iş veya Okul hesabıyla oturum açın ve kendi hesaplarına toohave erişim sınırlı toosome veri kümesini izin anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="08809-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="08809-109">Microsoft ya da bir 3. taraf serbestçe herkes için toouse yayımlar, uygulamalar için kullanıcılar ayrıca aracılığıyla erişimi verilebilir **yönetici izni**.</span><span class="sxs-lookup"><span data-stu-id="08809-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="08809-110">Bu, bir yönetici hello kuruluşunuzdaki herkes tarafından toohello uygulamasında bir genel yönetici hesabıyla oturum açın ve erişim tooeveryone hello kuruluşunuzdaki vermek Merhaba uygulaması kullanılabilir belirledi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="08809-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="08809-111">tootroubleshoot hello Başlarken sorununuzu [genel sorun alanlarından uygulama erişimi tooconsider](#general-problem-areas-with-application-access-to-consider) ve hello okuma [izlenecek yol: adımları tootroubleshoot Microsoft Application erişim](#walkthrough-steps-to-troubleshoot-microsoft-application-access) Merhaba ayrıntıları içine tooget.</span><span class="sxs-lookup"><span data-stu-id="08809-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="08809-112">Uygulama erişimi tooconsider genel sorun alanlarından</span><span class="sxs-lookup"><span data-stu-id="08809-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="08809-113">Merhaba listesini hızla giderek hello izlenecek tooget okuma toostart, ancak burada önerilir hakkında bir fikir varsa, ayrıntılarına geçebilir genel sorunlu alanları aşağıdadır: [izlenecek yol: adımları tootroubleshoot Microsoft Application erişim](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="08809-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="08809-114">Merhaba kullanıcının hesabı sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="08809-115">Grupları sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="08809-116">Koşullu erişim ilkeleri sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="08809-117">Uygulama onayı sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="08809-118">Adımları tootroubleshoot Microsoft Application erişim</span><span class="sxs-lookup"><span data-stu-id="08809-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="08809-119">Kullanıcılara tooa Microsoft uygulaması imzaladığınızda aşağıda bazı yaygın sorunlar terimleri içine çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="08809-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="08809-120">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-120">General issues toocheck first</span></span>

  * <span data-ttu-id="08809-121">Merhaba kullanıcı toohello içinde imzalama emin olun **URL'yi düzeltin** ve bir yerel uygulama URL değil.</span><span class="sxs-lookup"><span data-stu-id="08809-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="08809-122">Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**</span><span class="sxs-lookup"><span data-stu-id="08809-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="08809-123">Merhaba emin olun **kullanıcının hesabı zaten** Azure Active Directory'de.</span><span class="sxs-lookup"><span data-stu-id="08809-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="08809-124">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="08809-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="08809-125">Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar. [Bir kullanıcının hesap durumunu denetle](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="08809-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="08809-126">Emin hello kullanıcının olun **parola süresi değil veya unutulursa.**</span><span class="sxs-lookup"><span data-stu-id="08809-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="08809-127">[Bir kullanıcının parolasını sıfırlamak](#reset-a-users-password) veya [Self Servis parola sıfırlama etkinleştirme](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="08809-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="08809-128">Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="08809-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="08809-129">[Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetleme](#check-a-users-multi-factor-authentication-status) veya [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="08809-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="08809-130">Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.</span><span class="sxs-lookup"><span data-stu-id="08809-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="08809-131">[Belirli bir koşullu erişim ilkesini denetleme](#problems-with-conditional-access-policies) veya [belirli bir uygulamanın koşullu erişim ilkesini denetleme](#check-a-specific-applications-conditional-access-policy) veya [belirli koşullu erişim ilkesini devre dışı bırak](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="08809-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="08809-132">Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu.</span><span class="sxs-lookup"><span data-stu-id="08809-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="08809-133">[Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetleme](#check-a-users-multi-factor-authentication-status) veya [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="08809-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="08809-134">İçin **Microsoft** **lisans gerektiren uygulamalar** (Office365) gibi hello genel yukarıdaki sorunları çizgili sonra bazı belirli sorunları toocheck aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="08809-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="08809-135">Merhaba kullanıcı sağlayın ya da sahip bir **lisansı atanmış.**</span><span class="sxs-lookup"><span data-stu-id="08809-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="08809-136">[Bir kullanıcının atanan lisansları denetleme](#check-a-users-assigned-licenses) veya [bir grubun atanan lisansları denetleme](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="08809-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="08809-137">Merhaba lisans ise **tooa atanan** **statik grup**, o hello olun **kullanıcının üyesi olduğu** o grubun.</span><span class="sxs-lookup"><span data-stu-id="08809-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="08809-138">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="08809-139">Merhaba lisans ise **tooa atanan** **dinamik grup**, o hello olun **dinamik Grup kural doğru olarak ayarlandığında**.</span><span class="sxs-lookup"><span data-stu-id="08809-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="08809-140">Dinamik bir grubun üyeliğini ölçütlerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="08809-141">Merhaba lisans ise **tooa atanan** **dinamik grup**, o hello dinamik grup sahip olduğundan emin olun **işleme tamamlandı** üyeliğine ve o hello **kullanıcı bir üye** (Bu işlem biraz zaman alabilir).</span><span class="sxs-lookup"><span data-stu-id="08809-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="08809-142">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="08809-143">Merhaba lisans atandığı emin olun sonra hello lisans olduğundan emin olun **süresi**.</span><span class="sxs-lookup"><span data-stu-id="08809-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="08809-144">Merhaba lisans olduğundan emin olun **Merhaba uygulaması için** erişmekte olan.</span><span class="sxs-lookup"><span data-stu-id="08809-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="08809-145">İçin **Microsoft** **bir lisans gerektirmeyen uygulamalar**, başka bir şey toocheck şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08809-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="08809-146">Merhaba uygulaması istiyorsa **kullanıcı düzeyinde izinler** (örneğin "Bu kullanıcının posta kutusu erişim"), o hello kullanıcı toohello uygulamada imzaladığı emin olun ve gerçekleştirdiği bir **kullanıcı düzeyinde onay işlemi**  toolet Merhaba uygulaması kendi verilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="08809-147">Merhaba uygulaması istiyorsa **yönetici düzeyi izinler** (örneğin "tüm kullanıcının posta kutularına erişim"), genel yönetici yürüttü emin olun bir **yönetici düzeyi onay işlemi tüm kullanıcılar adına** hello kuruluşunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="08809-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="08809-148">Merhaba kullanıcının hesabı sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-148">Problems with hello user’s account</span></span>

<span data-ttu-id="08809-149">Uygulama erişimi toohello uygulama atanmış bir kullanıcı tooa sorun nedeniyle engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="08809-150">Aşağıdaki sorun giderme ve kullanıcıların ve hesap ayarları ile sorunları bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08809-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="08809-151">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="08809-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="08809-152">Bir kullanıcının hesap durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="08809-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="08809-153">Bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="08809-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="08809-154">Self servis parola sıfırlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="08809-155">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="08809-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="08809-156">Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri</span><span class="sxs-lookup"><span data-stu-id="08809-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="08809-157">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="08809-158">Bir kullanıcının atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="08809-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="08809-159">Bir kullanıcı bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="08809-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="08809-160">Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="08809-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="08809-161">bir kullanıcı hesabı varsa, toocheck hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-162">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-163">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-164">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-165">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-166">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-166">click **All users**.</span></span>

6.  <span data-ttu-id="08809-167">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-168">Merhaba kullanıcı nesnesi toobe beklediğiniz ve hiçbir veri eksik gibi göründüğünü emin Hello özelliklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="08809-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="08809-169">Bir kullanıcının hesap durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="08809-169">Check a user’s account status</span></span>

<span data-ttu-id="08809-170">toocheck bir kullanıcıya ait hesap durumu, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-171">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-172">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-173">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-174">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-175">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-175">click **All users**.</span></span>

6.  <span data-ttu-id="08809-176">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-177">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="08809-177">click **Profile**.</span></span>

8.  <span data-ttu-id="08809-178">Altında **ayarları** emin **blok oturum** çok ayarlanır**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="08809-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="08809-179">Bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="08809-179">Reset a user’s password</span></span>

<span data-ttu-id="08809-180">tooreset bir kullanıcının parolasını, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-181">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-182">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-183">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-184">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-185">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-185">click **All users**.</span></span>

6.  <span data-ttu-id="08809-186">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-187">Merhaba tıklatın **parola sıfırlama** hello kullanıcı dikey penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="08809-188">Merhaba tıklatın **parola sıfırlama** hello düğmesinde **parola sıfırlama** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="08809-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="08809-189">Kopya hello **geçici parola** veya **yeni bir parola girin** hello kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="08809-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="08809-190">Bu yeni parola toohello kullanıcı iletişim, bu parolayı sırasında bir sonraki oturum tooAzure Active Directory gerekli toochange olabilir.</span><span class="sxs-lookup"><span data-stu-id="08809-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="08809-191">Self Servis parola sıfırlama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-191">Enable self-service password reset</span></span>

<span data-ttu-id="08809-192">tooenable Self Servis parola sıfırlama, hello dağıtım adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="08809-193">Azure Active Directory parolalarını kullanıcılar tooreset etkinleştir</span><span class="sxs-lookup"><span data-stu-id="08809-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="08809-194">Kullanıcıların tooreset etkinleştirmek veya Active Directory şirket içi parolalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="08809-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="08809-195">Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="08809-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="08809-196">toocheck kullanıcı çok faktörlü kimlik doğrulama durumu, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-197">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-198">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-199">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-200">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-201">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-201">click **All users**.</span></span>

6.  <span data-ttu-id="08809-202">Merhaba tıklatın **çok faktörlü kimlik doğrulaması** hello dikey penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="08809-203">Bir kez hello **multi-Factor Authentication Yönetim Portalı** yüklendiğinde hello üzerinde olduğundan olun **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="08809-204">Merhaba kullanıcı arama, filtreleme veya sıralama hello kullanıcı listesinde bulun.</span><span class="sxs-lookup"><span data-stu-id="08809-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="08809-205">Kullanıcıların hello listesinden seçim hello kullanıcı ve **etkinleştirmek**, **devre dışı**, veya **zorla** istediğiniz gibi çok faktörlü kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="08809-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="08809-206">**Not**: kullanıcı ise bir **zorlanmış** durumunda, ayarladığınız bunları çok**devre dışı** geçici olarak toolet bunları kendi hesaba geri.</span><span class="sxs-lookup"><span data-stu-id="08809-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="08809-207">Bunlar geri olduktan sonra daha sonra durumlarına çok değiştirebilirsiniz**etkin** yeniden toorequire bunları toore kayıt sırasında bir sonraki kişi bilgileri oturum açın.</span><span class="sxs-lookup"><span data-stu-id="08809-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="08809-208">Alternatif olarak, hello hello adımları takip edebilirsiniz [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info) tooverify ya da bunlar için bu veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="08809-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="08809-209">Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri</span><span class="sxs-lookup"><span data-stu-id="08809-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="08809-210">bir kullanıcının kimlik doğrulamasını başvurun çok faktörlü kimlik doğrulaması, koşullu erişim, kimlik koruması ve parola sıfırlamak için kullanılan bilgileri toocheck hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-211">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-212">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-213">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-214">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-215">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-215">click **All users**.</span></span>

6.  <span data-ttu-id="08809-216">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-217">tıklatın **profil**.</span><span class="sxs-lookup"><span data-stu-id="08809-217">click **Profile**.</span></span>

8.  <span data-ttu-id="08809-218">Çok ilerleyin**kimlik doğrulaması kişi bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="08809-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="08809-219">**Gözden geçirme** hello veri, hello kullanıcı ve güncelleştirme için gerektiği şekilde kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="08809-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="08809-220">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-220">Check a user’s group memberships</span></span>

<span data-ttu-id="08809-221">toocheck bir kullanıcıya ait grup üyeliklerini, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-222">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-223">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-224">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-225">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-226">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-226">click **All users**.</span></span>

6.  <span data-ttu-id="08809-227">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-228">tıklatın **grupları** hello kullanıcı grupları toosee bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="08809-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="08809-229">Bir kullanıcının atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="08809-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="08809-230">toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-231">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-232">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-233">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-234">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-235">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-235">click **All users**.</span></span>

6.  <span data-ttu-id="08809-236">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-237">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="08809-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="08809-238">Bir kullanıcı bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="08809-238">Assign a user a license</span></span> 

<span data-ttu-id="08809-239">tooassign lisans tooa kullanıcı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-240">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-241">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-242">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-243">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-244">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="08809-244">click **All users**.</span></span>

6.  <span data-ttu-id="08809-245">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-246">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="08809-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="08809-247">Merhaba tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="08809-248">Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="08809-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="08809-249">**İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın.</span><span class="sxs-lookup"><span data-stu-id="08809-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="08809-250">Tıklatın **Tamam** ne zaman bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="08809-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="08809-251">Merhaba tıklatın **atamak** tooassign bu lisansları toothis kullanıcı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="08809-252">Grupları sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-252">Problems with groups</span></span>

<span data-ttu-id="08809-253">Uygulama erişimi toohello uygulama atanmış bir gruba tooa sorun nedeniyle engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="08809-254">Aşağıdaki sorun giderme ve gruplar ve grup üyelikleri ile sorunları bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08809-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="08809-255">Bir grubun üyeliğini kontrol edin</span><span class="sxs-lookup"><span data-stu-id="08809-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="08809-256">Dinamik bir grubun üyeliğini ölçütlerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="08809-257">Bir grubun atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="08809-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="08809-258">Bir grubun lisansları yeniden işleyin</span><span class="sxs-lookup"><span data-stu-id="08809-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="08809-259">Bir gruba bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="08809-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="08809-260">Bir grubun üyeliğini kontrol edin</span><span class="sxs-lookup"><span data-stu-id="08809-260">Check a group’s membership</span></span>

<span data-ttu-id="08809-261">toocheck bir grubun üyeliğini, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-262">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-263">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-264">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-265">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-266">tıklatın **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="08809-266">click **All groups**.</span></span>

6.  <span data-ttu-id="08809-267">**Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-268">tıklatın **üyeleri** tooreview hello kullanıcıların listesini atanan toothis grubu.</span><span class="sxs-lookup"><span data-stu-id="08809-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="08809-269">Dinamik bir grubun üyeliğini ölçütlerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="08809-270">toocheck dinamik grubun Üyelik ölçütleri hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-271">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-272">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-273">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-274">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-275">tıklatın **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="08809-275">click **All groups**.</span></span>

6.  <span data-ttu-id="08809-276">**Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-277">tıklatın **dinamik Üyelik kuralları.**</span><span class="sxs-lookup"><span data-stu-id="08809-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="08809-278">Gözden geçirme hello **basit** veya **Gelişmiş** tanımlanan bu grup için kural ve bu grubun üyesi toobe istediğiniz hello kullanıcının bu ölçütleri karşılayan emin olun.</span><span class="sxs-lookup"><span data-stu-id="08809-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="08809-279">Bir grubun atanan lisansları denetleme</span><span class="sxs-lookup"><span data-stu-id="08809-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="08809-280">toocheck bir gruba ait atanmış lisansların, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-281">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-282">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-283">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-284">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-285">tıklatın **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="08809-285">click **All groups**.</span></span>

6.  <span data-ttu-id="08809-286">**Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-287">tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.</span><span class="sxs-lookup"><span data-stu-id="08809-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="08809-288">Bir grubun lisansları yeniden işleyin</span><span class="sxs-lookup"><span data-stu-id="08809-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="08809-289">tooreprocess bir gruba ait atanmış lisansların, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-290">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-291">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-292">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-293">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-294">tıklatın **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="08809-294">click **All groups**.</span></span>

6.  <span data-ttu-id="08809-295">**Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-296">tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.</span><span class="sxs-lookup"><span data-stu-id="08809-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="08809-297">Merhaba tıklatın **yeniden işleyin** atanan lisansları toothis grubun üyeleri hello düğmesi tooensure güncel.</span><span class="sxs-lookup"><span data-stu-id="08809-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="08809-298">Bu, başlangıç boyutu ve karmaşıklığı hello grubunun bağlı olarak uzun bir süre devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="08809-299">toodo bu daha hızlı ve göz önünde bulundurun geçici olarak bir lisans toohello kullanıcı doğrudan atama.</span><span class="sxs-lookup"><span data-stu-id="08809-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="08809-300">[Bir kullanıcı bir lisans atamak](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="08809-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="08809-301">Bir gruba bir lisans atama</span><span class="sxs-lookup"><span data-stu-id="08809-301">Assign a group a license</span></span>

<span data-ttu-id="08809-302">tooassign bir lisans tooa grubu hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="08809-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="08809-303">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-304">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-305">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-306">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-307">tıklatın **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="08809-307">click **All groups**.</span></span>

6.  <span data-ttu-id="08809-308">**Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="08809-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="08809-309">tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.</span><span class="sxs-lookup"><span data-stu-id="08809-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="08809-310">Merhaba tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="08809-311">Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="08809-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="08809-312">**İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın.</span><span class="sxs-lookup"><span data-stu-id="08809-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="08809-313">Tıklatın **Tamam** ne zaman bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="08809-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="08809-314">Merhaba tıklatın **atamak** bu lisansları toothis Grup tooassign düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="08809-315">Bu, başlangıç boyutu ve karmaşıklığı hello grubunun bağlı olarak uzun bir süre devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="08809-316">toodo bu daha hızlı ve göz önünde bulundurun geçici olarak bir lisans toohello kullanıcı doğrudan atama.</span><span class="sxs-lookup"><span data-stu-id="08809-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="08809-317">[Bir kullanıcı bir lisans atamak](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="08809-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="08809-318">Koşullu erişim ilkeleri sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="08809-319">Belirli bir koşullu erişim ilkesine denetleyin</span><span class="sxs-lookup"><span data-stu-id="08809-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="08809-320">toocheck veya tek koşullu erişim ilkesini doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08809-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="08809-321">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-322">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-323">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-324">tıklatın **kurumsal uygulamalar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-325">Merhaba tıklatın **koşullu erişim** Gezinti öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="08809-326">inceleyerek ilgilendiğiniz hello İlkesi'ni tıklatın.</span><span class="sxs-lookup"><span data-stu-id="08809-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="08809-327">Belirli bir koşul, atamaları ya da kullanıcı erişimi engelliyor olabilecek diğer ayarları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="08809-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="08809-328">Bunu değil etkileyen oturum eklentiler toodo Bu, kümesi hello Bu ilke tooensure tootemporarily devre dışı bırak isteyebilir **ilkesini etkinleştir** çok geçiş**yok** hello tıklatıp **kaydetmek** düğmesi .</span><span class="sxs-lookup"><span data-stu-id="08809-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="08809-329">Belirli bir uygulamanın koşullu erişim ilkesini denetleme</span><span class="sxs-lookup"><span data-stu-id="08809-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="08809-330">toocheck veya tek bir uygulamanın şu anda yapılandırılmış koşullu erişim ilkesini doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08809-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="08809-331">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-332">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-333">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-334">tıklatın **kurumsal uygulamalar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-335">tıklatın **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="08809-335">click **All applications**.</span></span>

6.  <span data-ttu-id="08809-336">Arama ilgilendiğiniz ya da kullanıcı hello Merhaba uygulaması toosign tooby uygulamada çalışıyor için ad veya uygulama kimliği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="08809-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="08809-337">Aradığınız Merhaba uygulaması görmüyorsanız, hello tıklatın **filtre** düğmesine tıklayın ve hello listesi hello kapsamını çok genişletin**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="08809-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="08809-338">Daha fazla sütun toosee isterseniz, hello tıklatın **sütunları** düğmesini tooadd ek ayrıntılar, uygulamalarınız için.</span><span class="sxs-lookup"><span data-stu-id="08809-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="08809-339">Merhaba tıklatın **koşullu erişim** Gezinti öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="08809-340">inceleyerek ilgilendiğiniz hello İlkesi'ni tıklatın.</span><span class="sxs-lookup"><span data-stu-id="08809-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="08809-341">Belirli bir koşul, atamaları ya da kullanıcı erişimi engelliyor olabilecek diğer ayarları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="08809-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="08809-342">Bunu değil etkileyen oturum eklentiler toodo Bu, kümesi hello Bu ilke tooensure tootemporarily devre dışı bırak isteyebilir **ilkesini etkinleştir** çok geçiş**yok** hello tıklatıp **kaydetmek** düğmesi .</span><span class="sxs-lookup"><span data-stu-id="08809-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="08809-343">Belirli bir koşullu erişim ilkesine devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="08809-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="08809-344">toocheck veya tek koşullu erişim ilkesini doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08809-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="08809-345">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="08809-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08809-346">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="08809-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08809-347">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08809-348">tıklatın **kurumsal uygulamalar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="08809-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="08809-349">Merhaba tıklatın **koşullu erişim** Gezinti öğesi.</span><span class="sxs-lookup"><span data-stu-id="08809-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="08809-350">inceleyerek ilgilendiğiniz hello İlkesi'ni tıklatın.</span><span class="sxs-lookup"><span data-stu-id="08809-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="08809-351">Hello İlkesi ayarı hello tarafından devre dışı **ilkesini etkinleştir** çok geçiş**Hayır** hello tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08809-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="08809-352">Uygulama onayı sorunları</span><span class="sxs-lookup"><span data-stu-id="08809-352">Problems with application consent</span></span>

<span data-ttu-id="08809-353">Merhaba uygun izinlere onay işlemi değil oluştuğu için uygulama erişimi engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="08809-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="08809-354">Aşağıdaki sorun giderme ve uygulama izin sorunları çözmeye bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08809-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="08809-355">Bir kullanıcı düzeyinde onay işlemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="08809-356">Herhangi bir uygulama için yönetici düzeyi onay işlemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="08809-357">Bir tek kiracılı uygulama için yönetici düzeyi onay gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="08809-358">Çok kiracılı uygulama için yönetici düzeyi onay gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="08809-359">Bir kullanıcı düzeyinde onay işlemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="08809-360">İzinleri isteyen herhangi Open ID Connect özellikli bir uygulama için toohello uygulamanın oturum açma ekranı gezinme hello oturum açmış kullanıcı için kullanıcı düzeyinde izin toohello uygulaması gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="08809-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="08809-361">Toodo Bu program aracılığıyla istiyorsanız, bkz: [tek tek kullanıcı izni isteyen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="08809-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="08809-362">Herhangi bir uygulama için yönetici düzeyi onay işlemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="08809-363">İçin **yalnızca hello V1 uygulama modeli kullanılarak geliştirilen uygulamaları**, ekleyerek bu yönetici düzeyi onay toooccur zorlayabilirsiniz "**? yönetici komut isteminde =\_onayı**" toohello sonuna bir uygulamanın oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="08809-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="08809-364">İçin **hello V2 uygulama modeli kullanılarak geliştirilen herhangi bir uygulama**, hello altındaki hello yönergeleri izleyerek bu yönetici düzeyi onay toooccur zorunlu kılabilir **bir dizinden hello izinleri iste Yönetici** bölümünü [hello yönetici onayı uç noktası kullanarak](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="08809-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="08809-365">Bir tek kiracılı uygulama için yönetici düzeyi onay gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="08809-366">İçin **tek Kiracı uygulamaları** izinleri (gelenler geliştirdiğiniz veya, kuruluşunuzda sahip), istek gerçekleştirebileceğiniz bir **yönetici düzeyi onay** tüm adına işlemi Genel yönetici olarak oturum açmayı ve üzerinde hello tıklatarak kullanıcıları **izinleri verin** düğmesi hello hello üstündeki **uygulama kayıt defteri -&gt; tüm uygulamalar -&gt; - bir uygulama seçin &gt; Gerekli izinler** dikey.</span><span class="sxs-lookup"><span data-stu-id="08809-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="08809-367">İçin **hello V1 veya V2 uygulama modeli kullanılarak geliştirilen herhangi bir uygulama**, hello altındaki hello yönergeleri izleyerek bu yönetici düzeyi onay toooccur zorunlu kılabilir **isteği hello izinlerinin bir Dizin yönetici** bölümünü [hello yönetici onayı uç noktası kullanarak](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="08809-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="08809-368">Çok kiracılı uygulama için yönetici düzeyi onay gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="08809-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="08809-369">İçin **çok kiracılı uygulamalara** (bir uygulama bir üçüncü taraf veya Microsoft, geliştirir gibi) bu istek izinlerine gerçekleştirebileceğiniz bir **yönetici düzeyi onay** işlemi.</span><span class="sxs-lookup"><span data-stu-id="08809-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="08809-370">Genel yönetici olarak oturum açın ve üzerinde hello tıklayarak **izinleri verin** düğmesi hello altında **kurumsal uygulamalar -&gt; tüm uygulamalar -&gt; bir uygulama - seçin&gt; İzinleri** dikey (kullanılabilir yakında).</span><span class="sxs-lookup"><span data-stu-id="08809-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="08809-371">Merhaba altındaki hello yönergeleri izleyerek bu yönetici düzeyi onay toooccur zorlayabilir **hello izinleri directory yönetici olarak istek** bölümünü [hello yönetici onayı uç noktasıkullanarak](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="08809-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08809-372">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08809-372">Next steps</span></span>
[<span data-ttu-id="08809-373">Merhaba yönetici onayı uç noktası kullanma</span><span class="sxs-lookup"><span data-stu-id="08809-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

