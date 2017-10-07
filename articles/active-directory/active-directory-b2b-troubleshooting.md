---
title: "Azure Active Directory B2B işbirliği aaaTroubleshooting | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği ile ortak sorunları çözümler"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Azure Active Directory B2B işbirliği sorunlarını giderme

Azure Active Directory (Azure AD) B2B işbirliği ile ortak sorunları için bazı çözümler aşağıda verilmiştir.


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Bir dış kullanıcı eklediğiniz, ancak bunların benim genel adres defteri veya hello Kişi Seçici görmez

Burada dış kullanıcılar hello listesinde doldurulmaz durumlarda, birkaç dakika tooreplicate hello nesne alabilir.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>B2B Konuk kullanıcı SharePoint Online/OneDrive kişiler seçicide göstermiyor 
 
Merhaba özelliği toosearch hello SharePoint Online (SPO) Kişi Seçici varolan Konuk kullanıcılar için varsayılan toomatch eski davranışı tarafından Kapalı'dır.

Bu özellik 'ShowPeoplePickerSuggestionsForGuestUsers' hello Kiracı ve site koleksiyonu düzeyinde ayarlanması hello kullanarak etkinleştirebilirsiniz. Üyeleri izin veren hello kümesi SPOTenant ve Set-SPOSite cmdlet'lerini kullanarak hello özelliğini ayarlayabilirsiniz toosearch hello dizinindeki tüm mevcut Konuk kullanıcılar. Değişiklikler hello Kiracı kapsamda zaten sağlanan SPO site etkilemez.

## <a name="invitations-have-been-disabled-for-directory"></a>Dizin için davet devre dışı bırakıldı

İzinleri tooinvite kullanıcılar olmadığını bildirilir olursa, kullanıcı hesabınızın yetkili tooinvite dış kullanıcılar kullanıcı ayarları altında olduğundan emin olun:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Kısa süre önce bu ayarları veya değiştirdiyseniz hello Konuk davet eden rol tooa kullanıcı atanmış ise hello değişikliklerin etkili olması 15-60 dakikalık bir gecikmeyle olabilir.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>ı davet hello kullanıcı kullanım sırasında bir hata alıyor

Sık karşılaşılan hatalar şunlardır:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>Davetlilerin yönetici kendi Kiracı oluşturulan EmailVerified kullanıcılar izin verilmiyor

Ne zaman, kuruluşunuzun Azure Active Directory'yi kullanarak, ancak burada, özel kullanıcı hesabına hello kullanıcıları davet yok (örneğin, hello kullanıcı Azure AD contoso.com yok). contoso.com Merhaba yönetici kullanıcılar oluşturulmasını engelleyerek yerinde bir ilke olabilir. Dış kullanıcılar izin veriliyorsa hello kullanıcı kendi yönetim toodetermine ile denetlemeniz gerekir. Merhaba dış kullanıcının yönetici kendi etki alanındaki kullanıcıların e-posta doğrulandı tooallow gerekebilir (Bu bkz [makale](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) e-posta doğrulandı kullanıcıların üzerinde).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>Dış kullanıcı zaten bir Federasyon etki alanında mevcut değil

Federasyon kimlik doğrulaması kullanıyorsanız ve hello kullanıcı Azure Active Directory'de zaten yoksa, hello kullanıcı davet edilemez.

Bu sorun, hello tooresolve dış kullanıcının yönetici hello kullanıcının hesabı tooAzure Active Directory eşitleme gerekir.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Nasıl mu\#', olmayan normal olarak geçerli bir karakter, Azure AD ile eşitleme?

"\#" Merhaba hesap davet UPN'ler içinde Azure AD B2B işbirliği veya dış kullanıcılar için ayrılmış bir karakter çünkü user@contoso.com user_contoso.com# haleEXT@fabrikam.onmicrosoft.com. Bu nedenle, \# şirket içinden gelen UPN'ler içinde toosign toohello Azure portal izin verilmez. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Dış kullanıcılar tooa ekleme Grup eşitlendiğinde bir hata alıyorsunuz

Dış kullanıcılar yalnızca çok "atanan" eklenebilir veya şirket içi "Güvenlik" gruplarını ve değil misiniz toogroups yönetilen.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>My dış kullanıcı bir e-posta tooredeem almadı.

Merhaba davet edilene ISS ile denetlemelisiniz veya adres aşağıdaki hello istenmeyen posta Filtresi tooensure izin verilir:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>I hello özel ileti bazen davet iletileri ile birlikte almaz dikkat edin.

toocomply gizlilik yasalarıyla ile bizim API'leri içermeyen özel iletileri hello e-posta davetinde zaman:

- Merhaba davet eden Kiracı davet hello bir e-posta adresi yok
- Bir uygulama hizmeti asıl hello davet gönderdiğinde

Bu senaryoda önemli tooyou ise, bizim API davet e-posta bastırmak ve tercih ettiğiniz e-posta mekanizma hello gönderebilirsiniz. Kuruluşunuzun yasal Danışmanı toomake bu şekilde gönderdiğiniz e-posta ayrıca gizlilik yasalarına uygun emin başvurun.

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [Merhaba B2B işbirliği davet e-posta Hello öğeleri](active-directory-b2b-invitation-email.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B işbirliği lisanslama](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B işbirliği API ve özelleştirme](active-directory-b2b-api.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
