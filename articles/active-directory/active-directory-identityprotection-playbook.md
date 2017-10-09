---
title: "aaaAzure Active Directory kimlik koruması Kılavuzu | Microsoft Docs"
description: "Nasıl Azure AD Identity Protection toolimit hello yeteneğini bir saldırganın tooexploit güvenliği aşılmış kimlik veya cihaz ve bir kimlik veya şüpheli veya bilinen toobe öncekinden bir aygıtı tehlikeye toosecure sağlar öğrenin."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Azure Active Directory kimlik koruması Kılavuzu
Bu playbook size yardımcı olur:

* Merhaba kimlik koruması ortamında verileri benzetirme risk olaylarına ve güvenlik açıkları ile doldurma
* Risk bağlı olarak koşullu erişim ilkeleri Ayarla ve bu ilkeler hello etkisini test etme

## <a name="simulating-risk-events"></a>Risk olaylarını benzetimini yapma
Bu bölümde risk olayı türleri aşağıdaki hello benzetimi için adımlara sağlar:

* Oturum açma işlemleri anonim IP adreslerinden (kolay)
* Oturum açma işlemleri tanınmayan konumlardan (Orta)
* Mümkün olmayan seyahat tooatypical konumları (zor)

Diğer risk olaylarını güvenli bir şekilde benzetimi yapılamaz.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Anonim IP adreslerinden oturum açma işlemleri
Bu riski olay türü açan başarıyla anonim Ara sunucu IP adresi olarak tanımlanan bir IP adresinden kullanıcıları tanımlar. Bu proxy'leri olan kendi aygıtın IP adresi toohide istediğiniz kişiler tarafından kullanılan ve kötü amaçlı için kullanılabilir.

**bir oturum açma toosimulate anonim bir IP adresinden gerçekleştirme adımları izleyerek hello**:

