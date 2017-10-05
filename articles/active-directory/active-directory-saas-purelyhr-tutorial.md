---
title: "Öğretici: Azure Active Directory Tümleştirme ile PurelyHR | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile PurelyHR arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="915bb-103">Öğretici: Azure Active Directory Tümleştirme PurelyHR ile</span><span class="sxs-lookup"><span data-stu-id="915bb-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="915bb-104">Bu öğreticide, Azure Active Directory (Azure AD) ile PurelyHR tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="915bb-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="915bb-105">PurelyHR Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="915bb-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="915bb-106">PurelyHR erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="915bb-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="915bb-107">Otomatik olarak için PurelyHR (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="915bb-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="915bb-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="915bb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="915bb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="915bb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="915bb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="915bb-110">Prerequisites</span></span>

<span data-ttu-id="915bb-111">Azure AD tümleştirme PurelyHR ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="915bb-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="915bb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="915bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="915bb-113">Bir PurelyHR çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="915bb-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="915bb-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="915bb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="915bb-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="915bb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="915bb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="915bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="915bb-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="915bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="915bb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="915bb-118">Scenario description</span></span>
<span data-ttu-id="915bb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="915bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="915bb-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="915bb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="915bb-121">Galeriden PurelyHR ekleme</span><span class="sxs-lookup"><span data-stu-id="915bb-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="915bb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="915bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="915bb-123">Galeriden PurelyHR ekleme</span><span class="sxs-lookup"><span data-stu-id="915bb-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="915bb-124">Azure AD PurelyHR tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden PurelyHR eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="915bb-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="915bb-125">**Galeriden PurelyHR eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="915bb-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="915bb-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="915bb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="915bb-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="915bb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="915bb-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="915bb-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="915bb-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="915bb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="915bb-133">Arama kutusuna **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="915bb-133">In the search box, type **PurelyHR**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="915bb-135">Sonuçlar panelinde seçin **PurelyHR**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="915bb-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="915bb-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="915bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="915bb-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı PurelyHR ile test etme</span><span class="sxs-lookup"><span data-stu-id="915bb-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="915bb-139">Tekli çalışmaya oturum için Azure AD PurelyHR karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="915bb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="915bb-140">Diğer bir deyişle, bir Azure AD kullanıcısının PurelyHR ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="915bb-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="915bb-141">PurelyHR içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="915bb-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="915bb-142">Yapılandırma ve Azure AD çoklu oturum açma PurelyHR ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="915bb-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="915bb-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="915bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="915bb-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="915bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="915bb-145">**[PurelyHR test kullanıcısı oluşturma](#creating-a-purelyhr-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı PurelyHR sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="915bb-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="915bb-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="915bb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="915bb-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="915bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="915bb-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="915bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="915bb-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma PurelyHR uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="915bb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="915bb-150">**Azure AD çoklu oturum açma ile PurelyHR yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="915bb-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="915bb-151">Azure portalında üzerinde **PurelyHR** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="915bb-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="915bb-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="915bb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="915bb-155">Üzerinde **PurelyHR etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="915bb-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="915bb-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="915bb-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="915bb-158">Denetleme **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="915bb-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="915bb-160">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="915bb-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="915bb-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="915bb-161">These values are not the real.</span></span> <span data-ttu-id="915bb-162">Bu değerler gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="915bb-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="915bb-163">Kişi [PurelyHR istemci destek ekibi](http://support.purelyhr.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="915bb-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="915bb-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="915bb-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="915bb-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="915bb-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="915bb-168">Üzerinde **PurelyHR yapılandırma** 'yi tıklatın **yapılandırma PurelyHR** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="915bb-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="915bb-169">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="915bb-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="915bb-171">Çoklu oturum açma yapılandırmak için **PurelyHR** tarafı, kullanıcıların Web sitesi bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="915bb-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="915bb-172">Açık **Pano** seçeneklerden birini tıklatın ve araç **SSO ayarları**.</span><span class="sxs-lookup"><span data-stu-id="915bb-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="915bb-173">Aşağıdaki - açıklandığı gibi değerler kutularına yapıştırın</span><span class="sxs-lookup"><span data-stu-id="915bb-173">Paste the values in the boxes as described below-</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="915bb-175">a.</span><span class="sxs-lookup"><span data-stu-id="915bb-175">a.</span></span> <span data-ttu-id="915bb-176">Açık **Certificate(Bas64)** Not Defteri'nde Azure portalından indirdiğiniz ve sertifika değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="915bb-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="915bb-177">Kopyalanan değeri içine yapıştırabilirsiniz **X.509 sertifikası** kutusu.</span><span class="sxs-lookup"><span data-stu-id="915bb-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="915bb-178">b.</span><span class="sxs-lookup"><span data-stu-id="915bb-178">b.</span></span> <span data-ttu-id="915bb-179">İçinde **IDP veren URL'si** kutusunda, yapıştırma **SAML varlık kimliği** Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="915bb-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="915bb-180">c.</span><span class="sxs-lookup"><span data-stu-id="915bb-180">c.</span></span> <span data-ttu-id="915bb-181">İçinde **IDP uç nokta URL'si** kutusunda, yapıştırma **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="915bb-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="915bb-182">d.</span><span class="sxs-lookup"><span data-stu-id="915bb-182">d.</span></span> <span data-ttu-id="915bb-183">Denetleme **otomatik olarak oluşturma kullanıcıların** içinde PurelyHR otomatik kullanıcı sağlamayı etkinleştirmek için onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="915bb-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="915bb-184">e.</span><span class="sxs-lookup"><span data-stu-id="915bb-184">e.</span></span> <span data-ttu-id="915bb-185">Tıklatın **Değişiklikleri Kaydet** ayarları kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="915bb-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="915bb-186">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="915bb-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="915bb-187">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="915bb-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="915bb-188">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="915bb-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="915bb-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="915bb-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="915bb-190">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="915bb-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="915bb-192">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="915bb-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="915bb-193">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="915bb-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="915bb-195">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="915bb-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="915bb-197">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="915bb-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="915bb-199">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="915bb-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="915bb-201">a.</span><span class="sxs-lookup"><span data-stu-id="915bb-201">a.</span></span> <span data-ttu-id="915bb-202">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="915bb-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="915bb-203">b.</span><span class="sxs-lookup"><span data-stu-id="915bb-203">b.</span></span> <span data-ttu-id="915bb-204">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="915bb-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="915bb-205">c.</span><span class="sxs-lookup"><span data-stu-id="915bb-205">c.</span></span> <span data-ttu-id="915bb-206">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="915bb-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="915bb-207">d.</span><span class="sxs-lookup"><span data-stu-id="915bb-207">d.</span></span> <span data-ttu-id="915bb-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="915bb-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="915bb-209">PurelyHR test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="915bb-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="915bb-210">Azure AD kullanıcıları için PurelyHR oturum açmak etkinleştirmek için bunların PurelyHR sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="915bb-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="915bb-211">PurelyHR, sağlama otomatik bir görevdir ve otomatik kullanıcı sağlamayı etkinleştirildiğinde el ile yapılan hiçbir adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="915bb-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="915bb-212">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="915bb-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="915bb-213">Bu bölümde, Britta PurelyHR için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="915bb-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="915bb-215">**PurelyHR için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="915bb-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="915bb-216">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="915bb-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="915bb-218">Uygulamalar listesinde **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="915bb-218">In the applications list, select **PurelyHR**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="915bb-220">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="915bb-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="915bb-222">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="915bb-222">Click **Add** button.</span></span> <span data-ttu-id="915bb-223">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="915bb-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="915bb-225">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="915bb-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="915bb-226">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="915bb-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="915bb-227">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="915bb-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="915bb-228">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="915bb-228">Testing single sign-on</span></span>

<span data-ttu-id="915bb-229">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="915bb-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="915bb-230">Erişim paneli almak LMS parçasında tıklatıp, otomatik olarak Al LMS uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="915bb-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="915bb-231">Erişim paneli hakkında daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="915bb-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="915bb-232">[Erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="915bb-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="915bb-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="915bb-233">Additional resources</span></span>

* [<span data-ttu-id="915bb-234">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="915bb-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="915bb-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="915bb-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

