---
title: "Azure AD Connect: Doğrudan kimlik doğrulama - geçerli sınırlamalar | Microsoft Docs"
description: "Bu makalede, Azure Active Directory (Azure AD) geçiş kimlik doğrulamasının geçerli sınırlamalar açıklanır."
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="f30ff-104">Azure Active Directory doğrudan kimlik doğrulaması: Geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="f30ff-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="f30ff-105">Azure AD doğrudan kimlik doğrulama şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="f30ff-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="f30ff-106">Boş bir özelliktir ve kullanmak için Azure AD Ücretli tüm sürümleri olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f30ff-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="f30ff-107">Doğrudan kimlik doğrulama kullanılabilir yalnızca Azure ad ve değil dünya çapında örneğinde [Microsoft Cloud Almanya](http://www.microsoft.de/cloud-deutschland) ve [Microsoft Azure kamu bulut](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="f30ff-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="f30ff-108">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="f30ff-108">Supported scenarios</span></span>

<span data-ttu-id="f30ff-109">Aşağıdaki senaryolarda, Önizleme süresince tam olarak desteklenir:</span><span class="sxs-lookup"><span data-stu-id="f30ff-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="f30ff-110">Tüm web uygulamalarına tarayıcı tabanlı kullanıcı oturum açma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="f30ff-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="f30ff-111">Kullanıcı oturum açma işlemleri destekleyen Office 365 istemci uygulamalara [modern kimlik doğrulaması](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="f30ff-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="f30ff-112">Windows 10 cihazlar için Azure AD katılım.</span><span class="sxs-lookup"><span data-stu-id="f30ff-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="f30ff-113">Exchange ActiveSync desteği.</span><span class="sxs-lookup"><span data-stu-id="f30ff-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="f30ff-114">Desteklenmeyen senaryolar</span><span class="sxs-lookup"><span data-stu-id="f30ff-114">Unsupported scenarios</span></span>

<span data-ttu-id="f30ff-115">Aşağıdaki senaryolar _değil_ Önizleme sırasında desteklenir:</span><span class="sxs-lookup"><span data-stu-id="f30ff-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="f30ff-116">Kullanıcı oturum açma işlemlerine eski Office istemci uygulamalarına (Office 2013 veya önceki).</span><span class="sxs-lookup"><span data-stu-id="f30ff-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="f30ff-117">Kuruluşlar, modern kimlik doğrulaması için mümkünse geçmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="f30ff-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="f30ff-118">Modern kimlik doğrulama için doğrudan kimlik doğrulama desteği sağlar ancak da yardımcı olur, güvenli kullanıcı hesapları kullanarak [koşullu erişim](../active-directory-conditional-access.md) çok faktörlü kimlik doğrulama (MFA) gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="f30ff-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="f30ff-119">Kullanıcı oturum açmalarına Skype içine iş 2016 Skype dahil olmak üzere iş istemci uygulamaları için.</span><span class="sxs-lookup"><span data-stu-id="f30ff-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="f30ff-120">Kullanıcı oturum açma işlemlerine PowerShell v1.0 içine.</span><span class="sxs-lookup"><span data-stu-id="f30ff-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="f30ff-121">Bunun yerine PowerShell v2.0 kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="f30ff-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f30ff-122">Desteklenmeyen senaryolar için çözüm olarak, parola karma eşitlemesini etkinleştirmek [isteğe bağlı özellikler](active-directory-aadconnect-get-started-custom.md#optional-features) Azure AD Connect Sihirbazı sayfasında.</span><span class="sxs-lookup"><span data-stu-id="f30ff-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="f30ff-123">Parola karma eşitlemesi önceki senaryoları için bir geri dönüş olarak görev yapan _yalnızca_ (ve _değil_ doğrudan kimlik doğrulama için genel bir geri dönüş olarak).</span><span class="sxs-lookup"><span data-stu-id="f30ff-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="f30ff-124">Bu senaryolar gerekmiyorsa, parola karması eşitlemesi devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="f30ff-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f30ff-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f30ff-125">Next steps</span></span>
- <span data-ttu-id="f30ff-126">[**Hızlı Başlangıç** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - hale getirmek ve Azure AD doğrudan kimlik doğrulama çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="f30ff-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="f30ff-127">[**Teknik derinlemesine** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.</span><span class="sxs-lookup"><span data-stu-id="f30ff-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="f30ff-128">[**Sık sorulan sorular** ](active-directory-aadconnect-pass-through-authentication-faq.md) -sık sorulan sorulara yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="f30ff-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="f30ff-129">[**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -özelliği ile ilgili genel sorunları çözmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f30ff-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="f30ff-130">[**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f30ff-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="f30ff-131">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="f30ff-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
