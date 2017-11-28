---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler özel erişim (ZPA) | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Zscaler özel erişim (ZPA) arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="df9c1-103">Öğretici: Azure Active Directory Tümleştirme ile Zscaler özel erişim (ZPA)</span><span class="sxs-lookup"><span data-stu-id="df9c1-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="df9c1-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Zscaler özel erişim (ZPA) tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df9c1-105">Zscaler özel erişim (ZPA) Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="df9c1-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df9c1-106">Erişimi için Zscaler özel erişim (ZPA), Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="df9c1-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="df9c1-107">Azure AD hesaplarına otomatik olarak Zscaler özel erişim (ZPA için) (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="df9c1-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df9c1-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="df9c1-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="df9c1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df9c1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df9c1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="df9c1-110">Prerequisites</span></span>

<span data-ttu-id="df9c1-111">Azure AD tümleştirme Zscaler özel erişim (ZPA ile) yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="df9c1-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="df9c1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="df9c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df9c1-113">Bir Zscaler özel erişim (ZPA) çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="df9c1-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="df9c1-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="df9c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="df9c1-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="df9c1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df9c1-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df9c1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="df9c1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df9c1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="df9c1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="df9c1-118">Scenario description</span></span>
<span data-ttu-id="df9c1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df9c1-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="df9c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df9c1-121">Galeriden Zscaler özel erişim (ZPA) ekleme</span><span class="sxs-lookup"><span data-stu-id="df9c1-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="df9c1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="df9c1-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="df9c1-123">Galeriden Zscaler özel erişim (ZPA) ekleme</span><span class="sxs-lookup"><span data-stu-id="df9c1-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="df9c1-124">Azure AD tümleştirilmesi, Zscaler özel erişim (ZPA) yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Zscaler özel erişim (ZPA) eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df9c1-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df9c1-125">**Galeriden Zscaler özel erişim (ZPA) eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="df9c1-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df9c1-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df9c1-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df9c1-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="df9c1-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="df9c1-133">Arama kutusuna **Zscaler özel erişim (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="df9c1-135">Sonuçlar panelinde seçin **Zscaler özel erişim (ZPA)**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df9c1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="df9c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df9c1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Zscaler özel erişim ("Britta Simon" adlı bir test kullanıcı tabanlı ZPA) test etme.</span><span class="sxs-lookup"><span data-stu-id="df9c1-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df9c1-139">Tekli çalışmaya oturum için Azure AD içinde Zscaler özel erişim (ZPA) karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="df9c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="df9c1-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı içinde Zscaler özel erişim (ZPA) arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="df9c1-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="df9c1-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** içinde Zscaler özel erişim (ZPA).</span><span class="sxs-lookup"><span data-stu-id="df9c1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="df9c1-142">Yapılandırmak ve Azure AD çoklu oturum açma ile Zscaler özel erişim (ZPA) sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="df9c1-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df9c1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df9c1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df9c1-145">**[Zscaler özel erişim (ZPA) test kullanıcısı oluşturma](#creating-a-zscaler-private-access-(zpa)-test-user)**  - Britta Simon, karşılık gelen içinde Zscaler özel erişim (Azure AD gösterimini her için bağlantılı ZPA) sahip.</span><span class="sxs-lookup"><span data-stu-id="df9c1-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="df9c1-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df9c1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="df9c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df9c1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="df9c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df9c1-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Zscaler özel erişim (ZPA) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="df9c1-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="df9c1-150">**Azure AD çoklu oturum açma Zscaler özel erişim (ZPA ile) yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="df9c1-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="df9c1-151">Azure Yönetim Portalı'nda üzerinde **Zscaler özel erişim (ZPA)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="df9c1-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="df9c1-155">Üzerinde **Zscaler özel erişim (ZPA) etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="df9c1-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="df9c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="df9c1-157">a.</span></span> <span data-ttu-id="df9c1-158">İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="df9c1-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="df9c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="df9c1-159">b.</span></span> <span data-ttu-id="df9c1-160">İçinde **tanımlayıcısı** metin kutusuna, türü:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="df9c1-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df9c1-161">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-161">Please note that these are not the real values.</span></span> <span data-ttu-id="df9c1-162">Bu değerler gerçek oturum üzerinde URL ve tanımlayıcıdır ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df9c1-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="df9c1-163">Burada URL benzersiz değeri tanımlayıcıda kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="df9c1-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="df9c1-164">Kişi [Zscaler özel erişim (ZPA) destek ekibi](https://help.zscaler.com/zpa-submit-ticket) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="df9c1-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="df9c1-167">Üzerinde **yeni sertifika oluştur** iletişim kutusunda, Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="df9c1-168">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-168">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="df9c1-170">Üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="df9c1-172">Açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="df9c1-174">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="df9c1-176">Farklı web tarayıcısı penceresinde Zscaler özel erişim (ZPA) şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="df9c1-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="df9c1-177">Gidin **yönetici** ve ardından **IDP yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="df9c1-179">İçinde **IDP yapılandırma** 'yi tıklatın **yeni IDP Yapılandırması Ekle**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="df9c1-181">İçinde **yeni IDP yapılandırma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="df9c1-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="df9c1-183">a.</span><span class="sxs-lookup"><span data-stu-id="df9c1-183">a.</span></span> <span data-ttu-id="df9c1-184">Tıklatın **Dosya Seç** ve indirilen meta veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="df9c1-185">b.</span><span class="sxs-lookup"><span data-stu-id="df9c1-185">b.</span></span> <span data-ttu-id="df9c1-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df9c1-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="df9c1-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="df9c1-188">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="df9c1-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="df9c1-190">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="df9c1-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df9c1-191">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df9c1-193">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df9c1-195">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="df9c1-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df9c1-197">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="df9c1-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df9c1-199">a.</span><span class="sxs-lookup"><span data-stu-id="df9c1-199">a.</span></span> <span data-ttu-id="df9c1-200">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df9c1-201">b.</span><span class="sxs-lookup"><span data-stu-id="df9c1-201">b.</span></span> <span data-ttu-id="df9c1-202">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="df9c1-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df9c1-203">c.</span><span class="sxs-lookup"><span data-stu-id="df9c1-203">c.</span></span> <span data-ttu-id="df9c1-204">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="df9c1-205">d.</span><span class="sxs-lookup"><span data-stu-id="df9c1-205">d.</span></span> <span data-ttu-id="df9c1-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="df9c1-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="df9c1-207">Zscaler özel erişim (ZPA) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="df9c1-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="df9c1-208">Bu bölümde, Britta Simon Zscaler özel erişim (ZPA içinde) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="df9c1-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="df9c1-209">Lütfen çalışmak [Zscaler özel erişim (ZPA) destek ekibi](https://help.zscaler.com/zpa-submit-ticket) Zscaler özel erişim (ZPA) platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="df9c1-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="df9c1-210">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="df9c1-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="df9c1-211">Bu bölümde, Britta Zscaler özel erişim (ZPA) her erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="df9c1-213">**Britta Simon Zscaler özel erişim (ZPA) atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="df9c1-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="df9c1-214">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="df9c1-216">Uygulamalar listesinde **Zscaler özel erişim (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="df9c1-218">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="df9c1-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="df9c1-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="df9c1-220">Click **Add** button.</span></span> <span data-ttu-id="df9c1-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="df9c1-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="df9c1-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="df9c1-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="df9c1-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="df9c1-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df9c1-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="df9c1-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="df9c1-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="df9c1-226">Testing single sign-on</span></span>

<span data-ttu-id="df9c1-227">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="df9c1-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="df9c1-228">Erişim paneli Zscaler özel erişim (ZPA) parçasında tıklattığınızda, otomatik olarak Zscaler özel erişim (ZPA) uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="df9c1-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="df9c1-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="df9c1-229">Additional resources</span></span>

* [<span data-ttu-id="df9c1-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="df9c1-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df9c1-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="df9c1-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png