---
title: "aaaAzure Active Directory risk olaylarını | Microsoft Docs"
description: "Bu konu, risk olaylarını nelerdir ayrıntılı genel bakış sağlar."
services: active-directory
keywords: "Azure active directory kimlik koruması, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Azure Active Directory risk olayları

güvenlik ihlallerini ele Hello çoğunluğu saldırganların bir kullanıcının kimliğini çalarak erişim tooan ortamı elde zaman yerleştirin. Güvenliği aşılmış kimlikleri keşfetme hiçbir kolay bir görevdir. Azure Active Directory Uyarlamalı machine learning, ilgili tooyour kullanıcı hesapları olan algoritmalar ve buluşsal yöntemler toodetect şüpheli eylemleri kullanır. Her kuşkulu eylem olarak adlandırılan bir kayıtta depolanan algılanan *risk olayı*.

Şu anda, Azure Active Directory altı tür risk olaylarını algılar:

- [Sızan kimlik bilgilerine sahip kullanıcılar](#leaked-credentials) 
- [Anonim IP adreslerinden gerçekleştirilen oturum açma işlemleri](#sign-ins-from-anonymous-ip-addresses) 
- [Mümkün olmayan seyahat tooatypical konumları](#impossible-travel-to-atypical-locations) 
- [Fazla tanınmayan konumlardan gerçekleştirilen oturum açma işlemleri](#sign-in-from-unfamiliar-locations)
- [Virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri](#sign-ins-from-infected-devices) 
- [Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Risk olayı](./media/active-directory-reporting-risk-events/91.png)

Bu konuda, hangi risk olaylarını ayrıntılı bir genel bakış olan ve nasıl tooprotect kullanabilmek için Azure AD kimliklerinizi sağlar.


## <a name="risk-event-types"></a>Risk olayı türleri

Merhaba risk olay türü hello şüpheli eylem risk olay kaydı için tanımlayıcı için oluşturulan bir özelliktir.  
Microsoft'un sürekli Yatırımlar hello algılama işlemine neden:

- Varolan risk olayı geliştirmeleri toohello algılama doğruluğunu 
- Merhaba gelecekteki eklenecek yeni risk olayı türleri

### <a name="leaked-credentials"></a>Sızan kimlik bilgileri

Normal kullanıcıların geçerli parolalarını cybercriminals tehlikeye zaman hello suçlular genellikle bu kimlik bilgilerini paylaşır. Bu genellikle, bunları herkese açık şekilde hello koyu web ya da Yapıştır sitelerde veya ticaret veya hello kimlik hello siyah piyasadaki satış göndererek da gerçekleştirilir. Merhaba Microsoft sızmasını kimlik bilgilerini hizmet edinir kullanıcı adı / parola çiftleri ortak açık ve koyu renkli web siteleri izleme ve çalışma:

- Araştırmacılar
- Yasa uygulama
- Microsoft Güvenlik ekiplerden
- Güvenilir diğer kaynaklar 

Ne zaman hello hizmet edinir kullanıcı adı / parola çiftleri, bunlar denetlenir karşı AAD kullanıcıların geçerli geçerli kimlik bilgileri. Bir eşleşme bulunduğunda, bir kullanıcının parolasını aşıldığını gelir ve bir *kimlik bilgileri riskini olay sızmasını* oluşturulur.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Anonim IP adreslerinden oturum açma işlemleri

Bu riski olay türü açan başarıyla anonim Ara sunucu IP adresi olarak tanımlanan bir IP adresinden kullanıcıları tanımlar. Bu proxy'leri olan kendi aygıtın IP adresi toohide istediğiniz kişiler tarafından kullanılan ve kötü amaçlı için kullanılabilir.


### <a name="impossible-travel-tooatypical-locations"></a>Mümkün olmayan seyahat tooatypical konumları

Bu riski olay türü burada hello konumları en az biri de hello kullanıcı için alışılmadık olabilir, coğrafi olarak birbirinden uzak konumlardan davranış davranışlarına iki oturum açma işlemleri tanımlar. Ayrıca, hello zaman hello iki oturum açma işlemleri arasındaki ele hello kullanıcı tootravel hello ilk konum toohello gelen ikinci hello saatten kısa, farklı bir kullanıcı kullandığını gösteren, hello aynı kimlik bilgileri. 

Belirgin yoksayar bu makine öğrenme algoritmasını "*hatalı pozitif sonuç*" VPN'ler ve düzenli olarak hello kuruluşunuzdaki diğer kullanıcılar tarafından kullanılan konumlar gibi toohello mümkün olmayan seyahat koşul katkıda bulunan.  bir başlangıç öğrenme süre 14 gün boyunca yeni kullanıcının oturum açma davranışı öğrenir Hello sistemine sahiptir.

### <a name="sign-in-from-unfamiliar-locations"></a>Tanınmayan konumlardan oturum aç

Bu riski olay türü oturum açma konumları göz önünde bulundurur (IP, enlem / boylam ve ASN) toodetermine yeni / tanınmayan konumları. Merhaba sistem bir kullanıcı tarafından kullanılan önceki konumları hakkında bilgi depolar ve bu "bilinen" konumları göz önünde bulundurur. Merhaba oturum açma hello tanıdık konumları listesinde olmayan bir konumdan oluştuğunda hello risk olay tetiklenir. Merhaba sistem sırasında tüm yeni konumlar tanınmayan konumları olarak işaretlemez 30 günlük bir ilk öğrenme süresi vardır. Merhaba sistem ayrıca oturum açma işlemleri tanıdık aygıtlardan göz ardı eder ve coğrafi olarak olan konumları tooa tanıdık konumu kapatın. 

### <a name="sign-ins-from-infected-devices"></a>Virüs bulaşmış cihazlardan oturum açma işlemleri

Bu riski olay türüne bir bot sunucusu ile iletişim kurmak tooactively bilinen kötü amaçlı yazılım, virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri tanımlar. Bu, IP adreslerinin bir bot sunucusu ile iletişim kurmuş olan IP adresleri karşı hello kullanıcının cihaz ile ilişkilendirilmesi yoluyla belirlenir. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri
Bu riski olay türü, IP adresleri, çok sayıda başarısız oturum açma denemeleri, birden çok kullanıcı hesapları arasında kısa bir süre boyunca karşılaşılan tanımlar. Bu trafik düzenlerini saldırganlar tarafından kullanılan IP adresleri ile eşleşen ve hesapları ya da zaten olan ya da tehlikeye toobe hakkında güçlü bir göstergesidir. Belirgin yoksayar makine öğrenme algoritmasını budur "*yanlış pozitifler*", IP adresleri gibi hello kuruluşunuzdaki diğer kullanıcılar tarafından düzenli olarak kullanılır.  Burada hello oturum açma davranışını yeni bir kullanıcı ve yeni Kiracı öğrenir bir ilk öğrenme süre 14 gün Hello sistem var.


## <a name="detection-type"></a>Algılama türü

Merhaba algılama type özelliği olan bir gösterge (gerçek zamanlı veya çevrimdışı) için bir risk olayının hello algılama zaman çerçevesi.  
Şu anda Hello risk olay gerçekleştikten sonra çoğu risk olaylarını çevrimdışı bir işlem sonrası işlemi algılandı.

Aşağıdaki tablonun hello hello süreyi ilgili bir rapor için bir algılama türü tooshow işgal listeler:

| Algılama türü | Raporlama gecikme süresi |
| --- | --- |
| Gerçek zamanlı | 5 too10 dakika |
| Çevrimdışı | 2 too4 saatleri |


Azure Active Directory algılar hello risk olayı türleri için hello algılama türleri şunlardır:

| Risk olay türü | Algılama türü |
| :-- | --- | 
| [Sızan kimlik bilgilerine sahip kullanıcılar](#leaked-credentials) | Çevrimdışı |
| [Anonim IP adreslerinden gerçekleştirilen oturum açma işlemleri](#sign-ins-from-anonymous-ip-addresses) | Gerçek zamanlı |
| [Mümkün olmayan seyahat tooatypical konumları](#impossible-travel-to-atypical-locations) | Çevrimdışı |
| [Fazla tanınmayan konumlardan gerçekleştirilen oturum açma işlemleri](#sign-in-from-unfamiliar-locations) | Gerçek zamanlı |
| [Virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri](#sign-ins-from-infected-devices) | Çevrimdışı |
| [Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri](#sign-ins-from-ip-addresses-with-suspicious-activity) | Çevrimdışı|


## <a name="risk-level"></a>Risk düzeyi

Merhaba risk düzeyi bir risk olayı hello önem ve hello güvenirlik risk olayın bir göstergesi (yüksek, Orta veya düşük) özelliğidir. Bu özellik tooprioritize hello eylemler gerçekleştirmeniz gereken yardımcı olur. 

Hello önem hello risk olayın bir göstergesi olduğu kimlik güvenliğinin aşılmasına hello sinyal hello gücünü temsil eder.  
Merhaba güvenirlik hatalı pozitif sonuç hello olasılığını için bir göstergesidir. 

Örneğin, 

* **Yüksek**: yüksek güvenilirlik ve yüksek önem derecesi risk olay. Bu olaylar hello kullanıcının kimliğini tehlikeye girdiğini ve etkilenen herhangi bir kullanıcı hesabı hemen düzeltilmesi güçlü göstergeleri verilmiştir.

* **Orta**: yüksek öneme sahip, ancak daha düşük güvenilirlik risk olayı (veya tersi). Bu olaylar riskli ve etkilenen herhangi bir kullanıcı hesabı düzeltilmesi.

* **Düşük**: Düşük güvenilirlik ve düşük önem risk olay. Bu olay bir Acil eylem gerekli değil, ancak diğer risk olayları ile birleştirildiğinde, kimlik hello güçlü bir gösterge tehlikeye sağlayabilir.

![Risk düzeyi](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Sızan kimlik bilgileri

Kimlik bilgileri Risk olaylarını olarak sınıflandırılan sızmasını bir **yüksek**, hello kullanıcı adı ve parola kullanılabilir tooan saldırgan olduğunu NET bir belirti sağlarlar.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Anonim IP adreslerinden oturum açma işlemleri

Bu riski olay türü için Hello risk düzeyi **orta** anonim bir IP adresi bir hesap güvenliğin güçlü bir gösterge olmadığından.  
Anonim IP adresleri kullanıyorsanız, hemen hello kullanıcı tooverify başvurmanızı öneririz.


### <a name="impossible-travel-tooatypical-locations"></a>Mümkün olmayan seyahat tooatypical konumları

Mümkün olmayan seyahat genellikle bir korsan mümkün toosuccessfully oturum açma olduğunu iyi bir göstergesidir. Ancak, bir kullanıcı yeni bir cihaz veya genellikle hello kuruluşunuzdaki diğer kullanıcılar tarafından kullanılmayan bir VPN kullanarak dolaşırken yanlış pozitif sonuç ortaya çıkabilir. Yanlış sunucusu IP'leri hello görünüm verebilir IP'leri istemci olarak geçirmek uygulamaları yanlış pozitifler başka bir kaynağıdır oturum açma işlemleri burada bu uygulamayı arka uç hello veri merkezi alma yerden barındırılan (genellikle Microsoft veri merkezleri, bunlar Merhaba görünüm verebileceği oturum açma işlemleri Microsoft'tan gerçekleşmesini ait IP adresleri). Bu yanlış pozitifler sonucunda hello risk düzeyi bu risk olay olan **orta**.

> [!TIP]
> Yapılandırarak bu risk olay türü için bildirilen false positves hello miktarını azaltabilirsiniz [konumları adlı](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Tanınmayan konumlardan oturum aç

Tanınmayan konumlardan saldırgan mümkün toouse çalınan kimlik olduğunu güçlü bir gösterge sağlar. Bir kullanıcı seyahat ederken, yeni bir cihaz çalışıyor ya da yeni bir VPN kullanarak yanlış pozitif sonuç ortaya çıkabilir. Bu hatalı pozitif sonuç sonucu olarak, bu olay türü için hello risk düzeyi olan **orta**.

### <a name="sign-ins-from-infected-devices"></a>Virüs bulaşmış cihazlardan oturum açma işlemleri

Bu riski olay IP adresleri, kullanıcı aygıtları tanımlar. Tek bir IP adresi birkaç aygıtlardır ve bazı öğeler yalnızca oturum açma işlemleri diğer aygıtlardan bir bot ağ my tetikleyici bu olay gereksiz yere, bu risk olay sınıflandırma hello neden olduğu denetlediği olarak **düşük**.  

Merhaba kullanıcıyla iletişime geçin ve tüm hello kullanıcının aygıtları tarama öneririz. Kullanıcının kişisel cihaz bulaşmış veya başka birinin hello etkilenen bir aygıttan tarafından kullanılan daha önce belirtildiği gibi aynı IP adresi hello kullanıcı olarak mümkündür. Etkilenen cihazlar genellikle virüsten koruma yazılımı tarafından henüz tanımlanmamış ve etkilenen hello aygıt toobecome neden olmuş olabilir hatalı kullanıcı alışkanlıklarınıza da gösterebilir kötü amaçlı yazılımdan etkilenmiş durumdadır.

Hakkında daha fazla bilgi için tooaddress kötü amaçlı yazılımların yayılmasını bkz hello [kötü amaçlı yazılımdan koruma Merkezi](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri

Bunlar bir gerçekte şüpheli olarak işaretlendi bir IP adresinden imzalı olmadığını hello kullanıcı tooverify başvurmanızı öneririz. Bu olay türü için Hello risk düzeyi "**orta**" birkaç cihaz hello olabileceğinden aynı IP adresi yalnızca bazı hello şüpheli etkinlik için sorumlu olabilir. 


 
## <a name="next-steps"></a>Sonraki adımlar

Risk, Azure AD kimlik koruması hello foundation olaylardır. Azure AD, şu anda altı risk olaylarını tespit edebilirsiniz: 


| Risk olay türü | Risk düzeyi | Algılama türü |
| :-- | --- | --- |
| [Sızan kimlik bilgilerine sahip kullanıcılar](#leaked-credentials) | Yüksek | Çevrimdışı |
| [Anonim IP adreslerinden gerçekleştirilen oturum açma işlemleri](#sign-ins-from-anonymous-ip-addresses) | Orta | Gerçek zamanlı |
| [Mümkün olmayan seyahat tooatypical konumları](#impossible-travel-to-atypical-locations) | Orta | Çevrimdışı |
| [Fazla tanınmayan konumlardan gerçekleştirilen oturum açma işlemleri](#sign-in-from-unfamiliar-locations) | Orta | Gerçek zamanlı |
| [Virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri](#sign-ins-from-infected-devices) | Düşük | Çevrimdışı |
| [Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri](#sign-ins-from-ip-addresses-with-suspicious-activity) | Orta | Çevrimdışı|

Merhaba, ortamınızda algılanan risk olayı bulabileceğiniz?
Burada bildirilen risk olayları gözden iki yerde vardır:

 - **Azure AD raporlama** -Risk olaylarını Azure AD güvenlik parçası olan raporlar. Merhaba daha fazla ayrıntı için bkz: [risk güvenlik raporu kullanıcılar](active-directory-reporting-security-user-at-risk.md) ve hello [riskli oturum açma işlemleri güvenlik raporu](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection** -Risk olaylardır ayrıca parçası [Azure Active Directory Identity Protection'ın](active-directory-identityprotection.md) raporlama özellikleri.
    

Zaten Hello algılama risk olayların kimliklerinizi korumanın önemli bir özelliği temsil ederken bile koşullu erişim ilkeleri yapılandırarak otomatik yanıtlar uygulamak veya bunları el ile adresi hello seçeneği tooeither da vardır. Daha fazla ayrıntı için bkz: [Azure Active Directory Identity Protection'ın](active-directory-identityprotection.md).
 
