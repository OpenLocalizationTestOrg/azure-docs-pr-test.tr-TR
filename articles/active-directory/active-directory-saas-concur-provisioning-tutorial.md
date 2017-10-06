---
title: "Öğretici: Azure Active Directory Tümleştirme ile Concur | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Concur arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Öğretici: Yapılandırma Concur kullanıcı sağlamak için

Bu öğreticinin Hello hedefi Concur ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooConcur tooperform gereken adımları hello tooshow ' dir.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active directory kiracısı.
*   Bir Concur çoklu oturum açma abonelik etkin.
*   Concur takım yönetici izinlerine sahip bir kullanıcı hesabının.

## <a name="assigning-users-tooconcur"></a>Kullanıcıların tooConcur atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Concur uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Concur uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Kullanıcıların tooConcur atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooConcur tootest hello atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooConcur atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.

## <a name="enable-user-provisioning"></a>Kullanıcı sağlamayı etkinleştirin

Bu bölümde, Azure AD tooConcur kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Concur atanan kullanıcı hesaplarında devre dışı bırakın.

> [!Tip] 
> Sağlanan hello yönergeleri izleyerek Concur için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure kullanıcı hesabı sağlama:

Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı sağlama tooConcur hesapları.

tooenable uygulamalarında gider hizmet Merhaba, toobe uygun Kurulum ve kullanım Web Hizmeti Yönetim profili var olan. Merhaba, T & E yönetim işlevleri için kullandığınız WS yönetim rolü tooyour mevcut yönetici profili eklemeyin.

Danışmanlar concur veya hello İstemci Yöneticisi ayrı bir Web hizmeti yönetici profili oluşturmanız gerekir ve hello İstemci Yöneticisi bu profili hello Web Services Yöneticisi işlevleri (örneğin, etkinleştirme uygulamalar) kullanmanız gerekir. Bu profiller hello istemci yöneticinin günlük T & E yönetici profilinden ayrı tutulmalıdır (Merhaba T & E yönetim profili olmamalıdır atanan hello WSAdmin rolü).

Merhaba uygulama etkinleştirmek için kullanılan hello profil toobe oluşturduğunuzda, hello kullanıcı profili alanlarına hello istemci yöneticinin adı girin. Sahipliği toohello profil atar. Bir veya daha fazla profil oluşturulduktan sonra hello istemci bu profili tooclick hello oturum açmanız gerekir "*etkinleştirmek*" bir iş ortağı uygulamanın içinden hello Web Hizmetleri menü düğmesi.

Aşağıdaki nedenlerden hello için bu eylem normal T & E Yönetim için kullandıkları hello profiliyle yapılmalıdır değil.

* Merhaba istemci sahip tıklattığında bir hello toobe "*Evet*" uygulama etkinleştirildikten sonra görüntülenen hello iletişim penceresinde. Bunu siz veya hello iş ortağı Evet düğmesini tıklattıktan olamaz şekilde hello istemci hello iş ortağı uygulama tooaccess için kendi veri istekli bildirir.

* Merhaba T & E yönetim profili kullanarak bir uygulama etkinleştirilmiş bir istemci Yöneticisi (hello profiline devre kaynaklanan) hello şirketten ayrılırsa, bu profili kullanan etkinleştirilmiş uygulamalardan çalışmaz hello uygulama ile başka bir etkin WS yönetim etkinleştirilene kadar profili. Toocreate ayrı WS yönetim profilleri beklenen nedeni budur.

* Yönetici hello şirketten ayrılması durumunda WS yönetim profili değiştirilen toohello değiştirme yönetici etkin hello etkilemeden bu profili gerek yoktur çünkü uygulama devre isterseniz olabilir toohello ilişkili hello adı.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. Tooyour üzerinde oturum **Concur** Kiracı.

2. Merhaba gelen **Yönetim** menüsünde, select **Web Hizmetleri**.
   
    ![Concur kiracısı](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur kiracısı")

3. Hello tarafı, sol hello üzerinde **Web Hizmetleri** bölmesinde, **iş ortağı uygulamasını etkinleştir**.
   
    ![İş ortağı uygulamasını etkinleştir](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "iş ortağı uygulamasını etkinleştir")

4. Merhaba gelen **etkinleştirmek uygulama** listesinde **Azure Active Directory**ve ardından **etkinleştirmek**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Tıklatın **Evet** tooclose hello **eylemi onaylayın** iletişim.
   
    ![Eylemi onaylamak](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "eylemi onaylayın")

6. Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

7. Çoklu oturum açma için zaten Concur yapılandırdıysanız, hello arama alanı kullanarak Concur Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Concur** hello uygulama galerisinde. Concur hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

8. Concur örneğiniz seçin ve ardından hello **sağlama** sekmesi.

9. Set hello **sağlama modu** çok**otomatik**. 
 
    ![Sağlama](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. Merhaba altında **yönetici kimlik bilgileri** bölümünde, hello girin **kullanıcı adı** ve hello **parola** Concur yöneticinizin.

11. Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Concur uygulama bağlanabilir. Merhaba bağlantı başarısız olursa Concur hesabınızın Team yönetici izinleri olduğundan emin olun.

12. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

13. Tıklatın **kaydedin.**

14. Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooConcur.**

15. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooConcur eşitlenir hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Concur içinde güncelleştirme işlemleri için özelliklerdir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

16. tooenable hello Concur, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

17. Tıklatın **kaydedin.**

Şimdi sınama hesabı oluşturabilirsiniz. TooConcur hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-concur-tutorial.md)

