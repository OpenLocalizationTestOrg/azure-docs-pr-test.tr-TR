---
title: "Azure Active Directory'de koşullu erişim için aaaBest uygulamaları | Microsoft Docs"
description: "Bilmeniz gerekenler ve koşullu erişim ilkeleri yapılandırırken bunun kaçınmalısınız nedir hakkında bilgi edinin."
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
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Azure Active Directory'de koşullu erişim için en iyi yöntemler

Bu konu, bilmeniz gerekenler ve koşullu erişim ilkeleri yapılandırırken bunun kaçınmalısınız nedir hakkında bilgi sağlar. Bu konu okumadan önce hello kavramları öğrenmeniz ve hello terminolojisi özetlenen [Azure Active Directory'de koşullu erişim](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Bilmeniz gerekenler

### <a name="whats-required-toomake-a-policy-work"></a>Toomake bir ilke iş ne gereklidir?

Yeni bir ilke oluşturduğunuzda, hiçbir kullanıcıları, grupları, uygulamalar veya seçili erişim denetimleri vardır.

![Bulut uygulamaları](./media/active-directory-conditional-access-best-practices/02.png)


ilkeniz toomake çalışma, hello aşağıdakileri yapılandırın:


|Ne           | Nasıl                                  | Neden|
|:--            | :--                                  | :-- |
|**Bulut uygulamaları** |Bir veya daha fazla uygulama tooselect gerekir.  | Merhaba koşullu erişim ilkesi hedefidir tooenable toofine ayarlama nasıl yetkili kullanıcılar, uygulamalara erişebilir.|
| **Kullanıcılar ve gruplar** | En az bir tooselect gereken kullanıcı veya grup yetkili tooaccess hello bulut uygulamalarını seçtiniz. | Hiçbir zaman yok kullanıcılar ve gruplar atanan bir koşullu erişim ilkesi tetiklenir. |
| **Erişim denetimleri** | En az bir tooselect gereken erişim denetimi. | Koşullarınızı sağlanırsa, ilke işlemci hangi toodo tooknow gerekir.|


Toplama toothese temel gereksinimleri, çoğu durumda, bir koşul yapılandırmanız gerekir. Bir ilke yapılandırılmış bir koşulu de çalışması sırasında erişim tooyour uygulamaları ince ayar yapmak için hello yönlendirmeli faktörü koşullardır.


![Bulut uygulamaları](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Atamaları nasıl değerlendirildiği?

Tüm atamaları mantıksal olarak olan **and işleciyle**. Yapılandırılmış, birden fazla atama tootrigger bir ilke varsa, tüm atamaları sağlanmalıdır.  

Tooconfigure, kuruluşunuzun ağ dışından yapılan tooall bağlantılara uygulanır bir konum koşul gerekiyorsa, bunu gerçekleştirebilirsiniz:

- Dahil olmak üzere **tüm konumları**
- Hariç **tüm güvenilen IP'leri**

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>İlkeleri'nde hello Klasik Azure portalı ve Azure portalı yapılandırılmış varsa ne olur?  
Her iki ilkeleri Azure Active Directory tarafından uygulanır ve yalnızca tüm gereksinimleri karşılandığında hello kullanıcı erişim alır.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>Merhaba Intune Silverlight portal ilkelerinde ve hello Azure Portal varsa ne olur?
Her iki ilkeleri Azure Active Directory tarafından uygulanır ve yalnızca tüm gereksinimleri karşılandığında hello kullanıcı erişim alır.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>Aynı kullanıcı tarafından yapılandırılmış hello için birden çok ilke varsa ne olur?  
Her oturum açma için Azure Active Directory tüm ilkeler değerlendirir ve verilen toohello kullanıcıya erişim önce tüm gereksinimlerin karşılandığını sağlar.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>Koşullu erişim, Exchange ActiveSync ile çalışır mı?

Evet, Exchange ActiveSync bir koşullu erişim ilkesini kullanabilirsiniz.


## <a name="what-you-should-avoid-doing"></a>Bunu yaptığınızda kaçınmanız gerekir

Merhaba koşullu erişim framework harika yapılandırma esnekliği sağlar. Ancak, büyük esneklik ayrıca her yapılandırma İlkesi önceki tooreleasing dikkatle gözden geçirmelidir anlamına gelir, tooavoid istenmeyen sonuçları. Bu bağlamda tam kümeleri gibi etkileyen özel dikkat tooassignments ödeme **tüm kullanıcıları / grupları / bulut uygulamaları**.

Ortamınızda yapılandırmaları aşağıdaki hello kaçınmanız gerekir:


**Tüm kullanıcılar için tüm bulut uygulamalarından:**

- **Erişimi engelleme** -bu yapılandırmayı kesinlikle iyi bir fikir değil, tüm kuruluş engeller.

- **Uyumlu aygıt gerektiren** - kullanıcılar için yok sahip kayıtlı cihazlarını henüz, bu ilke erişim toohello Intune portalı dahil olmak üzere tüm erişimini engeller. Kayıtlı bir cihazın olmadan bir yöneticiyseniz Bu ilke hello Azure portal toochange hello İlkesi'ne geri alamazsınız engeller.

- **Etki alanına katılmayı gerektirecek** - Bu ilke bloğu erişimi de hello olası tooblock erişim tüm kullanıcılar için kuruluşunuzdaki bir etki alanına katılmış cihazınız henüz yoksa.


**Tüm kullanıcılar, tüm bulut uygulamaları, tüm cihaz platformları için:**

- **Erişimi engelleme** -bu yapılandırmayı kesinlikle iyi bir fikir değil, tüm kuruluş engeller.


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
