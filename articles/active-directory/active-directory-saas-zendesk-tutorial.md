---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zendesk | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Zendesk arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="4f375-103">Öğretici: Zendesk Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="4f375-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="4f375-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Zendesk tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f375-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f375-105">Zendesk Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4f375-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4f375-106">Zendesk erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4f375-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="4f375-107">Otomatik olarak için Zendesk (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4f375-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f375-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4f375-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4f375-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f375-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f375-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4f375-110">Prerequisites</span></span>

<span data-ttu-id="4f375-111">Azure AD tümleştirme Zendesk ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4f375-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="4f375-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4f375-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f375-113">Bir Zendesk çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4f375-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="4f375-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4f375-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="4f375-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4f375-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f375-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4f375-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f375-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f375-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="4f375-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4f375-118">Scenario description</span></span>
<span data-ttu-id="4f375-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4f375-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f375-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4f375-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f375-121">Galeriden Zendesk ekleme</span><span class="sxs-lookup"><span data-stu-id="4f375-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="4f375-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4f375-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="4f375-123">Galeriden Zendesk ekleme</span><span class="sxs-lookup"><span data-stu-id="4f375-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="4f375-124">Azure AD Zendesk tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Zendesk eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f375-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4f375-125">**Galeriden Zendesk eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4f375-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4f375-126">İçinde  **[Azure Portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f375-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4f375-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4f375-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4f375-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4f375-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4f375-133">Arama kutusuna **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="4f375-133">In the search box, type **Zendesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="4f375-135">Sonuçlar panelinde seçin **Zendesk**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f375-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4f375-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f375-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zendesk sınayın.</span><span class="sxs-lookup"><span data-stu-id="4f375-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f375-139">Tekli çalışmaya oturum için Azure AD Zendesk karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4f375-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="4f375-140">Diğer bir deyişle, bir Azure AD kullanıcısının Zendesk ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f375-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="4f375-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Zendesk içinde.</span><span class="sxs-lookup"><span data-stu-id="4f375-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="4f375-142">Yapılandırma ve Azure AD çoklu oturum açma Zendesk ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4f375-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4f375-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4f375-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4f375-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4f375-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f375-145">**[Zendesk test kullanıcısı oluşturma](#creating-a-zendesk-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Zendesk sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4f375-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f375-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4f375-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f375-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4f375-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f375-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4f375-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f375-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Zendesk uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4f375-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="4f375-150">**Azure AD çoklu oturum açma ile Zendesk yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4f375-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="4f375-151">Azure portalında üzerinde **Zendesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4f375-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4f375-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4f375-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="4f375-155">Üzerinde **Zendesk etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4f375-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="4f375-157">a.</span><span class="sxs-lookup"><span data-stu-id="4f375-157">a.</span></span> <span data-ttu-id="4f375-158">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="4f375-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="4f375-159">b.</span><span class="sxs-lookup"><span data-stu-id="4f375-159">b.</span></span> <span data-ttu-id="4f375-160">İçinde **tanımlayıcısı** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="4f375-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f375-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4f375-161">These values are not real.</span></span> <span data-ttu-id="4f375-162">Bu değerleri tanımlayıcı URL'sini ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4f375-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="4f375-163">Kişi [Zendesk destek ekibi](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="4f375-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="4f375-164">Zendesk SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="4f375-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="4f375-165">Zorunlu SAML özniteliklere vardır ancak özniteliği isteğe bağlı olarak ekleyebileceğiniz **kullanıcı öznitelikleri** izleyerek bölümü aşağıdaki adımları:</span><span class="sxs-lookup"><span data-stu-id="4f375-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="4f375-167">a.</span><span class="sxs-lookup"><span data-stu-id="4f375-167">a.</span></span> <span data-ttu-id="4f375-168">Tıklatın **görünümü ve tüm diğer özniteliklerle düzenleme** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="4f375-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="4f375-170">b.</span><span class="sxs-lookup"><span data-stu-id="4f375-170">b.</span></span> <span data-ttu-id="4f375-171">Tıklatın **özniteliği eklemek** açmak için **Ekle özniteliği** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4f375-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4f375-173">c.</span><span class="sxs-lookup"><span data-stu-id="4f375-173">c.</span></span> <span data-ttu-id="4f375-174">İçinde **adı** metin kutusuna, öznitelik adı yazın (örneğin **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="4f375-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="4f375-175">d.</span><span class="sxs-lookup"><span data-stu-id="4f375-175">d.</span></span> <span data-ttu-id="4f375-176">Gelen **değeri** listesinde, öznitelik değeri seçin (olarak **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="4f375-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="4f375-177">e.</span><span class="sxs-lookup"><span data-stu-id="4f375-177">e.</span></span> <span data-ttu-id="4f375-178">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="4f375-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="4f375-179">Uzantı öznitelikleri, varsayılan olarak Azure AD'de olmayan öznitelikler eklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f375-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="4f375-180">Tıklatın [SAML ayarlanabilir kullanıcı öznitelikleri](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tam listesini almak için SAML öznitelikleri **Zendesk** kabul eder.</span><span class="sxs-lookup"><span data-stu-id="4f375-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="4f375-181">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="4f375-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="4f375-183">Üzerinde **Zendesk yapılandırma** 'yi tıklatın **yapılandırma Zendesk** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4f375-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4f375-184">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4f375-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="4f375-186">Farklı web tarayıcısı penceresinde Zendesk şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4f375-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="4f375-187">Tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="4f375-187">Click **Admin**.</span></span>

9. <span data-ttu-id="4f375-188">Sol gezinti bölmesinde **ayarları**ve ardından **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="4f375-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="4f375-189">Üzerinde **güvenlik** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4f375-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="4f375-190">![Güvenlik](./media/active-directory-saas-zendesk-tutorial/ic773089.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="4f375-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="4f375-191">![Çoklu oturum açma](./media/active-directory-saas-zendesk-tutorial/ic773090.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="4f375-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="4f375-192">a.</span><span class="sxs-lookup"><span data-stu-id="4f375-192">a.</span></span> <span data-ttu-id="4f375-193">Tıklatın **yönetici & aracıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="4f375-194">b.</span><span class="sxs-lookup"><span data-stu-id="4f375-194">b.</span></span> <span data-ttu-id="4f375-195">Seçin **çoklu oturum açma (SSO) ve SAML**ve ardından **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4f375-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="4f375-196">c.</span><span class="sxs-lookup"><span data-stu-id="4f375-196">c.</span></span> <span data-ttu-id="4f375-197">İçinde **SAML SSO URL** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4f375-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="4f375-198">d.</span><span class="sxs-lookup"><span data-stu-id="4f375-198">d.</span></span> <span data-ttu-id="4f375-199">İçinde **uzak oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4f375-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="4f375-200">e.</span><span class="sxs-lookup"><span data-stu-id="4f375-200">e.</span></span> <span data-ttu-id="4f375-201">İçinde **sertifika parmak izi** metin kutusuna, Yapıştır **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="4f375-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="4f375-202">f.</span><span class="sxs-lookup"><span data-stu-id="4f375-202">f.</span></span> <span data-ttu-id="4f375-203">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f375-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f375-204">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f375-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f375-205">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4f375-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4f375-207">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4f375-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4f375-208">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f375-210">Kullanıcıların listesini görüntülemek için Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4f375-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f375-212">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4f375-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f375-214">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4f375-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f375-216">a.</span><span class="sxs-lookup"><span data-stu-id="4f375-216">a.</span></span> <span data-ttu-id="4f375-217">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f375-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f375-218">b.</span><span class="sxs-lookup"><span data-stu-id="4f375-218">b.</span></span> <span data-ttu-id="4f375-219">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4f375-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f375-220">c.</span><span class="sxs-lookup"><span data-stu-id="4f375-220">c.</span></span> <span data-ttu-id="4f375-221">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4f375-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4f375-222">d.</span><span class="sxs-lookup"><span data-stu-id="4f375-222">d.</span></span> <span data-ttu-id="4f375-223">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f375-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="4f375-224">Zendesk test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f375-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="4f375-225">Azure AD kullanıcıların oturum açmanız **Zendesk**, içine sağlanmalıdır **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="4f375-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="4f375-226">Uygulamalar atanan role bağlı olarak, bu beklenen bir davranıştır:</span><span class="sxs-lookup"><span data-stu-id="4f375-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="4f375-227">**Son kullanıcı** hesapları otomatik olarak oturum açarken sağlandı.</span><span class="sxs-lookup"><span data-stu-id="4f375-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="4f375-228">**Aracı** ve **yönetici** hesapları el ile olarak sağlanması gerekir **Zendesk** oturum açmadan önce.</span><span class="sxs-lookup"><span data-stu-id="4f375-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="4f375-229">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4f375-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4f375-230">Oturum, **Zendesk** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="4f375-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="4f375-231">Seçin **müşteri listesi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="4f375-232">Seçin **kullanıcı** sekmesine ve tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4f375-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="4f375-233">![Kullanıcı Ekle](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="4f375-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="4f375-234">Sağlamak istediğiniz ve ardından bir var olan bir Azure AD hesabının e-posta adresini yazın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="4f375-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="4f375-235">![Yeni kullanıcı](./media/active-directory-saas-zendesk-tutorial/ic773633.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="4f375-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="4f375-236">API sağlama AAD kullanıcı hesaplarına Zendesk tarafından sağlanan veya herhangi diğer Zendesk kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f375-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4f375-237">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4f375-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4f375-238">Bu bölümde, Britta Zendesk için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4f375-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4f375-240">**Zendesk için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4f375-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="4f375-241">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4f375-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4f375-243">Uygulamalar listesinde **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="4f375-243">In the applications list, select **Zendesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="4f375-245">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4f375-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4f375-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4f375-247">Click **Add** button.</span></span> <span data-ttu-id="4f375-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4f375-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4f375-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4f375-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4f375-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4f375-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f375-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4f375-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f375-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4f375-253">Testing single sign-on</span></span>

<span data-ttu-id="4f375-254">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4f375-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4f375-255">Erişim paneli Zendesk parçasında tıklattığınızda, otomatik olarak Zendesk uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="4f375-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="4f375-256">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f375-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f375-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4f375-257">Additional resources</span></span>

* [<span data-ttu-id="4f375-258">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4f375-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f375-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4f375-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
