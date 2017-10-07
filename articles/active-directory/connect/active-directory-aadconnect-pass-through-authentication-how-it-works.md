---
title: "Azure AD Connect: Doğrudan kimlik doğrulama - nasıl çalışır? | Microsoft Belgeleri"
description: "Bu makalede, Azure Active Directory doğrudan kimlik doğrulaması nasıl çalıştığı açıklanmaktadır."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="7698b-105">Azure Active Directory doğrudan kimlik doğrulaması: Teknik derinlemesine bakış</span><span class="sxs-lookup"><span data-stu-id="7698b-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="7698b-106">Azure AD doğrudan kimlik doğrulama şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="7698b-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="7698b-107">Azure Active Directory doğrudan kimlik doğrulaması nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="7698b-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="7698b-108">Bir kullanıcı Azure Active Directory (Azure AD) tarafından güvenli hale getirilmiş bir uygulamaya toosign çalışır ve hello Kiracı'geçişli kimlik doğrulaması etkinleştirilirse hello aşağıdaki adımlardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="7698b-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="7698b-109">Merhaba kullanıcı çalıştığında tooaccess bir uygulama (örneğin, Outlook Web App - hello https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="7698b-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="7698b-110">Merhaba kullanıcı zaten oturum açmamış, hello kullanıcının yeniden yönlendirilen toohello Azure AD oturum açma sayfası olur.</span><span class="sxs-lookup"><span data-stu-id="7698b-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="7698b-111">Merhaba kullanıcı oturum açma hello Azure AD sayfasına, kullanıcı adı ve parolasını girer ve hello "Oturum" düğmesine tıklar.</span><span class="sxs-lookup"><span data-stu-id="7698b-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="7698b-112">Merhaba oturum açma isteği alırken azure AD hello kullanıcı adı ve parola (bir ortak anahtar kullanılarak şifrelenmiş) bulunan bir sıra yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="7698b-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="7698b-113">Bir şirket içi doğrudan kimlik doğrulama Aracısı giden çağrı toohello sıra yapar ve hello kullanıcı adı ve şifrelenmiş parola alır.</span><span class="sxs-lookup"><span data-stu-id="7698b-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="7698b-114">Merhaba Aracısı özel anahtarını kullanarak hello parola şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="7698b-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="7698b-115">Merhaba Aracısı sonra hello kullanıcı adı ve parola (benzer bir mekanizma toowhat Active Directory Federasyon Hizmetleri tarafından kullanılır) standart Windows API'leri kullanarak Active Directory karşı doğrular.</span><span class="sxs-lookup"><span data-stu-id="7698b-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="7698b-116">Merhaba kullanıcı adı ya da hello şirket içi varsayılan kullanıcı adı olabilir (genellikle `userPrincipalName`) veya Azure AD Connect içinde yapılandırılmış başka bir öznitelik (olarak bilinen `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="7698b-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="7698b-117">Merhaba şirket içi Active Directory etki alanı denetleyicisi (DC) sonra hello isteği değerlendirir ve hello uygun yanıtı döndürür (başarılı, başarısız, parolanın süresi doldu veya kullanıcı kilitli) toohello aracı.</span><span class="sxs-lookup"><span data-stu-id="7698b-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="7698b-118">Merhaba Aracısı, buna karşılık, bu yanıt geri tooAzure AD döndürür.</span><span class="sxs-lookup"><span data-stu-id="7698b-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="7698b-119">Azure AD hello yanıt değerlendirir ve toohello kullanıcı uygun şekilde yanıt - Örneğin, hello hemen oturum açtığında ya da çok faktörlü kimlik doğrulama (MFA için) ister.</span><span class="sxs-lookup"><span data-stu-id="7698b-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="7698b-120">Merhaba kullanıcı oturum açma başarılı olursa, hello kullanıcı mümkün tooaccess hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="7698b-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="7698b-121">Merhaba Aşağıdaki diyagramda tüm hello bileşenleri ve hello adımlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7698b-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Doğrudan Kimlik Doğrulama](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="7698b-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7698b-123">Next steps</span></span>
- <span data-ttu-id="7698b-124">[**Geçerli sınırlamalar** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -bu özellik şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="7698b-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="7698b-125">Hangi senaryoları desteklenir ve hangilerinin olmayan öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7698b-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="7698b-126">[**Hızlı Başlangıç** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - hale getirmek ve Azure AD doğrudan kimlik doğrulama çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="7698b-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="7698b-127">[**Sık sorulan sorular** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7698b-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="7698b-128">[**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7698b-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="7698b-129">[**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7698b-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="7698b-130">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="7698b-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
