---
title: "Öğretici: Azure Active Directory Tümleştirme ile Innotas | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Innotas arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 674d01b2c0818dc10fdab5844a23c5ebf29bb2d2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="a8914-103">Öğretici: Azure Active Directory Tümleştirme Innotas ile</span><span class="sxs-lookup"><span data-stu-id="a8914-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="a8914-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Innotas tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a8914-104">In this tutorial, you learn how to integrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8914-105">Innotas Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8914-105">Integrating Innotas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8914-106">Innotas erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a8914-106">You can control in Azure AD who has access to Innotas</span></span>
- <span data-ttu-id="a8914-107">Otomatik olarak için Innotas (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a8914-107">You can enable your users to automatically get signed-on to Innotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8914-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a8914-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8914-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8914-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8914-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a8914-110">Prerequisites</span></span>

<span data-ttu-id="a8914-111">Azure AD tümleştirme Innotas ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8914-111">To configure Azure AD integration with Innotas, you need the following items:</span></span>

- <span data-ttu-id="a8914-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a8914-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8914-113">Bir Innotas çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a8914-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8914-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a8914-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8914-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8914-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8914-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a8914-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8914-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8914-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8914-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a8914-118">Scenario description</span></span>

<span data-ttu-id="a8914-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a8914-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8914-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a8914-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8914-121">Galeriden Innotas ekleme</span><span class="sxs-lookup"><span data-stu-id="a8914-121">Adding Innotas from the gallery</span></span>
2. <span data-ttu-id="a8914-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a8914-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-the-gallery"></a><span data-ttu-id="a8914-123">Galeriden Innotas ekleme</span><span class="sxs-lookup"><span data-stu-id="a8914-123">Adding Innotas from the gallery</span></span>
<span data-ttu-id="a8914-124">Azure AD Innotas tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Innotas eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8914-124">To configure the integration of Innotas into Azure AD, you need to add Innotas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8914-125">**Galeriden Innotas eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8914-125">**To add Innotas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8914-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a8914-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8914-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a8914-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8914-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a8914-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a8914-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8914-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a8914-133">Arama kutusuna **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="a8914-133">In the search box, type **Innotas**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="a8914-135">Sonuçlar panelinde seçin **Innotas**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8914-135">In the results panel, select **Innotas**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8914-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a8914-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a8914-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Innotas ile test etme</span><span class="sxs-lookup"><span data-stu-id="a8914-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8914-139">Tekli çalışmaya oturum için Azure AD Innotas karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a8914-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Innotas is to a user in Azure AD.</span></span> <span data-ttu-id="a8914-140">Diğer bir deyişle, bir Azure AD kullanıcısının Innotas ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8914-140">In other words, a link relationship between an Azure AD user and the related user in Innotas needs to be established.</span></span>

<span data-ttu-id="a8914-141">Innotas içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a8914-141">In Innotas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a8914-142">Yapılandırma ve Azure AD çoklu oturum açma Innotas ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8914-142">To configure and test Azure AD single sign-on with Innotas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8914-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a8914-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8914-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="a8914-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8914-145">**[Bir Innotas test kullanıcısı oluşturma](#creating-an-innotas-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Innotas sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a8914-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - to have a counterpart of Britta Simon in Innotas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8914-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a8914-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8914-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a8914-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8914-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a8914-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8914-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Innotas uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a8914-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="a8914-150">**Azure AD çoklu oturum açma ile Innotas yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8914-150">**To configure Azure AD single sign-on with Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="a8914-151">Azure portalında üzerinde **Innotas** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a8914-151">In the Azure portal, on the **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a8914-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a8914-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="a8914-155">Üzerinde **Innotas etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a8914-155">On the **Innotas Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="a8914-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="a8914-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a8914-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="a8914-158">This value is not real.</span></span> <span data-ttu-id="a8914-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8914-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a8914-160">Kişi [Innotas istemci destek ekibi](https://www.innotas.com/contact) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8914-160">Contact [Innotas Client support team](https://www.innotas.com/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="a8914-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a8914-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="a8914-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8914-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8914-165">Çoklu oturum açma yapılandırmak için **Innotas** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Innotas destek ekibi](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="a8914-165">To configure single sign-on on **Innotas** side, you need to send the downloaded **Metadata XML** to [Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="a8914-166">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a8914-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a8914-167">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a8914-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8914-168">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="a8914-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8914-169">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8914-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8914-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8914-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="a8914-171">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a8914-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a8914-173">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8914-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8914-174">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a8914-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8914-176">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a8914-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8914-178">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="a8914-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8914-180">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a8914-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8914-182">a.</span><span class="sxs-lookup"><span data-stu-id="a8914-182">a.</span></span> <span data-ttu-id="a8914-183">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8914-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8914-184">b.</span><span class="sxs-lookup"><span data-stu-id="a8914-184">b.</span></span> <span data-ttu-id="a8914-185">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a8914-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8914-186">c.</span><span class="sxs-lookup"><span data-stu-id="a8914-186">c.</span></span> <span data-ttu-id="a8914-187">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a8914-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8914-188">d.</span><span class="sxs-lookup"><span data-stu-id="a8914-188">d.</span></span> <span data-ttu-id="a8914-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8914-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="a8914-190">Bir Innotas test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8914-190">Creating an Innotas test user</span></span>

<span data-ttu-id="a8914-191">Kullanıcı için Innotas hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="a8914-191">There is no action item for you to configure user provisioning to Innotas.</span></span>  
<span data-ttu-id="a8914-192">Atanmış bir kullanıcı erişim paneli kullanılarak Innotas için oturum açma girişiminde bulunduğunda, Innotas kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="a8914-192">When an assigned user tries to log in to Innotas using the access panel, Innotas checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="a8914-193">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Innotas tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a8914-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8914-194">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a8914-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8914-195">Bu bölümde, Britta Innotas için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8914-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innotas.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a8914-197">**Innotas için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8914-197">**To assign Britta Simon to Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="a8914-198">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a8914-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a8914-200">Uygulamalar listesinde **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="a8914-200">In the applications list, select **Innotas**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="a8914-202">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a8914-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a8914-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8914-204">Click **Add** button.</span></span> <span data-ttu-id="a8914-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a8914-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a8914-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a8914-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8914-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a8914-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8914-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a8914-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8914-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a8914-210">Testing single sign-on</span></span>

<span data-ttu-id="a8914-211">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a8914-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a8914-212">Erişim paneli Innotas parçasında tıklattığınızda, otomatik olarak Innotas uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="a8914-212">When you click the Innotas tile in the Access Panel, you should get automatically signed-on to your Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8914-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a8914-213">Additional resources</span></span>

* [<span data-ttu-id="a8914-214">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="a8914-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8914-215">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a8914-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

