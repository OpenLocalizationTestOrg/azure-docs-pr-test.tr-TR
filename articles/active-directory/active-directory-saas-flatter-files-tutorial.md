---
title: "Öğretici: Azure Active Directory Tümleştirme daha düz dosyalarla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile daha düz dosyalar arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="bdd72-103">Öğretici: Azure Active Directory Tümleştirme ile daha düz dosyalar</span><span class="sxs-lookup"><span data-stu-id="bdd72-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="bdd72-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile daha düz dosyalar.</span><span class="sxs-lookup"><span data-stu-id="bdd72-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdd72-105">Azure AD ile daha düz dosyalar tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bdd72-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bdd72-106">Erişimi olan Azure AD'de denetim tooFlatter dosyaları</span><span class="sxs-lookup"><span data-stu-id="bdd72-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="bdd72-107">Kullanıcıların tooautomatically etkinleştirebilirsiniz açan tooFlatter dosyalarla (çoklu oturum açma) Azure AD hesaplarına Al</span><span class="sxs-lookup"><span data-stu-id="bdd72-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdd72-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bdd72-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bdd72-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdd72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdd72-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bdd72-110">Prerequisites</span></span>

<span data-ttu-id="bdd72-111">tooconfigure daha düz dosyalar ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdd72-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="bdd72-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bdd72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdd72-113">Bir daha düz dosyalar çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="bdd72-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdd72-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bdd72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdd72-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdd72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdd72-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bdd72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdd72-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdd72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdd72-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bdd72-118">Scenario description</span></span>
<span data-ttu-id="bdd72-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bdd72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdd72-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bdd72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdd72-121">Merhaba Galerisi'nden daha düz dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="bdd72-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="bdd72-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdd72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="bdd72-123">Merhaba Galerisi'nden daha düz dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="bdd72-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="bdd72-124">Azure AD'ye tooconfigure hello tümleştirme daha düz dosya tooadd daha düz dosyalar hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdd72-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdd72-125">**tooadd daha düz hello Galerisi dosyalardan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdd72-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdd72-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdd72-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bdd72-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bdd72-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bdd72-133">Merhaba arama kutusuna yazın **daha düz dosyalar**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-133">In hello search box, type **Flatter Files**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="bdd72-135">Merhaba Sonuçlar panelinde seçin **daha düz dosyalar**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bdd72-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdd72-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdd72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdd72-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı göre daha düz dosyalar ile test etme.</span><span class="sxs-lookup"><span data-stu-id="bdd72-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdd72-139">Tek toowork'ın oturum açma hangi hello karşılık gelen daha düz dosyalarında tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdd72-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="bdd72-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve daha düz dosyalarında hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdd72-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="bdd72-141">Merhaba hello değeri daha düz dosyalarında atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bdd72-142">tooconfigure ve daha düz dosyalar ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdd72-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdd72-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="bdd72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdd72-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="bdd72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdd72-145">**[Daha düz dosyalar test kullanıcısı oluşturma](#creating-a-flatter-files-test-user)**  -toohave karşılık gelen Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir daha düz dosyalarında biri.</span><span class="sxs-lookup"><span data-stu-id="bdd72-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdd72-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bdd72-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdd72-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="bdd72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdd72-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bdd72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdd72-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma daha düz dosyalar uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bdd72-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="bdd72-150">**tooconfigure Azure AD çoklu oturum açma daha düz dosyalarla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdd72-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdd72-151">Merhaba hello üzerinde Azure portal'ın **daha düz dosyalar** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bdd72-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bdd72-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="bdd72-155">Merhaba üzerinde **daha düz dosyalar etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.</span><span class="sxs-lookup"><span data-stu-id="bdd72-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="bdd72-157">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bdd72-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="bdd72-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bdd72-161">Merhaba üzerinde **daha düz dosyalar yapılandırma** 'yi tıklatın **yapılandırmak daha düz dosyalar** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bdd72-162">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="bdd72-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="bdd72-164">Oturum açma daha düz dosyalar uygulama yönetici olarak tooyour.</span><span class="sxs-lookup"><span data-stu-id="bdd72-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="bdd72-165">Tıklatın **PANO**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-165">Click **DASHBOARD**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="bdd72-167">Tıklatın **ayarları**ve ardından hello hello üzerinde aşağıdaki adımları gerçekleştirin **şirket** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="bdd72-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="bdd72-169">a.</span><span class="sxs-lookup"><span data-stu-id="bdd72-169">a.</span></span> <span data-ttu-id="bdd72-170">Seçin **SAML 2.0 kimlik doğrulaması için kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="bdd72-171">b.</span><span class="sxs-lookup"><span data-stu-id="bdd72-171">b.</span></span> <span data-ttu-id="bdd72-172">Tıklatın **SAML yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="bdd72-173">Merhaba üzerinde **SAML Yapılandırması** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdd72-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="bdd72-175">a.</span><span class="sxs-lookup"><span data-stu-id="bdd72-175">a.</span></span> <span data-ttu-id="bdd72-176">Merhaba, **etki alanı** metin kutusuna, kayıtlı etki alanınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="bdd72-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="bdd72-177">Bir kayıtlı bir etki alanı henüz, kişi yoksa daha düz dosyalarınızı takım aracılığıyla destek [ support@flatterfiles.com ](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="bdd72-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="bdd72-178">b.</span><span class="sxs-lookup"><span data-stu-id="bdd72-178">b.</span></span> <span data-ttu-id="bdd72-179">İçinde **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** kopyalanan Azure portalı form.</span><span class="sxs-lookup"><span data-stu-id="bdd72-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="bdd72-180">c.</span><span class="sxs-lookup"><span data-stu-id="bdd72-180">c.</span></span>  <span data-ttu-id="bdd72-181">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="bdd72-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="bdd72-182">d.</span><span class="sxs-lookup"><span data-stu-id="bdd72-182">d.</span></span> <span data-ttu-id="bdd72-183">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="bdd72-184">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bdd72-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bdd72-185">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="bdd72-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bdd72-186">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdd72-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdd72-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdd72-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdd72-188">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="bdd72-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bdd72-190">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdd72-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdd72-191">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdd72-193">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdd72-195">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdd72-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdd72-197">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdd72-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdd72-199">a.</span><span class="sxs-lookup"><span data-stu-id="bdd72-199">a.</span></span> <span data-ttu-id="bdd72-200">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdd72-201">b.</span><span class="sxs-lookup"><span data-stu-id="bdd72-201">b.</span></span> <span data-ttu-id="bdd72-202">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="bdd72-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdd72-203">c.</span><span class="sxs-lookup"><span data-stu-id="bdd72-203">c.</span></span> <span data-ttu-id="bdd72-204">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bdd72-205">d.</span><span class="sxs-lookup"><span data-stu-id="bdd72-205">d.</span></span> <span data-ttu-id="bdd72-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bdd72-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="bdd72-207">Daha düz dosyalar test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdd72-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="bdd72-208">Bu bölümde Hello amacı toocreate Britta Simon daha düz dosyalarında adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="bdd72-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="bdd72-209">**toocreate Britta Simon daha düz dosyalarında adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdd72-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdd72-210">Tooyour üzerinde oturum **daha düz dosyalar** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="bdd72-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="bdd72-211">Hello Gezinti hello sol taraftaki bölmede **ayarları**ve hello ardından **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Daha düz dosyalar kullanıcı oluştur](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="bdd72-213">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="bdd72-214">Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdd72-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Daha düz dosyalar kullanıcı oluştur](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="bdd72-216">a.</span><span class="sxs-lookup"><span data-stu-id="bdd72-216">a.</span></span> <span data-ttu-id="bdd72-217">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="bdd72-218">b.</span><span class="sxs-lookup"><span data-stu-id="bdd72-218">b.</span></span> <span data-ttu-id="bdd72-219">Merhaba, **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="bdd72-220">c.</span><span class="sxs-lookup"><span data-stu-id="bdd72-220">c.</span></span> <span data-ttu-id="bdd72-221">Merhaba, **e-posta adresi** metin kutusuna, hello Azure portal Britta'nın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="bdd72-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="bdd72-222">d.</span><span class="sxs-lookup"><span data-stu-id="bdd72-222">d.</span></span> <span data-ttu-id="bdd72-223">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bdd72-224">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bdd72-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bdd72-225">Bu bölümde, Britta Simon etkinleştirme verme tarafından toouse Azure çoklu oturum açma erişim tooFlatter dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bdd72-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bdd72-227">**tooassign Britta Simon tooFlatter dosyaları hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdd72-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdd72-228">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bdd72-230">Merhaba uygulamalar listesinde **daha düz dosyalar**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="bdd72-232">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bdd72-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bdd72-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdd72-234">Click **Add** button.</span></span> <span data-ttu-id="bdd72-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdd72-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bdd72-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bdd72-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bdd72-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdd72-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdd72-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdd72-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdd72-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bdd72-240">Testing single sign-on</span></span>

<span data-ttu-id="bdd72-241">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="bdd72-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdd72-242">Merhaba erişim paneli daha düz dosyalar döşeme hello tıkladığınızda, otomatik olarak imzalanmış üzerinde daha düz dosyalar uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdd72-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="bdd72-243">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdd72-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdd72-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bdd72-244">Additional resources</span></span>

* [<span data-ttu-id="bdd72-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bdd72-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdd72-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bdd72-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

