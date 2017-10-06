---
title: "Öğretici: Kullanıcı sağlamak için çalışma alanına Facebook tarafından yapılandırma | Microsoft Docs"
description: "Azure AD tooWorkplace Facebook tarafından gelen nasıl tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Öğretici: Facebook ile çalışma alanına kullanıcı sağlamak için yapılandırın

Sağlamak ve Azure Active Directory (Azure AD) tooWorkplace Facebook tarafından kullanıcı hesaplarından sağlanmasını adımları gerekli tooautomatically hello Bu öğretici gösterir.

## <a name="prerequisites"></a>Ön koşullar

Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, hello aşağıdaki gerekir:

- Bir Azure AD aboneliği
- Abonelik çalışma alanına Facebook çoklu oturum açma (SSO) tarafından etkin

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Kullanıcıların tooWorkplace Facebook tarafından atayın

Azure AD hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların Azure AD tooan uygulamada atanan eşitlenir.

Yapılandırma ve hizmet sağlama hello etkinleştirme karar vermeden önce hangi kullanıcıların ve grupların Azure AD içinde tooyour çalışma alanına Facebook uygulaması tarafından erişim hello kullanıcılar temsil eder. İzleyerek Facebook uygulaması tarafından bu kullanıcıların tooyour çalışma alanına daha sonra yeniden atayabilirsiniz hello yönergeleri [bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Tek bir atayarak yapılandırma sağlama test hello Azure AD kullanıcı tooWorkplace Facebook tarafından. Ek kullanıcılar ve gruplar daha sonra atayın.
>*   Bir kullanıcı tooWorkplace Facebook tarafından atadığınızda, geçerli bir kullanıcı rolünün seçmeniz gerekir. Merhaba varsayılan erişim rolü sağlama için çalışmaz.

## <a name="enable-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı etkinleştirin

Bu bölümde, çalışma alanına API Facebook tarafından sağlama, Azure AD toohello kullanıcı hesabınızın konusunda size rehberlik eder. Ayrıca nasıl tooconfigure hello sağlama hizmeti toocreate, güncelleştirme ve çalışma Facebook tarafından atanan kullanıcı hesapları devre dışı bırak öğrenin. Bu kullanıcı ve grup atama Azure AD'de dayanır.

>[!Tip]
>Ayrıca tooenabled SAML tabanlı SSO için çalışma alanı, Facebook tarafından göre hello sağlanan hello yönergelerini izleyerek seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayan olsa SSO otomatik sağlamayı bağımsız olarak yapılandırılabilir.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Azure AD'de tooWorkplace Facebook tarafından sağlama kullanıcı hesabı yapılandırın

Azure AD destekler Hello özelliği tooautomatically hello hesap ayrıntılarını eşitlemek kullanıcılar tooWorkplace Facebook tarafından atanır. Facebook tooget hello verileri, gereken tooauthorize kullanıcılar, erişimi için önce tarafından çalışma alanına bu otomatik eşitlenmesine olanak bunları içinde toosign hello için ilk kez çalışılıyor. Erişim Azure AD'de iptal edilmiş durumda olduğunda, ayrıca çalışma alanına Facebook tarafından kullanıcılardan XML'deki sağlamasını yapar.

1. Merhaba, [Azure portal](https://portal.azure.com)seçin **Azure Active Directory** > **Kurumsal uygulamaları** > **tüm uygulamaları**.

2. SSO için Facebook ile çalışma alanına zaten yapılandırdıysanız, çalışma alanına Facebook tarafından örneğiniz hello arama alanı kullanarak arayın. Aksi takdirde seçin **Ekle** arayın ve **Facebook ile çalışma alanına** hello uygulama galerisinde. Seçin **Facebook ile çalışma alanına** hello gelen arama sonuçlarında ve uygulamaların tooyour listesine ekleyin.

3. Facebook ile çalışma alanına örneğiniz seçin ve ardından hello seçin **sağlama** sekmesi.

4. Ayarlama **sağlama modu** çok**otomatik**. 

    ![Çalışma alanına ekran görüntüsü tarafından Facebook sağlama seçenekleri](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. Hello altında **yönetici kimlik bilgileri** bölümünde, hello girin **gizli belirteci** ve hello **Kiracı URL** Facebook yönetici tarafından çalışma alanı.

6. Hello Azure portal, seçin **Bağlantıyı Sına** tooensure Azure AD, Facebook uygulaması tarafından tooyour çalışma alanına bağlanabilir. Merhaba bağlantı başarısız olursa işyeriniz Facebook hesabına göre takım yönetici izinleri olduğundan emin olun.

7. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.

8. **Kaydet**’i seçin.

9. Hello eşlemeleri bölümü altında seçin **Facebook tarafından Azure Active Directory Kullanıcıları Eşitle tooWorkplace**.

10. Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooWorkplace Facebook tarafından eşitlenen hello kullanıcı öznitelikleri gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları çalışma Facebook tarafından güncelleştirme işlemleri için özelliklerdir. herhangi bir değişiklik toocommit seçin **kaydetmek**.

11. tooenable hello Azure AD sağlama hizmetinde tarafından Facebook, çalışma alanı için hello **ayarları** bölümünde, hello değiştirme **sağlama durumu** çok**üzerinde**.

12. **Kaydet**’i seçin.

Hakkında daha fazla bilgi için hazırlama, otomatik tooconfigure bkz [Facebook belgelerine hello](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Şimdi sınama hesabı oluşturabilirsiniz. İçin Facebook tarafından tooWorkplace hello hesap tooverify eşitlenmiş too20 dakika bekleyin.

## <a name="additional-resources"></a>Ek kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Çoklu oturum açmayı yapılandırın](active-directory-saas-facebook-at-work-tutorial.md)

