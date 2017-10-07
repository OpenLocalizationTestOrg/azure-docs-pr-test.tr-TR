---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Facebook ile çalışma alanına arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Öğretici: Facebook ile çalışma alanına Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Facebook ile Azure Active Directory (Azure AD) ile çalışma.

Çalışma alanına Facebook ile Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Facebook tarafından erişim tooWorkplace sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcılarınızın tooautomatically imzalı üzerinde tooWorkplace (çoklu oturum açma) tarafından Facebook ile Azure AD hesaplarına etkinleştirebilirsiniz.
- Hesaplarınızı tek bir merkezi konumda yönetebilirsiniz: Azure portal hello.

Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla ayrıntı için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Abonelik çalışma alanına Facebook çoklu oturum açma (SSO) tarafından etkin

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD SSO bir test ortamında test. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Facebook ile çalışma alanına hello Galerisi'nden ekleyin.
2. Yapılandırma ve Azure AD çoklu oturum açmayı sınayın.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Facebook ile çalışma alanına hello Galerisi'nden ekleme
tooconfigure hello tümleştirmeye çalışma alanı Facebook ile Azure AD hello galeri tooyour listesinden yönetilen SaaS uygulamaları Facebook ile çalışma alanına ekleyin.

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, seçin **Azure Active Directory**. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok Gözat**kurumsal uygulamalar** > **tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd hello yeni uygulama, select **yeni uygulama** hello iletişim kutusunun hello üstte.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Facebook ile çalışma alanına**seçip **Facebook ile çalışma alanına** sonuçlarından. Ardından **Ekle**, tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Facebook ile çalışma](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çalışma alanına "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Facebook tarafından SSO'su test etme

SSO toowork için hangi hello karşılık gelen çalışma Facebook tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Facebook ile çalışma hello ilgili kullanıcı arasında bağlantılı bir ilişkisi kurulmalıdır.

Merhaba hello değerini atayarak bu ilişki kurmak **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Facebook ile çalışma.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümdeki hello Azure portalında Azure AD SSO'yu etkinleştirmek ve SSO Facebook uygulama tarafından çalışma alanınızda yapılandırın.

1. Merhaba hello üzerinde Azure portal'ın **Facebook ile çalışma alanına** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba, **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable SSO.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Merhaba, **Facebook etki alanı ve URL'ler ile çalışma alanına** bölümünde, aşağıdaki hello:

    a. Merhaba, **oturum açma URL'si** metin kutusuna, hello desen kullanan bir URL yazın:`https://<company subdomain>.facebook.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, hello desen kullanan bir URL yazın:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Bu yalnızca bir örnek değerlerdir. Bu değerler, oturum açma hello gerçek URL ve tanımlayıcıdır ile güncelleştirin. Kişi hello [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/) tooget bu değerleri. 

4. Merhaba, **SAML imzalama sertifikası** bölümünde, select **sertifika (Base64)**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. **Kaydet**’i seçin.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. Merhaba, **Facebook yapılandırmaya göre çalışma alanına** bölümünde, select **yapılandırma çalışma Facebook tarafından** tooopen hello **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru** bölümü.

    ![Facebook yapılandırma ile çalışma](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. Farklı web tarayıcısı penceresinde bir yönetici olarak oturum açma tooyour Facebook şirket site tarafından çalışma alanı.
  
   > [!NOTE] 
   > Merhaba SAML kimlik doğrulama işleminin bir parçası olarak, çalışma alanına sipariş toopass parametreleri tooAzure AD boyutu too2.5 kilobayt yukarı sorgu dizelerini kullanabilirsiniz.

8. Merhaba, **şirket Pano**, Git toohello **kimlik doğrulaması** sekmesi.

9. Altında **SAML kimlik doğrulaması**seçin **yalnızca SSO** hello aşağı açılan listeden.

10. Merhaba kopyalanan hello değerleri girin **Facebook yapılandırmaya göre çalışma alanına** hello hello karşılık gelen alanlara Azure portalı bölümünde:

    *   İçinde **SAML URL** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si**, Azure portal hello kopyalanan.
    *   İçinde **SAML veren URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portal hello kopyalanan.
    *   İçinde **SAML oturum kapatma yeniden yönlendir (isteğe bağlı)**, hello değerini yapıştırın **Sign-Out URL**, Azure portal hello kopyalanan.
    *   Açık, **base-64 kodlamalı sertifika** hello Azure portal ' Not Defteri'nde, indirilen. Merhaba içeriğine, panoya kopyalayın ve ardından toothe yapıştırın **SAML sertifika** metin kutusu.

11. Tooenter hello İzleyici gerekebilecek URL, alıcı URL ve ACS (onaylama tüketici hizmeti) hello altında listelenen URL **SAML Yapılandırması** bölümü.

12. Merhaba bölümünün toohello altına'e gidin ve seçin **Test SSO**. Açılır pencere sahip hello Azure AD oturum açma sayfası görüntülenir. tooauthenticate, normal olarak kimlik bilgilerinizi girin. Azure AD geri döndürülen hello e-posta adresi iş yeri hesabı ile oturum açmış hello aynı hello olduğundan emin olun.

13. Merhaba test başarıyla tamamlandı, toohello alt hello sayfa seçin ve kaydırma **kaydetmek**.

14. Çalışma alanına kullanan herkesin artık kimlik doğrulaması için Azure AD oturum açma sayfası sunulur.

SAML oturum kapatma hello Azure AD oturum kapatma sayfasını kullanılan toopoint olabilir URL'si tooconfigure seçebilirsiniz. Bu ayar etkin ve yapılandırılmış durumda olduğunda hello kullanıcı artık yönlendirilmiş toohello çalışma alanına oturum kapatma sayfasıdır. Bunun yerine, hello kullanıcı hello SAML oturum kapatma yeniden yönlendirme ayarında eklenen yeniden yönlendirilen toohello URL'dir.


> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken. Bu uygulamayı hello ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümünde, hello seçmeniz yeterlidir **çoklu oturum açma** sekmesi ve erişim hello Merhaba aracılığıyla belgelere katıştırılmış **yapılandırma** hello alt kısmına. Daha fazla bilgiyi hello hello embedded belgeler özelliği hakkında [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Yeniden kimlik doğrulamanın sıklığını yapılandırma

SAML denetim, üç gün, her gün bir hafta, iki hafta, bir ay için çalışma alanına tooprompt yapılandırabilirsiniz ya da hiç.

> [!NOTE] 
>Merhaba mobil uygulamalar üzerinde hello SAML denetimi için en düşük değer ayarlanmış tooone hafta.

Ayrıca, tüm kullanıcılar için sıfırlama SAML zorlayabilirsiniz. toodo Bu, kullanım hello **şimdi gerektiren SAML kimlik doğrulaması tüm kullanıcılar için** düğmesi.


### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

1. Merhaba, **Azure portal**, buna hello sol bölmesinde, seçin **Azure Active Directory**.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**seçip **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki hello:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusunda, **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusu, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola**ve not edin.

    d. **Oluştur**’u seçin.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Facebook test kullanıcı tarafından bir çalışma alanı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı tarafından Facebook çalışma alanında oluşturulur. Çalışma alanına Facebook tarafından yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümdeki hiçbir şey yoktur. Bir kullanıcı çalışma Facebook tarafından yoksa, yeni bir tooaccess çalışma alanına çalıştığınızda Facebook tarafından oluşturulur.

>[!Note]
>Bir kullanıcı toocreate el ile gerekiyorsa hello başvurun [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, Facebook tarafından erişim tooWorkplace vererek Britta Simon toouse Azure SSO etkinleştirin.

![Kullanıcı atama][200] 

1. Hello Azure portal, açık hello uygulamaları görüntüleyin. Toohello dizin görünümüne gidin, çok Git**kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Facebook ile çalışma alanına**.

    ![Merhaba uygulamalar listesinde Facebook bağlantısıyla Hello çalışma alanı](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Merhaba soldaki Hello menüde seçin **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. **Add (Ekle)** seçeneğini belirleyin. Ardından hello **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.

    ![Merhaba eklemek atama bölmesi][203]

5. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **seçin**.

7. Merhaba, **eklemek atama** iletişim kutusunda **atamak**.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.
Daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Sonraki adımlar

* Merhaba bkz [nasıl öğreticiler listesi toointegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md).
* Okuma [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).
* Hakkında daha fazla çok bilgi[kullanıcı sağlamayı Yapılandır](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

