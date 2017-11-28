---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma - hızlı başlangıç | Microsoft Docs"
description: "Bu makalede, Azure Active Directory sorunsuz çoklu oturum açma ile tooget nasıl başlatılacağını açıklar."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="d3913-104">Azure Active Directory sorunsuz çoklu oturum açma: Hızlı Başlangıç</span><span class="sxs-lookup"><span data-stu-id="d3913-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="d3913-105">Nasıl toodeploy sorunsuz SSO</span><span class="sxs-lookup"><span data-stu-id="d3913-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="d3913-106">Azure Active Directory sorunsuz çoklu oturum açma (Azure AD sorunsuz SSO) otomatik olarak imzalar kurumsal masaüstü bağlı tooyour Kurumsal ağlarında olduklarında kullanıcıların.</span><span class="sxs-lookup"><span data-stu-id="d3913-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="d3913-107">Şirket içinde ek bileşenleri gerek kalmadan tooyour bulut tabanlı uygulamalar, kullanıcıların kolay erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3913-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d3913-108">Merhaba sorunsuz SSO özelliği şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="d3913-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="d3913-109">toodeploy sorunsuz SSO, toofollow gereken adımları:</span><span class="sxs-lookup"><span data-stu-id="d3913-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="d3913-110">1. adım: Önkoşul denetimi</span><span class="sxs-lookup"><span data-stu-id="d3913-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="d3913-111">Önkoşullar aşağıdaki o hello yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="d3913-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="d3913-112">Azure AD Connect sunucusunu ayarlama: kullanırsanız [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md) , oturum açma yöntemi başka bir eylem gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d3913-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="d3913-113">Kullanırsanız [parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md) , oturum açma yöntemi olarak ve Azure AD Connect ve Azure AD arasında bir güvenlik duvarı varsa, emin olun:</span><span class="sxs-lookup"><span data-stu-id="d3913-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="d3913-114">Sürümleri 1.1.484.0 kullanıyorsanız veya Azure AD Connect sonraki.</span><span class="sxs-lookup"><span data-stu-id="d3913-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="d3913-115">Azure AD Connect ile iletişim kurabilir `*.msappproxy.net` URL'leri ve üstünde bağlantı noktası 443'tür.</span><span class="sxs-lookup"><span data-stu-id="d3913-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="d3913-116">Yalnızca asıl kullanıcı oturum açma işlemleri için hello özelliğini etkinleştirdiğinizde bu geçerli bir önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="d3913-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="d3913-117">Azure AD Connect, doğrudan IP bağlantıları toohello yapabilir [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d3913-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="d3913-118">Yeniden yalnızca hello özelliğini etkinleştirdiğinizde bu önkoşulu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d3913-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="d3913-119">TooAzure AD eşitleme her bir AD orman için etki alanı yönetici kimlik bilgilerine ihtiyacınız (Azure AD Connect'i kullanarak) ve olan kullanıcılar için sorunsuz SSO tooenable istiyor.</span><span class="sxs-lookup"><span data-stu-id="d3913-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="d3913-120">2. adım: hello özelliğini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="d3913-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="d3913-121">Sorunsuz SSO kullanarak etkinleştirilebilir [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d3913-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="d3913-122">Azure AD Connect yeni yüklemesini yapıyorsanız, hello seçin [özel yükleme yolu](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d3913-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="d3913-123">Merhaba "Kullanıcı oturum açma" sayfanın hello "Etkinleştirme çoklu oturum açma" seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="d3913-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - kullanıcı oturum açma](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="d3913-125">Azure AD Connect yüklemesi zaten varsa, "Değişiklik kullanıcı oturum açma sayfasında" Azure AD Connect seçin ve "İleri" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d3913-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="d3913-126">Ardından hello "Etkinleştirme çoklu oturum açma" seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="d3913-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - değişiklik kullanıcı oturum açma](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="d3913-128">Toohello "Etkinleştirme çoklu oturum açma" sayfasına ulaşana kadar hello sihirbaza devam edin.</span><span class="sxs-lookup"><span data-stu-id="d3913-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="d3913-129">TooAzure AD eşitlemek için her bir AD orman etki alanı yönetici kimlik bilgilerini girin (Azure AD Connect'i kullanarak) ve olan kullanıcılar için sorunsuz SSO tooenable istiyor.</span><span class="sxs-lookup"><span data-stu-id="d3913-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="d3913-130">Merhaba Sihirbazı tamamlandıktan sonra Kiracı'sorunsuz SSO etkin.</span><span class="sxs-lookup"><span data-stu-id="d3913-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="d3913-131">Merhaba etki alanı yönetici kimlik bilgileri Azure AD Connect veya Azure AD depolanmaz, ancak yalnızca kullanılan tooenable hello özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d3913-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="d3913-132">Bu yönergeler tooverify sorunsuz SSO doğru etkinleştirdiyseniz izleyin:</span><span class="sxs-lookup"><span data-stu-id="d3913-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="d3913-133">İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello kiracınız için genel yönetici kimlik bilgileriyle.</span><span class="sxs-lookup"><span data-stu-id="d3913-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="d3913-134">Seçin **Azure Active Directory** hello sol gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="d3913-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="d3913-135">Seçin **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="d3913-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="d3913-136">Bu hello doğrulayın **sorunsuz çoklu oturum açma** özelliği gösterildiğinden **etkin**.</span><span class="sxs-lookup"><span data-stu-id="d3913-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure portal - Azure AD Connect dikey penceresi](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="d3913-138">3. adım: hello özelliği alma</span><span class="sxs-lookup"><span data-stu-id="d3913-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="d3913-139">tooroll hello özelliği tooyour kullanıcılar çıkışı tooadd iki Azure AD URL'leri (https://autologon.microsoftazuread-sso.com ve https://aadg.windows.net.nsatc.net) toousers'Intranet bölgesi ayarlarını Active Directory'de Grup İlkesi aracılığıyla gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3913-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="d3913-140">(Bu güvenilen site URL'leri kümesini Internet Explorer ile paylaşıyorsa) Windows Internet Explorer ve Google Chrome için yalnızca çalışma yönergeleri aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="d3913-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="d3913-141">Mozilla Firefox ve Mac üzerinde Google Chrome yönergeleri tooset için sonraki bölüme Hello okuma</span><span class="sxs-lookup"><span data-stu-id="d3913-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="d3913-142">Neden toomodify kullanıcıların Intranet bölgesi ayarlarını gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="d3913-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="d3913-143">Varsayılan olarak, hello tarayıcı bir URL'den hello sağ bölgesi (Internet veya Intranet) otomatik olarak hesaplar.</span><span class="sxs-lookup"><span data-stu-id="d3913-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="d3913-144">Örneğin, (Merhaba URL'si nokta içerdiğinden) http://intranet.contoso.com/ eşlenen toohello Internet bölgesi iken http://contoso/ eşlenen toohello Intranet bölgesi, ' dir.</span><span class="sxs-lookup"><span data-stu-id="d3913-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="d3913-145">URL'sini açıkça toohello tarayıcısının Intranet eklenmediği sürece tarayıcılar - gibi hello iki Azure AD URL'leri - Kerberos biletleri tooa bulut uç noktası göndermeyin.</span><span class="sxs-lookup"><span data-stu-id="d3913-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="d3913-146">Ayrıntılı adımlar</span><span class="sxs-lookup"><span data-stu-id="d3913-146">Detailed steps</span></span>

1. <span data-ttu-id="d3913-147">Merhaba Grup İlkesi yönetim aracını açın.</span><span class="sxs-lookup"><span data-stu-id="d3913-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="d3913-148">Merhaba uygulanan toosome ya da tüm kullanıcıları Grup İlkesi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="d3913-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="d3913-149">Bu örnekte, kullandığımız hello **varsayılan etki alanı ilkesi**.</span><span class="sxs-lookup"><span data-stu-id="d3913-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="d3913-150">Çok gidin**Kullanıcı Yapılandırması\Yönetim Şablonları\Windows Bileşenleri\Internet Explorer\Internet Denetim Panel\Security sayfası** seçip **tooZone ataması listesi Site**.</span><span class="sxs-lookup"><span data-stu-id="d3913-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="d3913-151">![Çoklu oturum açma](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="d3913-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="d3913-152">Merhaba ilkesini etkinleştirmek ve değerleri (Azure AD URL'ler Kerberos biletleri yere iletilmez) aşağıdaki hello ve veri girin (*1* Intranet bölgesine gösterir) hello iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="d3913-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="d3913-153">Bu kullanıcılar paylaşılan bilgi noktaları üzerinde - imzalama, bazı kullanıcıların sorunsuz SSO - Örneğin, kullanarak toodisallow istiyorsanız değerleri çok önceki hello ayarlayın*4*.</span><span class="sxs-lookup"><span data-stu-id="d3913-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="d3913-154">Bu eylemin hello Azure AD URL'leri toohello Yasak Bölge ekler ve sorunsuz SSO hello zaman başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d3913-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="d3913-155">Tıklatın **Tamam** ve **Tamam** yeniden.</span><span class="sxs-lookup"><span data-stu-id="d3913-155">Click **OK** and **OK** again.</span></span>

![Çoklu oturum açma](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="d3913-157">Tarayıcı konuları</span><span class="sxs-lookup"><span data-stu-id="d3913-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="d3913-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d3913-158">Mozilla Firefox</span></span>

<span data-ttu-id="d3913-159">Mozilla Firefox otomatik olarak Kerberos kimlik doğrulamasını yapmaz.</span><span class="sxs-lookup"><span data-stu-id="d3913-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="d3913-160">Her kullanıcının hello aşağıdaki adımları kullanarak hello Azure AD URL'leri tootheir Firefox ayarlarını eklemek toomanually vardır:</span><span class="sxs-lookup"><span data-stu-id="d3913-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="d3913-161">Firefox çalıştırın ve girin `about:config` hello adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="d3913-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="d3913-162">Gördüğünüz herhangi bir bildirim yok sayın.</span><span class="sxs-lookup"><span data-stu-id="d3913-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="d3913-163">Merhaba Ara **network.negotiate auth.trusted URI'ler** tercih.</span><span class="sxs-lookup"><span data-stu-id="d3913-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="d3913-164">Bu tercih Kerberos kimlik doğrulaması için Firefox'in Güvenilen siteler listelenir.</span><span class="sxs-lookup"><span data-stu-id="d3913-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="d3913-165">Sağ tıklayın ve "Değiştir"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="d3913-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="d3913-166">Girin "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" Merhaba alanında.</span><span class="sxs-lookup"><span data-stu-id="d3913-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="d3913-167">"Tamam" düğmesini tıklatın ve hello tarayıcı yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="d3913-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="d3913-168">Mac OS Safari</span><span class="sxs-lookup"><span data-stu-id="d3913-168">Safari on Mac OS</span></span>

<span data-ttu-id="d3913-169">Mac OS çalıştıran bu hello makine birleştirilmiş tooAD olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3913-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="d3913-170">Yönergeler Bkz toodo, [burada](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="d3913-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="d3913-171">Mac OS Google Chrome</span><span class="sxs-lookup"><span data-stu-id="d3913-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="d3913-172">Mac OS ve diğer Windows olmayan platformlarda Google Chrome için çok başvuran[bu makalede](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) nasıl toowhitelist hello tümleşik kimlik doğrulaması için Azure AD URL'ler hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d3913-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="d3913-173">Üçüncü taraf Active Directory Grup İlkesi'ni kullanarak bu makalenin kapsamı dışında Mac Kullanıcıları hello Azure AD URL'leri tooFirefox ve Google Chrome uzantıları tooroll değildir.</span><span class="sxs-lookup"><span data-stu-id="d3913-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="d3913-174">Bilinen sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="d3913-174">Known limitations</span></span>

<span data-ttu-id="d3913-175">Sorunsuz SSO Firefox ve kenar tarayıcılarda özel gözatma modunda çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="d3913-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="d3913-176">Merhaba tarayıcı geliştirilmiş koruma modunda çalışıyorsa, ayrıca Internet Explorer, işe yaramaz.</span><span class="sxs-lookup"><span data-stu-id="d3913-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d3913-177">Biz son kenar tooinvestigate desteği müşteri bildirilen sorunlar geri.</span><span class="sxs-lookup"><span data-stu-id="d3913-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="d3913-178">4. adım: Test hello özelliği</span><span class="sxs-lookup"><span data-stu-id="d3913-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="d3913-179">tootest hello özellik belirli bir kullanıcı için olmak _tüm_ koşullar aşağıdaki hello olan yerinde:</span><span class="sxs-lookup"><span data-stu-id="d3913-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="d3913-180">Merhaba kullanıcı kurumsal bir cihazda oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d3913-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="d3913-181">Merhaba aygıt daha önceden birleştirilmiş tooyour Active Directory (AD) etki alanı olmuştur.</span><span class="sxs-lookup"><span data-stu-id="d3913-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="d3913-182">Merhaba, doğrudan bağlantı tooyour etki alanı denetleyicisi (DC), hello şirket ağındaki kablolu veya kablosuz veya VPN bağlantısı gibi bir uzaktan erişim bağlantısı aracılığıyla aygıtın.</span><span class="sxs-lookup"><span data-stu-id="d3913-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="d3913-183">Sahip olduğunuz [hello özelliği alındı](##step-3-roll-out-the-feature) toothis kullanıcı Grup İlkesi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d3913-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="d3913-184">Burada hello kullanıcı adı, ancak değil hello parola hello kullanıcının girdiği tootest hello senaryo:</span><span class="sxs-lookup"><span data-stu-id="d3913-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="d3913-185">Oturum *https://myapps.microsoft.com/* yeni bir özel tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="d3913-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="d3913-186">tootest hello senaryo hello kullanıcı tooenter hello kullanıcı adı veya hello parola burada sahip değil:</span><span class="sxs-lookup"><span data-stu-id="d3913-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="d3913-187">Oturum *https://myapps.microsoft.com/contoso.onmicrosoft.com* yeni bir özel tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="d3913-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="d3913-188">Değiştir "*contoso*", kiracının ada sahip.</span><span class="sxs-lookup"><span data-stu-id="d3913-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="d3913-189">Veya oturum *https://myapps.microsoft.com/contoso.com* yeni bir özel tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="d3913-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="d3913-190">Değiştir "*contoso.com*" kiracınızda doğrulanmış bir etki alanıyla (bir Federasyon etki alanı değil).</span><span class="sxs-lookup"><span data-stu-id="d3913-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="d3913-191">5. adım: anahtarlar üzerinden alma</span><span class="sxs-lookup"><span data-stu-id="d3913-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="d3913-192">2. adımda, Azure AD Connect (Azure AD temsil eder) bilgisayar hesapları sorunsuz SSO etkin tüm hello AD ormanlardaki oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3913-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="d3913-193">İçinde daha ayrıntılı bilgi [burada](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="d3913-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="d3913-194">Gelişmiş güvenlik için bu bilgisayar hesaplarının hello Kerberos şifre çözme anahtarlarını sık alma önerilir.</span><span class="sxs-lookup"><span data-stu-id="d3913-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d3913-195">Bu adım toodo gerekmeyen _hemen_ hello özelliği etkinleştirdikten sonra.</span><span class="sxs-lookup"><span data-stu-id="d3913-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="d3913-196">Merhaba Kerberos şifre çözme anahtarları üzerinde en az 30 günde alma.</span><span class="sxs-lookup"><span data-stu-id="d3913-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3913-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3913-197">Next steps</span></span>

- <span data-ttu-id="d3913-198">[**Teknik derinlemesine** ](active-directory-aadconnect-sso-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.</span><span class="sxs-lookup"><span data-stu-id="d3913-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="d3913-199">[**Sık sorulan sorular** ](active-directory-aadconnect-sso-faq.md) -toofrequently sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3913-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="d3913-200">[**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d3913-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="d3913-201">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="d3913-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
