---
title: "Öğretici: Azure Active Directory Tümleştirme SilkRoad yaşam Suite ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SilkRoad yaşam Suite arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="5c382-103">Öğretici: Azure Active Directory Tümleştirme SilkRoad yaşam Suite ile</span><span class="sxs-lookup"><span data-stu-id="5c382-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="5c382-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate SilkRoad yaşam Suite Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c382-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="5c382-105">SilkRoad yaşam Suite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5c382-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="5c382-106">Erişim tooSilkRoad yaşam paketine sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5c382-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="5c382-107">Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooSilkRoad yaşam Suite çoklu oturum açma (SSO) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="5c382-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="5c382-108">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c382-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c382-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5c382-109">Prerequisites</span></span>
<span data-ttu-id="5c382-110">tooconfigure SilkRoad yaşam Suite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5c382-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="5c382-111">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5c382-111">An Azure AD subscription</span></span>
* <span data-ttu-id="5c382-112">Abonelik SilkRoad yaşam Suite SSO etkin</span><span class="sxs-lookup"><span data-stu-id="5c382-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="5c382-113">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5c382-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="5c382-114">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5c382-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5c382-115">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c382-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5c382-116">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c382-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="5c382-117">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5c382-117">Scenario Description</span></span>
<span data-ttu-id="5c382-118">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD SSO bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="5c382-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="5c382-119">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5c382-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c382-120">Merhaba Galerisi'nden SilkRoad yaşam paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="5c382-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="5c382-121">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="5c382-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="5c382-122">Merhaba Galerisi'nden SilkRoad yaşam paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="5c382-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="5c382-123">Azure AD'ye tooconfigure hello tümleştirme SilkRoad yaşam paketinin tooadd SilkRoad yaşam Suite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c382-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c382-124">**tooadd SilkRoad yaşam hello galeri paketinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5c382-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c382-125">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c382-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="5c382-127">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="5c382-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="5c382-128">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="5c382-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2]

4. <span data-ttu-id="5c382-130">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="5c382-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]

5. <span data-ttu-id="5c382-132">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5c382-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4]

6. <span data-ttu-id="5c382-134">Merhaba arama kutusuna yazın **SilkRoad yaşam Suite**.</span><span class="sxs-lookup"><span data-stu-id="5c382-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Uygulamalar][5]

7. <span data-ttu-id="5c382-136">Merhaba sonuçlar bölmesinde seçin **SilkRoad yaşam Suite**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5c382-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Uygulamalar][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5c382-138">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5c382-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5c382-139">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve test SilkRoad yaşam Suite ile Azure AD SSO temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="5c382-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c382-140">SSO toowork için Azure AD hangi hello karşılık gelen kullanıcı SilkRoad yaşam Suite tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c382-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="5c382-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve SilkRoad yaşam paketindeki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c382-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="5c382-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SilkRoad yaşam paketindeki.</span><span class="sxs-lookup"><span data-stu-id="5c382-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="5c382-143">tooconfigure ve SilkRoad yaşam Suite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5c382-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c382-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5c382-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c382-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5c382-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c382-146">**[SilkRoad yaşam Suite test kullanıcısı oluşturma](#creating-a-silkroad-life-suite-test-user)**  -toohave karşılık gelen, Britta Simon SilkRoad yaşam paketindeki, her bağlı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="5c382-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="5c382-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5c382-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c382-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5c382-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5c382-149">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5c382-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="5c382-150">Bu bölümde Hello amacı hello Klasik Azure portalı, Azure AD SSO tooenable ve tooconfigure SSO SilkRoad yaşam Suite uygulamanızda ' dir.</span><span class="sxs-lookup"><span data-stu-id="5c382-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="5c382-151">**Azure AD çoklu oturum açma tooconfigure SilkRoad yaşam Suite ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5c382-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c382-152">Yönetici olarak oturum açma tooyour SilkRoad şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="5c382-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="5c382-153">tooobtain erişim toohello Microsoft Azure AD ile Federasyon yapılandırma SilkRoad yaşam Suite kimlik doğrulaması uygulama SilkRoad desteği veya SilkRoad Hizmetleri temsilcinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="5c382-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="5c382-154">Çok Git**hizmet sağlayıcısı**ve ardından **Federasyon ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="5c382-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD çoklu oturum açma][10] 

3. <span data-ttu-id="5c382-156">Tıklatın **karşıdan Federasyon meta verileri**ve ardından hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5c382-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Azure AD çoklu oturum açma][11] 

4. <span data-ttu-id="5c382-158">Hello hello üzerinde Klasik Azure portalı içinde **SilkRoad yaşam Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5c382-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 

5. <span data-ttu-id="5c382-160">Merhaba üzerinde **nasıl tooSilkRoad yaşam paketi üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5c382-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][7] 

6. <span data-ttu-id="5c382-162">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD çoklu oturum açma][8]   
 1. <span data-ttu-id="5c382-164">Merhaba, **oturum üzerinde URL'si** metin kutusuna, kullanıcıların toosign üzerinde tooyour SilkRoad yaşam Suite site tarafından kullanılan türü hello URL'si (örn: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="5c382-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="5c382-165">İndirilen açık hello **Silkroad** meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="5c382-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="5c382-166">Merhaba bulun **AssertionConsumerService** etiketini ve kopyalama hello **konumu** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5c382-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Azure AD çoklu oturum açma][21] 
 4. <span data-ttu-id="5c382-168">Merhaba değeri hello yapıştırma **yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="5c382-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="5c382-169">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c382-169">Click **Next**.</span></span>

