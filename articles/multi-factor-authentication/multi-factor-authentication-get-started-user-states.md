---
title: "aaaMicrosoft Azure çok faktörlü kimlik doğrulama kullanıcı durumları"
description: "Azure MFA kullanıcı durumları hakkında bilgi edinin."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>Nasıl bir kullanıcı veya grup için toorequire iki aşamalı doğrulamayı

İki aşamalı doğrulama gerektirme iki yaklaşım vardır. Merhaba ilk seçenek tooenable her bağımsız kullanıcı Azure çok faktörlü kimlik doğrulama (MFA) değil. Kullanıcılar tek tek etkinleştirildiğinde, bunlar her zaman iki aşamalı doğrulamayı (bunlar güvenilen IP adreslerinden oturum açtığında veya hello hatırlanan aygıt özelliği açık gibi bazı özel durumlarla birlikte,) gerçekleştirin. Merhaba ikinci seçenek belirli koşullar altında iki aşamalı doğrulama gerektiren bir koşullu erişim ilkesi tooset olur.

>[!TIP] 
>Bu yöntemleri toorequire iki aşamalı doğrulama, ikisini birini seçin. Bir kullanıcı Azure MFA için etkinleştirmeye herhangi koşullu erişim ilkeleri geçersiz kılar.

## <a name="which-option-is-right-for-you"></a>Hangi sizin için uygun bir seçenektir

**Azure MFA kullanıcı durumları değiştirerek etkinleştirme** iki aşamalı doğrulama gerektirme hello geleneksel bir yaklaşımdır. Her iki hello bulutta Azure MFA ve Azure MFA sunucusu için çalışır. Sağlayan tüm hello hello kullanıcınız tooperform iki aşamalı doğrulamayı oturum her zaman olan aynı deneyimi. Bir kullanıcının kullanıcı etkileyebilecek herhangi bir koşullu erişim ilkeleri geçersiz kılar. 

**Koşullu erişim ilkesi ile Azure MFA'yı etkinleştirerek** iki aşamalı doğrulama gerektirme daha esnek bir yaklaşımdır. Yalnızca çalışır hello bulutta Azure MFA için yine de ve koşullu erişim bir [Özelliği Azure Active Directory Ücretli](https://www.microsoft.com/cloud-platform/azure-active-directory-features). Tek tek kullanıcılar yanı sıra toogroups uygulamak koşullu erişim ilkeleri oluşturabilirsiniz. Daha fazla kısıtlama düşük riskli grupları daha yüksek riskli grupları verilebilir veya iki aşamalı doğrulamayı yalnızca yüksek riskli bulut uygulamaları için gereklidir ve düşük riskli için olanları atlandı. 

