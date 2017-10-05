---
title: "Öğretici: Azure Active Directory Tümleştirme Uyarlamalı Suite ile | Microsoft Docs"
description: "Çoklu oturum açma Uyarlamalı Suite ile Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="ba940-103">Öğretici: Azure Active Directory Tümleştirme Uyarlamalı Suite ile</span><span class="sxs-lookup"><span data-stu-id="ba940-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="ba940-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Uyarlamalı Suite tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ba940-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba940-105">Uyarlamalı Suite Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ba940-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ba940-106">Uyarlamalı Suite erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ba940-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="ba940-107">Azure AD hesaplarına otomatik olarak Uyarlamalı paketine (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ba940-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba940-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ba940-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ba940-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba940-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba940-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ba940-110">Prerequisites</span></span>

<span data-ttu-id="ba940-111">Azure AD tümleştirme Uyarlamalı paketiyle yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba940-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="ba940-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ba940-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba940-113">Bir Uyarlamalı Suite çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="ba940-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba940-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ba940-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba940-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba940-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba940-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ba940-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba940-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba940-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba940-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ba940-118">Scenario description</span></span>
<span data-ttu-id="ba940-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ba940-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba940-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ba940-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba940-121">Galeriden Uyarlamalı paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="ba940-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="ba940-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ba940-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="ba940-123">Galeriden Uyarlamalı paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="ba940-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="ba940-124">Azure AD Uyarlamalı Suite tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Uyarlamalı paketi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba940-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ba940-125">**Galeriden Uyarlamalı paketi eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba940-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ba940-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ba940-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba940-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ba940-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ba940-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ba940-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ba940-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba940-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ba940-133">Arama kutusuna **Uyarlamalı Suite**.</span><span class="sxs-lookup"><span data-stu-id="ba940-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="ba940-135">Sonuçlar panelinde seçin **Uyarlamalı Suite**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba940-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba940-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ba940-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba940-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Uyarlamalı "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Suite ile test etme</span><span class="sxs-lookup"><span data-stu-id="ba940-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ba940-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Uyarlamalı grubundaki bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ba940-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="ba940-140">Diğer bir deyişle, bir Azure AD kullanıcısının Uyarlamalı paketindeki ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba940-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="ba940-141">Uyarlamalı paketindeki değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ba940-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ba940-142">Yapılandırma ve Azure AD çoklu oturum açma Uyarlamalı Suite ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba940-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ba940-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ba940-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ba940-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ba940-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba940-145">**[Uyarlamalı Suite test kullanıcısı oluşturma](#creating-an-adaptive-suite-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Uyarlamalı Suite sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ba940-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba940-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ba940-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba940-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ba940-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba940-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba940-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba940-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Uyarlamalı Suite uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ba940-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="ba940-150">**Azure AD çoklu oturum açma Uyarlamalı paketiyle yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba940-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="ba940-151">Azure portalında üzerinde **Uyarlamalı Suite** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ba940-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ba940-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ba940-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="ba940-155">Üzerinde **Uyarlamalı Suite etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba940-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="ba940-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="ba940-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="ba940-158">Bu değer Uyarlamalı paketinden 's alabilir **SAML SSO ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="ba940-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="ba940-159">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ba940-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="ba940-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba940-161">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba940-163">Üzerinde **Uyarlamalı paketi yapılandırma** 'yi tıklatın **yapılandırma Uyarlamalı Suite** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ba940-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ba940-164">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="ba940-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="ba940-166">Farklı web tarayıcısı penceresinde Uyarlamalı Suite şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ba940-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="ba940-167">Git **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="ba940-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="ba940-168">![Yönetici](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="ba940-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="ba940-169">İçinde **kullanıcılar ve roller** 'yi tıklatın **SAML SSO ayarları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="ba940-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="ba940-170">![SAML SSO ayarlarını Yönet](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO ayarlarını yönet")</span><span class="sxs-lookup"><span data-stu-id="ba940-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="ba940-171">Üzerinde **SAML SSO ayarları** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba940-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="ba940-172">![SAML SSO ayarları](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO ayarları")</span><span class="sxs-lookup"><span data-stu-id="ba940-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="ba940-173">a.</span><span class="sxs-lookup"><span data-stu-id="ba940-173">a.</span></span> <span data-ttu-id="ba940-174">İçinde **kimlik sağlayıcı adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="ba940-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="ba940-175">b.</span><span class="sxs-lookup"><span data-stu-id="ba940-175">b.</span></span> <span data-ttu-id="ba940-176">Yapıştır **SAML varlık kimliği** değeri kopyalanan Azure portalından **kimlik sağlayıcısı varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ba940-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="ba940-177">c.</span><span class="sxs-lookup"><span data-stu-id="ba940-177">c.</span></span> <span data-ttu-id="ba940-178">Yapıştır **SAML çoklu oturum açma hizmet URL'si** değeri kopyalanan Azure portalından **kimlik sağlayıcısı SSO URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ba940-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="ba940-179">d.</span><span class="sxs-lookup"><span data-stu-id="ba940-179">d.</span></span> <span data-ttu-id="ba940-180">Yapıştır **SAML çoklu oturum açma hizmet URL'si** değeri kopyalanan Azure portalından **özel oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ba940-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="ba940-181">e.</span><span class="sxs-lookup"><span data-stu-id="ba940-181">e.</span></span> <span data-ttu-id="ba940-182">İndirilen sertifikanızı karşıya yüklemek için tıklayın **dosya**.</span><span class="sxs-lookup"><span data-stu-id="ba940-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="ba940-183">f.</span><span class="sxs-lookup"><span data-stu-id="ba940-183">f.</span></span> <span data-ttu-id="ba940-184">İçin aşağıdakileri seçin:</span><span class="sxs-lookup"><span data-stu-id="ba940-184">Select the following, for:</span></span>
    * <span data-ttu-id="ba940-185">**SAML kullanıcı kimliği**seçin **Uyarlamalı Öngörüler kullanıcının adını**.</span><span class="sxs-lookup"><span data-stu-id="ba940-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="ba940-186">**SAML kullanıcı kimliği konumu**seçin **NameID, konu kullanıcı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="ba940-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="ba940-187">**SAML NameID biçimi**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="ba940-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="ba940-188">**SAML'yi etkinleştir**seçin **izin SAML SSO ve doğrudan Uyarlamalı Öngörüler oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ba940-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="ba940-189">g.</span><span class="sxs-lookup"><span data-stu-id="ba940-189">g.</span></span> <span data-ttu-id="ba940-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba940-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ba940-191">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ba940-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ba940-192">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ba940-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ba940-193">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba940-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba940-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba940-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba940-195">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ba940-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ba940-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba940-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ba940-198">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ba940-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba940-200">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ba940-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba940-202">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="ba940-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba940-204">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba940-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba940-206">a.</span><span class="sxs-lookup"><span data-stu-id="ba940-206">a.</span></span> <span data-ttu-id="ba940-207">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba940-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba940-208">b.</span><span class="sxs-lookup"><span data-stu-id="ba940-208">b.</span></span> <span data-ttu-id="ba940-209">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ba940-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba940-210">c.</span><span class="sxs-lookup"><span data-stu-id="ba940-210">c.</span></span> <span data-ttu-id="ba940-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ba940-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ba940-212">d.</span><span class="sxs-lookup"><span data-stu-id="ba940-212">d.</span></span> <span data-ttu-id="ba940-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba940-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="ba940-214">Uyarlamalı Suite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba940-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="ba940-215">Uyarlamalı paketine oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar Uyarlamalı paketine sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ba940-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="ba940-216">Uyarlamalı söz konusu olduğunda, sağlama el ile bir görev paketidir.</span><span class="sxs-lookup"><span data-stu-id="ba940-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="ba940-217">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba940-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="ba940-218">Oturum, **Uyarlamalı Suite** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="ba940-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="ba940-219">Git **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="ba940-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="ba940-220">![Yönetici](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="ba940-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="ba940-221">İçinde **kullanıcılar ve roller** 'yi tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ba940-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="ba940-222">![Kullanıcı ekleme](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="ba940-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="ba940-223">İçinde **yeni kullanıcı** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba940-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ba940-224">![Gönderme](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Gönder")</span><span class="sxs-lookup"><span data-stu-id="ba940-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="ba940-225">a.</span><span class="sxs-lookup"><span data-stu-id="ba940-225">a.</span></span> <span data-ttu-id="ba940-226">Tür **adı**, **oturum açma**, **e-posta**, **parola** istediğiniz ilgili metin kutularına sağlamayı geçerli bir Azure Active Directory kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="ba940-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="ba940-227">b.</span><span class="sxs-lookup"><span data-stu-id="ba940-227">b.</span></span> <span data-ttu-id="ba940-228">Seçin bir **rol**.</span><span class="sxs-lookup"><span data-stu-id="ba940-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="ba940-229">c.</span><span class="sxs-lookup"><span data-stu-id="ba940-229">c.</span></span> <span data-ttu-id="ba940-230">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="ba940-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="ba940-231">API sağlama AAD kullanıcı hesaplarına Uyarlamalı paketi tarafından sağlanan veya herhangi diğer Uyarlamalı Suite kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba940-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ba940-232">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ba940-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ba940-233">Bu bölümde, Uyarlamalı paketine erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ba940-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ba940-235">**Uyarlamalı paketine Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba940-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="ba940-236">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ba940-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ba940-238">Uygulamalar listesinde **Uyarlamalı Suite**.</span><span class="sxs-lookup"><span data-stu-id="ba940-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="ba940-240">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ba940-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ba940-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba940-242">Click **Add** button.</span></span> <span data-ttu-id="ba940-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ba940-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ba940-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ba940-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ba940-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ba940-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba940-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ba940-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba940-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ba940-248">Testing single sign-on</span></span>

<span data-ttu-id="ba940-249">Bu bölümün amacı erişim paneli kullanılarak Microsoft Azure AD çoklu oturum açma yapılandırmanızı test sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="ba940-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="ba940-250">Erişim paneli Uyarlamalı Suite parçasında tıklattığınızda, otomatik olarak Uyarlamalı Suite uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="ba940-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ba940-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ba940-251">Additional resources</span></span>

* [<span data-ttu-id="ba940-252">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ba940-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba940-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ba940-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

