---
title: "Öğretici: SAP Business ByDesign Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve SAP Business ByDesign arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="384b0-103">Öğretici: SAP Business ByDesign ile Azure Active Directory tümleştirme</span><span class="sxs-lookup"><span data-stu-id="384b0-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="384b0-104">Bu öğreticide, Azure Active Directory (Azure AD) ile SAP Business ByDesign tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="384b0-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="384b0-105">SAP Business ByDesign Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="384b0-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="384b0-106">SAP Business ByDesign erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384b0-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="384b0-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için SAP Business ByDesign açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384b0-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="384b0-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="384b0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="384b0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="384b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="384b0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="384b0-110">Prerequisites</span></span>

<span data-ttu-id="384b0-111">SAP Business ByDesign ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="384b0-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="384b0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="384b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="384b0-113">Bir SAP Business ByDesign çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="384b0-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="384b0-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="384b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="384b0-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="384b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="384b0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="384b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="384b0-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="384b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="384b0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="384b0-118">Scenario description</span></span>
<span data-ttu-id="384b0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="384b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="384b0-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="384b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="384b0-121">SAP Business ByDesign Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="384b0-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="384b0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="384b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="384b0-123">SAP Business ByDesign Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="384b0-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="384b0-124">Azure AD SAP Business ByDesign tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden SAP Business ByDesign eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="384b0-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="384b0-125">**SAP Business ByDesign Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="384b0-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="384b0-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="384b0-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="384b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="384b0-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="384b0-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="384b0-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="384b0-133">Arama kutusuna **SAP Business ByDesign**seçin **SAP Business ByDesign** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="384b0-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign sonuçlar listesinde](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="384b0-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="384b0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="384b0-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SAP Business "Britta Simon" adlı bir test kullanıcı tabanlı ByDesign ile test etme.</span><span class="sxs-lookup"><span data-stu-id="384b0-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="384b0-137">Tekli çalışmaya oturum için Azure AD SAP Business ByDesign karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="384b0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="384b0-138">Diğer bir deyişle, bir Azure AD kullanıcısının SAP Business ByDesign ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="384b0-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="384b0-139">SAP Business ByDesign içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="384b0-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="384b0-140">Yapılandırma ve Azure AD çoklu oturum açma SAP Business ByDesign ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="384b0-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="384b0-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="384b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="384b0-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="384b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="384b0-143">**[SAP Business ByDesign test kullanıcısı oluşturma](#create-an-sap-business-bydesign-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı SAP Business ByDesign sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="384b0-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="384b0-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="384b0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="384b0-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="384b0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="384b0-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="384b0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="384b0-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma SAP Business ByDesign uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="384b0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="384b0-148">**Azure AD çoklu oturum açma SAP Business ByDesign ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="384b0-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="384b0-149">Azure portalında üzerinde **SAP Business ByDesign** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="384b0-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="384b0-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="384b0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="384b0-153">Üzerinde **SAP Business ByDesign etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="384b0-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![SAP Business ByDesign etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="384b0-155">a.</span><span class="sxs-lookup"><span data-stu-id="384b0-155">a.</span></span> <span data-ttu-id="384b0-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="384b0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="384b0-157">b.</span><span class="sxs-lookup"><span data-stu-id="384b0-157">b.</span></span> <span data-ttu-id="384b0-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="384b0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="384b0-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="384b0-159">These values are not real.</span></span> <span data-ttu-id="384b0-160">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="384b0-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="384b0-161">Kişi [SAP Business ByDesign istemci destek ekibi](https://www.sap.com/products/cloud-analytics.support.html) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="384b0-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="384b0-162">Üzerinde **kullanıcı öznitelikleri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="384b0-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![SAP Business ByDesign özniteliği bölümü](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="384b0-164">a.</span><span class="sxs-lookup"><span data-stu-id="384b0-164">a.</span></span> <span data-ttu-id="384b0-165">İçinde **kullanıcı tanımlayıcısı** listesinde **ExtractMailPrefix()** işlevi.</span><span class="sxs-lookup"><span data-stu-id="384b0-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="384b0-166">b.</span><span class="sxs-lookup"><span data-stu-id="384b0-166">b.</span></span> <span data-ttu-id="384b0-167">Gelen **posta** listesinde, uygulamanız için kullanmak istediğiniz kullanıcı özniteliği seçin.</span><span class="sxs-lookup"><span data-stu-id="384b0-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="384b0-168">Örneğin, EmployeeID benzersiz kullanıcı tanımlayıcısı olarak kullanmak istediğiniz ve öznitelik değeri ExtensionAttribute2 depoladığınız, ardından user.extensionattribute2 seçin.</span><span class="sxs-lookup"><span data-stu-id="384b0-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="384b0-169">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="384b0-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="384b0-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-171">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="384b0-173">Üzerinde **SAP Business ByDesign yapılandırma** 'yi tıklatın **yapılandırma SAP Business ByDesign** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="384b0-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="384b0-174">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="384b0-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAP Business ByDesign yapılandırma](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="384b0-176">Uygulamanız için yapılandırılmış SSO almak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="384b0-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="384b0-177">a.</span><span class="sxs-lookup"><span data-stu-id="384b0-177">a.</span></span> <span data-ttu-id="384b0-178">SAP Business ByDesign portalınızı yönetici haklarıyla oturum açma.</span><span class="sxs-lookup"><span data-stu-id="384b0-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="384b0-179">b.</span><span class="sxs-lookup"><span data-stu-id="384b0-179">b.</span></span> <span data-ttu-id="384b0-180">Gidin **uygulama ve kullanıcı yönetimi görevinin** tıklatıp **kimlik sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="384b0-181">c.</span><span class="sxs-lookup"><span data-stu-id="384b0-181">c.</span></span> <span data-ttu-id="384b0-182">Tıklatın **yeni kimlik sağlayıcısı** ve Azure portalından indirdiğiniz meta veri XML dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="384b0-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="384b0-183">Meta verileri içe aktararak sistem otomatik olarak gerekli imza sertifikası ve şifreleme sertifikası karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="384b0-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="384b0-185">d.</span><span class="sxs-lookup"><span data-stu-id="384b0-185">d.</span></span> <span data-ttu-id="384b0-186">Eklenecek **onaylama tüketici hizmeti URL'si** SAML isteği seçin **onaylama tüketici hizmeti URL'si dahil**.</span><span class="sxs-lookup"><span data-stu-id="384b0-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="384b0-187">e.</span><span class="sxs-lookup"><span data-stu-id="384b0-187">e.</span></span> <span data-ttu-id="384b0-188">Tıklatın **çoklu oturum açmayı etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="384b0-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="384b0-189">f.</span><span class="sxs-lookup"><span data-stu-id="384b0-189">f.</span></span> <span data-ttu-id="384b0-190">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="384b0-190">Save your changes.</span></span>
   
    <span data-ttu-id="384b0-191">g.</span><span class="sxs-lookup"><span data-stu-id="384b0-191">g.</span></span> <span data-ttu-id="384b0-192">Tıklatın **My sistem** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-192">Click the **My System** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="384b0-194">h.</span><span class="sxs-lookup"><span data-stu-id="384b0-194">h.</span></span> <span data-ttu-id="384b0-195">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, içine Azure portalından kopyalanan **Azure AD oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="384b0-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="384b0-197">ı.</span><span class="sxs-lookup"><span data-stu-id="384b0-197">i.</span></span> <span data-ttu-id="384b0-198">Kullanıcı kimliği ve parola veya SSO ile seçerek oturum açma arasında çalışan el ile seçip seçemeyeceğini belirtin **el ile kimlik sağlayıcısı seçimi**.</span><span class="sxs-lookup"><span data-stu-id="384b0-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="384b0-199">j.</span><span class="sxs-lookup"><span data-stu-id="384b0-199">j.</span></span> <span data-ttu-id="384b0-200">İçinde **SSO URL** bölümünde, çalışan oturum açmak için sistem tarafından kullanılması gereken URL'yi belirtin.</span><span class="sxs-lookup"><span data-stu-id="384b0-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="384b0-201">URL gönderilen çalışan açılır listesi için aşağıdaki seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="384b0-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="384b0-202">**SSO olmayan URL'si**</span><span class="sxs-lookup"><span data-stu-id="384b0-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="384b0-203">Sistem, yalnızca normal sistem URL çalışana gönderir.</span><span class="sxs-lookup"><span data-stu-id="384b0-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="384b0-204">Çalışan olamaz SSO kullanarak oturum açın ve parolayı kullanın veya gerekir bunun yerine sertifika.</span><span class="sxs-lookup"><span data-stu-id="384b0-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="384b0-205">**SSO URL'Sİ**</span><span class="sxs-lookup"><span data-stu-id="384b0-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="384b0-206">Sistem yalnızca SSO URL çalışana gönderir.</span><span class="sxs-lookup"><span data-stu-id="384b0-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="384b0-207">Çalışan SSO kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="384b0-207">The employee can log on using SSO.</span></span> <span data-ttu-id="384b0-208">Kimlik doğrulama isteği IDP yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="384b0-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="384b0-209">**Otomatik Seçim**</span><span class="sxs-lookup"><span data-stu-id="384b0-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="384b0-210">SSO etkin değilse, sistem çalışana normal sistem URL gönderir.</span><span class="sxs-lookup"><span data-stu-id="384b0-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="384b0-211">SSO etkin değilse, sistem çalışan bir parolaya sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="384b0-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="384b0-212">Bir parola kullanılabilir durumdaysa, SSO URL'si ve olmayan SSO URL'si çalışana gönderilir.</span><span class="sxs-lookup"><span data-stu-id="384b0-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="384b0-213">Ancak, çalışan parolası yoksa, yalnızca SSO URL çalışana gönderilir.</span><span class="sxs-lookup"><span data-stu-id="384b0-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="384b0-214">k.</span><span class="sxs-lookup"><span data-stu-id="384b0-214">k.</span></span> <span data-ttu-id="384b0-215">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="384b0-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="384b0-216">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="384b0-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="384b0-217">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="384b0-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="384b0-218">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="384b0-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="384b0-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="384b0-219">Create an Azure AD test user</span></span>

