---
title: "İki basamaklı doğrulama ayarlarınızı yönetme | Microsoft Docs"
description: "İletişim bilgilerinizi değiştirmek veya aygıtlarınızı yapılandırma dahil olmak üzere Azure multi-Factor Authentication kullanımını yönetin."
services: multi-factor-authentication
keywords: "çok faktörlü kimlik doğrulama istemcisi, kimlik doğrulama sorunu bağıntı kimliği"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>İki aşamalı doğrulama için ayarlarınızı yönetme
Bu makalede, iki aşamalı doğrulama veya çok faktörlü kimlik doğrulama ayarlarını güncelleştirme hakkında sorular yanıtlanmaktadır. Hesabınızda oturum açma sorunu yaşıyor oluştuysa, [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md) sorun giderme Yardımı.

## <a name="where-to-find-the-settings-page"></a>Nerede Ayarları sayfası
Şirketiniz Azure çok faktörlü kimlik doğrulamasını nasıl ayarladığınıza bağlı olarak, ayarlarınızı telefon numaranız gibi değiştirebileceğiniz birkaç yer vardır.

İki aşamalı doğrulamayı yönetmek için belirli bir URL veya adımları BT yöneticinize gönderilen bu yönergeleri izleyin. Aksi takdirde, aşağıdaki yönergeleri herkes için çalışması gerekir. Aşağıdaki adımları izleyin, ancak aynı seçenekleri göremiyorsanız, işiniz veya okulunuz kendi portal özelleştirilmiş anlamına gelir. Bağlantı Azure multi-Factor Authentication portalınız için yöneticinize başvurun.

1. Oturum [https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Sağ üst hesap adınızı seçin, sonra seçin **profil**.  
3. Seçin **ek güvenlik doğrulaması**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. Ek güvenlik doğrulama sayfasında, ayarlarınızı ile yükler.

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a>Telefon numaramı değiştirmek veya ikincil bir sayı eklemek istiyorum
İkincil kimlik doğrulama telefon numaranızı yapılandırılması önemlidir.  Birincil telefon numaranızı ve mobil uygulamanızı büyük olasılıkla aynı telefonda olduğundan, ikincil bir telefon numarası telefonunuz kaybolur veya çalınırsa hesabınızda geri alma kuramaz tek yoludur.

> [!NOTE]
> Erişim birincil telefon numaranız varsa ve hesabınıza başlarken yardıma gerek yoktur, bizim Yardım konularına bakın [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md).  

**Birincil telefon numaranızı değiştirmek için:**  

1. Ek güvenlik doğrulama sayfasında, geçerli bir telefon numarası metin kutusunu seçin ve yeni telefon numaranızı ile düzenleyin.  
2. **Kaydet**’i seçin.  
3. Bu, tercih edilen doğrulama seçeneğini için kullandığınız sayı ise, kaydedebilmek için öncelikle yeni numarayı doğrulamak gerekir.  

**İkincil bir telefon numarası eklemek için:**  

1. Ek güvenlik doğrulama sayfasında yanındaki kutuyu işaretleyin **alternatif kimlik doğrulaması telefon.**  
2. İkincil telefon numaranızı metin kutusuna girin.  
3. Seçin **kaydetmek** ve değişikliklerinizi tamamlandı.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>İki aşamalı doğrulamayı yeniden güvenilir olarak işaretledikten bir aygıt gerektirir

Kuruluş ayarlarınıza bağlı olarak belirten bir onay kutusu olabilir "için sorma **X** gün" tarayıcınızdaki iki aşamalı doğrulama yapılırken. Bu onay kutusunu işaretleyin ve Cihazınızı kaybeder veya hesabınızın güvenliği ihlal olduğunu düşündüğünüz tüm cihazlarınıza iki aşamalı doğrulama geri yüklemeniz gerekir. 

1. Ek güvenlik doğrulama sayfasında, seçin **önceden güvenilen cihazlara geri yükleme çok faktörlü kimlik doğrulaması**.
2. Herhangi bir cihazda oturum açtığınızda iki aşamalı doğrulamayı gerçekleştirmek için istenir. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a>Nasıl eski aygıttan Microsoft Authenticator temizlemek ve yeni bir taşıma?
Uygulamasını cihazınızdan kaldırdığınızda veya cihaz sıfırlama etkinleştirme arka uçtaki kaldırmaz. Daha fazla bilgi için bkz: [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Sonraki adımlar
* Sorun giderme ipuçları alın ve Yardım [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md)
* Ayarlanan [uygulama parolaları](multi-factor-authentication-end-user-app-passwords.md) iki aşamalı doğrulamayı desteklemeyen uygulamalar için.
