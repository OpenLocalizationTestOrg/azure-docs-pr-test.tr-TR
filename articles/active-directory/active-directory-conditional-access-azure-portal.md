---
title: "Active Directory koşullu erişim aaaAzure | Microsoft Docs"
description: "Koşullu erişim denetimi için erişim tooapplications doğrulanırken belirli koşullar için Azure Active Directory toocheck kullanın."
services: active-directory
keywords: "koşullu erişim tooapps, Azure AD ile koşullu erişim toocompany kaynaklarına, koşullu erişim ilkeleri güvenli erişim"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Azure Active Directory'de koşullu erişim

Bir mobil ilk olarak, bulut ilk dünyasında, Azure Active Directory oturum açma tek toodevices, uygulama ve hizmetlere her yerden sağlar. Devre dışı şirket ağlarına (KCG) aygıtlar Hello artışı ile beraber çalışma ve 3 taraf SaaS uygulamalar, BT uzmanları iki rakip hedefle karşılaştığı:

- Merhaba son kullanıcıların toobe üretken yerde ve zamanda güç kazandırma
- Herhangi bir zamanda Hello şirket varlıklarını koruma

tooimprove üretkenlik, Azure Active Directory kullanıcılarınıza seçenekleri tooaccess geniş bir yelpazedeki şirket varlıklarınızı sağlar. Uygulama erişim yönetimini kullanarak, yalnızca tooensure sağlayan Azure Active Directory *doğru kişilerin hello* uygulamalarınızı erişebilirsiniz. Ne toohave hello doğru kişilerin kaynaklarınızı belirli koşullar altında nasıl erişiyorsunuz üzerinde daha fazla denetim isterseniz? Hatta koşullar altında istediğiniz tooblock erişim toocertain uygulamaları bile Merhaba yoksa ne *sağ kişiler*? Örneğin, belirli uygulamaların güvenilen bir ağdan Hello doğru kişilerin erişiyorsanız, Tamam olması olabilir; Ancak, siz bunları tooaccess güvenmediğiniz bir ağ üzerinden bu uygulamaları istemeyebilirsiniz. Koşullu erişim kullanarak bu soruları ele alabilir.

Koşullu erişim, ortamınızdaki belirli koşullara göre erişim tooapps hello tooenforce denetimleri sağlar Azure Active Directory bir yetenektir. Denetimler ile ya da ek gereksinimler toohello erişim bağlayabilirsiniz veya, engelleyebilirsiniz. Merhaba koşullu erişim ilkelerini temel alır. Erişim gereksinimlerinizi hakkında düşünmek hello yolu izleyen gerektiğinden, ilke tabanlı bir yaklaşım yapılandırma deneyiminizi kolaylaştırır.  

Genellikle, desen aşağıdaki hello üzerinde temel deyimleri kullanarak erişim gereksinimlerinizi tanımlayın:

![denetimi](./media/active-directory-conditional-access-azure-portal/10.png)

Merhaba iki oluşumları yerine ne zaman "*bu*" gerçek bilgilerle bir örnek için büyük olasılıkla tanıdık tooyou benzeyen bir ilke bildirimi vardır:

*Yükleniciler tooaccess bizim bulut uygulamalarını güvenilmeyen ağlarla çalışırken, erişimi engeller.*

Yukarıdaki Hello İlkesi ifade hello güç koşullu erişim vurgular. Yükleniciler toobasically etkinleştirebilirsiniz karşın, bulut uygulamalarınızı erişim (**kimin**), koşullu erişim ile koşullar altında hangi hello erişim mümkündür de tanımlayabilirsiniz (**nasıl**).

Azure Active Directory koşullu erişim Hello bağlamda

- "**Bu durumda**" olarak adlandırılır **koşul deyimi**
- "**Sonra bunu**" olarak adlandırılır **denetimleri**

![denetimi](./media/active-directory-conditional-access-azure-portal/11.png)

bir koşul deyimi, denetimleri ile Merhaba birleşimi bir koşullu erişim ilkesi temsil eder.

