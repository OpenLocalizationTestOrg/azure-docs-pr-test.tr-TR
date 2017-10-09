---
title: "aaaAzure Active Directory kimlik koruması Kılavuzu | Microsoft Docs"
description: "Nasıl Azure AD Identity Protection toolimit hello yeteneğini bir saldırganın tooexploit güvenliği aşılmış kimlik veya cihaz ve bir kimlik veya şüpheli veya bilinen toobe öncekinden bir aygıtı tehlikeye toosecure sağlar öğrenin."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="e1699-104">Azure Active Directory kimlik koruması Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="e1699-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="e1699-105">Bu playbook size yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="e1699-105">This playbook helps you to:</span></span>

* <span data-ttu-id="e1699-106">Merhaba kimlik koruması ortamında verileri benzetirme risk olaylarına ve güvenlik açıkları ile doldurma</span><span class="sxs-lookup"><span data-stu-id="e1699-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="e1699-107">Risk bağlı olarak koşullu erişim ilkeleri Ayarla ve bu ilkeler hello etkisini test etme</span><span class="sxs-lookup"><span data-stu-id="e1699-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="e1699-108">Risk olaylarını benzetimini yapma</span><span class="sxs-lookup"><span data-stu-id="e1699-108">Simulating Risk Events</span></span>
<span data-ttu-id="e1699-109">Bu bölümde risk olayı türleri aşağıdaki hello benzetimi için adımlara sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1699-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="e1699-110">Oturum açma işlemleri anonim IP adreslerinden (kolay)</span><span class="sxs-lookup"><span data-stu-id="e1699-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="e1699-111">Oturum açma işlemleri tanınmayan konumlardan (Orta)</span><span class="sxs-lookup"><span data-stu-id="e1699-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="e1699-112">Mümkün olmayan seyahat tooatypical konumları (zor)</span><span class="sxs-lookup"><span data-stu-id="e1699-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="e1699-113">Diğer risk olaylarını güvenli bir şekilde benzetimi yapılamaz.</span><span class="sxs-lookup"><span data-stu-id="e1699-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="e1699-114">Anonim IP adreslerinden oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="e1699-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="e1699-115">Bu riski olay türü açan başarıyla anonim Ara sunucu IP adresi olarak tanımlanan bir IP adresinden kullanıcıları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1699-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="e1699-116">Bu proxy'leri olan kendi aygıtın IP adresi toohide istediğiniz kişiler tarafından kullanılan ve kötü amaçlı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e1699-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="e1699-117">**bir oturum açma toosimulate anonim bir IP adresinden gerçekleştirme adımları izleyerek hello**:</span><span class="sxs-lookup"><span data-stu-id="e1699-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="e1699-118">Merhaba karşıdan [Tor tarayıcı](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="e1699-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="e1699-119">Merhaba Tor tarayıcı kullanarak gidin çok[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e1699-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="e1699-120">Merhaba hello tooappear istediğiniz hello hesabının kimlik bilgilerini girin **anonim IP adreslerinden gerçekleştirilen oturum açma işlemleri** rapor.</span><span class="sxs-lookup"><span data-stu-id="e1699-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="e1699-121">Merhaba oturum açma hello kimlik koruması Panoda 5 dakika içinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="e1699-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="e1699-122">Alışılmadık konumlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="e1699-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="e1699-123">Merhaba tanınmayan konumlardan oturum açma konumları göz önünde bulundurur bir oturum açma gerçek zamanlı değerlendirme mekanizması riskidir (IP, enlem / boylam ve ASN) toodetermine yeni / tanınmayan konumları.</span><span class="sxs-lookup"><span data-stu-id="e1699-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="e1699-124">Merhaba sistem depolar önceki IP'leri, enlem / boylam ve bir kullanıcının Asn'ler bu toobe tanıdık konumları olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="e1699-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="e1699-125">Merhaba oturum açma konumu hello varolan tanıdık konumlardan herhangi birinde eşleşmiyorsa bir oturum açma konumu tanınmayan olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="e1699-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="e1699-126">Azure Active Directory kimlik koruması:</span><span class="sxs-lookup"><span data-stu-id="e1699-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="e1699-127">14 gün boyunca, tüm yeni konumlar tanınmayan konumları olarak işaretlemez bir ilk öğrenme süre sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e1699-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="e1699-128">oturum açma işlemleri hakkında bilgi sahibi aygıtları ve coğrafi olarak Kapat tooan varolan tanıdık konumunun konumları yok sayar.</span><span class="sxs-lookup"><span data-stu-id="e1699-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="e1699-129">toosimulate tanınmayan konumlardan toosign bir konum ve hello hesap öğesinden önce oturum açtığı değil cihaz sizde.</span><span class="sxs-lookup"><span data-stu-id="e1699-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="e1699-130">**bir oturum açma tanınmayan bir konumdan toosimulate gerçekleştirme adımları izleyerek hello**:</span><span class="sxs-lookup"><span data-stu-id="e1699-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="e1699-131">Oturum açma en az bir 14 gün geçmiş olan bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="e1699-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="e1699-132">Ya da yapın:</span><span class="sxs-lookup"><span data-stu-id="e1699-132">Do either:</span></span>
   
   <span data-ttu-id="e1699-133">a.</span><span class="sxs-lookup"><span data-stu-id="e1699-133">a.</span></span> <span data-ttu-id="e1699-134">Bir VPN kullanırken, çok gidin[https://myapps.microsoft.com](https://myapps.microsoft.com) ve hello toosimulate hello risk olayı için istediğiniz hello hesabının kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="e1699-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="e1699-135">b.</span><span class="sxs-lookup"><span data-stu-id="e1699-135">b.</span></span> <span data-ttu-id="e1699-136">Bir ilişkilendirme (önerilmez) hello hesabın kimlik bilgilerini kullanarak farklı bir konuma toosign içinde isteyin.</span><span class="sxs-lookup"><span data-stu-id="e1699-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="e1699-137">Merhaba oturum açma hello kimlik koruması Panoda 5 dakika içinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="e1699-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="e1699-138">Mümkün olmayan seyahat tooatypical konumu</span><span class="sxs-lookup"><span data-stu-id="e1699-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="e1699-139">Merhaba algoritması machine learning tooweed yanlış pozitifler tanıdık aygıtlardan mümkün olmayan seyahat veya oturum açmalardan hello dizininde diğer kullanıcılar tarafından kullanılan VPN'ler gibi çıkışı kullandığından hello mümkün olmayan seyahat koşul benzetimi zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1699-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="e1699-140">Ayrıca, risk olaylarını oluşturma işlemi başlamadan önce hello algoritması hello kullanıcı için bir oturum açma geçmişine 3 too14 gün gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e1699-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="e1699-141">**toosimulate bir mümkün olmayan seyahat tooatypical konum gerçekleştirme adımları izleyerek hello**:</span><span class="sxs-lookup"><span data-stu-id="e1699-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="e1699-142">Standart, tarayıcı kullanarak gidin çok[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e1699-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="e1699-143">Merhaba bir mümkün olmayan seyahat risk olayı toogenerate istediğiniz hello hesabının kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="e1699-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="e1699-144">Kullanıcı Aracısı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1699-144">Change your user agent.</span></span> <span data-ttu-id="e1699-145">Geliştirici Araçları'ndan kullanıcı aracısı Internet Explorer'da değiştirmek veya kullanıcı aracınız Firefox veya kullanıcı aracısı değiştirici Eklentisi'ni kullanarak Chrome değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1699-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="e1699-146">IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1699-146">Change your IP address.</span></span> <span data-ttu-id="e1699-147">VPN, Tor eklentisi kullanılarak veya farklı bir veri merkezinde Azure içinde yeni bir makine dönmesini IP adresiniz değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1699-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="e1699-148">Oturum çok açma[https://myapps.microsoft.com](https://myapps.microsoft.com) hello olarak önce ve sonra hello önceki oturum açma birkaç dakika içinde aynı kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e1699-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="e1699-149">Merhaba oturum açma hello Identity Protection panosunda 2-4 saat içinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="e1699-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="e1699-150">Söz konusu modelleri hello karmaşık machine learning nedeniyle, bu toplanma değil şansı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e1699-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="e1699-151">Birden çok Azure AD hesapları için bu adımları tooreplicate isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1699-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="e1699-152">Güvenlik açıkları benzetimini yapma</span><span class="sxs-lookup"><span data-stu-id="e1699-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="e1699-153">Güvenlik açıkları tarafından hatalı aktör yararlanan bir Azure AD ortamda zayıf giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1699-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="e1699-154">Şu anda açık 3 türlerinin diğer özelliklerden Azure ad içinde Azure AD Identity Protection çıkmış.</span><span class="sxs-lookup"><span data-stu-id="e1699-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="e1699-155">Bu özellikler ayarlandıktan sonra bu güvenlik açıklarından otomatik olarak hello Identity Protection panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e1699-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="e1699-156">Azure AD [çok faktörlü kimlik doğrulaması?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e1699-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="e1699-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1699-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="e1699-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e1699-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="e1699-159">Kullanıcı güvenlik aşılması riski</span><span class="sxs-lookup"><span data-stu-id="e1699-159">User compromise risk</span></span>
<span data-ttu-id="e1699-160">**tootest kullanıcı güvenliğinin aşılmasına risk, aşağıdaki adımları hello gerçekleştirmek**:</span><span class="sxs-lookup"><span data-stu-id="e1699-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="e1699-161">Oturum çok açma[https://portal.azure.com](https://portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="e1699-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="e1699-162">Çok gidin**kimlik koruması**.</span><span class="sxs-lookup"><span data-stu-id="e1699-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="e1699-163">Merhaba ana üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e1699-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="e1699-164">Merhaba üzerinde **Portalı Ayarları** dikey altında **güvenlik kuralları**, tıklatın **kullanıcı güvenliğinin aşılmasına riski**.</span><span class="sxs-lookup"><span data-stu-id="e1699-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="e1699-165">Merhaba üzerinde **Risk oturum** dikey penceresinde kapatma **etkinleştir kural** kapalı ve ardından **kaydetmek** ayarları.</span><span class="sxs-lookup"><span data-stu-id="e1699-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="e1699-166">Belirtilen kullanıcı hesabı için bir tanınmayan benzetimini konumlar veya anonim IP risk olayı.</span><span class="sxs-lookup"><span data-stu-id="e1699-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="e1699-167">Bu çok yükseltmesine hello kullanıcı risk düzeyi bu kullanıcı için**orta**.</span><span class="sxs-lookup"><span data-stu-id="e1699-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="e1699-168">Birkaç dakika bekleyin ve kullanıcı için bu kullanıcı düzeyini doğrulayın **orta**.</span><span class="sxs-lookup"><span data-stu-id="e1699-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="e1699-169">Toohello Git **Portalı Ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="e1699-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="e1699-170">Merhaba üzerinde **kullanıcı güvenliğinin aşılmasına Risk** dikey altında **etkinleştir kural**seçin **üzerinde** .</span><span class="sxs-lookup"><span data-stu-id="e1699-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="e1699-171">Seçenekler aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="e1699-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="e1699-172">a.</span><span class="sxs-lookup"><span data-stu-id="e1699-172">a.</span></span> <span data-ttu-id="e1699-173">tooblock, select **orta** altında **blok oturum**.</span><span class="sxs-lookup"><span data-stu-id="e1699-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="e1699-174">b.</span><span class="sxs-lookup"><span data-stu-id="e1699-174">b.</span></span> <span data-ttu-id="e1699-175">tooenforce güvenli parola değişikliği, select **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="e1699-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="e1699-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1699-176">Click **Save**.</span></span>
12. <span data-ttu-id="e1699-177">Bir kullanıcı bir yükseltilmiş risk düzeyi ile kullanarak oturum açma tarafından risk bağlı olarak koşullu erişim artık test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1699-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="e1699-178">Merhaba kullanıcı risk Orta ise, ilkenizin hello yapılandırmasına bağlı olarak, oturum açma işleminiz olabilir ya da engellenen ya da toochange zorlanır parolanızı.</span><span class="sxs-lookup"><span data-stu-id="e1699-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="e1699-179">
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    </span><span class="sxs-lookup"><span data-stu-id="e1699-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="e1699-180">Oturum açma riski</span><span class="sxs-lookup"><span data-stu-id="e1699-180">Sign-in risk</span></span>
<span data-ttu-id="e1699-181">**tootest bir oturum açma riski hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1699-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1699-182">Oturum çok açma[https://portal.azure.com ](https://portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="e1699-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="e1699-183">Çok gidin**kimlik koruması**.</span><span class="sxs-lookup"><span data-stu-id="e1699-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="e1699-184">Merhaba ana üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e1699-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="e1699-185">Merhaba üzerinde **Portalı Ayarları** dikey altında **güvenlik kuralları**, tıklatın **risk oturum**.</span><span class="sxs-lookup"><span data-stu-id="e1699-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="e1699-186">Merhaba üzerinde ** Risk oturum ** dikey penceresinde, select **üzerinde** altında **etkinleştir kural**.</span><span class="sxs-lookup"><span data-stu-id="e1699-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="e1699-187">Seçenekler aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="e1699-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="e1699-188">a.</span><span class="sxs-lookup"><span data-stu-id="e1699-188">a.</span></span> <span data-ttu-id="e1699-189">tooblock, select **orta** altında **blok oturum açın**</span><span class="sxs-lookup"><span data-stu-id="e1699-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="e1699-190">b.</span><span class="sxs-lookup"><span data-stu-id="e1699-190">b.</span></span> <span data-ttu-id="e1699-191">tooenforce güvenli parola değişikliği, select **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="e1699-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="e1699-192">Blok altında select Orta tooblock, oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1699-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="e1699-193">tooenforce çok faktörlü kimlik doğrulaması, select **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="e1699-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="e1699-194">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1699-194">Click on **Save**.</span></span>
10. <span data-ttu-id="e1699-195">Merhaba tanınmayan konumlardan taklit ederek risk bağlı olarak koşullu erişim artık sınayabilirsiniz veya her ikisi de olduklarından anonim IP risk olayları **orta** risk olayları.</span><span class="sxs-lookup"><span data-stu-id="e1699-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="e1699-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="e1699-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="e1699-197">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e1699-197">See also</span></span>
* [<span data-ttu-id="e1699-198">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="e1699-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

