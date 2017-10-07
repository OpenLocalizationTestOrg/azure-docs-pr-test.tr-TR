---
title: "Öğretici: Azure Active Directory Tümleştirme Splunk Kurumsal ve Splunk bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Splunk Enterprise ve Splunk bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Öğretici: Azure Active Directory Tümleştirme Splunk Kurumsal ve Splunk bulut ile

Bu öğreticide, bilgi nasıl toointegrate Splunk Kurumsal ve Splunk bulut Azure Active Directory'ye (Azure AD).

Splunk Kurumsal ve Splunk bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- TooSplunk Kurumsal ve Splunk bulut erişimi olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooSplunk Kurumsal ve Splunk bulut çoklu oturum açma (SSO) etkinleştir
- Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD ile tümleştirme Splunk Enterprise ve Splunk bulut tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Abonelik Splunk Enterprise veya Splunk bulut SSO etkin


>[!NOTE]
>tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.
>

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Splunk Kurumsal ve Splunk bulut hello Galerisi'nden ekleme
2. Yapılandırma ve Azure AD SSO test etme


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Splunk Kurumsal ve Splunk bulut hello Galerisi'nden ekleme
SaaS uygulamaları listesinden hello galeri tooyour Splunk bulut yönetilen ve Azure AD'ye tooconfigure hello tümleştirme Splunk Enterprise ve Splunk bulut tooadd Splunk Kurumsal gerekir.

**tooadd Splunk Kurumsal ve Splunk bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.

    ![Active Directory][1]

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.

    ![Uygulamalar][2]

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.

    ![Uygulamalar][3]

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.

    ![Uygulamalar][4]

6. Merhaba arama kutusuna yazın **Splunk Enterprise veya Splunk bulut**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. Merhaba sonuçlar bölmesinde seçin **Splunk Kurumsal ve Splunk bulut**ve ardından **tam** tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Splunk kuruluş ile test etme ve "Britta Simon" adlı bir test kullanıcı Splunk bulut tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen Splunk Kurumsal ve Splunk bulut tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Splunk Kurumsal ve Splunk bulut arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Splunk Kurumsal ve Splunk bulut.

tooconfigure ve Splunk Kurumsal ve Splunk bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Splunk Kurumsal ve Splunk bulut test kullanıcısı oluşturma](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave karşılık gelen Britta Simon Splunk kuruluştaki ve her bağlantılı toohello Azure AD gösterimidir Splunk bulut.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD SSO hello Klasik portalında etkinleştirin ve SSO Splunk Kurumsal ve Splunk bulut uygulamanızda yapılandırın.


**Azure AD çoklu oturum açma tooconfigure Splunk Kurumsal ve Splunk bulut ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde hello Klasik Portalı'nda **Splunk Kurumsal ve Splunk bulut** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma** iletişim.
     
    ![Çoklu oturum açmayı yapılandırın][6] 

2. Merhaba üzerinde **nasıl istiyorsunuz tooSplunk Kurumsal üzerinde kullanıcılar toosign ve Splunk bulut** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. Merhaba, **oturum üzerinde URL'si** metin kutusuna, kullanıcıların toosign üzerinde tooyour Splunk Enterprise ve desen aşağıdaki hello kullanarak Splunk bulut uygulaması tarafından kullanılan türü hello URL'si:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. Merhaba, **tanımlayıcısı** metin kutusuna, Splunk sunucunuzun hello URL'sini yazın.
  3. Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL deseni takip hello ile:`https://<splunkserver>/saml/acs`
  4. **İleri**’ye tıklayın.
 
4. Merhaba üzerinde **çoklu oturum açma Splunk Enterprise ve Splunk bulut yapılandırma** sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Tıklatın **karşıdan meta veri**ve ardından hello dosyayı bilgisayarınıza kaydedin.
  2. **İleri**’ye tıklayın.

5. tooget uygulamanız için yapılandırılmış SSO Splunk Enterprise ve Splunk bulut Destek ekibine başvurun ve ile Merhaba aşağıdakileri sağlar:

    * indirilen hello **federaton meta verileri**
6. Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.
    
    ![Azure AD çoklu oturum açma][10]

7. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
 
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde, bir test kullanıcısı Britta Simon adlı hello Klasik portalda oluşturun.

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.
  2. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
  3. **İleri**’ye tıklayın.

6.  Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
  
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. Merhaba, **ad** metin kutusuna, türü **Britta**.  
  2. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.
  3. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
  4. Merhaba, **rol** listesinde **kullanıcı**.
  5. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Merhaba Hello değerini yazmak **yeni parola**.
  2. **Tamamla**’ya tıklayın.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Splunk Enterprise ve Splunk bulut test kullanıcısı oluşturma

Bu bölümde, Britta Simon Splunk kuruluştaki ve Splunk bulut adlı bir kullanıcı oluşturun. Lütfen destek ekibi tooadd hello kullanıcılar hello Splunk Enterprise ve Splunk bulut platformu Splunk Enterprise ve Splunk bulut çalışın.


### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, Britta Simon toouse Azure kendi erişim tooSplunk Kurumsal ve Splunk bulut verme SSOy etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSplunk Enterprise ve Splunk bulut hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Splunk Kurumsal ve Splunk bulut**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. Hello içinde hello üst menüsünde **kullanıcılar**.

    ![Kullanıcı atama][203]

4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.

5. Merhaba altta Hello araç çubuğunda **atamak**.

    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, Azure AD erişim paneli hello kullanarak SSOonfiguration test edin.

Merhaba Splunk Enterprise ve erişim paneli hello Splunk bulut parçasında tıkladığınızda, otomatik olarak oturum açma Splunk Kurumsal ve Splunk bulut uygulama tooyour almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
