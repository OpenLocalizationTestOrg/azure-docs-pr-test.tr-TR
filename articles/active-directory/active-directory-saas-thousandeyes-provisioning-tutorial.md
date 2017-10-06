---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı ThousandEyes yapılandırma | Microsoft Docs"
description: "Nasıl tooThousandEyes tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a>Öğretici: ThousandEyes otomatik kullanıcı sağlamayı için yapılandırma


Bu öğreticinin Hello hedefi ThousandEyes ve Azure AD tooautomatically sağlama tooperform gerekir ve Azure AD tooThousandEyes kullanıcı hesaplarından sağlanmasını adımları hello tooshow ' dir. 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı
*   Merhaba ThousandEyes kiracıyla [standart planı](https://www.thousandeyes.com/pricing) veya daha iyi etkin 
*   ThousandEyes yönetici izinlerine sahip bir kullanıcı hesabı 

> [!NOTE]
> Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [ThousandEyes SCIM'yi API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), kullanılabilir tooThousandEyes takımlar hello standart plan üzerinde ya da daha iyi olduğu.

## <a name="assigning-users-toothousandeyes"></a>Kullanıcıların tooThousandEyes atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir. 

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour ThousandEyes uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour ThousandEyes uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a>Kullanıcıların tooThousandEyes atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooThousandEyes tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooThousandEyes atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim. Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.


## <a name="configuring-user-provisioning-toothousandeyes"></a>Kullanıcı tooThousandEyes hazırlama yapılandırma 

Bu bölümde, Azure AD tooThousandEyes kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve grup atama göre ThousandEyes atanan kullanıcı hesaplarında devre dışı bırak Azure AD.

> [!TIP]
> Sağlanan hello yönergeleri izleyerek ThousandEyes için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a>Azure AD'de tooThousandEyes sağlama otomatik olarak bir kullanıcı hesabı yapılandırın


1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten ThousandEyes yapılandırdıysanız, hello arama alanı kullanarak ThousandEyes Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **ThousandEyes** hello uygulama galerisinde. Merhaba Arama sonuçlarından ThousandEyes seçin ve uygulamaların tooyour listesine ekleyin.

3. ThousandEyes örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**.

    ![ThousandEyes sağlama](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümü, giriş hello **gizli belirteci** ThousandEyes'ın hesap tarafından oluşturulan (Merhaba belirteci ThousandEyes hesabınızın altında bulabilirsiniz: **güvenlik & Kimlik doğrulama**). 

    ![ThousandEyes sağlama](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour ThousandEyes uygulama bağlanabilir. Merhaba bağlantı başarısız olursa ThousandEyes hesabınız yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.

7. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."

8. **Kaydet** düğmesine tıklayın. 

9. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooThousandEyes**.

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooThousandEyes eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları ThousandEyes içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello ThousandEyes, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

12. **Kaydet** düğmesine tıklayın. 

Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooThousandEyes ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Sonraki adımlar

* [Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın](active-directory-saas-provisioning-reporting.md)
