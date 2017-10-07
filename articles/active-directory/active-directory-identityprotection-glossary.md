---
title: "Active Directory kimlik koruması Kılavuzu sözlüğü aaaAzure | Microsoft Docs"
description: "Azure Active Directory kimlik koruması Kılavuzu sözlüğü"
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi, sözlük yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Azure Active Directory kimlik koruması Kılavuzu sözlüğü
### <a name="at-risk-user"></a>Risk (kullanıcı)
Bir veya daha fazla etkin risk olaylarına sahip bir kullanıcı. 

### <a name="atypical-sign-in-location"></a>Oturum açma alışılmadık konumu
Bir oturum açma bir coğrafi konumdan hello belirli bir kullanıcı, benzer kullanıcılar veya hello Kiracı için tipik değildir.

### <a name="azure-ad-identity-protection"></a>Azure AD Kimlik Koruması
Birleştirilmiş görünüme risk olaylarına ve olası güvenlik açıklarını kuruluşun kimlikleri etkileyen sağlayan Azure Active Directory güvenlik modül.

### <a name="conditional-access"></a>Koşullu erişim
Erişim tooresources güvenliğini sağlamaya yönelik bir ilke. Koşullu erişim kuralları hello Azure Active Directory'de depolanır ve erişim toohello kaynak vermeden önce Azure AD tarafından değerlendirilir.  Örnek kuralları içeren kullanıcı konuma göre erişimi kısıtlama cihaz sistem durumu veya kullanıcı kimlik doğrulama yöntemi.

### <a name="credentials"></a>Kimlik Bilgileri
Tanımlama ve kullanılan toogain erişim toolocal ve ağ kaynakları kimlik kanıtı içeren bilgiler. Kimlik bilgileri kullanıcı adları ve parolalar, akıllı kartlar ve sertifikalar gösterilebilir.

### <a name="event"></a>Olay
Azure Active Directory'de bir etkinliği kaydı.

### <a name="false-positive-risk-event"></a>Hatalı pozitif (risk olay)
Risk olay durumu hello risk olay araştırılan ve hatalı bir risk olayı olarak bayrak eklenen gösteren bir kimlik koruması kullanıcı tarafından el ile ayarlayın.

### <a name="identity"></a>Kimlik
Bir kişi veya parola veya sertifika gibi ölçütlere göre kimlik doğrulaması yoluyla doğrulanması gereken varlık.

### <a name="identity-risk-event"></a>Kimlik risk olayı
Anormal olarak kimlik koruması tarafından işaretlenen ve bir kimlik tehlikede olduğunu gösterebilecek AAD olay.

### <a name="ignored-risk-event"></a>Göz ardı (risk olay)
El ile bir düzeltme eylemi yapmadan hello risk olay kapalı belirten bir kimlik koruması kullanıcı tarafından ayarlanan risk olay durumu.

### <a name="impossible-travel-from-atypical-locations"></a>Alışılmadık konumlardan imkansız seyahat
Bunlar arasında seyahat iki oturum açma işlemleri için aynı kullanıcı, en az biri bir alışılmadık oturum açma konumundan olduğu algılanır ve hello oturum açma işlemleri arasındaki hello süre hello minimum kısa olduğu zaman hello toophysically götürecek harekete bir risk olayı konumları.  

### <a name="investigation"></a>Araştırma
düzeltme veya azaltma adımları gerekli olup olmadığını hello hello etkinlikleri, günlükler ve diğer ilgili bilgileri gözden geçirme işlemi tooa risk olayı toodecide ilgili, anlamak varsa ve nasıl hello kimlik aşılmış ve anlamak nasıl hello güvenliği aşılmış kimlik kullanıldı.

### <a name="leaked-credentials"></a>Sızan kimlik bilgileri
Geçerli kullanıcı kimlik bilgilerini (kullanıcı adı ve parola) bulunduğunda tetiklenen bir risk olayı hello koyu web bizim Araştırmacıları tarafından yayımlandığını.

### <a name="mitigation"></a>Risk azaltma
Bir eylem toolimit veya hello kimliği veya cihaza tooa güvenli geri yükleme durumunda olmadan hello özelliği, bir saldırganın tooexploit güvenliği aşılmış kimlik veya aygıt ortadan kaldırmak. Bir azaltma hello kimlik veya aygıtla ilişkili önceki risk olaylarını çözümlenmiyor.

