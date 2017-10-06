---
title: "Öğretici: Azure Active Directory Tümleştirme ile Lesson.ly | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Lesson.ly arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="cfa19-103">Öğretici: Azure Active Directory Tümleştirme Lesson.ly ile</span><span class="sxs-lookup"><span data-stu-id="cfa19-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="cfa19-104">Bu öğreticide, bilgi nasıl toointegrate Lesson.ly Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfa19-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfa19-105">Lesson.LY Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cfa19-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfa19-106">Erişim tooLesson.ly sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cfa19-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="cfa19-107">Kullanıcıların tooautomatically get açan tooLesson.ly (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cfa19-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfa19-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cfa19-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cfa19-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfa19-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfa19-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cfa19-110">Prerequisites</span></span>

<span data-ttu-id="cfa19-111">tooconfigure Lesson.ly ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cfa19-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="cfa19-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cfa19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfa19-113">Bir Lesson.ly çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cfa19-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfa19-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cfa19-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfa19-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cfa19-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfa19-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cfa19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfa19-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfa19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfa19-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cfa19-118">Scenario description</span></span>
<span data-ttu-id="cfa19-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cfa19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfa19-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cfa19-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfa19-121">Merhaba Galerisi'nden Lesson.LY ekleme</span><span class="sxs-lookup"><span data-stu-id="cfa19-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="cfa19-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cfa19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="cfa19-123">Merhaba Galerisi'nden Lesson.LY ekleme</span><span class="sxs-lookup"><span data-stu-id="cfa19-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="cfa19-124">Azure AD'ye tooconfigure hello tümleştirme Lesson.ly, tooadd Lesson.ly hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="cfa19-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfa19-125">**tooadd Lesson.ly hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cfa19-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfa19-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfa19-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfa19-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cfa19-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cfa19-133">Merhaba arama kutusuna yazın **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="cfa19-135">Merhaba Sonuçlar panelinde seçin **Lesson.ly**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cfa19-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfa19-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cfa19-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfa19-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Lesson.ly sınayın.</span><span class="sxs-lookup"><span data-stu-id="cfa19-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfa19-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Lesson.ly içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="cfa19-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="cfa19-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Lesson.ly hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cfa19-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="cfa19-141">Merhaba hello değeri Lesson.LY içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfa19-142">tooconfigure ve Lesson.ly ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cfa19-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfa19-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="cfa19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfa19-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="cfa19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfa19-145">**[Lesson.ly test kullanıcısı oluşturma](#creating-a-lessonly-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Lesson.ly içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="cfa19-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfa19-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cfa19-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfa19-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="cfa19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfa19-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cfa19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfa19-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Lesson.ly uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cfa19-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="cfa19-150">**tooconfigure Azure AD çoklu oturum açma ile Lesson.ly, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cfa19-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfa19-151">Hello hello üzerinde Azure portal'ın **Lesson.ly** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cfa19-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cfa19-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="cfa19-155">Merhaba üzerinde **Lesson.ly etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cfa19-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="cfa19-157">a.</span><span class="sxs-lookup"><span data-stu-id="cfa19-157">a.</span></span> <span data-ttu-id="cfa19-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="cfa19-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="cfa19-159">Ne zaman genel başvuran ad **ŞirketAdı** gerçek adıyla değiştirilen toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cfa19-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="cfa19-160">b.</span><span class="sxs-lookup"><span data-stu-id="cfa19-160">b.</span></span> <span data-ttu-id="cfa19-161">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="cfa19-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="cfa19-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cfa19-162">These values are not real.</span></span> <span data-ttu-id="cfa19-163">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cfa19-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cfa19-164">Kişi [Lesson.ly istemci destek ekibi](mailto:dev@lessonly.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="cfa19-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="cfa19-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cfa19-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="cfa19-167">Merhaba Lesson.ly uygulama bekliyor hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, **SAML belirteci öznitelikleri** ekran aşağıdaki configuration.hello gösteren bir örnek için Bu.</span><span class="sxs-lookup"><span data-stu-id="cfa19-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="cfa19-169">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntü önceki hello gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cfa19-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="cfa19-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="cfa19-170">Attribute Name</span></span>   | <span data-ttu-id="cfa19-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="cfa19-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="cfa19-172">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="cfa19-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="cfa19-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="cfa19-173">user.givenname</span></span> |
    | <span data-ttu-id="cfa19-174">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="cfa19-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="cfa19-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="cfa19-175">user.surname</span></span> |
    | <span data-ttu-id="cfa19-176">urn: oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="cfa19-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="cfa19-177">User.Mail</span><span class="sxs-lookup"><span data-stu-id="cfa19-177">user.mail</span></span> |

    <span data-ttu-id="cfa19-178">a.</span><span class="sxs-lookup"><span data-stu-id="cfa19-178">a.</span></span> <span data-ttu-id="cfa19-179">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cfa19-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="cfa19-182">b.</span><span class="sxs-lookup"><span data-stu-id="cfa19-182">b.</span></span> <span data-ttu-id="cfa19-183">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="cfa19-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="cfa19-184">c.</span><span class="sxs-lookup"><span data-stu-id="cfa19-184">c.</span></span> <span data-ttu-id="cfa19-185">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="cfa19-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cfa19-186">d.</span><span class="sxs-lookup"><span data-stu-id="cfa19-186">d.</span></span> <span data-ttu-id="cfa19-187">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cfa19-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="cfa19-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-188">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cfa19-190">Merhaba üzerinde **Lesson.ly yapılandırma** 'yi tıklatın **yapılandırma Lesson.ly** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cfa19-191">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cfa19-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="cfa19-193">tooconfigure çoklu oturum açma üzerinde **Lesson.ly** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Lesson.ly destek ekibi](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="cfa19-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="cfa19-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cfa19-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfa19-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="cfa19-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfa19-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfa19-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfa19-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cfa19-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfa19-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="cfa19-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cfa19-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cfa19-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfa19-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfa19-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfa19-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="cfa19-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfa19-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cfa19-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfa19-209">a.</span><span class="sxs-lookup"><span data-stu-id="cfa19-209">a.</span></span> <span data-ttu-id="cfa19-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfa19-211">b.</span><span class="sxs-lookup"><span data-stu-id="cfa19-211">b.</span></span> <span data-ttu-id="cfa19-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cfa19-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfa19-213">c.</span><span class="sxs-lookup"><span data-stu-id="cfa19-213">c.</span></span> <span data-ttu-id="cfa19-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cfa19-215">d.</span><span class="sxs-lookup"><span data-stu-id="cfa19-215">d.</span></span> <span data-ttu-id="cfa19-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cfa19-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="cfa19-217">Lesson.ly test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cfa19-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="cfa19-218">Bu bölümde Hello amacı toocreate Britta Simon içinde Lesson.ly adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="cfa19-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="cfa19-219">Lesson.LY yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="cfa19-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cfa19-220">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="cfa19-220">There is no action item for you in this section.</span></span> <span data-ttu-id="cfa19-221">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Lesson.ly sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cfa19-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="cfa19-222">Bir kullanıcı toocreate el ile yapmanız gerekir, toocontact hello gerekir [Lesson.ly destek ekibi](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="cfa19-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cfa19-223">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cfa19-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cfa19-224">Bu bölümde, erişim tooLesson.ly vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cfa19-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cfa19-226">**tooassign Britta Simon tooLesson.ly hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cfa19-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfa19-227">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cfa19-229">Merhaba uygulamalar listesinde **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="cfa19-231">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cfa19-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cfa19-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cfa19-233">Click **Add** button.</span></span> <span data-ttu-id="cfa19-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cfa19-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cfa19-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cfa19-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfa19-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cfa19-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfa19-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cfa19-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfa19-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cfa19-239">Testing single sign-on</span></span>

<span data-ttu-id="cfa19-240">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="cfa19-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cfa19-241">Merhaba Lesson.ly hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Lesson.ly uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cfa19-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfa19-242">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cfa19-242">Additional resources</span></span>

* [<span data-ttu-id="cfa19-243">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cfa19-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfa19-244">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cfa19-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

