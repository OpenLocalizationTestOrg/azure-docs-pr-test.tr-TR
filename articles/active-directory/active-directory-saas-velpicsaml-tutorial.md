---
title: "Öğretici: Azure Active Directory Tümleştirme Velpic SAML ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Velpic SAML arasında."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="eb31d-103">Öğretici: Azure Active Directory Tümleştirme Velpic SAML ile</span><span class="sxs-lookup"><span data-stu-id="eb31d-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="eb31d-104">Bu öğreticide, bilgi nasıl toointegrate Velpic SAML Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb31d-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb31d-105">Azure AD ile Velpic SAML tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="eb31d-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb31d-106">Erişim tooVelpic SAML sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eb31d-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="eb31d-107">Kullanıcıların tooautomatically get açan tooVelpic SAML (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eb31d-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb31d-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eb31d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="eb31d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb31d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb31d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eb31d-110">Prerequisites</span></span>

<span data-ttu-id="eb31d-111">tooconfigure Velpic SAML ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb31d-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="eb31d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="eb31d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb31d-113">Bir Velpic SAML çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="eb31d-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb31d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="eb31d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb31d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb31d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb31d-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="eb31d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb31d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb31d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="eb31d-118">Scenario description</span></span>
<span data-ttu-id="eb31d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb31d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="eb31d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb31d-121">Merhaba Galerisi'nden Velpic SAML ekleme</span><span class="sxs-lookup"><span data-stu-id="eb31d-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="eb31d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="eb31d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="eb31d-123">Merhaba Galerisi'nden Velpic SAML ekleme</span><span class="sxs-lookup"><span data-stu-id="eb31d-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="eb31d-124">Azure AD'ye tooconfigure hello tümleştirme Velpic SAML, tooadd Velpic SAML hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb31d-125">**tooadd Velpic SAML hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb31d-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb31d-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb31d-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb31d-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="eb31d-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="eb31d-133">Merhaba arama kutusuna yazın **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="eb31d-135">Merhaba Sonuçlar panelinde seçin **Velpic SAML**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="eb31d-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb31d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="eb31d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb31d-138">Bu bölümde, yapılandırmanız ve Velpic SAML ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="eb31d-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb31d-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Velpic SAML içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="eb31d-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Velpic SAML hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="eb31d-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Velpic SAML içinde.</span><span class="sxs-lookup"><span data-stu-id="eb31d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="eb31d-142">tooconfigure ve Velpic SAML ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb31d-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb31d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="eb31d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb31d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="eb31d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb31d-145">**[Velpic SAML test kullanıcısı oluşturma](#creating-a-velpic-saml-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir Velpic SAML içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="eb31d-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="eb31d-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eb31d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb31d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="eb31d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb31d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eb31d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb31d-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Velpic SAML uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="eb31d-150">**tooconfigure Azure AD çoklu oturum açma Velpic SAML ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb31d-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb31d-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **Velpic SAML** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="eb31d-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eb31d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="eb31d-155">Hello Hello ayrıntılarını girin **Velpic SAML etki alanı ve URL'leri** bölüm -</span><span class="sxs-lookup"><span data-stu-id="eb31d-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="eb31d-157">a.</span><span class="sxs-lookup"><span data-stu-id="eb31d-157">a.</span></span> <span data-ttu-id="eb31d-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="eb31d-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="eb31d-159">b.</span><span class="sxs-lookup"><span data-stu-id="eb31d-159">b.</span></span> <span data-ttu-id="eb31d-160">Merhaba, **tanımlayıcısı** metin kutusuna, Yapıştır hello **'Çoklu oturum açma URL'si'** değeri`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="eb31d-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="eb31d-161">Lütfen başlangıç oturum açma URL'si hello Velpic SAML ekibi tarafından sağlanacak ve tanımlayıcı değeri Velpic SAML tarafında hello SSO eklentisi yapılandırırken kullanılabilecek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="eb31d-162">Velpic SAML uygulama sayfasından değer ve burada Yapıştır toocopy gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="eb31d-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="eb31d-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb31d-167">Hello Velpic SAML yapılandırma bölümü, oturum açma yapılandırma Velpic SAML tooopen yapılandırma penceresi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="eb31d-168">Merhaba SAML varlık kimliği hızlı başvuru bölümünde hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="eb31d-169">Farklı web tarayıcısı penceresinde Velpic SAML şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="eb31d-170">Tıklayın **Yönet** sekmesinde ve çok Git**tümleştirme** ihtiyaç duyacağınız tooclick üzerinde bölüm **eklentileri** düğmesini toocreate yeni eklenti için oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eb31d-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="eb31d-172">Tıklatın hello üzerinde **'Eklenti ekleme'** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="eb31d-174">Tıklatın hello üzerinde **SAML** döşeme hello eklentisi ekleyin sayfasında.</span><span class="sxs-lookup"><span data-stu-id="eb31d-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="eb31d-176">Merhaba yeni SAML eklentisini Hello adını girin ve hello tıklayın **'Ekle'** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="eb31d-178">Aşağıdaki gibi Hello ayrıntılarını girin:</span><span class="sxs-lookup"><span data-stu-id="eb31d-178">Enter hello details as follows:</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="eb31d-180">a.</span><span class="sxs-lookup"><span data-stu-id="eb31d-180">a.</span></span> <span data-ttu-id="eb31d-181">Merhaba, **adı** metin kutusuna, SAML eklentisini hello adını yazın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="eb31d-182">b.</span><span class="sxs-lookup"><span data-stu-id="eb31d-182">b.</span></span> <span data-ttu-id="eb31d-183">Merhaba, **veren URL'si** metin kutusuna, Yapıştır hello **SAML varlık kimliği** hello kopyalanan **yapılandırma oturum açma** hello Azure portalı penceresi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="eb31d-184">c.</span><span class="sxs-lookup"><span data-stu-id="eb31d-184">c.</span></span> <span data-ttu-id="eb31d-185">Merhaba, **sağlayıcısı meta verileri yapılandırma** hello Azure portalından indirdiğiniz meta veri XML dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="eb31d-186">d.</span><span class="sxs-lookup"><span data-stu-id="eb31d-186">d.</span></span> <span data-ttu-id="eb31d-187">Yalnızca zaman hello etkinleştirerek sağlama tooenable SAML seçebilirsiniz **'Otomatik oluştur yeni kullanıcılar'** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="eb31d-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="eb31d-188">Bir kullanıcı Velpic yok ve bu bayrak etkin değil, Azure hello oturum açma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="eb31d-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="eb31d-189">Merhaba bayrağı etkinleştirilmiş hello kullanıcı otomatik olarak ise Velpic oturum açma hello aynı anda sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="eb31d-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="eb31d-190">e.</span><span class="sxs-lookup"><span data-stu-id="eb31d-190">e.</span></span> <span data-ttu-id="eb31d-191">Kopya hello **tek oturum açma URL'si** içinde hello metin kutusu ve Yapıştır Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="eb31d-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="eb31d-192">f.</span><span class="sxs-lookup"><span data-stu-id="eb31d-192">f.</span></span> <span data-ttu-id="eb31d-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb31d-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb31d-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb31d-195">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="eb31d-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb31d-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb31d-198">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb31d-200">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb31d-202">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb31d-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb31d-204">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb31d-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb31d-206">a.</span><span class="sxs-lookup"><span data-stu-id="eb31d-206">a.</span></span> <span data-ttu-id="eb31d-207">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb31d-208">b.</span><span class="sxs-lookup"><span data-stu-id="eb31d-208">b.</span></span> <span data-ttu-id="eb31d-209">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="eb31d-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb31d-210">c.</span><span class="sxs-lookup"><span data-stu-id="eb31d-210">c.</span></span> <span data-ttu-id="eb31d-211">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb31d-212">d.</span><span class="sxs-lookup"><span data-stu-id="eb31d-212">d.</span></span> <span data-ttu-id="eb31d-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="eb31d-214">Velpic SAML test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb31d-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="eb31d-215">Bu adım yalnızca zaman sağlama kullanıcı Merhaba uygulaması desteklediği genellikle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="eb31d-216">Merhaba otomatik kullanıcı sağlamayı etkinleştirilmemişse, el ile kullanıcı oluşturma aşağıda açıklandığı gibi yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="eb31d-217">Velpic SAML şirket sitenizin yönetici olarak oturum açın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb31d-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="eb31d-218">Yönet sekmesini tıklatın ve tooUsers bölümüne gidin, sonra yeni düğmesi tooadd kullanıcılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![Kullanıcı Ekle](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="eb31d-220">Merhaba üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![Kullanıcı](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="eb31d-222">a.</span><span class="sxs-lookup"><span data-stu-id="eb31d-222">a.</span></span> <span data-ttu-id="eb31d-223">Merhaba, **ad** metin kutusuna, türü hello Britta Simon adı.</span><span class="sxs-lookup"><span data-stu-id="eb31d-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="eb31d-224">b.</span><span class="sxs-lookup"><span data-stu-id="eb31d-224">b.</span></span> <span data-ttu-id="eb31d-225">Merhaba, **Soyadı** metin kutusuna, tür hello son adını Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb31d-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="eb31d-226">c.</span><span class="sxs-lookup"><span data-stu-id="eb31d-226">c.</span></span> <span data-ttu-id="eb31d-227">Merhaba, **kullanıcı adı** metin kutusuna, Britta Simon türü hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="eb31d-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="eb31d-228">d.</span><span class="sxs-lookup"><span data-stu-id="eb31d-228">d.</span></span> <span data-ttu-id="eb31d-229">Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="eb31d-230">e.</span><span class="sxs-lookup"><span data-stu-id="eb31d-230">e.</span></span> <span data-ttu-id="eb31d-231">Merhaba bilgi geri kalanı, gerekirse doldurabilir isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="eb31d-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="eb31d-232">f.</span><span class="sxs-lookup"><span data-stu-id="eb31d-232">f.</span></span> <span data-ttu-id="eb31d-233">**KAYDET**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb31d-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb31d-234">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="eb31d-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb31d-235">Bu bölümde, kendi erişim tooVelpic SAML vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="eb31d-237">**tooassign Britta Simon tooVelpic SAML, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb31d-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb31d-238">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="eb31d-240">Merhaba uygulamalar listesinde **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="eb31d-242">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="eb31d-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="eb31d-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb31d-244">Click **Add** button.</span></span> <span data-ttu-id="eb31d-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb31d-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="eb31d-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="eb31d-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb31d-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb31d-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb31d-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb31d-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb31d-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="eb31d-250">Testing single sign-on</span></span>

<span data-ttu-id="eb31d-251">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="eb31d-252">Velpic SAML döşeme hello erişim paneli hello tıkladığınızda, oturum açma sayfasına Velpic SAML uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb31d-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="eb31d-253">Merhaba görmelisiniz **'Günlük oturum Azure AD'** hello oturum açma sayfası düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="eb31d-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="eb31d-255">Tıklatın hello üzerinde **'Günlük oturum Azure AD'** düğmesini toolog Azure AD hesabınızı kullanarak tooVelpic içinde.</span><span class="sxs-lookup"><span data-stu-id="eb31d-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="eb31d-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="eb31d-256">Additional resources</span></span>

* [<span data-ttu-id="eb31d-257">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="eb31d-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb31d-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="eb31d-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

