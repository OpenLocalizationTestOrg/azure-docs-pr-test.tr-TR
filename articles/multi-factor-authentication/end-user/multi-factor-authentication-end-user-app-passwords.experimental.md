---
title: "aaaHow toouse Azure MFA uygulama parolaları? | Microsoft Belgeleri"
description: "Bu sayfayı kullanıcıların uygulama parolaları nedir ve ne olduklarını anlamasına yardımcı olacak şekilde tooAzure MFA ile kullanılır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Azure çok faktörlü kimlik doğrulaması'ndaki uygulama parolaları nedir?
Exchange Active Sync kullanan hello Apple yerel e-posta istemcisi gibi belirli bir tarayıcı olmayan uygulamaları, şu anda çok faktörlü kimlik doğrulamasını desteklemez. Çok faktörlü kimlik doğrulaması kullanıcı başına etkinleştirilir.  Başka bir deyişle, bir kullanıcı, çok faktörlü kimlik doğrulamasını kullanamaz:

- Merhaba kullanıcı çok faktörlü kimlik doğrulaması için etkinleştirildi
- Merhaba kullanıcı toouse bir tarayıcı olmayan uygulaması çalışıyor.

Bir uygulama parolası hello kullanıcı toouse hello uygulama sağlar.

Bir uygulama parolası sahip olduktan sonra özgün parolanızı bu tarayıcı olmayan uygulamaları ile yerine kullanın. İki aşamalı doğrulama için kaydolduğunuzda, hello ikinci doğrulama de gerçekleştirilemiyor, Microsoft olmayan herhangi bir kişi oturum toolet parolanızla oturum söyleyen. iki aşamalı doğrulama için istenemez olduğundan telefonunuzda hello Apple yerel e-posta istemcisi olarak oturum açamaz. Merhaba çözüm toothis toocreate kullanmadığınız daha güvenli bir uygulama parolası sorunudur günlük. Uygulama parolaları, iki aşamalı doğrulamayı destekleyemez yalnızca bu uygulamalar içindir. Uygulamalar çok faktörlü kimlik doğrulamasını atlamak ve toowork devam hello uygulama parolasını kullanın.


