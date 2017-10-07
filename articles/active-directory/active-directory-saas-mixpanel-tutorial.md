---
title: "Öğretici: Azure Active Directory Tümleştirme ile Mixpanel | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mixpanel arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="6ef4d-103">Öğretici: Azure Active Directory Tümleştirme Mixpanel ile</span><span class="sxs-lookup"><span data-stu-id="6ef4d-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="6ef4d-104">Bu öğreticide, bilgi nasıl toointegrate Mixpanel Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ef4d-104">In this tutorial, you learn how toointegrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ef4d-105">Mixpanel Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-105">Integrating Mixpanel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6ef4d-106">Erişim tooMixpanel sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6ef4d-106">You can control in Azure AD who has access tooMixpanel</span></span>
- <span data-ttu-id="6ef4d-107">Kullanıcıların tooautomatically get açan tooMixpanel (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6ef4d-107">You can enable your users tooautomatically get signed-on tooMixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ef4d-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6ef4d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6ef4d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ef4d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ef4d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6ef4d-110">Prerequisites</span></span>

<span data-ttu-id="6ef4d-111">tooconfigure Mixpanel ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-111">tooconfigure Azure AD integration with Mixpanel, you need hello following items:</span></span>

- <span data-ttu-id="6ef4d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6ef4d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ef4d-113">Bir Mixpanel çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6ef4d-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ef4d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ef4d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ef4d-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ef4d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ef4d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ef4d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6ef4d-118">Scenario description</span></span>
<span data-ttu-id="6ef4d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ef4d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ef4d-121">Merhaba Galerisi'nden Mixpanel ekleme</span><span class="sxs-lookup"><span data-stu-id="6ef4d-121">Adding Mixpanel from hello gallery</span></span>
2. <span data-ttu-id="6ef4d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6ef4d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-hello-gallery"></a><span data-ttu-id="6ef4d-123">Merhaba Galerisi'nden Mixpanel ekleme</span><span class="sxs-lookup"><span data-stu-id="6ef4d-123">Adding Mixpanel from hello gallery</span></span>
<span data-ttu-id="6ef4d-124">Azure AD'ye tooconfigure hello tümleştirme Mixpanel, tooadd Mixpanel hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-124">tooconfigure hello integration of Mixpanel into Azure AD, you need tooadd Mixpanel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6ef4d-125">**tooadd Mixpanel hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6ef4d-125">**tooadd Mixpanel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ef4d-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ef4d-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6ef4d-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6ef4d-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6ef4d-133">Merhaba arama kutusuna yazın **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-133">In hello search box, type **Mixpanel**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="6ef4d-135">Merhaba Sonuçlar panelinde seçin **Mixpanel**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-135">In hello results panel, select **Mixpanel**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ef4d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6ef4d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ef4d-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Mixpanel sınayın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ef4d-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Mixpanel içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mixpanel is tooa user in Azure AD.</span></span> <span data-ttu-id="6ef4d-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Mixpanel hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-140">In other words, a link relationship between an Azure AD user and hello related user in Mixpanel needs toobe established.</span></span>

<span data-ttu-id="6ef4d-141">Merhaba hello değeri Mixpanel içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-141">In Mixpanel, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6ef4d-142">tooconfigure ve Mixpanel ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-142">tooconfigure and test Azure AD single sign-on with Mixpanel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6ef4d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6ef4d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ef4d-145">**[Mixpanel test kullanıcısı oluşturma](#creating-a-mixpanel-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Mixpanel içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - toohave a counterpart of Britta Simon in Mixpanel that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ef4d-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ef4d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ef4d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6ef4d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ef4d-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mixpanel uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="6ef4d-150">**tooconfigure Azure AD çoklu oturum açma ile Mixpanel, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6ef4d-150">**tooconfigure Azure AD single sign-on with Mixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ef4d-151">Hello hello üzerinde Azure portal'ın **Mixpanel** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-151">In hello Azure portal, on hello **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6ef4d-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="6ef4d-155">Merhaba üzerinde **Mixpanel etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-155">On hello **Mixpanel Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="6ef4d-157">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="6ef4d-157">In hello **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ef4d-158">Lütfen adresindeki kayıt [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset oturum açma kimlik bilgilerinizi ve kişi hello yukarı [Mixpanel destek ekibi](mailto:support@mixpanel.com) kiracınız için tooenable SSO ayarları.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset up your login credentials and  contact hello [Mixpanel support team](mailto:support@mixpanel.com) tooenable SSO settings for your tenant.</span></span> <span data-ttu-id="6ef4d-159">Ayrıca, üzerinde oturum URL değeri gerekirse Mixpanel destek ekibinden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="6ef4d-160">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="6ef4d-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-162">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ef4d-164">Merhaba üzerinde **Mixpanel yapılandırma** 'yi tıklatın **yapılandırma Mixpanel** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-164">On hello **Mixpanel Configuration** section, click **Configure Mixpanel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6ef4d-165">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6ef4d-165">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="6ef4d-167">Farklı bir tarayıcı penceresinde tooyour Mixpanel uygulama yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-167">In a different browser window, sign-on tooyour Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="6ef4d-168">Merhaba sayfanın en altındaki üzerinde hello biraz tıklatın **gear** hello sol alt köşesindeki simgesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-168">On bottom of hello page, click hello little **gear** icon in hello left corner.</span></span> 
   
    ![Mixpanel çoklu oturum açma](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="6ef4d-170">Merhaba tıklatın **erişim güvenlik** sekmesini ve ardından **Ayarları Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-170">Click hello **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="6ef4d-172">Merhaba üzerinde **sertifikanızı değiştirme** iletişim sayfasında, tıklatın **dosya** tooupload indirilen sertifika ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-172">On hello **Change your certificate** dialog page, click **Choose file** tooupload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="6ef4d-174">Merhaba kimlik doğrulama URL'si metin kutusuna hello üzerinde **, kimlik doğrulaması URL'sini değiştirmek** iletişim sayfasında, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** hangi Azure portalından kopyaladığınız ve ardından **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-174">In hello authentication URL textbox on hello **Change your authentication  URL** dialog page, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="6ef4d-176">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="6ef4d-177">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6ef4d-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6ef4d-178">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6ef4d-179">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ef4d-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ef4d-180">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ef4d-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ef4d-181">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6ef4d-183">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6ef4d-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ef4d-184">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ef4d-186">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ef4d-188">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ef4d-190">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6ef4d-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ef4d-192">a.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-192">a.</span></span> <span data-ttu-id="6ef4d-193">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ef4d-194">b.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-194">b.</span></span> <span data-ttu-id="6ef4d-195">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ef4d-196">c.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-196">c.</span></span> <span data-ttu-id="6ef4d-197">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6ef4d-198">d.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-198">d.</span></span> <span data-ttu-id="6ef4d-199">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="6ef4d-200">Mixpanel test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ef4d-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="6ef4d-201">Bu bölümde Hello amacı toocreate Britta Simon içinde Mixpanel adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-201">hello objective of this section is toocreate a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="6ef4d-202">Üzerinde tooyour Mixpanel şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-202">Sign on tooyour Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="6ef4d-203">Hello sayfanın hello üzerinde küçük bir dişli düğmesini hello sol köşe tooopen hello üzerinde hello tıklatın **ayarları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-203">On hello bottom of hello page, click hello little gear button on hello left corner tooopen hello **Settings** window.</span></span>

3. <span data-ttu-id="6ef4d-204">Merhaba tıklatın **takım** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-204">Click hello **Team** tab.</span></span>

4. <span data-ttu-id="6ef4d-205">Merhaba, **ekip üyesine** metin kutusuna, hello Azure Britta'nın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-205">In hello **team member** textbox, type Britta's email address in hello Azure.</span></span>
   
    ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="6ef4d-207">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="6ef4d-208">Merhaba kullanıcı bir e-posta tooset hello profil alır.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-208">hello user will get an email tooset up hello profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6ef4d-209">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6ef4d-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6ef4d-210">Bu bölümde, erişim tooMixpanel vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMixpanel.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6ef4d-212">**tooassign Britta Simon tooMixpanel hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6ef4d-212">**tooassign Britta Simon tooMixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ef4d-213">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6ef4d-215">Merhaba uygulamalar listesinde **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-215">In hello applications list, select **Mixpanel**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="6ef4d-217">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6ef4d-219">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-219">Click **Add** button.</span></span> <span data-ttu-id="6ef4d-220">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6ef4d-222">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6ef4d-223">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ef4d-224">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ef4d-225">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6ef4d-225">Testing single sign-on</span></span>

<span data-ttu-id="6ef4d-226">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6ef4d-227">Merhaba Mixpanel hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Mixpanel uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ef4d-227">When you click hello Mixpanel tile in hello Access Panel, you should get automatically signed-on tooyour Mixpanel application.</span></span>
<span data-ttu-id="6ef4d-228">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ef4d-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ef4d-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6ef4d-229">Additional resources</span></span>

* [<span data-ttu-id="6ef4d-230">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6ef4d-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ef4d-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6ef4d-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