### <a name="multi-factor-authentication"></a>Multi-factor authentication
Bu tür bir sertifika hello kullanıcının sahip bir şey içerebilir, iki veya daha fazla kimlik doğrulama yöntemleri gerektiren bir kimlik doğrulama yöntemi; kullanıcı adları, parolalar veya parolalar; gibi hello kullanıcının bildiği bir şeyi bir parmak izi gibi fiziksel öznitelikleri; ve kişisel imza gibi kişisel öznitelikleri.

### <a name="offline-detection"></a>Çevrimdışı algılama
Daha fazla bilgi ve oturum açma girişimi gibi bir olay hello risk değerlendirme zaten gerçekleştirilmedi bir olay için hello olgu sonra Hello algılama.

### <a name="policy-condition"></a>İlke durumu
Merhaba ilkesine dahil veya ondan dışlanan hello varlıkları (grupları, kullanıcıları, uygulamalar, cihaz platformları, cihaz durumları, IP aralıkları, istemci türlerinin) tanımlayan bir güvenlik ilkesi parçası.

### <a name="policy-rule"></a>İlke kuralı
hello İlkesi ve hello İlkesi tetiklendiğinde yapılan hello Eylemler tetikleyecek hello durumlarda tanımlayan bir güvenlik ilkesi Hello bölümü.

### <a name="prevention"></a>Önleme
Bir eylem tooprevent zarar toohello organizasyonu kötüye aracılığıyla bir kimlik veya aygıt şüpheli veya tehlikeye toobe biliyor. Önleme eylem hello aygıt ya da kimliği güvenli değildir ve önceki risk olaylarını çözümlenmiyor.

### <a name="privileged-user"></a>Ayrıcalıklı (kullanıcı)
Olan bir risk olayının hello zamanında kalıcı veya geçici yönetim izinleri tooone ya da daha fazla kaynak genel bir yönetici gibi Azure Active Directory'de bir kullanıcı Faturalama Yöneticisi, Hizmet Yöneticisi, Kullanıcı Yöneticisi ve parola Yönetici. 

### <a name="real-time"></a>Gerçek zamanlı
Gerçek zamanlı algılama bakın.

### <a name="real-time-detection"></a>Gerçek zamanlı algılama
Merhaba algılama anormallikleri ve hello olay tooproceed izin verilmeden önce oturum açma girişimi gibi bir olay hello risk değerlendirmesi.

### <a name="remediated-risk-event"></a>Çözümlendi (risk olay)
Risk olay durumu Bu risk olay türü için hello standart düzeltme eylemini kullanarak bu hello risk olayı düzeltilme belirten kimlik koruması tarafından otomatik olarak ayarlanmış. Örneğin, Hello kullanıcı parolası sıfırladığınızda hello önceki parola aşılmış belirten birçok risk olayları otomatik olarak düzeltilir.

### <a name="remediation"></a>Düzeltme
Bir eylem toosecure güvenliği aşılmış bir kimlik veya önceden şüpheli veya toobe bilinen bir cihaz. Bir düzeltme eylemi hello kimlik veya aygıt tooa güvenli bir duruma geri yükler ve hello kimlik veya aygıtla ilişkili önceki risk olaylarını çözümler.

### <a name="resolved-risk-event"></a>Çözümlendi (risk olay)
El ile Merhaba kullanıcı bir kimlik koruması dışında uygun düzeltme eylemin ve o hello risk olayı olarak gösteren bir kimlik koruması kullanıcı tarafından ayarlanan bir risk olay durumu kapalı.

### <a name="risk-event-status"></a>Risk olay durumu
Bir özelliği bir risk olayının hello olay etkin olup olmadığını ve gösteren kapalı, kapatma hello neden.

### <a name="risk-event-type"></a>Risk olay türü
Hello için bir kategori riskli olarak kabul hello olay toobe neden anomali hello türünü gösteren olay riski oluşur.

### <a name="risk-level-risk-event"></a>Risk düzeyi (risk olay)
Merhaba risk olayı toohelp kimlik koruması kullanıcılar hello önemini belirtisi (yüksek, Orta veya düşük) tooreduce hello risk tootheir kuruluş işlemleri hello eylemleri öncelik verin. 

