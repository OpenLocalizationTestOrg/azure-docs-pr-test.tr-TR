---
title: "aaaAzure MFA oturum açma ile iki aşamalı doğrulama | Microsoft Docs"
description: "Bu sayfa, burada toogo toosee hello oturum açma Azure MFA ile kullanılabilen yöntemleri hakkında kılavuzluk sağlar."
keywords: "Kullanıcı kimlik doğrulaması, oturum açma deneyimi, cep telefonu ile oturum aç ofis telefonu ile oturum açma"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication ile Merhaba oturum açma deneyimi
> [!NOTE]
> Bu makalede Hello amacı tipik bir oturum açma deneyimi aracılığıyla toowalk budur. Oturum açma veya tootroubleshoot sorunları ile ilgili Yardım için bkz [Azure multi-Factor Authentication sorununuz](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Oturum açma deneyimini ne olacak?
Oturum açma deneyimini toouse ikinci faktörü olarak seçtiğiniz öğeye bağlı olarak farklılık gösterir: telefon araması, bir kimlik doğrulama uygulaması veya metinleri. En iyi ne yaptığınızı açıklayan hello seçenek belirleyin:

| Nasıl oturum? | 
| --- |
| [Olan bir telefon araması toomy cep telefonu numarası veya office telefon](#signing-in-with-a-phone-call) |
| [Metin toomy cep telefonuyla](#signing-in-with-a-text-message)
| [Merhaba Microsoft Authenticator uygulaması ile bildirim](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Merhaba Microsoft Authenticator uygulaması ile doğrulama kodları](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Alternatif bir yöntem ile my tercih edilen yöntem şu anda kullanamazsınız çünkü](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Bir telefon araması oturum imzalama
Aşağıdaki bilgilerle hello hello iki aşamalı doğrulama deneyimi bir çağrı tooyour mobil veya ofis telefonu açıklar.

1. Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.  
2. Microsoft, çağırır.  
3. Merhaba telefona yanıt verin ve hello # tuşuna basın.  

## <a name="signing-in-with-a-text-message"></a>SMS mesajı oturum imzalama
Aşağıdaki bilgilerle hello hello iki aşamalı doğrulama metin iletisi tooyour cep telefonu deneyimiyle açıklanmaktadır:

1. Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın. 
2. Microsoft bir numara kodu içeren bir kısa mesaj gönderir. 
3. Oturum açma hello sayfada sağlanan hello kutusuna Hello kodu girin. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Merhaba Microsoft Authenticator uygulama ile oturum açılmasını 
Merhaba aşağıdaki bilgiler için iki aşamalı Doğrulamalar hello Microsoft Authenticator uygulaması kullanılarak hello deneyimi açıklar. İki farklı şekilde toouse hello uygulama vardır. Cihazınızda anında iletme bildirimleri alabilir veya hello uygulama tooget bir doğrulama kodu açabilirsiniz.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>bir bildirim hello Microsoft Authenticator uygulamadan oturum toosign
1. Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.
2. Microsoft, Cihazınızda bir bildirim toohello Microsoft Authenticator uygulaması gönderir.

  ![Microsoft bildirim gönderir](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Telefon ve select hello açık hello bildirim **doğrula** anahtarı. Şirketiniz bir PIN gerektiriyorsa, buraya girin.
4. Artık oturum açmanız.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>Merhaba Microsoft Authenticator uygulamasıyla doğrulama kodunu kullanarak toosign

Merhaba Microsoft Authenticator uygulama tooget doğrulama kodları kullanırsanız, hello uygulamasını açın, sonra bir sayı, hesap adı altında görürsünüz. Bu sayı her 30 saniyede değiştirir, böylece aynı iki kez sayı hello kullanmayın. İçin bir doğrulama kodu sorulduğunda, hello uygulamasını açın ve sayıyı görüntülenmekte kullanın. 

1. Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.
2. Microsoft için bir doğrulama kodu ister.

  ![Doğrulama kodunu girin](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Telefonunuz Hello Microsoft Authenticator uygulamasını açın ve burada oturum hello kutusunda hello kodu girin.

## <a name="signing-in-with-an-alternate-method"></a>Alternatif bir yöntem ile imzalama
Bazen hello telefon veya tercih edilen doğrulama yöntemi olarak ayarladığınız cihaz yok. Hesabınız için yedekleme yöntemleri ayarlamak öneririz neden bu durumda. Merhaba aşağıdaki bölümde, nasıl gösterilir birincil yönteminiz kullanılamayabilir, alternatif bir yöntem oturum toosign.

1. Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.
2. Seçin **farklı bir doğrulama seçeneği kullanma**. Kaç tane Kurulum sahip bağlı olarak farklı bir doğrulama seçeneklerini bakın.
3. Alternatif bir yöntem seçin ve oturum açın.

  ![Alternatif yöntemi kullanın.](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Sonraki adımlar

İki aşamalı doğrulamayı oturum imzalama sorunlarınız varsa, daha fazla bilgi almak [Azure multi-Factor Authentication sorununuz](multi-factor-authentication-end-user-troubleshoot.md).

Nasıl çok öğrenin[iki basamaklı doğrulama ayarlarınızı yönetme](multi-factor-authentication-end-user-manage-settings.md).

Çok öğrenin[hello Microsoft Authenticator uygulaması ile çalışmaya başlama](microsoft-authenticator-app-how-to.md) böylece bildirimleri toosign, metinleri ve telefon aramaları yerine kullanabilirsiniz. 
