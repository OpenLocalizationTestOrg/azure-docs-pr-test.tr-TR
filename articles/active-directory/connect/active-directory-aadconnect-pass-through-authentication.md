---
title: "Azure AD Connect: Doğrudan kimlik doğrulama | Microsoft Docs"
description: "Bu makalede, Azure Active Directory (Azure AD) doğrudan kimlik doğrulama ve nasıl kullanıcıların parolalarını şirket içi Active Directory karşı doğrulayarak Azure AD oturum açma işlemleri sağlar açıklanmaktadır."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama nedir, Active Directory, Azure AD, SSO için gerekli bileşenleri yüklemek çoklu oturum açma"
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
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Kullanıcı oturum açma ile Azure Active Directory doğrudan kimlik doğrulaması

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>Azure Active Directory doğrudan kimlik doğrulaması nedir?

Azure Active Directory (Azure AD) doğrudan kimlik doğrulaması, kullanıcıların toosign tooboth şirket içi sağlar ve aynı parolayı kullanarak bulut tabanlı uygulamaları hello. Bu özellik, kullanıcılarınızın daha iyi bir deneyim - daha az bir parola tooremember sağlar ve kullanıcılarınızın olasılığını tooforget nasıl olduğundan BT Yardım Masası maliyetlerini azaltır, toosign. Azure AD kullanarak kullanıcılar oturum açtığında, bu özellik kullanıcıların parolalarını şirket içi Active Directory'nizi karşı doğrudan doğrular.

Bu özellik çok alternatiftir[Azure AD parola karması eşitlemesi](active-directory-aadconnectsync-implement-password-synchronization.md), sağlayan hello bulut kimlik doğrulaması tooorganizations aynı yararı. Ancak, belirli kuruluşlardaki güvenlik ve uyumluluk ilkeleri bu kuruluşların toosend kullanıcıların parolalarını bile formunda bir karma, kendi iç sınırları dışında izin vermez. Doğrudan kimlik doğrulama hello için doğru böyle kuruluşların çözümdür.

![Azure AD doğrudan kimlik doğrulama](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

Doğrudan kimlik doğrulama ile Merhaba birleştirebilirsiniz [sorunsuz çoklu oturum açma](active-directory-aadconnect-sso.md) özelliği. Kullanıcılarınızın şirket makinelerinin Kurumsal ağınızdaki uygulamaları erişirken bu şekilde, kendi parolalarını toosign tootype gerek yoktur.

>[!IMPORTANT]
>Azure AD doğrudan kimlik doğrulama şu anda önizlemede değil.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Azure AD geçişli kimlik doğrulaması kullanarak avantajları

- *Mükemmel bir kullanıcı deneyimi*
  - Kullanıcıların kullanması hello aynı parolaları toosign şirket içi ve bulut tabanlı uygulamalar.
  - Kullanıcıların parola ile ilgili sorunları giderme BT yardım masasına toohello Konuşmayı daha az süre beklemesini.
  - Kullanıcıların tamamlayabilir [Self Servis parola yönetimi](../active-directory-passwords-overview.md) hello bulutta görevler.
- *Kolay toodeploy & yönetme*
  - İçi karmaşık dağıtımlar veya ağ yapılandırması için gerekli.
  - İhtiyaçlarını basit aracı toobe yalnızca şirket içi yüklü.
  - Yönetim olmamasıdır. Merhaba Aracısı geliştirmeler ve hata düzeltmeleri otomatik olarak alır.
- *Güvenlik*
  - Şirket içi parolaları hiçbir zaman hello bulut herhangi bir biçimde depolanır.
  - Merhaba aracı yalnızca ağınıza giden bağlantılar sağlar. Bu nedenle, DMZ olarak da bilinen bir çevre ağında gereksinim tooinstall hello aracısı yoktur.
  - Kullanıcı hesapları ile sorunsuz çalışarak korur [Azure AD koşullu erişim ilkeleri](../active-directory-conditional-access-azure-portal.md), çok faktörlü kimlik doğrulama (MFA) de dahil olmak üzere ve göre [deneme yanılma parola saldırıları filtreleme](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Yüksek oranda kullanılabilir*
  - Ek aracıların birden çok şirket içi sunucuları tooprovide yüksek kullanılabilirliğini oturum açma isteklerini yüklenebilir.

## <a name="feature-highlights"></a>Özellik vurgular

- Kullanıcı oturum açma tüm web tarayıcı tabanlı uygulamalar ve Microsoft Office kullanan istemci uygulamaları destekleyen [modern kimlik doğrulaması](https://aka.ms/modernauthga).
- Oturum açma kullanıcı adları, her iki hello şirket içi varsayılan kullanıcı adı olabilir (`userPrincipalName`) veya Azure AD Connect içinde yapılandırılmış başka bir öznitelik (olarak bilinen `Alternate ID`).
- Merhaba özelliği sorunsuz çalışır [koşullu erişim](../active-directory-conditional-access.md) çok faktörlü kimlik doğrulama (MFA) toohelp gibi özellikleri, kullanıcılarınızın güvenli.
- Birden çok orman ortamlarına AD ormanlar arasında orman güvenleri varsa desteklenir ve ad soneki yönlendirmesi doğru yapılandırılmışsa.
- Boş bir özelliktir ve Azure AD toouse Ücretli tüm sürümleri olması gerekmez.
- Aracılığıyla etkinleştirilebilir [Azure AD Connect](active-directory-aadconnect.md).
- Dinler ve toopassword doğrulama isteklerini yanıtlayan bir basit şirket içi Aracısı kullanır.
- Birden çok aracı yükleme, oturum açma isteklerinin yüksek kullanılabilirlik sağlar.
- Bu [korur](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) parola saldırılarını hello bulutta şirket içi hesaplarınızı karşı deneme yanılma yoluyla yapılan zorla.

## <a name="next-steps"></a>Sonraki adımlar

- [**Hızlı Başlangıç** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - hale getirmek ve Azure AD doğrudan kimlik doğrulama çalıştıran.
- [**Geçerli sınırlamalar** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -bu özellik şu anda önizlemede değil. Hangi senaryoları desteklenir ve hangilerinin olmayan öğrenin.
- [**Teknik derinlemesine** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sık sorulan sorular** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
