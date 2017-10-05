---
title: "Öğretici: Azure Active Directory Tümleştirme ile Skillport | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Skillport arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="4c7c0-103">Öğretici: Azure Active Directory Tümleştirme Skillport ile</span><span class="sxs-lookup"><span data-stu-id="4c7c0-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="4c7c0-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Skillport tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c7c0-105">Skillport Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c7c0-106">Skillport erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4c7c0-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="4c7c0-107">Otomatik olarak için Skillport (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4c7c0-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c7c0-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4c7c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c7c0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c7c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c7c0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4c7c0-110">Prerequisites</span></span>

<span data-ttu-id="4c7c0-111">Azure AD tümleştirme Skillport ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="4c7c0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4c7c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c7c0-113">Bir Skillport çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="4c7c0-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c7c0-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c7c0-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c7c0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c7c0-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c7c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c7c0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4c7c0-118">Scenario description</span></span>
<span data-ttu-id="4c7c0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c7c0-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c7c0-121">Galeriden Skillport ekleme</span><span class="sxs-lookup"><span data-stu-id="4c7c0-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="4c7c0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4c7c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="4c7c0-123">Galeriden Skillport ekleme</span><span class="sxs-lookup"><span data-stu-id="4c7c0-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="4c7c0-124">Azure AD Skillport tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Skillport eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c7c0-125">**Galeriden Skillport eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c0-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c7c0-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c7c0-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c7c0-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4c7c0-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4c7c0-133">Arama kutusuna **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-133">In the search box, type **Skillport**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="4c7c0-135">Sonuçlar panelinde seçin **Skillport**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c7c0-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4c7c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c7c0-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Skillport sınayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c7c0-139">Tekli çalışmaya oturum için Azure AD Skillport karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="4c7c0-140">Diğer bir deyişle, bir Azure AD kullanıcısının Skillport ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="4c7c0-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Skillport içinde.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="4c7c0-142">Yapılandırma ve Azure AD çoklu oturum açma Skillport ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c7c0-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c7c0-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c7c0-145">**[Skillport test kullanıcısı oluşturma](#creating-a-skillport-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Skillport sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c7c0-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c7c0-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c7c0-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4c7c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c7c0-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Skillport uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="4c7c0-150">**Azure AD çoklu oturum açma ile Skillport yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c0-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="4c7c0-151">Azure portalında üzerinde **Skillport** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4c7c0-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="4c7c0-155">Üzerinde **Skillport etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="4c7c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-157">a.</span></span> <span data-ttu-id="4c7c0-158">İçinde **oturum açma URL'si** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="4c7c0-159">AB veri merkezi:`https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="4c7c0-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="4c7c0-160">ABD veri merkezi:`https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="4c7c0-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="4c7c0-161">b.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-161">b.</span></span> <span data-ttu-id="4c7c0-162">İçinde **yanıt URL'si** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="4c7c0-163">AB veri merkezi:`https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="4c7c0-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="4c7c0-164">ABD veri merkezi:`https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="4c7c0-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c7c0-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-165">These values are not the real.</span></span> <span data-ttu-id="4c7c0-166">Bu değerler gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="4c7c0-167">Kişi [Skillport istemci destek ekibi](https://www.skillsoft.com/contact.asp) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="4c7c0-168">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="4c7c0-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c7c0-172">Çoklu oturum açma yapılandırmak için **Skillport** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Skillport destek ekibi](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="4c7c0-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="4c7c0-173">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantısı kurar.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c7c0-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7c0-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c7c0-175">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4c7c0-177">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c0-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c7c0-178">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c7c0-180">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c7c0-182">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c7c0-184">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c7c0-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c7c0-186">a.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-186">a.</span></span> <span data-ttu-id="4c7c0-187">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c7c0-188">b.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-188">b.</span></span> <span data-ttu-id="4c7c0-189">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c7c0-190">c.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-190">c.</span></span> <span data-ttu-id="4c7c0-191">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c7c0-192">d.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-192">d.</span></span> <span data-ttu-id="4c7c0-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="4c7c0-194">Skillport test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7c0-194">Creating a Skillport test user</span></span>

<span data-ttu-id="4c7c0-195">İle iletişime geçmeniz Skillport test kullanıcı oluşturmak için [Skillport destek ekibi](https://www.skillsoft.com/contact.asp) son kullanıcı gereksinim göre birden çok iş senaryolarını sahip oldukları gibi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="4c7c0-196">Bunlar, kullanıcılarla tartışma sonra yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c7c0-197">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4c7c0-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c7c0-198">Bu bölümde, Britta Skillport için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4c7c0-200">**Skillport için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c7c0-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="4c7c0-201">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4c7c0-203">Uygulamalar listesinde **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-203">In the applications list, select **Skillport**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="4c7c0-205">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4c7c0-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-207">Click **Add** button.</span></span> <span data-ttu-id="4c7c0-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4c7c0-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c7c0-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c7c0-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c7c0-213">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4c7c0-213">Testing single sign-on</span></span>

<span data-ttu-id="4c7c0-214">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4c7c0-215">Erişim paneli Skillport parçasında tıklattığınızda, otomatik olarak Skillport uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="4c7c0-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="4c7c0-216">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4c7c0-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4c7c0-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4c7c0-217">Additional resources</span></span>

* [<span data-ttu-id="4c7c0-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4c7c0-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c7c0-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4c7c0-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

