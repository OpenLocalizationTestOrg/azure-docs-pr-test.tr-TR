---
title: "Öğretici: Azure Active Directory Tümleştirme ile ITRP | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile ITRP arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="a5634-103">Öğretici: Azure Active Directory Tümleştirme ITRP ile</span><span class="sxs-lookup"><span data-stu-id="a5634-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="a5634-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ITRP tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a5634-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5634-105">ITRP Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a5634-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5634-106">ITRP erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a5634-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="a5634-107">Otomatik olarak için ITRP (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a5634-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5634-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a5634-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5634-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5634-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5634-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a5634-110">Prerequisites</span></span>

<span data-ttu-id="a5634-111">Azure AD tümleştirme ITRP ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a5634-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="a5634-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a5634-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5634-113">Bir ITRP çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a5634-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5634-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a5634-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5634-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a5634-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5634-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a5634-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5634-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5634-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5634-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a5634-118">Scenario description</span></span>
<span data-ttu-id="a5634-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a5634-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5634-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a5634-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5634-121">Galeriden ITRP ekleme</span><span class="sxs-lookup"><span data-stu-id="a5634-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="a5634-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a5634-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="a5634-123">Galeriden ITRP ekleme</span><span class="sxs-lookup"><span data-stu-id="a5634-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="a5634-124">Azure ad içinde ITRP tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ITRP eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5634-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5634-125">**Galeriden ITRP eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a5634-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5634-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a5634-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5634-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a5634-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5634-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a5634-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a5634-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5634-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a5634-133">Arama kutusuna **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="a5634-133">In the search box, type **ITRP**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="a5634-135">Sonuçlar panelinde seçin **ITRP**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5634-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5634-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a5634-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a5634-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ITRP ile test etme</span><span class="sxs-lookup"><span data-stu-id="a5634-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5634-139">Tekli çalışmaya oturum için Azure AD ITRP karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a5634-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="a5634-140">Diğer bir deyişle, bir Azure AD kullanıcısının ITRP ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5634-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="a5634-141">ITRP içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a5634-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5634-142">Yapılandırma ve Azure AD çoklu oturum açma ITRP ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a5634-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5634-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a5634-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5634-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="a5634-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5634-145">**[Test kullanıcı bir ITRP oluşturma](#creating-an-itrp-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı ITRP sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a5634-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5634-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a5634-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5634-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a5634-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5634-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a5634-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5634-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ITRP uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a5634-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="a5634-150">**Azure AD çoklu oturum açma ile ITRP yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a5634-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="a5634-151">Azure portalında üzerinde **ITRP** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a5634-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a5634-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a5634-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="a5634-155">Üzerinde **ITRP etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a5634-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="a5634-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5634-157">a.</span></span> <span data-ttu-id="a5634-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="a5634-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="a5634-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5634-159">b.</span></span> <span data-ttu-id="a5634-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="a5634-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5634-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a5634-161">These values are not real.</span></span> <span data-ttu-id="a5634-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a5634-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a5634-163">Kişi [ITRP istemci destek ekibi](https://www.itrp.com/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="a5634-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="a5634-164">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="a5634-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="a5634-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5634-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5634-168">Üzerinde **ITRP yapılandırma** 'yi tıklatın **yapılandırma ITRP** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a5634-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5634-169">Kopya **SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="a5634-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="a5634-171">Farklı web tarayıcısı penceresinde ITRP şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a5634-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="a5634-172">Üstteki araç çubuğunda tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a5634-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="a5634-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="a5634-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="a5634-174">Sol gezinti bölmesinde seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a5634-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="a5634-175">![Çoklu oturum açma](./media/active-directory-saas-itrp-tutorial/ic775571.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a5634-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="a5634-176">Çoklu oturum açma yapılandırma bölümünde aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a5634-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="a5634-177">![Çoklu oturum açma](./media/active-directory-saas-itrp-tutorial/ic775572.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a5634-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="a5634-178">![Çoklu oturum açma](./media/active-directory-saas-itrp-tutorial/ic775573.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a5634-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="a5634-179">a.</span><span class="sxs-lookup"><span data-stu-id="a5634-179">a.</span></span> <span data-ttu-id="a5634-180">Tıklatın **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="a5634-180">Click **Enable**.</span></span>

    <span data-ttu-id="a5634-181">b.</span><span class="sxs-lookup"><span data-stu-id="a5634-181">b.</span></span> <span data-ttu-id="a5634-182">İçinde **uzak oturum kapatma URL'sini** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a5634-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5634-183">c.</span><span class="sxs-lookup"><span data-stu-id="a5634-183">c.</span></span> <span data-ttu-id="a5634-184">İçinde **SAML SSO URL** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a5634-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5634-185">d.In **sertifika parmak izi** metin kutusuna, Yapıştır **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="a5634-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="a5634-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5634-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a5634-187">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a5634-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5634-188">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="a5634-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5634-189">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5634-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5634-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5634-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5634-191">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a5634-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a5634-193">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a5634-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5634-194">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a5634-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5634-196">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a5634-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5634-198">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="a5634-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5634-200">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a5634-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5634-202">a.</span><span class="sxs-lookup"><span data-stu-id="a5634-202">a.</span></span> <span data-ttu-id="a5634-203">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5634-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5634-204">b.</span><span class="sxs-lookup"><span data-stu-id="a5634-204">b.</span></span> <span data-ttu-id="a5634-205">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a5634-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5634-206">c.</span><span class="sxs-lookup"><span data-stu-id="a5634-206">c.</span></span> <span data-ttu-id="a5634-207">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a5634-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5634-208">d.</span><span class="sxs-lookup"><span data-stu-id="a5634-208">d.</span></span> <span data-ttu-id="a5634-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5634-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="a5634-210">Bir ITRP test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5634-210">Creating an ITRP test user</span></span>

<span data-ttu-id="a5634-211">ITRP için oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar içinde ITRP için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5634-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="a5634-212">ITRP söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="a5634-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="a5634-213">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a5634-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a5634-214">Oturum, **ITRP** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="a5634-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="a5634-215">Üstteki araç çubuğunda tıklatın **kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="a5634-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="a5634-216">![Yönetici](./media/active-directory-saas-itrp-tutorial/ic775575.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="a5634-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="a5634-217">Açılır menüden seçin **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="a5634-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="a5634-218">![Kişiler](./media/active-directory-saas-itrp-tutorial/ic775587.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="a5634-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="a5634-219">Tıklatın **yeni bir kişiye eklemek** ("+").</span><span class="sxs-lookup"><span data-stu-id="a5634-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="a5634-220">![Yönetici](./media/active-directory-saas-itrp-tutorial/ic775576.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="a5634-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="a5634-221">Yeni Kişi Ekle iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a5634-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="a5634-222">![Kullanıcı](./media/active-directory-saas-itrp-tutorial/ic775577.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="a5634-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="a5634-223">a.</span><span class="sxs-lookup"><span data-stu-id="a5634-223">a.</span></span> <span data-ttu-id="a5634-224">Tür **adı**, **e-posta** sağlamak istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="a5634-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="a5634-225">b.</span><span class="sxs-lookup"><span data-stu-id="a5634-225">b.</span></span> <span data-ttu-id="a5634-226">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5634-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="a5634-227">API sağlama AAD kullanıcı hesaplarına ITRP tarafından sağlanan veya herhangi diğer ITRP kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5634-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5634-228">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a5634-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5634-229">Bu bölümde, Britta ITRP için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a5634-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a5634-231">**ITRP için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a5634-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="a5634-232">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a5634-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a5634-234">Uygulamalar listesinde **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="a5634-234">In the applications list, select **ITRP**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="a5634-236">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a5634-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a5634-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5634-238">Click **Add** button.</span></span> <span data-ttu-id="a5634-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a5634-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a5634-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a5634-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5634-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a5634-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5634-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a5634-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5634-244">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a5634-244">Testing single sign-on</span></span>

<span data-ttu-id="a5634-245">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a5634-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5634-246">Erişim paneli ITRP parçasında tıklattığınızda, otomatik olarak ITRP uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="a5634-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="a5634-247">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5634-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5634-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a5634-248">Additional resources</span></span>

* [<span data-ttu-id="a5634-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="a5634-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5634-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a5634-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

