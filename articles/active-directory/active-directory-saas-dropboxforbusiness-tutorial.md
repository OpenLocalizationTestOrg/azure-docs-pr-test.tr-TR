---
title: "Öğretici: İş için Dropbox Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve iş için Dropbox arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="6f1dc-103">Öğretici: İş için Dropbox Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="6f1dc-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="6f1dc-104">Bu öğreticide, bilgi nasıl toointegrate Dropbox iş ile Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f1dc-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f1dc-105">Dropbox iş için Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f1dc-106">İş için erişim tooDropbox olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6f1dc-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="6f1dc-107">Azure AD hesaplarına (çoklu oturum açma) iş için oturum açma, kullanıcıların tooautomatically get tooDropbox etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6f1dc-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f1dc-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6f1dc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6f1dc-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f1dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f1dc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6f1dc-110">Prerequisites</span></span>

<span data-ttu-id="6f1dc-111">İş için Dropbox ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="6f1dc-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6f1dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f1dc-113">Bir Dropbox iş çoklu oturum açma için abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6f1dc-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f1dc-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f1dc-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f1dc-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f1dc-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f1dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f1dc-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6f1dc-118">Scenario description</span></span>
<span data-ttu-id="6f1dc-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f1dc-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f1dc-121">İş için Dropbox hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="6f1dc-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="6f1dc-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f1dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="6f1dc-123">İş için Dropbox hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="6f1dc-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="6f1dc-124">Azure AD içinde iş için Dropbox tooconfigure hello tümleştirilmesi, tooadd Dropbox hello galeri tooyour listesinden yönetilen SaaS uygulamaları için iş gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f1dc-125">**tooadd hello galerisinden, iş için Dropbox hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f1dc-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f1dc-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f1dc-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f1dc-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6f1dc-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6f1dc-133">Merhaba arama kutusuna yazın **iş için Dropbox**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="6f1dc-135">Merhaba Sonuçlar panelinde seçin **iş için Dropbox**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f1dc-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f1dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f1dc-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı iş için Dropbox ile test etme</span><span class="sxs-lookup"><span data-stu-id="6f1dc-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6f1dc-139">Tek toowork'ın oturum açma hangi hello karşılık gelen iş için Dropbox'ın tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="6f1dc-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve kurumsal Dropbox hello ilgili kullanıcı arasında bir bağlantı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="6f1dc-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** iş için Dropbox içinde.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="6f1dc-142">tooconfigure ve Azure AD çoklu oturum açma ile test Dropbox iş için yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f1dc-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f1dc-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f1dc-145">**[Bir Dropbox iş test kullanıcısı için oluşturma](#creating-a-dropbox-for-business-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir iş için Dropbox'ın, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f1dc-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f1dc-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f1dc-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6f1dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f1dc-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Dropbox iş uygulaması için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="6f1dc-150">**tooconfigure Azure AD çoklu oturum açma iş, Dropbox ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f1dc-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f1dc-151">Merhaba hello üzerinde Azure portal'ın **iş için Dropbox** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6f1dc-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="6f1dc-155">Merhaba üzerinde **iş etki alanı ve URL'ler için Dropbox** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="6f1dc-156">a.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-156">a.</span></span> <span data-ttu-id="6f1dc-157">İş Kiracı için tooyour Dropbox oturum.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="6f1dc-158">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="6f1dc-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6f1dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-159">b.</span></span> <span data-ttu-id="6f1dc-160">Merhaba Gezinti hello sol taraftaki bölmede **Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="6f1dc-161">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="6f1dc-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6f1dc-162">c.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-162">c.</span></span> <span data-ttu-id="6f1dc-163">Merhaba üzerinde **Yönetici Konsolu**, tıklatın **kimlik doğrulaması** hello sol gezinti bölmesindeki.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="6f1dc-164">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="6f1dc-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6f1dc-165">d.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-165">d.</span></span> <span data-ttu-id="6f1dc-166">Merhaba, **çoklu oturum açma** bölümünde, select **çoklu oturum açmayı etkinleştir**ve ardından **daha fazla** tooexpand Bu bölüm.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="6f1dc-167">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="6f1dc-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6f1dc-168">e.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-168">e.</span></span> <span data-ttu-id="6f1dc-169">Merhaba URL'sini Kopyala sonraki çok**kullanıcılar uygulamasında oturum açabilir, e-posta adreslerini girerek veya doğrudan gidebilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="6f1dc-171">f.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-171">f.</span></span> <span data-ttu-id="6f1dc-172">Hello Azure portalında, hello üzerinde **oturum açma URL'si** metin kutusuna, Yapıştır hello URL.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="6f1dc-174">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="6f1dc-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f1dc-175">Bu değer gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-175">This value is not real value.</span></span> <span data-ttu-id="6f1dc-176">Kendi tek oturum açma bölümünden alma hello gerçek oturum açma URL'si ile Merhaba değerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="6f1dc-177">Kişi [iş istemci destek ekibi için Dropbox](https://www.dropbox.com/business/contact) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="6f1dc-178">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="6f1dc-180">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-180">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f1dc-182">Merhaba üzerinde **iş yapılandırması için Dropbox** 'yi tıklatın **yapılandırma Dropbox iş** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6f1dc-183">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6f1dc-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="6f1dc-185">tooconfigure çoklu oturum açma üzerinde **iş için Dropbox** tarafı, iş kiracısında hello için Dropbox gidin **çoklu oturum açma** hello bölümünü **kimlik doğrulaması** sayfasında, Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="6f1dc-186">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="6f1dc-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="6f1dc-187">a.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-187">a.</span></span> <span data-ttu-id="6f1dc-188">Tıklatın **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-188">Click **Required**.</span></span>
   
    <span data-ttu-id="6f1dc-189">b.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-189">b.</span></span> <span data-ttu-id="6f1dc-190">Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **SAML çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="6f1dc-191">c.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-191">c.</span></span> <span data-ttu-id="6f1dc-192">Tıklatın **Sertifika Seç**, tooyour göz atın **Base64 ile kodlanmış sertifika dosyası**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="6f1dc-193">d.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-193">d.</span></span> <span data-ttu-id="6f1dc-194">Tıklatın **değişiklikleri kaydetmek** toocomplete hello yapılandırmasına, DropBox iş Kiracı için.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="6f1dc-195">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6f1dc-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f1dc-196">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f1dc-197">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f1dc-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f1dc-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f1dc-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f1dc-199">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6f1dc-201">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f1dc-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f1dc-202">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="6f1dc-204">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f1dc-206">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f1dc-208">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f1dc-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f1dc-210">a.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-210">a.</span></span> <span data-ttu-id="6f1dc-211">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f1dc-212">b.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-212">b.</span></span> <span data-ttu-id="6f1dc-213">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f1dc-214">c.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-214">c.</span></span> <span data-ttu-id="6f1dc-215">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6f1dc-216">d.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-216">d.</span></span> <span data-ttu-id="6f1dc-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="6f1dc-218">Bir Dropbox iş test kullanıcısı için oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f1dc-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="6f1dc-219">Bu bölümde, iş için Dropbox Britta Simon adlı bir kullanıcı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="6f1dc-220">İş için Dropbox tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="6f1dc-221">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-221">There is no action item for you in this section.</span></span> <span data-ttu-id="6f1dc-222">İş için Dropbox'ın bir kullanıcı zaten mevcut değilse yeni bir iş için Dropbox tooaccess çalıştığınızda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="6f1dc-223">El ile bir kullanıcıyla iletişim toocreate gerekiyorsa [iş istemci destek ekibi için açılan kutu](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="6f1dc-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6f1dc-224">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6f1dc-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6f1dc-225">Bu bölümde, iş için erişim tooDropbox vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6f1dc-227">**tooassign iş Britta Simon tooDropbox hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f1dc-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f1dc-228">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6f1dc-230">Merhaba uygulamalar listesinde **iş için Dropbox**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="6f1dc-232">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6f1dc-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-234">Click **Add** button.</span></span> <span data-ttu-id="6f1dc-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6f1dc-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f1dc-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f1dc-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f1dc-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6f1dc-240">Testing single sign-on</span></span>

<span data-ttu-id="6f1dc-241">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f1dc-242">Merhaba erişim paneli iş parçasında Merhaba Dropbox'ı tıklattığınızda, Dropbox oturum açma sayfasında iş uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f1dc-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f1dc-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6f1dc-243">Additional resources</span></span>

* [<span data-ttu-id="6f1dc-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6f1dc-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f1dc-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6f1dc-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6f1dc-246">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="6f1dc-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

