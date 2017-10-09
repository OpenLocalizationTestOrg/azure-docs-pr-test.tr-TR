---
title: "Öğretici: Azure otomatik kullanıcı sağlamayı Google uygulamaları yapılandırma | Microsoft Docs"
description: "Azure AD tooGoogle uygulamaları ' nasıl tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Öğretici: Otomatik kullanıcı sağlamayı için Google uygulamaları yapılandırma

Bu öğreticinin Hello hedefi Google Apps ve Azure AD tooautomatically sağlama tooperform gerekir ve Azure AD tooGoogle uygulamalar kullanıcı hesaplarından sağlanmasını adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   İş veya eğitim için Google Apps için Google Apps için geçerli bir kiracı olması gerekir. Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.
*   Google Apps takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-toogoogle-apps"></a>Kullanıcıları tooGoogle uygulamalar atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Google Apps uygulamasına erişmesi hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Google Apps uygulama atayabilirsiniz: [bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooGoogle uygulamaları tootest hello atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.
>*   Bir kullanıcı tooGoogle uygulamaları atarken hello atama iletişim kutusunda hello kullanıcı ya da "Grup" rolünü seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooGoogle uygulamalarınızı'nın kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Google Apps Azure AD'de kullanıcı ve grup atama göre atanan kullanıcı hesaplarında devre dışı bırak .

>[!Tip]
>Sağlanan hello yönergeleri izleyerek Google Apps için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="configure-automatic-user-account-provisioning"></a>Hesap otomatik kullanıcı sağlamayı Yapılandır

