---
title: "Kullanıcılar ve aygıtlar - Azure MFA aaaAdmins yönetme | Microsoft Docs"
description: "Bu, nasıl hello kullanıcılar toodo zorlama gibi toochange kullanıcı ayarları güçlü işlem yeniden hello açıklar."
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Merhaba bulutta Azure multi Factor Authentication ile kullanıcı ayarlarını yönetme
Yönetici olarak, kullanıcı ve aygıt ayarlarını aşağıdaki hello yönetebilirsiniz:

* Kullanıcıların tooprovide iletişim yöntemlerini yeniden gerektirir
* Uygulama parolalarını Sil
* Tüm güvenilen aygıtlarda MFA gerektirir 

## <a name="require-users-tooprovide-contact-methods-again"></a>Kullanıcıların tooprovide iletişim yöntemlerini yeniden gerektirir
Bu ayar hello kullanıcı toocomplete hello kayıt işlemini yeniden zorlar. Merhaba kullanıcı bunlar için uygulama parolaları varsa tarayıcı olmayan uygulamalar toowork devam edin.  Ayrıca seçerek hello kullanıcıların uygulama parolaları silebilirsiniz **hello seçilen kullanıcılar tarafından oluşturulan mevcut tüm uygulama parolalarını Sil**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>Nasıl toorequire kullanıcılar tooprovide iletişim yöntemlerini yeniden
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba solda seçin **Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm kullanıcılar**.
3. Seçin **çok faktörlü kimlik doğrulaması**. Merhaba çok faktörlü kimlik doğrulaması sayfasını açar. 
4. Merhaba kutusunu sonraki toohello kullanıcı veya kullanıcılar toomanage istediğiniz kontrol edin. Hızlı adım seçeneklerin bir listesini hello sağ görünür. 
5. Seçin **kullanıcı ayarlarını yönetin**.
6. Hello kutuyu **seçilen kullanıcıların iletişim yöntemlerini yeniden tooprovide**.
   ![İletişim yöntemleri sağlar](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. **Kaydet**’e tıklayın.
8. Tıklatın **kapatmak**.

## <a name="delete-users-existing-app-passwords"></a>Uygulama parolaları varolan kullanıcıları Sil
Bu ayar, bir kullanıcının oluşturduğu hello uygulama parolaları siler. Bu uygulama parolalarıyla ilişkilendirilmiş tarayıcı olmayan uygulamaları yeni bir parola oluşturuluncaya kadar çalışmasını durdurabilir.

### <a name="how-toodelete-users-existing-app-passwords"></a>Nasıl toodelete kullanıcıların uygulama parolaları var
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba solda seçin **Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm kullanıcılar**.
3. Seçin **çok faktörlü kimlik doğrulaması**. Merhaba çok faktörlü kimlik doğrulaması sayfasını açar. 
6. Merhaba kutusunu sonraki toohello kullanıcı veya kullanıcılar toomanage istediğiniz kontrol edin. Hızlı adım seçeneklerin bir listesini hello sağ görünür. 
7. Seçin **kullanıcı ayarlarını yönetin**.
8. Merhaba kutuyu **hello seçilen kullanıcılar tarafından oluşturulan mevcut tüm uygulama parolalarını Sil**.
   ![Uygulama parolalarını Sil](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. **Kaydet**’e tıklayın.
10. Tıklatın **kapatmak**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>MFA bir kullanıcı için tüm hatırlanan cihazlarda geri yükle
Merhaba yapılandırılabilir özelliklerinden biri Azure çok faktörlü kimlik doğrulaması, kullanıcılarınızın hello seçeneği toomark cihaz güvenilir olarak veren. Daha fazla bilgi için bkz: [Azure çok faktörlü kimlik doğrulaması yapılandırma ayarlarını](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Kullanıcılar, yapılandırılabilir bir normal cihazlarına gün sayısı için iki aşamalı doğrulamayı dışında seçebilirsiniz. Bir hesap tehlikeye veya güvenilir bir aygıt kaybolursa, toobe mümkün tooremove güvenilen hello durum gerekir ve iki aşamalı doğrulamayı yeniden gerektirir.

Merhaba **tüm hatırlanan cihazlarda geri yükleme çok faktörlü kimlik doğrulaması** ayarı anlamına gelir hello kullanıcı yüküyle tooperform iki aşamalı doğrulama hello sonraki sefer oturum, bunlar toomark seçtiğiniz bağımsız olarak kaldırılır, cihaz güvenilir olarak. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Nasıl bir kullanıcı için askıya alınmış tüm cihazlarda toorestore MFA
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba solda seçin **Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm kullanıcılar**.
3. Seçin **çok faktörlü kimlik doğrulaması**. Merhaba çok faktörlü kimlik doğrulaması sayfasını açar. 
6. Merhaba kutusunu sonraki toohello kullanıcı veya kullanıcılar toomanage istediğiniz kontrol edin. Hızlı adım seçeneklerin bir listesini hello sağ görünür. 
7. Seçin **kullanıcı ayarlarını yönetin**.
8. Merhaba kutuyu **tüm hatırlanan cihazlarda geri yükleme çok faktörlü kimlik doğrulaması**
   ![uygulama parolalarını Sil](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. **Kaydet**’e tıklayın.
10. Tıklatın **kapatmak**.

## <a name="next-steps"></a>Sonraki adımlar

- Çok hakkında daha fazla bilgi almak[Azure çok faktörlü kimlik doğrulaması yapılandırma ayarları](multi-factor-authentication-whats-next.md)

- Kullanıcılarınızın yardıma gereksinim duyarsanız, bunları doğru hello noktası [iki aşamalı doğrulama için Kullanıcı Kılavuzu](./end-user/multi-factor-authentication-end-user.md)
