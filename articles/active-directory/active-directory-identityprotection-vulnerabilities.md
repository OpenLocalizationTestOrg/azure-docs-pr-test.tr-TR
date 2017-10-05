---
title: "Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı | Microsoft Docs"
description: "Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı genel bakış."
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
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="282ad-104">Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı</span><span class="sxs-lookup"><span data-stu-id="282ad-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="282ad-105">Güvenlik açıkları zayıf bir saldırgan tarafından yararlanılabilir ortamınızda giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="282ad-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="282ad-106">Kuruluşunuzun güvenlik tutumunu artırmak için bu güvenlik açıklarına ve bunları yararlanmasını saldırganların önlemeye öneririz.</span><span class="sxs-lookup"><span data-stu-id="282ad-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="282ad-107">![Güvenlik Açıkları](./media/active-directory-identityprotection-vulnerabilities/101.png "güvenlik açıkları")</span><span class="sxs-lookup"><span data-stu-id="282ad-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="282ad-108">Aşağıdaki bölümler kimlik koruması tarafından bildirilen güvenlik açıkları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="282ad-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="282ad-109">Çok faktörlü kimlik doğrulaması kayıt yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="282ad-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="282ad-110">Bu güvenlik açığından, kuruluşunuzda Azure multi-Factor Authentication dağıtımı denetlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="282ad-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="282ad-111">Azure çok faktörlü kimlik doğrulaması ikinci bir kullanıcı kimlik doğrulaması için güvenlik katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="282ad-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="282ad-112">Bu basit bir oturum açma işlemi için kullanıcı talebine buluştururken veri ve uygulamalara erişimi korunmasına yardımcı.</span><span class="sxs-lookup"><span data-stu-id="282ad-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="282ad-113">Kolay doğrulama seçeneklerini çeşitli aracılığıyla güçlü kimlik doğrulaması sunar — telefon araması, SMS mesajı veya mobil uygulama bildirimi veya doğrulama kodu ve 3. taraf OATH belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="282ad-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="282ad-114">Azure multi-Factor Authentication kullanıcı oturum açma işlemleri için gerekli öneririz.</span><span class="sxs-lookup"><span data-stu-id="282ad-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="282ad-115">Çok faktörlü kimlik doğrulaması risk bağlı olarak koşullu erişim ilkelerindeki kimlik koruması kullanılabilir önemli bir rol oynar.</span><span class="sxs-lookup"><span data-stu-id="282ad-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="282ad-116">Daha fazla ayrıntı için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="282ad-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="282ad-117">Yönetilmeyen bulut uygulamaları</span><span class="sxs-lookup"><span data-stu-id="282ad-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="282ad-118">Bu güvenlik açığından kuruluşunuzdaki yönetilmeyen bulut uygulamaları tanımlamasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="282ad-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="282ad-119">Modern kuruluşlarda, BT departmanları genellikle kuruluşlarındaki kullanıcılar işlerini yapmak için kullandığınız tüm bulut uygulamaları farkında değildir.</span><span class="sxs-lookup"><span data-stu-id="282ad-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="282ad-120">Yöneticileri Kurumsal verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine yetkisiz erişimi endişeniz neden olurdu görmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="282ad-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="282ad-121">Kuruluşunuzun Cloud App Discovery yönetilmeyen bulut uygulamaları bulmak ve Azure Active Directory'yi kullanarak bu uygulamaları yönetmek için dağıtmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="282ad-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="282ad-122">Daha fazla ayrıntı için bkz: [Cloud App Discovery ile yönetilmeyen bulut uygulamaları bulma](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="282ad-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="282ad-123">Privileged Identity Management güvenlik uyarıları</span><span class="sxs-lookup"><span data-stu-id="282ad-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="282ad-124">Bu güvenlik açığından bulmak ve uyarılar, kuruluşunuzda ayrıcalıklı kimlikleri hakkında çözümlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="282ad-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="282ad-125">Ayrıcalıklı işlemleri gerçekleştirmek kullanıcıları etkinleştirmek için Azure AD'de kullanıcıları geçici veya kalıcı ayrıcalıklı erişim vermek kuruluş gerekir Azure veya Office 365 kaynakları veya diğer SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="282ad-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="282ad-126">Her bu ayrıcalıklı kullanıcılar, kuruluşunuzun saldırı yüzeyini artırır.</span><span class="sxs-lookup"><span data-stu-id="282ad-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="282ad-127">Bu güvenlik açığından gereksiz ayrıcalıklı erişimi kullanıcıları tanımlamak ve azaltın veya bunlar teşkil riski ortadan kaldırmak için uygun eylemi gerçekleştirin yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="282ad-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="282ad-128">Kuruluşunuz, denetimi yönetmek için Azure AD Privileged Identity Management kullanır ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services yanı sıra kimlikleri ve bunların Azure ad'deki kaynaklara erişimi İzleyici ayrıcalıklı öneririz.</span><span class="sxs-lookup"><span data-stu-id="282ad-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="282ad-129">Daha fazla ayrıntı için bkz: [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="282ad-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="282ad-130">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="282ad-130">See also</span></span>
* [<span data-ttu-id="282ad-131">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="282ad-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

