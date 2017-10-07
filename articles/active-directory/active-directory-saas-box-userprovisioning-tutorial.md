---
title: "Öğretici: Azure Active Directory Tümleştirme kutusuyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin kutusunu ve Azure Active Directory arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Öğretici: Kutusunu otomatik kullanıcı sağlamayı için yapılandırma

Bu öğreticinin Hello hedefi kutusunu ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooBox tooperform gereken tooshow hello adımları ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir kutusunu çoklu oturum açma etkin abonelik.
*   Takım yönetici izinlerine sahip bir kullanıcı hesabı kutusunda.

## <a name="assigning-users-toobox"></a>Kullanıcıların tooBox atama 

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour kutusunu uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Box uygulamasına atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Kullanıcılar ve gruplar atayın
Merhaba **kutusunu > Kullanıcılar ve gruplar** hello Azure portal sekmesinde hangi kullanıcıların ve grupların verilmesi erişim tooBox toospecify sağlar. Bir kullanıcı veya grup ataması şeyler toooccur aşağıdaki hello neden olur:

* Azure AD hello atanan kullanıcı (da doğrudan atama veya grup üyeliği) tooauthenticate tooBox izin verir. Bir kullanıcı atanmamışsa, Azure AD bunları toosign tooBox içinde izin vermez ve hello Azure AD oturum açma sayfasında bir hata döndürür.
* Bir uygulama bölme kutusu için toohello kullanıcının eklenir [uygulama Başlatıcısı](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Otomatik sağlama etkinleştirildiğinde otomatik olarak sağlanan sıra toobe sağlama toohello hello atanan kullanıcılar ve/veya grupları eklenir.
  
  * Yalnızca kullanıcı nesneleri sağlanan yapılandırılmış toobe bundan sonra tüm doğrudan atanan kullanıcılar hello sağlama kuyruğuna yerleştirilir ve hiçbir atanan gruplarının üyeleri olan tüm kullanıcıları sıra sağlama hello yerleştirilir. 
  * Grup nesneleri sağlanan yapılandırılmış toobe olsaydı, tüm atanmış olan Grup nesneleri sağlanan tooBox ve bu grupların üyeleri olan tüm kullanıcılar ' dir. Merhaba grup ve kullanıcı üyeliklerini tooBox üzerine yazılan korunur.

Merhaba kullanabilirsiniz **öznitelikleri > çoklu oturum açma** hangi kullanıcı öznitelikleri (veya talep) sunulur tooBox SAML tabanlı kimlik doğrulaması ve hello sırasında tooconfigure sekmesinde **öznitelikleri > sağlama** Kullanıcı ve grup öznitelikleri işlemleri sağlama sırasında Azure AD tooBox nasıl gerçekleştiğini tooconfigure sekmesi.

### <a name="important-tips-for-assigning-users-toobox"></a>Kullanıcıların tooBox atamak için önemli ipuçları 

*   Önerilir tek bir Azure AD kullanıcı tarafından atanan tooBox tootest hello yapılandırma sağlama. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı toobox atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde Azure AD tooBox kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve atanan kullanıcı hesapları Azure AD'de kullanıcı ve grup atama göre kutusundaki devre dışı bırak.

Otomatik sağlama etkinleştirildiğinde otomatik olarak sağlanan sıra toobe sağlama toohello hello atanan kullanıcılar ve/veya grupları eklenir.
    
 * Yalnızca, doğrudan atanan kullanıcılar hello sağlama kuyruğuna yerleştirilir ve hiçbir atanan gruplarının üyeleri olan tüm kullanıcıları sıra sağlama hello yerleştirilir sağlanan yapılandırılmış toobe kullanıcı nesneleridir. 
    
 * Grup nesneleri sağlanan yapılandırılmış toobe olsaydı, tüm atanmış olan Grup nesneleri sağlanan tooBox ve bu grupların üyeleri olan tüm kullanıcılar ' dir. Merhaba grup ve kullanıcı üyeliklerini tooBox üzerine yazılan korunur.

> [!TIP] 
> SAML tabanlı çoklu oturum açma sağlanan hello yönergeleri izleyerek kutusunu tooenabled tercih edebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı sağlama tooBox hesapları.

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için kutusu zaten yapılandırdıysanız hello arama alanı kullanarak kutusunu Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **kutusunu** hello uygulama galerisinde. Hello Arama sonuçlarından kutusunu seçin ve uygulamaların tooyour listesine ekleyin.

3. Örneğiniz kutusunu seçin ve ardından hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize** tooopen bir kutusunun oturum açma iletişim kutusunda yeni bir tarayıcı penceresi.

6. Merhaba üzerinde **oturum açma toogrant erişim tooBox** sayfasında, gerekli hello kimlik bilgilerini sağlayın ve ardından **Authorize**. 
   
    ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "otomatik kullanıcı sağlamayı etkinleştirin")

7. Tıklatın **Grant erişim tooBox** tooauthorize bu işlemi ve tooreturn toohello Azure portalı. 
   
    ![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "otomatik kullanıcı sağlamayı etkinleştirin")

8. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Box uygulamasına bağlanabilir. Merhaba bağlantı başarısız olursa kutusunu hesabınızın Team yönetici izinlerine sahip olduğundan emin olun ve hello deneyin **"Yetkilendir"** adım yeniden uygulayın.

9. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

10. Tıklatın **kaydedin.**

11. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooBox.**

12. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooBox eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları kutusunda güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

13. tooenable hello Azure AD sağlama hizmeti kutusunu değişiklik hello **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

14. Tıklatın **kaydedin.**

Herhangi bir kullanıcı ve/veya hello kullanıcılar tooBox ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet kutusunu uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. Toobox hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

Altında listelenen kutusunu kiracınızda eşitlenmiş kullanıcıları **yönetilen kullanıcılara** hello içinde **Yönetici Konsolu**.

![Tümleştirme durumu](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "tümleştirme durumu")


## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-box-tutorial.md)