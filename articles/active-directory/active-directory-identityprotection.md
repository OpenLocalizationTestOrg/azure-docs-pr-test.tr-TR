---
title: "Active Directory kimlik koruması aaaAzure | Microsoft Docs"
description: "Nasıl Azure AD Identity Protection toolimit hello yeteneğini bir saldırganın tooexploit güvenliği aşılmış kimlik veya cihaz ve bir kimlik veya şüpheli veya bilinen toobe öncekinden bir aygıtı tehlikeye toosecure sağlar öğrenin."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Kimlik Koruması

Azure Active Directory kimlik koruması sağlar hello Azure AD Premium P2 edition özelliğidir:

- Kuruluşunuzdaki kimlikleri etkileyen olası güvenlik açıklarını algılama

- İlgili tooyour kuruluşunuzun kimlikleri otomatik yanıtlar toodetected şüpheli Eylemler yapılandırın  

- Şüpheli olayları araştırmanıza ve uygun eylemi tooresolve ele bunları   


## <a name="getting-started"></a>Başlarken

Microsoft bulut tabanlı kimlikleri birden fazla bir süredir güvenliğini sağlar. Azure Active Directory kimlik koruması ile ortamınızda hello kullanabilirsiniz aynı koruma sistemleri Microsoft toosecure kimlikleri kullanır.

güvenlik ihlallerini ele Hello çoğunluğu saldırganların bir kullanıcının kimliğini çalarak erişim tooan ortamı elde zaman yerleştirin. Merhaba yıllar içinde saldırganlar üçüncü taraf ihlallerini yararlanan ve Gelişmiş kimlik avı saldırıları kullanarak giderek etkin hale getirildi. Bir saldırgan tooeven düşük ayrıcalıklı kullanıcı hesaplarına erişim kazanır hemen bunları toogain tooimportant şirket kaynaklarına yanal hareket aracılığıyla için görece olarak daha kolay.

Bu gruplarındaki sonucu olarak, şunları yapmanız gerekir:

- Ayrıcalık düzeylerini bağımsız olarak tüm kimlikleri koru

- Proaktif olarak kötüye gelen güvenliği aşılmış kimlik engelle

Güvenliği aşılmış kimlikleri keşfetme hiçbir kolay bir görevdir. Buluşsal yöntemler toodetect anormallikleri ve potansiyel olarak belirtmek şüpheli olayları kimlikleri riske ve Azure Active Directory Uyarlamalı machine learning algoritmaları kullanır. Bu verileri kullanarak, kimlik koruması raporları oluşturur ve, tooevaluate hello etkinleştirmek uyarılar ilgili sorunlar algıladı ve uygun azaltma veya düzeltme eylemlerini gerçekleştirin.

Azure Active Directory kimlik koruması izleme ve Raporlama Aracı büyük. tooprotect kuruluşunuzdaki kimlikleri, belirtilen risk düzeyi erişildiğinde toodetected sorunları otomatik olarak yanıt veren risk tabanlı ilkeleri yapılandırabilirsiniz. Bu ilkeler ayrıca tooother koşullu erişim kontrolü Azure Active Directory ve EMS tarafından sağlanan, otomatik olarak engellemek ya da parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama gibi uyarlamalı düzeltme eylemleri başlatmak.


#### <a name="identity-protection-capabilities"></a>Kimlik koruma özellikleri

**Algılama Güvenlik Açıkları ve riskli hesapları:**  

* Özel öneriler tooimprove sağlayan güvenlik açıkları vurgulama tarafından genel güvenlik duruşunu
* Oturum açma risk düzeyleri hesaplama
* Kullanıcı risk düzeyleri hesaplama


**Risk olaylarını araştırma:**

* Risk olayları için bildirimleri gönderme
* Risk olaylarını ilgili ve bağlamsal bilgileri kullanarak araştırma
* Tootrack araştırmalar temel iş akışı sağlama
* Parola sıfırlama gibi tooremediation eylemleri kolay erişim sağlama

**Risk bağlı olarak koşullu erişim ilkeleri:**

* İlke toomitigate riskli gerçekleştirilen oturum açma tarafından gerçekleştirilen oturum açma engelleme veya çok faktörlü kimlik doğrulaması zorluklarını gerektirerek.
* İlke tooblock veya güvenli riskli kullanıcı hesapları
* Çok faktörlü kimlik doğrulama İlkesi toorequire kullanıcılar tooregister



