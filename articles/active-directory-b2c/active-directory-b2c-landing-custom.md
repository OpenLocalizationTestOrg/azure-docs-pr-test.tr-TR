---
title: "Azure Active Directory B2C: Özel İlkeler Giriş Sayfası | Microsoft Docs"
description: "Özel İlkeleri kullanarak Azure Active Directory B2C ile tüketiciye yönelik uygulamalar geliştirme"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: 28a39f282488b81fc9e2ab7841b5f2cb4cd58715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="5cb3d-103">Azure Active Directory B2C: Özel ilkeleri kullanarak tüketicilerinizin uygulamanıza kaydolmalarını ve oturum açmalarını sağlama</span><span class="sxs-lookup"><span data-stu-id="5cb3d-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="5cb3d-104">Özel ilkeler, Azure AD B2C kiracısı hello davranışını tanımlayan yapılandırma dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-104">Custom policies are configuration files that define hello behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="5cb3d-105">Bunlar tam olarak bir kimlik Geliştirici toocomplete tarafından görevleri yakın sınırsız sayıda düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-105">They can be fully edited by an identity developer toocomplete a near unlimited number of tasks.</span></span>

## <a name="how-tooarticles"></a><span data-ttu-id="5cb3d-106">Nasıl tooarticles</span><span class="sxs-lookup"><span data-stu-id="5cb3d-106">How-tooarticles</span></span>
<span data-ttu-id="5cb3d-107">Bilgi nasıl toouse belirli Azure Active Directory B2C özellikleri:</span><span class="sxs-lookup"><span data-stu-id="5cb3d-107">Learn how toouse specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="5cb3d-108">Kullanmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="5cb3d-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="5cb3d-109">[Azure AD](active-directory-b2c-setup-aad-custom.md) gibi OIDC Sağlayıcılarını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="5cb3d-110">[Salesforce](active-directory-b2c-setup-sf-app-custom.md) gibi SAML Sağlayıcılarını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="5cb3d-111">RESTful API'lerini tümleştirin:</span><span class="sxs-lookup"><span data-stu-id="5cb3d-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="5cb3d-112">[Ek talep alma](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5cb3d-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="5cb3d-113">[Kullanıcı girişini doğrulama](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5cb3d-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="5cb3d-114">Özel Giriş:</span><span class="sxs-lookup"><span data-stu-id="5cb3d-114">Customize Login:</span></span>
    * [<span data-ttu-id="5cb3d-115">Kullanıcı Erişimini Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5cb3d-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="5cb3d-116">Kullanıcı Arabirimini Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5cb3d-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="5cb3d-117">Belirteci Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5cb3d-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="5cb3d-118">[Application Insights ile günlükleri toplayarak](active-directory-b2c-troubleshoot-custom.md) sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="5cb3d-119">Yenilikler</span><span class="sxs-lookup"><span data-stu-id="5cb3d-119">What's new</span></span>
<span data-ttu-id="5cb3d-120">Geri genellikle toolearn gelecekteki değişiklikler toohello Azure Active Directory B2C hakkında burayı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-120">Check back here often toolearn about future changes toohello Azure Active Directory B2C.</span></span> <span data-ttu-id="5cb3d-121">@AzureAD kullanarak tüm değişiklikler hakkında tweet de göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-121">We'll also tweet about any updates by using @AzureAD.</span></span>



