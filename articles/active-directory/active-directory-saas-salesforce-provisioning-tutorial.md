---
title: "Öğretici: Azure Active Directory Tümleştirme Salesforce ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Öğretici: Salesforce otomatik kullanıcı sağlamayı için yapılandırma

Bu öğreticinin Hello hedefi tooshow hello adımları gerekli tooperform Salesforce ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarında bulunan Azure AD tooSalesforce ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   İş veya eğitim için Salesforce Salesforce için geçerli bir kiracı olması gerekir. Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.
*   Salesforce takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-toosalesforce"></a>Kullanıcıların tooSalesforce atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Salesforce uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Salesforce uygulamasına atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Kullanıcıların tooSalesforce atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooSalesforce tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*  Bir kullanıcı tooSalesforce atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmıyor

    > [!NOTE]
    > Bu uygulamayı Salesforce sağlama işlemi, hangi hello müşteri tooselect kullanıcılar atarken isteyebilirsiniz hello bir parçası olarak özel roller alır

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooSalesforce kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Salesforce atanan kullanıcı hesaplarında devre dışı bırak .

>[!Tip]
>Sağlanan hello yönergeleri izleyerek Salesforce için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline tooSalesforce tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten Salesforce yapılandırdıysanız, hello arama alanı kullanarak Salesforce Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Salesforce** hello uygulama galerisinde. Salesforce hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

3. Salesforce örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 
![sağlama](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
    a. Merhaba, **yönetici kullanıcı adı** metin kutusuna, bir Salesforce hesap hello sahip adı türü **Sistem Yöneticisi** atanan Salesforce.com profilinde.
   
    b. Merhaba, **yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.

6. tooget, Salesforce güvenlik belirtecinizdeki yeni bir sekme açın ve hello aynı oturum Salesforce yönetici hesabı. Merhaba sağ üst köşesinde başlangıç sayfası, adınıza tıklayın ve ardından **My ayarları**.

     ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "otomatik kullanıcı sağlamayı etkinleştirin")
7. Merhaba sol gezinti bölmesinde tıklatın **kişisel** tooexpand hello ilgili bölümü ve ardından **sıfırlama My güvenlik belirteci**.
  
    ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "otomatik kullanıcı sağlamayı etkinleştirin")
8. Merhaba üzerinde **sıfırlama My güvenlik belirteci** sayfasında, **güvenlik belirteci sıfırlama** düğmesi.

    ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "otomatik kullanıcı sağlamayı etkinleştirin")
9. Bu yönetici hesabıyla ilişkili hello e-posta gelen kutusunu kontrol edin. Bir e-postadan hello yeni güvenlik belirteci içeriyor Salesforce.com arayın.
10. Hello belirteci, Git tooyour Azure AD penceresi kopyalama ve hello yapıştırma **yuva belirteci** alan.

11. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Salesforce uygulamasına bağlanabilir.

12. Merhaba, **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve hello aşağıdaki onay hello e-posta adresini girin.

13. Tıklatın **kaydedin.**  
    
14.  Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooSalesforce.**

15. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSalesforce eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Seçilen öznitelikler hello Not **eşleşen** özelliklerdir Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Salesforce içinde güncelleştirme işlemleri için. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

16. tooenable hello Salesforce, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

17. Tıklatın **kaydedin.**

Bu, herhangi bir kullanıcı ve/veya hello kullanıcılar tooSalesforce ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform öncelikli olduğuna dikkat edin. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Salesforce uygulama hizmeti sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. TooSalesforce hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-salesforce-tutorial.md)