## <a name="identity-protection-roles"></a>Kimlik koruması rolleri

tooload Bakiye hello yönetim etkinliklerini kimlik koruması uygulamanız geçici çeşitli roller atayabilirsiniz. Azure AD Identity Protection 3 dizin rollerini destekler:

| Rol                         | Yapabilirsiniz                          | Yapamaz
| :--                          | ---                                |  ---   |
| Genel yönetici         | Tam erişim tooIdentity koruma, yerleşik kimlik koruması| |
| Güvenlik yöneticisi       | Tam erişim tooIdentity koruma | Yerleşik kimlik koruması, bir kullanıcı parolalarını sıfırlama |
| Güvenlik okuyucusu              | Yalnızca hazır erişim tooIdentity koruma | Yerleşik kimlik koruması, remidiate kullanıcılar, ilkelerini yapılandırmak, parolaları sıfırlama |




Daha fazla ayrıntı için bkz: [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Algılama

### <a name="vulnerabilities"></a>Güvenlik Açıkları

Azure Active Directory kimlik koruması yapılandırmanızı analizleri yaparken ve kullanıcı kimlikleri üzerinde bir etkisi olabilir güvenlik açıkları algılar. Daha fazla ayrıntı için bkz: [Azure Active Directory kimlik koruması tarafından algılanan Güvenlik Açığı](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Risk olayı

Azure Active Directory Uyarlamalı machine learning, ilgili tooyour kullanıcının kimlikleri algoritmaları ve buluşsal yöntemler toodetect şüpheli eylemleri kullanır. Merhaba sistem algılanan her şüpheli eylemi için bir kayıt oluşturur. Bu kayıtları olarak da bilinen risk olaylardır.  
Daha ayrıntılı bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Araştırma
Yolculuğunuzun kimlik koruması aracılığıyla genellikle hello kimlik koruması panosu ile başlar.

![Düzeltme](./media/active-directory-identityprotection/1000.png "düzeltme")

Merhaba Pano erişmenizi sağlar:

* Gibi raporları **bayrak eklenen kullanıcılar için risk**, **Risk olayları** ve **güvenlik açıkları**
* Merhaba yapılandırması gibi ayarları, **güvenlik ilkeleri**, **bildirimleri** ve **çok faktörlü kimlik doğrulaması kayıt**

Genellikle hello etkinlikleri, günlükler ve diğer ilgili bilgileri ilgili tooa risk olayı toodecide düzeltme veya azaltma adımları gerekli olup olmadığını gözden geçirme hello işlemidir, araştırma ve nasıl hello kimlik olduğu için başlangıç noktası. gizliliği ve nasıl hello kimlik tehlikeye anlamak kullanıldı.

Araştırma etkinlikleri toohello bağlayabilirsiniz [bildirimleri](active-directory-identityprotection-notifications.md) Azure Active Directory koruma e-posta gönderir.

Merhaba aşağıdaki bölümler, daha fazla ayrıntı ve ilgili tooan araştırma hello adımları sağlar.  


## <a name="risky-sign-ins"></a>Riskli oturum açma işlemleri

Azure Active Directory algılar [risk olayı türleri](active-directory-reporting-risk-events.md#risk-event-types) gerçek zamanlı ve çevrimdışı. Bir oturum açma için kullanıcı algılanan her risk olayı tooa mantıksal kavram riskli oturum açma adı verilen katkıda bulunur. Bir riskli oturum açma bir hello yasal sahibi bir kullanıcı hesabı tarafından gerçekleştirilmiş olabilecek olmayan bir oturum açma girişimi için göstergesidir.


### <a name="sign-in-risk-level"></a>Oturum açma risk düzeyi

Oturum açma risk düzeyi bir oturum açma girişimi hello yasal sahibi bir kullanıcı hesabı tarafından gerçekleştirilmedi bir (yüksek, Orta veya düşük) hello olasılığını göstergesidir.

### <a name="mitigating-sign-in-risk-events"></a>Oturum açma riski olaylar azaltılması

Bir azaltma bir eylem toolimit hello bir saldırganın tooexploit güvenliği aşılmış kimlik veya hello kimliği veya cihaza tooa güvenli geri yükleme durumunda olmadan cihaz özelliğidir. Bir azaltma hello kimlik veya aygıtla ilişkili önceki oturum açma risk olaylarını çözümlenmiyor.

toomitigate riskli gerçekleştirilen oturum açma, oturum açma riski güvenlik policicies otomatik olarak yapılandırabilirsiniz. Hello kullanıcı veya oturum açma hello tooblock hello risk düzeyi riskli oturum açma işlemleri göz önünde bulundurun bu ilkeleri kullanarak veya hello kullanıcı tooperform çok faktörlü kimlik doğrulaması gerektirir. Bu Eylemler, bir saldırganın çalınan kimlik toocause zarar yararlanmasını engelleyebilir ve bazı zaman toosecure hello kimlik verebilir.

### <a name="sign-in-risk-security-policy"></a>Oturum açma riski güvenlik ilkesi
Oturum açma riski hello risk tooa belirli oturum açma değerlendirir ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı geçerlidir bir koşullu erişim ilkesi ilkesidir.

![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1014.png "risk ilkesine oturum açma")

Azure AD kimlik koruması olanak tanıyarak hello azaltma riskli oturum açma işlemleri durumunu yönetmenize yardımcı olur:

* Kullanıcılar ve gruplar hello ilkenin uygulandığı hello ayarlayın:

    ![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1015.png "risk ilkesine oturum açma")
* Hello İlkesi tetikleyen hello oturum açma risk düzeyi eşiği (düşük, Orta veya yüksek) ayarlayın:

    ![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1016.png "risk ilkesine oturum açma")
* Set hello denetimleri toobe Hello İlkesi tetikler zorunlu tutulur:  

    ![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1017.png "risk ilkesine oturum açma")
* Anahtar hello durumunu ilkenizin:

    ![MFA kayıt](./media/active-directory-identityprotection/403.png "MFA kayıt")
* Gözden geçirin ve onu etkinleştirmek önce bir değişiklik hello etkisini değerlendirin:

    ![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1018.png "risk ilkesine oturum açma")

#### <a name="what-you-need-tooknow"></a>Gerekenler tooknow
Bir oturum açma riski güvenlik ilkesi toorequire multi-Factor authentication yapılandırabilirsiniz:

![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1017.png "risk ilkesine oturum açma")

Ancak, güvenlik nedeniyle, bu ayar yalnızca çok faktörlü kimlik doğrulaması için önceden kaydedilmiş olan kullanıcılar için çalışır. Merhaba koşulu toorequire çok faktörlü kimlik doğrulama için multi-Factor authentication henüz kaydedilmemiş bir kullanıcı için sağlanıyorsa hello kullanıcı engellendi.

Riskli oturum açma işlemleri için toorequire çok faktörlü kimlik doğrulamasını istiyorsanız, en iyi uygulama, aşağıdakileri yapmalısınız:

1. Merhaba etkinleştirmek [çok faktörlü kimlik doğrulaması kayıt ilkesi](#multi-factor-authentication-registration-policy) Merhaba etkilenen kullanıcılar.
2. Merhaba riskli olmayan oturum tooperform, kullanıcıların toologin MFA kayıt etkilenen gerektirir

Bu adımları tamamladıktan, çok faktörlü kimlik doğrulamasının bir riskli oturum açma için gerekli sağlar.

#### <a name="best-practices"></a>En iyi uygulamalar
Seçerek bir **yüksek** eşik bir ilke tetiklenir ve hello etkisi toousers en aza indirir hello sayısını azaltır.  

Ancak, dışlar **düşük** ve **orta** gerçekleştirilen oturum açma bayrağı güvenliği aşılmış kimlik bilgisinden faydalanmakta saldırganın engelleyebilir değil hello ilkesinden risk için.

Ne zaman ayarı hello İlkesi

* Sağlamadığı / çok faktörlü kimlik doğrulamasına sahip olmadığınız kullanıcılar Dışla
* Hello İlkesi etkinleştirme olduğu pratik yerel kullanıcılar hariç tutmak (örneğin hiçbir erişim toohelpdesk)
* Büyük olasılıkla toogenerate çok fazla yanlış pozitifler (geliştiriciler, güvenlik analistleri) olan kullanıcıların Dışla
* Kullanım bir **yüksek** eşiği ilk ilke dağıtımı, sırasında veya son kullanıcılar tarafından görülen sorunları en aza gerekir.
* Kullanım bir **düşük** kuruluşunuz daha yüksek güvenlik gerektiriyorsa eşiği. Seçerek bir **düşük** eşik ek kullanıcı oturum açma zorluklar, ancak daha yüksek düzeyde güvenlik sunar.

Çoğu kuruluş için tooconfigure bir kural için önerilen varsayılan hello bir **orta** eşik toostrike kullanılabilirlik ile güvenlik arasında bir denge.

Merhaba oturum açma risk ilkesine şöyledir:

* Uygulanan tooall tarayıcı trafiğini ve modern kimlik doğrulaması kullanarak oturum açma işlemleri.
* Devre dışı bırakarak eski güvenlik protokollerini kullanarak uygulanmamış tooapplications WS-Trust uç noktada ADFS gibi Federasyon hello IDP hello.

Merhaba **Risk olaylarını** hello kimlik koruması konsolundaki sayfasında tüm olayları listeler:

* Bu ilkenin uygulandığı
* Merhaba etkinliği gözden geçirin ve hello eylem uygun olup olmadığını belirleme

Merhaba genel bakış için kullanıcı deneyimi, ilgili bakın:

* [Oturum açma riskli kurtarma](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Riskli oturum engellenen açma](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Oturum açma deneyimlerini Azure AD kimlik koruması](active-directory-identityprotection-flows.md)  

**tooopen hello ilgili yapılandırma iletişim**:

- Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde hello **yapılandırma** 'yi tıklatın **oturum açma risk ilkesine**.

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1014.png "kullanıcı ridk İlkesi")



## <a name="users-flagged-for-risk"></a>Riskli oldukları belirlenen kullanıcılar

Tüm etkin [risk olayları](active-directory-identity-protection-risk-events.md) , algılandı Azure Active Directory tarafından bir kullanıcıya katkıda bulunan için tooa mantıksal kavram kullanıcı risk çağrılır. Risk bayrak eklenen kullanıcı geçirildiğini bir kullanıcı hesabı için bir göstergesidir.

![Riskli oldukları belirlenen kullanıcılar](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Kullanıcı risk düzeyi

Bir kullanıcı risk düzeyi hello kullanıcının kimliğini aşılmış bir (yüksek, Orta veya düşük) hello olasılığını göstergesidir. Bir kullanıcı kimliğiyle ilişkili hello kullanıcı risk olaylarına göre hesaplanır.

Merhaba bir risk olayı ya da durumudur **etkin** veya **kapalı**. Yalnızca olayları risk **etkin** toohello kullanıcı risk düzeyi hesaplama katkıda bulunun.

Merhaba kullanıcı risk düzeyi girişleri aşağıdaki hello kullanılarak hesaplanır:

* Merhaba kullanıcı etkileyen etkin risk olayları
* Bu olayların risk düzeyi
* Gerçekleştirilen tüm düzeltme eylemlerini olup önlemlerin

![Kullanıcı riskleri](./media/active-directory-identityprotection/1031.png "kullanıcı riskleri")

Oturum açma riskli kullanıcıların engellemek hello kullanıcı risk düzeyleri toocreate koşullu erişim ilkeleri kullanın veya bunları zorla toosecurely parolasını değiştirin.

### <a name="closing-risk-events-manually"></a>Risk olaylarını el ile kapatma

Çoğu durumda, tooautomatically Kapat risk olaylarını güvenli bir parola sıfırlama gibi düzeltme eylemleri gerçekleştirecek. Ancak, bu her zaman mümkün olmayabilir.  
Bu, örneğin, hello bir durumdur, ne zaman:

* Etkin risk olaylarına sahip bir kullanıcı silindi
* Bildirilen risk olayı sahip olan gerçekleştireceğini hello yasal kullanıcı tarafından bir araştırma ortaya çıkarır

Risk olaylarını olduğundan **etkin** toohello kullanıcı risk hesaplama katkıda, risk olaylarını el ile kapatarak risk düzeyi alt toomanually olabilir.  
Araştırma Hello sürecinde tootake herhangi bir risk olayı bu eylemler toochange hello durumunu birini seçebilirsiniz:

![Eylemler](./media/active-directory-identityprotection/34.png "Eylemler")

* **Gidermek** - bir risk olayı araştırdıktan sonra uygun düzeltme eylemi kimlik koruması dışında sürdü ve kapalı, işareti hello olayı çözümlenmiş olarak hello risk olay sayılacağı düşünüyorsanız. Çözümlenmiş olaylar hello risk olayın durumu tooClosed ayarlanır ve hello risk olay artık toouser risk katkıda bulunur.
* **Hatalı pozitif olarak işaretlemek** -bazı durumlarda, bir risk olayı araştırmak ve olabilirsiniz, yanlış bir riskli işaretlenen olduğunu bulmak. Merhaba risk olayı hatalı pozitif olarak işaretleyerek hello böyle sayısı azaltmaya yardımcı olabilir. Bu hello machine learning algoritmaları tooimprove hello sınıflandırma hello gelecekteki benzer olayların yardımcı olur. Merhaba hatalı pozitif olayların durumudur çok**kapalı** ve toouser risk artık katkıda bulunur.
* **Yoksay** - herhangi bir düzeltme eylemi olmadı ancak hello etkin listesinden kaldırıldı risk olayı toobe Merhaba, risk olayı yoksay işaretleyebilirsiniz ve hello olay durumu kapatılacak istiyorsanız. Yoksayılan olayları toouser risk katkıda bulunmamaktadır. Bu seçenek yalnızca olağan dışı durumlarda kullanılmalıdır.
* **Yeniden etkinleştirme** -Risk el ile kapatılan olaylar (seçerek **gidermek**, **yanlış pozitif**, veya **Yoksay**) hello ayarı etkinleştirilebilir Olay durumunu geri çok**etkin**. Yeniden etkinleştirilen risk olaylarını toohello kullanıcı risk düzeyi hesaplama katkıda. Risk olaylarına (güvenli bir parola sıfırlama gibi) düzeltme aracılığıyla kapalı etkinleştirilemez.

**tooopen hello ilgili yapılandırma iletişim**:

1. Merhaba üzerinde **Azure AD Identity Protection** dikey altında **Araştır**, tıklatın **Risk olayları**.

    ![El ile parola sıfırlama](./media/active-directory-identityprotection/1002.png "el ile parola sıfırlama")
2. Merhaba, **Risk olayları** listesinde, bir risk tıklayın.

    ![El ile parola sıfırlama](./media/active-directory-identityprotection/1003.png "el ile parola sıfırlama")
3. Merhaba risk dikey penceresinde, bir kullanıcı sağ tıklayın.

    ![El ile parola sıfırlama](./media/active-directory-identityprotection/1004.png "el ile parola sıfırlama")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Bir kullanıcı için tüm risk olaylarını el ile kapatma
El ile bir kullanıcı için risk olayları ayrı ayrı kapatmak yerine, Azure Active Directory kimlik koruması Ayrıca, bir yöntem tooclose ile tüm olayları tek bir tıklatmayla bir kullanıcı için sağlar.

![Eylemler](./media/active-directory-identityprotection/2222.png "Eylemler")

Tıkladığınızda **tüm olayları kapatmak**, tüm olayları kapatılır ve etkilenen hello kullanıcının, artık risk altında.

### <a name="remediating-user-risk-events"></a>Düzelterek kullanıcı risk olayı

Bir düzeltme bir kimlik veya önceden şüpheli veya toobe bilinen bir cihaz tehlikeye bir eylem toosecure ' dir. Bir düzeltme eylemi hello kimlik veya aygıt tooa güvenli bir duruma geri yükler ve hello kimlik veya aygıtla ilişkili önceki risk olaylarını çözümler.

tooremediate kullanıcı risk olaylarına, şunları yapabilirsiniz:

* Güvenli parola sıfırlama tooremediate kullanıcı risk olaylarına el ile gerçekleştirin
* Kullanıcı risk olayları otomatik olarak düzeltmek veya bir kullanıcı risk güvenlik ilkesi toomitigate yapılandırma
* Etkilenen hello aygıt yeniden görüntü  

#### <a name="manual-secure-password-reset"></a>El ile güvenli parola sıfırlama
Güvenli parola sıfırlama birçok risk olayı için geçerli bir düzeltme ve gerçekleştirildiğinde, otomatik olarak bu risk olaylarını kapatır ve hello kullanıcı risk düzeyi yeniden hesaplar. Merhaba kimlik koruması Pano tooinitiate parola sıfırlama riskli bir kullanıcı için kullanabilirsiniz.

Merhaba ilgili iletişim iki farklı yöntemler tooreset bir parola sağlar:

**Parola sıfırlama** - seçin **parolalarını hello kullanıcı tooreset gerektiren** hello kullanıcı çok faktörlü kimlik doğrulaması için kaydedildiyse tooallow hello kullanıcı tooself-Kurtar. Merhaba kullanıcının sonraki oturum açma sırasında hello kullanıcı çok faktörlü kimlik doğrulaması sınama başarıyla gerekli toosolve ve ardından, zorunlu toochange hello parola olacaktır. Merhaba kullanıcı hesabı kayıtlı çok faktörlü kimlik doğrulama değilse, bu seçenek kullanılamaz.

**Geçici parolayı** - seçin **geçici bir parola oluşturmak** tooimmediately hello mevcut parolayı geçersiz kılmak ve hello kullanıcı için yeni bir geçici parola oluşturun. Merhaba yeni geçici parola tooan alternatif e-posta adresi hello kullanıcı veya toohello kullanıcının yöneticisini gönderin. Merhaba parola geçici olduğundan hello kullanıcı oturum açma sırasında istendiğinde toochange hello parola olacaktır.

![İlke](./media/active-directory-identityprotection/1005.png "İlkesi")

**tooopen hello ilgili yapılandırma iletişim**:

1. Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **bayrak eklenen kullanıcılar için risk**.

    ![El ile parola sıfırlama](./media/active-directory-identityprotection/1006.png "el ile parola sıfırlama")
2. Kullanıcıların Hello listeden en az bir risk olaylarına sahip bir kullanıcı seçin.

    ![El ile parola sıfırlama](./media/active-directory-identityprotection/1007.png "el ile parola sıfırlama")
3. Merhaba kullanıcı dikey penceresinde **parola sıfırlama**.

    ![El ile parola sıfırlama](./media/active-directory-identityprotection/1008.png "el ile parola sıfırlama")

### <a name="user-risk-security-policy"></a>Kullanıcı risk güvenlik ilkesi
Bir kullanıcı risk güvenlik ilkesi hello risk düzeyi tooa belirli kullanıcı ve önceden tanımlanmış koşullara ve kurallarına göre düzeltme ve azaltma Eylemler uyguladığında bir koşullu erişim ilkesi var.

![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1009.png "kullanıcı ridk İlkesi")

Azure AD kimlik koruması hello azaltma ve risk olanak tanıyarak bayrak eklenen kullanıcılar düzeltmesi yönetmenize yardımcı olur:

* Kullanıcılar ve gruplar hello ilkenin uygulandığı hello ayarlayın:

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1010.png "kullanıcı ridk İlkesi")
* Hello İlkesi tetikleyen hello kullanıcı risk düzeyi eşiği (düşük, Orta veya yüksek) ayarlayın:

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1011.png "kullanıcı ridk İlkesi")
* Set hello denetimleri toobe Hello İlkesi tetikler zorunlu tutulur:

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1012.png "kullanıcı ridk İlkesi")
* Anahtar hello durumunu ilkenizin:

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/403.png "MFA kayıt")
* Gözden geçirin ve onu etkinleştirmek önce bir değişiklik hello etkisini değerlendirin:

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1013.png "kullanıcı ridk İlkesi")

