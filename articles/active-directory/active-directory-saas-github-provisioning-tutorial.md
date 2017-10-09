---
title: "Öğretici: Azure Active Directory ile otomatik olarak bir kullanıcı sağlamak için GitHub yapılandırma | Microsoft Docs"
description: "Nasıl tooGitHub tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Öğretici: Otomatik kullanıcı sağlamak için GitHub yapılandırma


Bu öğreticinin Hello hedefi GitHub ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooGitHub tooperform gereken adımları hello tooshow ' dir. 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı
*   Merhaba Github kiracıyla [iş planı](https://help.github.com/articles/organization-billing-plans/#business-plan) veya daha iyi etkin 
*   GitHub yönetici izinlerine sahip bir kullanıcı hesabı 

> [!NOTE]
> Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [GitHub SCIM'yi API](https://developer.github.com/v3/scim/), kullanılabilir tooGithub takımlar hello iş planı veya daha iyi olduğu.

## <a name="assigning-users-toogithub"></a>Kullanıcıların tooGitHub atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir. 

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour GitHub uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour GitHub uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Kullanıcıların tooGitHub atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooGitHub tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooGitHub atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim. Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.


## <a name="configuring-user-provisioning-toogithub"></a>Kullanıcı tooGitHub hazırlama yapılandırma 

Bu bölümde, Azure AD tooGitHub kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre github'da atanan kullanıcı hesapları devre dışı bırak.

> [!TIP]
> Sağlanan hello yönergeleri izleyerek GitHub için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Azure AD'de tooGitHub sağlama otomatik olarak bir kullanıcı hesabı yapılandırın


1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için GitHub zaten yapılandırdıysanız hello arama alanı kullanarak GitHub Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **GitHub** hello uygulama galerisinde. GitHub hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

3. GitHub örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**.

    ![GitHub sağlama](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**. Bu işlem, yeni bir tarayıcı penceresinde bir GitHub yetkilendirme iletişim kutusunu açar. 

6. Merhaba yeni pencerede GitHub yönetici hesabınızı kullanarak oturum açın. Hello elde edilen yetkilendirme iletişim kutusunda, tooenable sağlamayı istiyor ve ardından hello GitHub ekibi seçin **Authorize**. Bir kez tamamlanan, dönüş toohello Azure portal toocomplete hello yapılandırma sağlama.

    ![Yetkilendirme iletişim](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. Hello Azure portal, giriş **Kiracı URL** tıklatıp **Bağlantıyı Sına** tooensure Azure AD tooyour GitHub uygulama bağlanabilir. Merhaba bağlantı başarısız olursa, GitHub hesabınızda yönetici izinleri olduğundan emin olun ve **Kiracı URl** doğru girilen sonra hello "Yetkilendir" adımı yeniden deneyin (size oluşturabilecek **Kiracı URL** kuralı tarafından: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", kuruluşlar, GitHub hesabınızda altında bulabilirsiniz: **ayarları** > **kuruluşların**).

    ![Yetkilendirme iletişim](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."

9. **Kaydet** düğmesine tıklayın. 

10. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooGitHub**.

11. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooGitHub eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları github'da güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

12. tooenable hello GitHub, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

13. **Kaydet** düğmesine tıklayın. 

Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooGitHub ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Sonraki adımlar

* [Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın](active-directory-saas-provisioning-reporting.md)
