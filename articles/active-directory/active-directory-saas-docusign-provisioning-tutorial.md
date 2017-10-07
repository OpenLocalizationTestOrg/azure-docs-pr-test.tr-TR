---
title: "Öğretici: Azure Active Directory Tümleştirme ile DocuSign | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile DocuSign arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a>Öğretici: DocuSign kullanıcı sağlamak için yapılandırma

Bu öğreticinin Hello hedefi DocuSign ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooDocuSign tooperform gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir DocuSign çoklu oturum açma abonelik etkin.
*   Bir kullanıcı hesabında DocuSign takım yönetici izinlerine sahip.

## <a name="assigning-users-toodocusign"></a>Kullanıcıların tooDocuSign atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour DocuSign uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour DocuSign uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a>Kullanıcıların tooDocuSign atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooDocuSign tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooDocuSign atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-user-provisioning"></a>Kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooDocuSign kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre DocuSign atanan kullanıcı hesaplarında devre dışı bırakın.

> [!Tip]
> Sağlanan hello yönergeleri izleyerek DocuSign için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline tooDocuSign tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten DocuSign yapılandırdıysanız, hello arama alanı kullanarak DocuSign Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **DocuSign** hello uygulama galerisinde. Merhaba Arama sonuçlarından DocuSign seçin ve uygulamaların tooyour listesine ekleyin.

3. DocuSign örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
    a. Merhaba, **yönetici kullanıcı adı** metin kutusuna, bir DocuSign hesap hello sahip adı türü **Sistem Yöneticisi** atanan DocuSign.com profilinde.
   
    b. Merhaba, **yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.

6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour DocuSign uygulama bağlanabilir.

7. Merhaba, **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve hello onay hello e-posta adresini girin.

8. Tıklatın **kaydedin.**

9. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooDocuSign.**

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooDocuSign eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları DocuSign içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello DocuSign, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

12. Tıklatın **kaydedin.**

Herhangi bir kullanıcı ve/veya hello kullanıcılar tooDocuSign ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet DocuSign uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. TooDocuSign hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-docusign-tutorial.md)