6. <span data-ttu-id="5c382-170">Merhaba üzerinde **çoklu oturum açma SilkRoad yaşam Suite yapılandırma** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Azure AD çoklu oturum açma][9]  
 1. <span data-ttu-id="5c382-172">İndirme sertifikası'nı tıklatın ve ardından hello dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5c382-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="5c382-173">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c382-173">Click **Next**.</span></span>

7. <span data-ttu-id="5c382-174">İçinde **SilkRoad** uygulama tıklatın **kimlik doğrulaması kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="5c382-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD çoklu oturum açma][12] 

8. <span data-ttu-id="5c382-176">Tıklatın **kimlik doğrulaması kaynağı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5c382-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD çoklu oturum açma][13] 

9. <span data-ttu-id="5c382-178">Merhaba, **kimlik doğrulaması kaynağı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Azure AD çoklu oturum açma][14]  
 1. <span data-ttu-id="5c382-180">Altında **seçeneği 2 - meta veri dosyası**, tıklatın **Gözat** tooupload hello meta veri dosyası indirilir.</span><span class="sxs-lookup"><span data-stu-id="5c382-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="5c382-181">Tıklatın **kimlik dosya verilerini kullanarak sağlayıcısı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5c382-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="5c382-182">Merhaba, **kimlik doğrulaması kaynakları** 'yi tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="5c382-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD çoklu oturum açma][15] 

11. <span data-ttu-id="5c382-184">Merhaba üzerinde **kimlik doğrulaması kaynağını Düzenle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Azure AD çoklu oturum açma][16] 
 1. <span data-ttu-id="5c382-186">Olarak **etkin**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="5c382-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="5c382-187">Merhaba, **IDP açıklama** metin kutusuna, yapılandırmanız için bir açıklama yazın (örneğin: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="5c382-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="5c382-188">Merhaba, **IDP adı** metin kutusuna, belirli tooyour yapılandırma adını yazın (örneğin: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="5c382-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="5c382-189">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c382-189">Click **Save**.</span></span>

12. <span data-ttu-id="5c382-190">Diğer tüm kimlik doğrulaması kaynakları devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="5c382-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD çoklu oturum açma][17]

13. <span data-ttu-id="5c382-192">Merhaba hello üzerinde Klasik Azure portalı içinde **tek oturum açma onay** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5c382-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD çoklu oturum açma][18]

14. <span data-ttu-id="5c382-194">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="5c382-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD çoklu oturum açma][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5c382-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c382-196">Create an Azure AD test user</span></span>
<span data-ttu-id="5c382-197">Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5c382-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="5c382-199">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5c382-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c382-200">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c382-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="5c382-202">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="5c382-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="5c382-203">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5c382-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c382-205">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5c382-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="5c382-207">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="5c382-209">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="5c382-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="5c382-210">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c382-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="5c382-211">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c382-211">Click **Next**.</span></span>

6. <span data-ttu-id="5c382-212">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="5c382-214">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5c382-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="5c382-215">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c382-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="5c382-216">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c382-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="5c382-217">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="5c382-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="5c382-218">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c382-218">Click **Next**.</span></span>

7. <span data-ttu-id="5c382-219">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5c382-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="5c382-221">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5c382-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="5c382-223">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="5c382-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="5c382-224">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c382-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="5c382-225">SilkRoad yaşam Suite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c382-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="5c382-226">Bu bölümde Hello amacı toocreate Britta Simon SilkRoad yaşam paketindeki adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="5c382-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="5c382-227">Britta'nın bir SSO kimliği olmalıdır (bazen tooas başvurulan bir *AuthParam*) Britta'nın eşleşen **emailaddress** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="5c382-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="5c382-228">**toocreate Britta Simon SilkRoad yaşam paketindeki adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5c382-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="5c382-229">SilkRoad yaşam Suite Destek Ekibi toocreate sahip bir kullanıcıya sor **SSO kimliği** aynı değer hello özniteliği hello **emailaddress** Britta Simon Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="5c382-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5c382-230">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="5c382-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="5c382-231">Merhaba amacı, bu bölümde, kendi erişim tooSilkRoad yaşam Suite vererek tooenable Britta Simon toouse Azure SSO olur.</span><span class="sxs-lookup"><span data-stu-id="5c382-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5c382-233">**tooassign Britta Simon tooSilkRoad yaşam Suite hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5c382-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c382-234">Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="5c382-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5c382-236">Merhaba uygulamalar listesinde **SilkRoad yaşam Suite**.</span><span class="sxs-lookup"><span data-stu-id="5c382-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Kullanıcı atama][202] 

3. <span data-ttu-id="5c382-238">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5c382-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203] 

4. <span data-ttu-id="5c382-240">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c382-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="5c382-241">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="5c382-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="5c382-243">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="5c382-243">Test single sign-on</span></span>
<span data-ttu-id="5c382-244">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5c382-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5c382-245">Merhaba SilkRoad yaşam Suite hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SilkRoad yaşam paketi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c382-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c382-246">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5c382-246">Additional Resources</span></span>
* [<span data-ttu-id="5c382-247">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5c382-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c382-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5c382-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





