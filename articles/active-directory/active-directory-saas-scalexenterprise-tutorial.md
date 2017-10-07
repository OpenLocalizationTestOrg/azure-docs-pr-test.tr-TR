---
title: "Öğretici: Azure Active Directory Tümleştirme ScaleX kuruluş ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ScaleX kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="88c56-103">Öğretici: Azure Active Directory Tümleştirme ScaleX kuruluş ile</span><span class="sxs-lookup"><span data-stu-id="88c56-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="88c56-104">Bu öğreticide, bilgi nasıl toointegrate ScaleX kuruluş Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88c56-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88c56-105">ScaleX kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="88c56-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88c56-106">Erişim tooScaleX Kurumsal sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="88c56-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="88c56-107">Kullanıcıların tooautomatically get açan tooScaleX Enterprise (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="88c56-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88c56-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="88c56-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="88c56-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="88c56-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="88c56-110">Uygulama erişimi ve çoklu oturum açma ile nedir [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88c56-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88c56-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="88c56-111">Prerequisites</span></span>

<span data-ttu-id="88c56-112">tooconfigure ScaleX Kurumsal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="88c56-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="88c56-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="88c56-113">An Azure AD subscription</span></span>
- <span data-ttu-id="88c56-114">Bir ScaleX Kurumsal çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="88c56-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88c56-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="88c56-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88c56-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="88c56-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88c56-117">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="88c56-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="88c56-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88c56-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88c56-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="88c56-119">Scenario description</span></span>
<span data-ttu-id="88c56-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="88c56-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88c56-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="88c56-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88c56-122">Merhaba Galerisi'nden ScaleX Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="88c56-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="88c56-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="88c56-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="88c56-124">Merhaba Galerisi'nden ScaleX Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="88c56-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="88c56-125">tooAzure AD içinde tooconfigure hello tümleştirme ScaleX Enterprise tooadd ScaleX Kurumsal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="88c56-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88c56-126">**tooadd ScaleX Kurumsal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88c56-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88c56-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88c56-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="88c56-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88c56-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="88c56-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="88c56-132">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="88c56-134">Merhaba arama kutusuna yazın **ScaleX Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="88c56-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="88c56-136">Merhaba Sonuçlar panelinde seçin **ScaleX Kurumsal**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="88c56-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88c56-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="88c56-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88c56-139">Bu bölümde, yapılandırmanız ve ScaleX kuruluş ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="88c56-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88c56-140">Tek toowork'ın oturum açma hangi hello karşılık gelen ScaleX kuruluştaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="88c56-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="88c56-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve ScaleX kuruluştaki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="88c56-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="88c56-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ScaleX kuruluştaki.</span><span class="sxs-lookup"><span data-stu-id="88c56-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="88c56-143">tooconfigure ve ScaleX kuruluş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="88c56-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88c56-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="88c56-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88c56-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="88c56-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88c56-146">**[ScaleX Kurumsal test kullanıcısı oluşturma](#creating-a-scalex-enterprise-test-user)**  -toohave karşılık gelen, Britta Simon ScaleX kuruluştaki kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="88c56-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88c56-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="88c56-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88c56-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="88c56-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88c56-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="88c56-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88c56-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ScaleX Kurumsal uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88c56-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="88c56-151">**tooconfigure Azure AD çoklu oturum açma ScaleX kuruluş ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88c56-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="88c56-152">Merhaba hello üzerinde Azure portal'ın **ScaleX Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="88c56-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="88c56-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="88c56-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="88c56-156">Merhaba üzerinde **ScaleX kuruluş etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="88c56-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="88c56-158">a.</span><span class="sxs-lookup"><span data-stu-id="88c56-158">a.</span></span> <span data-ttu-id="88c56-159">Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="88c56-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="88c56-160">b.</span><span class="sxs-lookup"><span data-stu-id="88c56-160">b.</span></span> <span data-ttu-id="88c56-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="88c56-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="88c56-162">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="88c56-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="88c56-164">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="88c56-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="88c56-165">Bunlar hello gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="88c56-165">These are not hello real values.</span></span> <span data-ttu-id="88c56-166">Bu değerleri gerçek tanımlayıcısı, yanıt URL'si veya oturum açma URL'si hello ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="88c56-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="88c56-167">Kişi [ScaleX Kurumsal İstemci destek ekibi](http://info.rescale.com/contact_sales) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="88c56-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="88c56-168">ScaleX uygulamanızı hello SAML onaylar, toomodify özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="88c56-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="88c56-169">' I tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** onay kutusunu tooopen hello özel öznitelikleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="88c56-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="88c56-171">a.</span><span class="sxs-lookup"><span data-stu-id="88c56-171">a.</span></span> <span data-ttu-id="88c56-172">Merhaba özniteliği sağ tıklatın **adı** ve Sil'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="88c56-172">Right click hello attribute **name** and click delete.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="88c56-174">b.</span><span class="sxs-lookup"><span data-stu-id="88c56-174">b.</span></span> <span data-ttu-id="88c56-175">Tıklatın **emailaddress** özniteliği tooopen hello öznitelik Düzenle penceresi.</span><span class="sxs-lookup"><span data-stu-id="88c56-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="88c56-176">Kendi değerini değiştirmek **user.mail** çok**user.userprincipalname** ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="88c56-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="88c56-178">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="88c56-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="88c56-180">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-180">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="88c56-182">Merhaba üzerinde **ScaleX Kurumsal yapılandırma** 'yi tıklatın **ScaleX Kurumsal yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="88c56-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="88c56-183">Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="88c56-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="88c56-185">tooconfigure çoklu oturum açma üzerinde **ScaleX Kurumsal** tarafı, yönetici olarak oturum açma toohello ScaleX Kurumsal şirket Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="88c56-186">Merhaba hello üst menüde sağ tıklayın ve **Contoso Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="88c56-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88c56-187">Contoso yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="88c56-187">Contoso is just an example.</span></span> <span data-ttu-id="88c56-188">Bu, gerçek şirket adınızı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="88c56-188">This should be your actual Company Name.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="88c56-190">Seçin **tümleştirmeler** hello üst menüsünden ve select **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="88c56-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="88c56-192">Merhaba form aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="88c56-192">Complete hello form as follows:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="88c56-194">a.</span><span class="sxs-lookup"><span data-stu-id="88c56-194">a.</span></span> <span data-ttu-id="88c56-195">Seçin **"SSO ile doğrulanabilir herhangi bir kullanıcı oluşturun."**</span><span class="sxs-lookup"><span data-stu-id="88c56-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="88c56-196">b.</span><span class="sxs-lookup"><span data-stu-id="88c56-196">b.</span></span> <span data-ttu-id="88c56-197">**Hizmet sağlayıcısı saml**: yapıştırma hello değeri ***urn: OASIS: adları: tc: SAML:2.0:nameid-biçimi: kalıcı***</span><span class="sxs-lookup"><span data-stu-id="88c56-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="88c56-198">c.</span><span class="sxs-lookup"><span data-stu-id="88c56-198">c.</span></span> <span data-ttu-id="88c56-199">**ACS yanıt kimlik sağlayıcısı e-posta alanının adı**: hello değeri yapıştırın`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="88c56-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="88c56-200">d.</span><span class="sxs-lookup"><span data-stu-id="88c56-200">d.</span></span> <span data-ttu-id="88c56-201">**Kimlik sağlayıcısı EntityDescriptor varlık Tanıtıcısı:** Yapıştır hello **SAML varlık kimliği** değer hello Azure portal ' kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="88c56-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="88c56-202">e.</span><span class="sxs-lookup"><span data-stu-id="88c56-202">e.</span></span> <span data-ttu-id="88c56-203">**Kimlik sağlayıcısı SingleSignOnService URL'si:** Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="88c56-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="88c56-204">f.</span><span class="sxs-lookup"><span data-stu-id="88c56-204">f.</span></span> <span data-ttu-id="88c56-205">**Kimlik sağlayıcısı ortak X509 sertifikası:** not defteri ve Yapıştır hello içeriği bu kutuya hello Azure'ndan indirilen açık hello X509 sertifika.</span><span class="sxs-lookup"><span data-stu-id="88c56-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="88c56-206">Hiçbir satır hello hello sertifika içeriğini Orta sonlarını emin olun.</span><span class="sxs-lookup"><span data-stu-id="88c56-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="88c56-207">g.</span><span class="sxs-lookup"><span data-stu-id="88c56-207">g.</span></span> <span data-ttu-id="88c56-208">Aşağıdaki onay kutularını hello denetleyin: **etkin, NameID şifrelemek ve oturum AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="88c56-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="88c56-209">h.</span><span class="sxs-lookup"><span data-stu-id="88c56-209">h.</span></span> <span data-ttu-id="88c56-210">Tıklatın **güncelleştirme SSO ayarlarını** toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="88c56-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="88c56-211">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="88c56-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88c56-212">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="88c56-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88c56-213">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88c56-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88c56-214">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="88c56-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="88c56-215">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="88c56-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="88c56-217">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88c56-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88c56-218">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88c56-220">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88c56-222">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88c56-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88c56-224">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="88c56-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88c56-226">a.</span><span class="sxs-lookup"><span data-stu-id="88c56-226">a.</span></span> <span data-ttu-id="88c56-227">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88c56-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88c56-228">b.</span><span class="sxs-lookup"><span data-stu-id="88c56-228">b.</span></span> <span data-ttu-id="88c56-229">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="88c56-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88c56-230">c.</span><span class="sxs-lookup"><span data-stu-id="88c56-230">c.</span></span> <span data-ttu-id="88c56-231">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="88c56-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="88c56-232">d.</span><span class="sxs-lookup"><span data-stu-id="88c56-232">d.</span></span> <span data-ttu-id="88c56-233">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88c56-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="88c56-234">ScaleX Kurumsal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="88c56-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="88c56-235">tooenable Azure AD kullanıcıların toolog tooScaleX kuruluş'da, bunlar tooScaleX Kurumsal sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="88c56-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="88c56-236">Merhaba durumda ScaleX Enterprise sağlama otomatik bir görevdir ve el ile yapılan hiçbir adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="88c56-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="88c56-237">SSO kimlik bilgileriyle kimlik doğrulamasını başarıyla herhangi bir kullanıcı ScaleX yan hello üzerinde otomatik olarak sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="88c56-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88c56-238">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="88c56-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="88c56-239">Bu bölümde, kullanıcı erişim tooScaleX Kurumsal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="88c56-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="88c56-241">**tooassign Britta Simon tooScaleX Kurumsal hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="88c56-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="88c56-242">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="88c56-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="88c56-244">Merhaba uygulamalar listesinde **ScaleX Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="88c56-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="88c56-246">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="88c56-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="88c56-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="88c56-248">Click **Add** button.</span></span> <span data-ttu-id="88c56-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88c56-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="88c56-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="88c56-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88c56-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88c56-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88c56-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="88c56-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="88c56-254">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="88c56-254">Testing single sign-on</span></span>

<span data-ttu-id="88c56-255">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="88c56-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88c56-256">ScaleX Kurumsal döşeme hello erişim paneli hello tıklatın tooyour ScaleX Kurumsal uygulama otomatik olarak oturum açmış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="88c56-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="88c56-257">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="88c56-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="88c56-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="88c56-258">Additional resources</span></span>

* [<span data-ttu-id="88c56-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="88c56-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88c56-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="88c56-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

