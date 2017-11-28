---
title: "Öğretici: Azure Active Directory Tümleştirme ile Clarizen | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Clarizen arasında."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="8c80c-103">Öğretici: Azure Active Directory Tümleştirme Clarizen ile</span><span class="sxs-lookup"><span data-stu-id="8c80c-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="8c80c-104">Bu öğreticide, bilgi nasıl toointegrate Clarizen ile Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c80c-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="8c80c-105">Yararları hello Bu tümleştirme sağlar:</span><span class="sxs-lookup"><span data-stu-id="8c80c-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="8c80c-106">Erişim tooClarizen sahip Azure AD'de denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c80c-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="8c80c-107">Azure AD hesaplarına sahip (çoklu oturum açma) tooClarizen içinde otomatik olarak imzalanmış, kullanıcıların toobe etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c80c-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8c80c-108">Hesaplarınızı bir merkezi konumda, hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="8c80c-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="8c80c-109">Bu öğreticide Hello senaryo iki ana görevden oluşur:</span><span class="sxs-lookup"><span data-stu-id="8c80c-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="8c80c-110">Clarizen hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="8c80c-111">Yapılandırma ve Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="8c80c-112">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla bilgi istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c80c-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c80c-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8c80c-113">Prerequisites</span></span>
<span data-ttu-id="8c80c-114">tooconfigure Clarizen ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8c80c-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="8c80c-115">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8c80c-115">An Azure AD subscription</span></span>
- <span data-ttu-id="8c80c-116">Çoklu oturum açma için etkinleştirilen Clarizen abonelik</span><span class="sxs-lookup"><span data-stu-id="8c80c-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="8c80c-117">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="8c80c-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="8c80c-118">Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c80c-119">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8c80c-120">Bir Azure AD test ortamı yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c80c-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="8c80c-121">Merhaba Galerisi'nden Clarizen ekleme</span><span class="sxs-lookup"><span data-stu-id="8c80c-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="8c80c-122">Azure AD'ye Clarizen tooconfigure hello tümleştirilmesi hello galeri tooyour listesinden yönetilen SaaS uygulamaları Clarizen ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="8c80c-123">Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, hello tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory simgesi][1]

2. <span data-ttu-id="8c80c-125">Tıklatın **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="8c80c-126">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-126">Then click **All applications**.</span></span>

    !["Kurumsal uygulamalar" ve "Tüm uygulamalar" ı tıklatarak][2]

3. <span data-ttu-id="8c80c-128">Merhaba tıklatın **Ekle** hello hello iletişim kutusunun üstündeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="8c80c-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![Merhaba "Ekle" düğmesi][3]

