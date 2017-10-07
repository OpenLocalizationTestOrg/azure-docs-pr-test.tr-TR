---
title: "aaaAuthenticating aracılığıyla parolası olmayan kimlikleri iş ve Azure AD için Windows Hello | Microsoft Docs"
description: "İş ve iş için Windows Hello dağıtma hakkında ek bilgi için Windows Hello genel bakış sağlar."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Kimlik doğrulama aracılığıyla parolası olmayan kimlikleri iş için Windows Hello
Merhaba geçerli parolalar tek başına ile kimlik doğrulama yöntemlerinin yeterli tookeep kullanıcılar güvenli değildir. Kullanıcıların yeniden kullanmak ve parolaları unutmayın. Parolaları olan breachable, phishable, yatkın toocracks ve guessable. Yatkın tooattacks gibi ve bunlar da zor tooremember Al "[hello karma değer geçişi](https://technet.microsoft.com/dn785092.aspx)".

## <a name="about-windows-hello-for-business"></a>İş için Windows Hello hakkında
İş için Windows Hello bir özel/ortak anahtarı veya parolaları gider sertifika tabanlı kimlik doğrulaması yaklaşım kuruluşlar ve tüketicileri için kullanılabilir. Bu form kimlik doğrulaması parolaları ve olan dayanıklı toobreaches, thefts ve kimlik avı yerini anahtar çifti kimlik bilgilerini kullanır.

 İş için Windows Hello tooa Microsoft hesabı, bir Windows Server Active Directory hesabı, bir Microsoft Azure Active Directory (Azure AD) hesabı veya hızlı kimlik çevrimiçi (FIDO) kimlik doğrulamasını destekleyen Microsoft dışı hizmet kimlik doğrulaması sağlar. İşletme kaydı için bir ilk iki aşamalı doğrulama sırasında Windows Hello sonra iş için Windows Hello hello kullanıcının cihazında ayarlanır ve Windows Hello veya bir PIN olabilir bir hareketi hello kullanıcı ayarlar. Merhaba kullanıcı kimliklerini hello hareketi tooverify sağlar. Windows iş tooauthenticate hello kullanıcı için Windows Hello kullanır ve korumalı tooaccess kaynaklarını ve Hizmetleri Yardım.

Kullanıcı hello bir akıllı kart toosign toohello aygıt kullanır gibi hello özel anahtarı yalnızca bir PIN, Biyometri veya uzak bir aygıtı gibi "kullanıcı hareketi" yoluyla kullanılabilir hale getirilir. Bu, bağlantılı tooa sertifika ya da değiştirip asimetrik anahtar çifti bilgilerdir. Merhaba özel hello cihazı bir Güvenilir Platform Modülü (TPM) yongası varsa Onaylandı donanım anahtardır. Merhaba özel anahtar asla hello aygıt bırakır.

Hello ortak anahtarı, Azure Active Directory ve Windows Server Active Directory (şirket içi) kaydedilir. Kimlik sağlayıcısı (IDPs) eşleme hello ortak anahtarı hello kullanıcı toohello özel anahtarı tarafından hello kullanıcıyı doğrulamak ve oturum açma bilgileri bir saat parola (OTP), PhoneFactor veya farklı bildirim mekanizması aracılığıyla sağlayın.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Neden kuruluşların iş için Windows Hello benimsemeye
İş için Windows Hello etkinleştirerek, kuruluşların kaynaklarına göre daha da güvenli yapabilirsiniz:

* İş için Windows Hello donanım tercih edilen bir seçeneğiyle ayarlama. Bu anahtarlar TPM 1.2 veya TPM 2.0 kullanılabilir olduğunda oluşturulması anlamına gelir. TPM mevcut olmadığında, yazılım hello anahtarı oluşturur.
* Tanımlama hello karmaşıklığı ve hello uzunluğu sabitleme ve Hello kullanım, kuruluşunuzda etkinleştirilip etkinleştirilmediğini gösterir.
* Windows Hello iş toosupport akıllı kart gibi senaryolar için sertifika tabanlı güven kullanarak yapılandırma.

## <a name="how-windows-hello-for-business-works"></a>İş için Windows Hello işleyişi
1. Anahtarları hello donanımda TPM veya yazılım tarafından oluşturulur. Birçok cihaz hello donanım cihazlarının şifreleme anahtarları ile tümleştirerek güvenliğini sağlar yerleşik bir TPM yongası vardır. TPM 1.2 veya TPM 2.0 anahtar veya oluşturulan hello anahtarlarından oluşturulan sertifika oluşturur.
2. Bu donanım ilişkili tuşlarını Hello TPM gösterir.
3. Tek unlock hareketi hello cihaz kilidini açar. Merhaba cihaz etki alanına katılmış veya Azure ise bu hareketi AD alanına katılmış toomultiple kaynaklara erişmesine izin verir.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>İş yaşam döngüsü için Windows Hello hello nasıl çalışır?
![İş yaşam döngüsü için Windows Hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Merhaba önceki diyagramda hello özel/ortak anahtar çifti ve hello doğrulama hello kimlik sağlayıcısı tarafından gösterilmektedir. Bu adımların her biri aşağıda ayrıntılı olarak açıklanmıştır:

1. Merhaba kullanıcı kimliklerini kanıtlayan birden fazla yerleşik sağlama yöntemleri (hareketleri, fiziksel akıllı kartlar, çok faktörlü kimlik doğrulaması) ve bu bilgileri tooan Azure Active Directory gibi kimlik sağlayıcısı (IDP) gönderir veya şirket içi Active Directory.
2. Hello cihaz ardından hello anahtarı oluşturur, hello anahtar gösterir, bu anahtarı hello ortak kısmını alır, istasyon ifadelerle ekler, oturum açtığında ve toohello IDP tooregister hello anahtar gönderir.
3. Merhaba IDP hello anahtarının ortak kısmını hello kaydeder hemen hello IDP zorluklar aygıt toosign hello özel hello anahtar bölümünü ile Merhaba.
4. Merhaba IDP ardından doğrular ve sorunları hello kullanıcı ve hello aygıt hello korumalı kaynaklara erişmesine imkan tanıyan kimlik doğrulama belirteci hello. IDPs platformlar arası uygulamalar yazma veya tarayıcı (JavaScript/Webcrypto API) aracılığıyla destek toocreate kullanın ve Windows Hello için kullanıcılar iş kimlik bilgileri kullanın.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>İş için Windows Hello Hello dağıtım gereksinimleri
### <a name="at-hello-enterprise-level"></a>Merhaba Kurumsal düzeyde
* Merhaba kuruluş Azure aboneliği sahiptir.

### <a name="at-hello-user-level"></a>Merhaba kullanıcı düzeyinde
* Merhaba kullanıcının bilgisayarı Windows 10 Professional veya Enterprise çalışır.

Ayrıntılı dağıtım yönergeleri için bkz: [hello kuruluşunuzda iş için Windows Hello etkinleştirmek](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Ek bilgiler
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