Seçerek bir **yüksek** eşik bir ilke tetiklenir ve hello etkisi toousers en aza indirir hello sayısını azaltır.
Ancak, dışlar **düşük** ve **orta** kimlikleri veya cihazları, güvenli değil hello ilkesinden risk için işaretlenmiş kullanıcılar önceden şüpheli veya bilinen tehlikeye toobe.

Ne zaman ayarı hello İlkesi

* Büyük olasılıkla toogenerate çok fazla yanlış pozitifler (geliştiriciler, güvenlik analistleri) olan kullanıcıların Dışla
* Hello İlkesi etkinleştirme olduğu pratik yerel kullanıcılar hariç tutmak (örneğin hiçbir erişim toohelpdesk)
* Kullanım bir **yüksek** eşiği ilk ilke dağıtımı, sırasında veya son kullanıcılar tarafından görülen sorunları en aza gerekir.
* Kullanım bir **düşük** kuruluşunuz daha yüksek güvenlik gerektiriyorsa eşiği. Seçerek bir **düşük** eşik ek kullanıcı oturum açma zorluklar, ancak daha yüksek düzeyde güvenlik sunar.

Çoğu kuruluş için tooconfigure bir kural için önerilen varsayılan hello bir **orta** eşik toostrike kullanılabilirlik ile güvenlik arasında bir denge.

