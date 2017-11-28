---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kronos | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kronos arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="7c4fd-103">Öğretici: Azure Active Directory Tümleştirme Kronos ile</span><span class="sxs-lookup"><span data-stu-id="7c4fd-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="7c4fd-104">Bu öğreticide, bilgi nasıl toointegrate Kronos Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c4fd-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c4fd-105">Kronos Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c4fd-106">Erişim tooKronos sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c4fd-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="7c4fd-107">Kullanıcıların tooautomatically get açan tooKronos (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c4fd-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c4fd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7c4fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7c4fd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c4fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c4fd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c4fd-110">Prerequisites</span></span>

<span data-ttu-id="7c4fd-111">tooconfigure Kronos ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="7c4fd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7c4fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c4fd-113">A **Kronos işgücü Merkezi** SSO abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7c4fd-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c4fd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c4fd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c4fd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c4fd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c4fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c4fd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7c4fd-118">Scenario description</span></span>
<span data-ttu-id="7c4fd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c4fd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c4fd-121">Merhaba Galerisi'nden Kronos ekleme</span><span class="sxs-lookup"><span data-stu-id="7c4fd-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="7c4fd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c4fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="7c4fd-123">Merhaba Galerisi'nden Kronos ekleme</span><span class="sxs-lookup"><span data-stu-id="7c4fd-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="7c4fd-124">Azure AD'ye tooconfigure hello tümleştirme Kronos, tooadd Kronos hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c4fd-125">**tooadd Kronos hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c4fd-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c4fd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c4fd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c4fd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7c4fd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7c4fd-133">Merhaba arama kutusuna yazın **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-133">In hello search box, type **Kronos**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="7c4fd-135">Merhaba Sonuçlar panelinde seçin **Kronos**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c4fd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c4fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c4fd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Kronos ile test etme</span><span class="sxs-lookup"><span data-stu-id="7c4fd-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7c4fd-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Kronos içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="7c4fd-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Kronos hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="7c4fd-141">Merhaba hello değeri Kronos içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7c4fd-142">tooconfigure ve Kronos ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c4fd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c4fd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c4fd-145">**[Kronos test kullanıcısı oluşturma](#creating-a-kronos-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Kronos içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c4fd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c4fd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c4fd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c4fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c4fd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Kronos uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="7c4fd-150">**tooconfigure Azure AD çoklu oturum açma ile Kronos, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c4fd-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c4fd-151">Hello hello üzerinde Azure portal'ın **Kronos** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7c4fd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="7c4fd-155">Merhaba üzerinde **Kronos etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="7c4fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-157">a.</span></span> <span data-ttu-id="7c4fd-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="7c4fd-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="7c4fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-159">b.</span></span> <span data-ttu-id="7c4fd-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="7c4fd-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c4fd-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-161">These values are not real.</span></span> <span data-ttu-id="7c4fd-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7c4fd-163">Kişi [Kronos destek ekibi](https://www.kronos.in/contact/en-in/form) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="7c4fd-164">Kronos uygulamanızı belirli bir biçimde hello SAML onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7c4fd-165">Çalışmak [Kronos destek ekibi](https://www.kronos.in/contact/en-in/form) hello uygulamasına eşlenen ilk tooidentify hello doğru kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="7c4fd-166">Ayrıca hello Kılavuzu istedikleri hello özniteliği hakkında Lütfen uygulayın; bu eşlemenin toouse.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="7c4fd-167">Microsoft önerir hello kullanarak **"NameIdentifier"** kullanıcı tanımlayıcısı olarak özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="7c4fd-168">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Kullanıcı öznitelikleri"** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="7c4fd-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="7c4fd-170">Burada size hello eşledikten **kullanıcı tanımlayıcısı (nameid)** ile **ExtractMailPrefix()** işlevinin **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="7c4fd-171">Bu e-posta benzersiz kullanıcı kimliği hello hello kullanıcının hello önek değeri verir</span><span class="sxs-lookup"><span data-stu-id="7c4fd-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="7c4fd-172">Bu toohello Kronos uygulama her başarılı yanıt olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="7c4fd-174">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="7c4fd-175">a.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-175">a.</span></span> <span data-ttu-id="7c4fd-176">Merhaba kullanıcı tanımlayıcısı aşağı açılan listesinde seçin **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="7c4fd-177">b.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-177">b.</span></span> <span data-ttu-id="7c4fd-178">Merhaba, **posta** açılır listesinden, **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="7c4fd-179">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="7c4fd-181">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-181">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7c4fd-183">tooconfigure çoklu oturum açma üzerinde **Kronos** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Kronos destek ekibi](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="7c4fd-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="7c4fd-184">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7c4fd-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7c4fd-185">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7c4fd-186">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c4fd-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c4fd-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c4fd-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c4fd-188">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7c4fd-190">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c4fd-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c4fd-191">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c4fd-193">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c4fd-195">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c4fd-197">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c4fd-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c4fd-199">a.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-199">a.</span></span> <span data-ttu-id="7c4fd-200">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c4fd-201">b.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-201">b.</span></span> <span data-ttu-id="7c4fd-202">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c4fd-203">c.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-203">c.</span></span> <span data-ttu-id="7c4fd-204">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7c4fd-205">d.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-205">d.</span></span> <span data-ttu-id="7c4fd-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="7c4fd-207">Kronos test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c4fd-207">Creating a Kronos test user</span></span>

<span data-ttu-id="7c4fd-208">Bu bölümde, Kronos içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="7c4fd-209">Kronos uygulama hello uygulamada SSO yapmadan önce sağlanan tüm hello kullanıcılar toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="7c4fd-210">İş ile Merhaba [Kronos destek ekibi](https://www.kronos.in/contact/en-in/form) tooprovision bu kullanıcılar hello uygulamaya.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7c4fd-211">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7c4fd-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7c4fd-212">Bu bölümde, erişim tooKronos vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7c4fd-214">**tooassign Britta Simon tooKronos hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c4fd-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c4fd-215">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7c4fd-217">Merhaba uygulamalar listesinde **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-217">In hello applications list, select **Kronos**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="7c4fd-219">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7c4fd-221">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-221">Click **Add** button.</span></span> <span data-ttu-id="7c4fd-222">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7c4fd-224">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c4fd-225">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c4fd-226">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c4fd-227">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7c4fd-227">Testing single sign-on</span></span>

<span data-ttu-id="7c4fd-228">Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7c4fd-229">Hello erişim paneli Kronos döşeme hello tıkladığınızda, otomatik olarak oturum açma Kronos uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c4fd-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c4fd-230">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c4fd-230">Additional resources</span></span>

* [<span data-ttu-id="7c4fd-231">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7c4fd-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c4fd-232">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7c4fd-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

