---
title: "Öğretici: Azure Active Directory Tümleştirme ile FileCloud | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FileCloud arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="770a1-103">Öğretici: Azure Active Directory Tümleştirme FileCloud ile</span><span class="sxs-lookup"><span data-stu-id="770a1-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="770a1-104">Bu öğreticide, bilgi nasıl toointegrate FileCloud Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="770a1-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="770a1-105">FileCloud Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="770a1-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="770a1-106">Erişim tooFileCloud sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="770a1-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="770a1-107">Kullanıcıların tooautomatically get açan tooFileCloud (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="770a1-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="770a1-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="770a1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="770a1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="770a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="770a1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="770a1-110">Prerequisites</span></span>

<span data-ttu-id="770a1-111">tooconfigure FileCloud ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="770a1-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="770a1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="770a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="770a1-113">Bir FileCloud çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="770a1-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="770a1-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="770a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="770a1-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="770a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="770a1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="770a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="770a1-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="770a1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="770a1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="770a1-118">Scenario description</span></span>
<span data-ttu-id="770a1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="770a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="770a1-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="770a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="770a1-121">Merhaba Galerisi'nden FileCloud ekleme</span><span class="sxs-lookup"><span data-stu-id="770a1-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="770a1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="770a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="770a1-123">Merhaba Galerisi'nden FileCloud ekleme</span><span class="sxs-lookup"><span data-stu-id="770a1-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="770a1-124">Azure AD'ye tooconfigure hello tümleştirme FileCloud, tooadd FileCloud hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="770a1-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="770a1-125">**tooadd FileCloud hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="770a1-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a1-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="770a1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="770a1-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="770a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="770a1-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="770a1-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="770a1-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="770a1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="770a1-133">Merhaba arama kutusuna yazın **FileCloud**seçin **FileCloud** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="770a1-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="770a1-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="770a1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="770a1-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FileCloud sınayın.</span><span class="sxs-lookup"><span data-stu-id="770a1-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="770a1-137">Tek toowork'ın oturum açma hangi hello karşılık gelen FileCloud içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="770a1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="770a1-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı FileCloud hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="770a1-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="770a1-139">Merhaba hello değeri FileCloud içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="770a1-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="770a1-140">tooconfigure ve FileCloud ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="770a1-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="770a1-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="770a1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="770a1-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="770a1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="770a1-143">**[FileCloud test kullanıcısı oluşturma](#create-a-filecloud-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir FileCloud içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="770a1-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="770a1-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="770a1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="770a1-145">**[Test çoklu oturum açma](#test-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="770a1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="770a1-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="770a1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="770a1-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma FileCloud uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="770a1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="770a1-148">**tooconfigure Azure AD çoklu oturum açma ile FileCloud, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="770a1-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a1-149">Hello hello üzerinde Azure portal'ın **FileCloud** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="770a1-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="770a1-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="770a1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="770a1-153">Merhaba üzerinde **FileCloud etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="770a1-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![FileCloud etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="770a1-155">a.</span><span class="sxs-lookup"><span data-stu-id="770a1-155">a.</span></span> <span data-ttu-id="770a1-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="770a1-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="770a1-157">b.</span><span class="sxs-lookup"><span data-stu-id="770a1-157">b.</span></span> <span data-ttu-id="770a1-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="770a1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="770a1-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="770a1-159">These values are not real.</span></span> <span data-ttu-id="770a1-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="770a1-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="770a1-161">Kişi [FileCloud istemci destek ekibi](mailto:support@codelathe.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="770a1-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="770a1-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="770a1-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="770a1-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="770a1-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="770a1-166">Merhaba üzerinde **FileCloud yapılandırma** 'yi tıklatın **yapılandırma FileCloud** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="770a1-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="770a1-167">Kopya hello **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="770a1-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![FileCloud yapılandırma](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="770a1-169">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour FileCloud Kiracı.</span><span class="sxs-lookup"><span data-stu-id="770a1-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="770a1-170">Merhaba sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="770a1-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Ayarları bölümü üzerinde uygulama yan](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="770a1-172">Tıklatın **SSO** Ayarlar bölümünde sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="770a1-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Tek üzerinde uygulama oturum açma sekmesi yan](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="770a1-174">Seçin **SAML** olarak **varsayılan SSO türü** üzerinde **çoklu oturum açma (SSO) ayarları** paneli.</span><span class="sxs-lookup"><span data-stu-id="770a1-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Çoklu oturum açma ayarları paneli üzerinde uygulama yan](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="770a1-176">Yapıştır **SAML varlık kimliği**, hello Azure portalından kopyalanan **IDP uç noktası URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="770a1-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![IDP uç noktası URL'si metin kutusu](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="770a1-178">Not Defteri'nde, kopyalama hello panonuza bu içerik, indirilen meta veri dosyasını açın ve toohello Yapıştır **IDP Meta veri** textbox üzerinde **SAML ayarları** paneli.</span><span class="sxs-lookup"><span data-stu-id="770a1-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Uygulama tarafında IDP Meta veri bölümü](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="770a1-180">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="770a1-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="770a1-181">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="770a1-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="770a1-182">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="770a1-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="770a1-183">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="770a1-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="770a1-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="770a1-184">Create an Azure AD test user</span></span>

<span data-ttu-id="770a1-185">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="770a1-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="770a1-187">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="770a1-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a1-188">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="770a1-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="770a1-190">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="770a1-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="770a1-192">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="770a1-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="770a1-194">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="770a1-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="770a1-196">a.</span><span class="sxs-lookup"><span data-stu-id="770a1-196">a.</span></span> <span data-ttu-id="770a1-197">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="770a1-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="770a1-198">b.</span><span class="sxs-lookup"><span data-stu-id="770a1-198">b.</span></span> <span data-ttu-id="770a1-199">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="770a1-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="770a1-200">c.</span><span class="sxs-lookup"><span data-stu-id="770a1-200">c.</span></span> <span data-ttu-id="770a1-201">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="770a1-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="770a1-202">d.</span><span class="sxs-lookup"><span data-stu-id="770a1-202">d.</span></span> <span data-ttu-id="770a1-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="770a1-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="770a1-204">FileCloud test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="770a1-204">Create a FileCloud test user</span></span>

<span data-ttu-id="770a1-205">Bu bölümde Hello amacı toocreate Britta Simon içinde FileCloud adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="770a1-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="770a1-206">FileCloud yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="770a1-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="770a1-207">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="770a1-207">There is no action item for you in this section.</span></span> <span data-ttu-id="770a1-208">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess FileCloud sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="770a1-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="770a1-209">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [FileCloud istemci destek ekibi](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="770a1-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="770a1-210">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="770a1-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="770a1-211">Bu bölümde, erişim tooFileCloud vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="770a1-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="770a1-213">**tooassign Britta Simon tooFileCloud hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="770a1-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a1-214">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="770a1-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="770a1-216">Merhaba uygulamalar listesinde **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="770a1-216">In hello applications list, select **FileCloud**.</span></span>

    ![Merhaba FileCloud bağlantı hello uygulamalar listesinde](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="770a1-218">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="770a1-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="770a1-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="770a1-220">Click **Add** button.</span></span> <span data-ttu-id="770a1-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="770a1-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="770a1-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="770a1-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="770a1-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="770a1-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="770a1-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="770a1-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="770a1-226">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="770a1-226">Test single sign-on</span></span>

<span data-ttu-id="770a1-227">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="770a1-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="770a1-228">Merhaba FileCloud hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour FileCloud uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="770a1-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="770a1-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="770a1-229">Additional resources</span></span>

* [<span data-ttu-id="770a1-230">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="770a1-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="770a1-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="770a1-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

