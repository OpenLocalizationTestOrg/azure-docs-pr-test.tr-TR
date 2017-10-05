---
title: "Öğretici: Azure otomatik kullanıcı sağlamayı Google uygulamaları yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve Google Apps için kullanıcı hesapları Azure AD'den sağlanmasını öğrenin."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Öğretici: Otomatik kullanıcı sağlamayı için Google uygulamaları yapılandırma

Bu öğreticinin amacı, Google Apps ve Azure AD otomatik olarak sağlamak ve Google Apps için kullanıcı hesapları Azure AD'den sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   İş veya eğitim için Google Apps için Google Apps için geçerli bir kiracı olması gerekir. Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.
*   Google Apps takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-to-google-apps"></a>Google Apps kullanıcılar atama

Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır. Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.

Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Google Apps uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir. Karar sonra bu kullanıcılar, Google Apps uygulamanızın Buradaki yönergeleri izleyerek atayabilirsiniz: [bir kullanıcı veya grup için bir kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için Google Apps atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.
>*   Bir kullanıcı için Google Apps atarken, kullanıcı ya da "Grup" rol ataması iletişim kutusunda seçmeniz gerekir. "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Azure AD Google Apps'ın kullanıcı hesabı sağlama API'sine bağlanma ve sağlama hizmeti oluşturmak için yapılandırma güncelleştirmesi ve Google Apps atanan kullanıcı hesaplarında devre dışı bu bölümü kılavuzları kullanıcı ve grup atama Azure AD'de temel.

>[!Tip]
>Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için Google Apps, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="configure-automatic-user-account-provisioning"></a>Hesap otomatik kullanıcı sağlamayı Yapılandır

> [!NOTE]
> Google Apps kullanıcı sağlamayı otomatikleştirmek için başka bir uygulanabilir seçenek kullanmaktır [Google Apps dizin eşitleme (GADS)](https://support.google.com/a/answer/106368?hl=en) Google Apps, şirket içi Active Directory kimlikleri sağlar. Buna karşılık, çözüm Bu öğreticide, Azure Active Directory (bulut) kullanıcıları ve Google Apps için posta özellikli gruplar sağlamasını yapar. 

1. Oturum [Google Apps Yönetici Konsolu](http://admin.google.com/) yönetici hesabı kullanarak ve tıklayın **güvenlik**. Bağlantıyı görmüyorsanız, altında gizli olabilir **daha fazla denetim** ekranın altındaki menüsü.
   
    ![Güvenlik'e tıklayın.][10]

2. Üzerinde **güvenlik** sayfasında, **API Başvurusu**.
   
    ![API Başvurusu'ı tıklatın.][15]

3. Seçin **etkinleştirmek API erişimini**.
   
    ![API Başvurusu'ı tıklatın.][16]

    > [!IMPORTANT]
    > Google Apps, Azure Active Directory'de kullanıcı adlarını sağlamak istediğiniz her kullanıcı için *gerekir* özel bir etki alanına bağlı. Örneğin, neye benzediğini gösteren kullanıcı adları bob@contoso.onmicrosoft.com ancak Google Apps tarafından kabul edilmiyor bob@contoso.com kabul edilir. Mevcut bir kullanıcının etki alanı Azure AD'de özelliklerini düzenleyerek değiştirebilirsiniz. Yönergeler için Azure Active Directory ve Google Apps için özel bir etki alanı ayarlama adımları izleyerek dahil edilmiştir.
      
4. Ardından, bir özel etki alanı adı, Azure Active Directory'ye henüz eklemediyseniz, aşağıdaki adımları izleyin:
  
    a. İçinde [Azure portal](https://portal.azure.com), sol gezinti bölmesinde tıklatın **Active Directory**. Dizin listesinde dizininizi seçin. 

    b. Tıklatın **etki alanı adı** sol gezinti bölmesinde ve ardından **Ekle**.
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![etki alanı ekleme](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Etki alanı adınızı yazın **etki alanı adı** alan. Bu etki alanı adı, Google uygulamaları için kullanmak istediğiniz aynı etki alanı adı olmalıdır. Hazır olduğunuzda tıklatın **etki alanı Ekle** düğmesi.
     
     ![Etki alanı adı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Tıklatın **sonraki** doğrulama sayfasına gidin. Bu etki alanına ait olduğunu doğrulamak için etki alanının DNS kayıtlarını bu sayfada sağlanan değerlere göre düzenlemeniz gerekir. Kullanarak doğrulamak seçebilirsiniz **MX kayıtları** veya **TXT kayıtlarının**için seçtiğiniz bağlı olarak **kayıt türü** seçeneği. Azure AD etki alanı adıyla doğrulamak nasıl daha kapsamlı yönergeler için bkz [kendi etki alanı adını Azure AD'ye ekleme](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Dizininize eklemek istediğiniz tüm etki alanları için önceki adımları yineleyin.

5. Azure AD ile etki alanları doğruladıktan, artık bunları yeniden Google Apps ile doğrulamanız gerekiyor. Google Apps ile zaten kayıtlı değil her etki alanı için aşağıdaki adımları gerçekleştirin:
   
    a. İçinde [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **etki alanları**.
     
     ![Etki alanlarında tıklatın][20]

    b. Tıklatın **bir etki alanı veya bir etki alanı diğer adı eklemek**.
     
     ![Yeni bir etki alanı Ekle][21]

    c. Seçin **başka bir etki alanı ekleme**ve eklemek istediğiniz etki alanı adını yazın.
     
     ![Etki alanı adınızı yazın][22]

    d. Tıklatın **devam ve etki alanı sahipliği doğrulama**. Sonra etki alanı adının size ait olduğunu doğrulamak için adımları izleyin. Google Apps etki alanınızı doğrulayın konusunda kapsamlı yönergeler için bkz. [Google Apps ile site sahipliği doğrulamak](https://support.google.com/webmasters/answer/35179).

    e. Google Apps için eklemek istediğiniz her ek etki alanları için önceki adımları yineleyin.
     
     > [!WARNING]
     > Google Apps kiracınız için birincil etki alanı değiştirmek ve zaten var, yapılandırılan çoklu oturum açma Azure AD ile durumunda #3. adım altında yinelemek zorunda [adım iki: etkinleştirmek çoklu oturum açma](#step-two-enable-single-sign-on).
       
6. İçinde [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **yönetici rollerine**.
   
     ![Google Apps'ı tıklatın][26]

7. Kullanıcı sağlamayı yönetmek için kullanmak istediğiniz yönetici hesabı belirleyin. İçin **Yönetici rolü** bu hesabı, düzenleme **ayrıcalıkları** bu rol için. Tüm olduğundan emin olun **yönetici API ayrıcalıkları** sağlamak için bu hesabı kullanılabilir böylece etkin.
   
     ![Google Apps'ı tıklatın][27]
   
    > [!NOTE]
    > Bir üretim ortamında yapılandırıyorsanız, en iyi uygulama olarak bir yönetici hesabı Google Apps özellikle bu adım için oluşturmaktır. Bu hesaplar gerekli API ayrıcalıklara sahip bir yönetici rolü kendisiyle ilişkilendirilmiş olması gerekir.
     
8. İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

9. Çoklu oturum açma için Google Apps zaten yapılandırdıysanız arama alanı kullanarak Google Apps Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Google Apps** uygulama galerisinde. Arama sonuçlarından Google Apps seçin ve uygulamaları listenize ekleyin.

10. Google Apps örneğiniz seçin ve ardından **sağlama** sekmesi.

11. Ayarlama **sağlama modunda** için **otomatik**. 

     ![Sağlama](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. Altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**. Yeni bir tarayıcı penceresinde bir Google Apps yetkilendirme iletişim kutusunu açar.

13. Google Apps kiracınız değişiklik yapmak için Azure Active Directory izni vermek istediğiniz onaylayın. Tıklatın **kabul**.
    
     ![İzinleri doğrulayın.][28]

14. Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD, Google Apps uygulamanızın bağlanabilir. Bağlantı başarısız olursa, Google Apps hesabınız takım yönetici izinlerine sahip olduğundan emin olun ve deneyin **"Yetkilendir"** adım yeniden uygulayın.

15. Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve onay kutusunu işaretleyin.

16. Tıklatın **kaydedin.**

17. Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları Google Apps için.**

18. İçinde **öznitelik eşlemelerini** bölümünde, Google Apps Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin. Seçilen öznitelikler **eşleşen** özellikleri, Google Apps kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır. Değişiklikleri kaydetmek için Kaydet düğmesini seçin.

19. Google Apps için hizmet sağlama Azure AD etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** ayarları bölümünde

20. Tıklatın **kaydedin.**

Herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde Google Apps atanan ilk eşitleme başlatır. İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer. Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve Google Apps uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.

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