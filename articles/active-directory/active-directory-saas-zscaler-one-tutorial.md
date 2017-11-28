---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler bir | Microsoft Docs"
description: "Çoklu oturum açma arasındaki Azure Active Directory Zscaler bir yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7d655c482a16c991a819eec84c84556d2f288a75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="c124c-103">Öğretici: Azure Active Directory Tümleştirme ile Zscaler bir</span><span class="sxs-lookup"><span data-stu-id="c124c-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="c124c-104">Bu öğreticide, Zscaler bir Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c124c-104">In this tutorial, you learn how to integrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c124c-105">Zscaler bir Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c124c-105">Integrating Zscaler One with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c124c-106">Zscaler bir erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c124c-106">You can control in Azure AD who has access to Zscaler One</span></span>
- <span data-ttu-id="c124c-107">Azure AD hesaplarına otomatik olarak Zscaler bir için (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c124c-107">You can enable your users to automatically get signed-on to Zscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c124c-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c124c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c124c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c124c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c124c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c124c-110">Prerequisites</span></span>

<span data-ttu-id="c124c-111">Azure AD tümleştirme Zscaler bir ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c124c-111">To configure Azure AD integration with Zscaler One, you need the following items:</span></span>

- <span data-ttu-id="c124c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c124c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c124c-113">Bir Zscaler bir çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c124c-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c124c-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c124c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c124c-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c124c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c124c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c124c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c124c-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c124c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c124c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c124c-118">Scenario description</span></span>
<span data-ttu-id="c124c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c124c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c124c-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c124c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c124c-121">Galeriden Zscaler bir ekleme</span><span class="sxs-lookup"><span data-stu-id="c124c-121">Adding Zscaler One from the gallery</span></span>
2. <span data-ttu-id="c124c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c124c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-the-gallery"></a><span data-ttu-id="c124c-123">Galeriden Zscaler bir ekleme</span><span class="sxs-lookup"><span data-stu-id="c124c-123">Adding Zscaler One from the gallery</span></span>
<span data-ttu-id="c124c-124">Tümleştirmesini Zscaler bir Azure AD'ye yapılandırmak için Zscaler bir Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c124c-124">To configure the integration of Zscaler One into Azure AD, you need to add Zscaler One from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c124c-125">**Galeriden Zscaler bir eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c124c-125">**To add Zscaler One from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c124c-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c124c-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c124c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c124c-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c124c-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c124c-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c124c-133">Arama kutusuna **Zscaler bir**.</span><span class="sxs-lookup"><span data-stu-id="c124c-133">In the search box, type **Zscaler One**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="c124c-135">Sonuçlar panelinde seçin **Zscaler bir**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-135">In the results panel, select **Zscaler One**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c124c-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c124c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c124c-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Zscaler "Britta Simon" adlı bir test kullanıcı tabanlı bir test.</span><span class="sxs-lookup"><span data-stu-id="c124c-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c124c-139">Tekli çalışmaya oturum için Azure AD Zscaler bir karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c124c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler One is to a user in Azure AD.</span></span> <span data-ttu-id="c124c-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Zscaler bir arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c124c-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler One needs to be established.</span></span>

<span data-ttu-id="c124c-141">Bir Zscaler içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c124c-141">In Zscaler One, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c124c-142">Yapılandırma ve Azure AD çoklu oturum açma ile Zscaler bir test etmek için aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="c124c-142">To configure and test Azure AD single sign-on with Zscaler One, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c124c-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c124c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c124c-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  - Internet Explorer proxy ayarlarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="c124c-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="c124c-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c124c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="c124c-146">**[Zscaler bir test kullanıcısı oluşturma](#creating-a-zscaler-one-test-user)**  - Zscaler kullanıcı Azure AD gösterimini bağlantılı bir Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c124c-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - to have a counterpart of Britta Simon in Zscaler One that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="c124c-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c124c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="c124c-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c124c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c124c-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c124c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c124c-150">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Zscaler bir uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c124c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="c124c-151">**Azure AD çoklu oturum açma Zscaler bir ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c124c-151">**To configure Azure AD single sign-on with Zscaler One, perform the following steps:**</span></span>

1. <span data-ttu-id="c124c-152">Azure portalında üzerinde **Zscaler bir** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c124c-152">In the Azure portal, on the **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c124c-154">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c124c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="c124c-156">Üzerinde **Zscaler bir etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-156">On the **Zscaler One Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="c124c-158">Oturum açma URL'si metin kutusuna, kullanıcılarınıza oturum açma Zscaler bir uygulamanız tarafından kullanılan URL'yi yazın.</span><span class="sxs-lookup"><span data-stu-id="c124c-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c124c-159">Bu değer gerçek oturum açma URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c124c-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c124c-160">Kişi [Zscaler bir istemci destek ekibi](https://www.zscaler.com/company/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="c124c-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

4. <span data-ttu-id="c124c-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c124c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="c124c-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c124c-165">Üzerinde **Zscaler bir yapılandırma** 'yi tıklatın **Zscaler bir yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c124c-165">On the **Zscaler One Configuration** section, click **Configure Zscaler One** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c124c-166">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c124c-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="c124c-168">Farklı web tarayıcısı penceresinde Zscaler bir şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c124c-168">In a different web browser window, log in to your Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="c124c-169">Üstteki menüde tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="c124c-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="c124c-170">![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="c124c-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="c124c-171">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="c124c-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="c124c-172">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="c124c-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="c124c-173">İçinde **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="c124c-174">![Kimlik doğrulama](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="c124c-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="c124c-175">a.</span><span class="sxs-lookup"><span data-stu-id="c124c-175">a.</span></span> <span data-ttu-id="c124c-176">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="c124c-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="c124c-177">b.</span><span class="sxs-lookup"><span data-stu-id="c124c-177">b.</span></span> <span data-ttu-id="c124c-178">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="c124c-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="c124c-179">Üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfasında, aşağıdaki adımları uygulayın ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="c124c-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="c124c-180">![Çoklu oturum açma](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="c124c-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="c124c-181">a.</span><span class="sxs-lookup"><span data-stu-id="c124c-181">a.</span></span> <span data-ttu-id="c124c-182">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **için kullanıcıların kimlik doğrulaması için gönderilir SAML portalın URL'sini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c124c-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="c124c-183">b.</span><span class="sxs-lookup"><span data-stu-id="c124c-183">b.</span></span> <span data-ttu-id="c124c-184">İçinde **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="c124c-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="c124c-185">c.</span><span class="sxs-lookup"><span data-stu-id="c124c-185">c.</span></span> <span data-ttu-id="c124c-186">İndirilen sertifikanızı karşıya yüklemek için tıklayın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="c124c-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="c124c-187">d.</span><span class="sxs-lookup"><span data-stu-id="c124c-187">d.</span></span> <span data-ttu-id="c124c-188">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="c124c-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="c124c-189">Üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="c124c-190">![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="c124c-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="c124c-191">a.</span><span class="sxs-lookup"><span data-stu-id="c124c-191">a.</span></span> <span data-ttu-id="c124c-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c124c-192">Click **Save**.</span></span>

    <span data-ttu-id="c124c-193">b.</span><span class="sxs-lookup"><span data-stu-id="c124c-193">b.</span></span> <span data-ttu-id="c124c-194">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="c124c-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="c124c-195">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c124c-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="c124c-196">Internet Explorer proxy ayarlarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="c124c-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="c124c-197">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c124c-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="c124c-198">Seçin **Internet Seçenekleri** gelen **Araçları** açılan menü **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="c124c-199">![Internet Seçenekleri](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="c124c-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="c124c-200">Tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="c124c-201">![Bağlantıları](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="c124c-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="c124c-202">Tıklatın **LAN Ayarları** açmak için **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="c124c-203">Proxy sunucu bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="c124c-204">![Proxy sunucusu](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="c124c-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="c124c-205">a.</span><span class="sxs-lookup"><span data-stu-id="c124c-205">a.</span></span> <span data-ttu-id="c124c-206">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="c124c-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="c124c-207">b.</span><span class="sxs-lookup"><span data-stu-id="c124c-207">b.</span></span> <span data-ttu-id="c124c-208">Adresi metin kutusuna yazın **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="c124c-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="c124c-209">c.</span><span class="sxs-lookup"><span data-stu-id="c124c-209">c.</span></span> <span data-ttu-id="c124c-210">Bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="c124c-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="c124c-211">d.</span><span class="sxs-lookup"><span data-stu-id="c124c-211">d.</span></span> <span data-ttu-id="c124c-212">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="c124c-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="c124c-213">e.</span><span class="sxs-lookup"><span data-stu-id="c124c-213">e.</span></span> <span data-ttu-id="c124c-214">Tıklatın **Tamam** kapatmak için **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="c124c-215">Tıklatın **Tamam** kapatmak için **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="c124c-216">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c124c-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c124c-217">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c124c-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c124c-218">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c124c-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c124c-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c124c-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="c124c-220">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c124c-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c124c-222">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c124c-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c124c-223">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c124c-225">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c124c-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c124c-227">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="c124c-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c124c-229">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c124c-231">a.</span><span class="sxs-lookup"><span data-stu-id="c124c-231">a.</span></span> <span data-ttu-id="c124c-232">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c124c-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c124c-233">b.</span><span class="sxs-lookup"><span data-stu-id="c124c-233">b.</span></span> <span data-ttu-id="c124c-234">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c124c-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c124c-235">c.</span><span class="sxs-lookup"><span data-stu-id="c124c-235">c.</span></span> <span data-ttu-id="c124c-236">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c124c-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c124c-237">d.</span><span class="sxs-lookup"><span data-stu-id="c124c-237">d.</span></span> <span data-ttu-id="c124c-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c124c-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="c124c-239">Zscaler bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c124c-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="c124c-240">Azure AD kullanıcılarının Zscaler bir oturum açmayı etkinleştirmek için bunlar Zscaler bir sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c124c-240">To enable Azure AD users to log in to Zscaler One, they must be provisioned to Zscaler One.</span></span> <span data-ttu-id="c124c-241">Bir Zscaler söz konusu olduğunda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c124c-241">In the case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="c124c-242">Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="c124c-243">Oturum, **Zscaler bir** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="c124c-243">Log in to your **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="c124c-244">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="c124c-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="c124c-245">![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="c124c-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="c124c-246">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="c124c-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="c124c-247">![Ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="c124c-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="c124c-248">İçinde **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c124c-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="c124c-249">![Ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="c124c-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="c124c-250">Kullanıcı Ekle bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c124c-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="c124c-251">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="c124c-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="c124c-252">a.</span><span class="sxs-lookup"><span data-stu-id="c124c-252">a.</span></span> <span data-ttu-id="c124c-253">Türü **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları** ve **departmanı** geçerli bir Azure AD hesabının sağlamak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="c124c-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="c124c-254">b.</span><span class="sxs-lookup"><span data-stu-id="c124c-254">b.</span></span> <span data-ttu-id="c124c-255">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c124c-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c124c-256">Azure AD kullanıcı hesaplarını sağlamak için herhangi bir Zscaler bir kullanıcı hesabı oluşturma araçlarını veya Zscaler bir tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c124c-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c124c-257">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c124c-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c124c-258">Bu bölümde, Britta Zscaler bir erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c124c-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler One.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c124c-260">**Britta Simon Zscaler bir atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c124c-260">**To assign Britta Simon to Zscaler One, perform the following steps:**</span></span>

1. <span data-ttu-id="c124c-261">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c124c-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c124c-263">Uygulamalar listesinde **Zscaler bir**.</span><span class="sxs-lookup"><span data-stu-id="c124c-263">In the applications list, select **Zscaler One**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="c124c-265">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c124c-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c124c-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c124c-267">Click **Add** button.</span></span> <span data-ttu-id="c124c-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c124c-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c124c-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c124c-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c124c-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c124c-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c124c-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c124c-273">Testing single sign-on</span></span>

<span data-ttu-id="c124c-274">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c124c-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c124c-275">Erişim panelinde Zscaler bir kutucuğa tıkladığınızda, otomatik olarak Zscaler bir uygulamanız açan.</span><span class="sxs-lookup"><span data-stu-id="c124c-275">When you click the Zscaler One tile in the Access Panel, you should get automatically signed-on to your Zscaler One application.</span></span>
<span data-ttu-id="c124c-276">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c124c-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c124c-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c124c-277">Additional resources</span></span>

* [<span data-ttu-id="c124c-278">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c124c-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c124c-279">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c124c-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

