---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix GoToMeeting | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Citrix GoToMeeting arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="838a6-103">Öğretici: Citrix GoToMeeting Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="838a6-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="838a6-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Citrix GoToMeeting tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="838a6-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="838a6-105">Citrix GoToMeeting Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="838a6-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="838a6-106">Citrix GoToMeeting erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="838a6-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="838a6-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Citrix GoToMeeting açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="838a6-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="838a6-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="838a6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="838a6-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="838a6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="838a6-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="838a6-110">Prerequisites</span></span>

<span data-ttu-id="838a6-111">Azure AD tümleştirme Citrix GoToMeeting ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="838a6-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="838a6-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="838a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="838a6-113">Bir Citrix GoToMeeting çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="838a6-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="838a6-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="838a6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="838a6-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="838a6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="838a6-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="838a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="838a6-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="838a6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="838a6-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="838a6-118">Scenario description</span></span>
<span data-ttu-id="838a6-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="838a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="838a6-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="838a6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="838a6-121">Galeriden Citrix GoToMeeting ekleme</span><span class="sxs-lookup"><span data-stu-id="838a6-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="838a6-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="838a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="838a6-123">Galeriden Citrix GoToMeeting ekleme</span><span class="sxs-lookup"><span data-stu-id="838a6-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="838a6-124">Azure AD Citrix GoToMeeting tümleştirilmesi yapılandırmak için Citrix GoToMeeting Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="838a6-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="838a6-125">**Galeriden Citrix GoToMeeting eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="838a6-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="838a6-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="838a6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="838a6-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="838a6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="838a6-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="838a6-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="838a6-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="838a6-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="838a6-133">Arama kutusuna **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="838a6-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="838a6-135">Sonuçlar panelinde seçin **Citrix GoToMeeting**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="838a6-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="838a6-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="838a6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="838a6-138">Bu bölümde, yapılandırmanız ve Citrix GoToMeeting ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="838a6-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="838a6-139">Tekli çalışmaya oturum için Azure AD Citrix GoToMeeting karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="838a6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="838a6-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Citrix GoToMeeting ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="838a6-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="838a6-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Citrix GoToMeeting içinde.</span><span class="sxs-lookup"><span data-stu-id="838a6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="838a6-142">Yapılandırma ve Azure AD çoklu oturum açma Citrix GoToMeeting ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="838a6-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="838a6-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="838a6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="838a6-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="838a6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="838a6-145">**[Citrix GoToMeeting test kullanıcısı oluşturma](#creating-a-citrix-gotomeeting-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Citrix GoToMeeting sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="838a6-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="838a6-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="838a6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="838a6-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="838a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="838a6-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="838a6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="838a6-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Citrix GoToMeeting uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="838a6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="838a6-150">**Azure AD çoklu oturum açma ile Citrix GoToMeeting yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="838a6-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="838a6-151">Azure portalında üzerinde **Citrix GoToMeeting** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="838a6-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="838a6-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="838a6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="838a6-155">Üzerinde **Citrix GoToMeeting etki alanı ve URL'leri** bölümünde, herhangi bir adım gerçekleştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="838a6-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="838a6-157">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="838a6-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="838a6-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="838a6-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="838a6-161">Citrix GoToMeeting SAML yapılandırma bölümünde Yapılandır oturum açma penceresini açmak için Citrix GoToMeeting SAML Yapılandır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="838a6-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="838a6-162">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="838a6-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="838a6-163">Farklı bir tarayıcı penceresinde oturum açın, [Citrix kuruluş Merkezi](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="838a6-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="838a6-164">Tıklatın **kimlik sağlayıcısı** sekmesini ve sonra aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="838a6-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="838a6-165">![SAML Kurulumu](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="838a6-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="838a6-166">a.</span><span class="sxs-lookup"><span data-stu-id="838a6-166">a.</span></span> <span data-ttu-id="838a6-167">Seçin **el ile**</span><span class="sxs-lookup"><span data-stu-id="838a6-167">Select **Manual**</span></span>

    <span data-ttu-id="838a6-168">b.</span><span class="sxs-lookup"><span data-stu-id="838a6-168">b.</span></span> <span data-ttu-id="838a6-169">Azure portalında üzerinde **çoklu oturum açma sırasında Citrix GoToMeeting yapılandırma** iletişim sayfası, kopya **SAML çoklu oturum açma hizmet URL'si** değer ve ardından yapıştırın **oturum açma sayfası URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="838a6-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="838a6-170">c.</span><span class="sxs-lookup"><span data-stu-id="838a6-170">c.</span></span> <span data-ttu-id="838a6-171">Azure portalında üzerinde **çoklu oturum açma sırasında Citrix GoToMeeting yapılandırma** iletişim sayfası, kopya **Sign-Out URL** değer ve ardından yapıştırın **oturum kapatma sayfası URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="838a6-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="838a6-172">d.</span><span class="sxs-lookup"><span data-stu-id="838a6-172">d.</span></span> <span data-ttu-id="838a6-173">Azure portalında üzerinde **çoklu oturum açma sırasında Citrix GoToMeeting yapılandırma** iletişim sayfası, kopya **SAML varlık kimliği** değer ve ardından yapıştırın **kimlik sağlayıcısı varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="838a6-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="838a6-174">e.</span><span class="sxs-lookup"><span data-stu-id="838a6-174">e.</span></span> <span data-ttu-id="838a6-175">İndirilen sertifikanızı karşıya yüklemek için tıklayın **sertifikasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="838a6-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="838a6-176">f.</span><span class="sxs-lookup"><span data-stu-id="838a6-176">f.</span></span> <span data-ttu-id="838a6-177">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="838a6-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="838a6-178">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="838a6-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="838a6-179">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="838a6-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="838a6-180">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="838a6-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="838a6-181">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="838a6-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="838a6-182">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="838a6-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="838a6-184">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="838a6-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="838a6-185">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="838a6-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="838a6-187">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="838a6-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="838a6-189">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="838a6-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="838a6-191">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="838a6-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="838a6-193">a.</span><span class="sxs-lookup"><span data-stu-id="838a6-193">a.</span></span> <span data-ttu-id="838a6-194">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="838a6-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="838a6-195">b.</span><span class="sxs-lookup"><span data-stu-id="838a6-195">b.</span></span> <span data-ttu-id="838a6-196">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="838a6-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="838a6-197">c.</span><span class="sxs-lookup"><span data-stu-id="838a6-197">c.</span></span> <span data-ttu-id="838a6-198">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="838a6-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="838a6-199">d.</span><span class="sxs-lookup"><span data-stu-id="838a6-199">d.</span></span> <span data-ttu-id="838a6-200">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="838a6-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="838a6-201">Citrix GoToMeeting test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="838a6-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="838a6-202">Bu bölümde, bir kullanıcı Britta Simon olarak adlandırılır ve Citrix GoToMeeting oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="838a6-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="838a6-203">Citrix GoToMeeting tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="838a6-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="838a6-204">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="838a6-204">There is no action item for you in this section.</span></span> <span data-ttu-id="838a6-205">Bir kullanıcı zaten Citrix GoToMeeting yoksa, Citrix GoToMeeting erişmeyi denediğinde yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="838a6-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="838a6-206">Bir kullanıcı el ile oluşturmanız gerekirse başvurun [Citrix GoToMeeting destek ekibi](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="838a6-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="838a6-207">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="838a6-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="838a6-208">Bu bölümde, Britta Citrix GoToMeeting erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="838a6-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="838a6-210">**Citrix GoToMeeting Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="838a6-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="838a6-211">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="838a6-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="838a6-213">Uygulamalar listesinde **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="838a6-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="838a6-215">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="838a6-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="838a6-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="838a6-217">Click **Add** button.</span></span> <span data-ttu-id="838a6-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="838a6-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="838a6-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="838a6-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="838a6-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="838a6-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="838a6-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="838a6-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="838a6-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="838a6-223">Testing single sign-on</span></span>

<span data-ttu-id="838a6-224">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="838a6-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="838a6-225">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="838a6-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="838a6-226">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="838a6-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="838a6-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="838a6-227">Additional resources</span></span>

* [<span data-ttu-id="838a6-228">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="838a6-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="838a6-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="838a6-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="838a6-230">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="838a6-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