4. <span data-ttu-id="8c80c-130">Merhaba arama kutusuna yazın **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-130">In hello search box, type **Clarizen**.</span></span>

    ![Merhaba arama kutusuna "Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="8c80c-132">Merhaba sonuçlar bölmesinde seçin **Clarizen**ve ardından **Ekle** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8c80c-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Merhaba sonuçlar bölmesinde Clarizen seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8c80c-134">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8c80c-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8c80c-135">Aşağıdaki bölümlerde hello, yapılandırmak ve Azure AD çoklu oturum açma hello test kullanıcıya Britta Simon bağlı Clarizen test.</span><span class="sxs-lookup"><span data-stu-id="8c80c-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="8c80c-136">Tek toowork'ın oturum açma hangi hello karşılık gelen Clarizen içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c80c-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="8c80c-137">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Clarizen hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c80c-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="8c80c-138">Merhaba değerini atayarak bu bağlantı ilişkisini kurmak **kullanıcı adı** hello değeri olarak Azure AD'de **kullanıcıadı** Clarizen içinde.</span><span class="sxs-lookup"><span data-stu-id="8c80c-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="8c80c-139">tooconfigure ve Azure AD çoklu oturum açmayı test Clarizen, yapı taşları aşağıdaki tam hello ile:</span><span class="sxs-lookup"><span data-stu-id="8c80c-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="8c80c-140">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8c80c-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c80c-141">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  Britta Simon ile Azure AD çoklu oturum açma tootest.</span><span class="sxs-lookup"><span data-stu-id="8c80c-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c80c-142">**[Clarizen test kullanıcısı oluşturma](#create-a-clarizen-test-user)**  toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir Clarizen içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="8c80c-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8c80c-143">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8c80c-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c80c-144">**[Test çoklu oturum açma](#test-single-sign-on)**  tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8c80c-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8c80c-145">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8c80c-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="8c80c-146">Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Clarizen uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="8c80c-147">Hello hello üzerinde Azure portal'ın **Clarizen** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    !["Çoklu oturum açma" a tıklayarak][4]

2. <span data-ttu-id="8c80c-149">Merhaba, **çoklu oturum açma** iletişim kutusu için **modu**seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8c80c-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    !["SAML tabanlı oturum açma" seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="8c80c-151">Merhaba, **Clarizen etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c80c-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Tanımlayıcı ve yanıt URL'si için kutuları](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="8c80c-153">a.</span><span class="sxs-lookup"><span data-stu-id="8c80c-153">a.</span></span> <span data-ttu-id="8c80c-154">Merhaba, **tanımlayıcısı** kutusunda türü hello değeri olarak: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="8c80c-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="8c80c-155">b.</span><span class="sxs-lookup"><span data-stu-id="8c80c-155">b.</span></span> <span data-ttu-id="8c80c-156">Merhaba, **yanıt URL'si** desen aşağıdaki hello kullanarak bir URL yazın: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="8c80c-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c80c-157">Bunlar hello gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="8c80c-157">These are not hello real values.</span></span> <span data-ttu-id="8c80c-158">Toouse hello gerçek tanımlayıcısına sahip ve URL yanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="8c80c-159">Burada tanımlayıcı hello gibi hello benzersiz bir dize değerini kullanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="8c80c-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="8c80c-160">tooget hello gerçek değerler, kişi hello [Clarizen destek ekibi](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="8c80c-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="8c80c-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    !["Yeni Sertifika Oluştur" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="8c80c-163">Merhaba, **yeni sertifika oluştur** iletişim kutusunda, hello takvim simgesini tıklatın ve bir sona erme tarihi seçin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="8c80c-164">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-164">Then click **Save**.</span></span>

    ![Seçme ve sona erme tarihi kaydetme](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="8c80c-166">Merhaba, **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Merhaba yeni sertifika etkin hale getirme için Hello onay kutusu seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="8c80c-168">Merhaba, **geçiş sertifikası** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    !["Tamam" toomake hello sertifika etkin istediğiniz tooconfirm tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8c80c-170">Merhaba, **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    !["Sertifika (Base64)" toostart hello Yükle'yi tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="8c80c-172">Merhaba, **Clarizen yapılandırma** 'yi tıklatın **yapılandırma Clarizen** tooopen hello **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    !["Clarizen Yapılandır" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !["Oturum açma yapılandırma" penceresinde, dosyaları ve URL'leri dahil](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="8c80c-175">Farklı web tarayıcısı penceresinde tooyour Clarizen şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="8c80c-176">Kullanıcı adınıza tıklayın ve ardından **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="8c80c-177">![Kullanıcı adınızı "Ayarlar"'ı tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="8c80c-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="8c80c-178">Merhaba tıklatın **genel ayarları** sekmesi. Ardından, sonraki çok**şirket dışı kimlik doğrulaması**, tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="8c80c-179">!["Genel ayarları" sekmesini](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "genel ayarları")</span><span class="sxs-lookup"><span data-stu-id="8c80c-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="8c80c-180">Merhaba, **şirket dışı kimlik doğrulaması** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c80c-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="8c80c-181">!["Federe kimlik doğrulaması" iletişim kutusu](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "şirket dışı kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="8c80c-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="8c80c-182">a.</span><span class="sxs-lookup"><span data-stu-id="8c80c-182">a.</span></span> <span data-ttu-id="8c80c-183">Seçin **etkinleştir federe kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="8c80c-184">b.</span><span class="sxs-lookup"><span data-stu-id="8c80c-184">b.</span></span> <span data-ttu-id="8c80c-185">Tıklatın **karşıya** tooupload indirilen sertifikanızı.</span><span class="sxs-lookup"><span data-stu-id="8c80c-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="8c80c-186">c.</span><span class="sxs-lookup"><span data-stu-id="8c80c-186">c.</span></span> <span data-ttu-id="8c80c-187">Merhaba, **oturum açma URL'si** kutusuna, hello değerini girin **SAML çoklu oturum açma hizmet URL'si** hello Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="8c80c-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="8c80c-188">d.</span><span class="sxs-lookup"><span data-stu-id="8c80c-188">d.</span></span> <span data-ttu-id="8c80c-189">Merhaba, **Sign-out URL** kutusuna, hello değerini girin **Sign-Out URL** hello Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="8c80c-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="8c80c-190">e.</span><span class="sxs-lookup"><span data-stu-id="8c80c-190">e.</span></span> <span data-ttu-id="8c80c-191">Seçin **POST kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-191">Select **Use POST**.</span></span>

    <span data-ttu-id="8c80c-192">f.</span><span class="sxs-lookup"><span data-stu-id="8c80c-192">f.</span></span> <span data-ttu-id="8c80c-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8c80c-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c80c-194">Create an Azure AD test user</span></span>
<span data-ttu-id="8c80c-195">Hello Azure portal, Britta Simon adlı bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c80c-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Hello Azure AD test kullanıcı adı ve e-posta adresi][100]

1. <span data-ttu-id="8c80c-197">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory simgesi](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8c80c-199">Tıklatın **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8c80c-201">Merhaba iletişim kutusunun Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="8c80c-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![Merhaba "Ekle" düğmesi](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8c80c-203">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c80c-203">In hello **User** dialog box, perform hello following steps:</span></span>

    !["Kullanıcı" iletişim kutusu adı, e-posta adresi ve parola ile doldurulur](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8c80c-205">a.</span><span class="sxs-lookup"><span data-stu-id="8c80c-205">a.</span></span> <span data-ttu-id="8c80c-206">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c80c-207">b.</span><span class="sxs-lookup"><span data-stu-id="8c80c-207">b.</span></span> <span data-ttu-id="8c80c-208">Merhaba, **kullanıcı adı** kutusunda hello Britta Simon hesap türü hello e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="8c80c-209">c.</span><span class="sxs-lookup"><span data-stu-id="8c80c-209">c.</span></span> <span data-ttu-id="8c80c-210">Seçin **Göster parola** ve hello değerini yazmak **parola**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="8c80c-211">d.</span><span class="sxs-lookup"><span data-stu-id="8c80c-211">d.</span></span> <span data-ttu-id="8c80c-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="8c80c-213">Clarizen test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c80c-213">Create a Clarizen test user</span></span>
<span data-ttu-id="8c80c-214">tooenable Azure AD kullanıcıların toosign tooClarizen içinde kullanıcı hesapları hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c80c-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="8c80c-215">Clarizen Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="8c80c-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="8c80c-216">İçinde tooyour Clarizen şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="8c80c-217">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-217">Click **People**.</span></span>

    <span data-ttu-id="8c80c-218">!["Kişiler" tıklatarak](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="8c80c-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="8c80c-219">Tıklatın **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-219">Click **Invite User**.</span></span>

    <span data-ttu-id="8c80c-220">!["Kullanıcı davet" düğmesine](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="8c80c-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="8c80c-221">Merhaba, **kişileri davet** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c80c-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="8c80c-222">!["Kişileri davet edin" iletişim kutusu](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="8c80c-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="8c80c-223">a.</span><span class="sxs-lookup"><span data-stu-id="8c80c-223">a.</span></span> <span data-ttu-id="8c80c-224">Merhaba, **e-posta** kutusunda hello Britta Simon hesap türü hello e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="8c80c-225">b.</span><span class="sxs-lookup"><span data-stu-id="8c80c-225">b.</span></span> <span data-ttu-id="8c80c-226">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c80c-227">Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8c80c-228">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="8c80c-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="8c80c-229">Her erişim tooClarizen vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8c80c-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Atanan test kullanıcısı][200]

1. <span data-ttu-id="8c80c-231">Hello Azure portal, hello uygulamaları görünümü Aç, toohello dizin görünümü göz atın, tıklatın **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    !["Kurumsal uygulamalar" ve "Tüm uygulamalar" ı tıklatarak][201]

2. <span data-ttu-id="8c80c-233">Merhaba uygulamalar listesinde **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-233">In hello applications list, select **Clarizen**.</span></span>

    ![Merhaba listesinde Clarizen seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="8c80c-235">Merhaba sol bölmede **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-235">In hello left pane, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" a tıklayarak][202]

4. <span data-ttu-id="8c80c-237">Merhaba tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-237">Click hello **Add** button.</span></span> <span data-ttu-id="8c80c-238">Ardından hello **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8c80c-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Hello "Ekle" düğmesi ve hello "Atama Ekle" iletişim kutusu][203]

5. <span data-ttu-id="8c80c-240">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcılar hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="8c80c-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="8c80c-241">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda, hello **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="8c80c-242">Merhaba, **eklemek atama** iletişim hello kutusunda, **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8c80c-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="8c80c-243">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="8c80c-243">Test single sign-on</span></span>
<span data-ttu-id="8c80c-244">Azure AD çoklu oturum açma yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="8c80c-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="8c80c-245">Merhaba Clarizen hello erişim paneli parçasında tıklattığınızda tooyour Clarizen uygulama otomatik olarak imzalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8c80c-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c80c-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8c80c-246">Additional resources</span></span>

* [<span data-ttu-id="8c80c-247">İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8c80c-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c80c-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8c80c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
