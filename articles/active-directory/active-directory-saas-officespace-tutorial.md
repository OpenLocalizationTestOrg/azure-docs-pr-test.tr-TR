---
title: "Öğretici: Azure Active Directory Tümleştirme OfficeSpace yazılımıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve OfficeSpace yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="fdb25-103">Öğretici: Azure Active Directory Tümleştirme OfficeSpace yazılımıyla</span><span class="sxs-lookup"><span data-stu-id="fdb25-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="fdb25-104">Bu öğreticide, bilgi nasıl toointegrate OfficeSpace yazılım Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fdb25-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fdb25-105">OfficeSpace yazılım Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fdb25-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fdb25-106">Erişim tooOfficeSpace yazılım sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdb25-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="fdb25-107">Kullanıcıların tooautomatically get açan tooOfficeSpace yazılım (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdb25-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fdb25-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fdb25-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fdb25-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdb25-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fdb25-110">Prerequisites</span></span>

<span data-ttu-id="fdb25-111">tooconfigure OfficeSpace yazılım ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fdb25-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="fdb25-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fdb25-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fdb25-113">Bir OfficeSpace yazılım çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fdb25-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fdb25-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fdb25-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fdb25-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fdb25-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fdb25-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fdb25-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fdb25-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fdb25-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fdb25-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fdb25-118">Scenario description</span></span>
<span data-ttu-id="fdb25-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fdb25-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fdb25-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fdb25-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fdb25-121">Merhaba Galerisi'nden OfficeSpace yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="fdb25-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="fdb25-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fdb25-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="fdb25-123">Merhaba Galerisi'nden OfficeSpace yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="fdb25-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="fdb25-124">Azure AD'ye tooconfigure hello tümleştirme OfficeSpace yazılım tooadd OfficeSpace yazılım hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fdb25-125">**tooadd OfficeSpace yazılım hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fdb25-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdb25-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="fdb25-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fdb25-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="fdb25-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="fdb25-133">Merhaba arama kutusuna yazın **OfficeSpace yazılım**seçin **OfficeSpace yazılım** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fdb25-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba OfficeSpace yazılım listesi sonuçları](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fdb25-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fdb25-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fdb25-136">Bu bölümde, yapılandırmanız ve "Britta Simon" adlı bir test kullanıcı OfficeSpace yazılım ile Azure AD çoklu oturum açmayı test temel.</span><span class="sxs-lookup"><span data-stu-id="fdb25-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fdb25-137">Tek toowork'ın oturum açma hangi hello karşılık gelen OfficeSpace yazılım tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="fdb25-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve OfficeSpace yazılım hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="fdb25-139">Merhaba hello değeri OfficeSpace yazılımda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fdb25-140">tooconfigure ve OfficeSpace yazılım ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fdb25-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fdb25-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fdb25-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fdb25-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fdb25-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fdb25-143">**[OfficeSpace yazılım test kullanıcısı oluşturma](#create-a-officespace-software-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir OfficeSpace yazılım, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fdb25-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fdb25-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fdb25-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fdb25-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fdb25-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fdb25-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fdb25-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fdb25-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma OfficeSpace yazılım uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fdb25-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="fdb25-148">**tooconfigure Azure AD çoklu oturum açma OfficeSpace yazılımıyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fdb25-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdb25-149">Hello hello üzerinde Azure portal'ın **OfficeSpace yazılım** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="fdb25-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fdb25-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="fdb25-153">Merhaba üzerinde **OfficeSpace yazılım etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fdb25-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![OfficeSpace yazılım etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="fdb25-155">a.</span><span class="sxs-lookup"><span data-stu-id="fdb25-155">a.</span></span> <span data-ttu-id="fdb25-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="fdb25-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="fdb25-157">b.</span><span class="sxs-lookup"><span data-stu-id="fdb25-157">b.</span></span> <span data-ttu-id="fdb25-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="fdb25-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fdb25-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-159">These values are not real.</span></span> <span data-ttu-id="fdb25-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fdb25-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fdb25-161">Kişi [OfficeSpace yazılım istemci destek ekibi](mailto:support@officespacesoftware.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="fdb25-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="fdb25-162">OfficeSpace yazılım uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="fdb25-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="fdb25-163">Lütfen bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fdb25-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="fdb25-164">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="fdb25-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="fdb25-165">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-165">hello following screenshot shows an example for this.</span></span>
    
    ![Öznitelik yapılandırma](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="fdb25-167">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda **user.mail** olarak **kullanıcı tanımlayıcısı** ve gösterilen her satır için Merhaba aşağıdaki tabloda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fdb25-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="fdb25-168">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="fdb25-168">Attribute Name</span></span> | <span data-ttu-id="fdb25-169">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="fdb25-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="fdb25-170">E-posta</span><span class="sxs-lookup"><span data-stu-id="fdb25-170">email</span></span> | <span data-ttu-id="fdb25-171">User.Mail</span><span class="sxs-lookup"><span data-stu-id="fdb25-171">user.mail</span></span> |
    | <span data-ttu-id="fdb25-172">ad</span><span class="sxs-lookup"><span data-stu-id="fdb25-172">name</span></span> | <span data-ttu-id="fdb25-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="fdb25-173">user.displayname</span></span> |
    | <span data-ttu-id="fdb25-174">ilk_ad</span><span class="sxs-lookup"><span data-stu-id="fdb25-174">first_name</span></span> | <span data-ttu-id="fdb25-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="fdb25-175">user.givenname</span></span> |
    | <span data-ttu-id="fdb25-176">Soyadı</span><span class="sxs-lookup"><span data-stu-id="fdb25-176">last_name</span></span> | <span data-ttu-id="fdb25-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="fdb25-177">user.surname</span></span> |

    <span data-ttu-id="fdb25-178">a.</span><span class="sxs-lookup"><span data-stu-id="fdb25-178">a.</span></span> <span data-ttu-id="fdb25-179">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fdb25-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="fdb25-180">Yapılandırma ekleme</span><span class="sxs-lookup"><span data-stu-id="fdb25-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Öznitelik yapılandırma](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="fdb25-182">b.</span><span class="sxs-lookup"><span data-stu-id="fdb25-182">b.</span></span> <span data-ttu-id="fdb25-183">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="fdb25-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="fdb25-184">c.</span><span class="sxs-lookup"><span data-stu-id="fdb25-184">c.</span></span> <span data-ttu-id="fdb25-185">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="fdb25-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fdb25-186">d.</span><span class="sxs-lookup"><span data-stu-id="fdb25-186">d.</span></span> <span data-ttu-id="fdb25-187">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="fdb25-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="fdb25-188">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** hello sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="fdb25-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="fdb25-190">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-190">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fdb25-192">Merhaba üzerinde **OfficeSpace yazılım yapılandırma** 'yi tıklatın **OfficeSpace yazılımı Yapılandır** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fdb25-193">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fdb25-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![OfficeSpace yazılım yapılandırma](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="fdb25-195">Farklı web tarayıcısı penceresinde OfficeSpace yazılım Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fdb25-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="fdb25-196">Çok Git**ayarları** tıklatıp **Bağlayıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="fdb25-198">Tıklatın **SAML kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-198">Click **SAML Authentication**.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="fdb25-200">Merhaba, **SAML kimlik doğrulaması** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fdb25-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="fdb25-202">a.</span><span class="sxs-lookup"><span data-stu-id="fdb25-202">a.</span></span> <span data-ttu-id="fdb25-203">Merhaba, **oturum kapatma sağlayıcısı url** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fdb25-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fdb25-204">b.</span><span class="sxs-lookup"><span data-stu-id="fdb25-204">b.</span></span> <span data-ttu-id="fdb25-205">Merhaba, **istemci IDP hedef url** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fdb25-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fdb25-206">c.</span><span class="sxs-lookup"><span data-stu-id="fdb25-206">c.</span></span> <span data-ttu-id="fdb25-207">Yapıştır hello **parmak izi** hello Azure portalından kopyaladığınız değeri **istemci IDP sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="fdb25-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="fdb25-208">d.</span><span class="sxs-lookup"><span data-stu-id="fdb25-208">d.</span></span> <span data-ttu-id="fdb25-209">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="fdb25-210">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fdb25-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fdb25-211">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fdb25-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fdb25-212">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fdb25-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fdb25-213">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdb25-213">Create an Azure AD test user</span></span>

<span data-ttu-id="fdb25-214">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fdb25-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="fdb25-216">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fdb25-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdb25-217">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fdb25-219">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fdb25-221">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="fdb25-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fdb25-223">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fdb25-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fdb25-225">a.</span><span class="sxs-lookup"><span data-stu-id="fdb25-225">a.</span></span> <span data-ttu-id="fdb25-226">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fdb25-227">b.</span><span class="sxs-lookup"><span data-stu-id="fdb25-227">b.</span></span> <span data-ttu-id="fdb25-228">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="fdb25-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fdb25-229">c.</span><span class="sxs-lookup"><span data-stu-id="fdb25-229">c.</span></span> <span data-ttu-id="fdb25-230">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fdb25-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fdb25-231">d.</span><span class="sxs-lookup"><span data-stu-id="fdb25-231">d.</span></span> <span data-ttu-id="fdb25-232">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fdb25-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="fdb25-233">OfficeSpace yazılım test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdb25-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="fdb25-234">Bu bölümde Hello amacı toocreate Britta Simon OfficeSpace yazılım adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="fdb25-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="fdb25-235">OfficeSpace yazılımı yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="fdb25-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fdb25-236">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="fdb25-236">There is no action item for you in this section.</span></span> <span data-ttu-id="fdb25-237">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess OfficeSpace yazılım sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fdb25-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="fdb25-238">Bir kullanıcı toocreate el ile gerekiyorsa, tooContact gerek [OfficeSpace yazılım destek ekibi](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="fdb25-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fdb25-239">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="fdb25-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fdb25-240">Bu bölümde, erişim tooOfficeSpace yazılım vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fdb25-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="fdb25-242">**tooassign Britta Simon tooOfficeSpace yazılım, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fdb25-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdb25-243">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fdb25-245">Merhaba uygulamalar listesinde **OfficeSpace yazılım**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![Merhaba hello uygulamalar listesinde OfficeSpace yazılım bağlantısı](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="fdb25-247">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fdb25-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="fdb25-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fdb25-249">Click **Add** button.</span></span> <span data-ttu-id="fdb25-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fdb25-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="fdb25-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fdb25-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fdb25-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fdb25-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fdb25-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fdb25-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fdb25-255">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="fdb25-255">Test single sign-on</span></span>

<span data-ttu-id="fdb25-256">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fdb25-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fdb25-257">OfficeSpace yazılım döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma OfficeSpace yazılım uygulaması tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdb25-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fdb25-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fdb25-258">Additional resources</span></span>

* [<span data-ttu-id="fdb25-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fdb25-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fdb25-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fdb25-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