> [!NOTE]
> Kullanıcı tooGoogle uygulamaları hazırlama otomatikleştirmek için başka bir uygun toouse seçenektir [Google Apps dizin eşitleme (GADS)](https://support.google.com/a/answer/106368?hl=en) , şirket içi Active Directory kimlikleri tooGoogle uygulamaları sağlar. Buna karşılık, hello çözümü Bu öğreticide, Azure Active Directory (bulut) kullanıcıları ve posta özellikli gruplar tooGoogle uygulamaları sağlamasını yapar. 

1. Merhaba içine oturum [Google Apps Yönetici Konsolu](http://admin.google.com/) yönetici hesabı kullanarak ve tıklayın **güvenlik**. Merhaba bağlantısını görmüyorsanız, hello altında gizli olabilir **daha fazla denetim** hello ekranın hello menüsünde.
   
    ![Güvenlik'e tıklayın.][10]

2. Merhaba üzerinde **güvenlik** sayfasında, **API Başvurusu**.
   
    ![API Başvurusu'ı tıklatın.][15]

3. Seçin **etkinleştirmek API erişimini**.
   
    ![API Başvurusu'ı tıklatın.][16]

    > [!IMPORTANT]
    > Tooprovision tooGoogle uygulamaları, Azure Active Directory'de kullanıcı adlarını düşündüğünüz her kullanıcı için *gerekir* bağlı tooa özel etki alanı olması. Örneğin, neye benzediğini gösteren kullanıcı adları bob@contoso.onmicrosoft.com ancak Google Apps tarafından kabul edilmiyor bob@contoso.com kabul edilir. Mevcut bir kullanıcının etki alanı Azure AD'de özelliklerini düzenleyerek değiştirebilirsiniz. Yönergeler nasıl tooset Azure Active Directory ve Google Apps için özel bir etki alanı dahil edilmiştir için adımları izleyin.
      
4. Özel etki alanı adı tooyour Azure Active Directory henüz eklemediyseniz, hello aşağıdaki adımları izleyin:
  
    a. Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. Merhaba dizin listesinde dizininizi seçin. 

    b. Tıklatın **etki alanı adı** üzerinde sol gezinti bölmesinde hello ve ardından **Ekle**.
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![etki alanı ekleme](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Etki alanı adınızı hello yazın **etki alanı adı** alan. Bu etki alanı adı hello olmalıdır Google Apps için toouse düşündüğünüz aynı etki alanı adı. Hazır olduğunuzda hello tıklatın **etki alanı Ekle** düğmesi.
     
     ![Etki alanı adı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Tıklatın **sonraki** toogo toohello doğrulama sayfasında. Bu etki alanı kendi tooverify, bu sayfada sağlanan toohello değerleri göre hello etki alanının DNS kayıtlarını düzenlemeniz gerekir. Kullanarak tooverify seçebilirsiniz **MX kayıtları** veya **TXT kayıtlarının**Merhaba seçin bağlı olarak **kayıt türü** seçeneği. Nasıl tooverify etki alanı adı Azure AD ile daha kapsamlı yönergeler için bkz [kendi etki alanı adı tooAzure AD eklemek](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Merhaba önceki adımları tooadd tooyour directory düşündüğünüz tüm hello etki alanları için yineleyin.

5. Azure AD ile etki alanları doğruladıktan, artık bunları yeniden Google Apps ile doğrulamanız gerekiyor. Google Apps ile zaten kayıtlı değil her etki alanı için hello aşağıdaki adımları gerçekleştirin:
   
    a. Merhaba, [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **etki alanları**.
     
     ![Etki alanlarında tıklatın][20]

    b. Tıklatın **bir etki alanı veya bir etki alanı diğer adı eklemek**.
     
     ![Yeni bir etki alanı Ekle][21]

    c. Seçin **başka bir etki alanı ekleme**, tooadd istediğiniz hello etki alanının hello adı yazın.
     
     ![Etki alanı adınızı yazın][22]

    d. Tıklatın **devam ve etki alanı sahipliği doğrulama**. Daha sonra hello etki alanı adını kendi hello adımları tooverify izleyin. Kapsamlı yönergeler nasıl tooverify Google Apps etki alanınızı bakın. [Google Apps ile site sahipliği doğrulamak](https://support.google.com/webmasters/answer/35179).

    e. Adımları tooadd tooGoogle uygulamaları düşündüğünüz diğer etki alanlarını için önceki hello yineleyin.
     
     > [!WARNING]
     > Google Apps kiracınız için hello birincil etki alanı değiştirmek ve zaten var, yapılandırılan çoklu oturum açma Azure AD ile durumunda toorepeat adımı #3 altında sahip [adım iki: etkinleştirmek çoklu oturum açma](#step-two-enable-single-sign-on).
       
6. Merhaba, [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **yönetici rollerine**.
   
     ![Google Apps'ı tıklatın][26]

7. Hangi yönetim belirlemek istediğinizi toouse toomanage kullanıcı sağlamayı hesabı. Hello için **Yönetici rolü** bu hesabı, hello Düzenle **ayrıcalıkları** bu rol için. Tüm hello olduğundan emin olun **yönetici API ayrıcalıkları** sağlamak için bu hesabı kullanılabilir böylece etkin.
   
     ![Google Apps'ı tıklatın][27]
   
    > [!NOTE]
    > Bir üretim ortamında yapılandırıyorsanız, hello en iyi toocreate Google Apps özellikle bu adım için bir yönetici hesabı uygulamadır. Bu hesapları hello gerekli API ayrıcalıklara sahip bir yönetici rolü kendisiyle ilişkilendirilmiş olması gerekir.
     
8. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

9. Çoklu oturum açma için zaten Google Apps yapılandırdıysanız, Google hello arama alanı kullanarak uygulamaları Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Google Apps** hello uygulama galerisinde. Google Apps hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

10. Google Apps örneğiniz seçin ve ardından hello **sağlama** sekmesi.

11. Set hello **sağlama modu** çok**otomatik**. 

     ![Sağlama](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**. Yeni bir tarayıcı penceresinde bir Google Apps yetkilendirme iletişim kutusunu açar.

13. Toogive Azure Active Directory izin toomake değişiklikleri tooyour Google Apps Kiracı istediğinizi onaylayın. Tıklatın **kabul**.
    
     ![İzinleri doğrulayın.][28]

14. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Google Apps uygulama bağlanabilir. Merhaba bağlantı başarısız olursa, Google Apps hesabınız takım yönetici izinlerine sahip olduğundan emin olun ve hello deneyin **"Yetkilendir"** adım yeniden uygulayın.

15. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

16. Tıklatın **kaydedin.**

17. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooGoogle uygulamalar.**

18. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooGoogle uygulamaları eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Google Apps içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

19. tooenable hello Google Apps, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde

20. Tıklatın **kaydedin.**

Tüm kullanıcıların hello ilk eşitleme başlar ve/veya gruplarının tooGoogle uygulamaları hello kullanıcılar ve Gruplar bölümünde atanmış. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Google Apps uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png