---
title: "Öğretici: Azure Active Directory Tümleştirme ile ServiceChannel | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ServiceChannel arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="7db7d-103">Öğretici: Azure Active Directory Tümleştirme ServiceChannel ile</span><span class="sxs-lookup"><span data-stu-id="7db7d-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="7db7d-104">Bu öğreticide, bilgi nasıl toointegrate ServiceChannel Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7db7d-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7db7d-105">ServiceChannel Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7db7d-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7db7d-106">Erişim tooServiceChannel sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7db7d-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="7db7d-107">Kullanıcıların tooautomatically get açan tooServiceChannel (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7db7d-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7db7d-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7db7d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="7db7d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7db7d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7db7d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7db7d-110">Prerequisites</span></span>

<span data-ttu-id="7db7d-111">tooconfigure ServiceChannel ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7db7d-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="7db7d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7db7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7db7d-113">Bir ServiceChannel çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7db7d-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7db7d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7db7d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7db7d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7db7d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7db7d-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7db7d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7db7d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7db7d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7db7d-118">Scenario description</span></span>
<span data-ttu-id="7db7d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7db7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7db7d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7db7d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7db7d-121">Merhaba Galerisi'nden ServiceChannel ekleme</span><span class="sxs-lookup"><span data-stu-id="7db7d-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="7db7d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7db7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="7db7d-123">Merhaba Galerisi'nden ServiceChannel ekleme</span><span class="sxs-lookup"><span data-stu-id="7db7d-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="7db7d-124">Azure AD'ye tooconfigure hello tümleştirme ServiceChannel, tooadd ServiceChannel hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7db7d-125">**tooadd ServiceChannel hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7db7d-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7db7d-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7db7d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7db7d-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7db7d-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7db7d-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7db7d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7db7d-133">Merhaba arama kutusuna yazın **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="7db7d-135">Merhaba Sonuçlar panelinde seçin **ServiceChannel**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7db7d-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7db7d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7db7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7db7d-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ServiceChannel sınayın.</span><span class="sxs-lookup"><span data-stu-id="7db7d-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7db7d-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ServiceChannel içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="7db7d-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ServiceChannel hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="7db7d-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ServiceChannel içinde.</span><span class="sxs-lookup"><span data-stu-id="7db7d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="7db7d-142">tooconfigure ve ServiceChannel ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7db7d-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7db7d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7db7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7db7d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7db7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7db7d-145">**[ServiceChannel test kullanıcısı oluşturma](#creating-a-servicechannel-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7db7d-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="7db7d-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7db7d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7db7d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7db7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7db7d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7db7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7db7d-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma ServiceChannel uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7db7d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="7db7d-150">**tooconfigure Azure AD çoklu oturum açma ile ServiceChannel, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7db7d-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="7db7d-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **ServiceChannel** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7db7d-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7db7d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="7db7d-155">Merhaba üzerinde **ServiceChannel etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7db7d-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="7db7d-157">a.</span><span class="sxs-lookup"><span data-stu-id="7db7d-157">a.</span></span> <span data-ttu-id="7db7d-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="7db7d-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="7db7d-159">b.</span><span class="sxs-lookup"><span data-stu-id="7db7d-159">b.</span></span> <span data-ttu-id="7db7d-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="7db7d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7db7d-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7db7d-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="7db7d-162">Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="7db7d-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7db7d-163">Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz.</span><span class="sxs-lookup"><span data-stu-id="7db7d-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="7db7d-164">Kişi [ServiceChannel destek ekibi](https://servicechannel.zendesk.com/hc/en-us) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7db7d-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="7db7d-165">ServiceChannel uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7db7d-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="7db7d-166">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="7db7d-167">**NameIdentifier (kullanıcı tanımlayıcısı)** yalnızca zorunlu talep hello ve hello varsayılan değer **user.userprincipalname** ancak ServiceChannel bekliyor ile eşlenmiş bu toobe **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="7db7d-168">Tooenable süre yalnızca kullanıcı sağlamayı planlıyorsanız, aşağıda gösterildiği gibi talep aşağıdaki hello eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="7db7d-169">**Rol** talep gereken çok eşlenen toobe**user.assignedroles** hello kullanıcının hello rolünü içerir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="7db7d-170">ServiceChannel Kılavuzu başvurabilir [burada](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) talepler hakkında daha fazla yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="7db7d-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="7db7d-172">Lütfen tıklatın [burada](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow nasıl tooconfigure **rol** Azure AD'de</span><span class="sxs-lookup"><span data-stu-id="7db7d-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="7db7d-173">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7db7d-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="7db7d-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="7db7d-174">Attribute Name</span></span> | <span data-ttu-id="7db7d-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="7db7d-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="7db7d-176">Rol</span><span class="sxs-lookup"><span data-stu-id="7db7d-176">Role</span></span>| <span data-ttu-id="7db7d-177">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="7db7d-177">user.assignedroles</span></span> |

    <span data-ttu-id="7db7d-178">a.</span><span class="sxs-lookup"><span data-stu-id="7db7d-178">a.</span></span> <span data-ttu-id="7db7d-179">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7db7d-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="7db7d-182">b.</span><span class="sxs-lookup"><span data-stu-id="7db7d-182">b.</span></span> <span data-ttu-id="7db7d-183">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="7db7d-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7db7d-184">c.</span><span class="sxs-lookup"><span data-stu-id="7db7d-184">c.</span></span> <span data-ttu-id="7db7d-185">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="7db7d-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7db7d-186">d.</span><span class="sxs-lookup"><span data-stu-id="7db7d-186">d.</span></span> <span data-ttu-id="7db7d-187">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="7db7d-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="7db7d-188">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7db7d-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="7db7d-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7db7d-190">Click **Save**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7db7d-192">Merhaba üzerinde **ServiceChannel yapılandırma** 'yi tıklatın **yapılandırma ServiceChannel** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7db7d-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7db7d-193">Lütfen hello Not **SAML Enitity kimliği** hello gelen **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7db7d-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="7db7d-194">tooconfigure çoklu oturum açma üzerinde **ServiceChannel** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)** ve **SAML varlık kimliği** çok[ ServiceChannel destek ekibi](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="7db7d-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="7db7d-195">Bunlar Bu sipariş toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlamanız.</span><span class="sxs-lookup"><span data-stu-id="7db7d-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7db7d-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7db7d-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="7db7d-197">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7db7d-199">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7db7d-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7db7d-200">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7db7d-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7db7d-202">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="7db7d-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7db7d-204">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7db7d-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7db7d-206">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7db7d-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7db7d-208">a.</span><span class="sxs-lookup"><span data-stu-id="7db7d-208">a.</span></span> <span data-ttu-id="7db7d-209">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7db7d-210">b.</span><span class="sxs-lookup"><span data-stu-id="7db7d-210">b.</span></span> <span data-ttu-id="7db7d-211">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7db7d-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7db7d-212">c.</span><span class="sxs-lookup"><span data-stu-id="7db7d-212">c.</span></span> <span data-ttu-id="7db7d-213">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7db7d-214">d.</span><span class="sxs-lookup"><span data-stu-id="7db7d-214">d.</span></span> <span data-ttu-id="7db7d-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7db7d-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="7db7d-216">ServiceChannel test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7db7d-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="7db7d-217">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="7db7d-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="7db7d-218">Tam kullanıcı sağlama için temasa [ServiceChannel destek ekibi](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="7db7d-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7db7d-219">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7db7d-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7db7d-220">Bu bölümde, kendi erişim tooServiceChannel vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7db7d-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7db7d-222">**tooassign Britta Simon tooServiceChannel hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7db7d-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="7db7d-223">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7db7d-225">Merhaba uygulamalar listesinde **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="7db7d-227">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7db7d-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7db7d-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7db7d-229">Click **Add** button.</span></span> <span data-ttu-id="7db7d-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7db7d-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7db7d-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7db7d-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7db7d-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7db7d-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7db7d-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7db7d-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7db7d-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7db7d-235">Testing single sign-on</span></span>

<span data-ttu-id="7db7d-236">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7db7d-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7db7d-237">Merhaba ServiceChannel hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ServiceChannel uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7db7d-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7db7d-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7db7d-238">Additional resources</span></span>

* [<span data-ttu-id="7db7d-239">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7db7d-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7db7d-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7db7d-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png