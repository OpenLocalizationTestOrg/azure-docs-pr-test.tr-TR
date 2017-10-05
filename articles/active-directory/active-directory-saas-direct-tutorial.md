---
title: "Öğretici: Azure Active Directory Tümleştirme ile doğrudan | Microsoft Docs"
description: "Çoklu oturum açma ve doğrudan Azure Active Directory arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 84582492592613320bd3ec2bdffe08519852d7c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="6c952-103">Öğretici: Azure Active Directory Tümleştirme ile doğrudan</span><span class="sxs-lookup"><span data-stu-id="6c952-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="6c952-104">Bu öğreticide, doğrudan Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6c952-104">In this tutorial, you learn how to integrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c952-105">Doğrudan Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6c952-105">Integrating Direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c952-106">Doğrudan erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6c952-106">You can control in Azure AD who has access to Direct</span></span>
- <span data-ttu-id="6c952-107">Otomatik olarak (çoklu oturum açma) yönlendirmek için Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6c952-107">You can enable your users to automatically get signed-on to Direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c952-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6c952-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6c952-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c952-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c952-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6c952-110">Prerequisites</span></span>

<span data-ttu-id="6c952-111">Azure AD tümleştirme Direct ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c952-111">To configure Azure AD integration with Direct, you need the following items:</span></span>

- <span data-ttu-id="6c952-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6c952-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c952-113">Bir doğrudan çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6c952-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c952-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6c952-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c952-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c952-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c952-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6c952-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c952-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c952-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c952-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6c952-118">Scenario description</span></span>
<span data-ttu-id="6c952-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6c952-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c952-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6c952-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c952-121">Galeriden doğrudan ekleme</span><span class="sxs-lookup"><span data-stu-id="6c952-121">Adding Direct from the gallery</span></span>
2. <span data-ttu-id="6c952-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6c952-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="6c952-123">Galeriden doğrudan ekleme</span><span class="sxs-lookup"><span data-stu-id="6c952-123">Adding Direct from the gallery</span></span>
<span data-ttu-id="6c952-124">Azure AD doğrudan tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden doğrudan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c952-124">To configure the integration of Direct into Azure AD, you need to add Direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c952-125">**Galeriden doğrudan eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c952-125">**To add Direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c952-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6c952-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c952-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6c952-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c952-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6c952-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6c952-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c952-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6c952-133">Arama kutusuna **doğrudan**.</span><span class="sxs-lookup"><span data-stu-id="6c952-133">In the search box, type **Direct**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="6c952-135">Sonuçlar panelinde seçin **doğrudan**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c952-135">In the results panel, select **Direct**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c952-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6c952-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c952-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile doğrudan "Britta Simon." olarak adlandırılan bir test kullanıcı dayalı test etme</span><span class="sxs-lookup"><span data-stu-id="6c952-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6c952-139">Tekli çalışmaya oturum için Azure AD içinde karşılık gelen kullanıcı doğrudan bir kullanıcıya Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="6c952-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Direct is to a user in Azure AD.</span></span> <span data-ttu-id="6c952-140">Diğer bir deyişle, bir Azure AD kullanıcısının doğrudan ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c952-140">In other words, a link relationship between an Azure AD user and the related user in Direct needs to be established.</span></span>

