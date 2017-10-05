---
title: "Öğretici: Azure Active Directory Tümleştirme ile xMatters OnDemand | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile xMatters OnDemand arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="d341f-103">Öğretici: Azure Active Directory Tümleştirme xMatters OnDemand ile</span><span class="sxs-lookup"><span data-stu-id="d341f-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="d341f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile xMatters OnDemand tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d341f-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d341f-105">XMatters OnDemand Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d341f-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d341f-106">XMatters OnDemand erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d341f-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="d341f-107">Otomatik olarak Azure AD hesaplarına sahip xMatters OnDemand (çoklu oturum açma) için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d341f-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d341f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d341f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d341f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d341f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d341f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d341f-110">Prerequisites</span></span>

<span data-ttu-id="d341f-111">Azure AD tümleştirme OnDemand xMatters ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d341f-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="d341f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d341f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d341f-113">Abonelik xMatters OnDemand çoklu oturum açma etkin</span><span class="sxs-lookup"><span data-stu-id="d341f-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d341f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d341f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d341f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d341f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d341f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d341f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d341f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d341f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d341f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d341f-118">Scenario description</span></span>
<span data-ttu-id="d341f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d341f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d341f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d341f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d341f-121">Galeriden xMatters OnDemand ekleme</span><span class="sxs-lookup"><span data-stu-id="d341f-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="d341f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d341f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="d341f-123">Galeriden xMatters OnDemand ekleme</span><span class="sxs-lookup"><span data-stu-id="d341f-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="d341f-124">Azure AD xMatters OnDemand tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden xMatters OnDemand eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d341f-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d341f-125">**Galeriden xMatters OnDemand eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d341f-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d341f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d341f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d341f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d341f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d341f-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d341f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d341f-133">Arama kutusuna **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="d341f-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="d341f-135">Sonuçlar panelinde seçin **xMatters OnDemand**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d341f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d341f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d341f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı OnDemand tabanlı xMatters ile test etme.</span><span class="sxs-lookup"><span data-stu-id="d341f-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d341f-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen kullanıcı xMatters OnDemand Azure AD'de bir kullanıcı için olduğunu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d341f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="d341f-140">Diğer bir deyişle, bir Azure AD kullanıcısının xMatters ilgili kullanıcı arasında bir bağlantı ilişkisi OnDemand kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d341f-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="d341f-141">Değeri xMatters OnDemand'da, Ata **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d341f-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d341f-142">Yapılandırma ve Azure AD çoklu oturum açma xMatters OnDemand ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d341f-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d341f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d341f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d341f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d341f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d341f-145">**[XMatters OnDemand test kullanıcısı oluşturma](#creating-a-xmatters-ondemand-test-user)**  - bir Britta Simon karşılık gelen xMatters kullanıcı Azure AD gösterimini bağlı OnDemand içinde olması.</span><span class="sxs-lookup"><span data-stu-id="d341f-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d341f-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d341f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d341f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d341f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d341f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d341f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d341f-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma xMatters OnDemand uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d341f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="d341f-150">**Azure AD çoklu oturum açma OnDemand xMatters ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d341f-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="d341f-151">Azure portalında üzerinde **xMatters OnDemand** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d341f-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d341f-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d341f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="d341f-155">Üzerinde **xMatters OnDemand etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d341f-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="d341f-157">a.</span><span class="sxs-lookup"><span data-stu-id="d341f-157">a.</span></span> <span data-ttu-id="d341f-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="d341f-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="d341f-159">b.</span><span class="sxs-lookup"><span data-stu-id="d341f-159">b.</span></span> <span data-ttu-id="d341f-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="d341f-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="d341f-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d341f-161">These values are not real.</span></span> <span data-ttu-id="d341f-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d341f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d341f-163">Kişi [xMatters OnDemand destek ekibi](https://www.xmatters.com/company/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="d341f-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="d341f-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyasını yerel olarak kaydedin **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="d341f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="d341f-166">Sertifikayı iletmek gereken [xMatters OnDemand destek ekibi](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="d341f-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="d341f-167">Tek oturum açma yapılandırmasını son haline getirmek önce xMatters destek ekibi tarafından karşıya yüklenecek sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="d341f-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="d341f-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d341f-170">Üzerinde **xMatters OnDemand yapılandırma** 'yi tıklatın **xMatters OnDemand yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d341f-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d341f-171">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d341f-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="d341f-173">Farklı web tarayıcısı penceresinde XMatters OnDemand şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d341f-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="d341f-174">Üstteki araç çubuğunda tıklatın **yönetici**ve ardından **şirket ayrıntıları** sol taraftaki gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="d341f-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="d341f-175">![Yönetici](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="d341f-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="d341f-176">Üzerinde **SAML Yapılandırması** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d341f-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="d341f-177">![SAML Yapılandırması](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="d341f-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="d341f-178">a.</span><span class="sxs-lookup"><span data-stu-id="d341f-178">a.</span></span> <span data-ttu-id="d341f-179">Seçin **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="d341f-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="d341f-180">b.</span><span class="sxs-lookup"><span data-stu-id="d341f-180">b.</span></span> <span data-ttu-id="d341f-181">Yapıştır **SAML varlık kimliği**, Azure portalından kopyalanan **kimlik sağlayıcı kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d341f-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="d341f-182">c.</span><span class="sxs-lookup"><span data-stu-id="d341f-182">c.</span></span> <span data-ttu-id="d341f-183">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan **üzerinde tek oturum URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d341f-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="d341f-184">d.</span><span class="sxs-lookup"><span data-stu-id="d341f-184">d.</span></span> <span data-ttu-id="d341f-185">Yapıştır **Sign-Out URL**, Azure portalından kopyalanan **çoklu oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d341f-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="d341f-186">e.</span><span class="sxs-lookup"><span data-stu-id="d341f-186">e.</span></span> <span data-ttu-id="d341f-187">Şirket Ayrıntıları sayfası, en üstte tıklayın **Değişiklikleri Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="d341f-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="d341f-188">![Şirket ayrıntıları](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "şirket ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="d341f-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="d341f-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d341f-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d341f-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d341f-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d341f-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d341f-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d341f-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d341f-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d341f-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d341f-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d341f-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d341f-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d341f-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d341f-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d341f-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d341f-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="d341f-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d341f-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d341f-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d341f-204">a.</span><span class="sxs-lookup"><span data-stu-id="d341f-204">a.</span></span> <span data-ttu-id="d341f-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d341f-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d341f-206">b.</span><span class="sxs-lookup"><span data-stu-id="d341f-206">b.</span></span> <span data-ttu-id="d341f-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d341f-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d341f-208">c.</span><span class="sxs-lookup"><span data-stu-id="d341f-208">c.</span></span> <span data-ttu-id="d341f-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d341f-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d341f-210">d.</span><span class="sxs-lookup"><span data-stu-id="d341f-210">d.</span></span> <span data-ttu-id="d341f-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d341f-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="d341f-212">XMatters OnDemand test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d341f-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="d341f-213">Azure AD kullanıcılarının XMatters OnDemand oturum açmayı etkinleştirmek için bunların XMatters OnDemand sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d341f-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="d341f-214">XMatters OnDemand söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d341f-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="d341f-215">Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d341f-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="d341f-216">Oturum, **XMatters OnDemand** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="d341f-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="d341f-217">Tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-217">Click **Users** tab.</span></span> <span data-ttu-id="d341f-218">ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d341f-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="d341f-219">![Kullanıcıların](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="d341f-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="d341f-220">İçinde **kullanıcı ekleme** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d341f-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d341f-221">![Kullanıcı ekleme](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="d341f-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="d341f-222">a.</span><span class="sxs-lookup"><span data-stu-id="d341f-222">a.</span></span> <span data-ttu-id="d341f-223">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="d341f-223">Select **Active**.</span></span>

    <span data-ttu-id="d341f-224">b.</span><span class="sxs-lookup"><span data-stu-id="d341f-224">b.</span></span> <span data-ttu-id="d341f-225">İçinde **kullanıcı kimliği** metin kutusuna, kullanıcının kullanıcı kimliği türü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d341f-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="d341f-226">c.</span><span class="sxs-lookup"><span data-stu-id="d341f-226">c.</span></span> <span data-ttu-id="d341f-227">İçinde **ad** metin kutusuna, adı Britta gibi kullanıcı türü.</span><span class="sxs-lookup"><span data-stu-id="d341f-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="d341f-228">d.</span><span class="sxs-lookup"><span data-stu-id="d341f-228">d.</span></span> <span data-ttu-id="d341f-229">İçinde **Soyadı** metin kutusuna, türü kullanıcının soyadını Simon gibi.</span><span class="sxs-lookup"><span data-stu-id="d341f-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="d341f-230">e.</span><span class="sxs-lookup"><span data-stu-id="d341f-230">e.</span></span> <span data-ttu-id="d341f-231">İçinde **Site** metin kutusuna, Enter geçerli Azure geçerli site için sağlamak istediğiniz AD hesabı.</span><span class="sxs-lookup"><span data-stu-id="d341f-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="d341f-232">f.</span><span class="sxs-lookup"><span data-stu-id="d341f-232">f.</span></span> <span data-ttu-id="d341f-233">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d341f-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d341f-234">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d341f-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d341f-235">Bu bölümde, Britta xMatters OnDemand erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d341f-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d341f-237">**XMatters OnDemand Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d341f-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="d341f-238">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d341f-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d341f-240">Uygulamalar listesinde **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="d341f-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="d341f-242">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d341f-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d341f-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d341f-244">Click **Add** button.</span></span> <span data-ttu-id="d341f-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d341f-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d341f-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d341f-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d341f-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d341f-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d341f-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d341f-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d341f-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d341f-250">Testing single sign-on</span></span>

<span data-ttu-id="d341f-251">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d341f-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d341f-252">Erişim paneli OnDemand parçasında xMatters tıklattığınızda, otomatik olarak, xMatters OnDemand uygulama açan.</span><span class="sxs-lookup"><span data-stu-id="d341f-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="d341f-253">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d341f-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d341f-254">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d341f-254">Additional resources</span></span>

* [<span data-ttu-id="d341f-255">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d341f-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d341f-256">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d341f-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

