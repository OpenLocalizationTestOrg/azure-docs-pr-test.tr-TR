---
title: "aaaAzure AD katmanlı parola güvenlik | Microsoft Docs"
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
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Çok katmanlı bir yaklaşım tooAzure AD parola güvenliği

Bu makalede, Azure Active Directory (Azure AD) veya Microsoft Account veya bir kullanıcı bir yönetici tooprotect olarak izleyebilirsiniz bazı en iyi uygulamalar açıklanmıştır.

 > [!NOTE]
 > Azure AD Yöneticiler hello makalesindeki hello kılavuzu kullanarak kullanıcı parolalarını sıfırlama [Azure Active Directory'de bir kullanıcı için parola sıfırlama hello](active-directory-users-reset-password-azure-portal.md).
 >
 > Kullanıcıların hello makalesinde hello kılavuzu kullanarak kendi parolasını sıfırlama [Azure AD parolamı unuttum Yardım](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Parola gereksinimleri

Azure AD ortak yaklaşımlar toosecuring parolaları aşağıdaki hello içerir:

* Parola uzunluğu gereksinimleri
* Parola karmaşıklık gereksinimleri
* Normal ve düzenli parola sona erme süresi

Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için hello konusuna [Azure AD Self Servis parola sıfırlama hello BT uzmanları için](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Azure AD parola korumaları

Azure AD ve Microsoft hesap sisteminde kullanmak kanıtlanmış endüstri hello yaklaşıyor dahil olmak üzere kullanıcı ve yönetici parolalarını tooensure güvenli koruma:

* Dinamik olarak yasaklanmış parolalar
* Akıllı Parola Kilitleme

Geçerli araştırmaya dayanarak parola yönetimi hakkında daha fazla bilgi için hello teknik incelemesine bakın [parola Kılavuzu](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Dinamik olarak yasaklanmış parolalar

Azure AD ve Microsoft Accounts yaygın olarak kullanılan parolalar banning tarafından dinamik olarak parola koruması koruyun. Hello Azure kimliği kimlik koruması takım Engellenenler parola listeleri, kullanıcıların yaygın olarak kullanılan parolalar seçmesini önleyerek düzenli olarak analiz eder. Bu, kullanılabilir tooAzure AD ve hello Microsoft hesabı hizmet müşterileri hizmetidir.

Parolalar oluştururken, harfler, sayılar, karakterler veya sözcükler benzersiz bir bileşimini içeren Yöneticiler tooencourage kullanıcılar toochoose parola tümcecikleri için önemlidir. Bu yaklaşım, ancak kullanıcılar tooremember daha kolay neredeyse imkansız toobe tehlikeye toomake kullanıcı parolalarını yardımcı olur.

#### <a name="password-breaches"></a>Parola ihlallerinden

Microsoft, her zaman tek bir adımda toostay siber suçlular öncesinde çalışmaktadır.

Hello Azure AD Identity Protection ekibine yaygın olarak kullanılan parolalar sürekli analiz eder. Siber suçlular yapı gibi kendi saldırıları benzer stratejileri tooinform de bir [şifre tablo](https://en.wikipedia.org/wiki/Rainbow_table) parola karmaları çözme için.

Microsoft sürekli olarak çözümler [veri ihlallerinden](https://www.privacyrights.org/data-breaches) toomaintain gerçek haline gelmeden önce güvenlik açığı parolaları yasaklanan sağlayan dinamik olarak güncelleştirilen Engellenenler parola listesini tehdit tooAzure AD müşteriler. Merhaba bizim geçerli güvenlik çalışmaları hakkında daha fazla bilgi için bkz: [Microsoft Güvenlik Intelligence rapor](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Akıllı Parola Kilitleme

Azure AD kullanıcı parolanıza olası bir siber suçlunun çalışırken toohack algıladığında, biz akıllı parola kilitleme hello kullanıcı hesabıyla kilitleyin. Azure AD tasarlanmıştır belirli oturum açma oturumlarıyla ilişkili toodetermine hello risk. Merhaba en güncel güvenlik verileri kullanarak daha sonra biz kilitleme semantiği toostop siber tehditleri uygulayın.

Bir kullanıcı Azure AD dışında kilitliyse kendi ekran benzer toohello izleyen bir görünür:

  ![Azure AD dışında kalmış](./media/active-directory-secure-passwords/locked-out-azuread.png)

Diğer Microsoft hesapları için kendi ekran benzer toohello izleyen bir görünür:

  ![Microsoft hesabı dışında kalmış](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Parola Azure Active Directory'de sıfırlama hakkında daha fazla bilgi için hello konusuna [Azure AD Self Servis parola sıfırlama hello BT uzmanları için](active-directory-passwords.md).

  >[!NOTE]
  >Azure AD Yöneticiyseniz, toouse isteyebilirsiniz [Windows Hello](https://www.microsoft.com/windows/windows-hello) kullanıcılarınızın sahip tooavoid geleneksel parolaları tamamen oluşturun.
  >

## <a name="next-steps"></a>Sonraki adımlar

* [Nasıl tooupdate kendi parolanızı](active-directory-passwords-update-your-own-password.md)
* [Azure Kimlik Yönetimi Hello temelleri](fundamentals-identity.md)
* [Raporda parola sıfırlama etkinliği](active-directory-passwords-reporting.md)


