---
title: "Öğretici: Azure Active Directory Tümleştirme ile ThirdLight | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile ThirdLight arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="021e5-103">Öğretici: Azure Active Directory Tümleştirme ThirdLight ile</span><span class="sxs-lookup"><span data-stu-id="021e5-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="021e5-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ThirdLight tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="021e5-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="021e5-105">ThirdLight Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="021e5-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="021e5-106">ThirdLight erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="021e5-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="021e5-107">Otomatik olarak için ThirdLight (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="021e5-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="021e5-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="021e5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="021e5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="021e5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="021e5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="021e5-110">Prerequisites</span></span>

<span data-ttu-id="021e5-111">Azure AD tümleştirme ThirdLight ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="021e5-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="021e5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="021e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="021e5-113">Bir ThirdLight çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="021e5-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="021e5-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="021e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="021e5-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="021e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="021e5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="021e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="021e5-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="021e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="021e5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="021e5-118">Scenario description</span></span>
<span data-ttu-id="021e5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="021e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="021e5-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="021e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="021e5-121">Galeriden ThirdLight ekleme</span><span class="sxs-lookup"><span data-stu-id="021e5-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="021e5-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="021e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="021e5-123">Galeriden ThirdLight ekleme</span><span class="sxs-lookup"><span data-stu-id="021e5-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="021e5-124">Azure AD ThirdLight tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ThirdLight eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="021e5-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="021e5-125">**Galeriden ThirdLight eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="021e5-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="021e5-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="021e5-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="021e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="021e5-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="021e5-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="021e5-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="021e5-133">Arama kutusuna **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="021e5-133">In the search box, type **ThirdLight**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="021e5-135">Sonuçlar panelinde seçin **ThirdLight**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="021e5-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="021e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="021e5-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ThirdLight ile test etme</span><span class="sxs-lookup"><span data-stu-id="021e5-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="021e5-139">Tekli çalışmaya oturum için Azure AD ThirdLight karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="021e5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="021e5-140">Diğer bir deyişle, bir Azure AD kullanıcısının ThirdLight ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="021e5-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="021e5-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** ThirdLight içinde.</span><span class="sxs-lookup"><span data-stu-id="021e5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="021e5-142">Yapılandırma ve Azure AD çoklu oturum açma ThirdLight ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="021e5-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="021e5-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="021e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="021e5-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="021e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="021e5-145">**[ThirdLight test kullanıcısı oluşturma](#creating-a-thirdlight-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı ThirdLight sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="021e5-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="021e5-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="021e5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="021e5-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="021e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="021e5-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="021e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="021e5-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ThirdLight uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="021e5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="021e5-150">**Azure AD çoklu oturum açma ile ThirdLight yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="021e5-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="021e5-151">Azure portalında üzerinde **ThirdLight** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="021e5-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="021e5-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="021e5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="021e5-155">Üzerinde **ThirdLight etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="021e5-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="021e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="021e5-157">a.</span></span> <span data-ttu-id="021e5-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="021e5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="021e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="021e5-159">b.</span></span> <span data-ttu-id="021e5-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="021e5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="021e5-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="021e5-161">These values are not real.</span></span> <span data-ttu-id="021e5-162">Bu değerler gerçek oturum açma URL'si ve Identiifer ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="021e5-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="021e5-163">Kişi [ThirdLight istemci destek ekibi](https://www.thirdlight.com/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="021e5-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="021e5-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="021e5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="021e5-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="021e5-168">Farklı web tarayıcısı penceresinde ThirdLight şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="021e5-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="021e5-169">Git **yapılandırma \> Sistem Yönetimi**ve ardından **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="021e5-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="021e5-170">![Sistem Yönetimi](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="021e5-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="021e5-171">SAML2 yapılandırma bölümünde aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="021e5-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="021e5-172">![SAML çoklu oturum açma](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="021e5-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="021e5-173">a.</span><span class="sxs-lookup"><span data-stu-id="021e5-173">a.</span></span> <span data-ttu-id="021e5-174">Seçin **SAML2 çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="021e5-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="021e5-175">b.</span><span class="sxs-lookup"><span data-stu-id="021e5-175">b.</span></span> <span data-ttu-id="021e5-176">Olarak **IDP meta veriler için kaynak**seçin **XML yük IDP meta verilerini**.</span><span class="sxs-lookup"><span data-stu-id="021e5-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="021e5-177">c.</span><span class="sxs-lookup"><span data-stu-id="021e5-177">c.</span></span> <span data-ttu-id="021e5-178">İndirilen meta veri dosyasını açın, içeriği Kopyala ve ardından yapıştırın **IDP meta veri XML** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="021e5-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="021e5-179">d.</span><span class="sxs-lookup"><span data-stu-id="021e5-179">d.</span></span> <span data-ttu-id="021e5-180">Tıklatın **kaydetmek SAML2 ayarları**.</span><span class="sxs-lookup"><span data-stu-id="021e5-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="021e5-181">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="021e5-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="021e5-182">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="021e5-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="021e5-183">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="021e5-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="021e5-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="021e5-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="021e5-185">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="021e5-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="021e5-187">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="021e5-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="021e5-188">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="021e5-190">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="021e5-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="021e5-192">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="021e5-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="021e5-194">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="021e5-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="021e5-196">a.</span><span class="sxs-lookup"><span data-stu-id="021e5-196">a.</span></span> <span data-ttu-id="021e5-197">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="021e5-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="021e5-198">b.</span><span class="sxs-lookup"><span data-stu-id="021e5-198">b.</span></span> <span data-ttu-id="021e5-199">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="021e5-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="021e5-200">c.</span><span class="sxs-lookup"><span data-stu-id="021e5-200">c.</span></span> <span data-ttu-id="021e5-201">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="021e5-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="021e5-202">d.</span><span class="sxs-lookup"><span data-stu-id="021e5-202">d.</span></span> <span data-ttu-id="021e5-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="021e5-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="021e5-204">ThirdLight test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="021e5-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="021e5-205">Azure AD kullanıcıları için ThirdLight oturum açmak etkinleştirmek için bunların ThirdLight sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="021e5-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="021e5-206">ThirdLight söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="021e5-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="021e5-207">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="021e5-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="021e5-208">Oturum, **ThirdLight** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="021e5-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="021e5-209">Git **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="021e5-210">Seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="021e5-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="021e5-211">Tıklatın **yeni kullanıcı Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="021e5-212">Girin **kullanıcı adı, ad veya açıklama, e-posta, hazır veya yeni üyeler grup seçin** sağlamak istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="021e5-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="021e5-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="021e5-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="021e5-214">API sağlama AAD kullanıcı hesaplarına Thirdlight tarafından sağlanan veya herhangi diğer Thirdlight kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="021e5-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="021e5-215">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="021e5-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="021e5-216">Bu bölümde, Britta ThirdLight için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="021e5-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="021e5-218">**ThirdLight için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="021e5-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="021e5-219">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="021e5-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="021e5-221">Uygulamalar listesinde **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="021e5-221">In the applications list, select **ThirdLight**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="021e5-223">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="021e5-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="021e5-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="021e5-225">Click **Add** button.</span></span> <span data-ttu-id="021e5-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="021e5-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="021e5-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="021e5-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="021e5-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="021e5-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="021e5-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="021e5-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="021e5-231">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="021e5-231">Testing single sign-on</span></span>

<span data-ttu-id="021e5-232">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="021e5-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="021e5-233">Erişim paneli ThirdLight parçasında tıklattığınızda, otomatik olarak ThirdLight uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="021e5-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="021e5-234">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="021e5-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="021e5-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="021e5-235">Additional resources</span></span>

* [<span data-ttu-id="021e5-236">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="021e5-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="021e5-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="021e5-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

