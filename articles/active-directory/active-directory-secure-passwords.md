---
title: "Azure AD parola güvenlik katmanlı | Microsoft Docs"
description: "Açıklar nasıl Azure AD güçlü parolalar zorlar ve siber suçlular kullanıcı parolaları korur"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a>Azure AD parola güvenlik çok katmanlı bir yaklaşım

Bu makalede, bir kullanıcı, Azure Active Directory (Azure AD) veya Microsoft Account korumak için bir yönetici olarak veya izleyebilirsiniz bazı en iyi uygulamalar açıklanmıştır.

 > [!NOTE]
 > Azure AD Yöneticiler makalesindeki yönergeleri kullanarak kullanıcı parolalarını sıfırlama [Azure Active Directory'de bir kullanıcı parolasını sıfırlama](active-directory-users-reset-password-azure-portal.md).
 >
 > Kullanıcıların makalesindeki yönergeleri kullanarak kendi parolasını sıfırlama [Azure AD parolamı unuttum Yardım](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Parola gereksinimleri

Azure AD, parolaların güvenliğini sağlama konusunda aşağıdaki genel yaklaşımları benimser:

* Parola uzunluğu gereksinimleri
* Parola karmaşıklık gereksinimleri
* Normal ve düzenli parola sona erme süresi

Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için Ek Yardım konusuna [Azure AD Self Servis parola sıfırlama için BT Uzmanı](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Azure AD parola korumaları

Azure AD ve Microsoft hesabı sistemi yaklaşımlar kanıtlanmış endüstri dahil olmak üzere kullanıcı ve yönetici parolaların güvenli koruma sağlamak için kullanın:

* Dinamik olarak yasaklanmış parolalar
* Akıllı Parola Kilitleme

Geçerli araştırmaya dayanarak parola yönetimi hakkında daha fazla bilgi için teknik incelemesine bakın [parola Kılavuzu](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Dinamik olarak yasaklanmış parolalar

Azure AD ve Microsoft Accounts yaygın olarak kullanılan parolalar banning tarafından dinamik olarak parola koruması koruyun. Azure ID Kimlik Koruma ekibi, yasaklı parola listelerini düzenli olarak analiz eder ve kullanıcıların yaygın olarak kullanılan parolaları seçmesini engeller. Bu hizmet, Azure AD ve Microsoft Hesap Hizmeti müşterileri tarafından kullanılabilir.

Parolalar oluştururken, yöneticilerin harfler, sayılar, karakterler veya sözcükler benzersiz bir bileşimi dahil parola tümcecikleri seçmek için kullanıcıları teşvik için önemlidir. Bu yaklaşım, kullanıcı parolalarını neredeyse imkansız gizliliği ihlal edilmiş, ancak kullanıcılar için hatırlaması daha kolay yapmak için yardımcı olur.

#### <a name="password-breaches"></a>Parola ihlallerinden

Microsoft, her zaman tek bir adımda siber suçlular öncesinde kalmak için çalışmaktadır.

Azure AD Kimlik Koruması ekibi, yaygın olarak kullanılan parolaları sürekli olarak analiz eder. Siber suçlular da saldırılarını geliştirmek üzere parola karmalarını çözmek için [şifre tablosu](https://en.wikipedia.org/wiki/Rainbow_table) oluşturmak gibi benzer stratejiler kullanır.

Microsoft dinamik olarak güncellenen bir yasaklı parola listesi tutmak üzere [veri ihlallerini](https://www.privacyrights.org/data-breaches) sürekli olarak analiz eder; bu liste, güvenlik açığı olan parolaların Azure AD müşterileri için gerçek bir tehdit haline gelmesinden önce engellenmesini sağlar. Geçerli güvenlik çalışmalarımız hakkında daha fazla bilgi için bkz. [Microsoft Güvenlik Bilgileri Raporu](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Akıllı Parola Kilitleme

Azure AD bir kullanıcı parolasına saldırmaya çalışan olası bir siber suçluyu algıladığında, kullanıcı hesabı Akıllı Parola Kilitleme özelliğiyle kilitlenir. Azure AD, belirli oturumlarla ilişkili riski belirlemek için tasarlanmıştır. En güncel güvenlik verileri kullanarak daha sonra biz siber tehditleri durdurmaya kilitleme semantiği uygulayın.

Bir kullanıcı Azure AD dışında kilitliyse kendi ekran izleyen bir benzer:

  ![Azure AD dışında kalmış](./media/active-directory-secure-passwords/locked-out-azuread.png)

Diğer Microsoft hesapları için kendi ekran izleyen bir benzer:

  ![Microsoft hesabı dışında kalmış](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için Ek Yardım konusuna [Azure AD Self Servis parola sıfırlama için BT Uzmanı](active-directory-passwords.md).

  >[!NOTE]
  >Bir Azure AD yöneticisiyseniz, kullanıcıların geleneksel parolalar oluşturmasını önlemek için [Windows Hello](https://www.microsoft.com/windows/windows-hello) kullanabilirsiniz.
  >

## <a name="next-steps"></a>Sonraki adımlar

* [Kendi parolanızı güncelleştirme](active-directory-passwords-update-your-own-password.md)
* [Azure kimlik yönetimi ile ilgili temel bilgiler](fundamentals-identity.md)
* [Raporda parola sıfırlama etkinliği](active-directory-passwords-reporting.md)


