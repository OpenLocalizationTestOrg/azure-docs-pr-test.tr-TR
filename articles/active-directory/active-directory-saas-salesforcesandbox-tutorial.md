---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Salesforce korumalı alan arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="9745a-103">Öğretici: Azure Active Directory Tümleştirme ile Salesforce korumalı alan</span><span class="sxs-lookup"><span data-stu-id="9745a-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="9745a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Salesforce korumalı alan tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9745a-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9745a-105">Salesforce korumalı alan Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9745a-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9745a-106">Salesforce korumalı alan erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9745a-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="9745a-107">Azure AD hesaplarına otomatik olarak Salesforce korumalı alanda (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9745a-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9745a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9745a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9745a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9745a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9745a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9745a-110">Prerequisites</span></span>

<span data-ttu-id="9745a-111">Azure AD tümleştirme Salesforce Sandbox ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="9745a-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="9745a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9745a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9745a-113">Bir Salesforce korumalı alan çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="9745a-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9745a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9745a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9745a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9745a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9745a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9745a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9745a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9745a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9745a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9745a-118">Scenario description</span></span>
<span data-ttu-id="9745a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9745a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9745a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9745a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9745a-121">Galeriden Salesforce korumalı alan ekleme</span><span class="sxs-lookup"><span data-stu-id="9745a-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="9745a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9745a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="9745a-123">Galeriden Salesforce korumalı alan ekleme</span><span class="sxs-lookup"><span data-stu-id="9745a-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="9745a-124">Azure AD Salesforce korumalı alan tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Salesforce korumalı alan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9745a-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9745a-125">**Galeriden Salesforce korumalı alan eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9745a-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9745a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9745a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9745a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9745a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9745a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9745a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9745a-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9745a-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9745a-133">Arama kutusuna **Salesforce korumalı alan**.</span><span class="sxs-lookup"><span data-stu-id="9745a-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="9745a-135">Sonuçlar panelinde seçin **Salesforce korumalı alan**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9745a-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9745a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9745a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9745a-138">Bu bölümde, yapılandırmanız ve Salesforce korumalı alan Azure AD çoklu oturum açma testiyle "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="9745a-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9745a-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Salesforce korumalı alanı içinde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="9745a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="9745a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Salesforce korumalı alan ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9745a-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="9745a-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Salesforce korumalı alanı içinde.</span><span class="sxs-lookup"><span data-stu-id="9745a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="9745a-142">Yapılandırma ve Azure AD çoklu oturum açma Salesforce korumalı alan ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9745a-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9745a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9745a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9745a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="9745a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9745a-145">**[Salesforce korumalı alan test kullanıcısı oluşturma](#creating-a-salesforce-sandbox-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Salesforce Sandbox sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="9745a-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9745a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9745a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9745a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9745a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9745a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9745a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9745a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Salesforce korumalı alan uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9745a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="9745a-150">**Azure AD çoklu oturum açma Salesforce Sandbox ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9745a-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="9745a-151">Azure portalında üzerinde **Salesforce korumalı alan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9745a-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9745a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9745a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="9745a-155">Üzerinde **Salesforce korumalı alan etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9745a-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="9745a-157">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9745a-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9745a-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="9745a-158">This value is not the real.</span></span> <span data-ttu-id="9745a-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin. Kişi [Salesforce korumalı alan istemci destek ekibi](https://help.salesforce.com/support) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="9745a-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="9745a-160">Zaten başka bir Salesforce korumalı alan örneği için çoklu oturum açmayı dizininizde yapılandırdıktan sonra yapılandırmanız da gerekir **tanımlayıcısı** aynı değere sahip **URL üzerinde oturum**.</span><span class="sxs-lookup"><span data-stu-id="9745a-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="9745a-161">**Tanımlayıcısı** alan denetleyerek bulunabilir **Göster Gelişmiş ayarları** onay kutusuna bağlı **uygulama URL'sini Yapılandır** iletişim sayfası</span><span class="sxs-lookup"><span data-stu-id="9745a-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="9745a-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9745a-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="9745a-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9745a-164">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9745a-166">Üzerinde **Salesforce korumalı alan yapılandırma** 'yi tıklatın **yapılandırma Salesforce korumalı alan** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="9745a-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9745a-167">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="9745a-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="9745a-168">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="9745a-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="9745a-169">Tarayıcınızda yeni bir sekme açın ve Salesforce korumalı alan yönetici hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9745a-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="9745a-170">Üstteki menüde tıklatın **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="9745a-170">In the menu on the top, click **Setup**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="9745a-172">Sol gezinti bölmesinde tıklayın **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="9745a-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="9745a-174">Çoklu oturum açma ayarları bölümüne aşağıdaki adımları gerçekleştirin: ![yapılandırma çoklu oturum açma](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="9745a-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="9745a-175">a.</span><span class="sxs-lookup"><span data-stu-id="9745a-175">a.</span></span>  <span data-ttu-id="9745a-176">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="9745a-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="9745a-177">b.</span><span class="sxs-lookup"><span data-stu-id="9745a-177">b.</span></span>  <span data-ttu-id="9745a-178">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9745a-178">Click **New**.</span></span>

12. <span data-ttu-id="9745a-179">SAML çoklu oturum açma ayarları bölümüne aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9745a-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="9745a-181">a.In adı metin kutusuna yapılandırma adını yazın (örneğin: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="9745a-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="9745a-182">b.</span><span class="sxs-lookup"><span data-stu-id="9745a-182">b.</span></span> <span data-ttu-id="9745a-183">Yapıştır **SMAL varlık kimliği** içine değer **veren** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9745a-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="9745a-184">c.</span><span class="sxs-lookup"><span data-stu-id="9745a-184">c.</span></span> <span data-ttu-id="9745a-185">İçinde **varlık kimliği** metin kutusuna, türü **https://test.salesforce.com** dizininize eklediğiniz ilk Salesforce korumalı alan örnek ise.</span><span class="sxs-lookup"><span data-stu-id="9745a-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="9745a-186">Salesforce korumalı alan örneği sonra için eklediyseniz **varlık kimliği** yazın **oturum üzerinde URL'si**, şu biçimde olmalıdır:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="9745a-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="9745a-187">d.</span><span class="sxs-lookup"><span data-stu-id="9745a-187">d.</span></span> <span data-ttu-id="9745a-188">Tıklatın **Gözat** indirilen sertifikayı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="9745a-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="9745a-189">e.</span><span class="sxs-lookup"><span data-stu-id="9745a-189">e.</span></span> <span data-ttu-id="9745a-190">Olarak **SAML kimlik türü**seçin **onaylamayı içeren kullanıcı nesnesinden Federasyon kimliği**.</span><span class="sxs-lookup"><span data-stu-id="9745a-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="9745a-191">f.</span><span class="sxs-lookup"><span data-stu-id="9745a-191">f.</span></span> <span data-ttu-id="9745a-192">Olarak **SAML kimlik konumu**seçin **kimliktir konu deyimi NameIdentifier öğesinde**.</span><span class="sxs-lookup"><span data-stu-id="9745a-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="9745a-193">g.</span><span class="sxs-lookup"><span data-stu-id="9745a-193">g.</span></span> <span data-ttu-id="9745a-194">Yapıştır **çoklu oturum açma hizmet URL'si** içine **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9745a-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="9745a-195">h.</span><span class="sxs-lookup"><span data-stu-id="9745a-195">h.</span></span> <span data-ttu-id="9745a-196">SAML oturum kapatma SFDC desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9745a-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="9745a-197">'Https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' geçici bir çözüm olarak Yapıştır içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9745a-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="9745a-198">ı.</span><span class="sxs-lookup"><span data-stu-id="9745a-198">i.</span></span> <span data-ttu-id="9745a-199">Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="9745a-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="9745a-200">j.</span><span class="sxs-lookup"><span data-stu-id="9745a-200">j.</span></span> <span data-ttu-id="9745a-201">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9745a-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="9745a-202">Etki alanınızı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9745a-202">Enable your domain</span></span>
<span data-ttu-id="9745a-203">Bu bölümde, bir etki alanı zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="9745a-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="9745a-204">Daha fazla bilgi için bkz: [etki alanı adınız tanımlama](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="9745a-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="9745a-205">**Etki alanınızı etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9745a-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="9745a-206">Sol gezinti bölmesinde **etki alanı yönetimi**ve ardından **My etki alanı.**</span><span class="sxs-lookup"><span data-stu-id="9745a-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="9745a-208">Lütfen etki alanınızı doğru yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9745a-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="9745a-209">İçinde **oturum açma sayfası ayarları** 'yi tıklatın **Düzenle**, daha sonra olarak **kimlik doğrulama hizmeti**, önceki bölümden oturum açma SAML tek ayar adını seçin ve son olarak tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="9745a-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="9745a-211">Yapılandırılmış bir etki alanınız hemen kullanıcılarınızın Salesforce korumalı alan oturum açma etki alanı URL'si kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9745a-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="9745a-212">URL değerini almak için önceki bölümde oluşturduğunuz SSO profili tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9745a-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="9745a-213">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9745a-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9745a-214">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="9745a-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9745a-215">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9745a-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9745a-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9745a-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="9745a-217">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="9745a-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9745a-219">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9745a-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9745a-220">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9745a-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9745a-222">Kullanıcıların listesini görüntülemek için Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9745a-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9745a-224">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9745a-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9745a-226">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9745a-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9745a-228">a.</span><span class="sxs-lookup"><span data-stu-id="9745a-228">a.</span></span> <span data-ttu-id="9745a-229">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9745a-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9745a-230">b.</span><span class="sxs-lookup"><span data-stu-id="9745a-230">b.</span></span> <span data-ttu-id="9745a-231">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9745a-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9745a-232">c.</span><span class="sxs-lookup"><span data-stu-id="9745a-232">c.</span></span> <span data-ttu-id="9745a-233">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9745a-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9745a-234">d.</span><span class="sxs-lookup"><span data-stu-id="9745a-234">d.</span></span> <span data-ttu-id="9745a-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9745a-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="9745a-236">Salesforce korumalı alan test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9745a-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="9745a-237">Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce korumalı alanda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9745a-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="9745a-238">Salesforce korumalı alan yeni saat sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="9745a-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="9745a-239">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="9745a-239">There is no action item for you in this section.</span></span> <span data-ttu-id="9745a-240">Salesforce korumalı alan erişmeyi denediğinde Salesforce korumalı alanda bir kullanıcı zaten mevcut değilse yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9745a-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9745a-241">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9745a-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9745a-242">Bu bölümde, Britta Salesforce korumalı alan için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9745a-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9745a-244">**Salesforce korumalı alan Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9745a-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="9745a-245">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9745a-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9745a-247">Uygulamalar listesinde **Salesforce korumalı alan**.</span><span class="sxs-lookup"><span data-stu-id="9745a-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="9745a-249">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9745a-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9745a-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9745a-251">Click **Add** button.</span></span> <span data-ttu-id="9745a-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9745a-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9745a-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9745a-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9745a-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9745a-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9745a-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9745a-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9745a-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9745a-257">Testing single sign-on</span></span>

<span data-ttu-id="9745a-258">SSO ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="9745a-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="9745a-259">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9745a-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9745a-260">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9745a-260">Additional resources</span></span>

* [<span data-ttu-id="9745a-261">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="9745a-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9745a-262">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9745a-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9745a-263">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="9745a-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

