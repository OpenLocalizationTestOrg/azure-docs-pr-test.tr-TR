---
title: "Azure Active Directory'de koşullu erişim aaaGet Başlarken | Microsoft Docs"
description: "Koşullu erişim konumu koşulu kullanarak test edin."
services: active-directory
keywords: "koşullu erişim tooapps, Azure AD ile koşullu erişim toocompany kaynaklarına, koşullu erişim ilkeleri güvenli erişim"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Azure Active Directory'de koşullu erişimi kullanmaya başlama

Koşullu erişim, uygulamalarınızı yetkili kullanıcıların erişmek için toodefine koşulları sağlayan Azure Active Directory bir yetenektir. 

Bu konu, ortamınızdaki bir konum koşula göre koşullu bir erişim test etmek için yönergeler sağlar.  


## <a name="scenario-description"></a>Senaryo açıklaması

Birçok kuruluşta ortak gereksinimi olan tooonly hello Kurumsal intranet bağlantısı gerçekleştirilmez erişim tooapps için çok faktörlü kimlik doğrulaması gerektirir. Azure Active Directory ile konum temelli koşullu erişim ilkesini yapılandırarak bu amacı kolayca gerçekleştirebilirsiniz. Bu konu, ilgili ilke yapılandırmaya ilişkin ayrıntılı yönergeler sağlar. Hello İlkesi yararlanır [güvenilen IP'ler](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish hello şirket yapılan erişim denemesi arasındaki kullanıcının intranet ve diğer tüm konumları.


## <a name="prerequisites"></a>Ön koşullar

Merhaba bu konuda açıklanan senaryo, özetlenen hello kavramları hakkında bilgi sahibi olduğunu varsayar [Azure Active Directory koşullu erişim](active-directory-conditional-access-azure-portal.md).

tootest bu senaryo, gerekir:

- Test kullanıcısı oluşturma 

- Bir Azure AD Premium lisansı toohello test kullanıcısı atayın

- Yönetilen bir uygulama yapılandırma ve test kullanıcı tooit atayın

- Güvenilen IP'leri yapılandırmak

Güvenilen IP'ler hakkında daha fazla ayrıntı gerekirse bkz [güvenilen IP'ler](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>İlke yapılandırma adımları

**tooconfigure koşullu erişim ilkenizi yapın:**

1. Merhaba hello sol gezinti çubuğu üzerinde Azure portal'ı tıklatın **Azure Active Directory**. 

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. Merhaba üzerinde **Azure Active Directory** dikey penceresinde hello **Yönet** 'yi tıklatın **koşullu erişim**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. Merhaba üzerinde **koşullu erişim** dikey penceresinde, tooopen hello **yeni** hello araç çubuğunda hello üstte dikey tıklayın **Ekle**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. Merhaba üzerinde **yeni** dikey penceresinde hello **adı** metin kutusuna, ilkeniz için bir ad yazın.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. Merhaba, **atama** 'yi tıklatın **kullanıcılar ve gruplar**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Tıklatın **kullanıcıları ve grupları seçin**.

    b. **Seç**'e tıklayın.

    c. Merhaba üzerinde **seçin** dikey penceresinde, test kullanıcınız seçin ve ardından **seçin**.

    d. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde tıklatın **Bitti**.

7. Merhaba üzerinde **yeni** dikey penceresinde, tooopen hello **bulut uygulamaları** dikey penceresinde hello **atama** 'yi tıklatın **bulut uygulamaları**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. Merhaba üzerinde **bulut uygulamaları** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Tıklatın **uygulamaları**.

    b. **Seç**'e tıklayın.

    c. Merhaba üzerinde **seçin** dikey penceresinde, bulut uygulamanızı seçin ve ardından **seçin**.

    d. Merhaba üzerinde **bulut uygulamaları** dikey penceresinde tıklatın **Bitti**.

9. Merhaba üzerinde **yeni** dikey penceresinde, tooopen hello **koşullar** dikey penceresinde hello **atama** 'yi tıklatın **koşullar**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. Merhaba üzerinde **koşullar** dikey penceresinde, tooopen hello **konumları** dikey penceresinde tıklatın **konumları**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. Merhaba üzerinde **konumları** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. Altında **yapılandırma**, tıklatın **Evet**.

    b. Altında **INCLUDE**, tıklatın **tüm konumları**.

    c. Tıklatın **hariç**ve ardından **tüm güvenilen IP'leri**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. **Bitti**’ye tıklayın.

12. Merhaba üzerinde **koşullar** dikey penceresinde tıklatın **Bitti**.

13. Merhaba üzerinde **yeni** dikey penceresinde, tooopen hello **Grant** dikey penceresinde hello **denetimleri** 'yi tıklatın **Grant**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. Merhaba üzerinde **Grant** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Seçin **çok faktörlü kimlik doğrulaması gerektiren**.

    b. **Seç**'e tıklayın.

15. Merhaba üzerinde **yeni** dikey altında **ilkesini etkinleştir**, tıklatın **üzerinde**.

    ![Koşullu erişim](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. Merhaba üzerinde **yeni** dikey penceresinde tıklatın **oluşturma**.


## <a name="testing-hello-policy"></a>Merhaba ilkeyi test etme

tootest ilkeniz, uygulamanızı bir aygıttan erişim: 

1. İçinde yapılandırılmış güvenilen IP'ler bir IP adresi vardır 

1. Yapılandırılmış güvenilen IP'leri içinde olmayan bir IP adresi var.

Çok faktörlü kimlik doğrulaması yalnızca, yapılandırılmış güvenilen IP'leri içinde değil bir aygıttan yapılan bağlantı girişimi sırasında gerekli olması gerekir. 


## <a name="next-steps"></a>Sonraki adımlar

Toolearn koşullu erişim hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory koşullu erişim](active-directory-conditional-access-azure-portal.md).

