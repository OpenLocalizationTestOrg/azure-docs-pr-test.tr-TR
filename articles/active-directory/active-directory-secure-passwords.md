---
title: "Azure AD parola güvenlik katmanlı | Microsoft Docs"
description: "Açıklar nasıl Azure AD güçlü parolalar zorlar ve siber suçlular kullanıcı parolaları korur"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="45be3-103">Azure AD parola güvenlik çok katmanlı bir yaklaşım</span><span class="sxs-lookup"><span data-stu-id="45be3-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="45be3-104">Bu makalede, bir kullanıcı, Azure Active Directory (Azure AD) veya Microsoft Account korumak için bir yönetici olarak veya izleyebilirsiniz bazı en iyi uygulamalar açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="45be3-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="45be3-105">Azure AD Yöneticiler makalesindeki yönergeleri kullanarak kullanıcı parolalarını sıfırlama [Azure Active Directory'de bir kullanıcı parolasını sıfırlama](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="45be3-106">Kullanıcıların makalesindeki yönergeleri kullanarak kendi parolasını sıfırlama [Azure AD parolamı unuttum Yardım](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="45be3-107">Parola gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="45be3-107">Password requirements</span></span>

<span data-ttu-id="45be3-108">Azure AD, parolaların güvenliğini sağlama konusunda aşağıdaki genel yaklaşımları benimser:</span><span class="sxs-lookup"><span data-stu-id="45be3-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="45be3-109">Parola uzunluğu gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="45be3-109">Password length requirements</span></span>
* <span data-ttu-id="45be3-110">Parola karmaşıklık gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="45be3-110">Password complexity requirements</span></span>
* <span data-ttu-id="45be3-111">Normal ve düzenli parola sona erme süresi</span><span class="sxs-lookup"><span data-stu-id="45be3-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="45be3-112">Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için Ek Yardım konusuna [Azure AD Self Servis parola sıfırlama için BT Uzmanı](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="45be3-113">Azure AD parola korumaları</span><span class="sxs-lookup"><span data-stu-id="45be3-113">Azure AD password protections</span></span>

<span data-ttu-id="45be3-114">Azure AD ve Microsoft hesabı sistemi yaklaşımlar kanıtlanmış endüstri dahil olmak üzere kullanıcı ve yönetici parolaların güvenli koruma sağlamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="45be3-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="45be3-115">Dinamik olarak yasaklanmış parolalar</span><span class="sxs-lookup"><span data-stu-id="45be3-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="45be3-116">Akıllı Parola Kilitleme</span><span class="sxs-lookup"><span data-stu-id="45be3-116">Smart Password Lockout</span></span>

<span data-ttu-id="45be3-117">Geçerli araştırmaya dayanarak parola yönetimi hakkında daha fazla bilgi için teknik incelemesine bakın [parola Kılavuzu](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="45be3-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="45be3-118">Dinamik olarak yasaklanmış parolalar</span><span class="sxs-lookup"><span data-stu-id="45be3-118">Dynamically banned passwords</span></span>

<span data-ttu-id="45be3-119">Azure AD ve Microsoft Accounts yaygın olarak kullanılan parolalar banning tarafından dinamik olarak parola koruması koruyun.</span><span class="sxs-lookup"><span data-stu-id="45be3-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="45be3-120">Azure ID Kimlik Koruma ekibi, yasaklı parola listelerini düzenli olarak analiz eder ve kullanıcıların yaygın olarak kullanılan parolaları seçmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="45be3-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="45be3-121">Bu hizmet, Azure AD ve Microsoft Hesap Hizmeti müşterileri tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="45be3-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="45be3-122">Parolalar oluştururken, yöneticilerin harfler, sayılar, karakterler veya sözcükler benzersiz bir bileşimi dahil parola tümcecikleri seçmek için kullanıcıları teşvik için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="45be3-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="45be3-123">Bu yaklaşım, kullanıcı parolalarını neredeyse imkansız gizliliği ihlal edilmiş, ancak kullanıcılar için hatırlaması daha kolay yapmak için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="45be3-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="45be3-124">Parola ihlallerinden</span><span class="sxs-lookup"><span data-stu-id="45be3-124">Password breaches</span></span>

<span data-ttu-id="45be3-125">Microsoft, her zaman tek bir adımda siber suçlular öncesinde kalmak için çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="45be3-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="45be3-126">Azure AD Kimlik Koruması ekibi, yaygın olarak kullanılan parolaları sürekli olarak analiz eder.</span><span class="sxs-lookup"><span data-stu-id="45be3-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="45be3-127">Siber suçlular da saldırılarını geliştirmek üzere parola karmalarını çözmek için [şifre tablosu](https://en.wikipedia.org/wiki/Rainbow_table) oluşturmak gibi benzer stratejiler kullanır.</span><span class="sxs-lookup"><span data-stu-id="45be3-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="45be3-128">Microsoft dinamik olarak güncellenen bir yasaklı parola listesi tutmak üzere [veri ihlallerini](https://www.privacyrights.org/data-breaches) sürekli olarak analiz eder; bu liste, güvenlik açığı olan parolaların Azure AD müşterileri için gerçek bir tehdit haline gelmesinden önce engellenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="45be3-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="45be3-129">Geçerli güvenlik çalışmalarımız hakkında daha fazla bilgi için bkz. [Microsoft Güvenlik Bilgileri Raporu](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="45be3-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="45be3-130">Akıllı Parola Kilitleme</span><span class="sxs-lookup"><span data-stu-id="45be3-130">Smart Password Lockout</span></span>

<span data-ttu-id="45be3-131">Azure AD bir kullanıcı parolasına saldırmaya çalışan olası bir siber suçluyu algıladığında, kullanıcı hesabı Akıllı Parola Kilitleme özelliğiyle kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="45be3-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="45be3-132">Azure AD, belirli oturumlarla ilişkili riski belirlemek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="45be3-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="45be3-133">En güncel güvenlik verileri kullanarak daha sonra biz siber tehditleri durdurmaya kilitleme semantiği uygulayın.</span><span class="sxs-lookup"><span data-stu-id="45be3-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="45be3-134">Bir kullanıcı Azure AD dışında kilitliyse kendi ekran izleyen bir benzer:</span><span class="sxs-lookup"><span data-stu-id="45be3-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Azure AD dışında kalmış](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="45be3-136">Diğer Microsoft hesapları için kendi ekran izleyen bir benzer:</span><span class="sxs-lookup"><span data-stu-id="45be3-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Microsoft hesabı dışında kalmış](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="45be3-138">Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için Ek Yardım konusuna [Azure AD Self Servis parola sıfırlama için BT Uzmanı](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="45be3-139">Bir Azure AD yöneticisiyseniz, kullanıcıların geleneksel parolalar oluşturmasını önlemek için [Windows Hello](https://www.microsoft.com/windows/windows-hello) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45be3-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="45be3-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45be3-140">Next steps</span></span>

* [<span data-ttu-id="45be3-141">Kendi parolanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="45be3-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="45be3-142">Azure kimlik yönetimi ile ilgili temel bilgiler</span><span class="sxs-lookup"><span data-stu-id="45be3-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="45be3-143">Raporda parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="45be3-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


