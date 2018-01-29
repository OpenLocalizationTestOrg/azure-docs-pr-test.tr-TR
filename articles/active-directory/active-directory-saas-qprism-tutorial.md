---
title: "Öğretici: Azure Active Directory Tümleştirme ile QPrism | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile QPrism arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 72ab75ba-132b-4f83-a34b-d28b81b6d7bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/13/2017
ms.author: jeedes
ms.openlocfilehash: 1f697b95074e0fc9dbb3e8c7800e69f8ece9e0b3
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qprism"></a>Öğretici: Azure Active Directory Tümleştirme QPrism ile

Bu öğreticide, Azure Active Directory (Azure AD) ile QPrism tümleştirmek öğrenin.

QPrism Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- QPrism erişimi, Azure AD'de kontrol edebilirsiniz.
- Otomatik olarak için QPrism (çoklu oturum açma) ile Azure AD hesaplarına oturum, kullanıcılarınızın etkinleştirebilirsiniz.
- Hesaplarınızı tek bir merkezi konumda yönetebilirsiniz: Azure portal.

Azure AD SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme QPrism ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir QPrism çoklu oturum açma etkin abonelik

Bu öğreticide adımları test etmek için aşağıdaki önerileri uygulayın:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden QPrism ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="add-qprism-from-the-gallery"></a>Galeriden QPrism Ekle
Azure AD QPrism tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden QPrism eklemeniz gerekir.

**Galeriden QPrism eklemek için:**

1. İçinde [Azure portal](https://portal.azure.com), sol bölmede seçin **Azure Active Directory**. 

    ![Azure Active Directory düğmesi][1]

2. Gidin **kurumsal uygulamalar** > **tüm uygulamaları**.

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. İletişim kutusunun üstündeki yeni bir uygulama eklemek için seçin **yeni uygulama**.

    ![Yeni Uygulama düğmesi][3]

4. Arama kutusuna **QPrism**seçip **QPrism** sonuç panelinden. Ardından **Ekle** uygulama eklemek için.

    ![Sonuçlar listesinde QPrism](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı QPrism ile test etme

Tekli çalışmaya oturum için Azure AD için bir kullanıcı Azure AD'de QPrism karşılık gelen kullanıcı olan bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının ve QPrism ilgili kullanıcı arasında bağlı bir ilişki olmalıdır.

Bu ilişki içinde QPrism kurmak için değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı**.

Yapılandırma ve Azure AD çoklu oturum açma QPrism ile test etmek için aşağıdaki yapı taşları tamamlayın:

1. [Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on) bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. [Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user) Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. [QPrism test kullanıcısı oluşturma](#create-a-qprism-test-user) Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı QPrism sağlamak için.
4. [Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user) Britta Azure AD çoklu oturum açma kullanmak Simon etkinleştirmek için.
5. [Test çoklu oturum açma](#test-single-sign-on) yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma QPrism uygulamanızda yapılandırın.

1. Azure portalında üzerinde **QPrism** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_samlbase.png)

3. İçinde **QPrism etki alanı ve URL'leri** bölümünde, aşağıdakileri yapın:

    ![QPrism etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_url.png)

    a. İçinde **oturum açma URL'si** metin kutusunda, aşağıdaki desen kullanan bir URL yazın:`https://<customer domain>.qmyzone.com/login`

    b. İçinde **tanımlayıcısı** metin kutusunda, aşağıdaki desen kullanan bir URL yazın:`https://<customer domain>.qmyzone.com/metadata.php`
         
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri gerçek tanımlayıcısı ile güncelleştirin ve URL oturum açma. Kişi [QPrism istemci destek ekibi](mailto:qsupport-ce@quatrro.com) bu değerleri almak için. 

4. Oluşturulacak **meta veri** URL, aşağıdakileri yapın:

    a. Seçin **uygulama kayıtlar**.
    
    ![Çoklu oturum açma uygulama kayıtlar yapılandırın](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_appregistrations.png)
   
    b. Seçin **uç noktaları** açmak için **uç noktaları** iletişim kutusu.  
    
    ![Çoklu oturum açma uç noktasını yapılandırma](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_endpointicon.png)

    c. Kopyalamak için Kopyala düğmesini seçin **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.
    
    ![Çoklu oturum açma uç noktasını yapılandırma](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_endpoint.png)
     
    d. Özellik sayfasına Git **QPrism**ve kopyalama **uygulama kimliği** kullanarak **kopyalama**. Ardından Not Defteri'ne yapıştırın.
 
    ![Çoklu oturum açma uygulaması kimliği yapılandırın](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_appid.png)

    e. Oluştur **meta veri URL'sini** şu biçimi kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 

5. **Kaydet**’i seçin.

    ![Çoklu oturum açma düğmesi kaydetme yapılandırın](./media/active-directory-saas-qprism-tutorial/tutorial_general_400.png)
    
6. Çoklu oturum açma yapılandırmak için **QPrism** tarafı, Gönder **meta veri URL'sini** için [QPrism destek ekibi](mailto:qsupport-ce@quatrro.com). Bunlar, oturum açma SAML tek bağlantı iki tarafta da düzgün ayarlandığından emin olun.

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken. Bu uygulamadan ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve katıştırılmış erişim belgeleri etraflıca **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için:**

1. Azure portalında sol bölmede seçin **Azure Active Directory**.

    ![Azure Active Directory düğmesi](./media/active-directory-saas-qprism-tutorial/create_aaduser_01.png)

2. Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-qprism-tutorial/create_aaduser_02.png)

3. Açmak için **kullanıcı** en üstündeki iletişim kutusu **tüm kullanıcılar** iletişim kutusunda **Ekle**.

    ![Ekle düğmesi](./media/active-directory-saas-qprism-tutorial/create_aaduser_03.png)

4. İçinde **kullanıcı** iletişim kutusunda, aşağıdakileri yapın:

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-qprism-tutorial/create_aaduser_04.png)

    a. İçinde **adı** kutusuna **BrittaSimon**.

    b. İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.

    c. Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.

    d. **Oluştur**’u seçin.
 
### <a name="create-a-qprism-test-user"></a>QPrism test kullanıcısı oluşturma

Bu bölümde, QPrism içinde Britta Simon adlı bir kullanıcı oluşturun. Çalışmak [QPrism destek ekibi](mailto:qsupport-ce@quatrro.com) QPrism platform kullanıcıları eklemek için. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir. 

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, Britta QPrism için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı rolü atayın][200] 

**QPrism için Britta Simon atamak için:**

1. Azure Portalı'ndaki uygulamaları görünümünü açın ve dizin görünümüne gidin. Git **kurumsal uygulamalar**seçip **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **QPrism**.

    ![Uygulamalar listesinde QPrism bağlantı](./media/active-directory-saas-qprism-tutorial/tutorial_qprism_app.png)  

3. Soldaki menüde seçin **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. **Add (Ekle)** seçeneğini belirleyin. Ardından, altında **eklemek atama**seçin **kullanıcılar ve gruplar**.

    ![Ekleme atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** içinde **kullanıcılar** listesi.

6. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **seçin**.

7. Altında **eklemek atama**seçin **atamak**.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.

QPrism kutucuğunu seçtiğinizde erişim panelinde oturumunuz otomatik olarak QPrism uygulamanıza.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qprism-tutorial/tutorial_general_203.png

