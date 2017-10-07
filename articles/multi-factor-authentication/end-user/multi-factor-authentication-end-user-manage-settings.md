---
title: "aaaManage iki basamaklı doğrulama ayarlarınızı | Microsoft Docs"
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
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>İki aşamalı doğrulama için ayarlarınızı yönetme
Bu makalede nasıl hakkında sorular yanıtlanmaktadır iki aşamalı doğrulama veya çok faktörlü kimlik doğrulaması için tooupdate ayarlar. Tooyour hesabında imzalama sorunları yaşıyorsanız, çok başvuran[iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md) sorun giderme Yardımı.

## <a name="where-toofind-hello-settings-page"></a>Burada toofind hello Ayarları sayfası
Şirketiniz Azure çok faktörlü kimlik doğrulamasını nasıl ayarladığınıza bağlı olarak, ayarlarınızı telefon numaranız gibi değiştirebileceğiniz birkaç yer vardır.

BT yöneticiniz belirli URL veya adımları toomanage iki aşamalı doğrulamayı gönderirse, bu yönergeleri izleyin. Aksi durumda, yönergeleri izleyerek hello herkes için çalışması gerekir. Aşağıdaki adımları izleyin, ancak görmüyorum Merhaba, işiniz veya okulunuz kendi portal özelleştirilmiş anlamına aynı seçenekleri. Yöneticinizden hello bağlantı tooyour Azure çok faktörlü kimlik doğrulama portalı için isteyin.

1. Çok oturum[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Merhaba üst sağ hesap adınızı seçin, sonra seçin **profil**.  
3. Seçin **ek güvenlik doğrulaması**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. Merhaba ek güvenlik doğrulama sayfasında, ayarlarınızı ile yükler.

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>I toochange Telefon numaramı istediğiniz veya ikincil bir sayı Ekle
Önemli tooconfigure bir ikincil kimlik doğrulama telefon numarası olur.  Birincil telefon numarası ve mobil uygulamanızı çünkü olan büyük olasılıkla hello üzerinde aynı telefon, hello ikincil telefon numarası telefonunuz kaybolur veya çalınırsa mümkün tooget geri hesabınızda olacaktır hello tek yoludur.

> [!NOTE]
> Erişim tooyour birincil telefon numarası varsa ve tooyour hesabında başlarken yardıma gerek yoktur, bizim Yardım konularına bakın [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange birincil telefon numarası:**  

1. Hello ek güvenlik doğrulama sayfasında, geçerli bir telefon numarası ile Merhaba metin kutusunu seçin ve yeni telefon numaranızı ile düzenleyin.  
2. **Kaydet**’i seçin.  
3. Bu, tercih edilen doğrulama seçeneğini için kullandığınız hello sayı ise, kaydedebilmek için öncelikle tooverify hello yeni numarasına sahip.  

**tooadd ikincil bir telefon numarası:**  

1. Merhaba ek güvenlik doğrulama sayfasında hello sonraki çok onay kutusunu**alternatif kimlik doğrulaması telefon.**  
2. İkincil telefon numaranızı hello metin kutusuna girin.  
3. Seçin **kaydetmek** ve değişikliklerinizi tamamlandı.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>İki aşamalı doğrulamayı yeniden güvenilir olarak işaretledikten bir aygıt gerektirir

Kuruluş ayarlarınıza bağlı olarak belirten bir onay kutusu olabilir "için sorma **X** gün" tarayıcınızdaki iki aşamalı doğrulama yapılırken. Bu onay kutusunu işaretleyin ve Cihazınızı kaybeder veya hesabınızın güvenliği ihlal olduğunu düşündüğünüz iki aşamalı doğrulama tooall aygıtlarınızı geri yüklemeniz gerekir. 

1. Merhaba ek güvenlik doğrulama sayfasında, seçin **önceden güvenilen cihazlara geri yükleme çok faktörlü kimlik doğrulaması**.
2. Merhaba herhangi bir cihazda oturum açtığınızda, istendiğinde tooperform iki aşamalı doğrulamayı olmanız. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>Nasıl eski aygıttan Microsoft Authenticator temizlemek ve tooa yeni bir taşıma?
Aygıt ya da sıfırlama hello aygıt hello uygulamasını kaldırdığınızda hello etkinleştirme hello arka uçtaki kaldırmaz. Daha fazla bilgi için bkz: [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Sonraki adımlar
* Sorun giderme ipuçları alın ve Yardım [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md)
* Ayarlanan [uygulama parolaları](multi-factor-authentication-end-user-app-passwords.md) iki aşamalı doğrulamayı desteklemeyen uygulamalar için.
