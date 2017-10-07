---
title: "Azure AD Connect: Doğrudan kimlik doğrulama - nasıl çalışır? | Microsoft Belgeleri"
description: "Bu makalede, Azure Active Directory doğrudan kimlik doğrulaması nasıl çalıştığı açıklanmaktadır."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Azure Active Directory doğrudan kimlik doğrulaması: Teknik derinlemesine bakış

>[!IMPORTANT]
>Azure AD doğrudan kimlik doğrulama şu anda önizlemede değil. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Azure Active Directory doğrudan kimlik doğrulaması nasıl çalışır?

Bir kullanıcı Azure Active Directory (Azure AD) tarafından güvenli hale getirilmiş bir uygulamaya toosign çalışır ve hello Kiracı'geçişli kimlik doğrulaması etkinleştirilirse hello aşağıdaki adımlardan oluşur:

1. Merhaba kullanıcı çalıştığında tooaccess bir uygulama (örneğin, Outlook Web App - hello https://outlook.office365.com/owa/).
2. Merhaba kullanıcı zaten oturum açmamış, hello kullanıcının yeniden yönlendirilen toohello Azure AD oturum açma sayfası olur.
3. Merhaba kullanıcı oturum açma hello Azure AD sayfasına, kullanıcı adı ve parolasını girer ve hello "Oturum" düğmesine tıklar.
4. Merhaba oturum açma isteği alırken azure AD hello kullanıcı adı ve parola (bir ortak anahtar kullanılarak şifrelenmiş) bulunan bir sıra yerleştirir.
5. Bir şirket içi doğrudan kimlik doğrulama Aracısı giden çağrı toohello sıra yapar ve hello kullanıcı adı ve şifrelenmiş parola alır.
6. Merhaba Aracısı özel anahtarını kullanarak hello parola şifresini çözer.
7. Merhaba Aracısı sonra hello kullanıcı adı ve parola (benzer bir mekanizma toowhat Active Directory Federasyon Hizmetleri tarafından kullanılır) standart Windows API'leri kullanarak Active Directory karşı doğrular. Merhaba kullanıcı adı ya da hello şirket içi varsayılan kullanıcı adı olabilir (genellikle `userPrincipalName`) veya Azure AD Connect içinde yapılandırılmış başka bir öznitelik (olarak bilinen `Alternate ID`).
8. Merhaba şirket içi Active Directory etki alanı denetleyicisi (DC) sonra hello isteği değerlendirir ve hello uygun yanıtı döndürür (başarılı, başarısız, parolanın süresi doldu veya kullanıcı kilitli) toohello aracı.
9. Merhaba Aracısı, buna karşılık, bu yanıt geri tooAzure AD döndürür.
10. Azure AD hello yanıt değerlendirir ve toohello kullanıcı uygun şekilde yanıt - Örneğin, hello hemen oturum açtığında ya da çok faktörlü kimlik doğrulama (MFA için) ister.
11. Merhaba kullanıcı oturum açma başarılı olursa, hello kullanıcı mümkün tooaccess hello uygulamasıdır.

Merhaba Aşağıdaki diyagramda tüm hello bileşenleri ve hello adımlar gösterilmektedir.

![Doğrudan Kimlik Doğrulama](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Sonraki adımlar
- [**Geçerli sınırlamalar** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -bu özellik şu anda önizlemede değil. Hangi senaryoları desteklenir ve hangilerinin olmayan öğrenin.
- [**Hızlı Başlangıç** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - hale getirmek ve Azure AD doğrudan kimlik doğrulama çalıştıran.
- [**Sık sorulan sorular** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