Merhaba genel bakış için kullanıcı deneyimi, ilgili bakın:

* [Hesap kurtarma akışı tehlikeye](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Hesap engellendi akış tehlikeye](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**tooopen hello ilgili yapılandırma iletişim**:

- Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde hello **yapılandırma** 'yi tıklatın **kullanıcı risk ilkesine**.

    ![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1009.png "kullanıcı ridk İlkesi")

### <a name="mitigating-user-risk-events"></a>Kullanıcı risk olaylar azaltılması
Yöneticiler kullanıcı risk güvenlik ilkesi tooblock kullanıcılar oturum açma sırasında hello risk düzeyine bağlı olarak ayarlayabilirsiniz.

Bir oturum açma engelleme:

* Etkilenen hello kullanıcı için yeni kullanıcı risk olaylarına Hello oluşturulmasını engeller
* Etkinleştirir Yöneticiler toomanually hello kullanıcının kimliğini etkileyen hello risk olaylarını düzeltmek ve tooa güvenli durumunu geri yükle



## <a name="multi-factor-authentication-registration-policy"></a>Çok faktörlü kimlik doğrulaması kayıt ilkesi
Azure çok faktörlü kimlik doğrulaması hello kullanımını daha fazlasını bir kullanıcı adı ve parolası gerektiren kim olduğunuzu doğrulama bir yöntemdir. Güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı sağlar.  
Çünkü kullanıcı oturum açma işlemleri için Azure çok faktörlü kimlik doğrulaması ihtiyaç duyduğunuz öneririz:

* Kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması sunar
* Kuruluş tooprotect hazırlanırken önemli bir rol oynar ve hesap ödün kurtarma

![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1019.png "kullanıcı ridk İlkesi")

Daha fazla ayrıntı için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD kimlik koruması sağlayan bir ilkesi yapılandırarak hello üretimini çok faktörlü kimlik doğrulaması kayıt yönetmenize yardımcı olur:

* Kullanıcılar ve gruplar hello ilkenin uygulandığı hello ayarlayın:

    ![MFA ilkesini](./media/active-directory-identityprotection/1020.png "MFA İlkesi")
* Hello İlkesi tetikler zorunlu tutulur kümesi hello denetimleri toobe::  

    ![MFA ilkesini](./media/active-directory-identityprotection/1021.png "MFA İlkesi")
* Anahtar hello durumunu ilkenizin:

    ![MFA ilkesini](./media/active-directory-identityprotection/403.png "MFA İlkesi")
* Merhaba geçerli kayıt durumunu görüntüleyin:

    ![MFA ilkesini](./media/active-directory-identityprotection/1022.png "MFA İlkesi")

Merhaba genel bakış için kullanıcı deneyimi, ilgili bakın:

* [Çok faktörlü kimlik doğrulaması kayıt akışı](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Azure AD kimlik koruması ile karşılaştığında oturum açma](active-directory-identityprotection-flows.md).  

**tooopen hello ilgili yapılandırma iletişim**:

- Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde hello **yapılandırma** 'yi tıklatın **çok faktörlü kimlik doğrulaması kayıt**.

    ![MFA ilkesini](./media/active-directory-identityprotection/1019.png "MFA İlkesi")

## <a name="next-steps"></a>Sonraki adımlar
* [Kanal 9: Azure AD ve kimlik göster: kimlik koruması Önizleme](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Azure Active Directory kimlik koruması etkinleştirme](active-directory-identityprotection-enable.md)

* [Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı](active-directory-identityprotection-vulnerabilities.md)

* [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md)

* [Azure Active Directory kimlik koruması bildirimleri](active-directory-identityprotection-notifications.md)

* [Azure Active Directory kimlik koruması Kılavuzu](active-directory-identityprotection-playbook.md)

* [Azure Active Directory kimlik koruması Kılavuzu sözlüğü](active-directory-identityprotection-glossary.md)

* [Oturum açma deneyimlerini Azure AD kimlik koruması](active-directory-identityprotection-flows.md)

* [Azure Active Directory kimlik koruması - nasıl toounblock kullanıcılar](active-directory-identityprotection-unblock-howto.md)

* [Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama](active-directory-identityprotection-graph-getting-started.md)
