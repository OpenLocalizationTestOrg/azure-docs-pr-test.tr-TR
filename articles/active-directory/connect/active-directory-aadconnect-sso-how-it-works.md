---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma - nasıl çalışır? | Microsoft Docs"
description: "Bu makalede, Azure Active Directory sorunsuz çoklu oturum açma hello özelliğinin nasıl çalıştığı açıklanmaktadır."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="ef7dd-104">Azure Active Directory sorunsuz çoklu oturum açma: teknik derinlemesine bakış</span><span class="sxs-lookup"><span data-stu-id="ef7dd-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="ef7dd-105">Bu makalede hello Azure Active Directory sorunsuz çoklu oturum açma (sorunsuz SSO) özelliğinin nasıl çalıştığı içine teknik ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ef7dd-106">Merhaba sorunsuz SSO özelliği şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="ef7dd-107">Sorunsuz SSO nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="ef7dd-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="ef7dd-108">Bu bölüm iki bölümden tooit vardır:</span><span class="sxs-lookup"><span data-stu-id="ef7dd-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="ef7dd-109">Merhaba sorunsuz SSO özelliği Hello kurulumu.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="ef7dd-110">Nasıl bir tek kullanıcı oturum açma işlemi ile sorunsuz SSO çalışır.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="ef7dd-111">Nasıl iş ayarlamak?</span><span class="sxs-lookup"><span data-stu-id="ef7dd-111">How does set up work?</span></span>

<span data-ttu-id="ef7dd-112">Sorunsuz SSO etkin gösterildiği gibi Azure AD Connect'i kullanarak [burada](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="ef7dd-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="ef7dd-113">Merhaba özelliği etkinleştirirken, aşağıdaki adımları hello oluşur:</span><span class="sxs-lookup"><span data-stu-id="ef7dd-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="ef7dd-114">Adlı bir bilgisayar hesabı `AZUREADSSOACCT` (Azure AD temsil eden), şirket içi Active Directory (AD) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="ef7dd-115">Merhaba bilgisayar hesabının Kerberos şifre çözme anahtarı güvenli bir şekilde Azure AD ile paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="ef7dd-116">Ayrıca, iki Kerberos hizmet asıl adları (SPN) Azure AD oturum açma sırasında kullanılan toorepresent iki URL'leri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="ef7dd-117">Hello bilgisayar hesabı ve hello Kerberos SPN'lerinin her AD ormanında oluşturulan tooAzure AD eşitleme (Azure AD Connect'i kullanarak) ve olan kullanıcılar için sorunsuz SSO istiyor.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="ef7dd-118">Merhaba taşıma `AZUREADSSOACCT` bilgisayar hesabı tooan kuruluş birimi (OU) içinde yönetilen saklı tooensure olduğu diğer bilgisayar hesapları hello aynı şekilde ve silinmez.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ef7dd-119">Yüksek oranda öneririz, [hello Kerberos şifre çözme anahtarı alma](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) Merhaba, `AZUREADSSOACCT` bilgisayar hesabı en az 30 günde.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="ef7dd-120">Nasıl oturum sorunsuz SSO çalışmak açma?</span><span class="sxs-lookup"><span data-stu-id="ef7dd-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="ef7dd-121">Merhaba Kurulum tamamlandıktan sonra tümleşik Windows kimlik doğrulaması (IWA) kullanan aynı yolla diğer olarak oturum açma hello sorunsuz SSO çalışır.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="ef7dd-122">Merhaba akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ef7dd-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="ef7dd-123">Merhaba kullanıcı çalıştığında tooaccess bir uygulama (örneğin, Outlook Web App - hello https://outlook.office365.com/owa/) bir etki alanına katılmış kurumsal bir CİHAZDAN Kurumsal ağınızdaki.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="ef7dd-124">Merhaba kullanıcı zaten oturum açmamış, hello kullanıcının yeniden yönlendirilen toohello Azure AD oturum açma sayfası olur.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="ef7dd-125">Hello Azure AD oturum açma isteği içeriyorsa, bir `domain_hint` (örneğin, Kiracı - tanımlama, contoso.onmicrosoft.com) veya `login_hint` (Merhaba kullanıcı - Örneğin, tanımlayan user@contoso.onmicrosoft.com veya user@contoso.com) parametre sonra 2. adım atlanır.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="ef7dd-126">kullanıcı adlarını hello Azure AD oturum açma sayfası içine Hello kullanıcı türleri.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="ef7dd-127">JavaScript hello arka planda kullanarak, Azure AD bir Kerberos anahtarı hello tarayıcı 401 Yetkisiz bir yanıt olan tooprovide yoluyla sınar.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="ef7dd-128">Merhaba tarayıcı sırayla isteklerini bir bilet Active Directory'den Merhaba `AZUREADSSOACCT` (Azure AD temsil eden) bilgisayar hesabı.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="ef7dd-129">Active Directory hello bilgisayar hesabı bulur ve hello bilgisayar hesabının parolası ile şifrelenmiş bir Kerberos bileti toohello tarayıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="ef7dd-130">Merhaba tarayıcı iletir Active Directory tooAzure AD edinilen hello Kerberos bileti (Merhaba birinde [Azure AD URL'leri toohello tarayıcısının Intranet bölgesi ayarlarından daha önce eklediğiniz](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="ef7dd-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="ef7dd-131">Merhaba hello Kurumsal cihaz imzalı hello kullanıcının kimliğini içeren azure AD şifrelerinin çözülmesi hello Kerberos bileti, hello kullanarak önceden paylaşılan anahtar.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="ef7dd-132">Değerlendirme sonra Azure AD belirteci geri toohello uygulama döndürür ya da çok faktörlü kimlik doğrulaması gibi ek sağlamaları hello kullanıcı tooperform sorar.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="ef7dd-133">Merhaba kullanıcı oturum açma başarılı olursa, hello kullanıcı mümkün tooaccess hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="ef7dd-134">Merhaba Aşağıdaki diyagramda tüm hello bileşenleri ve hello adımlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Sorunsuz çoklu oturum açma](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="ef7dd-136">Sorunsuz SSO fırsatçılıktan, başarısız olursa hello oturum açma deneyimini döner geri tooits normal davranış - yani, hello başka bir deyişle, kullanıcının kendi parola toosign tooenter gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef7dd-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef7dd-137">Next steps</span></span>

- <span data-ttu-id="ef7dd-138">[**Hızlı Başlangıç** ](active-directory-aadconnect-sso-quick-start.md) - hale getirmek ve Azure AD sorunsuz SSO çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="ef7dd-139">[**Sık sorulan sorular** ](active-directory-aadconnect-sso-faq.md) -toofrequently sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="ef7dd-140">[**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="ef7dd-141">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="ef7dd-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
