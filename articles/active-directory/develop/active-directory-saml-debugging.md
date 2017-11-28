---
title: "aaaHow toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de | Microsoft Docs"
description: "Bilgi nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="ef4d6-103">Nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de</span><span class="sxs-lookup"><span data-stu-id="ef4d6-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="ef4d6-104">SAML tabanlı uygulama tümleştirmesi hata ayıklarken, genellikle yararlı toouse gibi bir araç olan [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML isteği, hello SAML yanıtını ve toohello uygulama verilen hello gerçek SAML belirteci.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="ef4d6-105">Merhaba SAML belirteci inceleyerek tüm hello öznitelikleri gerekli emin olun, hello SAML konu kullanıcı hello ve URI geliyor aracılığıyla beklendiği gibi veren hello.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="ef4d6-106">Merhaba yanıt hello SAML belirteci içeren Azure AD'den genellikle https://login.windows.net sonra bir HTTP 302 yeniden yönlendirme oluşan bir hello ve gönderilen toohello yapılandırılmış olan **yanıt URL'si** hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="ef4d6-107">Bu satırı ve hello seçerek hello SAML belirteci görüntüleyebilirsiniz **denetçiler > WebForms** hello sağ panelde sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="ef4d6-108">Buradan, hello sağ **SAMLResponse** değer ve seçin **Gönder tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="ef4d6-109">Seçip **gelen Base64** hello gelen **dönüştürme** menü toodecode hello belirteci ve içeriğini bakın.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="ef4d6-110">**Not**: toosee Merhaba içeriğine bu HTTP isteği, Fiddler isteminde ihtiyacınız olacak HTTPS trafiği tooconfigure şifrelerinin toodo.</span><span class="sxs-lookup"><span data-stu-id="ef4d6-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ef4d6-111">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="ef4d6-111">Related Articles</span></span>
* [<span data-ttu-id="ef4d6-112">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="ef4d6-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="ef4d6-113">Hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ef4d6-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="ef4d6-114">İçinde talep tooCustomize verilen nasıl Pre-Integrated uygulamalar için SAML belirteci hello</span><span class="sxs-lookup"><span data-stu-id="ef4d6-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png