Bu seçeneklerin ikisi de Azure multi-Factor Authentication hello için kullanıcıların tooregister hello gereksinimleri açtıktan sonra oturum ilk kez ister. Her iki seçenek de hello yapılandırılabilir ile çalışması [Azure çok faktörlü kimlik doğrulama ayarları](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Kullanıcı durumu değiştirerek Azure MFA etkinleştir

Azure multi-Factor Authentication kullanıcı hesaplarında hello aşağıdaki üç ayrı duruma sahiptir:

| Durum | Açıklama | Etkilenen tarayıcı olmayan uygulamalar |
|:---:|:---:|:---:|
| Devre dışı |Yeni bir kullanıcı için varsayılan duruma Hello Azure çok faktörlü kimlik doğrulama (MFA) kayıtlı değil. |Hayır |
| Etkin |Merhaba kullanıcı Azure MFA kayıtlı ancak kayıtlı değil. Kullanıcılar istendiğinde tooregister hello sonraki sefer oturum açın. |Hayır.  Merhaba kayıt işlemi tamamlanana kadar toowork devam edin. |
| Uygulandı |Merhaba kullanıcı kaydolmuş ve Azure MFA için hello kayıt işlemi tamamlandı. |Evet.  Uygulamaları, uygulama parolaları gerekir. |

Bir kullanıcının durumunu olup bir yönetim bunları Azure MFA kaydetmiştir ve hello kayıt işlemi tamamlanmadan yansıtır.

Tüm kullanıcılar Başlat *devre dışı*. Azure MFA, durum değişikliklerini kullanıcılar kaydettiğinizde *etkin*. Etkin kullanıcılar oturum açabilir ve hello kayıt işlemini tamamlayın, durumlarına çok değiştirir*zorunlu*.  

### <a name="view-hello-status-for-a-user"></a>Bir kullanıcı için hello durumunu görüntüle

Burada görüntüleyebilir ve kullanıcı durumları yönetmek tooaccess hello sayfa kullanım hello aşağıdaki adımları:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Çok Git**Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm kullanıcılar**.
3. Seçin **çok faktörlü kimlik doğrulaması**.
   ![Çok faktörlü kimlik doğrulama yöntemini seçin](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Merhaba kullanıcı durumlarını görüntüler, yeni bir sayfa açar.
   ![çok faktörlü kimlik doğrulaması kullanıcı durumu - ekran görüntüsü](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Bir kullanıcı için hello durumunu değiştir

1. Önceki adımları tooget toohello çok faktörlü kimlik doğrulaması kullanıcılar sayfası hello kullanın.
2. Azure MFA için tooenable istediğiniz Bul hello kullanıcı. Toochange gerekebilir hello hello üstünde görüntüle. 
   ![Kullanıcı - ekran görüntüsü Bul](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Merhaba kutusunu sonraki tootheir adını kontrol edin.
4. Hızlı adımlar altında sağ Hello üzerinde seçin **etkinleştirmek** veya **devre dışı**.
   ![Seçilen kullanıcının - ekran görüntüsü](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Etkin* kullanıcılar otomatik olarak geçiş çok*zorlanan* Azure MFA için bunlar kaydetme zaman. Hello kullanıcı durumu tooenforced el ile değiştirmeniz gerekir. 

5. Açılır hello açılır pencerede Seçiminizi onaylayın. 

Kullanıcıların etkinleştirdikten sonra e-posta aracılığıyla haber vermelisiniz. Bunlar tooregister hello bunlar oturum açtığınızda istenir gerektiğini söyleyin. Ayrıca, kuruluşunuz modern kimlik doğrulamayı desteklemeyen tarayıcı olmayan uygulamaları kullanıyorsa, toocreate uygulama parolaları gerekir. Bir bağlantı tooour da içerebilir [Azure MFA Son Kullanıcı Kılavuzu](./end-user/multi-factor-authentication-end-user.md) bunları Başlarken toohelp.

### <a name="use-powershell"></a>PowerShell kullanma
toochange hello kullanıcı durumunu durum kullanarak [Azure AD PowerShell](/powershell/azure/overview), değiştirme `$st.State`. Üç olası durum şunlardır:

* Etkin
* Uygulandı
* Devre dışı  

Kullanıcıların taşıma doğrudan toohello *zorlanmış* durumu. Tarayıcı tabanlı olmayan uygulamalar hello kullanıcı MFA kaydından gitti değil ve elde edilen çalışmayı durdurur bir [uygulama parolası](multi-factor-authentication-whats-next.md#app-passwords). 

Kullanıcıları etkinleştirme toobulk gerektiğinde PowerShell kullanarak iyi bir seçenektir. Kullanıcıların bir listesini döngüler ve bunları sağlayan bir PowerShell Betiği oluşturun:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Örnek aşağıda verilmiştir:

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Azure MFA ile koşullu erişim ilkesini etkinleştir

Koşullu erişim Ücretli Azure Active Directory, birçok olası yapılandırma seçenekleriyle özelliğidir. Bu adımları bir ilke tek yönlü toocreate yol. Hakkında daha fazla bilgi için okuma [Azure Active Directory'de koşullu erişim](../active-directory/active-directory-conditional-access-azure-portal.md).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Çok Git**Azure Active Directory** > **koşullu erişim**.
3. Seçin **yeni ilke**.
4. Altında **atamaları**seçin **kullanıcılar ve gruplar**. Kullanım hello **INCLUDE** ve **hariç** hangi kullanıcıların ve grupların hello İlkesi tarafından yönetilecek toospecify sekmeler.
5. Altında **atamaları**seçin **bulut uygulamaları**. Tooinclude seçin **tüm bulut uygulamaları**.
6. Altında **erişim denetimleri**seçin **Grant**. Seçin **çok faktörlü kimlik doğrulaması gerektiren**.
7. Kapatma **ilkesini etkinleştir** çok**üzerinde** ve ardından **kaydetmek**.

tam olarak iki aşamalı doğrulamayı gerekip gerekmeyeceğini zaman hello diğer seçenekler hello koşullu Erişim İlkesi'nde toospecify sağlar. Örneğin, bildiren bir ilke yapabilir: Yükleniciler tedarik uygulamamıza etki alanına katılmamış cihazlarda güvenilmeyen ağlardan tooaccess çalıştığınızda, iki aşamalı doğrulamayı gerektirir. 

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba ipuçları almak [koşullu erişim için en iyi uygulamaları](../active-directory/active-directory-conditional-access-best-practices.md)

- Çok faktörlü kimlik doğrulaması ayarlarını yönetme [, kullanıcılar ve aygıtları](multi-factor-authentication-manage-users-and-devices.md)