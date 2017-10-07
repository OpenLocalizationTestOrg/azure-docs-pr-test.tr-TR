---
title: "Öğretici: İş için Dropbox Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve iş için Dropbox arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Öğretici: Otomatik kullanıcı sağlamak için Dropbox iş için yapılandırma

Bu öğretici Hello amacı, Dropbox tooperform iş ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooDropbox için iş için gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir Dropbox iş çoklu oturum açma etkin abonelik için.
*   İş için Dropbox takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-toodropbox-for-business"></a>İş için kullanıcıların tooDropbox atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Dropbox iş uygulama için erişim hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek iş uygulama bu kullanıcıların tooyour Dropbox atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>İş için kullanıcıların tooDropbox atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama iş tootest hello tooDropbox atanır. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   İş için bir kullanıcı tooDropbox atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz...

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooDropbox API sağlama işletmenin kullanıcı hesabı için bağlanma yoluyla sırasında size kılavuzluk eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve Grup bağlı iş için Dropbox atanan kullanıcı hesaplarında devre dışı bırak Azure AD'de atama.

>[!Tip]
>Dropbox sağlanan hello yönergeleri izleyerek, iş için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:

1. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2. Çoklu oturum açma için zaten Dropbox iş için yapılandırdıysanız, Dropbox hello arama alanı kullanarak iş için örneğiniz arayın. Aksi takdirde seçin **Ekle** arayın ve **iş için Dropbox** hello uygulama galerisinde. İş için Dropbox hello Arama sonuçlarından seçin ve uygulamaların tooyour listesi ekleyin.

3. İş için Dropbox örneğiniz seçin, sonra seçin hello **sağlama** sekmesi.

4. Set hello **sağlama modu** çok**otomatik**. 

    ![Sağlama](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**. Bir Dropbox iş oturum açma iletişim için yeni bir tarayıcı penceresinde açar.

6. Merhaba üzerinde **oturum açma tooDropbox toolink Azure AD ile** iletişim kutusunda, oturum açma tooyour Dropbox iş Kiracı için.

     ![Kullanıcı sağlamayı](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "kullanıcı hazırlama")

7. İş Kiracı için toogive Azure Active Directory izni toomake değişiklikleri tooyour Dropbox istediğiniz onaylayın. Tıklatın **izin**.
    
      ![Kullanıcı sağlamayı](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "kullanıcı hazırlama")

8. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD iş uygulaması için Dropbox tooyour bağlanabilir. Merhaba bağlantı başarısız olursa, iş hesabı Team yönetici izinleri olan için Dropbox emin olun ve hello deneyin **"Yetkilendir"** adım yeniden uygulayın.

9. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

10. Tıklatın **kaydedin.**

11. Hello eşlemeleri bölümü altında seçin **iş için Azure Active Directory Kullanıcıları Eşitle tooDropbox.**

12. Merhaba, **öznitelik eşlemelerini** bölümü, işletmeniz için Azure AD tooDropbox eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları, iş için Dropbox güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

13. tooenable hello Azure AD sağlama hizmeti iş, değişiklik hello için dropbox **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

14. Tıklatın **kaydedin.**

Herhangi bir kullanıcı ve/veya hello kullanıcılar, iş için tooDropbox ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve, Dropbox bir hizmette iş uygulaması sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Şimdi sınama hesabı oluşturabilirsiniz. İçin iş için tooDropbox hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

Başarıyla tamamlanan kullanıcı döngüsü hazırlama ilgili durumuna göre belirtilir.

![Kullanıcılar atama](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "kullanıcı atama")


## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-dropboxforbusiness-tutorial.md)