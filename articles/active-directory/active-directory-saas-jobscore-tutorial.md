---
title: "Öğretici: Azure Active Directory Tümleştirme ile JobScore | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile JobScore arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed2d362f7b027bfdc38ba2fdaa03948ff5632c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="f8c8c-103">Öğretici: Azure Active Directory Tümleştirme JobScore ile</span><span class="sxs-lookup"><span data-stu-id="f8c8c-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="f8c8c-104">Bu öğreticide, Azure Active Directory (Azure AD) ile JobScore tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8c8c-105">JobScore Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f8c8c-106">JobScore erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f8c8c-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="f8c8c-107">Otomatik olarak için JobScore (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f8c8c-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8c8c-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f8c8c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f8c8c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8c8c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8c8c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f8c8c-110">Prerequisites</span></span>

<span data-ttu-id="f8c8c-111">Azure AD tümleştirme JobScore ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="f8c8c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f8c8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8c8c-113">Bir JobScore çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f8c8c-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8c8c-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8c8c-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8c8c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8c8c-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8c8c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8c8c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f8c8c-118">Scenario description</span></span>
<span data-ttu-id="f8c8c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8c8c-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8c8c-121">Galeriden JobScore ekleme</span><span class="sxs-lookup"><span data-stu-id="f8c8c-121">Adding JobScore from the gallery</span></span>
2. <span data-ttu-id="f8c8c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f8c8c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="f8c8c-123">Galeriden JobScore ekleme</span><span class="sxs-lookup"><span data-stu-id="f8c8c-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="f8c8c-124">Azure AD JobScore tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden JobScore eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f8c8c-125">**Galeriden JobScore eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f8c8c-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f8c8c-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8c8c-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f8c8c-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f8c8c-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f8c8c-133">Arama kutusuna **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-133">In the search box, type **JobScore**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="f8c8c-135">Sonuçlar panelinde seçin **JobScore**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8c8c-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f8c8c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8c8c-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı JobScore ile test etme</span><span class="sxs-lookup"><span data-stu-id="f8c8c-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8c8c-139">Tekli çalışmaya oturum için Azure AD JobScore karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="f8c8c-140">Diğer bir deyişle, bir Azure AD kullanıcısının JobScore ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="f8c8c-141">JobScore içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f8c8c-142">Yapılandırma ve Azure AD çoklu oturum açma JobScore ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f8c8c-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f8c8c-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8c8c-145">**[JobScore test kullanıcısı oluşturma](#creating-a-jobscore-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı JobScore sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8c8c-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8c8c-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8c8c-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f8c8c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8c8c-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma JobScore uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="f8c8c-150">**Azure AD çoklu oturum açma ile JobScore yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f8c8c-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="f8c8c-151">Azure portalında üzerinde **JobScore** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f8c8c-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="f8c8c-155">Üzerinde **JobScore etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-155">On the **JobScore Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="f8c8c-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="f8c8c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8c8c-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-158">This value is not real.</span></span> <span data-ttu-id="f8c8c-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f8c8c-160">Kişi [JobScore istemci destek ekibi](mailto:support@jobscore.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span></span> 
 
4. <span data-ttu-id="f8c8c-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="f8c8c-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8c8c-165">Çoklu oturum açma yapılandırmak için **JobScore** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [JobScore destek ekibi](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="f8c8c-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="f8c8c-166">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f8c8c-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f8c8c-167">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f8c8c-168">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8c8c-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8c8c-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8c8c-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8c8c-170">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f8c8c-172">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f8c8c-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f8c8c-173">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8c8c-175">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8c8c-177">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8c8c-179">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f8c8c-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8c8c-181">a.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-181">a.</span></span> <span data-ttu-id="f8c8c-182">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8c8c-183">b.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-183">b.</span></span> <span data-ttu-id="f8c8c-184">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8c8c-185">c.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-185">c.</span></span> <span data-ttu-id="f8c8c-186">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f8c8c-187">d.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-187">d.</span></span> <span data-ttu-id="f8c8c-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="f8c8c-189">JobScore test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8c8c-189">Creating a JobScore test user</span></span>

<span data-ttu-id="f8c8c-190">Bu bölümde, JobScore içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="f8c8c-191">Çalışmak [JobScore destek ekibi](mailto:support@jobscore.com) JobScore platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f8c8c-192">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f8c8c-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f8c8c-193">Bu bölümde, Britta JobScore için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f8c8c-195">**JobScore için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f8c8c-195">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="f8c8c-196">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f8c8c-198">Uygulamalar listesinde **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-198">In the applications list, select **JobScore**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="f8c8c-200">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f8c8c-202">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-202">Click **Add** button.</span></span> <span data-ttu-id="f8c8c-203">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f8c8c-205">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f8c8c-206">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8c8c-207">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8c8c-208">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f8c8c-208">Testing single sign-on</span></span>

<span data-ttu-id="f8c8c-209">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f8c8c-210">Erişim paneli JobScore parçasında tıklattığınızda, otomatik olarak JobScore uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="f8c8c-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8c8c-211">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f8c8c-211">Additional resources</span></span>

* [<span data-ttu-id="f8c8c-212">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f8c8c-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8c8c-213">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f8c8c-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

