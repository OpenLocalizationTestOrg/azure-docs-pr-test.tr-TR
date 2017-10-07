---
title: Azure AD uygulama proxy'si aaaPublish uygulamalarla | Microsoft Docs
description: "Azure AD uygulama proxy'si ile şirket içi uygulamalar toohello bulut hello Klasik Portalı'nda yayımlayın."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Azure AD Uygulama Ara Sunucusu ile uygulama yayımlama

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-application-proxy-publish.md)

Azure AD uygulama proxy'si hello erişilen şirket içi uygulamalar toobe yayımlayarak uzaktan çalışanlar destek yardımcı olan Internet. Bu noktası tarafından zaten [hello Klasik Azure portalında uygulama Proxy etkin](active-directory-application-proxy-enable.md). Bu makalede, yerel ağınızda çalışan hello adımları toopublish uygulamalar açıklanmaktadır ve ağınızın dışından güvenli uzaktan erişim'sağlayın. Bu makalede tamamladıktan sonra hazır tooconfigure Merhaba uygulaması kişiselleştirilmiş bilgileri veya güvenlik gereksinimlerine sahip olacaktır.

> [!NOTE]
> Uygulama proxy'si yalnızca toohello Premium veya Basic sürümüne Azure Active Directory yükselttiyseniz kullanılabilir olan bir özelliktir. Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md). Uygulama proxy'si toouse isterseniz [uygulamaları yayımlama hello Azure portal](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Başlangıç Sihirbazı'nı kullanarak uygulama yayımlama
1. Merhaba içinde bir yönetici olarak oturum açın [Klasik Azure portalı](https://manage.windowsazure.com/).
2. TooActive dizinine gidin ve uygulama proxy'si etkinleştirdiğiniz hello dizini seçin.
   
    ![Active Directory - simge](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Merhaba tıklatın **uygulamaları** sekmesini ve sonra hello **Ekle** hello ekranın hello düğmesini
   
    ![Uygulama ekleme](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. **Publish an application that will be accessible from outside your network (Ağınızın dışından erişilebilecek olan bir uygulamayı yayımlama)** seçeneğini belirleyin.
   
    ![Ağınızın dışından erişilebilecek olan bir uygulamayı yayımlama](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Uygulamanız hakkında bilgi aşağıdaki hello sağlar:
   
   * **Ad**: Merhaba, uygulamanız için kolay ad. Bu ad, dizininizde benzersiz olmalıdır.
   * **İç URL**: uygulama ara sunucusu Bağlayıcısı hello hello adresini özel ağınızdan tooaccess Merhaba uygulaması kullanır. Merhaba rest hello sunucusunun yayımdan olsa hello arka uç sunucu toopublish üzerinde belirli bir yol sağlayabilir. Bu şekilde, farklı sitelerde yayımlayabilirsiniz üzerinde hello aynı sunucu ve her biri kendi ad ve erişim kuralları verin.
     
     > [!TIP]
     > Bir yol yayımlarsanız, tüm hello gerekli görüntüleri, komut dosyalarını ve stil sayfaları, uygulamanız için dahil olduğundan emin olun. Uygulamanızı https://yourapp/app ise ve https://yourapp/media bulunan görüntüleri kullanır, örneğin, daha sonra https://yourapp/ hello yolu olarak yayımlamanız gerekir.
     > 
     > 
   * **Ön kimlik doğrulama yöntemi**: nasıl uygulama proxy'si erişim tooyour uygulama vermeden önce kullanıcıların doğrular. Merhaba açılan menüsünden hello seçeneklerden birini seçin.
     
     * Azure Active Directory: Uygulama proxy'si kullanıcılar toosign izinlerini hello dizin ve uygulama için kimlik doğrulaması Azure AD ile yeniden yönlendirir.
     * Geçiş: Kullanıcıların tooauthenticate tooaccess hello uygulama yok.
     
     ![Uygulama özellikleri](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. toofinish hello Sihirbazı'nı hello Merhaba ekranında hello altındaki onay işaretine tıklayın. Merhaba uygulama artık Azure AD içinde tanımlıdır.

## <a name="assign-users-and-groups-toohello-application"></a>Kullanıcılar ve gruplar toohello uygulama atama
Kullanıcılarınız için kullanıcılarınızın yayımlanan uygulamanıza tooaccess sipariş, tooassign ihtiyacınız bunları ayrı ayrı veya gruplar. (Tooassign unutmayın çok kendiniz erişim.) Atadığınız her kullanıcının Azure Basic veya sonraki sürüm için lisansı olmalıdır. Tek tek lisansları atayabilirsiniz veya toogroups. Daha fazla bilgi için bkz: [tooan uygulama kullanıcıları atama](active-directory-applications-guiding-developers-assigning-users.md). 

Ön kimlik doğrulaması gerektiren uygulamalar için bir kullanıcı atama izni toouse Merhaba uygulaması verir. Gerektirmeyen uygulamalar için ön kimlik doğrulaması, bir kullanıcı atamak hello kullanıcı Merhaba uygulaması hello erişim paneli erişebilirsiniz anlamına gelir.

1. Sonlandırma hello uygulama ekleme sihirbazını sonra hızlı başlangıç sayfasında uygulamanız için hello bakın. erişim toohello uygulamanın toomanage seçin **kullanıcılar ve gruplar**.
   
    ![Uygulama Ara Sunucusu hızlı başlangıç kullanıcı atama - ekran görüntüsü](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Dizininizde belirli grupları arayın veya tüm kullanıcılarınızı gösterin. toodisplay hello arama sonuçları, hello onay işaretine tıklayın.
   
      ![Grup veya kullanıcı arama - ekran görüntüsü](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Her kullanıcı veya tooassign toothis uygulama istediğiniz grubu seçin **atamak**. Siz bu eylemi tooconfirm istedi.

> [!NOTE]
> Tümleşik Windows Kimlik Doğrulaması Uygulamaları için yalnızca şirket içi Active Directory'nizden eşitlenen kullanıcıları ve grupları atayabilirsiniz. Microsoft hesabı ile oturum açan kullanıcılar ve konuklar, Azure Active Directory Uygulama Ara Sunucusu ile yayımlanan uygulamalar için atanamaz. Merhaba parçası olan kimlik bilgilerinizle oturum açın, kullanıcılarınızın emin yayımlama hello uygulama aynı etki alanında.
> 
> 

## <a name="test-your-published-application"></a>Yayımlanan uygulamanızı test etme
Uygulamanızı yayımladıktan sonra yayımladığınız toohello URL giderek teslim test edebilirsiniz. Uygulamaya erişebildiğinizden, doğru şekilde işlediğinden ve her şeyin beklendiği gibi çalıştığından emin olun. Sorun varsa veya bir hata iletisi alıyorum hello deneyin [sorun giderme kılavuzu](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Uygulamanızı yapılandırma
Yayımlanan uygulamaları değiştirebilir veya Gelişmiş Seçenekler hello Yapılandır sayfasında ayarlayın. Bu sayfada hello adının değiştirilmesi veya bir logoyu karşıya uygulamanızı özelleştirebilirsiniz. Ayrıca, ön kimlik doğrulama yöntemi veya çok faktörlü kimlik doğrulaması hello gibi erişim kurallarını yönetebilirsiniz.

![Gelişmiş yapılandırma](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Azure Active Directory Uygulama proxy'si, kullanarak uygulamaları yayımladıktan sonra Azure AD'de hello uygulamalar listesinde göründükleri ve onları burada yönetebilirsiniz.

Uygulamaları yayımladıktan sonra uygulama ara sunucusu hizmetlerini devre dışı bırakırsanız, hello uygulamalar artık özel ağınızın dışında erişilebilir değildir. Kullanıcılarınızın hala erişim hello uygulamaları şirket içi her zamanki gibi kullanabilirsiniz.

tooview bir uygulama ve marka emin olan erişilebilir, Merhaba uygulaması hello adına çift tıklayın. Merhaba uygulama proxy'si hizmeti devre dışı bırakılır ve hello uygulama kullanılabilir değilse, bir uyarı iletisi Merhaba ekranında hello üstünde görünür.

bir uygulama, toodelete hello listesinde bir uygulama seçin ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar
* [Kendi etki alanı adınızı kullanarak uygulama yayımlama](active-directory-application-proxy-custom-domains.md)
* [Çoklu oturum açmayı etkinleştirme](active-directory-application-proxy-sso-using-kcd.md)
* [Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md)
* [Talepleri kullanan uygulamalarla çalışma](active-directory-application-proxy-claims-aware-apps.md)

Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)

