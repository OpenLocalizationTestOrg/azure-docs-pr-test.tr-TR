---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Facebook ile çalışma alanına arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="d0c2b-103">Öğretici: Facebook ile çalışma alanına Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d0c2b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="d0c2b-104">Bu öğreticide, bilgi nasıl toointegrate Facebook ile Azure Active Directory (Azure AD) ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0c2b-105">Çalışma alanına Facebook ile Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0c2b-106">Facebook tarafından erişim tooWorkplace sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="d0c2b-107">Kullanıcılarınızın tooautomatically imzalı üzerinde tooWorkplace (çoklu oturum açma) tarafından Facebook ile Azure AD hesaplarına etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d0c2b-108">Hesaplarınızı tek bir merkezi konumda yönetebilirsiniz: Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="d0c2b-109">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla ayrıntı için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0c2b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d0c2b-110">Prerequisites</span></span>

<span data-ttu-id="d0c2b-111">Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="d0c2b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d0c2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0c2b-113">Abonelik çalışma alanına Facebook çoklu oturum açma (SSO) tarafından etkin</span><span class="sxs-lookup"><span data-stu-id="d0c2b-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="d0c2b-114">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d0c2b-115">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0c2b-116">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0c2b-117">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d0c2b-117">Scenario description</span></span>
<span data-ttu-id="d0c2b-118">Bu öğreticide, Azure AD SSO bir test ortamında test.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="d0c2b-119">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0c2b-120">Facebook ile çalışma alanına hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="d0c2b-121">Yapılandırma ve Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="d0c2b-122">Facebook ile çalışma alanına hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="d0c2b-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="d0c2b-123">tooconfigure hello tümleştirmeye çalışma alanı Facebook ile Azure AD hello galeri tooyour listesinden yönetilen SaaS uygulamaları Facebook ile çalışma alanına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="d0c2b-124">Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="d0c2b-126">Çok Gözat**kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="d0c2b-128">tooadd hello yeni uygulama, select **yeni uygulama** hello iletişim kutusunun hello üstte.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="d0c2b-130">Merhaba arama kutusuna yazın **Facebook ile çalışma alanına**seçip **Facebook ile çalışma alanına** sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="d0c2b-131">Ardından **Ekle**, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-131">Then select **Add**, tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Facebook ile çalışma](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d0c2b-133">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d0c2b-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d0c2b-134">Bu bölümde, yapılandırma ve Azure AD çalışma alanına "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Facebook tarafından SSO'su test etme</span><span class="sxs-lookup"><span data-stu-id="d0c2b-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0c2b-135">SSO toowork için hangi hello karşılık gelen çalışma Facebook tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="d0c2b-136">Diğer bir deyişle, bir Azure AD kullanıcısının ve Facebook ile çalışma hello ilgili kullanıcı arasında bağlantılı bir ilişkisi kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="d0c2b-137">Merhaba hello değerini atayarak bu ilişki kurmak **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Facebook ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d0c2b-138">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d0c2b-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d0c2b-139">Bu bölümdeki hello Azure portalında Azure AD SSO'yu etkinleştirmek ve SSO Facebook uygulama tarafından çalışma alanınızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="d0c2b-140">Merhaba hello üzerinde Azure portal'ın **Facebook ile çalışma alanına** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="d0c2b-142">Merhaba, **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="d0c2b-144">Merhaba, **Facebook etki alanı ve URL'ler ile çalışma alanına** bölümünde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="d0c2b-145">a.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-145">a.</span></span> <span data-ttu-id="d0c2b-146">Merhaba, **oturum açma URL'si** metin kutusuna, hello desen kullanan bir URL yazın:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="d0c2b-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="d0c2b-147">b.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-147">b.</span></span> <span data-ttu-id="d0c2b-148">Merhaba, **tanımlayıcısı** metin kutusuna, hello desen kullanan bir URL yazın:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="d0c2b-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0c2b-149">Bu yalnızca bir örnek değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-149">These values are an example only.</span></span> <span data-ttu-id="d0c2b-150">Bu değerler, oturum açma hello gerçek URL ve tanımlayıcıdır ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="d0c2b-151">Kişi hello [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="d0c2b-152">Merhaba, **SAML imzalama sertifikası** bölümünde, select **sertifika (Base64)**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="d0c2b-154">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-154">Select **Save**.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d0c2b-156">Merhaba, **Facebook yapılandırmaya göre çalışma alanına** bölümünde, select **yapılandırma çalışma Facebook tarafından** tooopen hello **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="d0c2b-157">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Facebook yapılandırma ile çalışma](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="d0c2b-159">Farklı web tarayıcısı penceresinde bir yönetici olarak oturum açma tooyour Facebook şirket site tarafından çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="d0c2b-160">Merhaba SAML kimlik doğrulama işleminin bir parçası olarak, çalışma alanına sipariş toopass parametreleri tooAzure AD boyutu too2.5 kilobayt yukarı sorgu dizelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="d0c2b-161">Merhaba, **şirket Pano**, Git toohello **kimlik doğrulaması** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="d0c2b-162">Altında **SAML kimlik doğrulaması**seçin **yalnızca SSO** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="d0c2b-163">Merhaba kopyalanan hello değerleri girin **Facebook yapılandırmaya göre çalışma alanına** hello hello karşılık gelen alanlara Azure portalı bölümünde:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="d0c2b-164">İçinde **SAML URL** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si**, Azure portal hello kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="d0c2b-165">İçinde **SAML veren URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portal hello kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="d0c2b-166">İçinde **SAML oturum kapatma yeniden yönlendir (isteğe bağlı)**, hello değerini yapıştırın **Sign-Out URL**, Azure portal hello kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="d0c2b-167">Açık, **base-64 kodlamalı sertifika** hello Azure portal ' Not Defteri'nde, indirilen.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="d0c2b-168">Merhaba içeriğine, panoya kopyalayın ve ardından toothe yapıştırın **SAML sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="d0c2b-169">Tooenter hello İzleyici gerekebilecek URL, alıcı URL ve ACS (onaylama tüketici hizmeti) hello altında listelenen URL **SAML Yapılandırması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="d0c2b-170">Merhaba bölümünün toohello altına'e gidin ve seçin **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="d0c2b-171">Açılır pencere sahip hello Azure AD oturum açma sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="d0c2b-172">tooauthenticate, normal olarak kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="d0c2b-173">Azure AD geri döndürülen hello e-posta adresi iş yeri hesabı ile oturum açmış hello aynı hello olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="d0c2b-174">Merhaba test başarıyla tamamlandı, toohello alt hello sayfa seçin ve kaydırma **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="d0c2b-175">Çalışma alanına kullanan herkesin artık kimlik doğrulaması için Azure AD oturum açma sayfası sunulur.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="d0c2b-176">SAML oturum kapatma hello Azure AD oturum kapatma sayfasını kullanılan toopoint olabilir URL'si tooconfigure seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="d0c2b-177">Bu ayar etkin ve yapılandırılmış durumda olduğunda hello kullanıcı artık yönlendirilmiş toohello çalışma alanına oturum kapatma sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="d0c2b-178">Bunun yerine, hello kullanıcı hello SAML oturum kapatma yeniden yönlendirme ayarında eklenen yeniden yönlendirilen toohello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="d0c2b-179">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="d0c2b-180">Bu uygulamayı hello ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümünde, hello seçmeniz yeterlidir **çoklu oturum açma** sekmesi ve erişim hello Merhaba aracılığıyla belgelere katıştırılmış **yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0c2b-181">Daha fazla bilgiyi hello hello embedded belgeler özelliği hakkında [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="d0c2b-182">Yeniden kimlik doğrulamanın sıklığını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0c2b-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="d0c2b-183">SAML denetim, üç gün, her gün bir hafta, iki hafta, bir ay için çalışma alanına tooprompt yapılandırabilirsiniz ya da hiç.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="d0c2b-184">Merhaba mobil uygulamalar üzerinde hello SAML denetimi için en düşük değer ayarlanmış tooone hafta.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="d0c2b-185">Ayrıca, tüm kullanıcılar için sıfırlama SAML zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="d0c2b-186">toodo Bu, kullanım hello **şimdi gerektiren SAML kimlik doğrulaması tüm kullanıcılar için** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d0c2b-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0c2b-187">Create an Azure AD test user</span></span>
<span data-ttu-id="d0c2b-188">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

1. <span data-ttu-id="d0c2b-190">Merhaba, **Azure portal**, buna hello sol bölmesinde, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0c2b-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**seçip **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0c2b-194">tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0c2b-196">Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c2b-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0c2b-198">a.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-198">a.</span></span> <span data-ttu-id="d0c2b-199">Merhaba, **adı** metin kutusunda, **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0c2b-200">b.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-200">b.</span></span> <span data-ttu-id="d0c2b-201">Merhaba, **kullanıcı adı** metin kutusu, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0c2b-202">c.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-202">c.</span></span> <span data-ttu-id="d0c2b-203">Seçin **Göster parola**ve not edin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="d0c2b-204">d.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-204">d.</span></span> <span data-ttu-id="d0c2b-205">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="d0c2b-206">Facebook test kullanıcı tarafından bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0c2b-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="d0c2b-207">Bu bölümde, Britta Simon adlı bir kullanıcı tarafından Facebook çalışma alanında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="d0c2b-208">Çalışma alanına Facebook tarafından yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d0c2b-209">Bu bölümdeki hiçbir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-209">There is no action for you in this section.</span></span> <span data-ttu-id="d0c2b-210">Bir kullanıcı çalışma Facebook tarafından yoksa, yeni bir tooaccess çalışma alanına çalıştığınızda Facebook tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="d0c2b-211">Bir kullanıcı toocreate el ile gerekiyorsa hello başvurun [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d0c2b-212">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="d0c2b-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d0c2b-213">Bu bölümde, Facebook tarafından erişim tooWorkplace vererek Britta Simon toouse Azure SSO etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Kullanıcı atama][200] 

1. <span data-ttu-id="d0c2b-215">Hello Azure portal, açık hello uygulamaları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="d0c2b-216">Toohello dizin görünümüne gidin, çok Git**kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d0c2b-218">Merhaba uygulamalar listesinde **Facebook ile çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Merhaba uygulamalar listesinde Facebook bağlantısıyla Hello çalışma alanı](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="d0c2b-220">Merhaba soldaki Hello menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="d0c2b-222">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-222">Select **Add**.</span></span> <span data-ttu-id="d0c2b-223">Ardından hello **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="d0c2b-225">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="d0c2b-226">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **seçin**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="d0c2b-227">Merhaba, **eklemek atama** iletişim kutusunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d0c2b-228">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="d0c2b-228">Test single sign-on</span></span>

<span data-ttu-id="d0c2b-229">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="d0c2b-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="d0c2b-230">Daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d0c2b-231">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0c2b-231">Next steps</span></span>

* <span data-ttu-id="d0c2b-232">Merhaba bkz [nasıl öğreticiler listesi toointegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="d0c2b-233">Okuma [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="d0c2b-234">Hakkında daha fazla çok bilgi[kullanıcı sağlamayı Yapılandır](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d0c2b-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

