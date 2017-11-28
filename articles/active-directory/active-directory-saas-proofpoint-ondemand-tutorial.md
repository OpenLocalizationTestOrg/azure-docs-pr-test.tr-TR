---
title: "Öğretici: Azure Active Directory Tümleştirme ile isteğe bağlı Proofpoint | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve isteğe bağlı Proofpoint arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="b5ed0-103">Öğretici: Azure Active Directory Tümleştirme ile Proofpoint isteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="b5ed0-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="b5ed0-104">Bu öğreticide, bilgi nasıl toointegrate Proofpoint Azure Active Directory (Azure AD) ile isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5ed0-105">İsteğe bağlı Proofpoint Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5ed0-106">İsteğe bağlı erişim tooProofpoint olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b5ed0-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="b5ed0-107">Kullanıcıların tooautomatically get açan tooProofpoint (çoklu oturum açma) isteğe bağlı Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b5ed0-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5ed0-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b5ed0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b5ed0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5ed0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5ed0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b5ed0-110">Prerequisites</span></span>

<span data-ttu-id="b5ed0-111">tooconfigure Azure AD tümleştirme isteğe bağlı Proofpoint ile aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="b5ed0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b5ed0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5ed0-113">İsteğe bağlı çoklu oturum açma etkin abonelik üzerinde Proofpoint</span><span class="sxs-lookup"><span data-stu-id="b5ed0-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5ed0-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5ed0-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5ed0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5ed0-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5ed0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5ed0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b5ed0-118">Scenario description</span></span>
<span data-ttu-id="b5ed0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5ed0-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5ed0-121">Proofpoint isteğe bağlı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="b5ed0-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="b5ed0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b5ed0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="b5ed0-123">Proofpoint isteğe bağlı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="b5ed0-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="b5ed0-124">Azure AD'ye tooconfigure hello tümleştirme Proofpoint isteğe bağlı olarak tooadd Proofpoint isteğe bağlı hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5ed0-125">**tooadd Proofpoint hello galerisinden istendiğinde hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5ed0-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5ed0-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5ed0-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5ed0-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b5ed0-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b5ed0-133">Merhaba arama kutusuna yazın **Proofpoint isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="b5ed0-135">Merhaba Sonuçlar panelinde seçin **isteğe bağlı Proofpoint**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5ed0-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b5ed0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5ed0-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı isteğe bağlı Proofpoint ile test etme</span><span class="sxs-lookup"><span data-stu-id="b5ed0-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b5ed0-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Proofpoint isteğe bağlı olarak tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="b5ed0-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve isteğe bağlı Proofpoint hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="b5ed0-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Proofpoint isteğe bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="b5ed0-142">tooconfigure ve test Azure AD çoklu oturum açma isteğe bağlı Proofpoint ile yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5ed0-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5ed0-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5ed0-145">**[Bir Proofpoint üzerinde isteğe bağlı test kullanıcısı oluşturma](#creating-a-proofpoint-on-demand-test-user)**  -toohave Britta Simon Proofpoint kullanıcı bağlantılı toohello Azure AD gösterimidir isteğe bağlı olarak, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5ed0-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5ed0-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5ed0-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b5ed0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5ed0-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Proofpoint isteğe bağlı uygulama üzerinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="b5ed0-150">**tooconfigure Azure AD çoklu oturum açma ile isteğe bağlı olarak, Proofpoint hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5ed0-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5ed0-151">Hello hello üzerinde Azure portal'ın **Proofpoint isteğe bağlı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b5ed0-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="b5ed0-155">Merhaba üzerinde **Proofpoint isteğe bağlı etki alanı ve URL'ler hakkında** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="b5ed0-157">a.In hello **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="b5ed0-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="b5ed0-158">b.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-158">b.</span></span> <span data-ttu-id="b5ed0-159">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="b5ed0-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="b5ed0-160">c.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-160">c.</span></span>  <span data-ttu-id="b5ed0-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="b5ed0-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b5ed0-162">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-162">These values are not hello real.</span></span> <span data-ttu-id="b5ed0-163">Bu güncelleştirme tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b5ed0-164">Kişi [isteğe bağlı müşteri destek ekibi üzerinde Proofpoint](https://www.proofpoint.com/us/support-services) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="b5ed0-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="b5ed0-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b5ed0-169">Merhaba üzerinde **isteğe bağlı yapılandırma Proofpoint** 'yi tıklatın **isteğe bağlı yapılandırma Proofpoint** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b5ed0-170">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b5ed0-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="b5ed0-172">tooconfigure çoklu oturum açma üzerinde **isteğe bağlı Proofpoint** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)**,**SAML varlık kimliği**, ve **SAML Çoklu oturum açma hizmet URL'si** çok[Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="b5ed0-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="b5ed0-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b5ed0-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5ed0-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5ed0-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5ed0-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5ed0-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ed0-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5ed0-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b5ed0-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5ed0-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5ed0-180">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5ed0-182">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-182">These values are not hello real.</span></span> <span data-ttu-id="b5ed0-183">Bu değerleri hello gerçek ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b5ed0-183">Update these values with hello actual</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5ed0-185">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5ed0-187">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5ed0-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5ed0-189">a.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-189">a.</span></span> <span data-ttu-id="b5ed0-190">Merhaba, **adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b5ed0-191">b.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-191">b.</span></span> <span data-ttu-id="b5ed0-192">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b5ed0-193">c.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-193">c.</span></span> <span data-ttu-id="b5ed0-194">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b5ed0-195">d.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-195">d.</span></span> <span data-ttu-id="b5ed0-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="b5ed0-197">Bir Proofpoint üzerinde isteğe bağlı test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ed0-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="b5ed0-198">Bu bölümde, Britta Simon Proofpoint isteğe bağlı olarak adlandırılan bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="b5ed0-199">Çalışmak [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services) hello Proofpoint isteğe bağlı bir platformda tooadd kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5ed0-200">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b5ed0-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5ed0-201">Bu bölümde, isteğe bağlı erişim tooProofpoint vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b5ed0-203">**tooassign Britta Simon tooProofpoint isteğe bağlı olarak, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5ed0-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5ed0-204">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b5ed0-206">Merhaba uygulamalar listesinde **Proofpoint isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="b5ed0-208">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b5ed0-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-210">Click **Add** button.</span></span> <span data-ttu-id="b5ed0-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b5ed0-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5ed0-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5ed0-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5ed0-216">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b5ed0-216">Testing single sign-on</span></span>

<span data-ttu-id="b5ed0-217">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b5ed0-218">Merhaba tıkladığınızda **Proofpoint isteğe bağlı** döşeme erişim paneli hello üzerinde isteğe bağlı uygulama üzerinde tooyour Proofpoint üzerinde otomatik olarak imzalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b5ed0-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="b5ed0-219">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5ed0-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="b5ed0-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b5ed0-220">Additional resources</span></span>

* [<span data-ttu-id="b5ed0-221">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b5ed0-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5ed0-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b5ed0-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

