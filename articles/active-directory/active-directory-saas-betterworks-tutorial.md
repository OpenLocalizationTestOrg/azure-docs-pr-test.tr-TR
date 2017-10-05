---
title: "Öğretici: Azure Active Directory Tümleştirme ile BetterWorks | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile BetterWorks arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="b83a4-103">Öğretici: Azure Active Directory Tümleştirme BetterWorks ile</span><span class="sxs-lookup"><span data-stu-id="b83a4-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="b83a4-104">Bu öğreticide, Azure Active Directory (Azure AD) ile BetterWorks tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b83a4-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b83a4-105">BetterWorks Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b83a4-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b83a4-106">BetterWorks erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b83a4-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="b83a4-107">Otomatik olarak için BetterWorks (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b83a4-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b83a4-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b83a4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b83a4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b83a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b83a4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b83a4-110">Prerequisites</span></span>

<span data-ttu-id="b83a4-111">Azure AD tümleştirme BetterWorks ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="b83a4-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="b83a4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b83a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b83a4-113">Bir BetterWorks çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="b83a4-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b83a4-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b83a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b83a4-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b83a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b83a4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b83a4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b83a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b83a4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b83a4-118">Scenario description</span></span>
<span data-ttu-id="b83a4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b83a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b83a4-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b83a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b83a4-121">Galeriden BetterWorks ekleme</span><span class="sxs-lookup"><span data-stu-id="b83a4-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="b83a4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b83a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="b83a4-123">Galeriden BetterWorks ekleme</span><span class="sxs-lookup"><span data-stu-id="b83a4-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="b83a4-124">Azure AD BetterWorks tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden BetterWorks eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b83a4-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b83a4-125">**Galeriden BetterWorks eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b83a4-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b83a4-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b83a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b83a4-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b83a4-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b83a4-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b83a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b83a4-133">Arama kutusuna **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-133">In the search box, type **BetterWorks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="b83a4-135">Sonuçlar panelinde seçin **BetterWorks**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b83a4-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b83a4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b83a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b83a4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BetterWorks ile test etme</span><span class="sxs-lookup"><span data-stu-id="b83a4-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b83a4-139">Tekli çalışmaya oturum için Azure AD BetterWorks karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="b83a4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="b83a4-140">Diğer bir deyişle, bir Azure AD kullanıcısının BetterWorks ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b83a4-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="b83a4-141">BetterWorks içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b83a4-142">Yapılandırma ve Azure AD çoklu oturum açma BetterWorks ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b83a4-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b83a4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b83a4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b83a4-145">**[BetterWorks test kullanıcısı oluşturma](#creating-a-betterworks-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı BetterWorks sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b83a4-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b83a4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b83a4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b83a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b83a4-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma BetterWorks uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="b83a4-150">**Azure AD çoklu oturum açma ile BetterWorks yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b83a4-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="b83a4-151">Azure portalında üzerinde **BetterWorks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b83a4-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="b83a4-155">Üzerinde **BetterWorks etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="b83a4-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="b83a4-157">a.</span><span class="sxs-lookup"><span data-stu-id="b83a4-157">a.</span></span> <span data-ttu-id="b83a4-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="b83a4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="b83a4-159">b.</span><span class="sxs-lookup"><span data-stu-id="b83a4-159">b.</span></span> <span data-ttu-id="b83a4-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="b83a4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="b83a4-161">Üzerinde **BetterWorks etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **SP tarafından başlatılan modu**, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b83a4-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="b83a4-163">a.</span><span class="sxs-lookup"><span data-stu-id="b83a4-163">a.</span></span> <span data-ttu-id="b83a4-164">Tıklayın **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="b83a4-165">b.</span><span class="sxs-lookup"><span data-stu-id="b83a4-165">b.</span></span> <span data-ttu-id="b83a4-166">İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="b83a4-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b83a4-167">Bunlar gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="b83a4-167">These are not real values.</span></span> <span data-ttu-id="b83a4-168">Bu değerleri yanıt URL'si, tanımlayıcı ve üzerinde gerçek oturum URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b83a4-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="b83a4-169">Kişi [BetterWorks destek ekibi](mailto:support@betterworks.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="b83a4-170">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b83a4-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="b83a4-172">BetterWorks uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="b83a4-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b83a4-173">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-173">Configure the following claims for this application.</span></span> <span data-ttu-id="b83a4-174">Bu öznitelik değerlerini yönetebilirsiniz "**özniteliği**" Uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="b83a4-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="b83a4-175">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="b83a4-175">The following screenshot shows an example for this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="b83a4-177">Üzerinde **SAML belirteci öznitelikleri** iletişim kutusunda, aşağıdaki tabloda gösterilen her satır için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b83a4-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="b83a4-178">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="b83a4-178">Attribute Name</span></span> | <span data-ttu-id="b83a4-179">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="b83a4-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="b83a4-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="b83a4-180">saml_token</span></span>     | <span data-ttu-id="b83a4-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="b83a4-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="b83a4-182">a.</span><span class="sxs-lookup"><span data-stu-id="b83a4-182">a.</span></span> <span data-ttu-id="b83a4-183">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b83a4-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="b83a4-186">b.</span><span class="sxs-lookup"><span data-stu-id="b83a4-186">b.</span></span> <span data-ttu-id="b83a4-187">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="b83a4-188">c.</span><span class="sxs-lookup"><span data-stu-id="b83a4-188">c.</span></span> <span data-ttu-id="b83a4-189">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="b83a4-190">d.</span><span class="sxs-lookup"><span data-stu-id="b83a4-190">d.</span></span> <span data-ttu-id="b83a4-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-191">Click **Ok**.</span></span>

7. <span data-ttu-id="b83a4-192">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b83a4-192">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b83a4-194">Çoklu oturum açma yapılandırmak için **BetterWorks** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [BetterWorks destek ekibi](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="b83a4-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="b83a4-195">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b83a4-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b83a4-196">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="b83a4-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b83a4-197">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b83a4-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b83a4-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b83a4-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="b83a4-199">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b83a4-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b83a4-201">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b83a4-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b83a4-202">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b83a4-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b83a4-204">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b83a4-206">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="b83a4-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b83a4-208">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b83a4-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b83a4-210">a.</span><span class="sxs-lookup"><span data-stu-id="b83a4-210">a.</span></span> <span data-ttu-id="b83a4-211">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b83a4-212">b.</span><span class="sxs-lookup"><span data-stu-id="b83a4-212">b.</span></span> <span data-ttu-id="b83a4-213">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b83a4-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b83a4-214">c.</span><span class="sxs-lookup"><span data-stu-id="b83a4-214">c.</span></span> <span data-ttu-id="b83a4-215">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b83a4-216">d.</span><span class="sxs-lookup"><span data-stu-id="b83a4-216">d.</span></span> <span data-ttu-id="b83a4-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b83a4-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="b83a4-218">BetterWorks test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b83a4-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="b83a4-219">Bu bölümde, BetterWorks içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b83a4-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="b83a4-220">Çalışmak [BetterWorks destek ekibi](mailto:support@betterworks.com) BetterWorks platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="b83a4-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b83a4-221">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b83a4-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b83a4-222">Bu bölümde, Britta BetterWorks için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b83a4-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b83a4-224">**BetterWorks için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b83a4-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="b83a4-225">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b83a4-227">Uygulamalar listesinde **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-227">In the applications list, select **BetterWorks**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="b83a4-229">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b83a4-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b83a4-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b83a4-231">Click **Add** button.</span></span> <span data-ttu-id="b83a4-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b83a4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b83a4-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b83a4-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b83a4-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b83a4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b83a4-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b83a4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b83a4-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b83a4-237">Testing single sign-on</span></span>

<span data-ttu-id="b83a4-238">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="b83a4-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b83a4-239">Erişim paneli BetterWorks parçasında tıklattığınızda, otomatik olarak BetterWorks uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="b83a4-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b83a4-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b83a4-240">Additional resources</span></span>

* [<span data-ttu-id="b83a4-241">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="b83a4-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b83a4-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b83a4-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

