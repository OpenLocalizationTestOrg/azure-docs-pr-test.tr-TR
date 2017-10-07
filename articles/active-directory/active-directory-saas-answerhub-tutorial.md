---
title: "Öğretici: Azure Active Directory Tümleştirme ile AnswerHub | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile AnswerHub arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="3c712-103">Öğretici: Azure Active Directory Tümleştirme AnswerHub ile</span><span class="sxs-lookup"><span data-stu-id="3c712-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="3c712-104">Bu öğreticide, bilgi nasıl toointegrate AnswerHub Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3c712-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c712-105">AnswerHub Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3c712-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3c712-106">Erişim tooAnswerHub sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3c712-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="3c712-107">Kullanıcıların tooautomatically get açan tooAnswerHub (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3c712-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c712-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3c712-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3c712-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c712-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c712-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3c712-110">Prerequisites</span></span>

<span data-ttu-id="3c712-111">tooconfigure AnswerHub ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c712-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="3c712-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3c712-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c712-113">Bir AnswerHub çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="3c712-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c712-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3c712-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c712-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c712-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c712-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3c712-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c712-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c712-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c712-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3c712-118">Scenario description</span></span>
<span data-ttu-id="3c712-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3c712-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c712-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3c712-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c712-121">Merhaba Galerisi'nden AnswerHub ekleme</span><span class="sxs-lookup"><span data-stu-id="3c712-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="3c712-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3c712-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="3c712-123">Merhaba Galerisi'nden AnswerHub ekleme</span><span class="sxs-lookup"><span data-stu-id="3c712-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="3c712-124">Azure AD'ye tooconfigure hello tümleştirme AnswerHub, tooadd AnswerHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c712-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3c712-125">**tooadd AnswerHub hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c712-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c712-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c712-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3c712-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3c712-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3c712-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3c712-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3c712-133">Merhaba arama kutusuna yazın **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="3c712-133">In hello search box, type **AnswerHub**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="3c712-135">Merhaba Sonuçlar panelinde seçin **AnswerHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3c712-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c712-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3c712-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c712-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı AnswerHub sınayın.</span><span class="sxs-lookup"><span data-stu-id="3c712-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3c712-139">Tek toowork'ın oturum açma hangi hello karşılık gelen AnswerHub içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c712-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="3c712-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı AnswerHub hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c712-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="3c712-141">Merhaba hello değeri AnswerHub içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="3c712-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3c712-142">tooconfigure ve AnswerHub ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c712-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3c712-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="3c712-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3c712-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="3c712-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c712-145">**[Bir AnswerHub test kullanıcısı oluşturma](#creating-an-answerhub-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir AnswerHub içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="3c712-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c712-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3c712-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c712-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="3c712-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c712-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3c712-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c712-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma AnswerHub uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3c712-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="3c712-150">**tooconfigure Azure AD çoklu oturum açma ile AnswerHub, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c712-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c712-151">Hello hello üzerinde Azure portal'ın **AnswerHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3c712-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3c712-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3c712-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="3c712-155">Merhaba üzerinde **AnswerHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3c712-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="3c712-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c712-157">a.</span></span> <span data-ttu-id="3c712-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="3c712-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="3c712-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c712-159">b.</span></span> <span data-ttu-id="3c712-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="3c712-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c712-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="3c712-161">These values are not real.</span></span> <span data-ttu-id="3c712-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3c712-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3c712-163">Kişi [AnswerHub istemci destek ekibi](mailto:success@answerhub.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="3c712-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="3c712-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3c712-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="3c712-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3c712-168">Merhaba üzerinde **AnswerHub yapılandırma** 'yi tıklatın **yapılandırma AnswerHub** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3c712-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3c712-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="3c712-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="3c712-171">Farklı web tarayıcısı penceresinde AnswerHub şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3c712-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="3c712-172">AnswerHub yapılandırmada yardıma gereksinim duyarsanız başvurun [AnswerHub'in destek ekibi](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="3c712-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="3c712-173">Çok Git**Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="3c712-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="3c712-174">Merhaba tıklatın **kullanıcı ve grup** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="3c712-175">Merhaba Gezinti bölmesindeki hello tarafı, sol hello **sosyal ayarları** 'yi tıklatın **SAML Kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="3c712-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="3c712-176">Tıklatın **IDP Config** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="3c712-177">Merhaba üzerinde **IDP Config** sekmesinde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3c712-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="3c712-178">![SAML Kurulumu](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="3c712-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="3c712-179">a.</span><span class="sxs-lookup"><span data-stu-id="3c712-179">a.</span></span> <span data-ttu-id="3c712-180">İçinde **IDP oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="3c712-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="3c712-181">b.</span><span class="sxs-lookup"><span data-stu-id="3c712-181">b.</span></span> <span data-ttu-id="3c712-182">İçinde **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri.</span><span class="sxs-lookup"><span data-stu-id="3c712-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="3c712-183">c.</span><span class="sxs-lookup"><span data-stu-id="3c712-183">c.</span></span> <span data-ttu-id="3c712-184">İçinde **IDP ad tanımlayıcısı biçimi** metin kutusuna, hello kullanıcı tanımlayıcısı olarak seçili Azure Portalı'nda aynı değeri girin **kullanıcı öznitelikleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="3c712-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="3c712-185">d.</span><span class="sxs-lookup"><span data-stu-id="3c712-185">d.</span></span> <span data-ttu-id="3c712-186">Tıklatın **anahtarlar ve Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="3c712-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="3c712-187">Merhaba anahtarlar ve sertifikalar sekmesinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3c712-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="3c712-188">![Anahtarlar ve Sertifikalar](./media/active-directory-saas-answerhub-tutorial/ic785173.png "anahtarlar ve sertifikalar")</span><span class="sxs-lookup"><span data-stu-id="3c712-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="3c712-189">a.</span><span class="sxs-lookup"><span data-stu-id="3c712-189">a.</span></span> <span data-ttu-id="3c712-190">Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure Portalı'ndan indirilen, base-64 kodlanmış sertifika açın ve ardından toohello yapıştırın **IDP ortak anahtarı (x 509 biçimi)** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3c712-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="3c712-191">b.</span><span class="sxs-lookup"><span data-stu-id="3c712-191">b.</span></span> <span data-ttu-id="3c712-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3c712-192">Click **Save**.</span></span>

14. <span data-ttu-id="3c712-193">Merhaba üzerinde **IDP Config** sekmesini tıklatın, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3c712-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3c712-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3c712-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3c712-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="3c712-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3c712-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c712-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c712-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c712-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c712-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="3c712-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3c712-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c712-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c712-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c712-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3c712-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c712-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c712-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c712-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3c712-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c712-209">a.</span><span class="sxs-lookup"><span data-stu-id="3c712-209">a.</span></span> <span data-ttu-id="3c712-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c712-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c712-211">b.</span><span class="sxs-lookup"><span data-stu-id="3c712-211">b.</span></span> <span data-ttu-id="3c712-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3c712-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c712-213">c.</span><span class="sxs-lookup"><span data-stu-id="3c712-213">c.</span></span> <span data-ttu-id="3c712-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3c712-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3c712-215">d.</span><span class="sxs-lookup"><span data-stu-id="3c712-215">d.</span></span> <span data-ttu-id="3c712-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3c712-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="3c712-217">Bir AnswerHub test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c712-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="3c712-218">tooenable Azure AD kullanıcıların toolog tooAnswerHub bunların AnswerHub sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c712-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="3c712-219">AnswerHub Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="3c712-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="3c712-220">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c712-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c712-221">İçinde tooyour oturum **AnswerHub** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="3c712-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="3c712-222">Çok Git**Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="3c712-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="3c712-223">Merhaba tıklatın **kullanıcıları ve grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="3c712-224">Merhaba Gezinti bölmesindeki hello tarafı, sol hello **kullanıcıları yönetme** 'yi tıklatın **oluşturma veya içeri aktarma kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="3c712-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="3c712-225">![Kullanıcıları ve grupları](./media/active-directory-saas-answerhub-tutorial/ic785175.png "kullanıcıları ve grupları")</span><span class="sxs-lookup"><span data-stu-id="3c712-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="3c712-226">Türü hello **e-posta adresi**, **kullanıcıadı** ve **parola** geçerli bir Azure hello tooprovision istediğiniz Active Directory hesabı ilgili metin kutularına ve 'ıtıklatın **Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="3c712-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="3c712-227">API AAD kullanıcı hesaplarının AnswerHub tooprovision tarafından sağlanan veya herhangi diğer AnswerHub kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c712-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3c712-228">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3c712-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3c712-229">Bu bölümde, erişim tooAnswerHub vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3c712-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3c712-231">**tooassign Britta Simon tooAnswerHub hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3c712-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c712-232">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3c712-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3c712-234">Merhaba uygulamalar listesinde **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="3c712-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="3c712-236">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3c712-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3c712-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c712-238">Click **Add** button.</span></span> <span data-ttu-id="3c712-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c712-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3c712-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3c712-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3c712-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c712-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c712-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3c712-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c712-244">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3c712-244">Testing single sign-on</span></span>

<span data-ttu-id="3c712-245">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="3c712-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3c712-246">Merhaba AnswerHub hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour AnswerHub uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c712-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="3c712-247">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c712-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c712-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3c712-248">Additional resources</span></span>

* [<span data-ttu-id="3c712-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3c712-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c712-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3c712-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