> [!NOTE]
> Office 2013 istemcileri (Outlook dahil) destekleyen yeni kimlik doğrulama protokolleri ve iki aşamalı doğrulamayla birlikte kullanılabilir. Uygulama parolaları Office 2013 istemcilerle kullanım için gerekli değildir.  Daha fazla bilgi için bkz: [Office 2013 modern kimlik doğrulaması genel önizlemesi Duyuruldu](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Nasıl toouse uygulama parolaları
Uygulama parolaları hakkında bazı şeyleri tooknow şunlardır:

* Kendi uygulama parolaları oluşturmayın. Bunlar otomatik olarak oluşturulur.
* Şu anda kullanıcı başına 40 parolalık bir sınırı yoktur. 
* Merhaba sınırına ulaştınız sonra toocreate bir uygulama parolası çalışırsanız, yeni bir tane oluşturmadan önce toodelete varolan uygulama parolalarınızdan birini sahip olacaksınız.
* Bir uygulama parolası aygıt başına, uygulama başına değil kullanın. Örneğin, dizüstü bilgisayarınız için bir uygulama parolası oluşturmanız ve tüm Dizüstü bilgisayarınızdaki uygulamalar için bu uygulama parolasını kullanın. Ardından, tüm uygulamalarınız için ikinci bir uygulama parolası toouse masaüstünüzde oluşturun. 
* Kaydettiğiniz ilk kez iki aşamalı doğrulama için bir uygulama parolası hello verilir.  Ek olanları ihtiyacınız varsa, bunları oluşturabilirsiniz.



## <a name="creating-and-deleting-app-passwords"></a>Oluşturma ve uygulama parolaları silme
İlk oturum açma işleminiz sırasında kullanabileceğiniz bir uygulama parolası verilir.  Ayrıca, oluşturabilir ve daha sonra uygulama parolalarını Sil. Uygulama parolalarını Sil nasıl çok faktörlü kimlik doğrulaması nasıl kullandığınıza bağlıdır. Aşağıdaki yanıt hello toomanage uygulama parolaları nereye toodetermine sorular: 

1. Kişisel Microsoft hesabınız için iki aşamalı doğrulama kullanıyor musunuz? Yanıt Evet ise, toohello başvurmalıdır [uygulama parolaları ve iki aşamalı doğrulamayı](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) Yardım makalesi. Öyle değilse, iki tooquestion devam edin.

2. İş veya Okul hesabınız için iki aşamalı doğrulamayı kullanmak için Tamam. Bu toosign tooOffice 365 uygulamalarında kullanıyorsunuz? Yanıt Evet ise, çok başvurmalıdır[Office 365 için bir uygulama parolası oluşturmanız](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) Yardım. Öyle değilse, tooquestion üç devam edin. 

3. Microsoft Azure ile iki aşamalı doğrulama kullanıyor musunuz? Yanıt Evet ise, toohello devam [hello Azure portalında uygulama parolaları yönetme](#manage-app-passwords-in-the-Azure-portal) bu makalenin. Öyle değilse, tooquestion dört devam edin.

4. İki aşamalı doğrulamayı kullandığınızda emin değil misiniz? Toohello devam [hello MyApps portal ile uygulama parolaları yönetme](#manage-app-passwords-with-the-myapps-portal) bu makalenin. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Hello Azure portalında uygulama parolaları yönetme
İki aşamalı doğrulamayı Azure ile kullanırsanız, toocreate uygulama parolaları hello Azure portal aracılığıyla istiyor.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>hello Azure portal toocreate uygulama parolaları
1. İçinde toohello Klasik Azure portalında oturum açın.
2. Merhaba üstünde, kullanıcı adını sağ tıklatın ve ek güvenlik doğrulama'yı seçin.
3. Uygulama parolaları hello üstünde hello düzenleyebileceğinizi sayfasında seçin
4. **Oluştur**'a tıklayın.
5. Merhaba uygulama parolası için bir ad girin ve tıklayın **sonraki**
6. Merhaba uygulama parolası toohello panoya kopyalayın ve uygulamanıza yapıştırın.
   
   ![Bulut](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>hello Azure portal toodelete uygulama parolaları
1. İçinde toohello Klasik Azure portalında oturum açın.
2. Merhaba üstünde, kullanıcı adını sağ tıklatın ve ek güvenlik doğrulama'yı seçin.
3. Merhaba üstünde, sonraki tooadditional güvenlik doğrulama seçin **uygulama parolaları.**
4. Toodelete, select istediğiniz sonraki toohello uygulama parolası **silmek**.
5. Merhaba silmeyi onaylamak **Evet**.
6. Merhaba uygulama parolası silindikten sonra tıklayabilirsiniz **kapatmak**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Uygulama parolaları hello MyApps portalı ile yönetin.
Çok faktörlü kimlik doğrulaması kullanımını emin değilseniz, daha sonra her zaman oluşturabilir ve hello myapps portalı üzerinden uygulama parolalarını Sil.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>kullanarak bir uygulama parolası toocreate hello Myapps portalı
1. Çok oturum[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Adınızı hello üst sağ tıklatın ve seçin **profil**.
3. Seçin **ek güvenlik doğrulaması**.
   ![Ek güvenlik doğrulaması - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Seçin **uygulama parolaları**.
   ![Uygulama parolaları - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. **Oluştur**'a tıklayın.
6. Merhaba uygulama parolası için bir ad girin ve tıklayın **sonraki**.
7. Merhaba uygulama parolası toohello panoya kopyalayın ve uygulamanıza yapıştırın.
   ![Bir uygulama parolası oluşturma](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>kullanarak bir uygulama parolası toodelete hello Myapps portalı
1. Çok oturum[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Merhaba üstünde profilini seçin.
3. Seçin **ek güvenlik doğrulaması**.

   ![Ek güvenlik doğrulaması - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Seçin **uygulama parolaları**.

   ![Uygulama parolaları - ekran görüntüsü seçin](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Toodelete, istediğiniz sonraki toohello uygulama parolası tıklatın **silmek**.

   ![Bir uygulama parolası Sil](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Tıklayarak, bu parolayı toodelete istediğinizi onaylamak **Evet**.
7. Merhaba uygulama parolası silindikten sonra tıklayabilirsiniz **kapatmak**.

## <a name="next-steps"></a>Sonraki adımlar

- [İki basamaklı doğrulama ayarlarınızı yönetme](multi-factor-authentication-end-user-manage-settings.md)

- Merhaba deneyin [Microsoft Authenticator uygulaması](microsoft-authenticator-app-how-to.md) tooverify oturum açma işlemleri metinleri veya aramaları almasını yerine uygulama bildirimleri ile. 