1. Merhaba karşıdan [Tor tarayıcı](https://www.torproject.org/projects/torbrowser.html.en).
2. Merhaba Tor tarayıcı kullanarak gidin çok[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Merhaba hello tooappear istediğiniz hello hesabının kimlik bilgilerini girin **anonim IP adreslerinden gerçekleştirilen oturum açma işlemleri** rapor.

Merhaba oturum açma hello kimlik koruması Panoda 5 dakika içinde görünecektir. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Alışılmadık konumlardan oturum açma işlemleri
Merhaba tanınmayan konumlardan oturum açma konumları göz önünde bulundurur bir oturum açma gerçek zamanlı değerlendirme mekanizması riskidir (IP, enlem / boylam ve ASN) toodetermine yeni / tanınmayan konumları. Merhaba sistem depolar önceki IP'leri, enlem / boylam ve bir kullanıcının Asn'ler bu toobe tanıdık konumları olarak değerlendirir. Merhaba oturum açma konumu hello varolan tanıdık konumlardan herhangi birinde eşleşmiyorsa bir oturum açma konumu tanınmayan olarak kabul edilir.

Azure Active Directory kimlik koruması:  

* 14 gün boyunca, tüm yeni konumlar tanınmayan konumları olarak işaretlemez bir ilk öğrenme süre sahiptir.
* oturum açma işlemleri hakkında bilgi sahibi aygıtları ve coğrafi olarak Kapat tooan varolan tanıdık konumunun konumları yok sayar.

toosimulate tanınmayan konumlardan toosign bir konum ve hello hesap öğesinden önce oturum açtığı değil cihaz sizde. 

**bir oturum açma tanınmayan bir konumdan toosimulate gerçekleştirme adımları izleyerek hello**:

1. Oturum açma en az bir 14 gün geçmiş olan bir hesap seçin. 
2. Ya da yapın:
   
   a. Bir VPN kullanırken, çok gidin[https://myapps.microsoft.com](https://myapps.microsoft.com) ve hello toosimulate hello risk olayı için istediğiniz hello hesabının kimlik bilgilerini girin.
   
   b. Bir ilişkilendirme (önerilmez) hello hesabın kimlik bilgilerini kullanarak farklı bir konuma toosign içinde isteyin.

Merhaba oturum açma hello kimlik koruması Panoda 5 dakika içinde görünecektir.

### <a name="impossible-travel-tooatypical-location"></a>Mümkün olmayan seyahat tooatypical konumu
Merhaba algoritması machine learning tooweed yanlış pozitifler tanıdık aygıtlardan mümkün olmayan seyahat veya oturum açmalardan hello dizininde diğer kullanıcılar tarafından kullanılan VPN'ler gibi çıkışı kullandığından hello mümkün olmayan seyahat koşul benzetimi zor olabilir. Ayrıca, risk olaylarını oluşturma işlemi başlamadan önce hello algoritması hello kullanıcı için bir oturum açma geçmişine 3 too14 gün gerektirir.

**toosimulate bir mümkün olmayan seyahat tooatypical konum gerçekleştirme adımları izleyerek hello**:

1. Standart, tarayıcı kullanarak gidin çok[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Merhaba bir mümkün olmayan seyahat risk olayı toogenerate istediğiniz hello hesabının kimlik bilgilerini girin.
3. Kullanıcı Aracısı değiştirin. Geliştirici Araçları'ndan kullanıcı aracısı Internet Explorer'da değiştirmek veya kullanıcı aracınız Firefox veya kullanıcı aracısı değiştirici Eklentisi'ni kullanarak Chrome değiştirin.
4. IP adresini değiştirin. VPN, Tor eklentisi kullanılarak veya farklı bir veri merkezinde Azure içinde yeni bir makine dönmesini IP adresiniz değiştirebilirsiniz.
5. Oturum çok açma[https://myapps.microsoft.com](https://myapps.microsoft.com) hello olarak önce ve sonra hello önceki oturum açma birkaç dakika içinde aynı kimlik bilgilerini kullanarak.

Merhaba oturum açma hello Identity Protection panosunda 2-4 saat içinde görünecektir.<br>
Söz konusu modelleri hello karmaşık machine learning nedeniyle, bu toplanma değil şansı yoktur.<br> Birden çok Azure AD hesapları için bu adımları tooreplicate isteyebilirsiniz.

## <a name="simulating-vulnerabilities"></a>Güvenlik açıkları benzetimini yapma
Güvenlik açıkları tarafından hatalı aktör yararlanan bir Azure AD ortamda zayıf giderilmiştir. Şu anda açık 3 türlerinin diğer özelliklerden Azure ad içinde Azure AD Identity Protection çıkmış. Bu özellikler ayarlandıktan sonra bu güvenlik açıklarından otomatik olarak hello Identity Protection panosunda görüntülenir.

* Azure AD [çok faktörlü kimlik doğrulaması?](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>Kullanıcı güvenlik aşılması riski
**tootest kullanıcı güvenliğinin aşılmasına risk, aşağıdaki adımları hello gerçekleştirmek**:

1. Oturum çok açma[https://portal.azure.com](https://portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.
2. Çok gidin**kimlik koruması**. 
3. Merhaba ana üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**. 
4. Merhaba üzerinde **Portalı Ayarları** dikey altında **güvenlik kuralları**, tıklatın **kullanıcı güvenliğinin aşılmasına riski**. 
5. Merhaba üzerinde **Risk oturum** dikey penceresinde kapatma **etkinleştir kural** kapalı ve ardından **kaydetmek** ayarları.
6. Belirtilen kullanıcı hesabı için bir tanınmayan benzetimini konumlar veya anonim IP risk olayı. Bu çok yükseltmesine hello kullanıcı risk düzeyi bu kullanıcı için**orta**.
7. Birkaç dakika bekleyin ve kullanıcı için bu kullanıcı düzeyini doğrulayın **orta**.
8. Toohello Git **Portalı Ayarları** dikey.
9. Merhaba üzerinde **kullanıcı güvenliğinin aşılmasına Risk** dikey altında **etkinleştir kural**seçin **üzerinde** . 
10. Seçenekler aşağıdaki hello birini seçin:
    
    a. tooblock, select **orta** altında **blok oturum**.
    
    b. tooenforce güvenli parola değişikliği, select **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.
11. **Kaydet** düğmesine tıklayın.
12. Bir kullanıcı bir yükseltilmiş risk düzeyi ile kullanarak oturum açma tarafından risk bağlı olarak koşullu erişim artık test edebilirsiniz. Merhaba kullanıcı risk Orta ise, ilkenizin hello yapılandırmasına bağlı olarak, oturum açma işleminiz olabilir ya da engellenen ya da toochange zorlanır parolanızı. 
    <br><br>
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    <br>

## <a name="sign-in-risk"></a>Oturum açma riski
**tootest bir oturum açma riski hello aşağıdaki adımları gerçekleştirin:**

1. Oturum çok açma[https://portal.azure.com ](https://portal.azure.com) kiracınız için genel yönetici kimlik bilgilerine sahip.
2. Çok gidin**kimlik koruması**.
3. Merhaba ana üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**. 
4. Merhaba üzerinde **Portalı Ayarları** dikey altında **güvenlik kuralları**, tıklatın **risk oturum**.
5. Merhaba üzerinde ** Risk oturum ** dikey penceresinde, select **üzerinde** altında **etkinleştir kural**. 
6. Seçenekler aşağıdaki hello birini seçin:
   
   a. tooblock, select **orta** altında **blok oturum açın**
   
   b. tooenforce güvenli parola değişikliği, select **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.
7. Blok altında select Orta tooblock, oturum açın.
8. tooenforce çok faktörlü kimlik doğrulaması, select **orta** altında **çok faktörlü kimlik doğrulaması gerektiren**.
9. **Kaydet**'e tıklayın.
10. Merhaba tanınmayan konumlardan taklit ederek risk bağlı olarak koşullu erişim artık sınayabilirsiniz veya her ikisi de olduklarından anonim IP risk olayları **orta** risk olayları.


![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")


## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory kimlik koruması](active-directory-identityprotection.md)

