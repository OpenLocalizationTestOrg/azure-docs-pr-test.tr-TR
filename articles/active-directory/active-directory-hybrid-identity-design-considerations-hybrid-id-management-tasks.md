---
title: "Active Directory karma kimlik aaaAzure tasarım konuları - karma kimlik yönetimi görevleri belirlemek | Microsoft Docs"
description: "Koşullu erişim denetimi ile Azure Active Directory hello belirli koşullar hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin vermeden önce çekme denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Karma kimlik yaşam döngüsü planlaması
Kimlik, enterprise mobility ve uygulama erişim stratejinizi hello temellerinden biridir. Tooyour mobil cihaz veya SaaS uygulamasına oturum açıyorsanız, kimliğinizi hello anahtar toogaining erişim tooeverything olup. En yüksek düzeyde bir kimlik yönetimi çözümü birleştirin ve otomatikleştirmek ve kaynakları sağlama işleminin hello merkezileştirme içeren, kimlik depoları arasında eşitleniyor kapsar. Hello kimlik çözümü merkezi kimlik şirket içi ve bulut arasında olması da çeşit kimlik Federasyon toomaintain merkezi kimlik doğrulaması kullanmak ve güvenli bir şekilde paylaşmak ve dış kullanıcılar ve işletmelerin işbirliği yapmak. Kaynakları işletim sistemlerini ve uygulamaları toopeople aralığı veya bir kuruluşla ilişkili. Organizasyon yapısı değiştirilmiş tooaccommodate hello sağlama ilkeleri ve yordamlarıyla olabilir.

Ayrıca toohave bir kimlik çözümü sağlamıştır tooempower kullanıcılarınıza bunlarla sağlayarak önemlidir Self Servis karşılaştığında tookeep üretken bunları. Kimlik çözümünüzü Yöneticiler hiç erişim ihtiyaç duydukları tüm hello kaynaklar arasında kullanıcılar için çoklu oturum açmayı etkinleştirir düzeyleri standartlaştırılmış yordamları kullanıcı kimlik bilgilerini yönetmek için kullanabilirsiniz daha sağlamdır. Bazı yönetim düzeylerini azaltılmış veya ortadan, yönetim çözümü sağlama hello hello derecesini bağlı olarak. Ayrıca, güvenli bir şekilde yönetim yetenekleri el ile veya otomatik olarak, çeşitli kuruluş arasında dağıtabilirsiniz. Örneğin, bir etki alanı yöneticisi, yalnızca hello kişileri ve bu etki alanındaki kaynaklara hizmet verebilir. Bu kullanıcı sağlama ve yönetim görevlerini gerçekleştirebilir, ancak yapılandırma görevleri, iş akışları oluşturma gibi yetkili değil toodo olur.

## <a name="determine-hybrid-identity-management-tasks"></a>Karma kimlik yönetimi görevleri belirleme
Kuruluşunuzdaki yönetim görevlerini dağıtma hello doğruluğunu ve yönetim verimliliğini artırır ve hello iş yükü, bir kuruluşun hello bakiyesini artırır. Güçlü kimlik yönetimi sistemi tanımlamak hello özetlere aşağıda verilmiştir.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

toodefine karma kimlik yönetimi görevleri, bazı temel özellikler karma kimlik benimsediği hello kuruluşun anlamanız gerekir. Önemli toounderstand hello geçerli depoları kimlik kaynakları için kullanılmakta olan. Öğrenerek bu öğeleri çekirdek, hello temel gereksinimleri vardır ve tooask gerektiğine göre daha ayrıntılı, sorular tooa daha iyi tasarım kararı Identity çözümünü götürür.  

Bu gereksinimleri tanımlarken, en az hello aşağıdaki olun soruları

* Sağlama seçenekleri: 
  
  * Merhaba karma kimlik çözümü, güçlü bir hesap erişim yönetimi ve sağlama sistem destekliyor mu?
  * Kullanıcıları, grupları ve yönetilen toobe giderek parolaları nasıl misiniz?
  * Merhaba kimlik yaşam döngüsü yönetimi esnek mi? 
    * Parola güncelleştirmeleri hesabı askıya ne kadar sürer?
* Lisans Yönetimi: 
  
  * Karma kimlik çözümü tanıtıcıları Lisans Yönetimi hello mu?
    * Yanıt Evet ise, hangi özellikler sağlanıyor?
* Çözüm tanıtıcısı grup tabanlı Lisans Yönetimi hello mu? 
  
      - Yanıt Evet ise, olası tooassign bir güvenlik grubu tooit mi? 
       - Yanıt Evet ise, hello bulut dizini lisansları tooall hello hello grubunun üyeleri otomatik olarak ata? 
        - Bir kullanıcı daha sonra eklenen veya hello grubundan kaldırılmış, bir lisans otomatik olarak atanmış veya kaldırılacak uygun şekilde kaldırılan neler? 
* Diğer üçüncü taraf kimlik sağlayıcıları ile tümleştirme:
* Bu karma çözümü, üçüncü taraf kimlik sağlayıcıları tooimplement çoklu oturum açma ile tümleştirilebilir?
* Olası toounify olan tüm bağlı kimlik sisteme farklı kimlik sağlayıcıları hello?
* Yanıt Evet ise, nasıl ve bunlar ve hangi özellikler sağlanıyor?

## <a name="synchronization-management"></a>Eşitleme Yönetimi
Merhaba hedeflerinden biri bir Identity manager toobe mümkün toobring tüm kimlik sağlayıcıları hello ve bunları eşitlenmiş tut. Merhaba verileri eşitlenmiş tutmak bir yetkili ana kimlik sağlayıcısını temel. Eşitlenmiş yönetim modeliyle bir karma kimlik senaryosunda bir şirket içi sunucu tüm kullanıcı ve cihaz kimliklerini yönetmek ve hello hesapları ve isteğe bağlı olarak, parolalar toohello bulut eşitleyin. Merhaba kullanıcı aynı parola şirket içi aksine hello bulutta ve oturum açma hello parola doğrulanır hello kimlik çözümü tarafından hello girer. Bu model, directory eşitleme aracını kullanır.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)karma kimlik çözümü tooproper tasarım hello eşitleme olun sorular aşağıdaki o hello yanıtlanır: • hello karma kimlik çözümü için kullanılabilir hello eşitleme çözümleri nelerdir?
• Hello çoklu oturum açma kullanılabilen özellikleri nelerdir?
• B2B B2C arasındaki Kimlik Federasyonu için hello seçenekleri nelerdir?

## <a name="next-steps"></a>Sonraki adımlar
[Karma kimlik yönetimini benimseme stratejinizi belirleme](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

