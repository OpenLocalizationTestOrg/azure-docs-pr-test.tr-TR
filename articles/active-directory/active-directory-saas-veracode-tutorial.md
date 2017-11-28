---
title: "Öğretici: Azure Active Directory Tümleştirme ile Veracode | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Veracode arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="5135a-103">Öğretici: Azure Active Directory Tümleştirme Veracode ile</span><span class="sxs-lookup"><span data-stu-id="5135a-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="5135a-104">Bu öğreticide, bilgi nasıl toointegrate Veracode Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5135a-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5135a-105">Veracode Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5135a-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5135a-106">Erişim tooVeracode sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5135a-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="5135a-107">Kullanıcıların tooautomatically get açan tooVeracode (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5135a-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5135a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="5135a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5135a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5135a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5135a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5135a-110">Prerequisites</span></span>

<span data-ttu-id="5135a-111">tooconfigure Veracode ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5135a-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="5135a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5135a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5135a-113">Bir Veracode çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="5135a-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5135a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5135a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5135a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5135a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5135a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5135a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5135a-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5135a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5135a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5135a-118">Scenario description</span></span>
<span data-ttu-id="5135a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5135a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5135a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5135a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5135a-121">Merhaba Galerisi'nden Veracode ekleme</span><span class="sxs-lookup"><span data-stu-id="5135a-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="5135a-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5135a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="5135a-123">Merhaba Galerisi'nden Veracode ekleme</span><span class="sxs-lookup"><span data-stu-id="5135a-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="5135a-124">Azure AD'ye tooconfigure hello tümleştirme Veracode, tooadd Veracode hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5135a-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5135a-125">**tooadd Veracode hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5135a-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5135a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5135a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="5135a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5135a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5135a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5135a-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="5135a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5135a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="5135a-133">Merhaba arama kutusuna yazın **Veracode**seçin **Veracode** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5135a-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5135a-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5135a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5135a-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Veracode sınayın.</span><span class="sxs-lookup"><span data-stu-id="5135a-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5135a-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Veracode içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5135a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="5135a-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Veracode hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5135a-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="5135a-139">Merhaba hello değeri Veracode içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="5135a-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5135a-140">tooconfigure ve Veracode ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5135a-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5135a-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5135a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5135a-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5135a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5135a-143">**[Veracode test kullanıcısı oluşturma](#create-a-veracode-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Veracode içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5135a-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5135a-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5135a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5135a-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5135a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5135a-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5135a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5135a-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Veracode uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5135a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="5135a-148">**tooconfigure Azure AD çoklu oturum açma ile Veracode, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5135a-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="5135a-149">Hello hello üzerinde Azure portal'ın **Veracode** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5135a-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="5135a-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5135a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="5135a-153">Merhaba üzerinde **Veracode etki alanı ve URL'leri** bölümü, kullanıcı hello uygulama zaten Azure ile önceden tümleştirilmiş gibi herhangi bir adım tooperform yok.</span><span class="sxs-lookup"><span data-stu-id="5135a-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="5135a-155">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5135a-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="5135a-157">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooVeracode Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="5135a-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="5135a-158">Veracode uygulamanızı hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, bekliyor **saml belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5135a-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="5135a-159">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="5135a-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="5135a-160">![Öznitelikleri](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="5135a-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="5135a-161">tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5135a-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="5135a-162">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="5135a-162">Attribute Name</span></span> | <span data-ttu-id="5135a-163">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="5135a-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="5135a-164">FirstName</span><span class="sxs-lookup"><span data-stu-id="5135a-164">firstname</span></span> |<span data-ttu-id="5135a-165">User.givenName</span><span class="sxs-lookup"><span data-stu-id="5135a-165">User.givenname</span></span> |
    | <span data-ttu-id="5135a-166">Soyadı</span><span class="sxs-lookup"><span data-stu-id="5135a-166">lastname</span></span> |<span data-ttu-id="5135a-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="5135a-167">User.surname</span></span> |
    | <span data-ttu-id="5135a-168">E-posta</span><span class="sxs-lookup"><span data-stu-id="5135a-168">email</span></span> |<span data-ttu-id="5135a-169">User.Mail</span><span class="sxs-lookup"><span data-stu-id="5135a-169">User.mail</span></span> |
    
    <span data-ttu-id="5135a-170">a.</span><span class="sxs-lookup"><span data-stu-id="5135a-170">a.</span></span> <span data-ttu-id="5135a-171">Yukarıdaki hello tablosundaki her veri satırı için tıklatın **kullanıcı özniteliği eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5135a-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="5135a-172">![Öznitelikleri](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="5135a-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="5135a-173">![Öznitelikleri](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="5135a-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="5135a-174">b.</span><span class="sxs-lookup"><span data-stu-id="5135a-174">b.</span></span> <span data-ttu-id="5135a-175">Merhaba, **öznitelik adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="5135a-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5135a-176">c.</span><span class="sxs-lookup"><span data-stu-id="5135a-176">c.</span></span> <span data-ttu-id="5135a-177">Merhaba, **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen select hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="5135a-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5135a-178">d.</span><span class="sxs-lookup"><span data-stu-id="5135a-178">d.</span></span> <span data-ttu-id="5135a-179">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5135a-179">Click **Ok**.</span></span>

7. <span data-ttu-id="5135a-180">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5135a-180">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5135a-182">Merhaba üzerinde **Veracode yapılandırma** 'yi tıklatın **yapılandırma Veracode** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5135a-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5135a-183">Kopya hello **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="5135a-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Veracode yapılandırma](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="5135a-185">Farklı web tarayıcısı penceresinde Veracode şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5135a-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="5135a-186">Hello içinde hello üst menüsünde **ayarları**ve ardından **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="5135a-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="5135a-187">![Yönetim](./media/active-directory-saas-veracode-tutorial/ic802911.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="5135a-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="5135a-188">Merhaba tıklatın **SAML** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5135a-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="5135a-189">Merhaba, **kuruluş SAML ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5135a-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5135a-190">![Yönetim](./media/active-directory-saas-veracode-tutorial/ic802912.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="5135a-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="5135a-191">a.</span><span class="sxs-lookup"><span data-stu-id="5135a-191">a.</span></span>  <span data-ttu-id="5135a-192">İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="5135a-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="5135a-193">b.</span><span class="sxs-lookup"><span data-stu-id="5135a-193">b.</span></span> <span data-ttu-id="5135a-194">Azure Portalı'ndan indirilen sertifikanızı tooupload tıklatın **Dosya Seç**.</span><span class="sxs-lookup"><span data-stu-id="5135a-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="5135a-195">c.</span><span class="sxs-lookup"><span data-stu-id="5135a-195">c.</span></span> <span data-ttu-id="5135a-196">Seçin **etkinleştirmek kendi kendine kayıt**.</span><span class="sxs-lookup"><span data-stu-id="5135a-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="5135a-197">Merhaba, **kendi kendine kayıt ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin ve ardından **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="5135a-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="5135a-198">![Yönetim](./media/active-directory-saas-veracode-tutorial/ic802913.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="5135a-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="5135a-199">a.</span><span class="sxs-lookup"><span data-stu-id="5135a-199">a.</span></span> <span data-ttu-id="5135a-200">Olarak **yeni kullanıcı etkinleştirme**seçin **Hayır etkinleştirmesinin**.</span><span class="sxs-lookup"><span data-stu-id="5135a-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="5135a-201">b.</span><span class="sxs-lookup"><span data-stu-id="5135a-201">b.</span></span> <span data-ttu-id="5135a-202">Olarak **kullanıcı veri güncelleştirmeleri**seçin **tercih Veracode kullanıcı verilerini**.</span><span class="sxs-lookup"><span data-stu-id="5135a-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="5135a-203">c.</span><span class="sxs-lookup"><span data-stu-id="5135a-203">c.</span></span> <span data-ttu-id="5135a-204">İçin **SAML özniteliği ayrıntılarını**, hello aşağıdakileri seçin:</span><span class="sxs-lookup"><span data-stu-id="5135a-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="5135a-205">**Kullanıcı rolleri**</span><span class="sxs-lookup"><span data-stu-id="5135a-205">**User Roles**</span></span>
      * <span data-ttu-id="5135a-206">**İlke Yöneticisi**</span><span class="sxs-lookup"><span data-stu-id="5135a-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="5135a-207">**Gözden Geçiren**</span><span class="sxs-lookup"><span data-stu-id="5135a-207">**Reviewer**</span></span>
      * <span data-ttu-id="5135a-208">**Güvenlik sağlama**</span><span class="sxs-lookup"><span data-stu-id="5135a-208">**Security Lead**</span></span>
      * <span data-ttu-id="5135a-209">**Executive**</span><span class="sxs-lookup"><span data-stu-id="5135a-209">**Executive**</span></span>
      * <span data-ttu-id="5135a-210">**Gönderen**</span><span class="sxs-lookup"><span data-stu-id="5135a-210">**Submitter**</span></span>
      * <span data-ttu-id="5135a-211">**Oluşturan**</span><span class="sxs-lookup"><span data-stu-id="5135a-211">**Creator**</span></span>
      * <span data-ttu-id="5135a-212">**Tüm taraması türleri**</span><span class="sxs-lookup"><span data-stu-id="5135a-212">**All Scan Types**</span></span>
      * <span data-ttu-id="5135a-213">**Takım üyelikleri**</span><span class="sxs-lookup"><span data-stu-id="5135a-213">**Team Memberships**</span></span>
      * <span data-ttu-id="5135a-214">**Varsayılan takım**</span><span class="sxs-lookup"><span data-stu-id="5135a-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="5135a-215">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5135a-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5135a-216">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="5135a-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5135a-217">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5135a-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5135a-218">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5135a-218">Create an Azure AD test user</span></span>

<span data-ttu-id="5135a-219">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5135a-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="5135a-221">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5135a-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5135a-222">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5135a-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5135a-224">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5135a-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5135a-226">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5135a-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5135a-228">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5135a-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5135a-230">a.</span><span class="sxs-lookup"><span data-stu-id="5135a-230">a.</span></span> <span data-ttu-id="5135a-231">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5135a-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5135a-232">b.</span><span class="sxs-lookup"><span data-stu-id="5135a-232">b.</span></span> <span data-ttu-id="5135a-233">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="5135a-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5135a-234">c.</span><span class="sxs-lookup"><span data-stu-id="5135a-234">c.</span></span> <span data-ttu-id="5135a-235">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="5135a-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5135a-236">d.</span><span class="sxs-lookup"><span data-stu-id="5135a-236">d.</span></span> <span data-ttu-id="5135a-237">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5135a-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="5135a-238">Veracode test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5135a-238">Create a Veracode test user</span></span>
<span data-ttu-id="5135a-239">Veracode içine sipariş tooenable Azure AD kullanıcıların toolog bunların Veracode sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5135a-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="5135a-240">Veracode Hello durumda sağlama otomatik bir görev haline gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="5135a-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="5135a-241">Sizin için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="5135a-241">There is no action item for you.</span></span> <span data-ttu-id="5135a-242">Kullanıcıları otomatik olarak hello ilk tek oturum açma girişimi sırasında gerekirse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5135a-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="5135a-243">API'leri, Azure AD kullanıcı hesapları Veracode tooprovision tarafından sağlanan veya herhangi diğer Veracode kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5135a-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5135a-244">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="5135a-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5135a-245">Bu bölümde, erişim tooVeracode vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5135a-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="5135a-247">**tooassign Britta Simon tooVeracode hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5135a-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="5135a-248">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5135a-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5135a-250">Merhaba uygulamalar listesinde **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="5135a-250">In hello applications list, select **Veracode**.</span></span>

    ![Merhaba Veracode bağlantı hello uygulamalar listesinde](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="5135a-252">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5135a-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="5135a-254">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5135a-254">Click **Add** button.</span></span> <span data-ttu-id="5135a-255">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5135a-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="5135a-257">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5135a-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5135a-258">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5135a-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5135a-259">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5135a-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5135a-260">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="5135a-260">Test single sign-on</span></span>

<span data-ttu-id="5135a-261">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5135a-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5135a-262">Merhaba Veracode hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Veracode uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5135a-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="5135a-263">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5135a-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5135a-264">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5135a-264">Additional resources</span></span>

* [<span data-ttu-id="5135a-265">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5135a-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5135a-266">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5135a-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