<span data-ttu-id="384b0-220">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="384b0-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="384b0-222">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="384b0-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="384b0-223">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="384b0-225">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="384b0-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="384b0-227">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="384b0-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="384b0-229">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="384b0-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="384b0-231">a.</span><span class="sxs-lookup"><span data-stu-id="384b0-231">a.</span></span> <span data-ttu-id="384b0-232">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="384b0-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="384b0-233">b.</span><span class="sxs-lookup"><span data-stu-id="384b0-233">b.</span></span> <span data-ttu-id="384b0-234">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="384b0-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="384b0-235">c.</span><span class="sxs-lookup"><span data-stu-id="384b0-235">c.</span></span> <span data-ttu-id="384b0-236">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="384b0-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="384b0-237">d.</span><span class="sxs-lookup"><span data-stu-id="384b0-237">d.</span></span> <span data-ttu-id="384b0-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="384b0-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="384b0-239">SAP Business ByDesign test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="384b0-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="384b0-240">Bu bölümde, SAP Business ByDesign Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="384b0-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="384b0-241">Lütfen çalışmak [SAP Business ByDesign istemci destek ekibi](https://www.sap.com/products/cloud-analytics.support.html) SAP Business ByDesign platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="384b0-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="384b0-242">Lütfen NameID değeri SAP Business ByDesign platform kullanıcıadı alanıyla eşleşmelidir emin olun.</span><span class="sxs-lookup"><span data-stu-id="384b0-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="384b0-243">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="384b0-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="384b0-244">Bu bölümde, SAP Business ByDesign erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="384b0-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="384b0-246">**SAP Business ByDesign Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="384b0-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="384b0-247">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="384b0-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="384b0-249">Uygulamalar listesinde **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="384b0-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![Uygulamalar listesinde SAP Business ByDesign bağlantı](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="384b0-251">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="384b0-251">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="384b0-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="384b0-253">Click **Add** button.</span></span> <span data-ttu-id="384b0-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="384b0-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="384b0-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="384b0-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="384b0-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="384b0-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="384b0-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="384b0-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="384b0-259">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="384b0-259">Test single sign-on</span></span>

<span data-ttu-id="384b0-260">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="384b0-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="384b0-261">Erişim paneli SAP Business ByDesign parçasında tıklattığınızda, otomatik olarak SAP Business ByDesign uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="384b0-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="384b0-262">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="384b0-262">Additional resources</span></span>

* [<span data-ttu-id="384b0-263">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="384b0-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="384b0-264">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="384b0-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

