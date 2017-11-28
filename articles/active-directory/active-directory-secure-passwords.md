---
title: "aaaAzure AD katmanlı parola güvenlik | Microsoft Docs"
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
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="03d1b-103">Çok katmanlı bir yaklaşım tooAzure AD parola güvenliği</span><span class="sxs-lookup"><span data-stu-id="03d1b-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="03d1b-104">Bu makalede, Azure Active Directory (Azure AD) veya Microsoft Account veya bir kullanıcı bir yönetici tooprotect olarak izleyebilirsiniz bazı en iyi uygulamalar açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="03d1b-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="03d1b-105">Azure AD Yöneticiler hello makalesindeki hello kılavuzu kullanarak kullanıcı parolalarını sıfırlama [Azure Active Directory'de bir kullanıcı için parola sıfırlama hello](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03d1b-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="03d1b-106">Kullanıcıların hello makalesinde hello kılavuzu kullanarak kendi parolasını sıfırlama [Azure AD parolamı unuttum Yardım](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="03d1b-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="03d1b-107">Parola gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="03d1b-107">Password requirements</span></span>

<span data-ttu-id="03d1b-108">Azure AD ortak yaklaşımlar toosecuring parolaları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="03d1b-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="03d1b-109">Parola uzunluğu gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="03d1b-109">Password length requirements</span></span>
* <span data-ttu-id="03d1b-110">Parola karmaşıklık gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="03d1b-110">Password complexity requirements</span></span>
* <span data-ttu-id="03d1b-111">Normal ve düzenli parola sona erme süresi</span><span class="sxs-lookup"><span data-stu-id="03d1b-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="03d1b-112">Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için hello konusuna [Azure AD Self Servis parola sıfırlama hello BT uzmanları için](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="03d1b-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="03d1b-113">Azure AD parola korumaları</span><span class="sxs-lookup"><span data-stu-id="03d1b-113">Azure AD password protections</span></span>

<span data-ttu-id="03d1b-114">Azure AD ve Microsoft hesap sisteminde kullanmak kanıtlanmış endüstri hello yaklaşıyor dahil olmak üzere kullanıcı ve yönetici parolalarını tooensure güvenli koruma:</span><span class="sxs-lookup"><span data-stu-id="03d1b-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="03d1b-115">Dinamik olarak yasaklanmış parolalar</span><span class="sxs-lookup"><span data-stu-id="03d1b-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="03d1b-116">Akıllı Parola Kilitleme</span><span class="sxs-lookup"><span data-stu-id="03d1b-116">Smart Password Lockout</span></span>

<span data-ttu-id="03d1b-117">Geçerli araştırmaya dayanarak parola yönetimi hakkında daha fazla bilgi için hello teknik incelemesine bakın [parola Kılavuzu](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="03d1b-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="03d1b-118">Dinamik olarak yasaklanmış parolalar</span><span class="sxs-lookup"><span data-stu-id="03d1b-118">Dynamically banned passwords</span></span>

<span data-ttu-id="03d1b-119">Azure AD ve Microsoft Accounts yaygın olarak kullanılan parolalar banning tarafından dinamik olarak parola koruması koruyun.</span><span class="sxs-lookup"><span data-stu-id="03d1b-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="03d1b-120">Hello Azure kimliği kimlik koruması takım Engellenenler parola listeleri, kullanıcıların yaygın olarak kullanılan parolalar seçmesini önleyerek düzenli olarak analiz eder.</span><span class="sxs-lookup"><span data-stu-id="03d1b-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="03d1b-121">Bu, kullanılabilir tooAzure AD ve hello Microsoft hesabı hizmet müşterileri hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="03d1b-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="03d1b-122">Parolalar oluştururken, harfler, sayılar, karakterler veya sözcükler benzersiz bir bileşimini içeren Yöneticiler tooencourage kullanıcılar toochoose parola tümcecikleri için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="03d1b-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="03d1b-123">Bu yaklaşım, ancak kullanıcılar tooremember daha kolay neredeyse imkansız toobe tehlikeye toomake kullanıcı parolalarını yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="03d1b-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="03d1b-124">Parola ihlallerinden</span><span class="sxs-lookup"><span data-stu-id="03d1b-124">Password breaches</span></span>

<span data-ttu-id="03d1b-125">Microsoft, her zaman tek bir adımda toostay siber suçlular öncesinde çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="03d1b-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="03d1b-126">Hello Azure AD Identity Protection ekibine yaygın olarak kullanılan parolalar sürekli analiz eder.</span><span class="sxs-lookup"><span data-stu-id="03d1b-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="03d1b-127">Siber suçlular yapı gibi kendi saldırıları benzer stratejileri tooinform de bir [şifre tablo](https://en.wikipedia.org/wiki/Rainbow_table) parola karmaları çözme için.</span><span class="sxs-lookup"><span data-stu-id="03d1b-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="03d1b-128">Microsoft sürekli olarak çözümler [veri ihlallerinden](https://www.privacyrights.org/data-breaches) toomaintain gerçek haline gelmeden önce güvenlik açığı parolaları yasaklanan sağlayan dinamik olarak güncelleştirilen Engellenenler parola listesini tehdit tooAzure AD müşteriler.</span><span class="sxs-lookup"><span data-stu-id="03d1b-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="03d1b-129">Merhaba bizim geçerli güvenlik çalışmaları hakkında daha fazla bilgi için bkz: [Microsoft Güvenlik Intelligence rapor](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="03d1b-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="03d1b-130">Akıllı Parola Kilitleme</span><span class="sxs-lookup"><span data-stu-id="03d1b-130">Smart Password Lockout</span></span>

<span data-ttu-id="03d1b-131">Azure AD kullanıcı parolanıza olası bir siber suçlunun çalışırken toohack algıladığında, biz akıllı parola kilitleme hello kullanıcı hesabıyla kilitleyin.</span><span class="sxs-lookup"><span data-stu-id="03d1b-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="03d1b-132">Azure AD tasarlanmıştır belirli oturum açma oturumlarıyla ilişkili toodetermine hello risk.</span><span class="sxs-lookup"><span data-stu-id="03d1b-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="03d1b-133">Merhaba en güncel güvenlik verileri kullanarak daha sonra biz kilitleme semantiği toostop siber tehditleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="03d1b-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="03d1b-134">Bir kullanıcı Azure AD dışında kilitliyse kendi ekran benzer toohello izleyen bir görünür:</span><span class="sxs-lookup"><span data-stu-id="03d1b-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Azure AD dışında kalmış](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="03d1b-136">Diğer Microsoft hesapları için kendi ekran benzer toohello izleyen bir görünür:</span><span class="sxs-lookup"><span data-stu-id="03d1b-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Microsoft hesabı dışında kalmış](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="03d1b-138">Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için hello konusuna [Azure AD Self Servis parola sıfırlama hello BT uzmanları için](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="03d1b-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="03d1b-139">Azure AD Yöneticiyseniz, toouse isteyebilirsiniz [Windows Hello](https://www.microsoft.com/windows/windows-hello) kullanıcılarınızın sahip tooavoid geleneksel parolaları tamamen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03d1b-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="03d1b-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03d1b-140">Next steps</span></span>

* [<span data-ttu-id="03d1b-141">Nasıl tooupdate kendi parolanızı</span><span class="sxs-lookup"><span data-stu-id="03d1b-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="03d1b-142">Azure Kimlik Yönetimi Hello temelleri</span><span class="sxs-lookup"><span data-stu-id="03d1b-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="03d1b-143">Raporda parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="03d1b-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


