---
title: "Öğretici: Azure Active Directory Tümleştirme kutusuyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin kutusunu ve Azure Active Directory arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="4598b-103">Öğretici: Azure Active Directory Tümleştirme kutusu</span><span class="sxs-lookup"><span data-stu-id="4598b-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="4598b-104">Bu öğreticide, bilgi nasıl toointegrate kutusunda Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="4598b-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4598b-105">Kutusunu Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4598b-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4598b-106">Erişim tooBox sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4598b-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="4598b-107">Kullanıcıların tooautomatically get açan tooBox (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4598b-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4598b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4598b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4598b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4598b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4598b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4598b-110">Prerequisites</span></span>

<span data-ttu-id="4598b-111">Azure AD tümleştirme kutusuyla tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4598b-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="4598b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4598b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4598b-113">Bir kutusunu çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="4598b-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4598b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4598b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4598b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4598b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4598b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4598b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4598b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4598b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4598b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4598b-118">Scenario description</span></span>
<span data-ttu-id="4598b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4598b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4598b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4598b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4598b-121">Merhaba Galerisi'nden kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="4598b-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="4598b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4598b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="4598b-123">Merhaba Galerisi'nden kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="4598b-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="4598b-124">Azure AD'ye tooconfigure hello tümleştirme kutusunun tooadd kutusunu hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4598b-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4598b-125">**tooadd hello galeri kutusundan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4598b-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4598b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4598b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4598b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4598b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4598b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4598b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4598b-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4598b-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4598b-133">Merhaba arama kutusuna yazın **kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="4598b-133">In hello search box, type **Box**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="4598b-135">Merhaba Sonuçlar panelinde seçin **kutusunu**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4598b-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4598b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4598b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4598b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı kutusuyla test etme</span><span class="sxs-lookup"><span data-stu-id="4598b-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4598b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen kutusunda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4598b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="4598b-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı kutusunda arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4598b-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="4598b-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** kutusunda.</span><span class="sxs-lookup"><span data-stu-id="4598b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="4598b-142">tooconfigure ve kutusuyla Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4598b-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4598b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4598b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4598b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4598b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4598b-145">**[Kutusunu test kullanıcısı oluşturma](#creating-a-box-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir kutusuna, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="4598b-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4598b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4598b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4598b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4598b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4598b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4598b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4598b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma kutusunu uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4598b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="4598b-150">**tooconfigure Azure AD çoklu oturum açma, kutusuyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4598b-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="4598b-151">Merhaba hello üzerinde Azure portal'ın **kutusunu** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4598b-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4598b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4598b-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="4598b-155">Merhaba üzerinde **kutusunu etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4598b-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="4598b-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="4598b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4598b-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="4598b-158">This value is not real.</span></span> <span data-ttu-id="4598b-159">Merhaba değerini hello gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4598b-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="4598b-160">Kişi [kutusunu istemci destek ekibi](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="4598b-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="4598b-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4598b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="4598b-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4598b-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4598b-165">tooget kişi, uygulamanız için yapılandırılmış SSO [kutusunu istemci destek ekibi](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) ve indirilen hello XML dosyasıyla verin.</span><span class="sxs-lookup"><span data-stu-id="4598b-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="4598b-166">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4598b-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4598b-167">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4598b-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4598b-168">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4598b-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4598b-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4598b-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="4598b-170">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4598b-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4598b-172">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4598b-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4598b-173">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4598b-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4598b-175">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4598b-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4598b-177">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4598b-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4598b-179">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4598b-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4598b-181">a.</span><span class="sxs-lookup"><span data-stu-id="4598b-181">a.</span></span> <span data-ttu-id="4598b-182">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4598b-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4598b-183">b.</span><span class="sxs-lookup"><span data-stu-id="4598b-183">b.</span></span> <span data-ttu-id="4598b-184">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4598b-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4598b-185">c.</span><span class="sxs-lookup"><span data-stu-id="4598b-185">c.</span></span> <span data-ttu-id="4598b-186">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4598b-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4598b-187">d.</span><span class="sxs-lookup"><span data-stu-id="4598b-187">d.</span></span> <span data-ttu-id="4598b-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4598b-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="4598b-189">Kutusunu test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4598b-189">Creating a Box test user</span></span>

<span data-ttu-id="4598b-190">Bu bölümde, Britta Simon adlı bir kullanıcı kutusunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4598b-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="4598b-191">Kutusu yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="4598b-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="4598b-192">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="4598b-192">There is no action item for you in this section.</span></span> <span data-ttu-id="4598b-193">Bir kullanıcı zaten kutusunda yoksa, tooaccess kutusunu çalıştığınızda yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4598b-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4598b-194">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4598b-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4598b-195">Bu bölümde, erişim tooBox vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4598b-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4598b-197">**tooassign Britta Simon tooBox hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4598b-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="4598b-198">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4598b-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4598b-200">Merhaba uygulamalar listesinde **kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="4598b-200">In hello applications list, select **Box**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="4598b-202">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4598b-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4598b-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4598b-204">Click **Add** button.</span></span> <span data-ttu-id="4598b-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4598b-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4598b-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4598b-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4598b-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4598b-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4598b-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4598b-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4598b-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4598b-210">Testing single sign-on</span></span>

<span data-ttu-id="4598b-211">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4598b-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4598b-212">Merhaba kutusunu hello erişim paneli parçasında tıkladığınızda, oturum açma sayfası tooget açan tooyour kutusunu uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4598b-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4598b-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4598b-213">Additional resources</span></span>

* [<span data-ttu-id="4598b-214">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4598b-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4598b-215">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4598b-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4598b-216">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="4598b-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

