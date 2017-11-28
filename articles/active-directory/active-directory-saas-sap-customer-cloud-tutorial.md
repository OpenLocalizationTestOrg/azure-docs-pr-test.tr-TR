---
title: "Öğretici: Müşteri için SAP bulut Azure Active Directory Tümleştirmesi | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve SAP bulut arasında müşteri için yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="709f7-103">Öğretici: Müşteri için SAP bulut Azure Active Directory Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="709f7-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="709f7-104">Bu öğreticide, Azure Active Directory (Azure AD) ile müşteri için SAP bulut tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="709f7-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="709f7-105">Azure AD ile müşteri için SAP bulut tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="709f7-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="709f7-106">SAP buluta müşteri için erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="709f7-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="709f7-107">Otomatik olarak SAP buluta müşteri için (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="709f7-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="709f7-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="709f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="709f7-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="709f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="709f7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="709f7-110">Prerequisites</span></span>

<span data-ttu-id="709f7-111">Azure AD tümleştirmesi için müşteri SAP bulut ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="709f7-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="709f7-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="709f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="709f7-113">SAP Bulutu müşteri çoklu oturum açma için abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="709f7-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="709f7-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="709f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="709f7-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="709f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="709f7-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="709f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="709f7-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="709f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="709f7-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="709f7-118">Scenario description</span></span>
<span data-ttu-id="709f7-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="709f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="709f7-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="709f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="709f7-121">SAP bulut müşteri için Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="709f7-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="709f7-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="709f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="709f7-123">SAP bulut müşteri için Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="709f7-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="709f7-124">SAP bulut tümleştirme Azure AD'ye müşteri için yapılandırmak için SAP bulut müşteri için Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="709f7-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="709f7-125">**SAP bulut müşteri için Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="709f7-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="709f7-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="709f7-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="709f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="709f7-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="709f7-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="709f7-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="709f7-133">Arama kutusuna **müşteri için SAP bulut**.</span><span class="sxs-lookup"><span data-stu-id="709f7-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="709f7-135">Sonuçlar panelinde seçin **müşteri için SAP bulut**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="709f7-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="709f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="709f7-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SAP bulut ile "Britta Simon" adlı bir test kullanıcıya bağlı müşteri için test etme.</span><span class="sxs-lookup"><span data-stu-id="709f7-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="709f7-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen SAP bulutta müşteri için bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="709f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="709f7-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP bulutta müşteri için ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="709f7-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="709f7-141">Değeri müşteri SAP buluta atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="709f7-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="709f7-142">Yapılandırmak ve Azure AD çoklu oturum açma SAP Bulutu ile müşterinin sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="709f7-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="709f7-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="709f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="709f7-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="709f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="709f7-145">**[Müşteri test kullanıcısı için bir SAP bulut oluşturma](#creating-a-sap-cloud-for-customer-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı müşteri için SAP buluta sahip.</span><span class="sxs-lookup"><span data-stu-id="709f7-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="709f7-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="709f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="709f7-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="709f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="709f7-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="709f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="709f7-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve SAP bulut müşteri uygulaması için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="709f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="709f7-150">**Azure AD çoklu oturum açma için müşteri SAP bulut ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="709f7-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="709f7-151">Azure portalında üzerinde **SAP bulut müşteri için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="709f7-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="709f7-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="709f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="709f7-155">Üzerinde **müşteri etki alanı ve URL'ler için SAP bulut** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="709f7-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="709f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="709f7-157">a.</span></span> <span data-ttu-id="709f7-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="709f7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="709f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="709f7-159">b.</span></span> <span data-ttu-id="709f7-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="709f7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="709f7-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="709f7-161">These values are not real.</span></span> <span data-ttu-id="709f7-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="709f7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="709f7-163">Kişi [müşteri istemci destek ekibi için SAP bulut](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="709f7-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="709f7-164">Üzerinde **kullanıcı öznitelikleri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="709f7-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="709f7-166">a.</span><span class="sxs-lookup"><span data-stu-id="709f7-166">a.</span></span> <span data-ttu-id="709f7-167">İçinde **kullanıcı tanımlayıcısı** listesinde **ExtractMailPrefix()** işlevi.</span><span class="sxs-lookup"><span data-stu-id="709f7-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="709f7-168">b.</span><span class="sxs-lookup"><span data-stu-id="709f7-168">b.</span></span> <span data-ttu-id="709f7-169">Gelen **posta** listesinde, uygulamanız için kullanmak istediğiniz kullanıcı özniteliği seçin.</span><span class="sxs-lookup"><span data-stu-id="709f7-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="709f7-170">Örneğin, EmployeeID benzersiz kullanıcı tanımlayıcısı olarak kullanmak istediğiniz ve öznitelik değeri ExtensionAttribute2 depoladığınız, ardından user.extensionattribute2 seçin.</span><span class="sxs-lookup"><span data-stu-id="709f7-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="709f7-171">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="709f7-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="709f7-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-173">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="709f7-175">Üzerinde **müşteri yapılandırması için SAP bulut** 'yi tıklatın **müşteri için SAP bulut yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="709f7-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="709f7-176">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="709f7-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="709f7-178">Yapılandırılmış SSO almak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="709f7-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="709f7-179">a.</span><span class="sxs-lookup"><span data-stu-id="709f7-179">a.</span></span> <span data-ttu-id="709f7-180">Müşteri portalı yönetici haklarıyla oturum açma SAP buluta.</span><span class="sxs-lookup"><span data-stu-id="709f7-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="709f7-181">b.</span><span class="sxs-lookup"><span data-stu-id="709f7-181">b.</span></span> <span data-ttu-id="709f7-182">Gidin **uygulama ve kullanıcı yönetimi görevinin** tıklatıp **kimlik sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="709f7-183">c.</span><span class="sxs-lookup"><span data-stu-id="709f7-183">c.</span></span> <span data-ttu-id="709f7-184">Tıklatın **yeni kimlik sağlayıcısı** ve Azure portalından indirdiğiniz meta veri XML dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="709f7-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="709f7-185">Meta verileri içe aktararak sistem otomatik olarak gerekli imza sertifikası ve şifreleme sertifikası karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="709f7-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="709f7-187">d.</span><span class="sxs-lookup"><span data-stu-id="709f7-187">d.</span></span> <span data-ttu-id="709f7-188">Azure Active Directory gerekir böylece select SAML isteği onaylama tüketici hizmeti URL'si öğesinde **onaylama tüketici hizmeti URL'si dahil** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="709f7-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="709f7-189">e.</span><span class="sxs-lookup"><span data-stu-id="709f7-189">e.</span></span> <span data-ttu-id="709f7-190">Tıklatın **çoklu oturum açmayı etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="709f7-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="709f7-191">f.</span><span class="sxs-lookup"><span data-stu-id="709f7-191">f.</span></span> <span data-ttu-id="709f7-192">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="709f7-192">Save your changes.</span></span>
   
    <span data-ttu-id="709f7-193">g.</span><span class="sxs-lookup"><span data-stu-id="709f7-193">g.</span></span> <span data-ttu-id="709f7-194">Tıklatın **My sistem** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-194">Click the **My System** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="709f7-196">h.</span><span class="sxs-lookup"><span data-stu-id="709f7-196">h.</span></span> <span data-ttu-id="709f7-197">İçinde **Azure AD oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="709f7-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="709f7-199">ı.</span><span class="sxs-lookup"><span data-stu-id="709f7-199">i.</span></span> <span data-ttu-id="709f7-200">Kullanıcı kimliği ve parola veya SSO ile seçerek oturum açma arasında çalışan el ile seçip seçemeyeceğini belirtin **el ile kimlik sağlayıcısı seçimi**.</span><span class="sxs-lookup"><span data-stu-id="709f7-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="709f7-201">j.</span><span class="sxs-lookup"><span data-stu-id="709f7-201">j.</span></span> <span data-ttu-id="709f7-202">İçinde **SSO URL** bölümünde, sisteme oturum açmaya çalışanlarınız tarafından kullanılan URL'yi belirtin.</span><span class="sxs-lookup"><span data-stu-id="709f7-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="709f7-203">İçinde **URL gönderilen çalışana** listesinde, aşağıdaki seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="709f7-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="709f7-204">**SSO olmayan URL'si**</span><span class="sxs-lookup"><span data-stu-id="709f7-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="709f7-205">Sistem, yalnızca normal sistem URL çalışana gönderir.</span><span class="sxs-lookup"><span data-stu-id="709f7-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="709f7-206">Çalışan olamaz SSO kullanarak oturum açın ve parolayı kullanın veya gerekir bunun yerine sertifika.</span><span class="sxs-lookup"><span data-stu-id="709f7-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="709f7-207">**SSO URL'Sİ**</span><span class="sxs-lookup"><span data-stu-id="709f7-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="709f7-208">Sistem yalnızca SSO URL çalışana gönderir.</span><span class="sxs-lookup"><span data-stu-id="709f7-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="709f7-209">Çalışan SSO kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="709f7-209">The employee can log on using SSO.</span></span> <span data-ttu-id="709f7-210">Kimlik doğrulama isteği IDP yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="709f7-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="709f7-211">**Otomatik Seçim**</span><span class="sxs-lookup"><span data-stu-id="709f7-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="709f7-212">SSO etkin değilse, sistem çalışana normal sistem URL gönderir.</span><span class="sxs-lookup"><span data-stu-id="709f7-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="709f7-213">SSO etkin değilse, sistem çalışan bir parolaya sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="709f7-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="709f7-214">Bir parola kullanılabilir durumdaysa, SSO URL'si ve olmayan SSO URL'si çalışana gönderilir.</span><span class="sxs-lookup"><span data-stu-id="709f7-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="709f7-215">Ancak, çalışan parolası yoksa, yalnızca SSO URL çalışana gönderilir.</span><span class="sxs-lookup"><span data-stu-id="709f7-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="709f7-216">k.</span><span class="sxs-lookup"><span data-stu-id="709f7-216">k.</span></span> <span data-ttu-id="709f7-217">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="709f7-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="709f7-218">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="709f7-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="709f7-219">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="709f7-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="709f7-220">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="709f7-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="709f7-221">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="709f7-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="709f7-222">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="709f7-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="709f7-224">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="709f7-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="709f7-225">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="709f7-227">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="709f7-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="709f7-229">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="709f7-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="709f7-231">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="709f7-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="709f7-233">a.</span><span class="sxs-lookup"><span data-stu-id="709f7-233">a.</span></span> <span data-ttu-id="709f7-234">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="709f7-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="709f7-235">b.</span><span class="sxs-lookup"><span data-stu-id="709f7-235">b.</span></span> <span data-ttu-id="709f7-236">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="709f7-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="709f7-237">c.</span><span class="sxs-lookup"><span data-stu-id="709f7-237">c.</span></span> <span data-ttu-id="709f7-238">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="709f7-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="709f7-239">d.</span><span class="sxs-lookup"><span data-stu-id="709f7-239">d.</span></span> <span data-ttu-id="709f7-240">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="709f7-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="709f7-241">Müşteri test kullanıcısı için bir SAP bulut oluşturma</span><span class="sxs-lookup"><span data-stu-id="709f7-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="709f7-242">Bu bölümde, Britta Simon SAP bulutta müşteri için adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="709f7-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="709f7-243">Lütfen çalışmak [müşteri destek ekibi için SAP bulut](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) müşteri platform için SAP bulutta kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="709f7-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="709f7-244">Lütfen NameID değeri SAP bulut müşteri platform için kullanıcı adı alanıyla eşleşmelidir emin olun.</span><span class="sxs-lookup"><span data-stu-id="709f7-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="709f7-245">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="709f7-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="709f7-246">Bu bölümde, müşteri için SAP buluta erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="709f7-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="709f7-248">**Britta Simon müşteri için SAP buluta atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="709f7-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="709f7-249">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="709f7-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="709f7-251">Uygulamalar listesinde **müşteri için SAP bulut**.</span><span class="sxs-lookup"><span data-stu-id="709f7-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="709f7-253">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="709f7-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="709f7-255">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="709f7-255">Click **Add** button.</span></span> <span data-ttu-id="709f7-256">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="709f7-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="709f7-258">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="709f7-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="709f7-259">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="709f7-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="709f7-260">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="709f7-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="709f7-261">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="709f7-261">Testing single sign-on</span></span>

<span data-ttu-id="709f7-262">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="709f7-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="709f7-263">Müşteri kutucuğu erişim Paneli'nde SAP bulut tıklattığınızda, otomatik olarak SAP Bulutunuzu müşteri uygulaması için açan.</span><span class="sxs-lookup"><span data-stu-id="709f7-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="709f7-264">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="709f7-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="709f7-265">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="709f7-265">Additional resources</span></span>

* [<span data-ttu-id="709f7-266">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="709f7-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="709f7-267">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="709f7-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

