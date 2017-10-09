---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jive | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jive arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Öğretici: Jive kullanıcı sağlamak için yapılandırma

Bu öğreticinin Hello hedefi Jive ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooJive tooperform gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir Jive çoklu oturum açma etkin abonelik.
*   Bir kullanıcı hesabında Jive takım yönetici izinlerine sahip.

## <a name="assigning-users-toojive"></a>Kullanıcıların tooJive atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Jive uygulamasına erişmesi hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Jive uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Kullanıcıların tooJive atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooJive tootest hello atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooJive atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-user-provisioning"></a>Kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooJive kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Jive atanan kullanıcı hesaplarında devre dışı bırakın.

> [!TIP]
> SAML tabanlı tek oturum açma için sağlanan hello yönergeleri izleyerek Jive tooenabled tercih edebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline tooJive tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.
Bu yordam bir parçası, gerekli tooprovide toorequest Jive.com gelen gereken kullanıcı güvenlik belirteci olur.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten Jive yapılandırdıysanız, hello arama alanı kullanarak Jive Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Jive** hello uygulama galerisinde. Merhaba Arama sonuçlarından Jive seçin ve uygulamaların tooyour listesine ekleyin.

3. Jive örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
    a. Merhaba, **Jive yönetici kullanıcı adı** metin kutusuna, bir Jive hesap hello sahip adı türü **Sistem Yöneticisi** atanan Jive.com profilinde.
   
    b. Merhaba, **Jive yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.
   
    c. Merhaba, **Jive Kiracı URL** metin kutusuna, türü hello Jive Kiracı URL.
      
      > [!NOTE]
      > Merhaba Jive Kiracı tooJive içinde kuruluş toolog tarafından kullanılan URL'dir.  
      > Genellikle, hello URL biçimi aşağıdaki hello sahiptir: **www.\< Kuruluş\>. jive.com**.          

6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Jive uygulama bağlanabilir.

7. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.

8. Tıklatın **kaydedin.**

9. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooJive.**

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooJive eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Jive içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello Jive, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

12. Tıklatın **kaydedin.**

Herhangi bir kullanıcı ve/veya hello kullanıcılar tooJive ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet Jive uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. TooJive hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-jive-tutorial.md)