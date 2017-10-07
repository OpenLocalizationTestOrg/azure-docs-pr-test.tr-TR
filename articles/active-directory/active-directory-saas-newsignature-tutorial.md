---
title: "Öğretici: Microsoft Azure için bulut Yönetim Portalı Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Microsoft Azure için bulut Yönetim Portalı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="b1a70-103">Öğretici: Microsoft Azure için bulut Yönetim Portalı Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="b1a70-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="b1a70-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile Microsoft Azure için bulut Yönetim Portalı.</span><span class="sxs-lookup"><span data-stu-id="b1a70-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1a70-105">Microsoft Azure için bulut Yönetim Portalı Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b1a70-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1a70-106">Erişim tooCloud Microsoft Azure Yönetim Portalı sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b1a70-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="b1a70-107">Kullanıcıların tooautomatically get açan tooCloud (çoklu oturum açma) Microsoft Azure Yönetim Portalı ile Azure AD hesaplarına etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b1a70-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1a70-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b1a70-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b1a70-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1a70-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1a70-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b1a70-110">Prerequisites</span></span>

<span data-ttu-id="b1a70-111">Microsoft Azure için bulut Yönetim Portalı ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1a70-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="b1a70-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b1a70-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1a70-113">Microsoft Azure çoklu oturum açma etkin abonelik için bir bulut Yönetim Portalı</span><span class="sxs-lookup"><span data-stu-id="b1a70-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1a70-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b1a70-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1a70-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1a70-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1a70-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b1a70-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1a70-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1a70-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1a70-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b1a70-118">Scenario description</span></span>
<span data-ttu-id="b1a70-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b1a70-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1a70-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b1a70-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1a70-121">Microsoft Azure için bulut Yönetim Portalı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="b1a70-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="b1a70-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b1a70-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="b1a70-123">Microsoft Azure için bulut Yönetim Portalı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="b1a70-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="b1a70-124">Azure AD'ye tooconfigure hello tümleştirme bulut Microsoft Azure Yönetim Portalı'nın tooadd bulut Yönetim Portalı hello galeri tooyour listesinden yönetilen SaaS uygulamaları için Microsoft Azure gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a70-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1a70-125">**tooadd hello Galerisi'nden Microsoft Azure için bulut Yönetim Portalı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a70-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a70-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1a70-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1a70-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b1a70-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b1a70-133">Merhaba arama kutusuna yazın **Microsoft Azure için bulut Yönetim Portalı**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="b1a70-135">Merhaba Sonuçlar panelinde seçin **Microsoft Azure için bulut Yönetim Portalı**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b1a70-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1a70-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b1a70-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1a70-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcıyı temel alarak Microsoft Azure için bulut Yönetim Portalı ile test etme.</span><span class="sxs-lookup"><span data-stu-id="b1a70-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1a70-139">Tek toowork'ın oturum açma hangi hello karşılık gelen bulut Microsoft Azure Yönetim Portalı'nda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a70-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="b1a70-140">Diğer bir deyişle, bir Azure AD kullanıcı ve Microsoft Azure için bulut Yönetim Portalı'nda hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a70-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="b1a70-141">Microsoft Azure için bulut Yönetim Portalı'nda hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b1a70-142">tooconfigure ve test Azure AD çoklu oturum açma bulut Yönetim Portalı ile Microsoft Azure, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1a70-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1a70-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b1a70-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1a70-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b1a70-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1a70-145">**[Microsoft Azure test kullanıcısı için bir bulut Yönetim Portalı oluşturma](#creating-a-cloud-management-portal-for-microsoft-azure-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Microsoft Azure için bulut Yönetim Portalı'nda, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="b1a70-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1a70-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b1a70-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1a70-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b1a70-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1a70-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b1a70-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1a70-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve bulut yönetim portalınızdaki Microsoft Azure uygulama için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b1a70-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="b1a70-150">**Microsoft Azure için bulut Yönetim Portalı ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a70-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a70-151">Merhaba hello üzerinde Azure portal'ın **Microsoft Azure için bulut Yönetim Portalı** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b1a70-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b1a70-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="b1a70-155">Merhaba üzerinde **bulut Microsoft Azure etki alanı ve URL'ler için Yönetim Portalı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a70-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="b1a70-157">a.</span><span class="sxs-lookup"><span data-stu-id="b1a70-157">a.</span></span> <span data-ttu-id="b1a70-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="b1a70-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="b1a70-159">b.</span><span class="sxs-lookup"><span data-stu-id="b1a70-159">b.</span></span> <span data-ttu-id="b1a70-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="b1a70-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="b1a70-161">c.</span><span class="sxs-lookup"><span data-stu-id="b1a70-161">c.</span></span> <span data-ttu-id="b1a70-162">Merhaba, **yanıt URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="b1a70-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="b1a70-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b1a70-163">These values are not real.</span></span> <span data-ttu-id="b1a70-164">Bu değerleri hello gerçek oturum açma URL'si, tanımlayıcı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b1a70-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="b1a70-165">Kişi [bulut Microsoft Azure istemci destek ekibi için Yönetim Portalı](mailto:jczernuszka@newsignature.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="b1a70-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="b1a70-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b1a70-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="b1a70-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1a70-170">Merhaba üzerinde **bulut Microsoft Azure yapılandırma için Yönetim Portalı** 'yi tıklatın **Microsoft Azure için bulut Yönetim Portalı yapılandırma** tooopen **oturum açmaYapılandırma**penceresi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b1a70-171">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b1a70-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="b1a70-173">tooconfigure çoklu oturum açma üzerinde **Microsoft Azure için bulut Yönetim Portalı** yan, indirilen toosend hello ihtiyacınız **sertifika**, **Sign-Out URL**, **SAML çoklu oturum açma hizmet URL'si** ve **SAML varlık kimliği** çok[bulut Microsoft Azure destek ekibi için Yönetim Portalı](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="b1a70-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="b1a70-174">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b1a70-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b1a70-175">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b1a70-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b1a70-176">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b1a70-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b1a70-177">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1a70-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1a70-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1a70-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1a70-179">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b1a70-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b1a70-181">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a70-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a70-182">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1a70-184">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1a70-186">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a70-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1a70-188">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a70-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1a70-190">a.</span><span class="sxs-lookup"><span data-stu-id="b1a70-190">a.</span></span> <span data-ttu-id="b1a70-191">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1a70-192">b.</span><span class="sxs-lookup"><span data-stu-id="b1a70-192">b.</span></span> <span data-ttu-id="b1a70-193">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b1a70-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1a70-194">c.</span><span class="sxs-lookup"><span data-stu-id="b1a70-194">c.</span></span> <span data-ttu-id="b1a70-195">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1a70-196">d.</span><span class="sxs-lookup"><span data-stu-id="b1a70-196">d.</span></span> <span data-ttu-id="b1a70-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1a70-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="b1a70-198">Microsoft Azure test kullanıcısı için bir bulut Yönetim Portalı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1a70-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="b1a70-199">Bu bölümde Hello amacı toocreate Britta Simon Microsoft Azure için bulut Yönetim Portalı'nda adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="b1a70-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="b1a70-200">Lütfen çalışmak [bulut Microsoft Azure destek ekibi için Yönetim Portalı](mailto:jczernuszka@newsignature.com) tooadd hello kullanıcılar Microsoft Azure hesabı için hello bulut Yönetim Portalı.</span><span class="sxs-lookup"><span data-stu-id="b1a70-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1a70-201">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b1a70-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1a70-202">Bu bölümde, erişim tooCloud Microsoft Azure Yönetim Portalı vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b1a70-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b1a70-204">**tooassign Britta Simon tooCloud Microsoft Azure Yönetim Portalı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a70-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a70-205">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b1a70-207">Merhaba uygulamalar listesinde **Microsoft Azure için bulut Yönetim Portalı**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="b1a70-209">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b1a70-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b1a70-211">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b1a70-211">Click **Add** button.</span></span> <span data-ttu-id="b1a70-212">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a70-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b1a70-214">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b1a70-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1a70-215">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a70-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1a70-216">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a70-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1a70-217">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b1a70-217">Testing single sign-on</span></span>

<span data-ttu-id="b1a70-218">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b1a70-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="b1a70-219">Merhaba bulut Yönetim Portalı hello erişim paneli Microsoft Azure parçasında tıkladığınızda, Microsoft Azure uygulaması için otomatik olarak imzalanmış üzerinde bulut Yönetim Portalı tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a70-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="b1a70-220">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1a70-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1a70-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b1a70-221">Additional resources</span></span>

* [<span data-ttu-id="b1a70-222">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b1a70-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1a70-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b1a70-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

