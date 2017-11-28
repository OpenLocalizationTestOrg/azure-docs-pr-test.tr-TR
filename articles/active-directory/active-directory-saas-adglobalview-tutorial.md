---
title: "Öğretici: Azure Active Directory Tümleştirme ile ADP Globalview | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ADP Globalview arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="45f28-103">Öğretici: Azure Active Directory Tümleştirme ADP Globalview ile</span><span class="sxs-lookup"><span data-stu-id="45f28-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="45f28-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ADP Globalview tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="45f28-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45f28-105">ADP Globalview Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="45f28-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="45f28-106">ADP Globalview erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="45f28-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="45f28-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için ADP Globalview açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="45f28-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45f28-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="45f28-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="45f28-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45f28-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45f28-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="45f28-110">Prerequisites</span></span>

<span data-ttu-id="45f28-111">Azure AD tümleştirme ADP Globalview ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="45f28-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="45f28-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="45f28-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45f28-113">Bir ADP Globalview çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="45f28-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45f28-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="45f28-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45f28-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="45f28-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45f28-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="45f28-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="45f28-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45f28-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45f28-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="45f28-118">Scenario description</span></span>
<span data-ttu-id="45f28-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="45f28-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45f28-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="45f28-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45f28-121">Galeriden ADP Globalview ekleme</span><span class="sxs-lookup"><span data-stu-id="45f28-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="45f28-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="45f28-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="45f28-123">Galeriden ADP Globalview ekleme</span><span class="sxs-lookup"><span data-stu-id="45f28-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="45f28-124">Azure AD ADP Globalview tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ADP Globalview eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="45f28-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="45f28-125">**Galeriden ADP Globalview eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45f28-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="45f28-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="45f28-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45f28-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="45f28-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="45f28-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="45f28-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="45f28-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45f28-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="45f28-133">Arama kutusuna **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="45f28-133">In the search box, type **ADP Globalview**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="45f28-135">Sonuçlar panelinde seçin **ADP Globalview**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45f28-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45f28-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="45f28-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45f28-138">Bu bölümde, yapılandırmanız ve ADP Globalview ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="45f28-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="45f28-139">Tekli çalışmaya oturum için Azure AD ADP Globalview karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="45f28-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="45f28-140">Diğer bir deyişle, bir Azure AD kullanıcısının ADP Globalview ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="45f28-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="45f28-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** ADP Globalview içinde.</span><span class="sxs-lookup"><span data-stu-id="45f28-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="45f28-142">Yapılandırma ve Azure AD çoklu oturum açma ADP Globalview ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="45f28-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="45f28-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="45f28-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="45f28-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="45f28-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45f28-145">**[ADP Globalview test kullanıcısı oluşturma](#creating-an-adp-globalview-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı ADP Globalview sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="45f28-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="45f28-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="45f28-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45f28-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="45f28-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45f28-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45f28-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45f28-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ADP Globalview uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="45f28-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="45f28-150">**Azure AD çoklu oturum açma ile ADP Globalview yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45f28-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="45f28-151">Azure portalında üzerinde **ADP Globalview** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="45f28-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="45f28-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="45f28-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="45f28-155">Üzerinde **ADP Globalview etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45f28-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="45f28-157">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın: `https://<subdomain>.globalview.adp.com/federate` veya`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="45f28-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45f28-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="45f28-158">The value is not real.</span></span> <span data-ttu-id="45f28-159">Değerin gerçek tanımlayıcısı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="45f28-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="45f28-160">Kişi [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="45f28-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="45f28-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45f28-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="45f28-163">ADP GlobalView uygulaması SAML onaylar SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemelerini ekleyin gerektiren belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="45f28-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="45f28-164">Aşağıdaki ekran görüntüsü için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="45f28-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="45f28-165">Her zaman talep adları olması **"PersonImmutableID"** ve hangisinin biz eşlenen kullanıcı EmployeeID içeren ExtensionAttribute2 değer.</span><span class="sxs-lookup"><span data-stu-id="45f28-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="45f28-166">Eşleşen kullanıcıya Azure AD'den ADP GlobalView üzerinde EmployeeID burada yapılır, ancak Ayrıca uygulama ayarlarınıza göre farklı bir değere eşleme.</span><span class="sxs-lookup"><span data-stu-id="45f28-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="45f28-167">Önce bir kullanıcının doğru tanıtıcısı kullanın ve bu değeri ile eşlemek için ADP GlobalView ekibi ile çalışabilirsiniz **"PersonImmutableID"** talep.</span><span class="sxs-lookup"><span data-stu-id="45f28-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="45f28-168">Ayrıca, aşağıdaki resimde gösterildiği gibi e-posta ve UserID talep eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f28-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="45f28-170">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45f28-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="45f28-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="45f28-171">Attribute Name</span></span> | <span data-ttu-id="45f28-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="45f28-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="45f28-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="45f28-173">personalimmutableid</span></span> | <span data-ttu-id="45f28-174">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="45f28-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="45f28-175">E-posta</span><span class="sxs-lookup"><span data-stu-id="45f28-175">email</span></span>               | <span data-ttu-id="45f28-176">User.Mail</span><span class="sxs-lookup"><span data-stu-id="45f28-176">user.mail</span></span> |
    | <span data-ttu-id="45f28-177">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="45f28-177">userid</span></span>              | <span data-ttu-id="45f28-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="45f28-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="45f28-179">a.</span><span class="sxs-lookup"><span data-stu-id="45f28-179">a.</span></span> <span data-ttu-id="45f28-180">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45f28-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="45f28-183">b.</span><span class="sxs-lookup"><span data-stu-id="45f28-183">b.</span></span> <span data-ttu-id="45f28-184">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="45f28-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="45f28-185">c.</span><span class="sxs-lookup"><span data-stu-id="45f28-185">c.</span></span> <span data-ttu-id="45f28-186">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="45f28-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="45f28-187">d.</span><span class="sxs-lookup"><span data-stu-id="45f28-187">d.</span></span> <span data-ttu-id="45f28-188">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f28-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45f28-189">SAML onayı yapılandırmadan önce başvurmanız gerekir, [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) ve kiracınız için benzersiz tanımlayıcı özniteliği değeri isteyin.</span><span class="sxs-lookup"><span data-stu-id="45f28-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="45f28-190">Uygulamanız için özel talep yapılandırmak için bu değeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="45f28-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="45f28-191">Üzerinde **ADP Globalview yapılandırma** 'yi tıklatın **yapılandırma ADP Globalview** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="45f28-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="45f28-192">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="45f28-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="45f28-194">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45f28-194">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="45f28-196">Çoklu oturum açma yapılandırmak için **ADP Globalview** yan, indirilen göndermek için ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="45f28-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="45f28-197">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="45f28-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="45f28-198">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="45f28-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="45f28-199">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45f28-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45f28-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45f28-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="45f28-201">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="45f28-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="45f28-203">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45f28-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="45f28-204">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="45f28-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="45f28-206">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="45f28-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45f28-208">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="45f28-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45f28-210">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45f28-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45f28-212">a.</span><span class="sxs-lookup"><span data-stu-id="45f28-212">a.</span></span> <span data-ttu-id="45f28-213">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45f28-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45f28-214">b.</span><span class="sxs-lookup"><span data-stu-id="45f28-214">b.</span></span> <span data-ttu-id="45f28-215">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="45f28-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45f28-216">c.</span><span class="sxs-lookup"><span data-stu-id="45f28-216">c.</span></span> <span data-ttu-id="45f28-217">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="45f28-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="45f28-218">d.</span><span class="sxs-lookup"><span data-stu-id="45f28-218">d.</span></span> <span data-ttu-id="45f28-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f28-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="45f28-220">ADP Globalview test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45f28-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="45f28-221">Bu bölümün amacı Britta Simon ADP GlobalView adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="45f28-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="45f28-222">Çalışmak [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) ADP GlobalView hesap kullanıcılar eklemek için.</span><span class="sxs-lookup"><span data-stu-id="45f28-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="45f28-223">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="45f28-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="45f28-224">Bu bölümde, Britta ADP Globalview erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="45f28-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="45f28-226">**ADP Globalview Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45f28-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="45f28-227">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="45f28-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="45f28-229">Uygulamalar listesinde **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="45f28-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="45f28-231">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="45f28-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="45f28-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45f28-233">Click **Add** button.</span></span> <span data-ttu-id="45f28-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45f28-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="45f28-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="45f28-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="45f28-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45f28-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45f28-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45f28-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45f28-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="45f28-239">Testing single sign-on</span></span>

<span data-ttu-id="45f28-240">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="45f28-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="45f28-241">Erişim paneli ADP GlobalView parçasında tıklattığınızda, otomatik olarak ADP GlobalView uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="45f28-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45f28-242">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="45f28-242">Additional resources</span></span>

* [<span data-ttu-id="45f28-243">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="45f28-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45f28-244">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="45f28-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

