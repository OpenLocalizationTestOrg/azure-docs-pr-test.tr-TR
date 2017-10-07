---
title: "Azure AD Connect eşitleme: hello varsayılan yapılandırmasını değiştirme | Microsoft Docs"
description: "Azure AD Connect eşitleme hello varsayılan yapılandırmasını değiştirmek için en iyi yöntemler sağlar."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Azure AD Connect eşitleme: en iyi uygulamalar hello varsayılan yapılandırmasını değiştirmek için
Bu konunun amacı Hello toodescribe desteklenen ve desteklenmeyen değişiklikleri tooAzure AD Connect Eşitleme ' dir.

Azure AD Connect tarafından oluşturulan hello yapılandırma, Azure AD ile şirket içi Active Directory eşitleme çoğu ortam için "olduğu gibi" çalışır. Ancak, bazı durumlarda, bazı değişiklikler tooa yapılandırma toosatisfy belirli bir gereksinim gerekli tooapply veya gereksinim budur.

## <a name="changes-toohello-service-account"></a>Değişiklikleri toohello hizmet hesabı
Azure AD Connect eşitleme hello Yükleme Sihirbazı tarafından oluşturulan bir hizmet hesabı altında çalışıyor. Bu hizmet hesabı eşitleme tarafından kullanılan hello şifreleme anahtarları toohello veritabanı tutar. İle 127 karakterden uzun bir parola oluşturulur ve hello parola toonot ayarlanmış süresi dolacak.

* Bu **desteklenmeyen** hello hizmet hesabının toochange veya sıfırlama hello parola. Bunun yapılması hello şifreleme anahtarları yok eder ve hello hizmeti mümkün tooaccess hello veritabanı değildir ve mümkün toostart değil.

## <a name="changes-toohello-scheduler"></a>Değişiklikleri toohello Zamanlayıcı
Yapı 1.1 hello sürümlerden itibaren (Şubat 2016) hello yapılandırabilir [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md) farklı bir eşitleme döngüsü hello varsayılandan 30 dakika toohave.

## <a name="changes-toosynchronization-rules"></a>Değişiklikleri tooSynchronization kuralları
Merhaba Yükleme Sihirbazı'nı toowork hello en yaygın senaryolar için beklenen bir yapılandırma sağlar. Toomake değişiklikleri toohello yapılandırmaya ihtiyaç durumunda, bu kurallar toostill desteklenen bir yapılandırmaya sahip izlemeniz gerekir.

* Yapabilecekleriniz [öznitelik akışları değiştirmek](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) hello varsayılan doğrudan öznitelik akışları, kuruluşunuz için uygun değilse.
* Çok istiyorsanız[bir öznitelik akışı değil](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) ve varolan bir özniteliğe toocreate bir kural bu senaryo için gereken sonra Azure AD'de değerlerini kaldırın.
* [İstenmeyen bir eşitleme kuralı devre dışı](#disable-an-unwanted-sync-rule) silmeden yerine. Kuralı silindi yükseltme sırasında yeniden oluşturulur.
* çok[bir out-of-box kuralı değiştirme](#change-an-out-of-box-rule), kural ve hello out-of-box kuralı devre dışı bir kopyasını hello özgün olmanız gerekir. Merhaba eşitleme kuralı Düzenleyicisi ister ve yardımcı olur.
* Özel eşitleme kurallarınızı Hello eşitleme kuralları Düzenleyicisi'ni kullanarak dışarı aktarın. Merhaba Düzenleyici sunar kullanabileceğiniz bir PowerShell Betiği ile tooeasily yeniden bunları bir olağanüstü durum kurtarma senaryosunda.

> [!WARNING]
> Merhaba out-of-box eşitleme kuralı bir parmak izine sahip. Toothese kuralları değişiklik yaparsanız, hello parmak izi artık eşleşen. Azure AD Connect yeni bir sürüm tooapply çalıştığınızda hello gelecekteki sorunlarla karşılaşabilirsiniz. Yalnızca bu makalede, açıklanan değişiklikleri hello şekilde olun.

### <a name="disable-an-unwanted-sync-rule"></a>İstenmeyen bir eşitleme kuralı devre dışı bırak
Bir out-of-box eşitleme kuralı silmeyin. Bir sonraki yükseltme sırasında yeniden oluşturulur.

Bazı durumlarda, hello Yükleme Sihirbazı'nı topolojiniz için çalışmayan bir yapılandırma üretilen. Örneğin, bir hesap-kaynak orman topolojisini var ancak hello Exchange şemasıyla hello hesap ormanındaki genişletilmiş hello şema sahip sonra Exchange için kuralları hello hesap ormanı ve hello kaynak ormanı için oluşturulur. Bu durumda, Exchange için toodisable hello eşitleme kuralı gerekir.

![Devre dışı eşitleme kuralı](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

Yukarıdaki Hello resim içinde hello Yükleme Sihirbazı'nı hello hesap ormanında bir eski Exchange 2003 şema buldu. Merhaba kaynak ormanı Fabrikam'ın ortamında sunulmadan önce bu şema uzantısı eklendi. tooensure hello eşitleme kuralı devre dışı bırakılmalıdır gösterildiği gibi özniteliklere hello eski Exchange uygulamadan eşitlenir.

### <a name="change-an-out-of-box-rule"></a>Out-of-box kuralı değiştirme
toochange hello birleştirme kuralı gerektiğinde bir out-of-box kuralı değiştirmelisiniz hello tek zamandır. Bir öznitelik akışı toochange gerekiyorsa, hello out-of-box kurallarından daha yüksek önceliği olan bir eşitleme kuralı oluşturmanız gerekir. Merhaba kural tooclone pratikte gereksinim kuralı, yalnızca hello **içinde AD'den - kullanıcı katılma**. Daha yüksek bir öncelik kural ile tüm diğer kuralları geçersiz kılabilirsiniz.

Ardından toomake değişiklikleri tooan out-of-box kural gerekiyorsa, hello out-of-box kuralı bir kopyasını alın ve hello özgün kuralı devre dışı bırakmak gerekir. Ardından hello değişiklikleri toohello kopyalanan kuralı yapın. Merhaba eşitleme kuralı Düzenleyicisi bu adımlara yardımcı oluyor. Bir out-of-box kuralı açtığınızda, bu iletişim kutusu sunulur:  
![Uyarı kutusu kural dışında](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Seçin **Evet** toocreate hello kuralın bir kopyası. Merhaba kopyalanan kuralı daha sonra açılır.  
![Kopyalanan kuralı](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

Kopyalanan bu kuralı, tüm gerekli değişiklikleri tooscope, birleştirme ve dönüşümleri yapın.

## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
