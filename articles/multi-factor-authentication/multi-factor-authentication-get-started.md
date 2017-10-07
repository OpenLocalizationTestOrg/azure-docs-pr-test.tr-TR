---
title: "Azure MFA Bulut veya sunucu arasında aaaChoose | Microsoft Docs"
description: "I toosecure ve Kullanıcılarım nerede çalışıyor bulunan neyi isteyerek, sizin için uygun olan hello çok faktörlü kimlik doğrulaması güvenlik çözümünüzü seçin.  Sonra bulut, MFA Sunucusu ya da AD FS arasından seçim yapın."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Sizin için Hello Azure multi-Factor Authentication çözümünü seçin
Çeşitli özellikleri Azure çok faktörlü kimlik doğrulama (MFA) olduğundan, size birkaç soru toofigure hangi sürümüdür hello uygun bir toouse yanıtlamanız gerekir.  Bu sorular şunlardır:

* [Ne toosecure çalışıyorum](#what-am-i-trying-to-secure)
* [Merhaba kullanıcıların bulunduğu](#where-are-the-users-located)
* [Hangi özelliklere ihtiyacım var?](#what-featured-do-i-need)

Merhaba aşağıdaki bölümlerde her Bu yanıtlar belirleme kılavuzluk.

## <a name="what-am-i-trying-toosecure"></a>Ne toosecure çalışıyorum?
toodetermine hello doğru iki aşamalı doğrulama çözümü, ilk biz, çalışırken toosecure ikinci bir kimlik doğrulama yöntemi ile nelerdir, hello sorusuna yanıt vermeniz gerekir.  Bu, Azure’da olan bir uygulama mi?  Veya uzaktan erişim sistemi mi?  Ne numaralı çalışıyoruz belirleme tarafından toosecure, biz yanıt burada çok faktörlü kimlik doğrulaması etkin toobe gereken hello sorunu çözmez.  

| Çalışırken toosecure nelerdir | Merhaba bulutta MFA | MFA Sunucusu |
| --- |:---:|:---:|
| Birinci taraf Microsoft uygulamaları |● |● |
| Merhaba uygulama galerisinde SaaS uygulamaları |● |  |
| Azure AD Uygulaması Proxy üzerinden yayımlanan web uygulamaları |● |  |
| Azure AD Uygulaması Proxy üzerinden yayımlanmayan IIS uygulamaları | |● |
| VPN, RDG gibi uzaktan erişim | ● | ● |

## <a name="where-are-hello-users-located"></a>Merhaba kullanıcıların bulunduğu
Ardından, kullanıcılarımızın bulunduğu adresindeki arayan toodetermine hello doğru çözüm toouse hello bulutta olup olmadığını veya yardımcı olur. kullanarak şirket içi MFA sunucusu hello.

| Kullanıcı Konumu | Merhaba bulutta MFA | MFA Sunucusu |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| AD FS ile federasyon kullanana Azure AD ve şirket içi AD |● |● |
| DirSync, Azure AD Sync, Azure AD Connect kullanan Azure AD ve şirket içi AD - parola eşitleme yok |● |● |
| DirSync, Azure AD Sync, Azure AD Connect kullanan Azure AD ve şirket içi AD - parola eşitleme ile |● | |
| Şirket içi Active Directory | |● |

## <a name="what-features-do-i-need"></a>Hangi özelliklere ihtiyacım var?
Merhaba aşağıdaki tabloda hello multi-Factor Authentication sunucusu ile Merhaba bulutta multi-Factor Authentication ile kullanılabilen hello özellikleri karşılaştırılmaktadır.

| Özellik | Merhaba bulutta MFA | MFA Sunucusu |
| --- |:---:|:---:|
| İkinci öğe olarak mobil uygulama bildirimi | ● | ● |
| İkinci öğe olarak mobil uygulama doğrulama kodu | ● | ● |
| İkinci öğe olarak telefon araması | ● | ● |
| İkinci öğe olarak tek yönlü SMS | ● | ● |
| İkinci öğe olarak iki yönlü SMS | | ● |
| İkinci öğe olarak Donanım Belirteçleri | | ● |
| MFA'yı desteklemeyen Office 365 istemcileri için uygulama parolaları | ● | |
| Kimlik doğrulama yöntemleri üzerinde yönetici denetimi | ● | ● |
| PIN modu | | ● |
| Sahtekarlık uyarısı |● | ● |
| MFA Raporları |● | ● |
| Bir Kerelik Atlama | | ● |
| Telefon aramaları için özel karşılama | ● | ● |
| Telefon aramaları için özelleştirilebilir arayan kimliği | ● | ● |
| Güvenilen IP'ler | ● | ● |
| Güvenilen cihazlar için MFA hatırlama | ● | |
| Koşullu erişim | ● | ● |
| Önbellek |  | ● |

## <a name="next-steps"></a>Sonraki adımlar

Göre toouse bulut olmadığını çok faktörlü kimlik doğrulaması veya içi MFA sunucusu Merhaba, biz Başlarken ayarlama ve Azure multi-Factor Authentication kullanarak belirledik. **Senaryonuz temsil hello simgesini seçin**

<center>




[![Bulut](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Sunucu](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
