---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı ZenDesk yapılandırma | Microsoft Docs"
description: "Nasıl tooZenDesk tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a>Öğretici: ZenDesk otomatik kullanıcı sağlamayı için yapılandırma


Bu öğreticinin Hello hedefi ZenDesk ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooZenDesk tooperform gereken adımları hello tooshow ' dir. 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı
*   ZenDesk Kiracı hello ile [Kurumsal planı](https://www.zendesk.com/product/pricing/) veya daha iyi etkin 
*   ZenDesk yönetici izinlerine sahip bir kullanıcı hesabı 

> [!NOTE]
> Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), kullanılabilir tooZenDesk takımlar hello temel plan üzerinde ya da daha iyi olduğu.

## <a name="assigning-users-toozendesk"></a>Kullanıcıların tooZenDesk atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir. 

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour ZenDesk uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour ZenDesk uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a>Kullanıcıların tooZenDesk atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooZenDesk tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooZenDesk atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim. Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.

> [!NOTE]
> Eklenen bir özellik olarak hizmet sağlama hello Zendesk içinde tanımlanan herhangi bir özel rolü okur ve bunları Azure AD hello rolü Seç iletişim kutusunda bunlar burada seçilebilir aktarır. Bu rolleri hizmet sağlama hello etkinleştirilir ve bir eşitleme döngüsü tamamlandıktan sonra hello Azure portalında görünür.

## <a name="configuring-user-provisioning-toozendesk"></a>Kullanıcı tooZenDesk hazırlama yapılandırma 

Bu bölümde, Azure AD tooZenDesk kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre ZenDesk atanan kullanıcı hesaplarında devre dışı bırakın.

> [!TIP] 
> Sağlanan hello yönergeleri izleyerek ZenDesk için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a>Azure AD'de tooZenDesk sağlama otomatik olarak bir kullanıcı hesabı yapılandırın


1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten ZenDesk yapılandırdıysanız, hello arama alanı kullanarak ZenDesk Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **ZenDesk** hello uygulama galerisinde. ZenDesk hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

3. ZenDesk örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**.

    ![ZenDesk sağlama](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümü, giriş hello **yönetici kullanıcı adı, tokenkey & etki alanı** ZenDesk'ın hesap tarafından oluşturulan (Merhaba belirteci hesabınızın altında bulabilirsiniz: **yönetici**   >  **API** > **ayarları**). 

    ![ZenDesk sağlama](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour ZenDesk uygulama bağlanabilir. Merhaba bağlantı başarısız olursa ZenDesk hesabınıza yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.

7. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."

8. **Kaydet** düğmesine tıklayın. 

9. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooZenDesk**.

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooZenDesk eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları ZenDesk içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello ZenDesk, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

12. **Kaydet** düğmesine tıklayın. 

Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooZenDesk ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Sonraki adımlar

* [Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın](active-directory-saas-provisioning-reporting.md)
