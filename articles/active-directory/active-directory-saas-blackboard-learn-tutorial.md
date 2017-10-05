---
title: "Öğretici: Azure Active Directory Tümleştirme ile Yazı tahtası öğrenin | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Yazı tahtası öğrenin arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="d7884-103">Öğretici: Azure Active Directory Tümleştirme ile Yazı tahtası öğrenin</span><span class="sxs-lookup"><span data-stu-id="d7884-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="d7884-104">Bu öğreticide, Azure Active Directory (Azure AD) ile tümleştirme Yazı tahtası öğrenin öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d7884-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7884-105">Azure AD ile tümleştirme Yazı tahtası öğrenin ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d7884-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7884-106">Yazı tahtası öğrenin erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7884-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="d7884-107">Azure AD hesaplarına otomatik olarak Yazı tahtası öğrenin (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7884-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7884-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d7884-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7884-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7884-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7884-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7884-110">Prerequisites</span></span>

<span data-ttu-id="d7884-111">Azure AD tümleştirme Yazı tahtası öğrenin ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7884-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="d7884-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d7884-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7884-113">Bir Yazı tahtası öğrenin çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d7884-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7884-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d7884-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7884-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7884-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7884-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d7884-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7884-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7884-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7884-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d7884-118">Scenario description</span></span>
<span data-ttu-id="d7884-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d7884-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7884-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d7884-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7884-121">Galeriden ekleme Yazı tahtası öğrenin</span><span class="sxs-lookup"><span data-stu-id="d7884-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="d7884-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d7884-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="d7884-123">Galeriden ekleme Yazı tahtası öğrenin</span><span class="sxs-lookup"><span data-stu-id="d7884-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="d7884-124">Yazı tahtası öğrenin tümleştirilmesi Azure AD'ye yapılandırmak için Yazı tahtası öğrenin Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7884-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7884-125">**Yazı tahtası öğrenin Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7884-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7884-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7884-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7884-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d7884-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7884-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7884-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d7884-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7884-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d7884-133">Arama kutusuna **Yazı tahtası öğrenin**.</span><span class="sxs-lookup"><span data-stu-id="d7884-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="d7884-135">Sonuçlar panelinde seçin **Yazı tahtası öğrenin**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7884-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7884-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d7884-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7884-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Yazı tahtası öğrenin ile test etme</span><span class="sxs-lookup"><span data-stu-id="d7884-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d7884-139">Tekli çalışmaya oturum için Azure AD karşılık gelen kullanıcı Yazı tahtası öğrenmek için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d7884-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="d7884-140">Diğer bir deyişle, bir Azure AD kullanıcısının ilgili Yazı tahtası öğrenin kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7884-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="d7884-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcı adı** içinde Yazı tahtası öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d7884-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="d7884-142">Yapılandırma ve Azure AD çoklu oturum açma Yazı tahtası öğrenin ile test etmek için aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7884-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7884-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d7884-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7884-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d7884-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7884-145">**[Yazı tahtası öğrenin test kullanıcısı oluşturma](#creating-a-blackboard-learn-test-user)**  - Britta Simon, karşılık gelen Yazı tahtası kullanıcı Azure AD gösterimini bağlantılı bilgi sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d7884-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7884-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d7884-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7884-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d7884-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7884-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d7884-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7884-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Yazı tahtası öğrenin uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d7884-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="d7884-150">**Azure AD çoklu oturum açma Yazı tahtası öğrenin ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7884-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="d7884-151">Azure portalında üzerinde **Yazı tahtası öğrenin** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d7884-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d7884-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d7884-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="d7884-155">Üzerinde **Yazı tahtası öğrenin etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7884-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="d7884-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7884-157">a.</span></span> <span data-ttu-id="d7884-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="d7884-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="d7884-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7884-159">b.</span></span> <span data-ttu-id="d7884-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="d7884-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d7884-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d7884-161">These values are not real.</span></span> <span data-ttu-id="d7884-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7884-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d7884-163">Kişi [Yazı tahtası öğrenin istemci destek ekibi](https://www.blackboard.com/support/index.aspx) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="d7884-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="d7884-164">Yazı tahtası öğrenin uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="d7884-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d7884-165">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d7884-165">Configure the following claims for this application.</span></span> <span data-ttu-id="d7884-166">Bu öznitelik değerlerini yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="d7884-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="d7884-167">Aşağıdaki ekran görüntüsünde ilgili bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7884-167">The following screenshot shows an example about it.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="d7884-169">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliklerini görüntüde gösterildiği gibi yapılandırmak ve aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7884-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="d7884-170">Userprincipalname burada benzersiz kullanıcı özniteliği eşledikten ancak benzersiz olarak ayırt, kuruluşunuzdaki kullanıcı ve Yazı tahtası öğrenin username alan eşlemeleri uygun değere eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7884-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="d7884-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="d7884-171">Attribute Name</span></span> | <span data-ttu-id="d7884-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="d7884-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="d7884-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="d7884-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="d7884-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="d7884-174">user.userprincipalname</span></span> |

    <span data-ttu-id="d7884-175">a.</span><span class="sxs-lookup"><span data-stu-id="d7884-175">a.</span></span> <span data-ttu-id="d7884-176">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7884-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d7884-179">b.</span><span class="sxs-lookup"><span data-stu-id="d7884-179">b.</span></span> <span data-ttu-id="d7884-180">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="d7884-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="d7884-181">c.</span><span class="sxs-lookup"><span data-stu-id="d7884-181">c.</span></span> <span data-ttu-id="d7884-182">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="d7884-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d7884-183">d.</span><span class="sxs-lookup"><span data-stu-id="d7884-183">d.</span></span> <span data-ttu-id="d7884-184">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7884-184">Click **Ok**.</span></span>

4. <span data-ttu-id="d7884-185">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7884-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="d7884-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7884-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d7884-189">Üzerinde **Yazı tahtası öğrenin yapılandırma** 'yi tıklatın **yapılandırma Yazı tahtası öğrenin** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d7884-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d7884-190">Kopya **SAML varlık kimliği** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d7884-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="d7884-192">Çoklu oturum açma yapılandırmak için **Yazı tahtası öğrenin** yan, indirilen göndermek için ihtiyacınız **meta veri XML** ve **SAML varlık kimliği** için [Yazı tahtası öğrenin Destek](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7884-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="d7884-193">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d7884-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7884-194">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d7884-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7884-195">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7884-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7884-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7884-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7884-197">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d7884-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d7884-199">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7884-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7884-200">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7884-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7884-202">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d7884-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7884-204">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="d7884-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7884-206">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7884-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7884-208">a.</span><span class="sxs-lookup"><span data-stu-id="d7884-208">a.</span></span> <span data-ttu-id="d7884-209">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7884-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7884-210">b.</span><span class="sxs-lookup"><span data-stu-id="d7884-210">b.</span></span> <span data-ttu-id="d7884-211">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="d7884-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d7884-212">c.</span><span class="sxs-lookup"><span data-stu-id="d7884-212">c.</span></span> <span data-ttu-id="d7884-213">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d7884-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7884-214">d.</span><span class="sxs-lookup"><span data-stu-id="d7884-214">d.</span></span> <span data-ttu-id="d7884-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7884-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="d7884-216">Yazı tahtası öğrenin test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7884-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="d7884-217">Bu bölümde, Yazı tahtası öğrenin Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d7884-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="d7884-218">Yazı tahtası öğrenin uygulama desteği yalnızca zaman sağlama kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="d7884-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="d7884-219">Bölümünde açıklandığı gibi talep yapılandırdığınızdan emin olun  **[yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="d7884-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7884-220">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d7884-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7884-221">Bu bölümde, Britta Yazı tahtası öğrenmek için erişim izni verme, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7884-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d7884-223">**Yazı tahtası öğrenin Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7884-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="d7884-224">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7884-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d7884-226">Uygulamalar listesinde **Yazı tahtası öğrenin**.</span><span class="sxs-lookup"><span data-stu-id="d7884-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="d7884-228">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d7884-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d7884-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7884-230">Click **Add** button.</span></span> <span data-ttu-id="d7884-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7884-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d7884-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d7884-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7884-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7884-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7884-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7884-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7884-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d7884-236">Testing single sign-on</span></span>

<span data-ttu-id="d7884-237">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d7884-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7884-238">Erişim paneli Yazı tahtası öğrenin parçasında tıklattığınızda, otomatik olarak Yazı tahtası öğrenin uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="d7884-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="d7884-239">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7884-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d7884-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d7884-240">Additional resources</span></span>

* [<span data-ttu-id="d7884-241">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d7884-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7884-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d7884-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

