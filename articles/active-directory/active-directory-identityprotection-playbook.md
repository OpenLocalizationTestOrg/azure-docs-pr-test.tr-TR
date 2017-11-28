---
title: "Azure Active Directory kimlik koruması Kılavuzu | Microsoft Docs"
description: "Azure AD kimlik koruması nasıl yeteneğini bir saldırgan güvenliği aşılmış kimlik veya aygıt yararlanmaya ve güvenli bir kimlik veya önceden şüpheli veya tehlikeye bilinen bir cihaz için sınırlamak sağladığını öğrenin."
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
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="89ea7-104">Azure Active Directory kimlik koruması Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="89ea7-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="89ea7-105">Bu playbook size yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="89ea7-105">This playbook helps you to:</span></span>

* <span data-ttu-id="89ea7-106">Kimlik koruması ortamında verileri benzetirme risk olaylarına ve güvenlik açıkları ile doldurma</span><span class="sxs-lookup"><span data-stu-id="89ea7-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="89ea7-107">Risk bağlı olarak koşullu erişim ilkeleri Ayarla ve bu ilkeler etkisini test etme</span><span class="sxs-lookup"><span data-stu-id="89ea7-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="89ea7-108">Risk olaylarını benzetimini yapma</span><span class="sxs-lookup"><span data-stu-id="89ea7-108">Simulating Risk Events</span></span>
<span data-ttu-id="89ea7-109">Bu bölümde aşağıdaki risk olayı türleri benzetimi için adımlara sağlar:</span><span class="sxs-lookup"><span data-stu-id="89ea7-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="89ea7-110">Oturum açma işlemleri anonim IP adreslerinden (kolay)</span><span class="sxs-lookup"><span data-stu-id="89ea7-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="89ea7-111">Oturum açma işlemleri tanınmayan konumlardan (Orta)</span><span class="sxs-lookup"><span data-stu-id="89ea7-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="89ea7-112">(Zor) alışılmadık konumlara imkansız seyahat</span><span class="sxs-lookup"><span data-stu-id="89ea7-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="89ea7-113">Diğer risk olaylarını güvenli bir şekilde benzetimi yapılamaz.</span><span class="sxs-lookup"><span data-stu-id="89ea7-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="89ea7-114">Anonim IP adreslerinden oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="89ea7-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="89ea7-115">Bu riski olay türü açan başarıyla anonim Ara sunucu IP adresi olarak tanımlanan bir IP adresinden kullanıcıları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="89ea7-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="89ea7-116">Bu proxy'leri kendi aygıtın IP adresi gizlemek istediğiniz ve kötü amaçlı için kullanılabilir kişiler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89ea7-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="89ea7-117">**Bir oturum açma anonim bir IP adresinden benzetimini yapmak için aşağıdaki adımları gerçekleştirin**:</span><span class="sxs-lookup"><span data-stu-id="89ea7-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="89ea7-118">Karşıdan [Tor tarayıcı](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="89ea7-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="89ea7-119">Tor tarayıcı kullanarak gidin [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="89ea7-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="89ea7-120">Görünmesini istediğiniz hesap kimlik bilgilerini girin **anonim IP adreslerinden gerçekleştirilen oturum açma işlemleri** rapor.</span><span class="sxs-lookup"><span data-stu-id="89ea7-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="89ea7-121">Oturum açma kimlik koruması Panoda 5 dakika içinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="89ea7-122">Alışılmadık konumlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="89ea7-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="89ea7-123">Oturum açma konumları göz önünde bulundurur bir oturum açma gerçek zamanlı değerlendirme mekanizması tanınmayan konumlardan riskidir (IP, enlem / boylam ve ASN) yeni / tanınmayan konumlarını belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="89ea7-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="89ea7-124">Sistem önceki IP'leri, enlem depolar / boylam ve bir kullanıcının Asn'ler ve tanıdık konumlarının olması için bu göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="89ea7-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="89ea7-125">Oturum açma konumu herhangi bir varolan tanıdık konumda eşleşmiyorsa bir oturum açma konumu tanınmayan olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="89ea7-126">Azure Active Directory kimlik koruması:</span><span class="sxs-lookup"><span data-stu-id="89ea7-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="89ea7-127">14 gün boyunca, tüm yeni konumlar tanınmayan konumları olarak işaretlemez bir ilk öğrenme süre sahiptir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="89ea7-128">oturum açma işlemleri hakkında bilgi sahibi aygıtları ve coğrafi olarak yakın varolan bir bilinen konum olan konumları yok sayar.</span><span class="sxs-lookup"><span data-stu-id="89ea7-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="89ea7-129">Tanınmayan konumlardan benzetimini yapmak için bir konum ve hesap öğesinden önce oturum açtığı olmayan bir aygıttan oturum açmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="89ea7-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="89ea7-130">**Bir oturum açma tanınmayan bir konumdan benzetimini yapmak için aşağıdaki adımları gerçekleştirin**:</span><span class="sxs-lookup"><span data-stu-id="89ea7-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="89ea7-131">Oturum açma en az bir 14 gün geçmiş olan bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="89ea7-132">Ya da yapın:</span><span class="sxs-lookup"><span data-stu-id="89ea7-132">Do either:</span></span>
   
   <span data-ttu-id="89ea7-133">a.</span><span class="sxs-lookup"><span data-stu-id="89ea7-133">a.</span></span> <span data-ttu-id="89ea7-134">Bir VPN kullanırken gidin [https://myapps.microsoft.com](https://myapps.microsoft.com) ve risk olayı için benzetimini yapmak istediğiniz hesabın kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="89ea7-135">b.</span><span class="sxs-lookup"><span data-stu-id="89ea7-135">b.</span></span> <span data-ttu-id="89ea7-136">Bir ilişkilendirme (önerilmez) hesabın kimlik bilgilerini kullanarak oturum farklı bir konumda isteyin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="89ea7-137">Oturum açma kimlik koruması Panoda 5 dakika içinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="89ea7-138">Alışılmadık konumu imkansız seyahat</span><span class="sxs-lookup"><span data-stu-id="89ea7-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="89ea7-139">Makine yanlış pozitifler tanıdık aygıtlardan mümkün olmayan seyahat veya oturum açmalardan dizindeki diğer kullanıcılar tarafından kullanılan VPN'ler gibi çıkışı ortadan kaldırmak öğrenme algoritmasını kullandığı için mümkün olmayan seyahat koşul benzetimi zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="89ea7-140">Ayrıca, risk olaylarını oluşturma işlemi başlamadan önce kullanıcı için bir oturum açma geçmişine 3-14 gün algoritma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="89ea7-141">**Bir mümkün olmayan seyahat alışılmadık konuma benzetimini yapmak için aşağıdaki adımları gerçekleştirin**:</span><span class="sxs-lookup"><span data-stu-id="89ea7-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="89ea7-142">Standart, tarayıcı kullanarak gidin [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="89ea7-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="89ea7-143">İçin bir mümkün olmayan seyahat risk olay oluşturmak için kullanmak istediğiniz hesabın kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="89ea7-144">Kullanıcı Aracısı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-144">Change your user agent.</span></span> <span data-ttu-id="89ea7-145">Geliştirici Araçları'ndan kullanıcı aracısı Internet Explorer'da değiştirmek veya kullanıcı aracınız Firefox veya kullanıcı aracısı değiştirici Eklentisi'ni kullanarak Chrome değiştirin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="89ea7-146">IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-146">Change your IP address.</span></span> <span data-ttu-id="89ea7-147">VPN, Tor eklentisi kullanılarak veya farklı bir veri merkezinde Azure içinde yeni bir makine dönmesini IP adresiniz değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89ea7-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="89ea7-148">Oturum açma için [https://myapps.microsoft.com](https://myapps.microsoft.com) olarak önce ve sonra önceki oturum açma birkaç dakika içinde aynı kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="89ea7-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="89ea7-149">Oturum açma kimlik koruması panosunda 2-4 saat içinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="89ea7-150">Modelleri ilgili karmaşık machine learning nedeniyle, bu toplanma değil bir fırsat yok.</span><span class="sxs-lookup"><span data-stu-id="89ea7-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="89ea7-151">Birden çok Azure AD hesapları için bu adımları çoğaltmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="89ea7-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="89ea7-152">Güvenlik açıkları benzetimini yapma</span><span class="sxs-lookup"><span data-stu-id="89ea7-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="89ea7-153">Güvenlik açıkları tarafından hatalı aktör yararlanan bir Azure AD ortamda zayıf giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="89ea7-154">Şu anda açık 3 türlerinin diğer özelliklerden Azure ad içinde Azure AD Identity Protection çıkmış.</span><span class="sxs-lookup"><span data-stu-id="89ea7-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="89ea7-155">Bu özellikler ayarlandıktan sonra bu güvenlik açıklarından otomatik olarak kimlik koruması panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="89ea7-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="89ea7-156">Azure AD [çok faktörlü kimlik doğrulaması?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="89ea7-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="89ea7-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89ea7-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="89ea7-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="89ea7-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="89ea7-159">Kullanıcı güvenlik aşılması riski</span><span class="sxs-lookup"><span data-stu-id="89ea7-159">User compromise risk</span></span>
<span data-ttu-id="89ea7-160">**Kullanıcı güvenlik aşılması risk sınamak için aşağıdaki adımları gerçekleştirin**:</span><span class="sxs-lookup"><span data-stu-id="89ea7-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="89ea7-161">Oturum açma için [https://portal.azure.com](https://portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="89ea7-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="89ea7-162">Gidin **kimlik koruması**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="89ea7-163">Ana **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="89ea7-164">Üzerinde **Portalı Ayarları** dikey altında **güvenlik kuralları**, tıklatın **kullanıcı güvenliğinin aşılmasına riski**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="89ea7-165">Üzerinde **Risk oturum** dikey penceresinde Aç **etkinleştir kural** kapalı ve ardından **kaydetmek** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="89ea7-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="89ea7-166">Belirtilen kullanıcı hesabı için bir tanınmayan benzetimini konumlar veya anonim IP risk olayı.</span><span class="sxs-lookup"><span data-stu-id="89ea7-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="89ea7-167">Bu, kullanıcı için kullanıcı risk düzeyini Yükselt **orta**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="89ea7-168">Birkaç dakika bekleyin ve kullanıcı için bu kullanıcı düzeyini doğrulayın **orta**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="89ea7-169">Git **Portalı Ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="89ea7-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="89ea7-170">Üzerinde **kullanıcı güvenliğinin aşılmasına Risk** dikey altında **etkinleştir kural**seçin **üzerinde** .</span><span class="sxs-lookup"><span data-stu-id="89ea7-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="89ea7-171">Aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="89ea7-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="89ea7-172">a.</span><span class="sxs-lookup"><span data-stu-id="89ea7-172">a.</span></span> <span data-ttu-id="89ea7-173">Bloğuna, select **orta** altında **blok oturum**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="89ea7-174">b.</span><span class="sxs-lookup"><span data-stu-id="89ea7-174">b.</span></span> <span data-ttu-id="89ea7-175">Güvenli parola değişikliğini uygulamak için seçin **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="89ea7-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89ea7-176">Click **Save**.</span></span>
12. <span data-ttu-id="89ea7-177">Bir kullanıcı bir yükseltilmiş risk düzeyi ile kullanarak oturum açma tarafından risk bağlı olarak koşullu erişim artık test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89ea7-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="89ea7-178">Kullanıcı risk Orta ise ya da engellenecek ilkeniz yapılandırmasına bağlı olarak, oturum açma işleminiz olduğundan veya parolanızı değiştirmek için zorlanır.</span><span class="sxs-lookup"><span data-stu-id="89ea7-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="89ea7-179">
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    </span><span class="sxs-lookup"><span data-stu-id="89ea7-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="89ea7-180">Oturum açma riski</span><span class="sxs-lookup"><span data-stu-id="89ea7-180">Sign-in risk</span></span>
<span data-ttu-id="89ea7-181">**Bir oturum risk test etmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89ea7-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="89ea7-182">Oturum açma için [https://portal.azure.com ](https://portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="89ea7-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="89ea7-183">Gidin **kimlik koruması**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="89ea7-184">Ana **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="89ea7-185">Üzerinde **Portalı Ayarları** dikey altında **güvenlik kuralları**, tıklatın **risk oturum**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="89ea7-186">Üzerinde ** Risk oturum ** dikey penceresinde, select **üzerinde** altında **etkinleştir kural**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="89ea7-187">Aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="89ea7-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="89ea7-188">a.</span><span class="sxs-lookup"><span data-stu-id="89ea7-188">a.</span></span> <span data-ttu-id="89ea7-189">Engellemek için seçin **orta** altında **blok oturum açın**</span><span class="sxs-lookup"><span data-stu-id="89ea7-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="89ea7-190">b.</span><span class="sxs-lookup"><span data-stu-id="89ea7-190">b.</span></span> <span data-ttu-id="89ea7-191">Güvenli parola değişikliğini uygulamak için seçin **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="89ea7-192">Engellemek için blok oturum açma altında Orta seçin.</span><span class="sxs-lookup"><span data-stu-id="89ea7-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="89ea7-193">Çok faktörlü kimlik doğrulamasını zorunlu kılmak için seçin **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="89ea7-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="89ea7-194">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89ea7-194">Click on **Save**.</span></span>
10. <span data-ttu-id="89ea7-195">Tanınmayan konumlardan taklit ederek risk bağlı olarak koşullu erişim artık sınayabilirsiniz veya her ikisi de olduklarından anonim IP risk olayları **orta** risk olayları.</span><span class="sxs-lookup"><span data-stu-id="89ea7-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="89ea7-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="89ea7-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="89ea7-197">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="89ea7-197">See also</span></span>
* [<span data-ttu-id="89ea7-198">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="89ea7-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

