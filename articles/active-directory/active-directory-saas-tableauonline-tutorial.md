---
title: "Öğretici: Azure Active Directory Tümleştirme Tableau Online ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Tableau çevrimiçi arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="f3329-103">Öğretici: Azure Active Directory Tümleştirme Tableau Online ile</span><span class="sxs-lookup"><span data-stu-id="f3329-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="f3329-104">Bu öğreticide, Tableau çevrimiçi Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f3329-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3329-105">Tableau çevrimiçi Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f3329-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3329-106">Tableau çevrimiçi erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f3329-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="f3329-107">Azure AD hesaplarına otomatik olarak Tableau Online'a (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f3329-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3329-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f3329-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3329-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3329-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3329-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f3329-110">Prerequisites</span></span>

<span data-ttu-id="f3329-111">Azure AD tümleştirme Tableau Online ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3329-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="f3329-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f3329-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3329-113">Bir Tableau çevrimiçi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f3329-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3329-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f3329-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3329-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3329-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3329-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f3329-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3329-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3329-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3329-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f3329-118">Scenario description</span></span>
<span data-ttu-id="f3329-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f3329-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3329-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f3329-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3329-121">Tableau çevrimiçi galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="f3329-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="f3329-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f3329-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="f3329-123">Tableau çevrimiçi galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="f3329-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="f3329-124">Azure AD Tableau Online tümleştirilmesi yapılandırmak için Tableau çevrimiçi galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3329-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3329-125">**Tableau çevrimiçi Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f3329-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3329-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f3329-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3329-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f3329-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3329-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f3329-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f3329-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f3329-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f3329-133">Arama kutusuna **Tableau çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="f3329-133">In the search box, type **Tableau Online**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="f3329-135">Sonuçlar panelinde seçin **Tableau çevrimiçi**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f3329-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3329-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f3329-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3329-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tableau "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme</span><span class="sxs-lookup"><span data-stu-id="f3329-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f3329-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Tableau çevrimiçi bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f3329-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="f3329-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Tableau çevrimiçi arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3329-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="f3329-141">Çevrimiçi Tableau olarak değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f3329-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3329-142">Yapılandırma ve Azure AD çoklu oturum açma Tableau Online ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3329-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3329-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f3329-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3329-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f3329-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3329-145">**[Tableau çevrimiçi bir test kullanıcısı oluşturma](#creating-a-tableau-online-test-user)**  - Tableau kullanıcı Azure AD gösterimini bağlantılı çevrimiçi Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f3329-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3329-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f3329-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3329-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f3329-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3329-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f3329-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3329-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Tableau çevrimiçi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f3329-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="f3329-150">**Azure AD çoklu oturum açma Tableau Online ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f3329-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="f3329-151">Azure portalında üzerinde **Tableau çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f3329-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f3329-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f3329-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="f3329-155">Üzerinde **Tableau çevrimiçi etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f3329-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="f3329-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3329-157">a.</span></span> <span data-ttu-id="f3329-158">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="f3329-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="f3329-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3329-159">b.</span></span> <span data-ttu-id="f3329-160">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="f3329-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="f3329-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f3329-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="f3329-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f3329-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3329-165">Farklı bir tarayıcı penceresinde Tableau çevrimiçi uygulamanıza oturum.</span><span class="sxs-lookup"><span data-stu-id="f3329-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="f3329-166">Git **ayarları** ve ardından **kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="f3329-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="f3329-168">SAML, altında etkinleştirmek için **kimlik doğrulama türleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f3329-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="f3329-169">Denetleme **çoklu oturum açma SAML ile** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="f3329-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="f3329-171">Kadar aşağıya kaydırın **alma meta veri dosyasına Tableau çevrimiçi** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f3329-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="f3329-172">Gözat'ı tıklatın ve Azure AD'den indirmiş meta veri dosyası içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="f3329-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="f3329-173">Ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="f3329-173">Then, click **Apply**.</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="f3329-175">İçinde **eşleşen onaylar** bölümünde, karşılık gelen kimlik sağlayıcısı onaylama adını eklemek **e-posta adresi**, **ad**, ve **Soyadı**.</span><span class="sxs-lookup"><span data-stu-id="f3329-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="f3329-176">Bu bilgiler Azure AD'den almak için:</span><span class="sxs-lookup"><span data-stu-id="f3329-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="f3329-177">a.</span><span class="sxs-lookup"><span data-stu-id="f3329-177">a.</span></span> <span data-ttu-id="f3329-178">Azure portalında geçin **Tableau çevrimiçi** uygulama tümleştirme sayfası.</span><span class="sxs-lookup"><span data-stu-id="f3329-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="f3329-179">b.</span><span class="sxs-lookup"><span data-stu-id="f3329-179">b.</span></span> <span data-ttu-id="f3329-180">Öznitelikleri bölümünde **"görüntülemek ve diğer tüm kullanıcı öznitelikleri Düzenle"** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="f3329-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="f3329-182">c.</span><span class="sxs-lookup"><span data-stu-id="f3329-182">c.</span></span> <span data-ttu-id="f3329-183">Bu öznitelikler için ad alanı değerini kopyalayın: givenname, e-posta ve aşağıdaki adımları kullanarak Soyadı:</span><span class="sxs-lookup"><span data-stu-id="f3329-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Azure AD çoklu oturum açma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="f3329-185">d.</span><span class="sxs-lookup"><span data-stu-id="f3329-185">d.</span></span> <span data-ttu-id="f3329-186">Tıklatın **user.givenname** değeri</span><span class="sxs-lookup"><span data-stu-id="f3329-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="f3329-187">e.</span><span class="sxs-lookup"><span data-stu-id="f3329-187">e.</span></span> <span data-ttu-id="f3329-188">Değerinden kopyalama **ad alanı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f3329-188">Copy the value from the **namespace** textbox.</span></span>

   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="f3329-190">f.</span><span class="sxs-lookup"><span data-stu-id="f3329-190">f.</span></span> <span data-ttu-id="f3329-191">Namesapce kopyalamak için değerler soyadını ve e-posta için yukarıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f3329-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="f3329-192">g.</span><span class="sxs-lookup"><span data-stu-id="f3329-192">g.</span></span> <span data-ttu-id="f3329-193">Tableau çevrimiçi uygulamaya geçiş yapın ve ardından ayarlamak **çevrimiçi öznitelikleri Tableau** gibi bölümünde:</span><span class="sxs-lookup"><span data-stu-id="f3329-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="f3329-194">E-posta: **posta** veya **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="f3329-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="f3329-195">Ad: **givenname**</span><span class="sxs-lookup"><span data-stu-id="f3329-195">First name: **givenname**</span></span>
     * <span data-ttu-id="f3329-196">Soyadı: **Soyadı**</span><span class="sxs-lookup"><span data-stu-id="f3329-196">Last name: **surname**</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="f3329-198">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f3329-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3329-199">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="f3329-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3329-200">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3329-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3329-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3329-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3329-202">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f3329-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f3329-204">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f3329-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3329-205">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f3329-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3329-207">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f3329-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3329-209">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="f3329-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3329-211">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f3329-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3329-213">a.</span><span class="sxs-lookup"><span data-stu-id="f3329-213">a.</span></span> <span data-ttu-id="f3329-214">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3329-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3329-215">b.</span><span class="sxs-lookup"><span data-stu-id="f3329-215">b.</span></span> <span data-ttu-id="f3329-216">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f3329-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3329-217">c.</span><span class="sxs-lookup"><span data-stu-id="f3329-217">c.</span></span> <span data-ttu-id="f3329-218">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f3329-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3329-219">d.</span><span class="sxs-lookup"><span data-stu-id="f3329-219">d.</span></span> <span data-ttu-id="f3329-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3329-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="f3329-221">Tableau çevrimiçi bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3329-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="f3329-222">Bu bölümde, Britta Simon Tableau çevrimiçi olarak adlandırılan bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f3329-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="f3329-223">Üzerinde **Tableau çevrimiçi**, tıklatın **ayarları** ve ardından **kimlik doğrulaması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f3329-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="f3329-224">Ekranı aşağı kaydırarak **Kullanıcıları Seç** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f3329-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="f3329-225">Tıklatın **kullanıcıları eklemek** ve ardından **e-posta adreslerini girin**.</span><span class="sxs-lookup"><span data-stu-id="f3329-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="f3329-227">Seçin **çoklu oturum açma (SSO) kimlik doğrulaması için kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="f3329-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="f3329-228">İçinde **e-posta adreslerini girin** textbox ekleyinbritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="f3329-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="f3329-230">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3329-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3329-231">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f3329-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3329-232">Bu bölümde, Britta Tableau Online'a erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f3329-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f3329-234">**Britta Simon Tableau Online'a atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f3329-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="f3329-235">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f3329-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f3329-237">Uygulamalar listesinde **Tableau çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="f3329-237">In the applications list, select **Tableau Online**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="f3329-239">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f3329-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f3329-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f3329-241">Click **Add** button.</span></span> <span data-ttu-id="f3329-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f3329-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f3329-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f3329-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3329-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f3329-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3329-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f3329-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3329-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f3329-247">Testing single sign-on</span></span>

<span data-ttu-id="f3329-248">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="f3329-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f3329-249">Erişim panelinde Tableau çevrimiçi kutucuğa tıkladığınızda, otomatik olarak Tableau çevrimiçi uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="f3329-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3329-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f3329-250">Additional resources</span></span>

* [<span data-ttu-id="f3329-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f3329-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3329-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f3329-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

