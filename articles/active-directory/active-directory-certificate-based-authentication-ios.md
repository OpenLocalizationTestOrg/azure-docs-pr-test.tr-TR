---
title: "aaaAzure Active Directory Sertifika tabanlı kimlik doğrulaması iOS | Microsoft Docs"
description: "Merhaba desteklenen senaryolar ve sertifika tabanlı kimlik doğrulaması ile iOS cihazları çözümlerinde yapılandırma hello gereksinimleri hakkında bilgi edinin"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Azure Active Directory Sertifika tabanlı kimlik doğrulaması iOS

Sertifika tabanlı kimlik doğrulaması (CBA) Azure Active Directory tarafından Windows, Android veya iOS aygıtında bir istemci sertifikası ile Exchange online hesabınızı bağlanırken kimlik doğrulaması toobe sağlar: 

* Microsoft Outlook ve Microsoft Word gibi Office mobil uygulamaları   
* Exchange ActiveSync (EAS) istemcileri 

Bu özelliği yapılandıran hello gerek tooenter bir kullanıcı adı ve parola birleşimi belirli mail ve Microsoft Office uygulamaları, mobil Cihazınızda içine ortadan kaldırır. 

Bu konu, hello gereksinimleri ve desteklenen hello senaryoları ile Office 365 Kurumsal, iş, eğitim, ABD devlet kurumları, Çin kiracılar kullanıcılarının iOS(Android) cihazında CBA yapılandırmak için sağlar ve Almanya planları.

Bu özellik, Office 365 US Government savunma ve Federal planlarda Önizleme'de kullanılabilir.




## <a name="office-mobile-applications-support"></a>Office mobil uygulamaları desteği

| Uygulamalar | Destek |
| --- | --- |
| Azure Information Protection uygulama |![İşaretli][1] |
| Microsoft Teams |![İşaretli][1] |
| OneNote |![İşaretli][1] |
| OneDrive |![İşaretli][1] |
| Outlook |![İşaretli][1] |
| Power BI mobil uygulamaları |![İşaretli][1] |
| Skype Kurumsal |![İşaretli][1] |
| Word / Excel / PowerPoint |![İşaretli][1] |
| Yammer |![İşaretli][1] |


## <a name="requirements"></a>Gereksinimler 

Merhaba aygıt işletim sistemi sürümü iOS 9 olmalıdır ve üstü 

Bir federasyon sunucusunun yapılandırılması gerekir.  

Office uygulamaları iOS için Microsoft Authenticator gereklidir.  

Azure Active Directory toorevoke bir istemci sertifikası hello ADFS belirteç talep aşağıdaki hello sahip olmanız gerekir:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (Merhaba sertifikanın seri numarası hello istemci) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (Merhaba veren hello istemci sertifikasının hello dize) 

Merhaba ADFS belirteç (veya başka bir SAML belirteci) kullanılabilir olmaları durumunda azure Active Directory bu talep toohello yenileme belirteci ekler. Merhaba yenileme belirteci doğrulanmış toobe gerektiğinde, bu bilgiler kullanılan toocheck hello iptal olur. 

En iyi uygulama, hello aşağıdakilerle hello ADFS hata sayfaları güncelleştirmeniz gerekir:

* Merhaba gereksinim İos'ta hello Microsoft Authenticator yüklemek için
* Yönergeler tooget bir kullanıcı sertifikası. 

Daha fazla ayrıntı için bkz: [hello AD FS oturum açma sayfalarını özelleştirme](https://technet.microsoft.com/library/dn280950.aspx).

Bazı Office uygulamaları (modern kimlik doğrulaması etkin ile) Gönder '*oturum açma istemini =*' tooAzure AD kendi isteği. Varsayılan olarak, Azure AD bu hello isteği tooADFS çok dönüşür '*wauth usernamepassworduri =*' (ADFS toodo U/P auth ister) ve '*wfresh = 0*' (ADFS tooignore SSO durumu ister ve yeni bir kimlik doğrulaması yapın) . Bu uygulamalar için sertifika tabanlı kimlik doğrulaması tooenable istiyorsanız toomodify hello varsayılan Azure AD davranışını gerekir. Yalnızca kümesi hello '*PromptLoginBehavior*' federasyon etki alanını ayarlarınızda çok '*devre dışı*'. Merhaba kullanabilirsiniz [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform bu görevi:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Exchange ActiveSync istemcileri desteği
İOS 9 veya sonrası, hello yerel iOS posta istemcisi desteklenir. Diğer tüm Exchange ActiveSync uygulamaları için toodetermine bu özellik destekleniyorsa, kişi, uygulama geliştiricisi.  


## <a name="next-steps"></a>Sonraki adımlar

Ortamınızda tooconfigure sertifika tabanlı kimlik doğrulaması istiyorsanız, bkz: [Android sertifika tabanlı kimlik doğrulamasını kullanmaya başlama](active-directory-certificate-based-authentication-get-started.md) yönergeler için.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
