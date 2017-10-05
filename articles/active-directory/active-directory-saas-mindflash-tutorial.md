---
title: "Öğretici: Azure Active Directory Tümleştirme ile Mindflash | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Mindflash arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="ad482-103">Öğretici: Azure Active Directory Tümleştirme Mindflash ile</span><span class="sxs-lookup"><span data-stu-id="ad482-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="ad482-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Mindflash tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ad482-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad482-105">Mindflash Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ad482-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ad482-106">Mindflash erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ad482-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="ad482-107">Otomatik olarak için Mindflash (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ad482-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad482-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ad482-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ad482-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad482-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad482-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ad482-110">Prerequisites</span></span>

<span data-ttu-id="ad482-111">Azure AD tümleştirme Mindflash ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad482-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="ad482-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ad482-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad482-113">Bir Mindflash çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ad482-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad482-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ad482-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad482-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad482-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad482-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ad482-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad482-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad482-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad482-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ad482-118">Scenario description</span></span>
<span data-ttu-id="ad482-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ad482-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad482-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ad482-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad482-121">Galeriden Mindflash ekleme</span><span class="sxs-lookup"><span data-stu-id="ad482-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="ad482-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ad482-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="ad482-123">Galeriden Mindflash ekleme</span><span class="sxs-lookup"><span data-stu-id="ad482-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="ad482-124">Azure AD Mindflash tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Mindflash eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad482-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ad482-125">**Galeriden Mindflash eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ad482-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ad482-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ad482-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad482-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ad482-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ad482-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ad482-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ad482-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ad482-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ad482-133">Arama kutusuna **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="ad482-133">In the search box, type **Mindflash**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="ad482-135">Sonuçlar panelinde seçin **Mindflash**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ad482-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad482-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ad482-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad482-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Mindflash sınayın.</span><span class="sxs-lookup"><span data-stu-id="ad482-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad482-139">Tekli çalışmaya oturum için Azure AD Mindflash karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ad482-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="ad482-140">Diğer bir deyişle, bir Azure AD kullanıcısının Mindflash ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad482-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="ad482-141">Mindflash içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ad482-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ad482-142">Yapılandırma ve Azure AD çoklu oturum açma Mindflash ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad482-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ad482-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ad482-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ad482-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ad482-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad482-145">**[Mindflash test kullanıcısı oluşturma](#creating-a-mindflash-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Mindflash sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ad482-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad482-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ad482-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad482-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ad482-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad482-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ad482-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad482-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Mindflash uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ad482-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="ad482-150">**Azure AD çoklu oturum açma ile Mindflash yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ad482-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="ad482-151">Azure portalında üzerinde **Mindflash** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ad482-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ad482-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ad482-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="ad482-155">Üzerinde **Mindflash etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ad482-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="ad482-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad482-157">a.</span></span> <span data-ttu-id="ad482-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="ad482-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="ad482-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad482-159">b.</span></span> <span data-ttu-id="ad482-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="ad482-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad482-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="ad482-161">These values are not real.</span></span> <span data-ttu-id="ad482-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad482-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ad482-163">Kişi [Mindflash istemci destek ekibi](https://www.mindflash.com/contact/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="ad482-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="ad482-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad482-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="ad482-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ad482-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad482-168">Çoklu oturum açma yapılandırmak için **Mindflash** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Mindflash destek ekibi](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ad482-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="ad482-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ad482-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ad482-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ad482-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ad482-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad482-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad482-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad482-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad482-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ad482-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ad482-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ad482-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ad482-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ad482-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad482-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ad482-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad482-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="ad482-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad482-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ad482-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad482-184">a.</span><span class="sxs-lookup"><span data-stu-id="ad482-184">a.</span></span> <span data-ttu-id="ad482-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad482-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad482-186">b.</span><span class="sxs-lookup"><span data-stu-id="ad482-186">b.</span></span> <span data-ttu-id="ad482-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ad482-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad482-188">c.</span><span class="sxs-lookup"><span data-stu-id="ad482-188">c.</span></span> <span data-ttu-id="ad482-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ad482-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ad482-190">d.</span><span class="sxs-lookup"><span data-stu-id="ad482-190">d.</span></span> <span data-ttu-id="ad482-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ad482-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="ad482-192">Mindflash test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad482-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="ad482-193">Azure AD kullanıcıların Mindflash oturum etkinleştirmek için bunların Mindflash sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ad482-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="ad482-194">Mindflash söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="ad482-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="ad482-195">Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ad482-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="ad482-196">Oturum, **Mindflash** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="ad482-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="ad482-197">Git **kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="ad482-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="ad482-198">![Kullanıcıları yönetme](./media/active-directory-saas-mindflash-tutorial/ic787140.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="ad482-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="ad482-199">Tıklatın **Kullanıcı Ekle**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="ad482-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="ad482-200">İçinde **yeni kullanıcı Ekle** bölümünde, geçerli bir Azure aşağıdaki adımları gerçekleştirin sağlamak istediğiniz AD hesabı:</span><span class="sxs-lookup"><span data-stu-id="ad482-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="ad482-201">![Yeni kullanıcı ekleme](./media/active-directory-saas-mindflash-tutorial/ic787141.png "yeni kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="ad482-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="ad482-202">a.</span><span class="sxs-lookup"><span data-stu-id="ad482-202">a.</span></span> <span data-ttu-id="ad482-203">İçinde **ad** metin kutusuna, türü **ad** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ad482-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="ad482-204">b.</span><span class="sxs-lookup"><span data-stu-id="ad482-204">b.</span></span> <span data-ttu-id="ad482-205">İçinde **Soyadı** metin kutusuna, türü **Soyadı** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad482-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="ad482-206">c.</span><span class="sxs-lookup"><span data-stu-id="ad482-206">c.</span></span> <span data-ttu-id="ad482-207">İçinde **e-posta** metin kutusuna, türü **e-posta adresi** kullanıcının  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ad482-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="ad482-208">b.</span><span class="sxs-lookup"><span data-stu-id="ad482-208">b.</span></span> <span data-ttu-id="ad482-209">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ad482-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="ad482-210">API sağlama AAD kullanıcı hesaplarına Mindflash tarafından sağlanan veya herhangi diğer Mindflash kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad482-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ad482-211">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ad482-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ad482-212">Bu bölümde, Britta Mindflash için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad482-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ad482-214">**Mindflash için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ad482-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="ad482-215">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ad482-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ad482-217">Uygulamalar listesinde **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="ad482-217">In the applications list, select **Mindflash**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="ad482-219">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ad482-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ad482-221">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ad482-221">Click **Add** button.</span></span> <span data-ttu-id="ad482-222">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ad482-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ad482-224">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ad482-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ad482-225">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ad482-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad482-226">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ad482-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad482-227">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ad482-227">Testing single sign-on</span></span>

<span data-ttu-id="ad482-228">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ad482-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ad482-229">Erişim paneli Mindflash parçasında tıkladığınızda, oturum açma sayfasına Mindflash uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad482-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="ad482-230">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad482-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad482-231">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ad482-231">Additional resources</span></span>

* [<span data-ttu-id="ad482-232">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ad482-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad482-233">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ad482-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

