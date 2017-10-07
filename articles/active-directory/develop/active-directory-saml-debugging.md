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
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de
SAML tabanlı uygulama tümleştirmesi hata ayıklarken, genellikle yararlı toouse gibi bir araç olan [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML isteği, hello SAML yanıtını ve toohello uygulama verilen hello gerçek SAML belirteci. Merhaba SAML belirteci inceleyerek tüm hello öznitelikleri gerekli emin olun, hello SAML konu kullanıcı hello ve URI geliyor aracılığıyla beklendiği gibi veren hello.

![][1]

Merhaba yanıt hello SAML belirteci içeren Azure AD'den genellikle https://login.windows.net sonra bir HTTP 302 yeniden yönlendirme oluşan bir hello ve gönderilen toohello yapılandırılmış olan **yanıt URL'si** hello uygulamasının. 

Bu satırı ve hello seçerek hello SAML belirteci görüntüleyebilirsiniz **denetçiler > WebForms** hello sağ panelde sekmesindedir. Buradan, hello sağ **SAMLResponse** değer ve seçin **Gönder tooTextWizard**. Seçip **gelen Base64** hello gelen **dönüştürme** menü toodecode hello belirteci ve içeriğini bakın.

**Not**: toosee Merhaba içeriğine bu HTTP isteği, Fiddler isteminde ihtiyacınız olacak HTTPS trafiği tooconfigure şifrelerinin toodo.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](../active-directory-apps-index.md)
* [Hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma](../active-directory-saas-custom-apps.md)
* [İçinde talep tooCustomize verilen nasıl Pre-Integrated uygulamalar için SAML belirteci hello](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png