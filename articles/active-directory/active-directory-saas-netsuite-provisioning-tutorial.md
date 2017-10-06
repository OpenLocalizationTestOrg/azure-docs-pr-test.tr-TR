---
title: "Öğretici: Azure Active Directory Tümleştirme ile Netsuite | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Netsuite arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Öğretici: Netsuite otomatik kullanıcı sağlamayı için yapılandırma

Bu öğreticinin Hello hedefi Netsuite ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooNetsuite tooperform gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir Netsuite çoklu oturum açma etkin abonelik.
*   Bir kullanıcı hesabında Netsuite takım yönetici izinlerine sahip.

## <a name="assigning-users-toonetsuite"></a>Kullanıcıların tooNetsuite atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Netsuite uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Netsuite uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Kullanıcıların tooNetsuite atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooNetsuite tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooNetsuite atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-user-provisioning"></a>Kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooNetsuite kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Netsuite atanan kullanıcı hesaplarında devre dışı bırakın.

> [!TIP] 
> Sağlanan hello yönergeleri izleyerek Netsuite için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline tooNetsuite tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten Netsuite yapılandırdıysanız, hello arama alanı kullanarak Netsuite Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Netsuite** hello uygulama galerisinde. Merhaba Arama sonuçlarından Netsuite seçin ve uygulamaların tooyour listesine ekleyin.

3. Netsuite örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
    a. Merhaba, **yönetici kullanıcı adı** metin kutusuna, bir Netsuite hesap hello sahip adı türü **Sistem Yöneticisi** atanan Netsuite.com profilinde.
   
    b. Merhaba, **yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.
      
6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Netsuite uygulama bağlanabilir.

7. Merhaba, **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve hello onay hello e-posta adresini girin.

8. Tıklatın **kaydedin.**

9. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooNetsuite.**

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooNetsuite eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Seçilen öznitelikler hello Not **eşleşen** özelliklerdir Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Netsuite içinde güncelleştirme işlemleri için. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello Netsuite, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

12. Tıklatın **kaydedin.**

Herhangi bir kullanıcı ve/veya hello kullanıcılar tooNetsuite ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform öncelikli olduğuna dikkat edin. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet Netsuite uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. TooNetsuite hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-netsuite-tutorial.md)