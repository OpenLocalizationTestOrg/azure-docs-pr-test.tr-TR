---
title: "Öğretici: Azure Active Directory Tümleştirme ile BenefitHub | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile BenefitHub arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="9a228-103">Öğretici: Azure Active Directory Tümleştirme BenefitHub ile</span><span class="sxs-lookup"><span data-stu-id="9a228-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="9a228-104">Bu öğreticide, Azure Active Directory (Azure AD) ile BenefitHub tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9a228-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a228-105">BenefitHub Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9a228-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a228-106">BenefitHub erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9a228-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="9a228-107">Otomatik olarak için BenefitHub (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9a228-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a228-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9a228-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a228-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a228-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a228-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9a228-110">Prerequisites</span></span>

<span data-ttu-id="9a228-111">Azure AD tümleştirme BenefitHub ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="9a228-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="9a228-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9a228-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a228-113">Bir BenefitHub çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="9a228-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a228-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9a228-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a228-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9a228-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a228-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9a228-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a228-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a228-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a228-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9a228-118">Scenario description</span></span>
<span data-ttu-id="9a228-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9a228-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a228-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9a228-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a228-121">Galeriden BenefitHub ekleme</span><span class="sxs-lookup"><span data-stu-id="9a228-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="9a228-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9a228-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="9a228-123">Galeriden BenefitHub ekleme</span><span class="sxs-lookup"><span data-stu-id="9a228-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="9a228-124">Azure AD BenefitHub tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden BenefitHub eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a228-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a228-125">**Galeriden BenefitHub eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9a228-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a228-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9a228-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a228-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9a228-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a228-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9a228-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9a228-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9a228-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9a228-133">Arama kutusuna **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="9a228-133">In the search box, type **BenefitHub**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="9a228-135">Sonuçlar panelinde seçin **BenefitHub**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9a228-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a228-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9a228-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a228-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BenefitHub ile test etme</span><span class="sxs-lookup"><span data-stu-id="9a228-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9a228-139">Tekli çalışmaya oturum için Azure AD BenefitHub karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="9a228-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="9a228-140">Diğer bir deyişle, bir Azure AD kullanıcısının BenefitHub ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a228-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="9a228-141">BenefitHub içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="9a228-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a228-142">Yapılandırma ve Azure AD çoklu oturum açma BenefitHub ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9a228-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a228-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9a228-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a228-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="9a228-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a228-145">**[BenefitHub test kullanıcısı oluşturma](#creating-a-benefithub-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı BenefitHub sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="9a228-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a228-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9a228-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a228-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9a228-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a228-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9a228-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a228-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma BenefitHub uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a228-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="9a228-150">**Azure AD çoklu oturum açma ile BenefitHub yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9a228-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="9a228-151">Azure portalında üzerinde **BenefitHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9a228-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9a228-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9a228-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="9a228-155">Üzerinde **BenefitHub etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9a228-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="9a228-157">a.</span><span class="sxs-lookup"><span data-stu-id="9a228-157">a.</span></span> <span data-ttu-id="9a228-158">İçinde **tanımlayıcısı** metin kutusuna, türü:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="9a228-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="9a228-159">b.</span><span class="sxs-lookup"><span data-stu-id="9a228-159">b.</span></span> <span data-ttu-id="9a228-160">İçinde **yanıt URL'si** metin kutusuna, türü:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="9a228-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="9a228-161">BenefitHub uygulaması SAML onaylar SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemelerini ekleyin gerektiren belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="9a228-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="9a228-162">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a228-162">Configure the following claims for this application.</span></span> <span data-ttu-id="9a228-163">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="9a228-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="9a228-165">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, önceki görüntüde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9a228-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="9a228-166">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="9a228-166">Attribute Name</span></span> | <span data-ttu-id="9a228-167">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="9a228-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="9a228-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="9a228-168">organizationid</span></span> | <span data-ttu-id="9a228-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="9a228-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="9a228-170">Bu öznitelik değerini gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="9a228-170">This attribute value is not real.</span></span> <span data-ttu-id="9a228-171">Bu değer ile gerçek organizationid güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9a228-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="9a228-172">Kişi [BenefitHub destek ekibi](https://www.benefithub.com/Home/ContactUs) gerçek organizationid alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="9a228-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="9a228-173">a.</span><span class="sxs-lookup"><span data-stu-id="9a228-173">a.</span></span> <span data-ttu-id="9a228-174">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9a228-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9a228-177">b.</span><span class="sxs-lookup"><span data-stu-id="9a228-177">b.</span></span> <span data-ttu-id="9a228-178">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="9a228-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="9a228-179">c.</span><span class="sxs-lookup"><span data-stu-id="9a228-179">c.</span></span> <span data-ttu-id="9a228-180">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="9a228-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9a228-181">d.</span><span class="sxs-lookup"><span data-stu-id="9a228-181">d.</span></span> <span data-ttu-id="9a228-182">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a228-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a228-183">SAML onayı yapılandırmadan önce başvurmanız gerekir, [BenefitHub Destek](https://www.benefithub.com/Home/ContactUs) ve kiracınız için benzersiz tanımlayıcı özniteliği değeri isteyin.</span><span class="sxs-lookup"><span data-stu-id="9a228-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="9a228-184">Uygulamanız için özel talep yapılandırmak için bu değeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a228-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="9a228-185">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9a228-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="9a228-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9a228-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9a228-189">Çoklu oturum açma yapılandırmak için **BenefitHub** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [BenefitHub destek ekibi](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="9a228-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="9a228-190">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a228-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9a228-191">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9a228-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a228-192">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="9a228-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a228-193">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a228-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a228-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a228-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a228-195">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="9a228-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9a228-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9a228-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a228-198">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9a228-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a228-200">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9a228-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a228-202">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="9a228-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a228-204">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9a228-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a228-206">a.</span><span class="sxs-lookup"><span data-stu-id="9a228-206">a.</span></span> <span data-ttu-id="9a228-207">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a228-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a228-208">b.</span><span class="sxs-lookup"><span data-stu-id="9a228-208">b.</span></span> <span data-ttu-id="9a228-209">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9a228-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a228-210">c.</span><span class="sxs-lookup"><span data-stu-id="9a228-210">c.</span></span> <span data-ttu-id="9a228-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9a228-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a228-212">d.</span><span class="sxs-lookup"><span data-stu-id="9a228-212">d.</span></span> <span data-ttu-id="9a228-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a228-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="9a228-214">BenefitHub test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a228-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="9a228-215">Bu bölümde, BenefitHub içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a228-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="9a228-216">Çalışmak [BenefitHub destek ekibi](https://www.benefithub.com/Home/ContactUs) BenefitHub platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="9a228-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="9a228-217">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="9a228-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9a228-218">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9a228-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9a228-219">Bu bölümde, Britta BenefitHub için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9a228-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9a228-221">**BenefitHub için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9a228-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="9a228-222">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9a228-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9a228-224">Uygulamalar listesinde **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="9a228-224">In the applications list, select **BenefitHub**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="9a228-226">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9a228-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9a228-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9a228-228">Click **Add** button.</span></span> <span data-ttu-id="9a228-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9a228-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9a228-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9a228-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a228-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9a228-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a228-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9a228-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a228-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9a228-234">Testing single sign-on</span></span>

<span data-ttu-id="9a228-235">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9a228-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a228-236">Erişim paneli BenefitHub parçasında tıklattığınızda, otomatik olarak BenefitHub uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="9a228-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="9a228-237">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9a228-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a228-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9a228-238">Additional resources</span></span>

* [<span data-ttu-id="9a228-239">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="9a228-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a228-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9a228-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

