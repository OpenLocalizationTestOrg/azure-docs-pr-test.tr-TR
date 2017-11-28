---
title: "Öğretici: Azure Active Directory Tümleştirme ile BlueJeans | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile BlueJeans arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="eef53-103">Öğretici: Azure Active Directory Tümleştirme BlueJeans ile</span><span class="sxs-lookup"><span data-stu-id="eef53-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="eef53-104">Bu öğreticide, bilgi nasıl toointegrate BlueJeans Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eef53-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eef53-105">BlueJeans Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="eef53-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eef53-106">Erişim tooBlueJeans sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eef53-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="eef53-107">Kullanıcıların tooautomatically get açan tooBlueJeans (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eef53-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eef53-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="eef53-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eef53-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eef53-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eef53-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eef53-110">Prerequisites</span></span>

<span data-ttu-id="eef53-111">tooconfigure BlueJeans ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eef53-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="eef53-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="eef53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eef53-113">Bir BlueJeans çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="eef53-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eef53-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="eef53-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eef53-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="eef53-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eef53-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="eef53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eef53-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eef53-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eef53-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="eef53-118">Scenario description</span></span>
<span data-ttu-id="eef53-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="eef53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eef53-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="eef53-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eef53-121">Merhaba Galerisi'nden BlueJeans ekleme</span><span class="sxs-lookup"><span data-stu-id="eef53-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="eef53-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="eef53-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="eef53-123">Merhaba Galerisi'nden BlueJeans ekleme</span><span class="sxs-lookup"><span data-stu-id="eef53-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="eef53-124">Azure AD'ye tooconfigure hello tümleştirme BlueJeans, tooadd BlueJeans hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="eef53-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eef53-125">**tooadd BlueJeans hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eef53-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eef53-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eef53-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eef53-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="eef53-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eef53-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eef53-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="eef53-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef53-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="eef53-133">Merhaba arama kutusuna yazın **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="eef53-133">In hello search box, type **BlueJeans**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="eef53-135">Merhaba Sonuçlar panelinde seçin **BlueJeans**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="eef53-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eef53-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="eef53-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eef53-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BlueJeans ile test etme</span><span class="sxs-lookup"><span data-stu-id="eef53-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eef53-139">Tek toowork'ın oturum açma hangi hello karşılık gelen BlueJeans içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="eef53-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="eef53-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı BlueJeans hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="eef53-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="eef53-141">Merhaba hello değeri BlueJeans içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="eef53-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eef53-142">tooconfigure ve BlueJeans ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eef53-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eef53-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="eef53-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eef53-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="eef53-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eef53-145">**[BlueJeans test kullanıcısı oluşturma](#creating-a-bluejeans-test-user)**  -toohave karşılık gelen, Britta Simon BlueJeans içinde kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="eef53-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eef53-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eef53-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eef53-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="eef53-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eef53-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eef53-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eef53-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma BlueJeans uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eef53-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="eef53-150">**tooconfigure Azure AD çoklu oturum açma ile BlueJeans, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eef53-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="eef53-151">Hello hello üzerinde Azure portal'ın **BlueJeans** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="eef53-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="eef53-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eef53-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="eef53-155">Merhaba üzerinde **BlueJeans etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eef53-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="eef53-157">a.</span><span class="sxs-lookup"><span data-stu-id="eef53-157">a.</span></span> <span data-ttu-id="eef53-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="eef53-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="eef53-159">b.</span><span class="sxs-lookup"><span data-stu-id="eef53-159">b.</span></span> <span data-ttu-id="eef53-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="eef53-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eef53-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="eef53-161">These values are not real.</span></span> <span data-ttu-id="eef53-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="eef53-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eef53-163">Kişi [BlueJeans istemci destek ekibi](https://support.bluejeans.com/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="eef53-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="eef53-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eef53-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="eef53-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef53-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eef53-168">Merhaba üzerinde **BlueJeans yapılandırma** 'yi tıklatın **yapılandırma BlueJeans** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="eef53-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eef53-169">Kopya hello **Sign-Out URL, değişiklik parola URL'si ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="eef53-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="eef53-171">Farklı web tarayıcısı penceresinde tooyour içinde oturum **BlueJeans** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="eef53-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="eef53-172">Çok Git**yönetici \> grup ayarları \> güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="eef53-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="eef53-173">![Yönetici](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="eef53-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="eef53-174">Merhaba, **güvenlik** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eef53-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="eef53-175">![SAML çoklu oturum açma](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="eef53-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="eef53-176">a.</span><span class="sxs-lookup"><span data-stu-id="eef53-176">a.</span></span> <span data-ttu-id="eef53-177">Seçin **SAML çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="eef53-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="eef53-178">b.</span><span class="sxs-lookup"><span data-stu-id="eef53-178">b.</span></span> <span data-ttu-id="eef53-179">Seçin **otomatik sağlamayı etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="eef53-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="eef53-180">Aşağıdaki adımları hello ile geçin:</span><span class="sxs-lookup"><span data-stu-id="eef53-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="eef53-181">![Sertifika yolu](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "sertifika yolu")</span><span class="sxs-lookup"><span data-stu-id="eef53-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="eef53-182">a.</span><span class="sxs-lookup"><span data-stu-id="eef53-182">a.</span></span> <span data-ttu-id="eef53-183">Tıklatın **Dosya Seç**ve indirilen hello sertifikasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eef53-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="eef53-184">b.</span><span class="sxs-lookup"><span data-stu-id="eef53-184">b.</span></span> <span data-ttu-id="eef53-185">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello içine **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="eef53-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="eef53-186">c.</span><span class="sxs-lookup"><span data-stu-id="eef53-186">c.</span></span> <span data-ttu-id="eef53-187">Yapıştır **değişiklik parola URL'si** hello içine **parola değişikliği URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="eef53-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="eef53-188">d.</span><span class="sxs-lookup"><span data-stu-id="eef53-188">d.</span></span> <span data-ttu-id="eef53-189">Yapıştır **Sign-Out URL** hello içine **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="eef53-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="eef53-190">Aşağıdaki adımları hello ile geçin:</span><span class="sxs-lookup"><span data-stu-id="eef53-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="eef53-191">![Değişiklikleri kaydetmek](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Değişiklikleri Kaydet")</span><span class="sxs-lookup"><span data-stu-id="eef53-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="eef53-192">a.</span><span class="sxs-lookup"><span data-stu-id="eef53-192">a.</span></span> <span data-ttu-id="eef53-193">Merhaba, **kullanıcı kimliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="eef53-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="eef53-194">b.</span><span class="sxs-lookup"><span data-stu-id="eef53-194">b.</span></span> <span data-ttu-id="eef53-195">Merhaba, **e-posta** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="eef53-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="eef53-196">c.</span><span class="sxs-lookup"><span data-stu-id="eef53-196">c.</span></span> <span data-ttu-id="eef53-197">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="eef53-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="eef53-198">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="eef53-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eef53-199">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="eef53-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eef53-200">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eef53-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eef53-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eef53-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="eef53-202">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="eef53-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="eef53-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eef53-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eef53-205">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eef53-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eef53-207">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="eef53-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eef53-209">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="eef53-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eef53-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eef53-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eef53-213">a.</span><span class="sxs-lookup"><span data-stu-id="eef53-213">a.</span></span> <span data-ttu-id="eef53-214">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eef53-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eef53-215">b.</span><span class="sxs-lookup"><span data-stu-id="eef53-215">b.</span></span> <span data-ttu-id="eef53-216">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="eef53-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eef53-217">c.</span><span class="sxs-lookup"><span data-stu-id="eef53-217">c.</span></span> <span data-ttu-id="eef53-218">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="eef53-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eef53-219">d.</span><span class="sxs-lookup"><span data-stu-id="eef53-219">d.</span></span> <span data-ttu-id="eef53-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eef53-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="eef53-221">BlueJeans test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eef53-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="eef53-222">tooenable Azure AD kullanıcıların toolog tooBlueJeans bunların BlueJeans sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eef53-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="eef53-223">BlueJeans durumunda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="eef53-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="eef53-224">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="eef53-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="eef53-225">İçinde tooyour oturum **BlueJeans** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="eef53-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="eef53-226">Çok Git**yönetici \> kullanıcıları yönetme \> Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="eef53-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="eef53-227">![Yönetici](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="eef53-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="eef53-228">Merhaba **Kullanıcı Ekle** sekmesi kullanılabilir yalnızca hello içindeki IF **Güvenlik sekmesinde**, **otomatik sağlamayı etkinleştirmek** işaretli değildir.</span><span class="sxs-lookup"><span data-stu-id="eef53-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="eef53-229">Merhaba, **Kullanıcı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eef53-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="eef53-230">![Kullanıcı ekleme](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="eef53-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="eef53-231">a.</span><span class="sxs-lookup"><span data-stu-id="eef53-231">a.</span></span> <span data-ttu-id="eef53-232">Tür a **BlueJeans kullanıcı adı**, bir **e-posta adresi**, **BlueJeans toplantı kimliği**, **yönetici parolası**, **tam adı** , hello **şirket** , metin kutuları hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.</span><span class="sxs-lookup"><span data-stu-id="eef53-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="eef53-233">b.</span><span class="sxs-lookup"><span data-stu-id="eef53-233">b.</span></span> <span data-ttu-id="eef53-234">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="eef53-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="eef53-235">API AAD kullanıcı hesaplarının BlueJeans tooprovision tarafından sağlanan veya herhangi diğer BlueJeans kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eef53-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eef53-236">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="eef53-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eef53-237">Bu bölümde, erişim tooBlueJeans vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eef53-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="eef53-239">**tooassign Britta Simon tooBlueJeans hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eef53-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="eef53-240">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eef53-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="eef53-242">Merhaba uygulamalar listesinde **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="eef53-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="eef53-244">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="eef53-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="eef53-246">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eef53-246">Click **Add** button.</span></span> <span data-ttu-id="eef53-247">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eef53-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="eef53-249">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="eef53-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eef53-250">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eef53-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eef53-251">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eef53-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eef53-252">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="eef53-252">Testing single sign-on</span></span>

<span data-ttu-id="eef53-253">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="eef53-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eef53-254">Merhaba erişim paneli BlueJeans döşeme hello tıkladığınızda, oturum açma sayfasına BlueJeans uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eef53-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="eef53-255">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eef53-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eef53-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="eef53-256">Additional resources</span></span>

* [<span data-ttu-id="eef53-257">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="eef53-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eef53-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="eef53-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

