---
title: "Öğretici: Azure Active Directory Tümleştirme ile Asana | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Asana arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="14a26-103">Öğretici: Azure Active Directory Tümleştirme Asana ile</span><span class="sxs-lookup"><span data-stu-id="14a26-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="14a26-104">Bu öğreticide, bilgi nasıl toointegrate Asana Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14a26-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14a26-105">Asana Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="14a26-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="14a26-106">Erişim tooAsana sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="14a26-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="14a26-107">Kullanıcıların tooautomatically get açan tooAsana (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="14a26-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14a26-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="14a26-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="14a26-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14a26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14a26-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="14a26-110">Prerequisites</span></span>

<span data-ttu-id="14a26-111">tooconfigure Asana ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="14a26-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="14a26-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="14a26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14a26-113">Bir Asana çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="14a26-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14a26-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="14a26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14a26-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="14a26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14a26-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="14a26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14a26-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14a26-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14a26-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="14a26-118">Scenario description</span></span>
<span data-ttu-id="14a26-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="14a26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14a26-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="14a26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14a26-121">Merhaba Galerisi'nden Asana ekleme</span><span class="sxs-lookup"><span data-stu-id="14a26-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="14a26-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="14a26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="14a26-123">Merhaba Galerisi'nden Asana ekleme</span><span class="sxs-lookup"><span data-stu-id="14a26-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="14a26-124">Azure AD'ye tooconfigure hello tümleştirme Asana, tooadd Asana hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="14a26-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="14a26-125">**tooadd Asana hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="14a26-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="14a26-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="14a26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="14a26-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="14a26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="14a26-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="14a26-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="14a26-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="14a26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="14a26-133">Merhaba arama kutusuna yazın **Asana**seçin **Asana** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="14a26-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="14a26-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="14a26-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="14a26-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Asana ile test etme</span><span class="sxs-lookup"><span data-stu-id="14a26-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="14a26-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Asana içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="14a26-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="14a26-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Asana hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="14a26-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="14a26-139">Merhaba hello değeri Asana içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="14a26-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="14a26-140">tooconfigure ve Asana ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="14a26-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="14a26-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="14a26-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="14a26-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="14a26-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14a26-143">**[Bir Asana test kullanıcısı oluşturma](#create-an-asana-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Asana içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="14a26-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="14a26-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="14a26-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14a26-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="14a26-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="14a26-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="14a26-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="14a26-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Asana uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="14a26-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="14a26-148">**tooconfigure Azure AD çoklu oturum açma ile Asana, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="14a26-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="14a26-149">Hello hello üzerinde Azure portal'ın **Asana** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="14a26-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="14a26-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="14a26-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="14a26-153">Merhaba üzerinde **Asana etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="14a26-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Asana etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="14a26-155">a.</span><span class="sxs-lookup"><span data-stu-id="14a26-155">a.</span></span> <span data-ttu-id="14a26-156">Merhaba, **oturum açma URL'si** metin kutusuna, türü URL'si:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="14a26-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="14a26-157">b.</span><span class="sxs-lookup"><span data-stu-id="14a26-157">b.</span></span> <span data-ttu-id="14a26-158">Merhaba, **tanımlayıcısı** metin kutusuna, tür değeri:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="14a26-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="14a26-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="14a26-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="14a26-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="14a26-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14a26-163">Merhaba üzerinde **Asana yapılandırma** 'yi tıklatın **yapılandırma Asana** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="14a26-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="14a26-164">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="14a26-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Asana yapılandırma](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="14a26-166">Farklı bir tarayıcı penceresinde oturum açma Asana uygulama tooyour.</span><span class="sxs-lookup"><span data-stu-id="14a26-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="14a26-167">tooconfigure Asana, erişim hello çalışma alanı ayarları'hello çalışma hello sağ üst köşesinde hello ekran adına tıklayarak SSO.</span><span class="sxs-lookup"><span data-stu-id="14a26-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="14a26-168">Ardından, tıklatın  **\<çalışma alanı adınız\> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="14a26-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Asana sso ayarları](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="14a26-170">Merhaba üzerinde **kuruluş ayarları** penceresinde tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="14a26-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="14a26-171">Ardından **üyeleri gerekir oturum SAML** tooenable hello SSO yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="14a26-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="14a26-172">Merhaba hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="14a26-172">hello perform hello following steps:</span></span>
   
    ![Çoklu oturum açma kuruluş ayarlarını yapılandırma](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="14a26-174">a.</span><span class="sxs-lookup"><span data-stu-id="14a26-174">a.</span></span> <span data-ttu-id="14a26-175">Merhaba, **oturum açma sayfası URL'si** metin kutusuna, Yapıştır hello **SAML çoklu oturum açma hizmet URL'si**.</span><span class="sxs-lookup"><span data-stu-id="14a26-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="14a26-176">b.</span><span class="sxs-lookup"><span data-stu-id="14a26-176">b.</span></span> <span data-ttu-id="14a26-177">Azure portalından indirdiğiniz hello sertifikayı sağ tıklatın, sonra hello sertifika dosyasını Not Defteri'nde veya tercih edilen metin düzenleyiciyi kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="14a26-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="14a26-178">Merhaba arasında kopyalama hello içerik başlamak ve hello son sertifika başlık ve hello yapıştırın **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="14a26-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="14a26-179">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14a26-179">Click **Save**.</span></span> <span data-ttu-id="14a26-180">Çok Git[SSO'yu ayarlamak için Asana Kılavuzu](https://asana.com/guide/help/premium/authentication#gl-saml) daha fazla yardıma ihtiyacınız varsa.</span><span class="sxs-lookup"><span data-stu-id="14a26-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="14a26-181">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="14a26-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="14a26-182">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="14a26-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="14a26-183">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14a26-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="14a26-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="14a26-184">Create an Azure AD test user</span></span>

<span data-ttu-id="14a26-185">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="14a26-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="14a26-187">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="14a26-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="14a26-188">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="14a26-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14a26-190">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="14a26-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14a26-192">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="14a26-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14a26-194">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="14a26-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14a26-196">a.</span><span class="sxs-lookup"><span data-stu-id="14a26-196">a.</span></span> <span data-ttu-id="14a26-197">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14a26-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14a26-198">b.</span><span class="sxs-lookup"><span data-stu-id="14a26-198">b.</span></span> <span data-ttu-id="14a26-199">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="14a26-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14a26-200">c.</span><span class="sxs-lookup"><span data-stu-id="14a26-200">c.</span></span> <span data-ttu-id="14a26-201">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="14a26-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="14a26-202">d.</span><span class="sxs-lookup"><span data-stu-id="14a26-202">d.</span></span> <span data-ttu-id="14a26-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14a26-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="14a26-204">Bir Asana test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="14a26-204">Create an Asana test user</span></span>

<span data-ttu-id="14a26-205">Bu bölümde, Asana içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14a26-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="14a26-206">Üzerinde **Asana**, Git toohello **takımlar** hello Sol paneldeki bölümü.</span><span class="sxs-lookup"><span data-stu-id="14a26-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="14a26-207">Yanı sıra düğmesi oturum Hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="14a26-207">Click hello plus sign button.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="14a26-209">Tür hello e-posta britta.simon@contoso.com hello metin kutusuna ve ardından **davet**.</span><span class="sxs-lookup"><span data-stu-id="14a26-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="14a26-210">Tıklatın **Gönder davet**.</span><span class="sxs-lookup"><span data-stu-id="14a26-210">Click **Send Invite**.</span></span> <span data-ttu-id="14a26-211">Merhaba yeni kullanıcı bir e-posta kendi e-posta dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="14a26-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="14a26-212">Kendisinin toocreate gerekir ve hello hesabı doğrulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="14a26-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="14a26-213">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="14a26-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="14a26-214">Bu bölümde, erişim tooAsana vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="14a26-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Merhaba kullanıcı rolü atayın][200]

<span data-ttu-id="14a26-216">**tooassign Britta Simon tooAsana hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="14a26-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="14a26-217">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="14a26-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="14a26-219">Merhaba uygulamalar listesinde **Asana**.</span><span class="sxs-lookup"><span data-stu-id="14a26-219">In hello applications list, select **Asana**.</span></span>

    ![Merhaba Asana bağlantı hello uygulamalar listesinde](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="14a26-221">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="14a26-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="14a26-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="14a26-223">Click **Add** button.</span></span> <span data-ttu-id="14a26-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="14a26-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="14a26-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="14a26-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="14a26-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="14a26-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14a26-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="14a26-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="14a26-229">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="14a26-229">Test single sign-on</span></span>

<span data-ttu-id="14a26-230">Bu bölümde Hello amacı, Azure AD çoklu oturum açma tootest değil.</span><span class="sxs-lookup"><span data-stu-id="14a26-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="14a26-231">TooAsana oturum açma sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="14a26-231">Go tooAsana login page.</span></span> <span data-ttu-id="14a26-232">Merhaba e-posta adresi metin kutusuna hello e-posta adresi eklemek britta.simon@contoso.com. Merhaba parola metin kutusunu boş bırakın ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="14a26-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="14a26-233">Yeniden yönlendirilen tooAzure AD oturum açma sayfasına olacaktır.</span><span class="sxs-lookup"><span data-stu-id="14a26-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="14a26-234">Azure AD kimlik bilgilerinizi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="14a26-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="14a26-235">Şimdi, Asana üzerinde oturum açtınız.</span><span class="sxs-lookup"><span data-stu-id="14a26-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14a26-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="14a26-236">Additional resources</span></span>

* [<span data-ttu-id="14a26-237">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="14a26-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14a26-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="14a26-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
