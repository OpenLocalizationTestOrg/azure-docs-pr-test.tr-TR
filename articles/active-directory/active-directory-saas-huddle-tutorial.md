---
title: "Öğretici: Azure Active Directory Tümleştirme ile Huddle | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Huddle arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="29881-103">Öğretici: Azure Active Directory Tümleştirme Huddle ile</span><span class="sxs-lookup"><span data-stu-id="29881-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="29881-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Huddle tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="29881-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29881-105">Huddle Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="29881-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29881-106">Huddle erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="29881-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="29881-107">Otomatik olarak için Huddle (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="29881-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29881-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="29881-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="29881-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29881-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29881-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="29881-110">Prerequisites</span></span>

<span data-ttu-id="29881-111">Azure AD tümleştirme Huddle ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="29881-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="29881-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="29881-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29881-113">Bir Huddle çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="29881-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29881-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="29881-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29881-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="29881-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29881-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="29881-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29881-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29881-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29881-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="29881-118">Scenario description</span></span>

<span data-ttu-id="29881-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="29881-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29881-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="29881-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29881-121">Galeriden Huddle ekleme</span><span class="sxs-lookup"><span data-stu-id="29881-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="29881-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="29881-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="29881-123">Galeriden Huddle ekleme</span><span class="sxs-lookup"><span data-stu-id="29881-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="29881-124">Azure AD'ye Huddle tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Huddle eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="29881-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29881-125">**Galeriden Huddle eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="29881-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29881-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="29881-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29881-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="29881-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29881-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="29881-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="29881-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29881-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="29881-133">Arama kutusuna **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="29881-133">In the search box, type **Huddle**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="29881-135">Sonuçlar panelinde seçin **Huddle**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29881-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29881-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="29881-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="29881-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Huddle ile test etme</span><span class="sxs-lookup"><span data-stu-id="29881-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29881-139">Tekli çalışmaya oturum için Azure AD Huddle karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="29881-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="29881-140">Diğer bir deyişle, bir Azure AD kullanıcısının Huddle ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29881-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="29881-141">Huddle içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="29881-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="29881-142">Yapılandırma ve Azure AD çoklu oturum açma Huddle ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="29881-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29881-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="29881-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="29881-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="29881-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="29881-145">**[Huddle test kullanıcısı oluşturma](#creating-a-huddle-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Huddle sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="29881-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="29881-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="29881-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="29881-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="29881-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29881-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="29881-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29881-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Huddle uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="29881-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="29881-150">**Azure AD çoklu oturum açma ile Huddle yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="29881-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="29881-151">Azure portalında üzerinde **Huddle** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="29881-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="29881-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="29881-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="29881-155">Üzerinde **Huddle etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="29881-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="29881-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="29881-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29881-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="29881-158">This value is not real.</span></span> <span data-ttu-id="29881-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="29881-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="29881-160">Kişi [Huddle istemci destek ekibi](https://huddle.zendesk.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="29881-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="29881-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="29881-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="29881-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29881-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29881-165">Üzerinde **Huddle yapılandırma** 'yi tıklatın **yapılandırma Huddle** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="29881-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29881-166">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="29881-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="29881-168">Çoklu oturum açma Huddle tarafında yapılandırmak için indirilen Gönder gereksinim **sertifika**, **SAML çoklu oturum açma hizmet URL'si**, ve **SAML varlık kimliği** için [ İstemci destek ekibi huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="29881-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="29881-169">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="29881-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="29881-170">Çoklu oturum açma Huddle destek ekibi tarafından etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="29881-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="29881-171">Yapılandırma tamamlandığında, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="29881-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="29881-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="29881-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29881-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="29881-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29881-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29881-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29881-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="29881-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="29881-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="29881-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="29881-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="29881-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29881-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="29881-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29881-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="29881-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29881-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="29881-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29881-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="29881-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29881-187">a.</span><span class="sxs-lookup"><span data-stu-id="29881-187">a.</span></span> <span data-ttu-id="29881-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29881-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29881-189">b.</span><span class="sxs-lookup"><span data-stu-id="29881-189">b.</span></span> <span data-ttu-id="29881-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="29881-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29881-191">c.</span><span class="sxs-lookup"><span data-stu-id="29881-191">c.</span></span> <span data-ttu-id="29881-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="29881-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="29881-193">d.</span><span class="sxs-lookup"><span data-stu-id="29881-193">d.</span></span> <span data-ttu-id="29881-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="29881-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="29881-195">Huddle test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="29881-195">Creating a Huddle test user</span></span>

<span data-ttu-id="29881-196">Azure AD kullanıcıları için Huddle oturum açmak etkinleştirmek için bunların Huddle sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="29881-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="29881-197">Huddle söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="29881-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="29881-198">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="29881-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="29881-199">Oturum, **Huddle** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="29881-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="29881-200">Tıklatın **çalışma**.</span><span class="sxs-lookup"><span data-stu-id="29881-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="29881-201">Tıklatın **kişiler \> kişileri davet edin**.</span><span class="sxs-lookup"><span data-stu-id="29881-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="29881-202">![Kişiler](./media/active-directory-saas-huddle-tutorial/IC787838.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="29881-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="29881-203">İçinde **yeni bir davet oluşturma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="29881-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="29881-204">![Yeni davet](./media/active-directory-saas-huddle-tutorial/IC787839.png "yeni davet")</span><span class="sxs-lookup"><span data-stu-id="29881-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="29881-205">a.</span><span class="sxs-lookup"><span data-stu-id="29881-205">a.</span></span> <span data-ttu-id="29881-206">İçinde **katılmaya kişileri davet etmek için bir takım seçin** listesinde **takım**.</span><span class="sxs-lookup"><span data-stu-id="29881-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="29881-207">b.</span><span class="sxs-lookup"><span data-stu-id="29881-207">b.</span></span> <span data-ttu-id="29881-208">Türü **e-posta adresi** geçerli bir Azure AD hesabının içinde sağlamak **Enter e-posta adresi davet etmek istediğiniz kişiler için** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="29881-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="29881-209">c.</span><span class="sxs-lookup"><span data-stu-id="29881-209">c.</span></span> <span data-ttu-id="29881-210">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="29881-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="29881-211">Azure AD hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="29881-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="29881-212">Azure AD kullanıcı hesaplarını sağlamak için herhangi bir Huddle kullanıcı hesabı oluşturma araçlarını veya Huddle tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29881-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="29881-213">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="29881-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="29881-214">Bu bölümde, Britta Huddle için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="29881-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="29881-216">**Huddle için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="29881-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="29881-217">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="29881-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="29881-219">Uygulamalar listesinde **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="29881-219">In the applications list, select **Huddle**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="29881-221">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="29881-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="29881-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29881-223">Click **Add** button.</span></span> <span data-ttu-id="29881-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="29881-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="29881-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="29881-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29881-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="29881-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29881-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="29881-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29881-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="29881-229">Testing single sign-on</span></span>

<span data-ttu-id="29881-230">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="29881-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29881-231">Erişim paneli Huddle parçasında tıkladığınızda, oturum açma sayfasına Huddle uygulamasının otomatik olarak almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="29881-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="29881-232">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29881-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29881-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="29881-233">Additional resources</span></span>

* [<span data-ttu-id="29881-234">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="29881-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29881-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="29881-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
