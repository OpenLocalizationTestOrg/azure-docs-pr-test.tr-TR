---
title: Azure AD uygulama proxy'si aaaPublish uygulamalarla | Microsoft Docs
description: "Azure AD uygulama proxy'si ile şirket içi uygulamalar toohello bulut hello Azure portalında yayımlarsınız."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Azure AD Uygulama Ara Sunucusu ile uygulama yayımlama

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-application-proxy-publish.md)

Azure Active Directory (AD) uygulama proxy'si hello erişilen şirket içi uygulamalar toobe yayımlayarak uzaktan çalışanlar destek yardımcı olan Internet. Ağınızın dışından hello Azure portal tooprovide güvenli uzaktan erişim yoluyla bu uygulamaları yayımlayabilirsiniz.

Bu makalede hello adımları toopublish uygulama proxy'si ile bir şirket içi uygulama anlatılmaktadır. Bu makalede tamamladıktan sonra kullanıcılarınızın olacak mümkün tooaccess uygulamanızı uzaktan olabilir. Ve ek özellikler gibi hello uygulama için hazır tooconfigure olacak tek oturum açma, kişiselleştirilmiş bilgileri ve güvenlik gereksinimleri.

Yeni tooApplication Proxy değilseniz, bu özellik ile Merhaba makalesi hakkında daha fazla bilgi [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Uzaktan erişim için şirket içi uygulama yayımlama

Bu adımları toopublish uygulamalarınızı uygulama proxy'si ile izleyin. Önceden indirilen henüz ve kuruluşunuz için bir bağlayıcı yapılandırılmış, çok gidin[uygulama proxy'si ile başlayın ve hello Bağlayıcısı yüklemeniz](active-directory-application-proxy-enable.md) ilk olarak ve uygulamanızı yayımlayın.

> [!TIP]
> Hello için uygulama proxy'si ilk kez test ediyorsanız parola tabanlı kimlik doğrulaması için ayarlanmış bir uygulama seçin. Uygulama proxy'si diğer kimlik doğrulama türlerini destekler, ancak parola tabanlı uygulamalar hello kolay tooget yukarı ve hızlı bir şekilde çalışıyor. 

