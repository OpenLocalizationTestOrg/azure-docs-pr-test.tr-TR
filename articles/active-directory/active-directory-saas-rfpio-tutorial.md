---
title: "Öğretici: Azure Active Directory Tümleştirme ile RFPIO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile RFPIO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="b5cc4-103">Öğretici: Azure Active Directory Tümleştirme RFPIO ile</span><span class="sxs-lookup"><span data-stu-id="b5cc4-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="b5cc4-104">Bu öğreticide, bilgi nasıl toointegrate RFPIO Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5cc4-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5cc4-105">RFPIO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5cc4-106">Denetleyebilirsiniz kimlerin erişimi tooRFPIO olan Azure AD içinde.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="b5cc4-107">Kullanıcıların tooautomatically get açan tooRFPIO (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b5cc4-108">Hesaplarınızı bir merkezi konumda--hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="b5cc4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5cc4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5cc4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b5cc4-110">Prerequisites</span></span>

<span data-ttu-id="b5cc4-111">tooconfigure RFPIO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="b5cc4-112">Bir Azure AD abonelik.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="b5cc4-113">RFPIO tek bir oturum üzerinde etkin olmayan abonelik.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b5cc4-114">Bu öğreticide, bir üretim ortamı tootest hello adımları kullanmanızı öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="b5cc4-115">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="b5cc4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="b5cc4-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5cc4-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5cc4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b5cc4-118">Scenario description</span></span>
<span data-ttu-id="b5cc4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5cc4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5cc4-121">RFPIO hello Galerisi'nden ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="b5cc4-122">Yapılandırma ve Azure AD sınama çoklu oturum açmayı.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="b5cc4-123">Merhaba Galerisi'nden RFPIO ekleme</span><span class="sxs-lookup"><span data-stu-id="b5cc4-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="b5cc4-124">Azure AD'ye tooconfigure hello tümleştirme RFPIO, tooadd RFPIO hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="b5cc4-125">tooadd RFPIO hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="b5cc4-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="b5cc4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesinde Merhaba, seçin hello **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5cc4-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b5cc4-130">tooadd yeni bir uygulama seçin hello **yeni uygulama** hello iletişim kutusunun üstündeki düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b5cc4-132">Merhaba arama kutusuna yazın **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-132">In hello search box, type **RFPIO**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="b5cc4-134">Merhaba Sonuçlar panelinde seçin **RFPIO**ve ardından hello **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b5cc4-136">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b5cc4-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b5cc4-137">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı RFPIO sınayın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5cc4-138">Tek toowork'ın oturum açma, Azure AD hangi hello RFPIO karşılık gelen kullanıcı ve bir kullanıcı Azure AD'de arasındaki ilişkidir tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="b5cc4-139">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı RFPIO hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="b5cc4-140">Merhaba değeri RFPIO içinde atayın **kullanıcı adı** hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b5cc4-141">tooconfigure ve RFPIO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5cc4-142">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**--tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5cc4-143">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**--Britta Simon ile Azure AD çoklu oturum açma tootest.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5cc4-144">**[RFPIO test kullanıcısı oluşturma](#creating-a-rfpio-test-user)**  --toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir RFPIO içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5cc4-145">**[Hello Azure AD test kullanıcısı atayın](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5cc4-146">**[Test çoklu oturum açma](#testing-single-sign-on)**  --tooverify hello yapılandırma çalışıyorsa.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b5cc4-147">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b5cc4-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b5cc4-148">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma RFPIO uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="b5cc4-149">**tooconfigure Azure AD çoklu oturum açma ile RFPIO, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5cc4-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5cc4-150">Hello hello üzerinde Azure portal'ın **RFPIO** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b5cc4-152">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="b5cc4-154">Merhaba üzerinde **RFPIO etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="b5cc4-156">a.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-156">a.</span></span> <span data-ttu-id="b5cc4-157">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="b5cc4-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="b5cc4-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-159">b.</span></span> <span data-ttu-id="b5cc4-160">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="b5cc4-161">c.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-161">c.</span></span> <span data-ttu-id="b5cc4-162">Merhaba, **geçiş durumunu** metin kutusuna bir dize değeri girin.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="b5cc4-163">Kişi [RFPIO destek ekibi](https://www.rfpio.com/contact/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="b5cc4-164">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="b5cc4-165">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="b5cc4-167">Merhaba, **URL üzerinde oturum** metin kutusuna, türü hello URL'si:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="b5cc4-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="b5cc4-168">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="b5cc4-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b5cc4-172">Farklı bir web tarayıcısı penceresinde, oturum açma toohello **RFPIO** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="b5cc4-173">Merhaba alt sol köşe açılan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-173">Click on hello bottom left corner dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="b5cc4-175">Tıklatın hello üzerinde **kuruluş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-175">Click on hello **Organization Settings**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="b5cc4-177">Tıklatın hello üzerinde **özellikler ve tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="b5cc4-179">Merhaba, **SAML SSO Yapılandırması** tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="b5cc4-181">Bu bölümde aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-181">In this Section perform following actions:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="b5cc4-183">a.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-183">a.</span></span> <span data-ttu-id="b5cc4-184">Merhaba Merhaba içeriğine kopyalama **indirilen meta veri XML** ve hello yapıştırma **kimlik Yapılandırması** alan.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="b5cc4-185">toocopy hello içeriğini indirilen **meta veri XML** kullanım **not defteri ++** veya uygun **XML Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="b5cc4-186">b.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-186">b.</span></span> <span data-ttu-id="b5cc4-187">Tıklatın **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-187">Click **Validate**.</span></span>

    <span data-ttu-id="b5cc4-188">c.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-188">c.</span></span> <span data-ttu-id="b5cc4-189">Tıkladığınızda sonra **doğrulama**Çevir, **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="b5cc4-190">d.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-190">d.</span></span> <span data-ttu-id="b5cc4-191">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="b5cc4-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b5cc4-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5cc4-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5cc4-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5cc4-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b5cc4-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5cc4-195">Create an Azure AD test user</span></span>
<span data-ttu-id="b5cc4-196">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b5cc4-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5cc4-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5cc4-199">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5cc4-201">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5cc4-203">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5cc4-205">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5cc4-207">a.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-207">a.</span></span> <span data-ttu-id="b5cc4-208">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5cc4-209">b.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-209">b.</span></span> <span data-ttu-id="b5cc4-210">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5cc4-211">c.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-211">c.</span></span> <span data-ttu-id="b5cc4-212">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b5cc4-213">d.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-213">d.</span></span> <span data-ttu-id="b5cc4-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="b5cc4-215">RFPIO test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5cc4-215">Create a RFPIO test user</span></span>

<span data-ttu-id="b5cc4-216">tooenable Azure AD kullanıcıların toolog tooRFPIO bunların RFPIO sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="b5cc4-217">RFPIO Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="b5cc4-218">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5cc4-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5cc4-219">İçinde tooyour RFPIO şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="b5cc4-220">Merhaba alt sol köşe açılan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-220">Click on hello bottom left corner dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="b5cc4-222">Tıklatın hello üzerinde **kuruluş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-222">Click on hello **Organization Settings**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="b5cc4-224">Tıklatın **ekip ÜYELERİNİN**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-224">Click **TEAM MEMBERS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="b5cc4-226">Tıklayın **ÜYELER Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-226">Click on **ADD MEMBERS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="b5cc4-228">Merhaba, **eklediğiniz yeni üyeler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="b5cc4-229">Aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5cc4-229">Perform following actions:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="b5cc4-231">a.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-231">a.</span></span> <span data-ttu-id="b5cc4-232">ENTER **e-posta adresi** hello içinde **satır başına bir e-posta girin** alan.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="b5cc4-233">b.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-233">b.</span></span> <span data-ttu-id="b5cc4-234">Lütfen seçin **rol** gereksinimlerinize göre.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="b5cc4-235">c.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-235">c.</span></span> <span data-ttu-id="b5cc4-236">Tıklatın **ÜYELER Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="b5cc4-237">Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b5cc4-238">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="b5cc4-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b5cc4-239">Bu bölümde, erişim tooRFPIO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b5cc4-241">**tooassign Britta Simon tooRFPIO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5cc4-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5cc4-242">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b5cc4-244">Merhaba uygulamalar listesinde **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-244">In hello applications list, select **RFPIO**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="b5cc4-246">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b5cc4-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-248">Click **Add** button.</span></span> <span data-ttu-id="b5cc4-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b5cc4-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5cc4-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5cc4-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b5cc4-254">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="b5cc4-254">Test single sign-on</span></span>

<span data-ttu-id="b5cc4-255">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="b5cc4-256">RFPIO döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma tooyour RFPIO uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5cc4-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="b5cc4-257">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5cc4-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5cc4-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b5cc4-258">Additional resources</span></span>

* [<span data-ttu-id="b5cc4-259">İlgili öğreticiler listesi toointegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b5cc4-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5cc4-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b5cc4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

