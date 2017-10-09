---
title: "Azure Active Directory kimlik koruması tarafından algılanan aaaVulnerabilities | Microsoft Docs"
description: "Azure Active Directory kimlik koruması tarafından algılanan hello güvenlik açıkları genel bakış."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="599f0-104">Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı</span><span class="sxs-lookup"><span data-stu-id="599f0-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="599f0-105">Güvenlik açıkları zayıf bir saldırgan tarafından yararlanılabilir ortamınızda giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="599f0-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="599f0-106">Bu güvenlik açıkları tooimprove hello güvenlik yaklaşımı, kuruluşunuzun adres ve bunları yararlanmasını saldırganların önlemeye öneririz.</span><span class="sxs-lookup"><span data-stu-id="599f0-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="599f0-107">![Güvenlik Açıkları](./media/active-directory-identityprotection-vulnerabilities/101.png "güvenlik açıkları")</span><span class="sxs-lookup"><span data-stu-id="599f0-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="599f0-108">Merhaba aşağıdaki bölümlerde kimlik koruması tarafından bildirilen hello güvenlik açıkları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="599f0-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="599f0-109">Çok faktörlü kimlik doğrulaması kayıt yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="599f0-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="599f0-110">Bu güvenlik açığından yardımcı olacak denetim kuruluşunuzda Azure çok faktörlü kimlik doğrulamasının hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="599f0-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="599f0-111">Azure çok faktörlü kimlik doğrulaması güvenlik toouser kimlik doğrulamasının ikinci bir katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="599f0-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="599f0-112">Bu koruma erişim toodata ve uygulamaları basit bir oturum açma işlemi için kullanıcı talebine buluştururken yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="599f0-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="599f0-113">Kolay doğrulama seçeneklerini çeşitli aracılığıyla güçlü kimlik doğrulaması sunar — telefon araması, SMS mesajı veya mobil uygulama bildirimi veya doğrulama kodu ve 3. taraf OATH belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="599f0-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="599f0-114">Azure multi-Factor Authentication kullanıcı oturum açma işlemleri için gerekli öneririz. Çok faktörlü kimlik doğrulaması risk bağlı olarak koşullu erişim ilkelerindeki kimlik koruması kullanılabilir önemli bir rol oynar.</span><span class="sxs-lookup"><span data-stu-id="599f0-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="599f0-115">Daha fazla ayrıntı için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="599f0-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="599f0-116">Yönetilmeyen bulut uygulamaları</span><span class="sxs-lookup"><span data-stu-id="599f0-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="599f0-117">Bu güvenlik açığından kuruluşunuzdaki yönetilmeyen bulut uygulamaları tanımlamasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="599f0-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="599f0-118">Modern kuruluşlarda, BT departmanları genellikle kullanıcılar kuruluşlarındaki işlerine toodo kullanmakta olduğunuz tüm hello bulut uygulamaları farkında değildir.</span><span class="sxs-lookup"><span data-stu-id="599f0-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="599f0-119">Yöneticiler yetkisiz erişim toocorporate verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine endişeniz neden olurdu kolay toosee olur.</span><span class="sxs-lookup"><span data-stu-id="599f0-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="599f0-120">Kuruluşunuz Azure Active Directory'yi kullanarak bu uygulamaları Cloud App Discovery toodiscover yönetilmeyen bulut uygulamaları ve toomanage dağıtmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="599f0-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="599f0-121">Daha fazla ayrıntı için bkz: [Cloud App Discovery ile yönetilmeyen bulut uygulamaları bulma](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="599f0-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="599f0-122">Privileged Identity Management güvenlik uyarıları</span><span class="sxs-lookup"><span data-stu-id="599f0-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="599f0-123">Bu güvenlik açığından bulmak ve uyarılar, kuruluşunuzda ayrıcalıklı kimlikleri hakkında çözümlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="599f0-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="599f0-124">tooenable kullanıcılar toocarry genişletme ayrıcalıklı işlemleri kuruluşların gerekir geçici veya kalıcı ayrıcalıklı erişim Azure AD'de toogrant kullanıcılar Azure veya Office 365 kaynakları veya diğer SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="599f0-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="599f0-125">Bunların her biri, kullanıcıların artar hello saldırı yüzeyini, kuruluşunuzun ayrıcalıklı.</span><span class="sxs-lookup"><span data-stu-id="599f0-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="599f0-126">Bu güvenlik açığından gereksiz ayrıcalıklı erişimi kullanıcıları tanımlamak ve tooreduce uygun eylemi gerçekleştirin ve bunlar teşkil hello riski ortadan kaldırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="599f0-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="599f0-127">Kuruluşunuzun Azure AD Privileged Identity Management toomanage, Denetim ve ayrıcalıklı izleme kimlikleri ve bunların erişim tooresources Azure AD'de yanı sıra Office 365 veya Microsoft Intune gibi diğer Microsoft online services kullandığı öneririz.</span><span class="sxs-lookup"><span data-stu-id="599f0-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="599f0-128">Daha fazla ayrıntı için bkz: [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="599f0-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="599f0-129">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="599f0-129">See also</span></span>
* [<span data-ttu-id="599f0-130">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="599f0-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

