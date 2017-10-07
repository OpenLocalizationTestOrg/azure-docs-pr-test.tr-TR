---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Facebook ile çalışma alanına arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Öğretici: Kullanıcı sağlamak için çalışma alanına Facebook ile yapılandırma

Bu öğreticinin Hello hedefi çalışma tooperform Facebook ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooWorkplace Facebook tarafından tarafından gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Facebook çoklu oturum açma etkin abonelik tarafından bir çalışma alanı

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Kullanıcıların tooWorkplace Facebook tarafından atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour çalışma alanına Facebook uygulaması tarafından erişim hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour çalışma alanına Facebook uygulaması tarafından atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Kullanıcıların tooWorkplace Facebook tarafından atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının tooWorkplace yapılandırma sağlama Facebook tootest hello tarafından atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooWorkplace Facebook tarafından atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-user-provisioning"></a>Kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooWorkplace Facebook'ın kullanıcı hesabı tarafından API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve çalışma Facebook kullanıcı ve Grup göre tarafından atanan kullanıcı hesapları devre dışı bırak Azure AD'de atama.

>[!Tip]
>İş yeri tarafından sağlanan hello yönergeleri izleyerek Facebook için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Azure AD'de tooWorkplace Facebook tarafından sağlama tooconfigure kullanıcı hesabı:

Bu bölümde Hello amacı olan toooutline tooWorkplace Facebook tarafından Active Directory kullanıcısı tooenable sağlama nasıl hesapları.

Azure AD destekler Hello özelliği tooautomatically hello hesap ayrıntılarını eşitlemek kullanıcılar tooWorkplace Facebook tarafından atanır. Facebook tooget hello verileri, gereken tooauthorize kullanıcılar, erişimi için önce tarafından çalışma alanına bu otomatik eşitlenmesine olanak bunları içinde toosign hello için ilk kez çalışılıyor. Erişim Azure AD'de iptal edilmiş durumda olduğunda, ayrıca çalışma alanına Facebook tarafından kullanıcılardan XML'deki sağlamasını yapar.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory** > **Kurumsal uygulamaları** > **tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten çalışma alanına Facebook tarafından yapılandırdıysanız, çalışma alanına hello arama alanı kullanarak Facebook tarafından örneğiniz arayın. Aksi takdirde seçin **Ekle** arayın ve **Facebook ile çalışma alanına** hello uygulama galerisinde. Merhaba Arama sonuçlarından Facebook tarafından çalışma alanı seçin ve uygulamaların tooyour listesine ekleyin.

3. Facebook ile çalışma alanına örneğiniz seçin, sonra seçin hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** bölümünde hello gizli belirteci girin ve Kiracı URL'si işyeriniz Facebook yönetici tarafından hello.

6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD, Facebook uygulaması tarafından tooyour çalışma alanına bağlanabilir. Merhaba bağlantı başarısız olursa işyeriniz Facebook hesabına göre takım yönetici izinleri olduğundan emin olun.

7. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

8. Tıklatın **kaydedin.**

9. Hello eşlemeleri bölümü altında seçin **Facebook tarafından Azure Active Directory Kullanıcıları Eşitle tooWorkplace.**

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooWorkplace Facebook tarafından eşitlenen hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları çalışma Facebook tarafından güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello Facebook, değişiklik hello tarafından çalışma alanı için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

12. Tıklatın **kaydedin.**

Hakkında daha fazla bilgi için hazırlama, otomatik tooconfigure bkz [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Şimdi sınama hesabı oluşturabilirsiniz. İçin Facebook tarafından tooWorkplace hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-workplacebyfacebook-tutorial.md)