![denetimi](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Denetimler

Bir koşullu erişim ilkesi, bir koşul deyimi yerine getirdiğinizde olacağını nedir denetimleri tanımlayın.  
Denetimler ile için erişimi engellemek veya ek gereksinimler erişimle izin verebilirsiniz.
Erişime izin veren bir ilke yapılandırdığınızda tooselect gereken en az bir gereksinimi.   

### <a name="grant-controls"></a>Verme denetimleri
Merhaba geçerli uygulama Azure Active Directory grant denetimi gereksinimlerine tooconfigure hello sağlar:

![denetimi](./media/active-directory-conditional-access-azure-portal/05.png)

- **Çok faktörlü kimlik doğrulaması** -çok faktörlü kimlik doğrulaması aracılığıyla güçlü kimlik doğrulaması gerektirir. Sağlayıcısı olarak, Azure multi-Factor veya Active Directory Federasyon Hizmetleri (AD FS) ile birlikte bir şirket içi çok faktörlü kimlik doğrulama sağlayıcısı olarak kullanabilirsiniz. Çok faktörlü kimlik doğrulamasını kullanarak erişim toohello geçerli bir kullanıcı kimlik bilgilerini elde etmiştir yetkisiz bir kullanıcı tarafından erişilen kaynaklar korunmasına yardımcı olur.

- **Uyumlu aygıt** -hello cihaz düzeyinde koşullu erişim ilkeleri ayarlayabilirsiniz. Uyumlu olan bir ilke tooonly etkinleştir bilgisayarları ayarlayabilir veya mobil aygıtları, kuruluşunuzun kaynakları bir mobil cihaz Yönetimi tooaccess içinde kayıtlı. Örneğin, Intune toocheck cihaz uyumluluğu kullanın ve hello kullanıcı tooaccess uygulama çalıştığında tooAzure AD zorlama için rapor. Toouse Intune tooprotect uygulamaları ve verileri nasıl görürüm hakkında ayrıntılı yönergeler için [uygulamaları ve Microsoft Intune ile verileri koruma](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). Intune tooenforce veri koruması kaybolan veya çalınan cihazlar için de kullanabilirsiniz. Daha fazla bilgi için bkz: [Microsoft Intune kullanarak tam veya seçmeli Temizleme ile verilerinizin korunmasına yardımcı olma](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Etki alanına katılmış bir cihaz** – tooconnect tooAzure Active Directory toobe etki alanına katılmış tooyour kullanmış hello cihaz şirket içi Active Directory (AD) gerektirebilir. Bu ilke tooWindows Masaüstü ve dizüstü bilgisayarlar ile Kurumsal tabletlerde uygulanır. 

Seçilen birden çok denetim varsa, ilkenizi işlendiğinde, bunların tümünün gerekli olup olmadığını da yapılandırabilirsiniz.

![denetimi](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Oturum denetimleri
Oturum denetimleri bir bulut uygulama içinde sınırlama deneyimi sağlar. Hello oturum denetimleri bulut uygulamaları tarafından zorunlu tutulmaz ve Azure AD toohello uygulaması hello oturumla ilgili tarafından sağlanan ek bilgileri kullanır.

![denetimi](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Zorlanan uygulama kısıtlamaları kullanan
Bu denetim toorequire Azure AD toopass hello cihaz bilgileri toohello bulut uygulaması kullanabilirsiniz. Bu hello bulut uygulamanın hello kullanıcı bir uyumlu aygıt veya etki alanına katılmış CİHAZDAN geliyorsa bilmesini sağlar. Bu denetimidir şu anda yalnızca hello bulut uygulaması olarak SharePoint ile desteklenir. SharePoint hello aygıt bilgileri tooprovide kullanıcıları hello cihaz durumuna bağlı olarak bir tam veya sınırlı deneyimi kullanır.
nasıl toorequire SharePoint erişimle sınırlı hakkında daha fazla toolearn Git [burada](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Koşul deyimi

Merhaba önceki bölümde toosupported seçenekleri tooblock anlatılmıştır veya denetimleri biçiminde tooyour kaynaklara erişmek kısıtlayın. Bir koşullu erişim ilkesi için bir koşul deyimi formunda uygulanan, denetimleri toobe karşılanır toobe gereken hello ölçütleri tanımlayın.  

Atamaları, bir koşul deyimi aşağıdaki hello içerebilir:

![denetimi](./media/active-directory-conditional-access-azure-portal/07.png)


- **Kimin** -çoğu durumda, denetimleri uygulanan toobe tooa belirli kullanıcıları kümesini istiyor. Bir koşul deyiminde hello kullanıcılar ve gruplar, ilkenin uygulandığı seçerek bu kümesi tanımlayabilirsiniz. Gerekirse, ilkeden muaf tutma tarafından bir kullanıcı kümesini açıkça dışlayabilirsiniz.  
Kullanıcılar ve Gruplar'ı seçerek, ilkenin uygulandığı kullanıcılar hello kapsamını tanımlayın.    

    ![denetimi](./media/active-directory-conditional-access-azure-portal/08.png)



- **Ne** -genellikle, bir koruma açısından diğerlerinden daha fazla dikkat gerektiren ortamınızda çalışan belirli uygulamalar vardır. Bu, örneğin, erişim toosensitive verilere sahip uygulamaları etkiler.
Bulut uygulamalarını seçerek, ilkenin uygulandığı bulut uygulamalarını hello kapsamını tanımlayın. Gerekirse, ilkeden uygulamaları kümesi de açıkça hariç tutabilirsiniz.

    ![denetimi](./media/active-directory-conditional-access-azure-portal/09.png)


- **Nasıl** - erişim tooyour uygulamaları gerçekleştirilir sürece koşullarda denetleyebilirsiniz, üzerinde ek denetimler izlenmesi için gerekli nasıl bulut uygulamalarınız erişilebilir kullanıcılarınız tarafından orada olabilir. Ancak, işleri erişim tooyour bulut uygulamalarını gerçekleştirilir, örneğin, güvenilir olmayan ağlara veya uyumlu olmayan cihazlardan farklı görünebilir. Bir koşul deyiminde erişim tooyour uygulamaları nasıl gerçekleştirildiğini için ek gereksinimlerin belirli erişim koşulları tanımlayabilirsiniz.

    ![Koşullar](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Koşullar

Merhaba geçerli uygulama Azure Active Directory, hello alanları aşağıdaki koşulları tanımlayabilirsiniz:

- Oturum açma riski
- Cihaz platformları
- Konumlar
- İstemci uygulamaları

![Koşullar](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Oturum açma riski

Bir oturum açma riski bir oturum açma girişimi hello yasal sahibi bir kullanıcı hesabı tarafından gerçekleştirilmedi Azure Active Directory tootrack hello olasılığını tarafından kullanılan bir nesne oluşturur. Bu nesne, hello olasılığını (yüksek, Orta veya düşük) adlı bir öznitelik biçiminde depolanır [oturum açma risk düzeyi](active-directory-reporting-risk-events.md#risk-level). Oturum açma riskleri Azure Active Directory tarafından algılanmış ise bu nesne bir oturum açma sırasında bir kullanıcının oluşturulur. Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins).  
Bir koşullu erişim ilkesi koşulu olarak hesaplanan hello oturum açma risk düzeyi kullanabilirsiniz. 

![Koşullar](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Cihaz platformları

Merhaba cihaz platformu, cihazda çalışan hello işletim sistemi tarafından belirlenir:

- Android
- iOS
- Windows Phone
- Windows
- macOS (Önizleme). 

![Koşullar](./media/active-directory-conditional-access-azure-portal/02.png)

Bir ilkeden muaf tutulan cihaz platformları yanı sıra dahil edilen hello cihaz platformları tanımlayabilirsiniz.  
toouse cihaz platformları hello İlkesi'nde, ilk değişiklik hello yapılandırma değiştirir çok**Evet**, tümünü seçin ve tek tek cihaz platformları hello ilkesi uygulanır. Tek tek cihaz platformlarını seçin hello İlkesi bu platformlarda yalnızca bir etkisi yoktur. Bu durumda, oturum açma işlemleri tooother desteklenen platformlar hello İlkesi tarafından etkilenmez.


### <a name="locations"></a>Konumlar

Merhaba konumu tanımlanan hello istemcisinin hello IP adresine göre tooconnect tooAzure Active Directory kullandınız. Bu durum toobe aşina gerektirir **konumları adlı** ve **MFA güvenilen IP'leri**.  

**Konumları adlı** , kuruluşların güvenilir toolabel IP adres aralıklarını verir Azure Active Directory özelliğidir. Ortamınızda, adlandırılmış konumlarını hello algılanması hello bağlamda kullanabilirsiniz [risk olayları](active-directory-reporting-risk-events.md) koşullu erişim yanı sıra. Azure Active Directory konumlarında adlı yapılandırma hakkında daha fazla ayrıntı için bkz: [Azure Active Directory konumlarında adlı](active-directory-named-locations.md).

yapılandırabileceğiniz konumları Hello sayısı hello ilgili nesne hello boyutu tarafından Azure AD'de kısıtlıdır. Aşağıdakileri yapılandırabilirsiniz:
 
 - Bir adlandırılmış konumla too500 IP aralıkları
 - En fazla 60 adlandırılmış konumları (Önizleme) bir IP aralığı ile bunların tooeach atanan 


**MFA güvenilen IP'leri** kuruluşunuzun yerel intranet temsil eden toodefine güvenilen IP adres aralıklarını sağlayan çok faktörlü kimlik doğrulaması, bir özelliğidir. Güvenilen IP'ler konumu koşullar yapılandırdığınızda, kuruluşunuzun ağ ve diğer tüm konumlara yapılan bağlantılar arasında toodistinguish sağlar. Daha fazla ayrıntı için bkz: [güvenilen IP'leri](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Tüm konumları ya da içerebilir veya tüm güvenilen IP'leri ve tüm güvenilen IP'leri hariç tutabilirsiniz.

![Koşullar](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>İstemci uygulaması

Hello istemci uygulama, genel düzey hello uygulama (web tarayıcısı, mobil uygulama, masaüstü istemcisi) tooconnect tooAzure Active Directory kullandınız veya Exchange Active Sync özellikle seçebilirsiniz olabilir.  
Eski kimlik doğrulaması modern kimlik doğrulaması kullanmayan eski Office istemcileri gibi temel kimlik doğrulaması kullanarak tooclients başvuruyor. Koşullu erişim eski kimlik doğrulaması ile şu anda desteklenmiyor.

![Koşullar](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Genel senaryolar

### <a name="requiring-multi-factor-authentication-for-apps"></a>Çok faktörlü kimlik doğrulaması gerektiren uygulamalar için

Çoğu ortam daha yüksek düzeyde koruma hello daha başkalarının gerektiren uygulamalar vardır.
Bu, örneğin, hello erişim toosensitive verilere sahip uygulamalar için geçerlidir.
Koruma toothese uygulamaların başka bir katmana tooadd istiyorsanız, kullanıcılar bu uygulamaları erişirken, çok faktörlü kimlik doğrulaması gerektiren bir koşullu erişim ilkesi yapılandırabilirsiniz.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Güvenilir olmayan ağlara erişim için çok faktörlü kimlik doğrulama gerektirme

Bu senaryo benzer toohello önceki senaryoda nedeni, çok faktörlü kimlik doğrulama gereksinimini ekler.
Ancak, hello temel fark hello bu gereksinim için bir durumdur.  
Merhaba odak hello önceki senaryonun uygulamalara erişim toosensitve verilerle çalışırken, bu senaryonun hello odak güvenilen konumlarının noktasıdır.  
Diğer bir deyişle, bir uygulama güvenmediğiniz bir ağdan bir kullanıcı tarafından erişilen, çok faktörlü kimlik doğrulama gereksinimini olabilir.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Yalnızca güvenilir cihazlar Office 365 hizmetlerine erişebilir

Ortamınızda Intune kullanıyorsanız, hello koşullu erişim ilkesi hello Azure konsolunda arabiriminde kullanmaya hemen başlayabilirsiniz.

Birçok Intune müşterileri yalnızca güvenilen cihazların Office 365 hizmetlerine erişmesini koşullu erişim tooensure kullanıyor. Bu, mobil cihazları Intune'a kayıtlı ve uyumluluk ilkesi gereksinimlerini ve Windows bilgisayarları şirket içi etki alanına katılmış tooan olduğunu anlamına gelir. Önemli geliştirmelerden, olmadığı olduğu tooset hello aynı ilke her hello Office 365 Hizmetleri için.  Yeni bir ilke oluşturduğunuzda, hello bulut uygulamaları tooinclude her ile koşullu erişim ile tooprotect istediğiniz hello O365 uygulamaların yapılandırın.

## <a name="next-steps"></a>Sonraki adımlar

Tooknow nasıl tooconfigure bir koşullu erişim ilkesi görmek istiyorsanız [Azure Active Directory'de koşullu erişimi kullanmaya başlama](active-directory-conditional-access-azure-portal-get-started.md).

Ortamınız için hazır tooconfigure koşullu erişim ilkeleri olup olmadığını hello görmek [Azure Active Directory'de koşullu erişim için en iyi uygulamaları](active-directory-conditional-access-best-practices.md). 
