---
title: "Öğretici: Azure Active Directory Tümleştirme ile StatusPage | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile StatusPage arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="7c405-103">Öğretici: Azure Active Directory Tümleştirme StatusPage ile</span><span class="sxs-lookup"><span data-stu-id="7c405-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="7c405-104">Bu öğreticide, bilgi nasıl toointegrate StatusPage Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c405-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c405-105">StatusPage Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7c405-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c405-106">Erişim tooStatusPage sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c405-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="7c405-107">Kullanıcıların tooautomatically get açan tooStatusPage (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c405-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c405-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7c405-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7c405-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c405-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c405-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c405-110">Prerequisites</span></span>

<span data-ttu-id="7c405-111">tooconfigure StatusPage ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c405-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="7c405-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7c405-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c405-113">Bir StatusPage çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7c405-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c405-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7c405-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c405-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c405-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c405-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7c405-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c405-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c405-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c405-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7c405-118">Scenario description</span></span>
<span data-ttu-id="7c405-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7c405-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c405-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7c405-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c405-121">Merhaba Galerisi'nden StatusPage ekleme</span><span class="sxs-lookup"><span data-stu-id="7c405-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="7c405-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c405-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="7c405-123">Merhaba Galerisi'nden StatusPage ekleme</span><span class="sxs-lookup"><span data-stu-id="7c405-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="7c405-124">Azure AD'ye tooconfigure hello tümleştirme StatusPage, tooadd StatusPage hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c405-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c405-125">**tooadd StatusPage hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c405-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c405-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c405-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7c405-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c405-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c405-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7c405-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7c405-133">Merhaba arama kutusuna yazın **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="7c405-133">In hello search box, type **StatusPage**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="7c405-135">Merhaba Sonuçlar panelinde seçin **StatusPage**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7c405-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c405-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c405-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c405-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı StatusPage sınayın.</span><span class="sxs-lookup"><span data-stu-id="7c405-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c405-139">Tek toowork'ın oturum açma hangi hello karşılık gelen StatusPage içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c405-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="7c405-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı StatusPage hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c405-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="7c405-141">Merhaba hello değeri StatusPage içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7c405-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7c405-142">tooconfigure ve StatusPage ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c405-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c405-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7c405-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c405-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7c405-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c405-145">**[StatusPage test kullanıcısı oluşturma](#creating-a-statuspage-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir StatusPage içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7c405-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c405-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c405-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c405-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c405-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c405-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c405-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c405-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma StatusPage uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7c405-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="7c405-150">**tooconfigure Azure AD çoklu oturum açma ile StatusPage, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c405-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c405-151">Hello hello üzerinde Azure portal'ın **StatusPage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7c405-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7c405-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c405-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="7c405-155">Merhaba üzerinde **StatusPage etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c405-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="7c405-157">a.</span><span class="sxs-lookup"><span data-stu-id="7c405-157">a.</span></span> <span data-ttu-id="7c405-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="7c405-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="7c405-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c405-159">b.</span></span> <span data-ttu-id="7c405-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="7c405-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="7c405-161">Merhaba StatusPage destek ekibi ile iletişime geçin [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest meta veri gerekli tooconfigure çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c405-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="7c405-162">a.</span><span class="sxs-lookup"><span data-stu-id="7c405-162">a.</span></span> <span data-ttu-id="7c405-163">Merhaba meta verilerden hello veren değerini kopyalayın ve hello yapıştırma **tanımlayıcısı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7c405-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="7c405-164">b.</span><span class="sxs-lookup"><span data-stu-id="7c405-164">b.</span></span> <span data-ttu-id="7c405-165">Merhaba meta verilerden hello yanıt URL'si kopyalayıp hello yapıştırın **yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7c405-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="7c405-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7c405-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="7c405-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c405-170">Merhaba üzerinde **StatusPage yapılandırma** 'yi tıklatın **yapılandırma StatusPage** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7c405-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7c405-171">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7c405-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="7c405-173">Başka bir tarayıcı penceresinde tooyour StatusPage şirket sitesinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7c405-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="7c405-174">Merhaba ana araç çubuğunda **hesabı Yönet**.</span><span class="sxs-lookup"><span data-stu-id="7c405-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="7c405-176">Merhaba tıklatın **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="7c405-178">Merhaba SSO Kurulum sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c405-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="7c405-181">a.</span><span class="sxs-lookup"><span data-stu-id="7c405-181">a.</span></span> <span data-ttu-id="7c405-182">Merhaba, **SSO hedef URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="7c405-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7c405-183">b.</span><span class="sxs-lookup"><span data-stu-id="7c405-183">b.</span></span> <span data-ttu-id="7c405-184">İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7c405-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="7c405-185">c.</span><span class="sxs-lookup"><span data-stu-id="7c405-185">c.</span></span> <span data-ttu-id="7c405-186">Tıklatın **yapılandırma kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="7c405-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="7c405-187">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7c405-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7c405-188">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7c405-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7c405-189">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c405-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c405-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c405-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c405-191">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7c405-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7c405-193">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c405-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c405-194">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c405-196">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7c405-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c405-198">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c405-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c405-200">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c405-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c405-202">a.</span><span class="sxs-lookup"><span data-stu-id="7c405-202">a.</span></span> <span data-ttu-id="7c405-203">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c405-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c405-204">b.</span><span class="sxs-lookup"><span data-stu-id="7c405-204">b.</span></span> <span data-ttu-id="7c405-205">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7c405-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c405-206">c.</span><span class="sxs-lookup"><span data-stu-id="7c405-206">c.</span></span> <span data-ttu-id="7c405-207">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7c405-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7c405-208">d.</span><span class="sxs-lookup"><span data-stu-id="7c405-208">d.</span></span> <span data-ttu-id="7c405-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c405-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="7c405-210">StatusPage test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c405-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="7c405-211">Bu bölümde Hello amacı toocreate Britta Simon içinde StatusPage adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="7c405-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="7c405-212">Yalnızca zaman sağlama StatusPage destekler.</span><span class="sxs-lookup"><span data-stu-id="7c405-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="7c405-213">İçinde zaten etkinleştirdiğiniz [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="7c405-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="7c405-214">**toocreate StatusPage içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c405-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c405-215">Yönetici olarak oturum açma tooyour StatusPage şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="7c405-216">Hello içinde hello üst menüsünde **hesabı Yönet**.</span><span class="sxs-lookup"><span data-stu-id="7c405-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="7c405-218">Merhaba tıklatın **ekip üyelerinin** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-218">Click hello **Team Members** tab.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="7c405-220">Tıklatın **Ekle ekip ÜYESİNE**.</span><span class="sxs-lookup"><span data-stu-id="7c405-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="7c405-222">Türü hello **e-posta adresi**, **ad**, ve **soyad** geçerli bir kullanıcı olarak hello tooprovision istediğiniz ilgili metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="7c405-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="7c405-224">Olarak **rol**, seçin **İstemci Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="7c405-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="7c405-225">Tıklatın **hesap oluştur**.</span><span class="sxs-lookup"><span data-stu-id="7c405-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7c405-226">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7c405-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7c405-227">Bu bölümde, erişim tooStatusPage vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c405-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7c405-229">**tooassign Britta Simon tooStatusPage hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c405-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c405-230">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c405-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7c405-232">Merhaba uygulamalar listesinde **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="7c405-232">In hello applications list, select **StatusPage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="7c405-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7c405-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7c405-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c405-236">Click **Add** button.</span></span> <span data-ttu-id="7c405-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c405-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7c405-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7c405-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c405-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c405-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c405-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c405-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c405-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7c405-242">Testing single sign-on</span></span>

<span data-ttu-id="7c405-243">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7c405-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7c405-244">Merhaba StatusPage hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour StatusPage uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c405-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c405-245">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c405-245">Additional resources</span></span>

* [<span data-ttu-id="7c405-246">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7c405-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c405-247">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7c405-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

