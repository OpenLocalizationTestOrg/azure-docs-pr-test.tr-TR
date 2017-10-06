---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Facebook ile çalışma alanına arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Öğretici: Facebook ile çalışma alanına Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Facebook ile Azure Active Directory (Azure AD) ile çalışma.

Çalışma alanına Facebook ile Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Facebook tarafından erişim tooWorkplace sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooWorkplace Facebook (çoklu oturum açma) tarafından kendi Azure AD hesapları ile etkinleştirme
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Abonelik çalışma alanına Facebook çoklu oturum açma tarafından etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Facebook ile çalışma alanına hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Facebook ile çalışma alanına hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme çalışma alanı Facebook tarafından tooadd Facebook ile çalışma alanına hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd çalışma alanına hello galerisinden Facebook tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Facebook ile çalışma alanına**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. Merhaba Sonuçlar panelinde seçin **Facebook ile çalışma alanına**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile çalışma alanına Facebook "Britta Simon." olarak adlandırılan bir test kullanıcıya bağlı olarak test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen çalışma Facebook tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Facebook ile çalışma hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** Facebook ile çalışma.

tooconfigure ve Facebook ile çalışma alanına ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Yeniden kimlik doğrulamanın sıklığını yapılandırma](#configuring-reauthentication-frequency)**  -tooconfigure çalışma alanına tooprompt SAML olmadığını kontrol edin.
3. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
4. **[Facebook test kullanıcı tarafından bir çalışma alanı oluşturma](#creating-a-workplace-by-facebook-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Facebook tarafından çalışma, karşılık gelen.
5. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
6. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Facebook uygulama tarafından çalışma alanınızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile çalışma alanına Facebook tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Facebook ile çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Merhaba üzerinde **Facebook etki alanı ve URL'ler ile çalışma alanına** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instancename>.facebook.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Bu değerler hello gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Facebook yapılandırmaya göre çalışma alanına** 'yi tıklatın **yapılandırma çalışma Facebook tarafından** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. Bir farklı web tarayıcısı penceresinde, oturum açma tooyour yönetici olarak Facebook şirket site tarafından çalışma alanı.
  
   > [!NOTE] 
   > Merhaba SAML kimlik doğrulama işleminin bir parçası olarak, çalışma alanına sorgu dizelerini too2.5 sipariş toopass parametreleri tooAzure AD boyutu kilobayt yukarı değerlendirebilir.

8. Merhaba, **şirket Pano**, Git toohello **kimlik doğrulaması** sekmesi.

9. Altında **SAML kimlik doğrulaması**seçin **yalnızca SSO** hello aşağı açılan listeden.

10. Kopyalanan giriş hello değerleri **Facebook yapılandırmaya göre çalışma alanına** hello hello karşılık gelen alanlara Azure portalı bölümünde:

    *   İçinde **SAML URL** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.
    *   İçinde **SAML veren URL'si metin kutusuna**, hello değerini yapıştırın **SAML varlık kimliği**, hangi Azure portalından kopyalanır.
    *   İçinde **SAML oturum kapatma yönlendirme** (isteğe bağlı) hello değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.
    *   Açık, **base-64 kodlamalı sertifika** Azure portalından indirdiğiniz Defteri'nde Merhaba içeriğine, panoya kopyalayın ve toothe Yapıştır **SAML sertifika** metin kutusu.

11. Tooenter hello İzleyici URL alıcı URL gerekebilir ve ACS (onaylama tüketici hizmeti) URL hello altında listelenen **SAML Yapılandırması** bölümü.

12. Merhaba bölümünün toohello altına kaydırın ve hello tıklatın **Test SSO** düğmesi. Bu sonuç ile Azure AD oturum açma sayfası görünen açılır pencerede sunulur. Kimlik bilgilerinizi normal tooauthenticate girin. 

    **Sorun giderme:** olun hello e-posta adresi geri Azure AD'den döndürülen iş yeri hesabı ile oturum hello aynı hello olduğu.

13. Merhaba test başarıyla tamamlandıktan sonra hello sayfanın toohello'e gidin ve hello tıklatın **kaydetmek** düğmesi.

14. Çalışma alanına kullanan tüm kullanıcıların kimlik doğrulaması için Azure AD oturum açma sayfası artık sunulur.

15. **SAML oturum kapatma yeniden yönlendir (isteğe bağlı)** - 

    Seçebileceğiniz toooptionally Azure AD oturum kapatma sayfasını kullanılan toopoint olabilen bir SAML oturum kapatma URL'si yapılandırın. Bu ayar etkin ve yapılandırılmış durumda olduğunda hello kullanıcı artık yönlendirilmiş toohello çalışma alanına oturum kapatma sayfasının olacaktır. Bunun yerine, hello kullanıcı hello SAML oturum kapatma yönlendirme ayarında eklendi yeniden yönlendirilen toohello url olacaktır.


> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Yeniden kimlik doğrulamanın sıklığını yapılandırma

SAML onay günde üç gün, hafta, iki hafta, ay için çalışma alanına tooprompt yapılandırabilirsiniz ya da hiç.

> [!NOTE] 
>Merhaba mobil uygulamalar üzerinde hello SAML denetimi için en düşük değer ayarlanmış tooone hafta.

Ayrıca, bir SAML hello düğmesini kullanarak tüm kullanıcılar için sıfırlama zorlayabilirsiniz: artık gerektiren SAML kimlik doğrulaması tüm kullanıcılar için.


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Facebook test kullanıcı tarafından bir çalışma alanı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı tarafından Facebook çalışma alanında oluşturulur. Çalışma alanına Facebook tarafından yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.

Bu bölümdeki hiçbir şey yoktur. Bir kullanıcı çalışma Facebook tarafından yoksa, yeni bir tooaccess çalışma alanına çalıştığınızda Facebook tarafından oluşturulur.

>[!Note]
>El ile bir kullanıcıyla iletişim toocreate gerekiyorsa [Facebook istemcisini destek ekibi ile çalışma](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, Facebook tarafından erişim tooWorkplace vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooWorkplace Facebook tarafından hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Facebook ile çalışma alanına**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

