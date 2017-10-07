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
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Azure Active Directory sorunsuz çoklu oturum açma: teknik derinlemesine bakış

Bu makalede hello Azure Active Directory sorunsuz çoklu oturum açma (sorunsuz SSO) özelliğinin nasıl çalıştığı içine teknik ayrıntılar sağlar.

>[!IMPORTANT]
>Merhaba sorunsuz SSO özelliği şu anda önizlemede değil.

## <a name="how-does-seamless-sso-work"></a>Sorunsuz SSO nasıl çalışır?

Bu bölüm iki bölümden tooit vardır:
1. Merhaba sorunsuz SSO özelliği Hello kurulumu.
2. Nasıl bir tek kullanıcı oturum açma işlemi ile sorunsuz SSO çalışır.

### <a name="how-does-set-up-work"></a>Nasıl iş ayarlamak?

Sorunsuz SSO etkin gösterildiği gibi Azure AD Connect'i kullanarak [burada](active-directory-aadconnect-sso-quick-start.md). Merhaba özelliği etkinleştirirken, aşağıdaki adımları hello oluşur:
- Adlı bir bilgisayar hesabı `AZUREADSSOACCT` (Azure AD temsil eden), şirket içi Active Directory (AD) oluşturulur.
- Merhaba bilgisayar hesabının Kerberos şifre çözme anahtarı güvenli bir şekilde Azure AD ile paylaşılır.
- Ayrıca, iki Kerberos hizmet asıl adları (SPN) Azure AD oturum açma sırasında kullanılan toorepresent iki URL'leri oluşturulur.

>[!NOTE]
> Hello bilgisayar hesabı ve hello Kerberos SPN'lerinin her AD ormanında oluşturulan tooAzure AD eşitleme (Azure AD Connect'i kullanarak) ve olan kullanıcılar için sorunsuz SSO istiyor. Merhaba taşıma `AZUREADSSOACCT` bilgisayar hesabı tooan kuruluş birimi (OU) içinde yönetilen saklı tooensure olduğu diğer bilgisayar hesapları hello aynı şekilde ve silinmez.

>[!IMPORTANT]
>Yüksek oranda öneririz, [hello Kerberos şifre çözme anahtarı alma](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) Merhaba, `AZUREADSSOACCT` bilgisayar hesabı en az 30 günde.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Nasıl oturum sorunsuz SSO çalışmak açma?

Merhaba Kurulum tamamlandıktan sonra tümleşik Windows kimlik doğrulaması (IWA) kullanan aynı yolla diğer olarak oturum açma hello sorunsuz SSO çalışır. Merhaba akışı aşağıdaki gibidir:

1. Merhaba kullanıcı çalıştığında tooaccess bir uygulama (örneğin, Outlook Web App - hello https://outlook.office365.com/owa/) bir etki alanına katılmış kurumsal bir CİHAZDAN Kurumsal ağınızdaki.
2. Merhaba kullanıcı zaten oturum açmamış, hello kullanıcının yeniden yönlendirilen toohello Azure AD oturum açma sayfası olur.

  >[!NOTE]
  >Hello Azure AD oturum açma isteği içeriyorsa, bir `domain_hint` (örneğin, Kiracı - tanımlama, contoso.onmicrosoft.com) veya `login_hint` (Merhaba kullanıcı - Örneğin, tanımlayan user@contoso.onmicrosoft.com veya user@contoso.com) parametre sonra 2. adım atlanır.

3. kullanıcı adlarını hello Azure AD oturum açma sayfası içine Hello kullanıcı türleri.
4. JavaScript hello arka planda kullanarak, Azure AD bir Kerberos anahtarı hello tarayıcı 401 Yetkisiz bir yanıt olan tooprovide yoluyla sınar.
5. Merhaba tarayıcı sırayla isteklerini bir bilet Active Directory'den Merhaba `AZUREADSSOACCT` (Azure AD temsil eden) bilgisayar hesabı.
6. Active Directory hello bilgisayar hesabı bulur ve hello bilgisayar hesabının parolası ile şifrelenmiş bir Kerberos bileti toohello tarayıcı döndürür.
7. Merhaba tarayıcı iletir Active Directory tooAzure AD edinilen hello Kerberos bileti (Merhaba birinde [Azure AD URL'leri toohello tarayıcısının Intranet bölgesi ayarlarından daha önce eklediğiniz](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Merhaba hello Kurumsal cihaz imzalı hello kullanıcının kimliğini içeren azure AD şifrelerinin çözülmesi hello Kerberos bileti, hello kullanarak önceden paylaşılan anahtar.
9. Değerlendirme sonra Azure AD belirteci geri toohello uygulama döndürür ya da çok faktörlü kimlik doğrulaması gibi ek sağlamaları hello kullanıcı tooperform sorar.
10. Merhaba kullanıcı oturum açma başarılı olursa, hello kullanıcı mümkün tooaccess hello uygulamasıdır.

Merhaba Aşağıdaki diyagramda tüm hello bileşenleri ve hello adımlar gösterilmektedir.

![Sorunsuz çoklu oturum açma](./media/active-directory-aadconnect-sso/sso2.png)

Sorunsuz SSO fırsatçılıktan, başarısız olursa hello oturum açma deneyimini döner geri tooits normal davranış - yani, hello başka bir deyişle, kullanıcının kendi parola toosign tooenter gerekir.

## <a name="next-steps"></a>Sonraki adımlar

- [**Hızlı Başlangıç** ](active-directory-aadconnect-sso-quick-start.md) - hale getirmek ve Azure AD sorunsuz SSO çalışıyor.
- [**Sık sorulan sorular** ](active-directory-aadconnect-sso-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
