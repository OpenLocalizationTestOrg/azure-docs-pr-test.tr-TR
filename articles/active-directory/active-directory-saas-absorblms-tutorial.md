---
title: "Öğretici: Azure Active Directory Tümleştirme almak LMS ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve almak LMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="18b12-103">Öğretici: Azure Active Directory Tümleştirme almak LMS ile</span><span class="sxs-lookup"><span data-stu-id="18b12-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="18b12-104">Bu öğreticide, bilgi nasıl toointegrate Absorb LMS Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18b12-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18b12-105">Almak LMS Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="18b12-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18b12-106">Erişim tooAbsorb LMS sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="18b12-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="18b12-107">Kullanıcıların tooautomatically get açan tooAbsorb LMS (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="18b12-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18b12-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="18b12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18b12-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="18b12-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="18b12-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18b12-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18b12-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="18b12-111">Prerequisites</span></span>

<span data-ttu-id="18b12-112">tooconfigure almak LMS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="18b12-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="18b12-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="18b12-113">An Azure AD subscription</span></span>
- <span data-ttu-id="18b12-114">Bir almak LMS çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="18b12-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18b12-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="18b12-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18b12-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="18b12-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18b12-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="18b12-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18b12-118">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18b12-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18b12-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="18b12-119">Scenario description</span></span>
<span data-ttu-id="18b12-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="18b12-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18b12-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="18b12-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18b12-122">Merhaba Galerisi'nden almak LMS ekleme</span><span class="sxs-lookup"><span data-stu-id="18b12-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="18b12-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="18b12-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="18b12-124">Merhaba Galerisi'nden almak LMS ekleme</span><span class="sxs-lookup"><span data-stu-id="18b12-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="18b12-125">Merhaba tümleştirilmesi tooconfigure almak LMS tooAzure AD içinde tooadd Absorb LMS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="18b12-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18b12-126">**tooadd Absorb LMS hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18b12-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18b12-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="18b12-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="18b12-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18b12-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="18b12-130">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="18b12-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="18b12-134">Hello arama kutusuna yazın **almak LMS**seçin **almak LMS** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="18b12-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçlar listesinde LMS Al](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="18b12-136">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="18b12-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="18b12-137">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı LMS almak ile test etme</span><span class="sxs-lookup"><span data-stu-id="18b12-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="18b12-138">Tek toowork'ın oturum açma hangi hello karşılık gelen almak LMS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="18b12-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="18b12-139">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı almak LMS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="18b12-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="18b12-140">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** almak LMS içinde.</span><span class="sxs-lookup"><span data-stu-id="18b12-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="18b12-141">tooconfigure ve almak LMS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="18b12-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18b12-142">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="18b12-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18b12-143">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="18b12-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18b12-144">**[Bir almak LMS test kullanıcısı oluşturma](#create-an-absorb-lms-test-user)**  -toohave Britta Simon kapsamına bağlantılı toohello Azure AD kullanıcı gösterimidir LMS içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="18b12-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18b12-145">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="18b12-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18b12-146">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="18b12-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="18b12-147">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="18b12-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="18b12-148">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma almak LMS uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="18b12-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="18b12-149">**tooconfigure Azure AD çoklu oturum açma almak LMS ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18b12-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="18b12-150">Merhaba hello üzerinde Azure portal'ın **almak LMS** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="18b12-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="18b12-152">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="18b12-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="18b12-154">Merhaba üzerinde **LMS etki alanı almak ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="18b12-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![LMS etki alanı ve URL'leri tek oturum açma bilgilerini al](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="18b12-156">a.</span><span class="sxs-lookup"><span data-stu-id="18b12-156">a.</span></span> <span data-ttu-id="18b12-157">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="18b12-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="18b12-158">b.</span><span class="sxs-lookup"><span data-stu-id="18b12-158">b.</span></span> <span data-ttu-id="18b12-159">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="18b12-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="18b12-160">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="18b12-160">These values are not hello real.</span></span> <span data-ttu-id="18b12-161">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="18b12-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="18b12-162">Kişi [almak LMS istemci destek ekibi](https://www.absorblms.com/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="18b12-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="18b12-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="18b12-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="18b12-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-165">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="18b12-167">Merhaba üzerinde **almak LMS yapılandırma** 'yi tıklatın **almak LMS yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="18b12-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="18b12-168">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="18b12-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![LMS yapılandırma Al](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="18b12-170">Farklı web tarayıcısı penceresinde tooyour almak LMS şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="18b12-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="18b12-171">Merhaba tıklatın **hesabı simgesi** hello yönetici arabirimde.</span><span class="sxs-lookup"><span data-stu-id="18b12-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="18b12-173">Tıklatın **Portal ayarları**.</span><span class="sxs-lookup"><span data-stu-id="18b12-173">Click **Portal Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="18b12-175">Merhaba tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-175">Click hello **Users** tab.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="18b12-177">Yapılandırma alanları çoklu oturum açma adımları tooaccess hello izleyen hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="18b12-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="18b12-179">a.</span><span class="sxs-lookup"><span data-stu-id="18b12-179">a.</span></span> <span data-ttu-id="18b12-180">Select hello uygun **modu**.</span><span class="sxs-lookup"><span data-stu-id="18b12-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="18b12-181">b.</span><span class="sxs-lookup"><span data-stu-id="18b12-181">b.</span></span> <span data-ttu-id="18b12-182">Açık hello hello Not Defteri'nde, Azure Portalı'ndan indirilen sertifika kaldırmak hello **---başlangıç sertifika---** ve **---son SERTİFİKAYI---** etiketi ve içeriği kalan hello yapıştırın Merhaba **anahtar** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="18b12-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="18b12-183">c.</span><span class="sxs-lookup"><span data-stu-id="18b12-183">c.</span></span> <span data-ttu-id="18b12-184">Merhaba, **ID özelliği**, select hello hello (örneğin kullanıcı adı burada seçilen sonra hello userprinciplename Azure AD'de seçtiyseniz,.) Azure AD kullanıcı tanımlayıcısını hello olarak yapılandırılmış uygun özniteliği</span><span class="sxs-lookup"><span data-stu-id="18b12-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="18b12-185">d.</span><span class="sxs-lookup"><span data-stu-id="18b12-185">d.</span></span> <span data-ttu-id="18b12-186">Merhaba, **oturum açma URL'si**, hello yapıştırın **"SAML çoklu oturum açma hizmeti URL'si"** hello kopyalanıp değeri **yapılandırma oturum açma** hello Azure portalı penceresi.</span><span class="sxs-lookup"><span data-stu-id="18b12-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="18b12-187">e.</span><span class="sxs-lookup"><span data-stu-id="18b12-187">e.</span></span> <span data-ttu-id="18b12-188">Merhaba, **oturum kapatma URL'si**, hello yapıştırın **"Sign-Out URL"** hello kopyalanıp değeri **yapılandırma oturum açma** hello Azure portalı penceresi.</span><span class="sxs-lookup"><span data-stu-id="18b12-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="18b12-189">Etkinleştirme **'Yalnızca izin ver SSO oturum açma'**.</span><span class="sxs-lookup"><span data-stu-id="18b12-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="18b12-191">Tıklatın **"Kaydedin."**</span><span class="sxs-lookup"><span data-stu-id="18b12-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="18b12-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="18b12-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18b12-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="18b12-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18b12-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18b12-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="18b12-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18b12-195">Create an Azure AD test user</span></span>

<span data-ttu-id="18b12-196">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="18b12-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="18b12-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18b12-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18b12-199">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18b12-201">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="18b12-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18b12-203">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18b12-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18b12-205">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="18b12-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18b12-207">a.</span><span class="sxs-lookup"><span data-stu-id="18b12-207">a.</span></span> <span data-ttu-id="18b12-208">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18b12-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18b12-209">b.</span><span class="sxs-lookup"><span data-stu-id="18b12-209">b.</span></span> <span data-ttu-id="18b12-210">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="18b12-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18b12-211">c.</span><span class="sxs-lookup"><span data-stu-id="18b12-211">c.</span></span> <span data-ttu-id="18b12-212">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="18b12-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18b12-213">d.</span><span class="sxs-lookup"><span data-stu-id="18b12-213">d.</span></span> <span data-ttu-id="18b12-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="18b12-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="18b12-215">Bir almak LMS test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18b12-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="18b12-216">tooenable Azure AD kullanıcıların toolog tooAbsorb LMS'da, bunlar tooAbsorb LMS sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="18b12-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="18b12-217">LMS almak için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="18b12-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="18b12-218">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18b12-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="18b12-219">İçinde tooyour almak LMS şirket site yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="18b12-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="18b12-220">Tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-220">Click **Users** tab.</span></span>

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="18b12-222">Tıklatın **kullanıcılar** hello altında **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-222">Click **Users** under hello **Users** tab.</span></span>

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="18b12-224">Seçin **kullanıcı** gelen **yeni Ekle** açılır.</span><span class="sxs-lookup"><span data-stu-id="18b12-224">Select **User** from **Add New** drop-down.</span></span>

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="18b12-226">Merhaba üzerinde **Kullanıcı Ekle** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="18b12-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="18b12-228">a.</span><span class="sxs-lookup"><span data-stu-id="18b12-228">a.</span></span> <span data-ttu-id="18b12-229">Merhaba, **ad** metin kutusuna, türü hello ad Britta gibi.</span><span class="sxs-lookup"><span data-stu-id="18b12-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="18b12-230">b.</span><span class="sxs-lookup"><span data-stu-id="18b12-230">b.</span></span> <span data-ttu-id="18b12-231">Merhaba, **Soyadı** metin kutusuna, türü hello Soyadı Simon gibi.</span><span class="sxs-lookup"><span data-stu-id="18b12-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="18b12-232">c.</span><span class="sxs-lookup"><span data-stu-id="18b12-232">c.</span></span> <span data-ttu-id="18b12-233">Merhaba, **kullanıcıadı** metin kutusuna, Britta Simon gibi türü hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="18b12-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="18b12-234">d.</span><span class="sxs-lookup"><span data-stu-id="18b12-234">d.</span></span> <span data-ttu-id="18b12-235">Merhaba, **parola** metin kutusuna, Britta Simon hello parola türünde.</span><span class="sxs-lookup"><span data-stu-id="18b12-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="18b12-236">e.</span><span class="sxs-lookup"><span data-stu-id="18b12-236">e.</span></span> <span data-ttu-id="18b12-237">Merhaba, **parolayı onayla** metin kutusuna, türü hello aynı parola.</span><span class="sxs-lookup"><span data-stu-id="18b12-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="18b12-238">f.</span><span class="sxs-lookup"><span data-stu-id="18b12-238">f.</span></span> <span data-ttu-id="18b12-239">Olarak olun **etkin**.</span><span class="sxs-lookup"><span data-stu-id="18b12-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="18b12-240">Tıklatın **"Kaydedin."**</span><span class="sxs-lookup"><span data-stu-id="18b12-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="18b12-241">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="18b12-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="18b12-242">Bu bölümde, erişim tooAbsorb LMS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="18b12-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Merhaba kullanıcı rolü atayın][200]

<span data-ttu-id="18b12-244">**tooassign Britta Simon tooAbsorb LMS, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18b12-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="18b12-245">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="18b12-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="18b12-247">Merhaba uygulamalar listesinde **almak LMS**.</span><span class="sxs-lookup"><span data-stu-id="18b12-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![Merhaba almak LMS bağlantı hello uygulamalar listesinde](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="18b12-249">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="18b12-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="18b12-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18b12-251">Click **Add** button.</span></span> <span data-ttu-id="18b12-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18b12-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="18b12-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="18b12-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18b12-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18b12-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18b12-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18b12-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="18b12-257">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="18b12-257">Test single sign-on</span></span>

<span data-ttu-id="18b12-258">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="18b12-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18b12-259">Hello almak LMS döşeme hello erişim paneli tıklatın otomatik olarak oturum açma tooyour almak LMS uygulama alırsınız.</span><span class="sxs-lookup"><span data-stu-id="18b12-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="18b12-260">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="18b12-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18b12-261">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="18b12-261">Additional resources</span></span>

* [<span data-ttu-id="18b12-262">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="18b12-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18b12-263">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="18b12-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

