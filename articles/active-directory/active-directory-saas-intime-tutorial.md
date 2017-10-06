---
title: "Öğretici: Azure Active Directory Tümleştirme ile InTime | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile InTime arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="50dd8-103">Öğretici: Azure Active Directory Tümleştirme InTime ile</span><span class="sxs-lookup"><span data-stu-id="50dd8-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="50dd8-104">Bu öğreticide, bilgi nasıl toointegrate InTime Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50dd8-104">In this tutorial, you learn how toointegrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50dd8-105">InTime Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="50dd8-105">Integrating InTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="50dd8-106">Erişim tooInTime sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50dd8-106">You can control in Azure AD who has access tooInTime.</span></span>
- <span data-ttu-id="50dd8-107">Kullanıcıların tooautomatically get açan tooInTime (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50dd8-107">You can enable your users tooautomatically get signed-on tooInTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="50dd8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="50dd8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50dd8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50dd8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="50dd8-110">Prerequisites</span></span>

<span data-ttu-id="50dd8-111">tooconfigure InTime ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="50dd8-111">tooconfigure Azure AD integration with InTime, you need hello following items:</span></span>

- <span data-ttu-id="50dd8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="50dd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50dd8-113">Bir InTime çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="50dd8-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50dd8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="50dd8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50dd8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="50dd8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50dd8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="50dd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50dd8-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50dd8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50dd8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="50dd8-118">Scenario description</span></span>
<span data-ttu-id="50dd8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="50dd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50dd8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="50dd8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50dd8-121">Merhaba Galerisi'nden InTime ekleme</span><span class="sxs-lookup"><span data-stu-id="50dd8-121">Adding InTime from hello gallery</span></span>
2. <span data-ttu-id="50dd8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="50dd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-hello-gallery"></a><span data-ttu-id="50dd8-123">Merhaba Galerisi'nden InTime ekleme</span><span class="sxs-lookup"><span data-stu-id="50dd8-123">Adding InTime from hello gallery</span></span>
<span data-ttu-id="50dd8-124">Azure AD'ye tooconfigure hello tümleştirme InTime, tooadd InTime hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-124">tooconfigure hello integration of InTime into Azure AD, you need tooadd InTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="50dd8-125">**tooadd InTime hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50dd8-125">**tooadd InTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="50dd8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="50dd8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="50dd8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="50dd8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="50dd8-133">Merhaba arama kutusuna yazın **InTime**seçin **InTime** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="50dd8-133">In hello search box, type **InTime**, select **InTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde inTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="50dd8-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="50dd8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="50dd8-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı InTime sınayın.</span><span class="sxs-lookup"><span data-stu-id="50dd8-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50dd8-137">Tek toowork'ın oturum açma hangi hello karşılık gelen InTime içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InTime is tooa user in Azure AD.</span></span> <span data-ttu-id="50dd8-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı InTime hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-138">In other words, a link relationship between an Azure AD user and hello related user in InTime needs toobe established.</span></span>

<span data-ttu-id="50dd8-139">Merhaba hello değeri InTime içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-139">In InTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="50dd8-140">tooconfigure ve InTime ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="50dd8-140">tooconfigure and test Azure AD single sign-on with InTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="50dd8-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="50dd8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="50dd8-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="50dd8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50dd8-143">**[InTime test kullanıcısı oluşturma](#create-a-intime-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir InTime içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="50dd8-143">**[Create a InTime test user](#create-a-intime-test-user)** - toohave a counterpart of Britta Simon in InTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="50dd8-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="50dd8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50dd8-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="50dd8-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="50dd8-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="50dd8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="50dd8-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma InTime uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="50dd8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="50dd8-148">**tooconfigure Azure AD çoklu oturum açma ile InTime, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50dd8-148">**tooconfigure Azure AD single sign-on with InTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="50dd8-149">Hello hello üzerinde Azure portal'ın **InTime** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-149">In hello Azure portal, on hello **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="50dd8-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="50dd8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="50dd8-153">Merhaba üzerinde **InTime etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="50dd8-153">On hello **InTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Oturum açma bilgileri inTime etki alanı ve URL'leri tek](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="50dd8-155">a.</span><span class="sxs-lookup"><span data-stu-id="50dd8-155">a.</span></span> <span data-ttu-id="50dd8-156">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="50dd8-156">In hello **Sign-on URL** textbox, type hello URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="50dd8-157">b.</span><span class="sxs-lookup"><span data-stu-id="50dd8-157">b.</span></span> <span data-ttu-id="50dd8-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="50dd8-158">In hello **Identifier** textbox, type hello URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="50dd8-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="50dd8-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="50dd8-161">InTime uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="50dd8-161">Your InTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="50dd8-162">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-162">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="50dd8-163">Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak InTime hello kullanıcının e-posta adresiyle eşleşen bu toobe bekliyor.</span><span class="sxs-lookup"><span data-stu-id="50dd8-163">hello default value of **User Identifier** is **user.userprincipalname** but InTime expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="50dd8-164">Bunun için kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın</span><span class="sxs-lookup"><span data-stu-id="50dd8-164">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration</span></span> 

    ![Öznitelik yapılandırma](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="50dd8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-166">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="50dd8-168">Merhaba üzerinde **InTime yapılandırma** 'yi tıklatın **yapılandırma InTime** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-168">On hello **InTime Configuration** section, click **Configure InTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="50dd8-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="50dd8-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![İnTime yapılandırma](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="50dd8-171">tooconfigure çoklu oturum açma üzerinde **InTime** yan, indirilen toosend hello ihtiyacınız **meta veri XML**, **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** çok[İnTime destek ekibi](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="50dd8-171">tooconfigure single sign-on on **InTime** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** too[InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="50dd8-172">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="50dd8-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="50dd8-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="50dd8-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="50dd8-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="50dd8-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="50dd8-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50dd8-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="50dd8-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="50dd8-176">Create an Azure AD test user</span></span>

<span data-ttu-id="50dd8-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="50dd8-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="50dd8-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50dd8-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="50dd8-180">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-180">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="50dd8-182">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-182">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="50dd8-184">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="50dd8-184">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="50dd8-186">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="50dd8-186">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="50dd8-188">a.</span><span class="sxs-lookup"><span data-stu-id="50dd8-188">a.</span></span> <span data-ttu-id="50dd8-189">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-189">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50dd8-190">b.</span><span class="sxs-lookup"><span data-stu-id="50dd8-190">b.</span></span> <span data-ttu-id="50dd8-191">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="50dd8-191">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="50dd8-192">c.</span><span class="sxs-lookup"><span data-stu-id="50dd8-192">c.</span></span> <span data-ttu-id="50dd8-193">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="50dd8-193">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="50dd8-194">d.</span><span class="sxs-lookup"><span data-stu-id="50dd8-194">d.</span></span> <span data-ttu-id="50dd8-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50dd8-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="50dd8-196">InTime test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="50dd8-196">Create a InTime test user</span></span>

<span data-ttu-id="50dd8-197">Bu bölümde, InTime içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="50dd8-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="50dd8-198">Çalışmak [InTime destek ekibi](mailto:hdollard@intimesoft.com) tooadd hello kullanıcılar hello InTime Platform.</span><span class="sxs-lookup"><span data-stu-id="50dd8-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) tooadd hello users in hello InTime platform.</span></span> <span data-ttu-id="50dd8-199">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="50dd8-200">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="50dd8-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="50dd8-201">Bu bölümde, erişim tooInTime vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="50dd8-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInTime.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="50dd8-203">**tooassign Britta Simon tooInTime hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50dd8-203">**tooassign Britta Simon tooInTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="50dd8-204">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="50dd8-206">Merhaba uygulamalar listesinde **InTime**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-206">In hello applications list, select **InTime**.</span></span>

    ![Merhaba InTime hello uygulamalar listesinde bağlantı](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="50dd8-208">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="50dd8-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="50dd8-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50dd8-210">Click **Add** button.</span></span> <span data-ttu-id="50dd8-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="50dd8-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="50dd8-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="50dd8-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="50dd8-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="50dd8-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50dd8-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="50dd8-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="50dd8-216">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="50dd8-216">Test single sign-on</span></span>

<span data-ttu-id="50dd8-217">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="50dd8-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="50dd8-218">Merhaba InTime kutucuğa tıkladığınızda de erişim paneli Merhaba, hello oturum açma sayfasına InTime uygulamanızın almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-218">When you click hello InTime tile in hello Access Panel, you should get hello login page of your InTime application.</span></span> <span data-ttu-id="50dd8-219">Merhaba tıklatın **oturum açma** düğmesi, sonra da IdPs bir dizi düğmeleri listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="50dd8-219">Click hello **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="50dd8-220">tıklatın **IDP adı** tarafından verilen [InTime destek ekibi](mailto:hdollard@intimesoft.com) toologin InTime uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="50dd8-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) toologin into your InTime application.</span></span> <span data-ttu-id="50dd8-221">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50dd8-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50dd8-222">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="50dd8-222">Additional resources</span></span>

* [<span data-ttu-id="50dd8-223">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="50dd8-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50dd8-224">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="50dd8-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

