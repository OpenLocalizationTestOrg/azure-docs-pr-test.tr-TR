---
title: "Öğretici: Azure Active Directory Tümleştirme Tableau sunucusuyla | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Tableau sunucusu arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="a257f-103">Öğretici: Azure Active Directory Tümleştirme Tableau sunucusuyla</span><span class="sxs-lookup"><span data-stu-id="a257f-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="a257f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Tableau Server Tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a257f-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a257f-105">Tableau Server Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a257f-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a257f-106">Tableau sunucu erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a257f-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="a257f-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) Tableau sunucuya açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a257f-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a257f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a257f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a257f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a257f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a257f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a257f-110">Prerequisites</span></span>

<span data-ttu-id="a257f-111">Azure AD tümleştirme Tableau sunucusuyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a257f-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="a257f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a257f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a257f-113">Bir Tableau Server Çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a257f-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a257f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a257f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a257f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a257f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a257f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a257f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a257f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a257f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a257f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a257f-118">Scenario description</span></span>
<span data-ttu-id="a257f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a257f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a257f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a257f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a257f-121">Galeriden Tableau sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="a257f-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="a257f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a257f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="a257f-123">Galeriden Tableau sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="a257f-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="a257f-124">Azure AD Tableau sunucu tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Tableau sunucusu eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a257f-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a257f-125">**Galeriden Tableau sunucusu eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a257f-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a257f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a257f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a257f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a257f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a257f-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a257f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a257f-133">Arama kutusuna **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="a257f-133">In the search box, type **Tableau Server**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="a257f-135">Sonuçlar panelinde seçin **Tableau Server**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a257f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a257f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a257f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tableau "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı sunucu ile test etme</span><span class="sxs-lookup"><span data-stu-id="a257f-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a257f-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Tableau Server'daki bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a257f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="a257f-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Tableau Server'daki ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a257f-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="a257f-141">Değeri Tableau Server'da atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a257f-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a257f-142">Yapılandırma ve Azure AD çoklu oturum açma Tableau sunucusu ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a257f-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a257f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a257f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a257f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="a257f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a257f-145">**[Tableau Server test kullanıcısı oluşturma](#creating-a-tableau-server-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Tableau sunucusu sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a257f-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a257f-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a257f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a257f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a257f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a257f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a257f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a257f-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Tableau Server uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a257f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="a257f-150">**Azure AD çoklu oturum açma Tableau sunucusuyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a257f-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="a257f-151">Azure portalında üzerinde **Tableau sunucu** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a257f-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a257f-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a257f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="a257f-155">Üzerinde **Tableau sunucu etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a257f-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="a257f-157">a.</span><span class="sxs-lookup"><span data-stu-id="a257f-157">a.</span></span> <span data-ttu-id="a257f-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="a257f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="a257f-159">b.</span><span class="sxs-lookup"><span data-stu-id="a257f-159">b.</span></span> <span data-ttu-id="a257f-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="a257f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="a257f-161">c.</span><span class="sxs-lookup"><span data-stu-id="a257f-161">c.</span></span> <span data-ttu-id="a257f-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="a257f-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a257f-163">Yukarıdaki değerleri gerçek değerler değildir.</span><span class="sxs-lookup"><span data-stu-id="a257f-163">The preceding values are not real values.</span></span> <span data-ttu-id="a257f-164">Daha sonra gerçek URL ve Tableau sunucu yapılandırma sayfasından tanımlayıcı değerlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a257f-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="a257f-165">Tableau sunucu uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="a257f-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a257f-166">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a257f-166">Configure the following claims for this application.</span></span> <span data-ttu-id="a257f-167">Bu öznitelik değerlerini yönetebilirsiniz **"Kullanıcı öznitelikleri"** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="a257f-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="a257f-168">Aşağıdaki ekran görüntüsünde bir örnek için aynı gösterir.</span><span class="sxs-lookup"><span data-stu-id="a257f-168">The following screenshot shows an example for the same.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="a257f-170">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, yukarıdaki resimde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a257f-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="a257f-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="a257f-171">Attribute Name</span></span> | <span data-ttu-id="a257f-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="a257f-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="a257f-173">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a257f-173">username</span></span> | <span data-ttu-id="a257f-174">*User.DisplayName*</span><span class="sxs-lookup"><span data-stu-id="a257f-174">*user.displayname*</span></span> |

    <span data-ttu-id="a257f-175">a.</span><span class="sxs-lookup"><span data-stu-id="a257f-175">a.</span></span> <span data-ttu-id="a257f-176">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a257f-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="a257f-179">b.</span><span class="sxs-lookup"><span data-stu-id="a257f-179">b.</span></span> <span data-ttu-id="a257f-180">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="a257f-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a257f-181">c.</span><span class="sxs-lookup"><span data-stu-id="a257f-181">c.</span></span> <span data-ttu-id="a257f-182">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="a257f-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a257f-183">d.</span><span class="sxs-lookup"><span data-stu-id="a257f-183">d.</span></span> <span data-ttu-id="a257f-184">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="a257f-184">Click **Ok**</span></span>