1. Merhaba içinde bir yönetici olarak oturum açın [Azure portal](https://portal.azure.com/).
2. Seçin **Azure Active Directory** > **kurumsal uygulamalar** > **yeni uygulama**.

  ![Kurumsal uygulama ekleme](./media/application-proxy-publish-azure-portal/add-app.png)

3. Seçin **tüm**seçeneğini belirleyip **şirket içi uygulama**.  

  ![Kendi uygulama ekleme](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Uygulamanız hakkında bilgi aşağıdaki hello sağlar:

   - **Ad**: hello erişim paneli ve hello Azure portalında görünür hello uygulamanın hello adı. 

   - **İç URL**: özel ağınızda tooaccess hello uygulamadan kullandığınız URL hello. Merhaba rest hello sunucusunun yayımdan olsa hello arka uç sunucu toopublish üzerinde belirli bir yol sağlayabilir. Bu şekilde, farklı siteleri yayımlama hello farklı uygulamalar aynı sunucuya ve her biri kendi adı ve erişim kuralları belirleyebilirsiniz.

     > [!TIP]
     > Bir yol yayımlarsanız, tüm hello gerekli görüntüleri, komut dosyalarını ve stil sayfaları, uygulamanız için dahil olduğundan emin olun. Uygulamanızı https://yourapp/app ise ve https://yourapp/media bulunan görüntüleri kullanır, örneğin, daha sonra https://yourapp/ hello yolu olarak yayımlamanız gerekir. Bu iç URL kullanıcılarınızın toobe hello giriş sayfası sahip değil. Daha fazla bilgi için bkz: [yayımlanan uygulamalar için özel bir ana sayfa ayarlamak](application-proxy-office365-app-launcher.md).

   - **Dış URL**: Merhaba adresi kullanıcılarınızın tooin sipariş tooaccess hello uygulamadan ağınızın dışından gider. Toouse hello varsayılan uygulama proxy'si etki alanı istemiyorsanız, bilgiyi [Azure AD uygulama proxy'si özel etki alanlarında](active-directory-application-proxy-custom-domains.md).
   - **Ön kimlik doğrulamasını**: nasıl uygulama proxy'si erişim tooyour uygulama vermeden önce kullanıcıların doğrular. 

     - Azure Active Directory: Uygulama proxy'si kullanıcılar toosign izinlerini hello dizin ve uygulama için kimlik doğrulaması Azure AD ile yeniden yönlendirir. Koşullu erişim ve çok faktörlü kimlik doğrulaması gibi Azure AD güvenlik özelliklerden yararlanabilmeniz hello varsayılan olarak bu seçenek tutmanızı önerir.
     - Geçiş: Kullanıcıların Azure Active Directory tooaccess Merhaba uygulaması karşı tooauthenticate yok. Hala hello arka uç kimlik doğrulaması gereksinimleri ayarlayabilirsiniz.
   - **Bağlayıcı grup**: bağlayıcıları işlem hello uzaktan erişim tooyour uygulama ve bağlayıcı grupları, bağlayıcılar ve bölge, ağ veya amacı uygulamaların düzenlemenize yardımcı olur. Bağlayıcı gruplarda henüz yoksa, uygulamanız çok atanan**varsayılan**.

   ![Uygulamanızı yapılandırma](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Gerekirse, ek ayarları yapılandırın. Çoğu uygulama için bu ayarları varsayılan durumlarına tutmanız gerekir. 
   - **Arka uç uygulaması zaman aşımı**: Bu değeri çok ayarlayın**uzun** yalnızca uygulamanızı yavaş tooauthenticate ve bağlanın ise. 
   - **Üst bilgileri URL'leri**: Bu değer olarak tutun **Evet** hello özgün ana bilgisayar üstbilgisi hello kimlik doğrulama isteği için uygulamanız gereken sürece.
   - **Uygulama gövdesindeki URL'leri**: Bu değer olarak tutun **Hayır** kodlanmış HTML bağlantılar tooother şirket içi uygulamalarınız mevcutsa ve özel etki alanlarını kullanmadığınız sürece. Daha fazla bilgi için bkz: [bağlantı uygulama proxy'si ile çeviri](application-proxy-link-translation.md).
   
   ![Uygulamanızı yapılandırma](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. **Add (Ekle)** seçeneğini belirleyin.


## <a name="add-a-test-user"></a>Test kullanıcı ekleme 

uygulamanız doğru bir şekilde, yayımlanan tootest bir test kullanıcı hesabı ekleyin. Bu hesap izinleri tooaccess hello uygulamadan olduğunu doğrulayın hello kurumsal ağ içinde.

1. Geri hello hızlı başlangıç dikey penceresinde, seçin **test etmek için bir kullanıcı atamak**.

  ![Test etmek için bir kullanıcı atama](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Merhaba kullanıcıları ve grupları dikey penceresinde, seçin **Ekle**.

  ![Bir kullanıcı veya Grup Ekle](./media/application-proxy-publish-azure-portal/add-user.png)

3. Merhaba Ekle atama dikey seçin **kullanıcılar ve gruplar** tooadd istediğiniz hello hesabı seçin. 
4. Seçin **atamak**.

## <a name="test-your-published-app"></a>Yayımlanan uygulamanızı test etme

Tarayıcınızda, gezinme sırasında hello yapılandırılmış toohello dış URL'si adım yayımlama. Merhaba Başlangıç ekranına görmeniz gerekir ve mümkün toosign hello test hesabıyla, ayarlanmış.

![Yayımlanan uygulamanızı test etme](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Sonraki adımlar
- [Bağlayıcılar karşıdan](active-directory-application-proxy-enable.md) ve [bağlayıcı grupları oluşturma](active-directory-application-proxy-connectors-azure-portal.md) ayrı ağlar ve konumları toopublish uygulamaları.

- [Çoklu oturum açmayı kurduğunuzda](application-proxy-sso-azure-portal.md) yeni yayımlanan uygulamanız için
