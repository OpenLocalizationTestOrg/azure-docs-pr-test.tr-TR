---
title: "Azure AD Connect: Sonraki adımlar ve nasıl toomanage Azure AD Connect | Microsoft Docs"
description: "Nasıl tooextend hello varsayılan yapılandırması ve işletimsel görevler için Azure AD Connect öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Sonraki adımlar ve nasıl toomanage Azure AD Connect
Bu makale toocustomize Azure Active Directory (Azure AD) Bağlan toomeet Hello işletimsel yordamları, kuruluşunuzun ihtiyaçları ve gereksinimleri kullanın.  

## <a name="add-additional-sync-admins"></a>Ek eşitleme yöneticileri ekleyin
Varsayılan olarak, yükleme ve yerel Yöneticiler hello yalnızca hello kullanıcının mümkün toomanage yüklü hello eşitleme altyapısı etkilenir. Diğer kişilere toobe mümkün tooaccess için ve hello eşitleme altyapısı yönetmek, hello yerel sunucuda ADSyncAdmins adlı hello grubunu bulun ve toothis grubunu ekleyin.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Kullanıcıların AD Premium ve Enterprise Mobility Suite lisansları tooAzure atayın
Kullanıcılarınızın silinmiş göre toohello bulut eşitlenen tooassign gerekir bunları bunlar Office 365 gibi bulut uygulamalarıyla kullanmaya başlayabilirsiniz için bir lisans.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>bir Azure AD Premium veya Enterprise Mobility Suite lisansı tooassign

1. İçinde toohello Azure portalında bir yönetici olarak oturum açın.
2. Merhaba solda seçin **Active Directory**.
3. Merhaba üzerinde **Active Directory** sayfasında, Yukarı tooset istediğiniz hello kullanıcılara hello dizini çift tıklatın.
4. Merhaba hello dizin sayfanın en üstünde, seçin **lisansları**.
5. Merhaba üzerinde **lisansları** sayfasında, **Active Directory Premium** veya **Enterprise Mobility Suite**ve ardından **atamak**.
6. Merhaba iletişim kutusunda, tooassign lisansları istediğiniz ve hello onay işareti simgesi toosave hello değişiklikleri ardından hello kullanıcıları seçin.

## <a name="verify-hello-scheduled-synchronization-task"></a>Merhaba zamanlanmış eşitleme görevi doğrulayın
Hello Azure portal toocheck hello bir eşitleme durumunu kullanın.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tooverify hello zamanlanmış eşitleme görevi
1. İçinde toohello Azure portalında bir yönetici olarak oturum açın.
2. Merhaba solda seçin **Active Directory**.
3. Merhaba üzerinde **Active Directory** sayfasında, Yukarı tooset istediğiniz hello kullanıcılara hello dizini çift tıklatın.
4. Merhaba hello dizin sayfanın en üstünde, seçin **dizin tümleştirme**.
5. Altında **yerel active directory ile tümleştirme**, Not hello son eşitleme zamanı.

<center>![Dizin eşitleme zamanı](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Zamanlanan eşitleme görevi Başlat
Eşitleme görevi toorun gerekiyorsa, hello Azure AD Connect Sihirbazı yeniden çalıştırarak bunu yapabilirsiniz.  Azure AD kimlik bilgilerinizi tooprovide gerekir.  Merhaba Hello Sihirbazı'nda seçin **eşitleme seçeneklerini özelleştirme** tıklayın ve görev **sonraki** toomove hello Sihirbazı aracılığıyla. Bu hello Hello sonunda olun **hello ilk yapılandırma tamamlandıktan hemen sonra hello eşitleme işlemini başlatmak** kutusu seçilidir.

<center>![Eşitlemeyi Başlat](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Hello Azure AD Connect eşitleme Zamanlayıcı hakkında daha fazla bilgi için bkz: [Azure AD Connect Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Azure AD Connect kullanılabilir ek görevler
Azure AD Connect ilk, yüklemeden sonra her zaman hello Sihirbazı'nı yeniden hello Azure AD Connect başlangıç sayfası veya Masaüstü kısayoldan başlatabilirsiniz.  Merhaba Sihirbazı aracılığıyla yeniden giderek ek görevler hello formunda yeni bazı seçenekler sunar fark edeceksiniz.  

Merhaba aşağıdaki tabloda bu görevleri özetini ve her görevin kısa bir açıklamasını sağlar.

![Ek görevler listesi](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Ek görevi | Açıklama |
| --- | --- |
| **Görünüm hello seçili senaryosu** |Geçerli Azure AD Connect çözümünüzü görüntüleyin.  Bu eşitlenmiş genel ayarları içeren dizinler ve eşitleme ayarları. |
| **Eşitleme seçeneklerini özelleştirme** |Ek Active Directory ormanları toohello yapılandırma ekleme ya da kullanıcı, Grup, cihaz veya parola geri yazma gibi eşitleme seçeneklerini etkinleştirme gibi hello geçerli yapılandırmasını değiştirin. |
| **Hazırlama modunu etkinleştir** |Hemen eşitlenmemiş ve değil aşaması bilgilerini tooAzure AD veya şirket içi Active Directory verildi.  Bu özellik ile ortaya çıkmadan önce hello eşitlemeler önizleyebilirsiniz. |

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).
