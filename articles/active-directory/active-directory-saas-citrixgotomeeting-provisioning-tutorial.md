---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix GoToMeeting | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Citrix GoToMeeting arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Öğretici: Citrix GoToMeeting otomatik kullanıcı sağlamayı için yapılandırma

Bu öğreticinin Hello hedefi Citrix GoToMeeting ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooCitrix GoToMeeting tooperform gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir Citrix GoToMeeting çoklu oturum açma etkin abonelik.
*   Citrix GoToMeeting takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-toocitrix-gotomeeting"></a>Kullanıcıların tooCitrix GoToMeeting atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Citrix GoToMeeting uygulama erişim hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Citrix GoToMeeting uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Kullanıcıların tooCitrix GoToMeeting atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooCitrix GoToMeeting tootest hello atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooCitrix GoToMeeting atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde, API sağlama, Azure AD tooCitrix GoToMeeting'ın kullanıcı hesabı konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve Grup Citrix GoToMeeting hesaplarında göre atanan kullanıcı devre dışı bırak Azure AD'de atama.

> [!TIP]
> Sağlanan hello yönergeleri izleyerek Citrix GoToMeeting için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için Citrix GoToMeeting zaten yapılandırdıysanız Citrix hello arama alanı kullanarak GoToMeeting Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Citrix GoToMeeting** hello uygulama galerisinde. Citrix GoToMeeting hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

3. Citrix GoToMeeting örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama** modu çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. Merhaba yönetici kimlik bilgileri bölümü altında hello aşağıdaki adımları gerçekleştirin:
   
    a. Merhaba, **Citrix GoToMeeting yönetici kullanıcı adı** metin kutusuna, bir yöneticinin türü hello kullanıcı adı.

    b. Merhaba, **Citrix GoToMeeting yönetici parolası** metin kutusuna, hello yöneticinin parola.

6. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Citrix GoToMeeting uygulama bağlanabilir. Merhaba bağlantı başarısız olursa, Citrix GoToMeeting hesabınızın Team yönetici izinleri olduğundan emin olun ve hello deneyin **"Yönetici kimlik bilgileri"** adım yeniden uygulayın.

7. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

8. Tıklatın **kaydedin.**

9. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooCitrix GoToMeeting.**

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooCitrix GoToMeeting eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Citrix GoToMeeting içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

11. tooenable hello Citrix GoToMeeting, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

12. Tıklatın **kaydedin.**

Tüm kullanıcıların hello ilk eşitleme başlar ve/veya gruplarının tooCitrix GoToMeeting hello kullanıcılar ve Gruplar bölümünde atanmış. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Citrix GoToMeeting uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-citrix-gotomeeting-tutorial.md)


