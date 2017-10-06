---
title: "Öğretici: Azure Active Directory Tümleştirme SensoScientific kablosuz sıcaklık izleme sistemi | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SensoScientific kablosuz sıcaklık izleme sistemi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="85e09-103">Öğretici: Azure Active Directory Tümleştirme ile SensoScientific kablosuz sıcaklık sistem izleme</span><span class="sxs-lookup"><span data-stu-id="85e09-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="85e09-104">Bu öğreticide, bilgi nasıl toointegrate SensoScientific kablosuz sıcaklık izleme sistemi Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85e09-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85e09-105">SensoScientific kablosuz sıcaklık sistem izleme Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="85e09-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85e09-106">Erişim tooSensoScientific kablosuz sıcaklık sistem izleme sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="85e09-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="85e09-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooSensoScientific kablosuz sıcaklık sistem izleme (çoklu oturum açma) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="85e09-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85e09-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="85e09-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="85e09-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85e09-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85e09-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85e09-110">Prerequisites</span></span>

<span data-ttu-id="85e09-111">tooconfigure SensoScientific kablosuz sıcaklık izleme sistemi ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="85e09-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="85e09-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="85e09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85e09-113">Bir SensoScientific kablosuz sıcaklık sistem izleme çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="85e09-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85e09-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="85e09-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85e09-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="85e09-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85e09-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="85e09-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85e09-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85e09-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85e09-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="85e09-118">Scenario description</span></span>
<span data-ttu-id="85e09-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="85e09-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85e09-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="85e09-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85e09-121">Merhaba Galerisi'nden SensoScientific kablosuz sıcaklık sistem izleme ekleme</span><span class="sxs-lookup"><span data-stu-id="85e09-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="85e09-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="85e09-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="85e09-123">Merhaba Galerisi'nden SensoScientific kablosuz sıcaklık sistem izleme ekleme</span><span class="sxs-lookup"><span data-stu-id="85e09-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="85e09-124">Azure AD'ye tooconfigure hello tümleştirme SensoScientific kablosuz Sıcaklık İzleme sisteminin tooadd SensoScientific kablosuz sıcaklık sistem izleme hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="85e09-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85e09-125">**tooadd SensoScientific kablosuz sıcaklık izleme sistemi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85e09-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85e09-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="85e09-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85e09-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="85e09-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85e09-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="85e09-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="85e09-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85e09-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="85e09-133">Merhaba arama kutusuna yazın **SensoScientific kablosuz sıcaklık sistem izleme**.</span><span class="sxs-lookup"><span data-stu-id="85e09-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="85e09-135">Merhaba Sonuçlar panelinde seçin **SensoScientific kablosuz sıcaklık sistem izleme**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="85e09-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85e09-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="85e09-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85e09-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SensoScientific kablosuz Sıcaklık "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı sistem izleme ile test etme</span><span class="sxs-lookup"><span data-stu-id="85e09-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="85e09-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SensoScientific kablosuz Sıcaklık İzleme sisteminde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="85e09-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="85e09-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve izleme SensoScientific kablosuz sıcaklık sistemindeki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="85e09-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="85e09-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SensoScientific kablosuz Sıcaklık İzleme sistem.</span><span class="sxs-lookup"><span data-stu-id="85e09-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="85e09-142">tooconfigure ve SensoScientific kablosuz sıcaklık sistem izleme ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="85e09-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85e09-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="85e09-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85e09-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="85e09-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85e09-145">**[SensoScientific kablosuz sıcaklık sistem izleme test kullanıcısı oluşturma](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave Britta Simon SensoScientific kablosuz sıcaklık izleme sistemi içinde karşılık gelen bağlı toohello Azure AD gösterimi Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="85e09-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="85e09-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="85e09-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85e09-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="85e09-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85e09-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="85e09-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85e09-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SensoScientific kablosuz sıcaklık sistem izleme uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="85e09-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="85e09-150">**Azure AD çoklu oturum açma tooconfigure SensoScientific kablosuz sıcaklık sistemi, izleme hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85e09-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="85e09-151">Merhaba hello üzerinde Azure portal'ın **SensoScientific kablosuz sıcaklık sistem izleme** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="85e09-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="85e09-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="85e09-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="85e09-155">Merhaba üzerinde **SensoScientific kablosuz sıcaklık sistem etki alanı izleme ve URL'leri** bölümünde, herhangi bir adım hello uygulaması olarak zaten önceden tümleştirilmiştir Azure ile hiçbir gerek tooperform:</span><span class="sxs-lookup"><span data-stu-id="85e09-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="85e09-157">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="85e09-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="85e09-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85e09-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="85e09-161">Merhaba üzerinde **SensoScientific kablosuz Sıcaklık İzleme Sistem Yapılandırması** 'yi tıklatın **SensoScientific kablosuz Sıcaklık İzleme sistem yapılandırma** tooopen  **Oturum açma özelliğini yapılandırın** penceresi.</span><span class="sxs-lookup"><span data-stu-id="85e09-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="85e09-162">Kopya hello **Sign-Out URL, SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="85e09-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="85e09-164">Üzerinde tooyour SensoScientific kablosuz sıcaklık sistem izleme uygulama yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="85e09-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="85e09-165">Merhaba Gezinti menüsünde hello üstte tıklatın **yapılandırma** ve Git **yapılandırma** altında **çoklu oturum açma** tooopen hello tek oturum açma ayarları.</span><span class="sxs-lookup"><span data-stu-id="85e09-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="85e09-167">İçinde **tek oturum açma ayarları** form hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85e09-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="85e09-168">a.</span><span class="sxs-lookup"><span data-stu-id="85e09-168">a.</span></span> <span data-ttu-id="85e09-169">Seçin **verenin adı** Azure AD olarak.</span><span class="sxs-lookup"><span data-stu-id="85e09-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="85e09-170">b.</span><span class="sxs-lookup"><span data-stu-id="85e09-170">b.</span></span> <span data-ttu-id="85e09-171">Yapıştır hello **SAML varlık kimliği** veren URL'si metin kutusuna Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="85e09-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="85e09-172">c.</span><span class="sxs-lookup"><span data-stu-id="85e09-172">c.</span></span> <span data-ttu-id="85e09-173">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** çoklu oturum açma hizmet URL'si metin kutusuna Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="85e09-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="85e09-174">d.</span><span class="sxs-lookup"><span data-stu-id="85e09-174">d.</span></span> <span data-ttu-id="85e09-175">Yapıştır hello **Sign-Out URL** tek Sign-Out hizmeti URL'si metin kutusuna Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="85e09-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="85e09-176">e.</span><span class="sxs-lookup"><span data-stu-id="85e09-176">e.</span></span> <span data-ttu-id="85e09-177">Azure portalından indirdiğiniz ve burada karşıya hello sertifika göz atın.</span><span class="sxs-lookup"><span data-stu-id="85e09-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="85e09-178">f.</span><span class="sxs-lookup"><span data-stu-id="85e09-178">f.</span></span> <span data-ttu-id="85e09-179">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85e09-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="85e09-180">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="85e09-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85e09-181">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="85e09-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85e09-182">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85e09-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85e09-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="85e09-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="85e09-184">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="85e09-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="85e09-186">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85e09-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85e09-187">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="85e09-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85e09-189">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="85e09-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85e09-191">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="85e09-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85e09-193">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85e09-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85e09-195">a.</span><span class="sxs-lookup"><span data-stu-id="85e09-195">a.</span></span> <span data-ttu-id="85e09-196">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85e09-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85e09-197">b.</span><span class="sxs-lookup"><span data-stu-id="85e09-197">b.</span></span> <span data-ttu-id="85e09-198">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="85e09-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85e09-199">c.</span><span class="sxs-lookup"><span data-stu-id="85e09-199">c.</span></span> <span data-ttu-id="85e09-200">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="85e09-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="85e09-201">d.</span><span class="sxs-lookup"><span data-stu-id="85e09-201">d.</span></span> <span data-ttu-id="85e09-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85e09-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="85e09-203">SensoScientific kablosuz sıcaklık sistem izleme test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="85e09-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="85e09-204">tooenable Azure AD kullanıcıların toolog tooSensoScientific kablosuz sıcaklık izleme sistemi, bunlar SensoScientific kablosuz sıcaklık izleme sistemine sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85e09-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="85e09-205">Çalışmak [SensoScientific kablosuz sıcaklık sistem izleme destek ekibi](https://www.sensoscientific.com/contact-us/) hello SensoScientific kablosuz sıcaklık sistem izleme platformunda hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="85e09-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="85e09-206">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="85e09-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="85e09-207">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="85e09-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="85e09-208">Bu bölümde, erişim tooSensoScientific kablosuz sıcaklık sistem izleme vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="85e09-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="85e09-210">**tooassign Britta Simon tooSensoScientific izleme kablosuz sıcaklık sistem hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85e09-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="85e09-211">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="85e09-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="85e09-213">Merhaba uygulamalar listesinde **SensoScientific kablosuz sıcaklık sistem izleme**.</span><span class="sxs-lookup"><span data-stu-id="85e09-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="85e09-215">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="85e09-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="85e09-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85e09-217">Click **Add** button.</span></span> <span data-ttu-id="85e09-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85e09-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="85e09-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="85e09-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85e09-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85e09-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85e09-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85e09-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85e09-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="85e09-223">Testing single sign-on</span></span>

<span data-ttu-id="85e09-224">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="85e09-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="85e09-225">Merhaba SensoScientific kablosuz sıcaklık sistem izleme kutucuğa tıklayın hello erişim paneli, otomatik olarak oturum açma tooyour SensoScientific kablosuz sıcaklık sistem izleme uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="85e09-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="85e09-226">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="85e09-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85e09-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="85e09-227">Additional resources</span></span>

* [<span data-ttu-id="85e09-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="85e09-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85e09-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="85e09-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

