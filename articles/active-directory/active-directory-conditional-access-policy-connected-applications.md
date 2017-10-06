---
title: "aaaConfigure Azure Active Directory cihaz temelli koşullu erişim ilkeleri | Microsoft Docs"
description: "Nasıl tooconfigure Azure Active Directory cihaz temelli koşullu erişim ilkeleri hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Azure Active Directory cihaz temelli koşullu erişim ilkelerini yapılandırma

İle [Azure Active Directory (Azure AD) koşullu erişim](active-directory-conditional-access-azure-portal.md), ince ayar yapabilirsiniz nasıl yetkili kullanıcılar, kaynaklara erişebilir. Örneğin, hello erişim toocertain kaynakları tootrusted aygıtları sınırlayın. Güvenilir bir aygıt gerektiren bir koşullu erişim ilkesi cihaz temelli koşullu erişim ilkesi de denir.

Bu konu, nasıl tooconfigure cihaz temelli koşullu erişim ilkeleri Azure AD bağlı uygulamalar için bilgi sağlar. 


## <a name="before-you-begin"></a>Başlamadan önce

Cihaz temelli koşullu erişim TIES **Azure AD koşullu erişimi** ve **Azure AD cihaz Yönetimi birlikte**. Bu alanlardan biri ile tanıdık değilse, aşağıdaki konularda, ilk hello şöyle olmalıdır:

- **[Azure Active Directory'de koşullu erişim](active-directory-conditional-access-azure-portal.md)**  -Bu konu, koşullu kavramsal genel bakış ile erişmek ve hello ilgili terminolojiyi sağlar.

- **[Giriş toodevice Yönetimi Azure Active Directory'de](device-management-introduction.md)**  -Bu konu genel bir fikir veren Merhaba Azure AD ile tooconnect aygıtları sahip çeşitli seçenekleri. 


## <a name="trusted-devices"></a>Güvenilen cihazlar

Bir mobil ilk olarak, bulut ilk dünyasında, Azure Active Directory oturum açma tek toodevices, uygulama ve hizmetlere her yerden sağlar. Belirli toohello doğru kullanıcılar erişim verilmesi, ortamınızdaki kaynakları iyi yeterli olmayabilir. Ayrıca toohello doğru kullanıcılar, aynı zamanda güvenilir cihaz toobe tooaccess kaynak kullanılan gerektirebilir. Ortamınızda, güvenilir bir aygıt, dayanır tanımlayabilirsiniz hello bileşenleri:

- Merhaba [cihaz platformları](active-directory-conditional-access-azure-portal.md#device-platforms) bir cihazda
- Bir cihazın uyumlu olup
- Bir cihaz etki alanına katılmış olup olmadığı 

Merhaba [cihaz platformları](active-directory-conditional-access-azure-portal.md#device-platforms) , cihazda çalışan hello işletim sistemi tarafından belirlenir. Cihaz temelli koşullu erişim ilkenizi erişim toocertain kaynakları toospecific cihaz platformları sınırlayabilirsiniz.



Bir cihaz temelli koşullu erişim ilkesinde uyumlu olarak işaretlenmiş güvenilen cihazlar toobe gerektirebilir.

![Bulut uygulamaları](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Cihazların Merhaba dizininde tarafından uyumlu olarak işaretlenebilir:

- Intune 
- Azure AD ile tümleşen bir üçüncü taraf mobil cihaz yönetim sistemi  

Bağlı tooAzure AD yalnızca cihazlar uyumlu olarak işaretlenebilir. tooconnect aygıt tooAzure Active Directory, aşağıdaki seçenekleri şu hello vardır: 

- Azure AD kayıtlı
- Azure AD alanına katılmış
- Karma Azure AD alanına katılmış

    ![Bulut uygulamaları](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Bir şirket içi Active Directory (AD) ayak izini varsa, bağlı tooAzure AD ancak birleştirilmiş tooyour AD toobe güvenilir olmayan cihazları düşünebilirsiniz.

![Bulut uygulamaları](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Sonraki adımlar

Ortamınızda bir cihaz temelli koşullu erişim ilkesini yapılandırmadan önce hello bir göz atalım [Azure Active Directory'de koşullu erişim için en iyi uygulamaları](active-directory-conditional-access-best-practices.md).

