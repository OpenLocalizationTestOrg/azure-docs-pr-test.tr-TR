---
title: "Öğretici: Azure Active Directory Tümleştirme ile FilesAnywhere | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FilesAnywhere arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="643f9-103">Öğretici: Azure Active Directory Tümleştirme FilesAnywhere ile</span><span class="sxs-lookup"><span data-stu-id="643f9-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="643f9-104">Bu öğreticide, bilgi nasıl toointegrate FilesAnywhere Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="643f9-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="643f9-105">FilesAnywhere Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="643f9-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="643f9-106">Erişim tooFilesAnywhere sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="643f9-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="643f9-107">Kullanıcıların tooautomatically get açan tooFilesAnywhere (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="643f9-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="643f9-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="643f9-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="643f9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="643f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="643f9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="643f9-110">Prerequisites</span></span>

<span data-ttu-id="643f9-111">tooconfigure FilesAnywhere ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="643f9-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="643f9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="643f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="643f9-113">Bir FilesAnywhere çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="643f9-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="643f9-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="643f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="643f9-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="643f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="643f9-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="643f9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="643f9-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="643f9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="643f9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="643f9-118">Scenario description</span></span>
<span data-ttu-id="643f9-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="643f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="643f9-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="643f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="643f9-121">Merhaba Galerisi'nden FilesAnywhere ekleme</span><span class="sxs-lookup"><span data-stu-id="643f9-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="643f9-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="643f9-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="643f9-123">Merhaba Galerisi'nden FilesAnywhere ekleme</span><span class="sxs-lookup"><span data-stu-id="643f9-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="643f9-124">Azure AD'ye tooconfigure hello tümleştirme FilesAnywhere, tooadd FilesAnywhere hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="643f9-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="643f9-125">**tooadd FilesAnywhere hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="643f9-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="643f9-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="643f9-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="643f9-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="643f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="643f9-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="643f9-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="643f9-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="643f9-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="643f9-133">Merhaba arama kutusuna yazın **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="643f9-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="643f9-135">Merhaba Sonuçlar panelinde seçin **FilesAnywhere**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="643f9-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="643f9-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="643f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="643f9-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FilesAnywhere sınayın.</span><span class="sxs-lookup"><span data-stu-id="643f9-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="643f9-139">Tek toowork'ın oturum açma hangi hello karşılık gelen FilesAnywhere içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="643f9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="643f9-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı FilesAnywhere hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="643f9-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="643f9-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** FilesAnywhere içinde.</span><span class="sxs-lookup"><span data-stu-id="643f9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="643f9-142">tooconfigure ve FilesAnywhere ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="643f9-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="643f9-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="643f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="643f9-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="643f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="643f9-145">**[FilesAnywhere test kullanıcısı oluşturma](#creating-a-filesanywhere-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir FilesAnywhere içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="643f9-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="643f9-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="643f9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="643f9-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="643f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="643f9-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="643f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="643f9-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FilesAnywhere uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="643f9-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="643f9-150">**tooconfigure Azure AD çoklu oturum açma ile FilesAnywhere, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="643f9-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="643f9-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **FilesAnywhere** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="643f9-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="643f9-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="643f9-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="643f9-155">Merhaba üzerinde **FilesAnywhere etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="643f9-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="643f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="643f9-157">a.</span></span> <span data-ttu-id="643f9-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="643f9-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="643f9-159">Lütfen bu hello değerini not edin **215** olan bir **ClientID** ve yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="643f9-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="643f9-160">Tooreplace ihtiyacınız hello gerçek ClientID değeri ile.</span><span class="sxs-lookup"><span data-stu-id="643f9-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="643f9-161">Merhaba üzerinde **FilesAnywhere etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="643f9-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="643f9-163">a.</span><span class="sxs-lookup"><span data-stu-id="643f9-163">a.</span></span> <span data-ttu-id="643f9-164">Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları** seçeneği</span><span class="sxs-lookup"><span data-stu-id="643f9-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="643f9-165">b.</span><span class="sxs-lookup"><span data-stu-id="643f9-165">b.</span></span> <span data-ttu-id="643f9-166">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="643f9-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="643f9-167">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="643f9-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="643f9-168">Tooupdate hello gerçek oturum üzerinde URL'si ve yanıt URL'si ile bu değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="643f9-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="643f9-169">Kişi [FilesAnywhere destek ekibi](mailto:support@FilesAnywhere.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="643f9-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="643f9-170">FilesAnywhere yazılım uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="643f9-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="643f9-171">Lütfen bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="643f9-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="643f9-172">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="643f9-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="643f9-173">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="643f9-173">hello following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="643f9-175">Ne zaman, kullanıcılar işaretleriyle yukarı hello değeri elde FilesAnywhere hello **ClientID** özniteliğini [FilesAnywhere takım](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="643f9-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="643f9-176">FilesAnywhere tarafından sağlanan hello benzersiz değer ile tooadd hello "İstemci kimliği" özniteliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="643f9-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="643f9-177">Yukarıda gösterilen bu öznitelikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="643f9-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="643f9-178">Lütfen bu hello değerini not edin **2331** , **ClientID** yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="643f9-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="643f9-179">Tooprovide hello gerçek değer gerekir.</span><span class="sxs-lookup"><span data-stu-id="643f9-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="643f9-180">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="643f9-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="643f9-181">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="643f9-181">Attribute Name</span></span> | <span data-ttu-id="643f9-182">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="643f9-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="643f9-183">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="643f9-183">clientid</span></span> | <span data-ttu-id="643f9-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="643f9-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="643f9-185">a.</span><span class="sxs-lookup"><span data-stu-id="643f9-185">a.</span></span> <span data-ttu-id="643f9-186">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="643f9-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="643f9-189">b.</span><span class="sxs-lookup"><span data-stu-id="643f9-189">b.</span></span> <span data-ttu-id="643f9-190">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="643f9-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="643f9-191">c.</span><span class="sxs-lookup"><span data-stu-id="643f9-191">c.</span></span> <span data-ttu-id="643f9-192">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="643f9-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="643f9-193">d.</span><span class="sxs-lookup"><span data-stu-id="643f9-193">d.</span></span> <span data-ttu-id="643f9-194">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="643f9-194">Click **Ok**</span></span>

7. <span data-ttu-id="643f9-195">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="643f9-195">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="643f9-197">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="643f9-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="643f9-199">Merhaba üzerinde **FilesAnywhere yapılandırma** 'yi tıklatın **yapılandırma FilesAnywhere** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="643f9-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="643f9-202">tooget SSO yapılandırması tamamlandı FilesAnywhere uçtaki kişi, uygulamanız için [FilesAnywhere destek ekibi](mailto:support@FilesAnywhere.com) ve indirilen hello SAML belirteç sertifika ve çoklu oturum açma (SSO) URL imzalama verin.</span><span class="sxs-lookup"><span data-stu-id="643f9-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="643f9-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="643f9-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="643f9-204">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="643f9-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="643f9-206">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="643f9-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="643f9-207">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="643f9-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="643f9-209">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="643f9-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="643f9-211">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="643f9-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="643f9-213">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="643f9-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="643f9-215">a.</span><span class="sxs-lookup"><span data-stu-id="643f9-215">a.</span></span> <span data-ttu-id="643f9-216">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="643f9-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="643f9-217">b.</span><span class="sxs-lookup"><span data-stu-id="643f9-217">b.</span></span> <span data-ttu-id="643f9-218">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="643f9-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="643f9-219">c.</span><span class="sxs-lookup"><span data-stu-id="643f9-219">c.</span></span> <span data-ttu-id="643f9-220">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="643f9-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="643f9-221">d.</span><span class="sxs-lookup"><span data-stu-id="643f9-221">d.</span></span> <span data-ttu-id="643f9-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="643f9-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="643f9-223">FilesAnywhere test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="643f9-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="643f9-224">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="643f9-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="643f9-225">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="643f9-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="643f9-226">Bu bölümde, kendi erişim tooFilesAnywhere vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="643f9-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="643f9-228">**tooassign Britta Simon tooFilesAnywhere hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="643f9-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="643f9-229">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="643f9-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="643f9-231">Merhaba uygulamalar listesinde **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="643f9-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="643f9-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="643f9-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="643f9-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="643f9-235">Click **Add** button.</span></span> <span data-ttu-id="643f9-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="643f9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="643f9-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="643f9-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="643f9-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="643f9-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="643f9-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="643f9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="643f9-241">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="643f9-241">Testing single sign-on</span></span>

<span data-ttu-id="643f9-242">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="643f9-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="643f9-243">Merhaba FilesAnywhere hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour FilesAnywhere uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="643f9-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="643f9-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="643f9-244">Additional resources</span></span>

* [<span data-ttu-id="643f9-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="643f9-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="643f9-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="643f9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
