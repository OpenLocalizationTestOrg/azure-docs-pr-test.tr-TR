---
title: "aaaAzure Active Directory B2B işbirliği API ve özelleştirme | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği Kurumsal uygulamalarınıza iş ortakları tooselectively erişim sağlayarak, şirketler arası ilişkilerinizi destekler."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Azure Active Directory B2B işbirliği API ve özelleştirme

Biz toocustomize hello davet işlem kuruluşlarının en iyi şekilde çalışır şekilde istedikleri bize birçok müşteri karşılaşmışsınız. Bizim API'si ile tam olarak bunu yapabilirsiniz. [https://Developer.microsoft.com/Graph/docs/api-Reference/V1.0/Resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Merhaba davet API özellikleri
Hello API hello aşağıdaki özellikleri sunmaktadır:

1. Bir dış kullanıcı ile davet *herhangi* e-posta adresi.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Bunlar, daveti kabul ettikten sonra kullanıcılar tooland istediğiniz özelleştirin.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Bize aracılığıyla toosend hello standart davet posta seçin

    ```
    "sendInvitationMessage": true
    ```

  özelleştirebileceğiniz bir ileti toohello alıcı

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. Ve toocc seçin: Merhaba tookeep istediğiniz kişilerin döngü, bu ortak çalışanı davet hakkında.

5. Veya Azure AD aracılığıyla değil toosend bildirimleri seçerek daveti ve hazırlama iş akışı tamamen özelleştirebilirsiniz.

    ```
    "sendInvitationMessage": false
    ```

  Bu durumda, bir kullanım URL hello bir e-posta şablonu, anlık ileti veya tercih ettiğiniz başka bir dağıtım yöntem katıştırma API öğesinden ulaşırsınız.

6. Son olarak, bir yönetici, üye olarak tooinvite hello kullanıcı seçebilirsiniz.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Yetkilendirme modeli
Merhaba API yetkilendirme modları aşağıdaki hello çalıştırabilirsiniz:

### <a name="app--user-mode"></a>Uygulama + kullanıcı modu
Bu modda, aktaranın kullanarak hello API gereksinimlerini toohave hello izinleri toobe B2B davetleri oluşturun.

### <a name="app-only-mode"></a>Uygulama yalnızca modu
Uygulama yalnızca bağlamda hello uygulamanın hello davet toosucceed için hello User.ReadWrite.All veya Directory.ReadWrite.All kapsamı gerekir.

Daha fazla bilgi için bkz: https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
Şimdi olası toouse PowerShell tooadd ve davet dış kullanıcılar tooan kuruluş kolayca değil. Merhaba cmdlet'ini kullanarak bir davet oluşturun:

```
New-AzureADMSInvitation
```

Hello aşağıdaki seçenekleri kullanabilirsiniz:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

Merhaba davet API Başvurusu'nda uğradı kontrol edebilirsiniz [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [Merhaba B2B işbirliği davet e-posta Hello öğeleri](active-directory-b2b-invitation-email.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B işbirliği lisanslama](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B işbirliği sorunlarını giderme](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)](active-directory-b2b-faq.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
