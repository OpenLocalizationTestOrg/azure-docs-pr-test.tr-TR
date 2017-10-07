---
title: "Öğretici: Azure Active Directory Tümleştirme SD öğelerle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SD öğeleri arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="ec189-103">Öğretici: Azure Active Directory Tümleştirme SD öğeleri</span><span class="sxs-lookup"><span data-stu-id="ec189-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="ec189-104">Bu öğreticide, bilgi nasıl toointegrate SD öğeleri Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec189-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec189-105">SD öğeleri Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ec189-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec189-106">Erişim tooSD öğeleri sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ec189-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="ec189-107">Kullanıcıların tooautomatically get açan tooSD öğeleri (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ec189-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec189-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ec189-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ec189-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec189-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec189-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ec189-110">Prerequisites</span></span>

<span data-ttu-id="ec189-111">tooconfigure SD öğeleri ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec189-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="ec189-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ec189-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec189-113">Bir SD öğeleri çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ec189-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec189-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ec189-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec189-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec189-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec189-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ec189-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec189-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec189-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec189-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ec189-118">Scenario description</span></span>
<span data-ttu-id="ec189-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ec189-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec189-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ec189-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec189-121">Merhaba Galerisi'nden SD öğeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="ec189-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="ec189-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ec189-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="ec189-123">Merhaba Galerisi'nden SD öğeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="ec189-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="ec189-124">Azure AD'ye tooconfigure hello tümleştirme SD öğelerinin tooadd SD öğeleri hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec189-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec189-125">**tooadd SD öğeleri hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec189-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec189-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ec189-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec189-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ec189-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec189-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ec189-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ec189-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec189-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ec189-133">Merhaba arama kutusuna yazın **SD öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="ec189-133">In hello search box, type **SD Elements**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="ec189-135">Merhaba Sonuçlar panelinde seçin **SD öğeleri**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ec189-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec189-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ec189-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec189-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SD "Britta Simon" adlı bir test kullanıcıya bağlı öğeleri ile test etme.</span><span class="sxs-lookup"><span data-stu-id="ec189-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec189-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SD öğelerinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec189-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="ec189-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı SD öğeleri arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec189-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="ec189-141">SD öğelerinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="ec189-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec189-142">tooconfigure ve SD öğeleri ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec189-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec189-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="ec189-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec189-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="ec189-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec189-145">**[SD öğeleri test kullanıcısı oluşturma](#creating-a-sd-elements-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SD öğelerinde, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="ec189-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec189-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ec189-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec189-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="ec189-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec189-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ec189-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec189-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SD öğeleri uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ec189-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="ec189-150">**tooconfigure Azure AD çoklu oturum açma SD öğelerle hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec189-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec189-151">Merhaba hello üzerinde Azure portal'ın **SD öğeleri** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ec189-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ec189-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ec189-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="ec189-155">Merhaba üzerinde **SD öğeleri etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec189-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="ec189-157">a.</span><span class="sxs-lookup"><span data-stu-id="ec189-157">a.</span></span> <span data-ttu-id="ec189-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="ec189-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="ec189-159">b.</span><span class="sxs-lookup"><span data-stu-id="ec189-159">b.</span></span> <span data-ttu-id="ec189-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="ec189-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec189-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="ec189-161">These values are not real.</span></span> <span data-ttu-id="ec189-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ec189-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ec189-163">Kişi [SD öğeleri destek ekibi](mailto:support@sdelements.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="ec189-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="ec189-164">SD öğeleri uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="ec189-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ec189-165">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ec189-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="ec189-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Kullanıcı özniteliği"** hello uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="ec189-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="ec189-167">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec189-167">hello following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="ec189-169">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec189-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="ec189-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="ec189-170">Attribute Name</span></span> | <span data-ttu-id="ec189-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="ec189-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ec189-172">E-posta</span><span class="sxs-lookup"><span data-stu-id="ec189-172">email</span></span> |<span data-ttu-id="ec189-173">User.Mail</span><span class="sxs-lookup"><span data-stu-id="ec189-173">user.mail</span></span> |
    | <span data-ttu-id="ec189-174">FirstName</span><span class="sxs-lookup"><span data-stu-id="ec189-174">firstname</span></span> |<span data-ttu-id="ec189-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ec189-175">user.givenname</span></span> |
    | <span data-ttu-id="ec189-176">Soyadı</span><span class="sxs-lookup"><span data-stu-id="ec189-176">lastname</span></span> |<span data-ttu-id="ec189-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="ec189-177">user.surname</span></span> |

    <span data-ttu-id="ec189-178">a.</span><span class="sxs-lookup"><span data-stu-id="ec189-178">a.</span></span> <span data-ttu-id="ec189-179">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec189-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="ec189-182">b.</span><span class="sxs-lookup"><span data-stu-id="ec189-182">b.</span></span> <span data-ttu-id="ec189-183">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="ec189-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="ec189-184">c.</span><span class="sxs-lookup"><span data-stu-id="ec189-184">c.</span></span> <span data-ttu-id="ec189-185">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="ec189-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="ec189-186">d.</span><span class="sxs-lookup"><span data-stu-id="ec189-186">d.</span></span> <span data-ttu-id="ec189-187">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ec189-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="ec189-188">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ec189-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="ec189-190">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec189-190">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ec189-192">Merhaba üzerinde **SD öğeleri yapılandırma** 'yi tıklatın **yapılandırma SD öğeleri** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ec189-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ec189-193">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="ec189-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="ec189-195">tooget tekli etkin oturum kişi, [SD öğeleri destek ekibi](mailto:support@sdelements.com) ve hello indirilen sertifika dosyasıyla verin.</span><span class="sxs-lookup"><span data-stu-id="ec189-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="ec189-196">Farklı bir tarayıcı penceresinde bir yönetici olarak oturum açma tooyour SD öğeleri Kiracı.</span><span class="sxs-lookup"><span data-stu-id="ec189-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="ec189-197">Hello içinde hello üst menüsünde **sistem**ve ardından **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ec189-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="ec189-199">Merhaba üzerinde **çoklu oturum açma ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec189-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="ec189-201">a.</span><span class="sxs-lookup"><span data-stu-id="ec189-201">a.</span></span> <span data-ttu-id="ec189-202">Olarak **SSO türü**seçin **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ec189-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="ec189-203">b.</span><span class="sxs-lookup"><span data-stu-id="ec189-203">b.</span></span> <span data-ttu-id="ec189-204">Merhaba, **kimlik sağlayıcısı varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="ec189-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="ec189-205">c.</span><span class="sxs-lookup"><span data-stu-id="ec189-205">c.</span></span> <span data-ttu-id="ec189-206">Merhaba, **kimlik sağlayıcısı çoklu oturum açma hizmeti** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="ec189-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="ec189-207">d.</span><span class="sxs-lookup"><span data-stu-id="ec189-207">d.</span></span> <span data-ttu-id="ec189-208">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ec189-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ec189-209">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ec189-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec189-210">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="ec189-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec189-211">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec189-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec189-212">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec189-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec189-213">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="ec189-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ec189-215">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec189-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec189-216">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ec189-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec189-218">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ec189-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec189-220">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec189-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec189-222">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec189-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec189-224">a.</span><span class="sxs-lookup"><span data-stu-id="ec189-224">a.</span></span> <span data-ttu-id="ec189-225">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec189-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec189-226">b.</span><span class="sxs-lookup"><span data-stu-id="ec189-226">b.</span></span> <span data-ttu-id="ec189-227">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ec189-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec189-228">c.</span><span class="sxs-lookup"><span data-stu-id="ec189-228">c.</span></span> <span data-ttu-id="ec189-229">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ec189-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ec189-230">d.</span><span class="sxs-lookup"><span data-stu-id="ec189-230">d.</span></span> <span data-ttu-id="ec189-231">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ec189-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="ec189-232">SD öğeleri test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec189-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="ec189-233">Bu bölümde Hello amacı toocreate SD öğelerinde Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="ec189-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="ec189-234">SD öğeleri Hello durumda SD öğeleri kullanıcıları oluşturarak bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="ec189-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="ec189-235">**toocreate Britta Simon SD öğelerinde hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec189-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec189-236">Bir web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour SD öğeleri şirket site.</span><span class="sxs-lookup"><span data-stu-id="ec189-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="ec189-237">Hello içinde hello üst menüsünde **kullanıcı yönetimi**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ec189-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![SD öğeleri test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="ec189-239">Tıklatın **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ec189-239">Click **Add New User**.</span></span>
   
    ![SD öğeleri test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="ec189-241">Merhaba üzerinde **yeni kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec189-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![SD öğeleri test kullanıcısı oluşturma](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="ec189-243">a.</span><span class="sxs-lookup"><span data-stu-id="ec189-243">a.</span></span> <span data-ttu-id="ec189-244">Merhaba, **e-posta** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ec189-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="ec189-245">b.</span><span class="sxs-lookup"><span data-stu-id="ec189-245">b.</span></span> <span data-ttu-id="ec189-246">Merhaba, **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ec189-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="ec189-247">c.</span><span class="sxs-lookup"><span data-stu-id="ec189-247">c.</span></span> <span data-ttu-id="ec189-248">Merhaba, **Soyadı** metin kutusuna, hello son gibi kullanıcı adını girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ec189-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="ec189-249">d.</span><span class="sxs-lookup"><span data-stu-id="ec189-249">d.</span></span> <span data-ttu-id="ec189-250">Olarak **rol**seçin **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="ec189-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="ec189-251">e.</span><span class="sxs-lookup"><span data-stu-id="ec189-251">e.</span></span> <span data-ttu-id="ec189-252">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ec189-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ec189-253">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ec189-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ec189-254">Bu bölümde, tooSD öğeleri erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ec189-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ec189-256">**tooassign Britta Simon tooSD öğeleri hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ec189-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec189-257">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ec189-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ec189-259">Merhaba uygulamalar listesinde **SD öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="ec189-259">In hello applications list, select **SD Elements**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="ec189-261">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ec189-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ec189-263">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec189-263">Click **Add** button.</span></span> <span data-ttu-id="ec189-264">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec189-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ec189-266">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ec189-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec189-267">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec189-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec189-268">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec189-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec189-269">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ec189-269">Testing single sign-on</span></span>

<span data-ttu-id="ec189-270">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ec189-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="ec189-271">SD öğeleri hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak imzalanmış üzerinde SD öğeleri uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec189-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec189-272">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec189-272">Additional resources</span></span>

* [<span data-ttu-id="ec189-273">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ec189-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec189-274">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ec189-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