6. <span data-ttu-id="a257f-185">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a257f-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="a257f-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-187">Click **Save** button.</span></span>

    <span data-ttu-id="a257f-188">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="a257f-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="a257f-189">Uygulamanız için yapılandırılmış SSO almak için Tableau sunucu kiracınız yönetici olarak oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="a257f-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="a257f-190">a.</span><span class="sxs-lookup"><span data-stu-id="a257f-190">a.</span></span> <span data-ttu-id="a257f-191">Tableau sunucu yapılandırmasında tıklatın **SAML** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="a257f-193">b.</span><span class="sxs-lookup"><span data-stu-id="a257f-193">b.</span></span> <span data-ttu-id="a257f-194">Onay kutusunu işaretleyin **kullanım SAML çoklu oturum açma için**.</span><span class="sxs-lookup"><span data-stu-id="a257f-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="a257f-195">c.</span><span class="sxs-lookup"><span data-stu-id="a257f-195">c.</span></span> <span data-ttu-id="a257f-196">Tableau sunucu dönüşü URL — http://tableau_server gibi Tableau Server kullanıcıları erişecek URL.</span><span class="sxs-lookup"><span data-stu-id="a257f-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="a257f-197">Http://localhost kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="a257f-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="a257f-198">Bir URL sondaki eğik çizgi (örneğin, http://tableau_server/) ile kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="a257f-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="a257f-199">Kopya **Tableau sunucu dönüşü URL** ve Azure AD ile yapıştırma **oturum üzerinde URL'si** metin kutusuna **Tableau sunucu etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="a257f-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="a257f-200">d.</span><span class="sxs-lookup"><span data-stu-id="a257f-200">d.</span></span> <span data-ttu-id="a257f-201">SAML varlık kimliği — varlık kimliği Tableau Server yüklemenize IDP benzersiz olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a257f-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="a257f-202">Tableau sunucu URL'si yeniden burada isterseniz girebilirsiniz, ancak Tableau sunucu URL'si olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a257f-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="a257f-203">Kopya **SAML varlık kimliği** ve Azure AD ile yapıştırma **tanımlayıcısı** metin kutusuna **Tableau sunucu etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="a257f-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="a257f-204">e.</span><span class="sxs-lookup"><span data-stu-id="a257f-204">e.</span></span> <span data-ttu-id="a257f-205">Tıklatın **meta veri dosyası ver** ve metin düzenleyici uygulamada açın.</span><span class="sxs-lookup"><span data-stu-id="a257f-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="a257f-206">Onaylama işlemi tüketici hizmet URL'si Http Post ile bulup 0 dizin ve URL'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a257f-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="a257f-207">Artık Azure AD ile yapıştırma **yanıt URL'si** metin kutusuna **Tableau sunucu etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="a257f-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="a257f-208">f.</span><span class="sxs-lookup"><span data-stu-id="a257f-208">f.</span></span> <span data-ttu-id="a257f-209">Azure portalından indirdiğiniz, Federasyon meta veri dosyasını bulun ve bunu karşıya **SAML IDP meta veri dosyası**.</span><span class="sxs-lookup"><span data-stu-id="a257f-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="a257f-210">g.</span><span class="sxs-lookup"><span data-stu-id="a257f-210">g.</span></span> <span data-ttu-id="a257f-211">Tıklatın **Tamam** Tableau sunucu yapılandırması sayfasında düğmesini.</span><span class="sxs-lookup"><span data-stu-id="a257f-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="a257f-212">Müşteriniz Tableau Server SAML SSO yapılandırmasında herhangi bir sertifikayı karşıya yüklemek ve SSO akışında dikkate.</span><span class="sxs-lookup"><span data-stu-id="a257f-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="a257f-213">SAML Tableau sunucuda yapılandırmaya yardımcı sonra lütfen bu makalesine başvurun [yapılandırma SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="a257f-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="a257f-214">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a257f-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a257f-215">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="a257f-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a257f-216">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a257f-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a257f-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a257f-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="a257f-218">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a257f-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a257f-220">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a257f-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a257f-221">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a257f-223">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a257f-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a257f-225">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="a257f-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a257f-227">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a257f-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a257f-229">a.</span><span class="sxs-lookup"><span data-stu-id="a257f-229">a.</span></span> <span data-ttu-id="a257f-230">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a257f-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a257f-231">b.</span><span class="sxs-lookup"><span data-stu-id="a257f-231">b.</span></span> <span data-ttu-id="a257f-232">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a257f-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a257f-233">c.</span><span class="sxs-lookup"><span data-stu-id="a257f-233">c.</span></span> <span data-ttu-id="a257f-234">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a257f-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a257f-235">d.</span><span class="sxs-lookup"><span data-stu-id="a257f-235">d.</span></span> <span data-ttu-id="a257f-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a257f-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="a257f-237">Tableau Server test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a257f-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="a257f-238">Bu bölümün amacı Britta Simon Tableau Server'da adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a257f-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="a257f-239">Tableau sunucusundaki tüm kullanıcılar sağlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="a257f-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="a257f-240">Bu kullanıcı adını Azure AD özel özniteliğinde yapılandırdığınız değeri eşleşmelidir **kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="a257f-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="a257f-241">Doğru eşlemesi ile tümleştirme çalışmalıdır [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a257f-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="a257f-242">Bir kullanıcı el ile oluşturmanız gerekiyorsa, kuruluşunuzdaki Tableau sunucu yöneticisine başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a257f-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a257f-243">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a257f-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a257f-244">Bu bölümde, Britta Tableau sunucuya erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a257f-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a257f-246">**Britta Simon Tableau sunucusuna atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a257f-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="a257f-247">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a257f-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a257f-249">Uygulamalar listesinde **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="a257f-249">In the applications list, select **Tableau Server**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="a257f-251">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a257f-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a257f-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a257f-253">Click **Add** button.</span></span> <span data-ttu-id="a257f-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a257f-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a257f-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a257f-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a257f-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a257f-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a257f-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a257f-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a257f-259">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a257f-259">Testing single sign-on</span></span>

<span data-ttu-id="a257f-260">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a257f-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a257f-261">Erişim panelinde Tableau sunucu bölmesi tıklattığınızda, otomatik olarak Tableau sunucu uygulamanızı açan.</span><span class="sxs-lookup"><span data-stu-id="a257f-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="a257f-262">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a257f-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a257f-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a257f-263">Additional resources</span></span>

* [<span data-ttu-id="a257f-264">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="a257f-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a257f-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a257f-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

