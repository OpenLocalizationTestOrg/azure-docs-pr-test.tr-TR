---
title: "Azure Active Directory B2C: E-posta doğrulama tüketici kaydolma sırasında devre dışı bırakma | Microsoft Docs"
description: "Nasıl toodisable e-posta doğrulama tüketici Azure Active Directory B2C'de kaydolma sırasında gösteren bir konu"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: Tüketicinin kaydolma devre dışı bırak e-posta doğrulama
Etkin olduğunda, tüketici bir Azure Active Directory (Azure AD) B2C verir özelliği toosign uygulamalar için bir e-posta adresi sağlayarak ve yerel bir hesap oluşturma hello. Azure AD B2C, tüketiciye tooverify kılarak geçerli e-posta adresleri sağlar hello kaydolma işlemi sırasında bunları. Ayrıca, kötü amaçlı bir otomatik işlem'in hello uygulamaları için sahte hesapları oluşturma engeller.

Bazı uygulama geliştiricileri tooskip e-posta doğrulama hello kaydolma işlemi sırasında tercih ve bunun yerine hello e-posta adresini doğrulayın. daha sonra bir tüketiciye sahip. Bu, Azure AD B2C için toosupport yapılandırılmış toodisable e-posta doğrulama olabilir. Bunun yapılması daha sorunsuz bir kaydolma işlemi oluşturur ve geliştiricilerin sahip değilse bu Tüketiciler, e-posta adresinden doğruladıktan hello esneklik toodifferentiate hello tüketicileri sağlar.

Varsayılan olarak, e-posta doğrulama açık kayıt ilkeleri vardır. Kullanım hello adımları tooturn onu devre dışı:

1. [Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Tıklatın **kayıt ilkeleri** veya **oturum açma veya kaydolma ilkeleri** için yapılandırdığınıza bağlı olarak kaydolma.
3. İlke (örneğin, "B2C_1_SiUp") tooopen'ı tıklatın. Tıklatın **Düzenle** hello dikey penceresinde hello üstünde.
4. Tıklatın **sayfa UI özelleştirme**.
5. Tıklatın **yerel hesap kayıt sayfasına**.
6. Tıklatın **e-posta adresi** hello içinde **adı** hello sütununda **kaydolma özniteliklerini** bölümü.
7. İki durumlu hello **bölgedeki tüm sitelerden** çok seçenek**Hayır**.
8. Tıklatın **Tamam** hello ulaşana kadar hello altındaki **Düzenle İlkesi** dikey.
9. Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde. İşiniz bittiğinde!

> [!NOTE]
> E-posta doğrulama hello kaydolma işlemini devre dışı bırakma toospam neden olabilir. Merhaba varsayılan devre dışı bırakırsanız, kendi doğrulama sistemi ekleme öneririz.
> 
> 

Her zaman açık toofeedback ve öneriler duyuyoruz! Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, hello sayfanın hello sonundaki görüşlerinize değer veriyoruz. Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
