---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma - hızlı başlangıç | Microsoft Docs"
description: "Bu makalede, Azure Active Directory sorunsuz çoklu oturum açma ile çalışmaya başlama açıklar."
services: active-directory
keywords: "Azure AD, SSO, gerekli bileşenleri yükleme Active Directory, Azure AD Connect nedir çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="fa983-104">Azure Active Directory sorunsuz çoklu oturum açma: Hızlı Başlangıç</span><span class="sxs-lookup"><span data-stu-id="fa983-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="fa983-105">Sorunsuz SSO dağıtma</span><span class="sxs-lookup"><span data-stu-id="fa983-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="fa983-106">Azure Active Directory sorunsuz çoklu oturum açma (Azure AD sorunsuz SSO) otomatik olarak oturum açtığında şirket ağınıza bağlı kurumsal masaüstü üzerinde olduklarında kullanıcıların.</span><span class="sxs-lookup"><span data-stu-id="fa983-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="fa983-107">Şirket içinde ek bileşenleri gerek kalmadan, kullanıcılarınızın bulut tabanlı uygulamalar için kolay erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa983-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fa983-108">Sorunsuz SSO özelliği şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="fa983-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="fa983-109">Sorunsuz SSO dağıtmak için şu adımları izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa983-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="fa983-110">1. adım: Önkoşul denetimi</span><span class="sxs-lookup"><span data-stu-id="fa983-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="fa983-111">Aşağıdaki önkoşulların yerine getirildiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="fa983-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="fa983-112">Azure AD Connect sunucusunu ayarlama: kullanırsanız [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md) , oturum açma yöntemi başka bir eylem gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="fa983-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="fa983-113">Kullanırsanız [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) , oturum açma yöntemi olarak ve Azure AD Connect ve Azure AD arasında bir güvenlik duvarı varsa, emin olun:</span><span class="sxs-lookup"><span data-stu-id="fa983-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="fa983-114">Sürümleri 1.1.484.0 kullanıyorsanız veya Azure AD Connect sonraki.</span><span class="sxs-lookup"><span data-stu-id="fa983-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="fa983-115">Azure AD Connect ile iletişim kurabilir `*.msappproxy.net` URL'leri ve üstünde bağlantı noktası 443'tür.</span><span class="sxs-lookup"><span data-stu-id="fa983-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="fa983-116">Yalnızca asıl kullanıcı oturum açma işlemleri için özelliğini etkinleştirdiğinizde bu geçerli bir önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="fa983-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="fa983-117">Azure AD Connect, doğrudan IP bağlantılar yapabilir [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="fa983-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="fa983-118">Yeniden yalnızca özelliğini etkinleştirdiğinizde bu önkoşulu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fa983-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="fa983-119">(Azure AD Connect'i kullanarak) Azure AD eşitleme ve olan kullanıcılar için sorunsuz SSO etkinleştirmek istediğiniz her AD ormanı için etki alanı yönetici kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa983-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="fa983-120">2. adım: özelliğini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fa983-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="fa983-121">Sorunsuz SSO kullanarak etkinleştirilebilir [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="fa983-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="fa983-122">Azure AD Connect yeni yüklemesini yapıyorsanız seçin [özel yükleme yolu](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="fa983-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="fa983-123">"Kullanıcı oturum açma" sayfanın "çoklu oturum açmayı etkinleştir" seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="fa983-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect - kullanıcı oturum açma](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="fa983-125">Azure AD Connect yüklemesi zaten varsa, "Değişiklik kullanıcı oturum açma sayfasında" Azure AD Connect seçin ve "İleri" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fa983-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="fa983-126">Ardından "çoklu oturum açmayı etkinleştir" seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="fa983-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect - değişiklik kullanıcı oturum açma](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="fa983-128">"Çoklu oturum açmayı etkinleştir" sayfasına ulaşana kadar sihirbaza devam edin.</span><span class="sxs-lookup"><span data-stu-id="fa983-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="fa983-129">(Azure AD Connect'i kullanarak) Azure AD eşitleme ve olan kullanıcılar için sorunsuz SSO etkinleştirmek istediğiniz her AD orman için etki alanı yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="fa983-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="fa983-130">Sihirbaz tamamlandıktan sonra Kiracı'sorunsuz SSO etkin.</span><span class="sxs-lookup"><span data-stu-id="fa983-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="fa983-131">Etki alanı yönetici kimlik bilgileri Azure AD Connect veya Azure AD depolanmaz, ancak yalnızca özelliğini etkinleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fa983-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="fa983-132">Sorunsuz SSO doğru etkinleştirdiğinizden emin doğrulamak için bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="fa983-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="fa983-133">Oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="fa983-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="fa983-134">Seçin **Azure Active Directory** sol gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="fa983-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="fa983-135">Seçin **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="fa983-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="fa983-136">Doğrulayın **sorunsuz çoklu oturum açma** özelliği gösterildiğinden **etkin**.</span><span class="sxs-lookup"><span data-stu-id="fa983-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure portal - Azure AD Connect dikey penceresi](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="fa983-138">3. adım: özelliği alma</span><span class="sxs-lookup"><span data-stu-id="fa983-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="fa983-139">Kullanıcılarınız için özelliği geri dönmek için iki Azure AD URL'leri (https://autologon.microsoftazuread-sso.com ve https://aadg.windows.net.nsatc.net) eklemek için kullanıcıların Intranet bölgesi ayarlarını Active Directory'de Grup İlkesi aracılığıyla gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa983-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="fa983-140">(Bunu kümesini güvenilen site URL'lerin Internet Explorer ile paylaşır) aşağıdaki yönergeleri yalnızca Internet Explorer ve Google Chrome için Windows üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="fa983-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="fa983-141">Mozilla Firefox ve Mac üzerinde Google Chrome ayarlama yönergeleri için sonraki bölüme okuma</span><span class="sxs-lookup"><span data-stu-id="fa983-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="fa983-142">Neden kullanıcıların Intranet bölgesi ayarlarını değiştirmeniz gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="fa983-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="fa983-143">Varsayılan olarak, tarayıcının bir URL sağ bölgesi (Internet veya Intranet) otomatik olarak hesaplar.</span><span class="sxs-lookup"><span data-stu-id="fa983-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="fa983-144">Örneğin, (URL nokta içerdiğinden) http://intranet.contoso.com/ Internet bölgesine eşlendi ancak http://contoso/ Intranet bölgesine eşlenir.</span><span class="sxs-lookup"><span data-stu-id="fa983-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="fa983-145">URL'sini tarayıcının Intranet bölgesine açıkça eklenmediği sürece tarayıcıları bir bulut uç noktası için - iki Azure AD URL'leri gibi-Kerberos biletleri gönderme.</span><span class="sxs-lookup"><span data-stu-id="fa983-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="fa983-146">Ayrıntılı adımlar</span><span class="sxs-lookup"><span data-stu-id="fa983-146">Detailed steps</span></span>

1. <span data-ttu-id="fa983-147">Grup İlkesi yönetim aracını açın.</span><span class="sxs-lookup"><span data-stu-id="fa983-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="fa983-148">Bazı uygulanan Grup İlkesi düzenleme veya tüm kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="fa983-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="fa983-149">Bu örnekte, kullandığımız **varsayılan etki alanı ilkesi**.</span><span class="sxs-lookup"><span data-stu-id="fa983-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="fa983-150">Gidin **Kullanıcı Yapılandırması\Yönetim Şablonları\Windows Bileşenleri\Internet Explorer\Internet Denetim Panel\Security sayfası** seçip **siteyi bölgeye ataması listesi**.</span><span class="sxs-lookup"><span data-stu-id="fa983-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="fa983-151">![Çoklu oturum açma](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="fa983-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="fa983-152">İlkeyi etkinleştirin ve aşağıdaki değerleri (Azure AD URL'ler Kerberos biletleri yere iletilmez) ve veri girin (*1* Intranet bölgesine gösterir) iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="fa983-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="fa983-153">Bu kullanıcılar paylaşılan bilgi noktaları üzerinde - imzalama, bazı kullanıcıların sorunsuz SSO - Örneğin, kullanarak izin vermeyecek şekilde istiyorsanız önceki değerleri kümesine *4*.</span><span class="sxs-lookup"><span data-stu-id="fa983-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="fa983-154">Bu eylem, Azure AD URL'leri kısıtlı bölgesine ekler ve sorunsuz SSO her zaman başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fa983-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="fa983-155">Tıklatın **Tamam** ve **Tamam** yeniden.</span><span class="sxs-lookup"><span data-stu-id="fa983-155">Click **OK** and **OK** again.</span></span>

![Çoklu oturum açma](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="fa983-157">Tarayıcı konuları</span><span class="sxs-lookup"><span data-stu-id="fa983-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="fa983-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="fa983-158">Mozilla Firefox</span></span>

<span data-ttu-id="fa983-159">Mozilla Firefox otomatik olarak Kerberos kimlik doğrulamasını yapmaz.</span><span class="sxs-lookup"><span data-stu-id="fa983-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="fa983-160">Azure AD URL'leri Firefox ayarlarına aşağıdaki adımları kullanarak el ile eklemek her kullanıcının vardır:</span><span class="sxs-lookup"><span data-stu-id="fa983-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="fa983-161">Firefox çalıştırın ve girin `about:config` adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="fa983-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="fa983-162">Gördüğünüz herhangi bir bildirim yok sayın.</span><span class="sxs-lookup"><span data-stu-id="fa983-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="fa983-163">Arama **network.negotiate auth.trusted URI'ler** tercih.</span><span class="sxs-lookup"><span data-stu-id="fa983-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="fa983-164">Bu tercih Kerberos kimlik doğrulaması için Firefox'in Güvenilen siteler listelenir.</span><span class="sxs-lookup"><span data-stu-id="fa983-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="fa983-165">Sağ tıklayın ve "Değiştir"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="fa983-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="fa983-166">Girin "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" alanında.</span><span class="sxs-lookup"><span data-stu-id="fa983-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="fa983-167">"Tamam" düğmesini tıklatın ve tarayıcıyı kapatıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="fa983-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="fa983-168">Mac OS Safari</span><span class="sxs-lookup"><span data-stu-id="fa983-168">Safari on Mac OS</span></span>

<span data-ttu-id="fa983-169">Mac OS çalıştıran makine için AD alanına katılmış olmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fa983-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="fa983-170">Bunu nasıl yönergeler bkz [burada](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="fa983-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="fa983-171">Mac OS Google Chrome</span><span class="sxs-lookup"><span data-stu-id="fa983-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="fa983-172">Mac OS ve diğer Windows olmayan platformlarda Google Chrome için başvurmak [bu makalede](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) tümleşik kimlik doğrulaması için beyaz liste Azure AD URL'ler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="fa983-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="fa983-173">Azure AD URL'lerine Firefox ve Google Chrome Mac Kullanıcıları geri dönmek için üçüncü taraf Active Directory Grup İlkesi uzantıları kullanarak bu makalenin kapsamı dışında değildir.</span><span class="sxs-lookup"><span data-stu-id="fa983-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="fa983-174">Bilinen sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="fa983-174">Known limitations</span></span>

<span data-ttu-id="fa983-175">Sorunsuz SSO Firefox ve kenar tarayıcılarda özel gözatma modunda çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="fa983-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="fa983-176">Tarayıcı geliştirilmiş koruma modunda çalışıyorsa, ayrıca Internet Explorer, işe yaramaz.</span><span class="sxs-lookup"><span data-stu-id="fa983-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fa983-177">Biz son müşteri bildirilen sorunları araştırmak sınır desteği geri.</span><span class="sxs-lookup"><span data-stu-id="fa983-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="fa983-178">4. adım: Test özelliği</span><span class="sxs-lookup"><span data-stu-id="fa983-178">Step 4: Test the feature</span></span>

<span data-ttu-id="fa983-179">Belirli bir kullanıcı için özelliğini sınamak için emin _tüm_ aşağıdaki koşulların karşılandığından:</span><span class="sxs-lookup"><span data-stu-id="fa983-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="fa983-180">Kullanıcı bir kurumsal aygıtta oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fa983-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="fa983-181">Cihaz daha önce Active Directory (AD) etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="fa983-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="fa983-182">Cihaz için etki alanı denetleyicisi (DC), Kurumsal kablolu veya kablosuz ağ üzerindeki veya bir VPN bağlantısı gibi bir uzaktan erişim bağlantısı aracılığıyla doğrudan bir bağlantı vardır.</span><span class="sxs-lookup"><span data-stu-id="fa983-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="fa983-183">Sahip olduğunuz [özelliği alındı](##step-3-roll-out-the-feature) Grup İlkesi kullanarak bu kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="fa983-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="fa983-184">Burada yalnızca kullanıcı adı ve parola kullanıcının girdiği senaryoyu test etmek için:</span><span class="sxs-lookup"><span data-stu-id="fa983-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="fa983-185">Oturum *https://myapps.microsoft.com/* yeni bir özel tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="fa983-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="fa983-186">Burada kullanıcının kullanıcı adı veya parola girmesi gerekmez senaryoyu test etmek için:</span><span class="sxs-lookup"><span data-stu-id="fa983-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="fa983-187">Oturum *https://myapps.microsoft.com/contoso.onmicrosoft.com* yeni bir özel tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="fa983-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="fa983-188">Değiştir "*contoso*", kiracının ada sahip.</span><span class="sxs-lookup"><span data-stu-id="fa983-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="fa983-189">Veya oturum *https://myapps.microsoft.com/contoso.com* yeni bir özel tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="fa983-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="fa983-190">Değiştir "*contoso.com*" kiracınızda doğrulanmış bir etki alanıyla (bir Federasyon etki alanı değil).</span><span class="sxs-lookup"><span data-stu-id="fa983-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="fa983-191">5. adım: anahtarlar üzerinden alma</span><span class="sxs-lookup"><span data-stu-id="fa983-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="fa983-192">2. adımda, Azure AD Connect (Azure AD temsil eder) bilgisayar hesapları sorunsuz SSO etkin tüm ormanlardaki AD oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fa983-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="fa983-193">İçinde daha ayrıntılı bilgi [burada](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="fa983-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="fa983-194">Gelişmiş güvenlik için Kerberos sık bu bilgisayar hesaplarının şifre çözme anahtarlarını alma önerilir.</span><span class="sxs-lookup"><span data-stu-id="fa983-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fa983-195">Bu adım gerekmez _hemen_ özelliği etkinleştirdikten sonra.</span><span class="sxs-lookup"><span data-stu-id="fa983-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="fa983-196">En az 30 günde Kerberos şifre çözme anahtarlarını alma.</span><span class="sxs-lookup"><span data-stu-id="fa983-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa983-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa983-197">Next steps</span></span>

- <span data-ttu-id="fa983-198">[**Teknik derinlemesine** ](active-directory-aadconnect-sso-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.</span><span class="sxs-lookup"><span data-stu-id="fa983-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="fa983-199">[**Sık sorulan sorular** ](active-directory-aadconnect-sso-faq.md) -sık sorulan sorulara yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="fa983-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="fa983-200">[**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -özelliği ile ilgili genel sorunları çözmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fa983-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="fa983-201">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="fa983-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
