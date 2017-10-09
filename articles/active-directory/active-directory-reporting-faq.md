---
title: aaaAzure Active Directory Raporlama ile ilgili SSS | Microsoft Docs
description: Azure Active Directory Raporlama ile ilgili SSS.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>SSS raporlama Azure Active Directory

Bu makale, Azure Active Directory raporlama hakkında sorulan sorular (SSS) yanıtlar toofrequently içerir.  
Daha fazla ayrıntı için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md). 

**S: hello veri bekletme etkinlik günlükleri (Denetim ve oturum açma işlemleri) için hello Azure portalı nedir?** 

**Y:** ücretsiz müşterilerimiz için ve tooan Azure AD Premium 1 veya Premium 2 lisans geçiş tarafından 7 günlük verileri sağlamak için verileri too30 günlerini erişebilirsiniz. Bekletme hakkında daha fazla bilgi için bkz: [Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md)

--- 

**S: my görev tamamladığınızda hello etkinlik verileri görene kadar ne kadar sürer?**

**Y:** denetim etkinlik günlükleri 15 dakika tooan saat arasında bir gecikme vardır. Oturum açma etkinliği günlükleri çoğu kaydeder ve birkaç kayıtları too2 saat 15 dakika arasında değişen bir gecikme süresine sahiptir.

---

**S: bir genel yönetici toosee hello etkinliği hello Azure Portal ya da hello API üzerinden tooget veri günlüklerini toobe gerekiyor?**

**C:** Hayır. Ya da olabilir bir **güvenlik okuyucu**, **güvenlik yönetici** veya **genel yönetici** raporlama verilerini Azure portalında veya hello API erişerek toosee.

---

**S: Office 365 etkinlik günlüğü bilgilerini hello Azure portal aracılığıyla alabilirim?**

**Y:** olsa bile Office 365 etkinliği ve Azure AD etkinlik günlükleri paylaşım çok fazla tam görünümünü istiyorsanız hello dizin kaynak, Office 365 etkinlik günlükleri Merhaba, toohello Office 365 Yönetim Merkezi tooget Office 365 etkinlik günlüğü bilgilerini tamamlamalıdır.

---


**S: hangi API'leri yapmak Office 365 etkinlik günlükleri tooget bilgilerini kullanmak?**

**Y:** kullanım hello Office 365 Yönetim API'leri tooaccess hello [Office 365 etkinlik günlükleri bir API aracılığıyla](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**S: kaç kayıt Azure portalından karşıdan yükleyebilir miyim?**

**Y:** hello Azure portal too120K kayıtları yukarı indirebilirsiniz. Merhaba kayıtları tarafından sıralanır *en son* ve varsayılan olarak, en son 120 K hello kayıtları alın. 

---

**S: kaç kayıt ı hello etkinlikleri API sorgulama yapabilirsiniz?**

**Y:** too1 milyon kayıtlarını sorgulama yapabilirsiniz (çoğu tarafından hello kayıt sıralar hello top işleci kullanmazsanız son). Merhaba "top" işleci kullanırsanız too500K kayıtları sorgulayabilirsiniz. Örnek sorgular nasıl toouse hello API burada üzerinde bulabilirsiniz [burada](active-directory-reporting-api-getting-started.md).

---

**S: premium lisansı nasıl sağlarım?**

**Y:** bkz [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md) bir yanıt toothis soru için.

---

**S: kadar kısa sürede ı etkinlikleri veri premium lisansı aldıktan sonra görmeniz gerekir?**

**Y:** ücretsiz bir lisans gibi etkinlikler veriler zaten varsa, görebilirsiniz hello aynı veri. Herhangi bir veri yoksa, bir veya iki gün sürer.

---

**S: Son ayın verilerini bir Azure AD premium lisansı aldıktan sonra görüyor musunuz?**

**Y:** (bir deneme sürümü dahil) tooa Premium sürüm son geçtiyseniz, veri too7 günlerini başlangıçta görebilirsiniz. Veri öğelerden too30 günleri görürsünüz.

---

**S: bir risk olayı kimlik koruması olmakla birlikte hello karşılık gelen oturum içindeki tüm oturum açma işlemleri görüyorum değil. Bu beklenen bir durumdur?**

**Y:** Evet, kimlik koruması tüm kimlik doğrulama akışlar için risk olup olmadığını değerlendirir etkileşimli veya etkileşimli olmayan olabilir. Ancak, tüm oturum açma işlemleri yalnızca rapor yalnızca hello etkileşimli oturum açma işlemleri gösterir.

---

**S: nasıl hello "İçin risk bayrak eklenen kullanıcılar" rapor Azure portalında karşıdan yükleyebilir miyim?**

**Y:** hello seçeneği toodownload *bayrak eklenen kullanıcılar için risk* rapor yakında eklenecek.

---

**S: neden bir oturum açma veya bir kullanıcı hello Azure portal'ın riskli bayrakla edildi nasıl biliyor musunuz?**

**Y:** Premium edition müşteriler risk olaylarını "İçin risk bayrak eklenen kullanıcılar" Merhaba kullanıcı tıklayarak veya "Riskli gerçekleştirilen oturum açma" Merhaba üzerinde tıklatarak temel hello hakkında daha fazla bilgi. Ücretsiz ve temel sürümü müşteriler risk olay bilgilerini temel hello toosee hello at-risk kullanıcılar ve oturum açma işlemleri alın.

---

**S: nasıl IP adreslerini hello oturum açma işlemleri ve riskli oturum açma işlemleri raporu hesaplandığını??**

**Y:** IP adresleri, bir IP adresi ve hello bilgisayarın adresine sahip fiziksel olarak bulunduğu arasında kesin bağlantı yoktur şekilde yayınlanır. Bu etkenler mobil sağlayıcıları ve hello istemci aygıt gerçekte kullanıldığı gölgeden uzak IP adresleri merkezi havuzlarından genellikle çok veren VPN gibi karmaşık. IP adresi tooa fiziksel konum dönüştürme Hello yukarıdaki verildiğinde, izlemeleri, kayıt defteri verilerini, geriye doğru arama ve diğer bilgilere göre en iyi çaba olur. 

---
