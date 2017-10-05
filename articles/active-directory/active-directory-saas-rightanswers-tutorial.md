---
title: "Öğretici: Azure Active Directory Tümleştirme ile RightAnswers | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile RightAnswers arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e5985831598a0e5b1277d2c6cd02b03c919aad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="76e3d-103">Öğretici: Azure Active Directory Tümleştirme RightAnswers ile</span><span class="sxs-lookup"><span data-stu-id="76e3d-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="76e3d-104">Bu öğreticide, Azure Active Directory (Azure AD) ile RightAnswers tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="76e3d-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76e3d-105">RightAnswers Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="76e3d-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="76e3d-106">RightAnswers erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="76e3d-106">You can control in Azure AD who has access to RightAnswers</span></span>
- <span data-ttu-id="76e3d-107">Otomatik olarak için RightAnswers (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="76e3d-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76e3d-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="76e3d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="76e3d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76e3d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76e3d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="76e3d-110">Prerequisites</span></span>

<span data-ttu-id="76e3d-111">Azure AD tümleştirme RightAnswers ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="76e3d-111">To configure Azure AD integration with RightAnswers, you need the following items:</span></span>

- <span data-ttu-id="76e3d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="76e3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76e3d-113">Bir RightAnswers çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="76e3d-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76e3d-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="76e3d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76e3d-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="76e3d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76e3d-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="76e3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76e3d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76e3d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76e3d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="76e3d-118">Scenario description</span></span>
<span data-ttu-id="76e3d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="76e3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76e3d-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="76e3d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76e3d-121">Galeriden RightAnswers ekleme</span><span class="sxs-lookup"><span data-stu-id="76e3d-121">Adding RightAnswers from the gallery</span></span>
2. <span data-ttu-id="76e3d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="76e3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-the-gallery"></a><span data-ttu-id="76e3d-123">Galeriden RightAnswers ekleme</span><span class="sxs-lookup"><span data-stu-id="76e3d-123">Adding RightAnswers from the gallery</span></span>
<span data-ttu-id="76e3d-124">Azure AD RightAnswers tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden RightAnswers eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76e3d-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="76e3d-125">**Galeriden RightAnswers eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="76e3d-125">**To add RightAnswers from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="76e3d-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="76e3d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76e3d-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="76e3d-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="76e3d-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76e3d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="76e3d-133">Arama kutusuna **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-133">In the search box, type **RightAnswers**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="76e3d-135">Sonuçlar panelinde seçin **RightAnswers**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76e3d-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76e3d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="76e3d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76e3d-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı RightAnswers ile test etme</span><span class="sxs-lookup"><span data-stu-id="76e3d-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="76e3d-139">Tekli çalışmaya oturum için Azure AD RightAnswers karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="76e3d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span></span> <span data-ttu-id="76e3d-140">Diğer bir deyişle, bir Azure AD kullanıcısının RightAnswers ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="76e3d-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span></span>

<span data-ttu-id="76e3d-141">RightAnswers içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="76e3d-142">Yapılandırma ve Azure AD çoklu oturum açma RightAnswers ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="76e3d-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="76e3d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="76e3d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76e3d-145">**[RightAnswers test kullanıcısı oluşturma](#creating-a-rightanswers-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı RightAnswers sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="76e3d-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76e3d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="76e3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76e3d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="76e3d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76e3d-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma RightAnswers uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="76e3d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="76e3d-150">**Azure AD çoklu oturum açma ile RightAnswers yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="76e3d-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="76e3d-151">Azure portalında üzerinde **RightAnswers** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="76e3d-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="76e3d-155">Üzerinde **RightAnswers etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="76e3d-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="76e3d-157">a.</span><span class="sxs-lookup"><span data-stu-id="76e3d-157">a.</span></span> <span data-ttu-id="76e3d-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="76e3d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="76e3d-159">b.</span><span class="sxs-lookup"><span data-stu-id="76e3d-159">b.</span></span> <span data-ttu-id="76e3d-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="76e3d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76e3d-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="76e3d-161">These values are not real.</span></span> <span data-ttu-id="76e3d-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="76e3d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="76e3d-163">Kişi [RightAnswers istemci destek ekibi](https://www.rightanswers.com/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="76e3d-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="76e3d-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="76e3d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="76e3d-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76e3d-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76e3d-168">Çoklu oturum açma yapılandırmak için **RightAnswers** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [RightAnswers destek ekibi](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="76e3d-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="76e3d-169">Gerçek SSO yapılandırmasını yapmak RightAnswers destek ekibinize sahiptir.</span><span class="sxs-lookup"><span data-stu-id="76e3d-169">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="76e3d-170">SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="76e3d-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="76e3d-171">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="76e3d-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="76e3d-172">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="76e3d-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="76e3d-173">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76e3d-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76e3d-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="76e3d-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="76e3d-175">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="76e3d-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="76e3d-177">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="76e3d-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="76e3d-178">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="76e3d-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76e3d-180">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76e3d-182">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="76e3d-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76e3d-184">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="76e3d-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76e3d-186">a.</span><span class="sxs-lookup"><span data-stu-id="76e3d-186">a.</span></span> <span data-ttu-id="76e3d-187">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76e3d-188">b.</span><span class="sxs-lookup"><span data-stu-id="76e3d-188">b.</span></span> <span data-ttu-id="76e3d-189">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="76e3d-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76e3d-190">c.</span><span class="sxs-lookup"><span data-stu-id="76e3d-190">c.</span></span> <span data-ttu-id="76e3d-191">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="76e3d-192">d.</span><span class="sxs-lookup"><span data-stu-id="76e3d-192">d.</span></span> <span data-ttu-id="76e3d-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76e3d-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="76e3d-194">RightAnswers test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="76e3d-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="76e3d-195">Azure AD kullanıcıları için RightAnswers oturum açmak etkinleştirmek için bunların RightAnswers sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="76e3d-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="76e3d-196">Bu yüzden, hiçbir eylem öğesi sağlama RightAnswers, otomatik bir görev olduğunda.</span><span class="sxs-lookup"><span data-stu-id="76e3d-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="76e3d-197">Kullanıcıları otomatik olarak ilk tek oturum açma girişimi sırasında gerekirse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="76e3d-197">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="76e3d-198">API sağlama AAD kullanıcı hesaplarına RightAnswers tarafından sağlanan veya herhangi diğer RightAnswers kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76e3d-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="76e3d-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="76e3d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="76e3d-200">Bu bölümde, Britta RightAnswers için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="76e3d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="76e3d-202">**RightAnswers için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="76e3d-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="76e3d-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="76e3d-205">Uygulamalar listesinde **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-205">In the applications list, select **RightAnswers**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="76e3d-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="76e3d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="76e3d-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76e3d-209">Click **Add** button.</span></span> <span data-ttu-id="76e3d-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="76e3d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="76e3d-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="76e3d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="76e3d-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="76e3d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76e3d-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="76e3d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="76e3d-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="76e3d-215">Testing single sign-on</span></span>

<span data-ttu-id="76e3d-216">SSO ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="76e3d-216">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="76e3d-217">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76e3d-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="76e3d-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="76e3d-218">Additional resources</span></span>

* [<span data-ttu-id="76e3d-219">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="76e3d-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76e3d-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="76e3d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

