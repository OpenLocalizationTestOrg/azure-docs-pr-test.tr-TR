---
title: "Öğretici: Azure Active Directory Tümleştirme Qlik algılama kuruluş ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Qlik algılama kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="75256-103">Öğretici: Azure Active Directory Tümleştirme Qlik algılama kuruluş ile</span><span class="sxs-lookup"><span data-stu-id="75256-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="75256-104">Bu öğreticide, bilgi nasıl toointegrate Qlik algılama kuruluş Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75256-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75256-105">Qlik algılama kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="75256-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="75256-106">Erişim tooQlik algılama Kurumsal sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75256-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="75256-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooQlik algılama Enterprise (çoklu oturum açma) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75256-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="75256-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="75256-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="75256-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75256-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75256-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="75256-110">Prerequisites</span></span>

<span data-ttu-id="75256-111">tooconfigure Qlik algılama Kurumsal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="75256-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="75256-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="75256-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75256-113">Bir Qlik algılama Kurumsal çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="75256-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75256-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="75256-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75256-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="75256-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75256-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="75256-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75256-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75256-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75256-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="75256-118">Scenario description</span></span>
<span data-ttu-id="75256-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="75256-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75256-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="75256-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75256-121">Merhaba Galerisi'nden Qlik algılama Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="75256-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="75256-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="75256-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="75256-123">Merhaba Galerisi'nden Qlik algılama Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="75256-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="75256-124">Azure AD'ye tooconfigure hello tümleştirme Qlik algılama Enterprise tooadd Qlik algılama Kurumsal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="75256-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="75256-125">**tooadd Qlik algılama Kurumsal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75256-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="75256-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="75256-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="75256-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="75256-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="75256-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="75256-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="75256-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="75256-133">Hello arama kutusuna yazın **Qlik algılama Kurumsal**seçin **Qlik algılama Kurumsal** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="75256-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Qlik algılama Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="75256-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="75256-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="75256-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Qlik algılama "Britta Simon" adlı bir test kullanıcı tabanlı kuruluş ile test etme.</span><span class="sxs-lookup"><span data-stu-id="75256-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75256-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Qlik algılama kuruluştaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="75256-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="75256-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Qlik algılama kuruluştaki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="75256-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="75256-139">Merhaba hello değeri Qlik algılama kuruluşta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="75256-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="75256-140">tooconfigure ve Qlik algılama kuruluş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="75256-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="75256-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="75256-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="75256-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="75256-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75256-143">**[Qlik algılama Kurumsal test kullanıcısı oluşturma](#create-a-qlik-sense-enterprise-test-user)**  -toohave karşılık gelen, Britta Simon Qlik algılama kuruluşta, kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="75256-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="75256-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="75256-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75256-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="75256-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="75256-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="75256-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="75256-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Qlik algılama Kurumsal uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="75256-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="75256-148">**Azure AD çoklu oturum açma tooconfigure Qlik algılama kuruluş ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75256-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="75256-149">Merhaba hello üzerinde Azure portal'ın **Qlik algılama Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="75256-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="75256-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="75256-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="75256-153">Merhaba üzerinde **Qlik algılama kuruluş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="75256-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Qlik algılama kuruluş etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="75256-155">a.</span><span class="sxs-lookup"><span data-stu-id="75256-155">a.</span></span> <span data-ttu-id="75256-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="75256-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="75256-157">Sondaki eğik çizgi bu URI hello sonunda hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75256-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="75256-158">Gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="75256-158">It is required.</span></span>
    
    <span data-ttu-id="75256-159">b.</span><span class="sxs-lookup"><span data-stu-id="75256-159">b.</span></span> <span data-ttu-id="75256-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="75256-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="75256-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="75256-161">These values are not real.</span></span> <span data-ttu-id="75256-162">Bu değerleri ile Merhaba gerçek oturum açma URL'si ve tanımlayıcı, daha sonra Bu öğreticide veya kişi açıklanacak güncelleştirme [Qlik algılama Kurumsal İstemci destek ekibi](https://www.qlik.com/us/services/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="75256-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="75256-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="75256-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="75256-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-165">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75256-167">Böylece bu tooQlik algılama sunucu yükleyebilirsiniz hello Federasyon meta veri XML dosyasını hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="75256-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="75256-168">Merhaba IDP meta veri toohello Qlik algılama sunucu karşıya yüklemeden önce hello dosyasının düzenlenen toobe tooremove bilgi tooensure düzgün çalışmasını Azure AD arasında gerekir ve Qlik algılama sunucu.</span><span class="sxs-lookup"><span data-stu-id="75256-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="75256-170">a.</span><span class="sxs-lookup"><span data-stu-id="75256-170">a.</span></span> <span data-ttu-id="75256-171">Bir metin düzenleyicisinde Azure portalından indirmiş hello FederationMetaData.xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="75256-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="75256-172">b.</span><span class="sxs-lookup"><span data-stu-id="75256-172">b.</span></span> <span data-ttu-id="75256-173">Merhaba değeri için arama **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="75256-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="75256-174">Dört girdi (açma ve kapatma öğesi etiketleri iki çiftleri) vardır.</span><span class="sxs-lookup"><span data-stu-id="75256-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="75256-175">c.</span><span class="sxs-lookup"><span data-stu-id="75256-175">c.</span></span> <span data-ttu-id="75256-176">Merhaba RoleDescriptor etiketleri ve tüm bilgileri arasında hello dosyadan silin.</span><span class="sxs-lookup"><span data-stu-id="75256-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="75256-177">d.</span><span class="sxs-lookup"><span data-stu-id="75256-177">d.</span></span> <span data-ttu-id="75256-178">Merhaba dosyasını kaydedin ve yakındaki bu belgenin sonraki bölümlerinde kullanmak için saklayın.</span><span class="sxs-lookup"><span data-stu-id="75256-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="75256-179">Sanal proxy yapılandırmaları oluşturabilirsiniz bir kullanıcı olarak toohello Qlik algılama Qlik Yönetim Konsolu (QMC) gidin.</span><span class="sxs-lookup"><span data-stu-id="75256-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="75256-180">Hello QMC, üzerinde hello tıklatın **sanal proxy'leri** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="75256-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="75256-182">Merhaba ekranında Hello altındaki hello tıklatın **Yeni Oluştur** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="75256-184">Merhaba sanal proxy düzenleme ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75256-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="75256-185">Merhaba üzerinde Merhaba ekranında sağ tarafında yapılandırma seçenekleri görünür yapmak için bir menü ' dir.</span><span class="sxs-lookup"><span data-stu-id="75256-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="75256-187">Kimlik menü seçeneğini işaretli hello ile Merhaba hello Azure sanal proxy yapılandırması için tanımlayıcı bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="75256-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="75256-189">a.</span><span class="sxs-lookup"><span data-stu-id="75256-189">a.</span></span> <span data-ttu-id="75256-190">Merhaba **açıklama** hello sanal proxy yapılandırması için bir kolay ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="75256-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="75256-191">Bir değer için bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="75256-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="75256-192">b.</span><span class="sxs-lookup"><span data-stu-id="75256-192">b.</span></span> <span data-ttu-id="75256-193">Merhaba **önek** alan Azure AD çoklu oturum açma ile tooQlik algılama bağlamak için hello sanal proxy uç nokta tanımlar.</span><span class="sxs-lookup"><span data-stu-id="75256-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="75256-194">Bu sanal proxy için bir benzersiz önek adı girin.</span><span class="sxs-lookup"><span data-stu-id="75256-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="75256-195">c.</span><span class="sxs-lookup"><span data-stu-id="75256-195">c.</span></span> <span data-ttu-id="75256-196">**Oturum etkin olmama zaman aşımı (dakika)** hello zaman aşımı değeri bu sanal proxy üzerinden bağlantıları için.</span><span class="sxs-lookup"><span data-stu-id="75256-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="75256-197">d.</span><span class="sxs-lookup"><span data-stu-id="75256-197">d.</span></span> <span data-ttu-id="75256-198">Merhaba **oturum tanımlama bilgisi üstbilgisi adı** olan kullanıcı Qlik algılama oturumu alır başarılı kimlik doğrulamasından sonra hello için oturum tanımlayıcısı hello hello tanımlama bilgisi adı depolama.</span><span class="sxs-lookup"><span data-stu-id="75256-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="75256-199">Bu ad benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="75256-199">This name must be unique.</span></span>

12. <span data-ttu-id="75256-200">Merhaba kimlik doğrulaması menü seçeneği toomake üzerinde görünür tıklatın.</span><span class="sxs-lookup"><span data-stu-id="75256-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="75256-201">Merhaba kimlik doğrulama ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75256-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="75256-203">a.</span><span class="sxs-lookup"><span data-stu-id="75256-203">a.</span></span> <span data-ttu-id="75256-204">Merhaba **anonim erişim modu** açılan belirler anonim kullanıcılar hello sanal proxy üzerinden Qlik algılama erişimi.</span><span class="sxs-lookup"><span data-stu-id="75256-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="75256-205">Anonim kullanıcı Hello varsayılan seçenektir.</span><span class="sxs-lookup"><span data-stu-id="75256-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="75256-206">b.</span><span class="sxs-lookup"><span data-stu-id="75256-206">b.</span></span> <span data-ttu-id="75256-207">Merhaba **kimlik doğrulama yöntemini** açılan belirler hello kimlik doğrulama düzeni hello sanal proxy kullanır.</span><span class="sxs-lookup"><span data-stu-id="75256-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="75256-208">SAML hello aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="75256-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="75256-209">Daha fazla seçenek sonuç olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="75256-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="75256-210">c.</span><span class="sxs-lookup"><span data-stu-id="75256-210">c.</span></span> <span data-ttu-id="75256-211">Merhaba, **SAML konak URI alan**, giriş hello hostname kullanıcılar bu SAML sanal proxy üzerinden tooaccess Qlik algılama girin.</span><span class="sxs-lookup"><span data-stu-id="75256-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="75256-212">Merhaba ana hello Qlik algılama sunucu hello URI'sini adıdır.</span><span class="sxs-lookup"><span data-stu-id="75256-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="75256-213">d.</span><span class="sxs-lookup"><span data-stu-id="75256-213">d.</span></span> <span data-ttu-id="75256-214">Merhaba, **SAML varlık kimliği**, hello girilen hello SAML konak URI alanı için aynı değeri girin.</span><span class="sxs-lookup"><span data-stu-id="75256-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="75256-215">e.</span><span class="sxs-lookup"><span data-stu-id="75256-215">e.</span></span> <span data-ttu-id="75256-216">Merhaba **SAML IDP meta veri** önceki hello düzenlenebilir hello dosyası **Düzenle Federasyon meta verilerini Azure AD yapılandırma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="75256-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="75256-217">**Merhaba IDP meta veriler karşıya yüklemeden önce hello dosyasının düzenlenen toobe gerekir** tooremove bilgi tooensure düzgün çalışmasını Azure AD arasında ve Qlik algılama sunucu.</span><span class="sxs-lookup"><span data-stu-id="75256-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="75256-218">**Lütfen yukarıdaki toohello yönergeleri hello dosyanın henüz toobe düzenlenebilir bakın.**</span><span class="sxs-lookup"><span data-stu-id="75256-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="75256-219">Merhaba dosyayı düzenlerseniz hello Gözat düğmesi ve select hello düzenlenen meta veri dosyası tooupload toohello sanal proxy yapılandırması tıklatın.</span><span class="sxs-lookup"><span data-stu-id="75256-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="75256-220">f.</span><span class="sxs-lookup"><span data-stu-id="75256-220">f.</span></span> <span data-ttu-id="75256-221">Merhaba temsil eden hello SAML öznitelik için Hello öznitelik adı veya şema başvurusu girin **UserID** Azure AD toohello Qlik algılama sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="75256-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="75256-222">Şema başvurusu bilgileri hello Azure uygulaması ekranlar post yapılandırmada kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75256-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="75256-223">toouse hello name özniteliği girin `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="75256-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="75256-224">g.</span><span class="sxs-lookup"><span data-stu-id="75256-224">g.</span></span> <span data-ttu-id="75256-225">Merhaba Hello değeri girin **kullanıcı dizini** , olacaktır ekli toousers tooQlik algılama sunucusu aracılığıyla Azure AD kimlik doğrulaması sırasında.</span><span class="sxs-lookup"><span data-stu-id="75256-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="75256-226">Sabit kodlanmış değerler arasına, tarafından **köşeli ayraçlar []**.</span><span class="sxs-lookup"><span data-stu-id="75256-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="75256-227">Bu metin kutusunda toouse hello Azure AD SAML onayı gönderilen bir öznitelik girin hello hello özniteliğin adını **olmadan** köşeli ayraç.</span><span class="sxs-lookup"><span data-stu-id="75256-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="75256-228">h.</span><span class="sxs-lookup"><span data-stu-id="75256-228">h.</span></span> <span data-ttu-id="75256-229">Merhaba **SAML imzalama algoritmasını** kümeleri hello hello sanal proxy yapılandırması için imzalama hizmet sağlayıcısı (Server'daki bu servis talebi Qlik algılama) sertifikası.</span><span class="sxs-lookup"><span data-stu-id="75256-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="75256-230">Qlik algılama sunucusu Microsoft Gelişmiş RSA ve AES şifreleme sağlayıcısı kullanılarak oluşturulan güvenilen bir sertifika kullanıyorsa, hello SAML imzalama algoritmasını çok değiştirmek**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="75256-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="75256-231">ı.</span><span class="sxs-lookup"><span data-stu-id="75256-231">i.</span></span> <span data-ttu-id="75256-232">Merhaba SAML özniteliği eşleme bölümüne güvenlik kuralları kullanmak için grupları gönderilen toobe tooQlik algılama gibi ek özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="75256-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="75256-233">Tıklatın hello üzerinde **yük DENGELEME** menü seçeneği toomake onu görünür.</span><span class="sxs-lookup"><span data-stu-id="75256-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="75256-234">Merhaba Yük Dengeleme ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75256-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="75256-236">Merhaba üzerinde tıklatın **Ekle yeni sunucu düğümü** düğmesini tıklatın, select altyapısı düğüm veya düğümler Qlik algılama amacıyla oturumları toofor dengelemesini gönderir ve Başlangıç'ı tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="75256-238">Merhaba Gelişmiş menü seçeneği toomake üzerinde görünür tıklatın.</span><span class="sxs-lookup"><span data-stu-id="75256-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="75256-239">Merhaba Gelişmiş ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75256-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="75256-241">Merhaba konak beyaz liste toohello Qlik algılama sunucusuna bağlanırken kabul ana bilgisayar adlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="75256-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="75256-242">**Kullanıcıların tooQlik algılama sunucusu bağlanırken belirteceği hello ana bilgisayar adı girin.**</span><span class="sxs-lookup"><span data-stu-id="75256-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="75256-243">Merhaba ana bilgisayar adı olan hello SAML konak URI hello https:// olmadan hello gibi aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="75256-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="75256-244">Merhaba tıklatın **Uygula** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="75256-246">Bağlantılı toohello sanal proxy başlatılacak proxy'leri bildiren Tamam tooaccept hello uyarı iletisi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75256-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="75256-248">Merhaba sağ tarafında Merhaba ekranında, hello ilişkili öğeler menüsü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75256-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="75256-249">Tıklatın hello üzerinde **proxy'leri** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="75256-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="75256-251">Merhaba proxy ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75256-251">hello proxy screen appears.</span></span>  <span data-ttu-id="75256-252">Merhaba tıklatın **bağlantı** hello alt toolink sırasında bir proxy toohello sanal proxy düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="75256-254">Bu sanal proxy bağlantı desteklemek ve hello tıklatın select hello proxy düğümü **bağlantı** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="75256-255">Bağladıktan sonra hello proxy ilişkili proxy'leri altında listelenir.</span><span class="sxs-lookup"><span data-stu-id="75256-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="75256-258">Sonra yaklaşık beş tooten saniye, hello yenileme QMC iletisi görünür.</span><span class="sxs-lookup"><span data-stu-id="75256-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="75256-259">Merhaba tıklatın **yenileme QMC** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="75256-261">Merhaba QMC yenilendiğinde hello üzerinde tıklatın **sanal proxy'leri** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="75256-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="75256-262">Merhaba yeni SAML sanal proxy giriş Merhaba ekranında hello tablosundaki listelenir.</span><span class="sxs-lookup"><span data-stu-id="75256-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="75256-263">Merhaba sanal proxy girişini tek tıklatın.</span><span class="sxs-lookup"><span data-stu-id="75256-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="75256-265">Merhaba ekranında Hello altındaki hello karşıdan SP meta verileri düğmesi etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="75256-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="75256-266">Merhaba tıklatın **karşıdan SP meta veri** düğmesini toosave hello meta veri tooa dosyası.</span><span class="sxs-lookup"><span data-stu-id="75256-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="75256-268">Açık hello sp meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="75256-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="75256-269">Merhaba gözlemlemek **Entityıd** girişi ve hello **AssertionConsumerService** girişi.</span><span class="sxs-lookup"><span data-stu-id="75256-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="75256-270">Bu değerler eşdeğer toohello **tanımlayıcısı** ve hello **URL üzerinde oturum** hello Azure AD uygulama yapılandırmasında.</span><span class="sxs-lookup"><span data-stu-id="75256-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="75256-271">Bu değerleri hello yapıştırmak **Qlik algılama kuruluş etki alanı ve URL'leri** hello Azure AD uygulaması Yapılandırma Sihirbazı'nda değiştirmelisiniz sonra bunlar, eşleşen değil, hello Azure AD uygulama yapılandırma bölümünde.</span><span class="sxs-lookup"><span data-stu-id="75256-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="75256-273">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="75256-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="75256-274">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="75256-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="75256-275">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75256-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75256-276">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75256-276">Create an Azure AD test user</span></span>
<span data-ttu-id="75256-277">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="75256-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="75256-279">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75256-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="75256-280">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="75256-282">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="75256-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="75256-284">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="75256-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![Merhaba Ekle düğmesi](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="75256-286">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="75256-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="75256-288">a.</span><span class="sxs-lookup"><span data-stu-id="75256-288">a.</span></span> <span data-ttu-id="75256-289">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75256-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="75256-290">b.</span><span class="sxs-lookup"><span data-stu-id="75256-290">b.</span></span> <span data-ttu-id="75256-291">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="75256-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="75256-292">c.</span><span class="sxs-lookup"><span data-stu-id="75256-292">c.</span></span> <span data-ttu-id="75256-293">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="75256-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="75256-294">d.</span><span class="sxs-lookup"><span data-stu-id="75256-294">d.</span></span> <span data-ttu-id="75256-295">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75256-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="75256-296">Qlik algılama Kurumsal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75256-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="75256-297">Bu bölümde, Britta Simon Qlik algılama kuruluşta adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75256-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="75256-298">Çalışmak [Qlik algılama Kurumsal İstemci destek ekibi](https://www.qlik.com/us/services/support) hello Qlik algılama Kurumsal platformunda hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="75256-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="75256-299">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="75256-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="75256-300">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="75256-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="75256-301">Bu bölümde, erişim tooQlik algılama Kurumsal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75256-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="75256-303">**tooassign Britta Simon tooQlik algılama Kurumsal hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="75256-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="75256-304">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="75256-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="75256-306">Merhaba uygulamalar listesinde **Qlik algılama Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="75256-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Merhaba Qlik algılama Kurumsal bağlantı hello uygulamalar listesinde](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="75256-308">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="75256-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="75256-310">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75256-310">Click **Add** button.</span></span> <span data-ttu-id="75256-311">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75256-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="75256-313">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="75256-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="75256-314">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75256-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75256-315">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="75256-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="75256-316">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="75256-316">Test single sign-on</span></span>

<span data-ttu-id="75256-317">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="75256-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="75256-318">Merhaba Qlik algılama Kurumsal hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Qlik algılama Kurumsal uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="75256-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="75256-319">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="75256-319">Additional resources</span></span>

* [<span data-ttu-id="75256-320">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="75256-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75256-321">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="75256-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

