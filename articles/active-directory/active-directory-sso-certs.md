---
title: "Azure AD'de aaaManage Federasyon sertifikalarını | Microsoft Docs"
description: "Nasıl toocustomize hello sona erme tarihini, Federasyon sertifikalarını ve nasıl toorenew sertifikalar yakında dolacak öğrenin."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Federasyon tek oturum açma için Azure Active Directory'de sertifikaları yönetme
Bu makale ortak soruları kapsar ve tekli oturum açma (SSO) tooyour SaaS uygulamaları Azure Active Directory (Azure AD) tooestablish oluşturur toohello sertifikalar Federasyon ile ilgili bilgiler. Uygulamaları'hello Azure AD uygulama galerisinde veya bir galeri olmayan uygulama şablonu kullanarak ekleyin. Merhaba uygulaması hello Federasyon SSO seçeneğini kullanarak yapılandırın.

Bu makalede SAML Federasyon üzerinden yapılandırılmış toouse Azure AD SSO olan ilgili yalnızca tooapps aşağıdaki örneğine hello gösterildiği gibi olur:

![Azure AD çoklu oturum açma](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Galeri ve galeri olmayan uygulamalar için otomatik olarak oluşturulan sertifika
Azure AD hello galeriden yeni bir uygulama eklemek ve bir SAML tabanlı oturum açma yapılandırdığınızda üç yıl geçerlidir hello uygulama için bir sertifika oluşturur. Merhaba bu sertifikayı indirebilirsiniz **SAML imzalama sertifikası** bölümü. Galeri uygulamalar için bu bölümde bir seçeneği toodownload hello sertifika veya meta verileri, hello gereksinim hello uygulamasının bağlı olarak gösterebilir.

![Azure AD çoklu oturum açma](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Federasyon sertifikanızı Hello sona erme tarihini özelleştirebilir ve yeni bir sertifika tooa alma
Varsayılan olarak, sertifikaları tooexpire üç yıl sonra ayarlanır. Merhaba aşağıdaki adımları tamamlayarak sertifikanızı farklı sona erme tarihini seçebilirsiniz.
Merhaba ekran görüntüleri Salesforce örnek hello artırmak amacıyla için kullanın, ancak Federasyon tooany SaaS uygulama adımları uygulayabilirsiniz.

1. Merhaba, [Azure portal](https://aad.portal.azure.com), tıklatın **Kurumsal uygulama** hello sol bölmesinde ve ardından **yeni uygulama** hello üzerinde **genel bakış** Sayfa:

   ![Açık hello SSO Yapılandırma Sihirbazı](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Merhaba galeri uygulaması için arama yapın ve ardından tooadd istediğiniz hello uygulamayı seçin. Gerekli hello uygulama bulamazsa hello uygulamasını hello kullanarak eklemek **olmayan galeri uygulama** seçeneği. Bu özellik yalnızca hello Azure AD Premium (P1 ve P2) SKU kullanılabilir.

    ![Azure AD çoklu oturum açma](./media/active-directory-sso-certs/add_gallery_application.png)

3. Merhaba tıklatın **çoklu oturum açma** sol bölmesinde ve değişiklik hello bağlantıyı **tek oturum açma modu** çok**SAML tabanlı oturum açma**. Bu adımı uygulamanız için üç yıllık sertifika oluşturur.

4. toocreate yeni bir sertifika tıklatın hello **yeni sertifika oluştur** hello bağlantıyı **SAML imzalama sertifikası** bölümü.

    ![Yeni bir sertifika oluşturma](./media/active-directory-sso-certs/create_new_certficate.png)

5. Merhaba **yeni bir sertifika oluşturmak** bağlantı hello Takvim denetimi açar. Geçerli tarih hello tüm tarih ve saat toothree yıl yukarı ayarlayabilirsiniz. Başlangıç tarihi seçili ve hello yeni sona erme tarihi ve saati, yeni sertifikanın saattir. **Kaydet** düğmesine tıklayın.

    ![İndirme sonra hello sertifikasını karşıya yükle](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Merhaba yeni sertifika kullanılabilir toodownload sunulmuştur. Merhaba tıklatın **sertifika** bağlantı toodownload onu. Bu noktada, sertifikanızı etkin değil. Toothis sertifika tooroll istediğinizde hello seçin **yeni sertifika etkin hale getirin** onay kutusunu ve tıklatın **kaydetmek**. Bu noktadan itibaren Azure AD hello yanıt imzalama için hello yeni sertifikayı kullanarak başlatır.

7.  toolearn tooupload hello sertifika nasıl tooyour belirli SaaS uygulama hello tıklatın **görünüm uygulaması yapılandırma Öğreticisi** bağlantı.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Süresi yakında dolacak bir sertifikayı yenileme
Merhaba aşağıdaki yenileme adımları kullanıcılarınız için önemli kapalı kalma süresi neden. Bu bölümde özelliği Salesforce örneği, ancak bu adımların olarak Hello görüntülerde Federasyon tooany SaaS uygulama uygulayabilirsiniz.

1. Merhaba üzerinde **Azure Active Directory** uygulama **çoklu oturum açma** sayfasında, uygulamanız için hello yeni sertifika oluşturun. Merhaba tıklayarak bunu yapabilirsiniz **yeni sertifika oluştur** hello bağlantıyı **SAML imzalama sertifikası** bölümü.

    ![Yeni bir sertifika oluşturma](./media/active-directory-sso-certs/create_new_certficate.png)

2. Select hello istenen tıklatın ve yeni sertifika için sona erme tarihi ve saati **kaydetmek**.

3. Merhaba Hello sertifikada karşıdan **SAML imzalama sertifikası** seçeneği. Merhaba yeni sertifika toohello SaaS uygulamanın tek oturum açma yapılandırma ekranında karşıya yükleyin. toolearn nasıl toodo belirli SaaS uygulamanız için burayı tıklatın hello **görünüm uygulaması yapılandırma Öğreticisi** bağlantı.
   
4. Azure AD'de select hello tooactivate hello yeni sertifika **yeni sertifika etkin hale getirin** onay kutusunu işaretleyin ve hello tıklatın **kaydetmek** hello sayfanın üst kısmındaki hello düğmesi. Bu Azure AD yan hello üzerinde yeni bir sertifika hello yapar. Merhaba sertifikanın Hello durumunu değiştirir **yeni** çok**etkin**. Bu noktadan itibaren Azure AD hello yanıt imzalama için hello yeni sertifikayı kullanarak başlatır. 
   
    ![Yeni bir sertifika oluşturma](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>İlgili makaleler
* [İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Azure Active Directory'de uygulama yönetimi için makale dizini](active-directory-apps-index.md)
* [Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma](active-directory-appssoaccess-whatis.md)
* [Sorun giderme SAML tabanlı çoklu oturum açma](active-directory-saml-debugging.md)
