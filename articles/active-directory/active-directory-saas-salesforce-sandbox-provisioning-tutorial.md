---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce korumalı alan arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Öğretici: Salesforce korumalı alan otomatik kullanıcı sağlamayı için yapılandırma

Bu öğreticinin Hello hedefi Salesforce korumalı alan ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooSalesforce korumalı alan tooperform gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Salesforce korumalı alan için iş veya eğitim için Salesforce korumalı alan için geçerli bir kiracı olması gerekir. Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.
*   Salesforce korumalı alan takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-toosalesforce-sandbox"></a>Kullanıcıların tooSalesforce korumalı alan atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Salesforce korumalı alan uygulama erişim hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Salesforce korumalı alan uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Kullanıcıların tooSalesforce korumalı alan atamak için önemli ipuçları

* Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooSalesforce korumalı alan tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

* Bir kullanıcı tooSalesforce Sandbox atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

> [!NOTE]
> Bu uygulama özel roller Salesforce korumalı sağlama işlemi, hangi hello müşteri tooselect kullanıcılar atarken isteyebilirsiniz hello bir parçası olarak alır.

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde, API sağlama, Azure AD tooSalesforce korumalı alanın kullanıcı hesabı konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve atanan kullanıcı hesapları Salesforce korumalı alanı içinde kullanıcı ve grup tabanlı devre dışı bırak Azure AD'de atama.

>[!Tip]
>Sağlanan hello yönergeleri izleyerek Salesforce korumalı alan için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı kullanıcı sağlamayı tooSalesforce korumalı alan hesapları.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için Salesforce korumalı alan zaten yapılandırdıysanız Salesforce korumalı alan hello arama alanı kullanarak Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Salesforce korumalı alan** hello uygulama galerisinde. Salesforce korumalı alan hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

3. Salesforce korumalı alan örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 
    ![sağlama](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
    a. Merhaba, **yönetici kullanıcı adı** metin kutusuna, Salesforce korumalı alan hesap hello sahip adı türü **Sistem Yöneticisi** atanan Salesforce.com profilinde.
   
    b. Merhaba, **yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.

6. tooget, Salesforce korumalı alan güvenlik belirtecinizdeki yeni bir sekme açın ve hello aynı oturum Salesforce korumalı alan yönetici hesabı. Merhaba sağ üst köşesinde başlangıç sayfası, adınıza tıklayın ve ardından **My ayarları**.

     ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "otomatik kullanıcı sağlamayı etkinleştirin")
7. Merhaba sol gezinti bölmesinde tıklatın **kişisel** tooexpand hello ilgili bölümü ve ardından **sıfırlama My güvenlik belirteci**.
  
    ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "otomatik kullanıcı sağlamayı etkinleştirin")
8. Merhaba üzerinde **sıfırlama My güvenlik belirteci** hello sayfasında, **güvenlik belirteci sıfırlama** düğmesi.

    ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "otomatik kullanıcı sağlamayı etkinleştirin")
9. Bu yönetici hesabıyla ilişkili hello e-posta gelen kutusunu kontrol edin. Bir e-postadan hello yeni güvenlik belirteci içeriyor Salesforce Sandbox.com arayın.
10. Hello belirteci, Git tooyour Azure AD penceresi kopyalama ve hello yapıştırma **yuva belirteci** alan.

11. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Salesforce korumalı alan uygulama bağlanabilir.

12. Merhaba, **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve hello onay hello e-posta adresini girin.

13. Tıklatın **kaydedin.**  
    
14.  Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooSalesforce korumalı alan.**

15. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSalesforce korumalı alan eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Salesforce korumalı alanı içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

16. tooenable hello Salesforce korumalı alan, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

17. Tıklatın **kaydedin.**


Tüm kullanıcıların hello ilk eşitleme başlar ve/veya gruplarının tooSalesforce hello kullanıcılar ve Gruplar bölümünde Sandbox atanmış. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Salesforce korumalı alan uygulama hizmeti sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. Toosalesforce hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-salesforcesandbox-tutorial.md)