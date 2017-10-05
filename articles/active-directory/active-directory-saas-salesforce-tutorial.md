---
title: "Öğretici: Azure Active Directory Tümleştirme Salesforce ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Salesforce arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="2c2f8-103">Öğretici: Salesforce Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="2c2f8-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="2c2f8-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Salesforce tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c2f8-105">Salesforce Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2c2f8-106">Salesforce erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2c2f8-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="2c2f8-107">Otomatik olarak Salesforce (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2c2f8-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2c2f8-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2c2f8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2c2f8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2c2f8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c2f8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2c2f8-110">Prerequisites</span></span>

<span data-ttu-id="2c2f8-111">Azure AD tümleştirme Salesforce ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="2c2f8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2c2f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2c2f8-113">Bir Salesforce çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="2c2f8-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2c2f8-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2c2f8-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2c2f8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2c2f8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c2f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2c2f8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2c2f8-118">Scenario description</span></span>
<span data-ttu-id="2c2f8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2c2f8-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c2f8-121">Salesforce Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="2c2f8-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="2c2f8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2c2f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="2c2f8-123">Salesforce Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="2c2f8-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="2c2f8-124">Azure AD Salesforce tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Salesforce eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2c2f8-125">**Salesforce Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2c2f8-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2c2f8-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2c2f8-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2c2f8-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2c2f8-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2c2f8-133">Arama kutusuna **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-133">In the search box, type **Salesforce**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="2c2f8-135">Sonuçlar panelinde seçin **Salesforce**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2c2f8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2c2f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2c2f8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Salesforce ile test etme</span><span class="sxs-lookup"><span data-stu-id="2c2f8-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2c2f8-139">Tekli çalışmaya oturum için Azure AD Salesforce karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="2c2f8-140">Diğer bir deyişle, bir Azure AD kullanıcısının Salesforce ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="2c2f8-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Salesforce içinde.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="2c2f8-142">Yapılandırma ve Azure AD çoklu oturum açma Salesforce ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2c2f8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2c2f8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2c2f8-145">**[Salesforce test kullanıcısı oluşturma](#creating-a-salesforce-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Salesforce sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2c2f8-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c2f8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2c2f8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2c2f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2c2f8-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Salesforce uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="2c2f8-150">**Azure AD çoklu oturum açma ile Salesforce yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2c2f8-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="2c2f8-151">Azure portalında üzerinde **Salesforce** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2c2f8-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="2c2f8-155">Üzerinde **Salesforce etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="2c2f8-157">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="2c2f8-158">Kurumsal hesap:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2c2f8-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="2c2f8-159">Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2c2f8-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2c2f8-160">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-160">These values are not the real.</span></span> <span data-ttu-id="2c2f8-161">Bu değerleri gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="2c2f8-162">Kişi [Salesforce istemci destek ekibi](https://help.salesforce.com/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="2c2f8-163">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="2c2f8-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2c2f8-167">Üzerinde **Salesforce yapılandırma** 'yi tıklatın **yapılandırma Salesforce** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2c2f8-168">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2c2f8-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="2c2f8-169">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="2c2f8-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="2c2f8-170">Tarayıcı ve günlüğüne Salesforce yönetici hesabınız için yeni bir sekme açın.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="2c2f8-171">Altında **yönetici** Gezinti bölmesinde, tıklatın **güvenlik denetimleri** ilgili bölümü genişletin.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="2c2f8-172">Ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-172">Then click **Single Sign-On Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="2c2f8-174">Üzerinde **çoklu oturum açma ayarları** sayfasında, **Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="2c2f8-175">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="2c2f8-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="2c2f8-176">Salesforce hesabınız için çoklu oturum açma ayarlarını etkinleştirmek erişemiyorsanız başvurmanız gerekebilir [Salesforce istemci destek ekibi](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="2c2f8-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="2c2f8-177">Seçin **SAML etkin**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="2c2f8-179">SAML çoklu oturum açma ayarlarınızı yapılandırmak için tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="2c2f8-181">Üzerinde **SAML çoklu oturum açma ayarını Düzenle** sayfasında, aşağıdaki yapılandırmaları yapın:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="2c2f8-183">a.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-183">a.</span></span> <span data-ttu-id="2c2f8-184">İçin **adı** alanına, bu yapılandırma için bir kolay ad yazın.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="2c2f8-185">İçin bir değer sağlama **adı** otomatik olarak doldurulması **API adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="2c2f8-186">b.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-186">b.</span></span> <span data-ttu-id="2c2f8-187">Yapıştır **SMAL varlık kimliği** içine değer **veren** Salesforce alanındaki.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="2c2f8-188">c.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-188">c.</span></span> <span data-ttu-id="2c2f8-189">İçinde **varlık kimliği textbox**, şu biçimi kullanarak Salesforce etki alanı adınızı yazın:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="2c2f8-190">Kurumsal hesap:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2c2f8-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="2c2f8-191">Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2c2f8-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="2c2f8-192">d.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-192">d.</span></span> <span data-ttu-id="2c2f8-193">Tıklatın **Gözat** veya **Dosya Seç** açmak için **karşıya yüklenecek dosyayı Seç** iletişim kutusunda, Salesforce sertifikanızı seçin ve ardından **açmak** sertifikayı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="2c2f8-194">e.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-194">e.</span></span> <span data-ttu-id="2c2f8-195">İçin **SAML kimlik türü**seçin **onaylamayı kullanıcının salesforce.com kullanıcı adını içeren**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="2c2f8-196">f.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-196">f.</span></span> <span data-ttu-id="2c2f8-197">İçin **SAML kimlik konumu**seçin **kimliktir konu deyiminin NameIdentifier öğesi**</span><span class="sxs-lookup"><span data-stu-id="2c2f8-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="2c2f8-198">g.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-198">g.</span></span> <span data-ttu-id="2c2f8-199">Yapıştır **çoklu oturum açma hizmet URL'si** içine **kimlik sağlayıcısı oturum açma URL'si** Salesforce alanındaki.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="2c2f8-200">h.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-200">h.</span></span> <span data-ttu-id="2c2f8-201">İçin **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="2c2f8-202">ı.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-202">i.</span></span> <span data-ttu-id="2c2f8-203">Son olarak, tıklatın **kaydetmek** , SAML çoklu oturum açma ayarları uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="2c2f8-204">Salesforce sol gezinti bölmesinde üzerinde tıklatın **etki alanı yönetimi** ilgili bölümü genişletin ve ardından **My etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="2c2f8-206">Ekranı aşağı kaydırarak **kimlik doğrulama Yapılandırması** bölüm ve'ı tıklatın **Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="2c2f8-208">İçinde **kimlik doğrulama hizmeti** bölümünde, SAML SSO yapılandırmanızı kolay adını seçin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="2c2f8-210">Birden fazla kimlik doğrulama hizmeti seçili ise, kullanıcıların bunlar çoklu oturum açma Salesforce ortamınıza başlatma sırasında oturum açmak istiyor hangi kimlik doğrulama hizmeti seçmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="2c2f8-211">Bunu olmasını istemiyorsanız sonra yapmanız gerekenler **diğer tüm kimlik doğrulama hizmetleri işaretlemeden bırakın**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="2c2f8-212">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2c2f8-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2c2f8-213">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2c2f8-214">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2c2f8-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2c2f8-215">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c2f8-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="2c2f8-216">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2c2f8-218">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2c2f8-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2c2f8-219">Sol gezinti bölmesindeki **Azure portal**, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2c2f8-221">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2c2f8-223">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2c2f8-225">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2c2f8-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2c2f8-227">a.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-227">a.</span></span> <span data-ttu-id="2c2f8-228">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2c2f8-229">b.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-229">b.</span></span> <span data-ttu-id="2c2f8-230">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2c2f8-231">c.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-231">c.</span></span> <span data-ttu-id="2c2f8-232">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2c2f8-233">d.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-233">d.</span></span> <span data-ttu-id="2c2f8-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="2c2f8-235">Salesforce test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c2f8-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="2c2f8-236">Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce'ta oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="2c2f8-237">Salesforce yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="2c2f8-238">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-238">There is no action item for you in this section.</span></span> <span data-ttu-id="2c2f8-239">Bir kullanıcı zaten Salesforce'ta yoksa, Salesforce erişmeyi denediğinde yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2c2f8-240">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2c2f8-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2c2f8-241">Bu bölümde, Britta Salesforce erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2c2f8-243">**Salesforce Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2c2f8-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="2c2f8-244">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2c2f8-246">Uygulamalar listesinde **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-246">In the applications list, select **Salesforce**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="2c2f8-248">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2c2f8-250">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-250">Click **Add** button.</span></span> <span data-ttu-id="2c2f8-251">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2c2f8-253">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2c2f8-254">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2c2f8-255">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2c2f8-256">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2c2f8-256">Testing single sign-on</span></span>

<span data-ttu-id="2c2f8-257">Çoklu oturum açma ayarlarınızı sınamak için adresinden erişim Paneli'nde açın [https://myapps.microsoft.com](https://myapps.microsoft.com/), test hesaba oturum ve tıklatın **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="2c2f8-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c2f8-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2c2f8-258">Additional resources</span></span>

* [<span data-ttu-id="2c2f8-259">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="2c2f8-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c2f8-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2c2f8-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2c2f8-261">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2c2f8-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

