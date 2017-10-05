---
title: "Öğretici: Azure Active Directory Tümleştirme ile Abintegro | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Abintegro arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="e5205-103">Öğretici: Azure Active Directory Tümleştirme Abintegro ile</span><span class="sxs-lookup"><span data-stu-id="e5205-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="e5205-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Abintegro tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e5205-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5205-105">Abintegro Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e5205-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5205-106">Abintegro erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e5205-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="e5205-107">Otomatik olarak için Abintegro (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e5205-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5205-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e5205-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e5205-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5205-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5205-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e5205-110">Prerequisites</span></span>

<span data-ttu-id="e5205-111">Azure AD tümleştirme Abintegro ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5205-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="e5205-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e5205-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5205-113">Bir Abintegro çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e5205-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5205-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e5205-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5205-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5205-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5205-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e5205-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5205-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5205-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5205-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e5205-118">Scenario description</span></span>
<span data-ttu-id="e5205-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e5205-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5205-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e5205-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5205-121">Galeriden Abintegro ekleme</span><span class="sxs-lookup"><span data-stu-id="e5205-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="e5205-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e5205-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="e5205-123">Galeriden Abintegro ekleme</span><span class="sxs-lookup"><span data-stu-id="e5205-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="e5205-124">Azure AD Abintegro tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Abintegro eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5205-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5205-125">**Galeriden Abintegro eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5205-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5205-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e5205-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e5205-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e5205-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5205-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e5205-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e5205-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5205-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e5205-133">Arama kutusuna **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="e5205-133">In the search box, type **Abintegro**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="e5205-135">Sonuçlar panelinde seçin **Abintegro**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5205-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5205-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e5205-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5205-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Abintegro ile test etme</span><span class="sxs-lookup"><span data-stu-id="e5205-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e5205-139">Tekli çalışmaya oturum için Azure AD Abintegro karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e5205-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="e5205-140">Diğer bir deyişle, bir Azure AD kullanıcısının Abintegro ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5205-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="e5205-141">Abintegro içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e5205-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5205-142">Yapılandırma ve Azure AD çoklu oturum açma Abintegro ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5205-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5205-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e5205-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e5205-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e5205-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5205-145">**[Bir Abintegro test kullanıcısı oluşturma](#creating-an-abintegro-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Abintegro sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e5205-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5205-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e5205-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5205-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5205-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5205-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e5205-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5205-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Abintegro uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5205-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="e5205-150">**Azure AD çoklu oturum açma ile Abintegro yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5205-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="e5205-151">Azure portalında üzerinde **Abintegro** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e5205-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e5205-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e5205-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="e5205-155">Üzerinde **Abintegro etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5205-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="e5205-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="e5205-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5205-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="e5205-158">This value is not real.</span></span> <span data-ttu-id="e5205-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5205-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e5205-160">Kişi [Abintegro istemci destek ekibi](mailto:support@abintegro.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="e5205-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="e5205-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e5205-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="e5205-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5205-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5205-165">Çoklu oturum açma yapılandırmak için **Abintegro** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Abintegro destek ekibi](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="e5205-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="e5205-166">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e5205-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e5205-167">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e5205-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5205-168">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e5205-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5205-169">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5205-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5205-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5205-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5205-171">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e5205-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e5205-173">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5205-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5205-174">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e5205-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5205-176">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e5205-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5205-178">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e5205-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5205-180">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5205-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5205-182">a.</span><span class="sxs-lookup"><span data-stu-id="e5205-182">a.</span></span> <span data-ttu-id="e5205-183">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5205-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5205-184">b.</span><span class="sxs-lookup"><span data-stu-id="e5205-184">b.</span></span> <span data-ttu-id="e5205-185">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e5205-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5205-186">c.</span><span class="sxs-lookup"><span data-stu-id="e5205-186">c.</span></span> <span data-ttu-id="e5205-187">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e5205-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e5205-188">d.</span><span class="sxs-lookup"><span data-stu-id="e5205-188">d.</span></span> <span data-ttu-id="e5205-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5205-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="e5205-190">Bir Abintegro test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5205-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="e5205-191">Kullanıcı için Abintegro hazırlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e5205-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="e5205-192">Atanmış bir kullanıcı erişim paneli kullanılarak Abintegro oturum açmaya çalıştığında Abintegro kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="e5205-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="e5205-193">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Abintegro tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5205-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e5205-194">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e5205-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e5205-195">Bu bölümde, Britta Abintegro için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5205-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e5205-197">**Abintegro için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5205-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="e5205-198">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e5205-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e5205-200">Uygulamalar listesinde **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="e5205-200">In the applications list, select **Abintegro**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="e5205-202">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e5205-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e5205-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5205-204">Click **Add** button.</span></span> <span data-ttu-id="e5205-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5205-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e5205-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e5205-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e5205-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5205-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5205-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5205-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5205-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e5205-210">Testing single sign-on</span></span>

<span data-ttu-id="e5205-211">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e5205-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e5205-212">Erişim paneli Abintegro parçasında tıkladığınızda, oturum açma sayfasına Abintegro uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5205-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="e5205-213">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5205-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e5205-214">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5205-214">Additional resources</span></span>

* [<span data-ttu-id="e5205-215">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e5205-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5205-216">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e5205-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