### <a name="risk-level-sign-in"></a>Risk düzeyi (oturum açma)
Bir özel oturum açma için başka birinin toouse hello kullanıcının kimliğini çalıştığının belirtisi (yüksek, Orta veya düşük) hello olasılığı.

### <a name="risk-level-user-compromise"></a>Risk düzeyi (kullanıcı güvenliğinin aşılması)
Bir göstergesi (yüksek, Orta veya düşük) hello olasılığını Kimlikteki aşılmış.

### <a name="risk-level-vulnerability"></a>Risk düzeyi (güvenlik açığı)
Merhaba güvenlik açığı toohelp kimlik koruması kullanıcılar hello önemini belirtisi (yüksek, Orta veya düşük) tooreduce hello risk tootheir kuruluş işlemleri hello eylemleri öncelik verin.

### <a name="secure-identity"></a>(Kimlik) güvenli
Parola değiştirme veya toorestore riskli kimlik güvenliği aşılmamış tooan durumu yeniden görüntüsünü oluşturuyor makine gibi düzeltme eylemi gerçekleştirin.

### <a name="security-policy"></a>Güvenlik ilkesi
İlke kuralları ve koşul koleksiyonu. İlke, kullanıcılar, gruplar, uygulamalar, cihazları, cihaz platformları, cihaz durumları, IP aralıkları ve Auth2.0 istemci türleri gibi uygulanan tooentities olabilir. Bir ilke etkinleştirildiğinde, bir kaynak için bir belirteç hello İlkesi'nde bulunan bir varlık verilen her değerlendirilir.

### <a name="sign-in-v"></a>(V'de) oturum açın
Azure Active Directory'de tooauthenticate tooan kimliği.

### <a name="sign-in-n"></a>Oturum açma (n)
işlem veya Azure Active Directory'de bir kimlik doğrulama eylemi hello ve bu işlem yakalar olay hello.

### <a name="sign-in-from-anonymous-ip-address"></a>Anonim IP adresinden oturum açın
Bir başarılı oturum açma anonim Ara sunucu IP adresi olarak tanımlanan IP adresinden sonra bir risk olayı tetiklenir.

### <a name="sign-in-from-infected-device"></a>Etkilenen aygıttan oturum aç
Bir oturum açma etkin bir şekilde bir bot sunucusu ile toocommunicate çalıştığınız bir veya daha fazla güvenliği aşılmış cihazlara tarafından kullanılan toobe bilinen bir IP adresi kaynaklanan harekete bir risk olayı.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Oturum IP adresinden kuşkulu etkinliği ile açma
Birden çok kullanıcı hesapları arasında kısa bir süre boyunca çok sayıda başarısız oturum açma denemesi bir başarılı oturum açma gelen bir IP adresi sonra risk olay tetiklenir.

### <a name="sign-in-from-unfamiliar-location"></a>Tanınmayan bir konumdan oturum aç
Kullanıcı başarıyla yeni bir konumdan (IP, enlem/boylam ve ASN) oturum açtığında tetiklenen bir risk olayı.

### <a name="sign-in-risk"></a>Oturum açma riski
Risk bkz düzeyi (oturum açma)

### <a name="sign-in-risk-policy"></a>Oturum açma riski İlkesi
Merhaba risk tooa belirli oturum açma değerlendirir ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı geçerlidir koşullu erişim ilkesi.

### <a name="user-compromise-risk"></a>Kullanıcı güvenlik aşılması riski
Risk bakın (kullanıcı güvenliğinin aşılması) düzeyi

### <a name="user-risk"></a>Kullanıcı riski
Risk bakın (kullanıcı güvenliğinin aşılması) düzeyi.

### <a name="user-risk-policy"></a>Kullanıcı risk İlkesi
Merhaba oturum açma göz önünde bulundurur ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı geçerlidir koşullu erişim ilkesi.

### <a name="users-flagged-for-risk"></a>Riskli oldukları belirlenen kullanıcılar
Etkin ya da düzeltilen risk olaylarına sahip kullanıcılar

### <a name="vulnerability"></a>Güvenlik Açığı
Bir yapılandırma veya Azure Active Directory'de hello dizin uygulanmadıkça tooexploits veya tehditler olmasını sağlayan koşulu.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory kimlik koruması](active-directory-identityprotection.md)