<span data-ttu-id="6c952-141">Doğrudan içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6c952-141">In Direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6c952-142">Yapılandırmak ve Azure AD çoklu oturum açma ile doğrudan sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c952-142">To configure and test Azure AD single sign-on with Direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c952-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6c952-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c952-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="6c952-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c952-145">**[Doğrudan test kullanıcısı oluşturma](#creating-a-direct-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı doğrudan sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="6c952-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in Direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c952-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6c952-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c952-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6c952-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c952-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c952-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c952-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma doğrudan uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6c952-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="6c952-150">**Azure AD çoklu oturum açma ile doğrudan yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c952-150">**To configure Azure AD single sign-on with Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="6c952-151">Azure portalında üzerinde **doğrudan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6c952-151">In the Azure portal, on the **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6c952-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6c952-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="6c952-155">Üzerinde **doğrudan etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="6c952-155">On the **Direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="6c952-157">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="6c952-157">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="6c952-158">Denetleme **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="6c952-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="6c952-160">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="6c952-160">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="6c952-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6c952-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="6c952-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c952-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6c952-165">Çoklu oturum açma yapılandırmak için **doğrudan** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [doğrudan destek ekibi](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="6c952-165">To configure single sign-on on **Direct** side, you need to send the downloaded **Metadata XML** to [Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="6c952-166">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6c952-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6c952-167">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="6c952-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6c952-168">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c952-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c952-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c952-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c952-170">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6c952-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6c952-172">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c952-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c952-173">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6c952-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c952-175">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6c952-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c952-177">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="6c952-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c952-179">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c952-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c952-181">a.</span><span class="sxs-lookup"><span data-stu-id="6c952-181">a.</span></span> <span data-ttu-id="6c952-182">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c952-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c952-183">b.</span><span class="sxs-lookup"><span data-stu-id="6c952-183">b.</span></span> <span data-ttu-id="6c952-184">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6c952-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c952-185">c.</span><span class="sxs-lookup"><span data-stu-id="6c952-185">c.</span></span> <span data-ttu-id="6c952-186">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6c952-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6c952-187">d.</span><span class="sxs-lookup"><span data-stu-id="6c952-187">d.</span></span> <span data-ttu-id="6c952-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c952-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="6c952-189">Doğrudan test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c952-189">Creating a Direct test user</span></span>

<span data-ttu-id="6c952-190">Bu bölümde, doğrudan içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c952-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="6c952-191">Çalışmak [doğrudan destek ekibi](https://direct4b.com/ja/support.html#inquiry) doğrudan platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="6c952-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the Direct platform.</span></span> <span data-ttu-id="6c952-192">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="6c952-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6c952-193">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6c952-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6c952-194">Bu bölümde, Britta doğrudan erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c952-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Direct.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6c952-196">**Britta Simon doğrudan olarak atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c952-196">**To assign Britta Simon to Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="6c952-197">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6c952-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6c952-199">Uygulamalar listesinde **doğrudan**.</span><span class="sxs-lookup"><span data-stu-id="6c952-199">In the applications list, select **Direct**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="6c952-201">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6c952-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6c952-203">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c952-203">Click **Add** button.</span></span> <span data-ttu-id="6c952-204">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6c952-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6c952-206">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6c952-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6c952-207">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6c952-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c952-208">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6c952-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c952-209">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6c952-209">Testing single sign-on</span></span>

<span data-ttu-id="6c952-210">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6c952-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="6c952-211">Test isterseniz, **IDP başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="6c952-211">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="6c952-212">Tıkladığınızda **doğrudan** döşeme erişim panelinde otomatik olarak oturum açmayı almanız gerekir, **doğrudan** uygulama.</span><span class="sxs-lookup"><span data-stu-id="6c952-212">When you click the **Direct** tile in the Access Panel, you should get automatically signed-on to your **Direct** application.</span></span>

2. <span data-ttu-id="6c952-213">Test isterseniz, **SP tarafından başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="6c952-213">If you wish to test in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="6c952-214">a.</span><span class="sxs-lookup"><span data-stu-id="6c952-214">a.</span></span> <span data-ttu-id="6c952-215">Tıklayın **doğrudan** döşeme erişim panelinde ve uygulama oturum açma sayfasına yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="6c952-215">Click on the **Direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="6c952-216">b.</span><span class="sxs-lookup"><span data-stu-id="6c952-216">b.</span></span> <span data-ttu-id="6c952-217">Giriş, `subdomain` görüntülenen metin kutusu ve tuşuna '次へ (İleri)' ve otomatik olarak oturum açmayı almanız gerekir, **doğrudan** uygulama.</span><span class="sxs-lookup"><span data-stu-id="6c952-217">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **Direct** application .</span></span>
    
<span data-ttu-id="6c952-218">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c952-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c952-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6c952-219">Additional resources</span></span>

* [<span data-ttu-id="6c952-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="6c952-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c952-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6c952-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

