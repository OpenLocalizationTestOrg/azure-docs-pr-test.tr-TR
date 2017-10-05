---
title: "Öğretici: Azure Active Directory Tümleştirme Cerner orta ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Cerner Orta arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="a522f-103">Öğretici: Azure Active Directory Tümleştirme ile Cerner Orta</span><span class="sxs-lookup"><span data-stu-id="a522f-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="a522f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Cerner Orta tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a522f-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a522f-105">Cerner Orta Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a522f-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a522f-106">Cerner Orta erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a522f-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="a522f-107">Azure AD hesaplarına otomatik olarak Cerner Merkezi (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a522f-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a522f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a522f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a522f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a522f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a522f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a522f-110">Prerequisites</span></span>

<span data-ttu-id="a522f-111">Azure AD tümleştirme Cerner orta ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a522f-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="a522f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a522f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a522f-113">Onaylanan bir Cerner Merkezi sistem hesabı</span><span class="sxs-lookup"><span data-stu-id="a522f-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="a522f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a522f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a522f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a522f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a522f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a522f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a522f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a522f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a522f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a522f-118">Scenario description</span></span>
<span data-ttu-id="a522f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a522f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a522f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a522f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a522f-121">Galeriden Cerner Orta ekleme</span><span class="sxs-lookup"><span data-stu-id="a522f-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="a522f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a522f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="a522f-123">Galeriden Cerner Orta ekleme</span><span class="sxs-lookup"><span data-stu-id="a522f-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="a522f-124">Azure AD Cerner Orta tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Cerner Orta eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a522f-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a522f-125">**Galeriden Cerner Orta eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a522f-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a522f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a522f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a522f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a522f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a522f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a522f-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a522f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** düğmesi iletişim kutusunun en üstünde.</span><span class="sxs-lookup"><span data-stu-id="a522f-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a522f-133">Arama kutusuna **Cerner orta**.</span><span class="sxs-lookup"><span data-stu-id="a522f-133">In the search box, type **Cerner Central**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="a522f-135">Sonuçlar panelinde seçin **Cerner orta**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a522f-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a522f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a522f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a522f-138">Bu bölümde, yapılandırmanız ve Cerner orta ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="a522f-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a522f-139">Tekli çalışmaya oturum için Azure AD Cerner Orta karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a522f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="a522f-140">Diğer bir deyişle, bir Azure AD kullanıcısının Cerner Orta ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a522f-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="a522f-141">Yapılandırma ve Azure AD çoklu oturum açma Cerner orta ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a522f-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a522f-142">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a522f-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a522f-143">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="a522f-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a522f-144">**[Cerner Orta test kullanıcısı oluşturma](#creating-a-cerner-central-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Cerner Orta sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a522f-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="a522f-145">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a522f-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a522f-146">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a522f-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a522f-147">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a522f-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a522f-148">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Cerner Orta uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a522f-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="a522f-149">**Azure AD çoklu oturum açma Cerner orta ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a522f-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="a522f-150">Azure portalında üzerinde **Cerner orta** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a522f-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a522f-152">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a522f-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="a522f-154">Üzerinde **Cerner merkezi etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a522f-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="a522f-156">a.</span><span class="sxs-lookup"><span data-stu-id="a522f-156">a.</span></span> <span data-ttu-id="a522f-157">İçinde **tanımlayıcısı** metin kutusuna, aşağıdaki desenleri kullanarak değeri yazın:</span><span class="sxs-lookup"><span data-stu-id="a522f-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="a522f-158">b.</span><span class="sxs-lookup"><span data-stu-id="a522f-158">b.</span></span> <span data-ttu-id="a522f-159">İçinde **yanıt URL'si** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="a522f-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="a522f-160">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a522f-160">These values are not the real.</span></span> <span data-ttu-id="a522f-161">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a522f-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a522f-162">Kişi [Cerner Orta destek ekibi](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="a522f-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="a522f-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a522f-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="a522f-165">Oluşturulacak **meta veri** url, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a522f-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="a522f-166">a.</span><span class="sxs-lookup"><span data-stu-id="a522f-166">a.</span></span> <span data-ttu-id="a522f-167">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="a522f-167">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="a522f-169">b.</span><span class="sxs-lookup"><span data-stu-id="a522f-169">b.</span></span> <span data-ttu-id="a522f-170">Tıklatın **uç noktaları** açmak için **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a522f-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="a522f-172">c.</span><span class="sxs-lookup"><span data-stu-id="a522f-172">c.</span></span> <span data-ttu-id="a522f-173">Kopyalamak için Kopyala düğmesini tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a522f-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="a522f-175">d.</span><span class="sxs-lookup"><span data-stu-id="a522f-175">d.</span></span> <span data-ttu-id="a522f-176">Şimdi özellik sayfasına gidin **Cerner orta** ve kopyalama **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a522f-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="a522f-178">e.</span><span class="sxs-lookup"><span data-stu-id="a522f-178">e.</span></span> <span data-ttu-id="a522f-179">Oluştur **meta veri URL'sini** şu biçimi kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="a522f-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="a522f-180">Çoklu oturum açma yapılandırmak için **Cerner orta** yan, ihtiyacınız göndermek **meta veri URL'sini** için [Cerner Orta Destek](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="a522f-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="a522f-181">Tümleştirme tamamlamak için uygulama tarafında SSO yapılandırırlar.</span><span class="sxs-lookup"><span data-stu-id="a522f-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="a522f-182">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a522f-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a522f-183">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="a522f-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a522f-184">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a522f-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a522f-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a522f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="a522f-186">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a522f-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a522f-188">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a522f-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a522f-189">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a522f-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a522f-191">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a522f-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a522f-193">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a522f-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a522f-195">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a522f-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a522f-197">a.</span><span class="sxs-lookup"><span data-stu-id="a522f-197">a.</span></span> <span data-ttu-id="a522f-198">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a522f-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a522f-199">b.</span><span class="sxs-lookup"><span data-stu-id="a522f-199">b.</span></span> <span data-ttu-id="a522f-200">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="a522f-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a522f-201">c.</span><span class="sxs-lookup"><span data-stu-id="a522f-201">c.</span></span> <span data-ttu-id="a522f-202">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a522f-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a522f-203">d.</span><span class="sxs-lookup"><span data-stu-id="a522f-203">d.</span></span> <span data-ttu-id="a522f-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a522f-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="a522f-205">Cerner Orta test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a522f-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="a522f-206">**Cerner orta** uygulama tüm Federal Kimlik sağlayıcısından kimlik doğrulamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="a522f-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="a522f-207">Bir kullanıcı uygulama giriş sayfası oturum açamaz ise, Federasyon ve herhangi bir el ile sağlama gerek vardır.</span><span class="sxs-lookup"><span data-stu-id="a522f-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a522f-208">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a522f-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a522f-209">Bu bölümde, Britta Cerner Merkezi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a522f-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a522f-211">**Cerner Orta Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a522f-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="a522f-212">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a522f-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a522f-214">Uygulamalar listesinde **Cerner orta**.</span><span class="sxs-lookup"><span data-stu-id="a522f-214">In the applications list, select **Cerner Central**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="a522f-216">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a522f-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a522f-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a522f-218">Click **Add** button.</span></span> <span data-ttu-id="a522f-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a522f-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a522f-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a522f-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a522f-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a522f-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a522f-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a522f-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a522f-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a522f-224">Testing single sign-on</span></span>

<span data-ttu-id="a522f-225">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a522f-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a522f-226">Erişim paneli Cerner Orta parçasında tıklattığınızda, otomatik olarak Cerner Orta uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="a522f-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="a522f-227">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a522f-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a522f-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a522f-228">Additional resources</span></span>

* [<span data-ttu-id="a522f-229">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="a522f-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a522f-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a522f-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

