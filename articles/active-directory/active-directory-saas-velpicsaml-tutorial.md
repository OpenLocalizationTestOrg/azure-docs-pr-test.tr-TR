---
title: "Öğretici: Azure Active Directory Tümleştirme Velpic SAML ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Velpic SAML arasında yapılandırmayı öğrenin."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="a43e3-103">Öğretici: Azure Active Directory Tümleştirme Velpic SAML ile</span><span class="sxs-lookup"><span data-stu-id="a43e3-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="a43e3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Velpic SAML tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a43e3-105">Azure AD ile Velpic SAML tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a43e3-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a43e3-106">Velpic SAML erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a43e3-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="a43e3-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Velpic SAML açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a43e3-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a43e3-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="a43e3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="a43e3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a43e3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a43e3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a43e3-110">Prerequisites</span></span>

<span data-ttu-id="a43e3-111">Azure AD tümleştirme Velpic SAML ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a43e3-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="a43e3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a43e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a43e3-113">Bir Velpic SAML çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a43e3-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a43e3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a43e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a43e3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a43e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a43e3-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a43e3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a43e3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a43e3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a43e3-118">Scenario description</span></span>
<span data-ttu-id="a43e3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a43e3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a43e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a43e3-121">Galeriden Velpic SAML ekleme</span><span class="sxs-lookup"><span data-stu-id="a43e3-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="a43e3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a43e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="a43e3-123">Galeriden Velpic SAML ekleme</span><span class="sxs-lookup"><span data-stu-id="a43e3-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="a43e3-124">Azure AD Velpic SAML tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Velpic SAML eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a43e3-125">**Galeriden Velpic SAML eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a43e3-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a43e3-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a43e3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a43e3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a43e3-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a43e3-133">Arama kutusuna **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-133">In the search box, type **Velpic SAML**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="a43e3-135">Sonuçlar panelinde seçin **Velpic SAML**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a43e3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a43e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a43e3-138">Bu bölümde, yapılandırmanız ve Velpic SAML ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="a43e3-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a43e3-139">Tekli çalışmaya oturum için Azure AD Velpic SAML karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a43e3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="a43e3-140">Diğer bir deyişle, bir Azure AD kullanıcısının Velpic SAML ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="a43e3-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Velpic SAML içinde.</span><span class="sxs-lookup"><span data-stu-id="a43e3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="a43e3-142">Yapılandırma ve Azure AD çoklu oturum açma Velpic SAML ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a43e3-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a43e3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a43e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a43e3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="a43e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a43e3-145">**[Velpic SAML test kullanıcısı oluşturma](#creating-a-velpic-saml-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Velpic SAML sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="a43e3-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a43e3-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a43e3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a43e3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a43e3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a43e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a43e3-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Velpic SAML uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="a43e3-150">**Azure AD çoklu oturum açma Velpic SAML ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a43e3-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="a43e3-151">Azure Yönetim Portalı'nda üzerinde **Velpic SAML** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a43e3-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a43e3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="a43e3-155">Ayrıntılar girin **Velpic SAML etki alanı ve URL'leri** bölüm -</span><span class="sxs-lookup"><span data-stu-id="a43e3-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="a43e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="a43e3-157">a.</span></span> <span data-ttu-id="a43e3-158">İçinde **oturum açma URL'si** metin değeri olarak yazın:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="a43e3-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="a43e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="a43e3-159">b.</span></span> <span data-ttu-id="a43e3-160">İçinde **tanımlayıcısı** metin kutusuna, Yapıştır **'Çoklu oturum açma URL'si'** değeri`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="a43e3-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a43e3-161">Oturum açma URL'si Velpic SAML ekibi tarafından sağlanacak ve tanımlayıcı değeri Velpic SAML tarafında SSO eklentisi yapılandırırken kullanılabilecek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="a43e3-162">Bu değer Velpic SAML uygulama sayfadan kopyalayın ve burada yapıştırın gerekir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="a43e3-163">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="a43e3-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a43e3-167">Velpic SAML yapılandırma bölümünde Velpic SAML yapılandırma oturum açma penceresini açmak için Yapılandır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="a43e3-168">SAML varlık kimliği hızlı başvuru bölümünden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="a43e3-169">Farklı web tarayıcısı penceresinde Velpic SAML şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="a43e3-170">Tıklayın **Yönet** sekmesinde ve Git **tümleştirme** tıklayın gereken bölüm **eklentileri** oturum açmak için yeni eklenti oluşturmak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="a43e3-172">Tıklayın **'Eklenti ekleme'** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="a43e3-174">Tıklayın **SAML** döşeme eklentisi ekleyin sayfasında.</span><span class="sxs-lookup"><span data-stu-id="a43e3-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="a43e3-176">Yeni SAML eklentisini adını girin ve tıklayın **'Ekle'** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="a43e3-178">Ayrıntılar aşağıdaki gibi girin:</span><span class="sxs-lookup"><span data-stu-id="a43e3-178">Enter the details as follows:</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="a43e3-180">a.</span><span class="sxs-lookup"><span data-stu-id="a43e3-180">a.</span></span> <span data-ttu-id="a43e3-181">İçinde **adı** metin kutusuna, SAML eklentisini adını yazın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="a43e3-182">b.</span><span class="sxs-lookup"><span data-stu-id="a43e3-182">b.</span></span> <span data-ttu-id="a43e3-183">İçinde **veren URL'si** metin kutusuna, Yapıştır **SAML varlık kimliği** , kopyalanan **yapılandırma oturum açma** Azure portalının penceresi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="a43e3-184">c.</span><span class="sxs-lookup"><span data-stu-id="a43e3-184">c.</span></span> <span data-ttu-id="a43e3-185">İçinde **sağlayıcısı meta verileri yapılandırma** Azure Portalı'ndan indirilen meta veri XML dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="a43e3-186">d.</span><span class="sxs-lookup"><span data-stu-id="a43e3-186">d.</span></span> <span data-ttu-id="a43e3-187">Yalnızca zaman etkinleştirerek sağlama SAML etkinleştirmeyi seçebilirsiniz **'Otomatik oluştur yeni kullanıcılar'** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="a43e3-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="a43e3-188">Bir kullanıcı Velpic yok ve bu bayrak etkin değil, Azure oturum açma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a43e3-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="a43e3-189">Bayrak etkinleştirilirse kullanıcı otomatik olarak Velpic oturum açma sırasında sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="a43e3-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="a43e3-190">e.</span><span class="sxs-lookup"><span data-stu-id="a43e3-190">e.</span></span> <span data-ttu-id="a43e3-191">Kopya **tek oturum açma URL'si** metinden kutusuna ve Azure portalında yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="a43e3-192">f.</span><span class="sxs-lookup"><span data-stu-id="a43e3-192">f.</span></span> <span data-ttu-id="a43e3-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a43e3-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a43e3-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="a43e3-195">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a43e3-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a43e3-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a43e3-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a43e3-198">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a43e3-200">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="a43e3-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a43e3-202">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a43e3-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a43e3-204">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a43e3-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a43e3-206">a.</span><span class="sxs-lookup"><span data-stu-id="a43e3-206">a.</span></span> <span data-ttu-id="a43e3-207">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a43e3-208">b.</span><span class="sxs-lookup"><span data-stu-id="a43e3-208">b.</span></span> <span data-ttu-id="a43e3-209">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a43e3-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a43e3-210">c.</span><span class="sxs-lookup"><span data-stu-id="a43e3-210">c.</span></span> <span data-ttu-id="a43e3-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a43e3-212">d.</span><span class="sxs-lookup"><span data-stu-id="a43e3-212">d.</span></span> <span data-ttu-id="a43e3-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="a43e3-214">Velpic SAML test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a43e3-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="a43e3-215">Bu adım yalnızca zaman sağlama kullanıcı uygulamayı desteklediği genellikle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="a43e3-216">Otomatik kullanıcı sağlamayı etkinleştirilmemişse, el ile kullanıcı oluşturma aşağıda açıklandığı gibi yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="a43e3-217">Velpic SAML şirket sitenizin yönetici olarak oturum açın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a43e3-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="a43e3-218">Yönet sekmesini tıklatın ve kullanıcıların bölümüne gidin, sonra kullanıcı eklemek için yeni düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![Kullanıcı Ekle](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="a43e3-220">Üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![Kullanıcı](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="a43e3-222">a.</span><span class="sxs-lookup"><span data-stu-id="a43e3-222">a.</span></span> <span data-ttu-id="a43e3-223">İçinde **ad** metin kutusuna, Britta Simon ilk türünün adı.</span><span class="sxs-lookup"><span data-stu-id="a43e3-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="a43e3-224">b.</span><span class="sxs-lookup"><span data-stu-id="a43e3-224">b.</span></span> <span data-ttu-id="a43e3-225">İçinde **Soyadı** metin kutusuna, Britta Simon son adını yazın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="a43e3-226">c.</span><span class="sxs-lookup"><span data-stu-id="a43e3-226">c.</span></span> <span data-ttu-id="a43e3-227">İçinde **kullanıcı adı** metin kutusuna, Britta Simon kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="a43e3-228">d.</span><span class="sxs-lookup"><span data-stu-id="a43e3-228">d.</span></span> <span data-ttu-id="a43e3-229">İçinde **e-posta** metin kutusuna, Britta Simon hesabı e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="a43e3-230">e.</span><span class="sxs-lookup"><span data-stu-id="a43e3-230">e.</span></span> <span data-ttu-id="a43e3-231">Bilgi geri kalanı isteğe bağlıdır, gerekirse doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a43e3-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="a43e3-232">f.</span><span class="sxs-lookup"><span data-stu-id="a43e3-232">f.</span></span> <span data-ttu-id="a43e3-233">**KAYDET**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a43e3-234">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a43e3-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a43e3-235">Bu bölümde, Britta Velpic SAML kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a43e3-237">**Britta Simon Velpic SAML atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a43e3-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="a43e3-238">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a43e3-240">Uygulamalar listesinde **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="a43e3-242">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a43e3-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a43e3-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a43e3-244">Click **Add** button.</span></span> <span data-ttu-id="a43e3-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a43e3-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a43e3-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a43e3-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a43e3-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a43e3-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a43e3-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a43e3-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a43e3-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a43e3-250">Testing single sign-on</span></span>

<span data-ttu-id="a43e3-251">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a43e3-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="a43e3-252">Erişim paneli Velpic SAML parçasında tıkladığınızda, oturum açma sayfasına Velpic SAML uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a43e3-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="a43e3-253">Görmeniz gerekir **'Günlük oturum Azure AD'** oturum açma sayfası düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="a43e3-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="a43e3-255">Tıklayın **'Günlük oturum Azure AD'** düğmesini Velpic için Azure AD hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a43e3-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a43e3-256">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a43e3-256">Additional resources</span></span>

* [<span data-ttu-id="a43e3-257">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="a43e3-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a43e3-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a43e3-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

