---
title: "Öğretici: Azure Active Directory Tümleştirme daha düz dosyalarla | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile daha düz dosyalar arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="7fa41-103">Öğretici: Azure Active Directory Tümleştirme ile daha düz dosyalar</span><span class="sxs-lookup"><span data-stu-id="7fa41-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="7fa41-104">Bu öğreticide, Azure Active Directory (Azure AD) ile tümleştirme daha düz dosyalarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7fa41-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fa41-105">Azure AD ile daha düz dosyalar tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7fa41-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7fa41-106">Daha düz dosyalara erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7fa41-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="7fa41-107">Azure AD hesaplarına otomatik olarak daha düz dosyalara (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7fa41-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fa41-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7fa41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7fa41-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fa41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fa41-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7fa41-110">Prerequisites</span></span>

<span data-ttu-id="7fa41-111">Azure AD tümleştirme daha düz dosyalarıyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fa41-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="7fa41-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7fa41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fa41-113">Bir daha düz dosyalar çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7fa41-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fa41-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7fa41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fa41-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fa41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fa41-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7fa41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fa41-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fa41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fa41-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7fa41-118">Scenario description</span></span>
<span data-ttu-id="7fa41-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7fa41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fa41-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7fa41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fa41-121">Galeriden daha düz dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="7fa41-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="7fa41-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7fa41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="7fa41-123">Galeriden daha düz dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="7fa41-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="7fa41-124">Azure AD daha düz dosyalar tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden daha düz dosyalar eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fa41-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7fa41-125">**Galeriden daha düz dosya eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fa41-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7fa41-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7fa41-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7fa41-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7fa41-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7fa41-133">Arama kutusuna **daha düz dosyalar**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-133">In the search box, type **Flatter Files**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="7fa41-135">Sonuçlar panelinde seçin **daha düz dosyalar**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7fa41-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7fa41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7fa41-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı göre daha düz dosyalar ile test etme.</span><span class="sxs-lookup"><span data-stu-id="7fa41-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7fa41-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen daha düz dosyalarında bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="7fa41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="7fa41-140">Diğer bir deyişle, bir Azure AD kullanıcısının daha düz dosyalar ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fa41-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="7fa41-141">Değerini daha düz dosyalarında atamak **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7fa41-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7fa41-142">Yapılandırmak ve Azure AD çoklu oturum açma daha düz dosyalarıyla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fa41-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7fa41-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fa41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7fa41-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="7fa41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fa41-145">**[Daha düz dosyalar test kullanıcısı oluşturma](#creating-a-flatter-files-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı daha düz dosyalar sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="7fa41-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fa41-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fa41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fa41-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7fa41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7fa41-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7fa41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7fa41-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma daha düz dosyalar uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7fa41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="7fa41-150">**Azure AD çoklu oturum açma daha düz dosyalarıyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fa41-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="7fa41-151">Azure portalında üzerinde **daha düz dosyalar** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7fa41-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fa41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="7fa41-155">Üzerinde **daha düz dosyalar etki alanı ve URL'leri** bölümü, kullanıcı gerekmez uygulama zaten Azure ile önceden tümleştirilmiş gibi tüm adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7fa41-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="7fa41-157">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7fa41-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="7fa41-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7fa41-161">Üzerinde **daha düz dosyalar yapılandırma** 'yi tıklatın **yapılandırmak daha düz dosyalar** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7fa41-162">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7fa41-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="7fa41-164">Yönetici olarak daha düz dosyalar uygulamanıza oturum.</span><span class="sxs-lookup"><span data-stu-id="7fa41-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="7fa41-165">Tıklatın **PANO**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-165">Click **DASHBOARD**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="7fa41-167">Tıklatın **ayarları**ve ardından üzerinde aşağıdaki adımları gerçekleştirebilirsiniz **şirket** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="7fa41-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="7fa41-169">a.</span><span class="sxs-lookup"><span data-stu-id="7fa41-169">a.</span></span> <span data-ttu-id="7fa41-170">Seçin **SAML 2.0 kimlik doğrulaması için kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="7fa41-171">b.</span><span class="sxs-lookup"><span data-stu-id="7fa41-171">b.</span></span> <span data-ttu-id="7fa41-172">Tıklatın **SAML yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="7fa41-173">Üzerinde **SAML Yapılandırması** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fa41-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="7fa41-175">a.</span><span class="sxs-lookup"><span data-stu-id="7fa41-175">a.</span></span> <span data-ttu-id="7fa41-176">İçinde **etki alanı** metin kutusuna, kayıtlı etki alanınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="7fa41-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="7fa41-177">Bir kayıtlı bir etki alanı henüz, kişi yoksa daha düz dosyalarınızı takım aracılığıyla destek [ support@flatterfiles.com ](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="7fa41-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="7fa41-178">b.</span><span class="sxs-lookup"><span data-stu-id="7fa41-178">b.</span></span> <span data-ttu-id="7fa41-179">İçinde **kimlik sağlayıcısı URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** kopyalanan Azure portalı form.</span><span class="sxs-lookup"><span data-stu-id="7fa41-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="7fa41-180">c.</span><span class="sxs-lookup"><span data-stu-id="7fa41-180">c.</span></span>  <span data-ttu-id="7fa41-181">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7fa41-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="7fa41-182">d.</span><span class="sxs-lookup"><span data-stu-id="7fa41-182">d.</span></span> <span data-ttu-id="7fa41-183">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="7fa41-184">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7fa41-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7fa41-185">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="7fa41-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7fa41-186">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fa41-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7fa41-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fa41-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="7fa41-188">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7fa41-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7fa41-190">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fa41-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7fa41-191">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fa41-193">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fa41-195">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="7fa41-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fa41-197">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fa41-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fa41-199">a.</span><span class="sxs-lookup"><span data-stu-id="7fa41-199">a.</span></span> <span data-ttu-id="7fa41-200">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fa41-201">b.</span><span class="sxs-lookup"><span data-stu-id="7fa41-201">b.</span></span> <span data-ttu-id="7fa41-202">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7fa41-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fa41-203">c.</span><span class="sxs-lookup"><span data-stu-id="7fa41-203">c.</span></span> <span data-ttu-id="7fa41-204">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7fa41-205">d.</span><span class="sxs-lookup"><span data-stu-id="7fa41-205">d.</span></span> <span data-ttu-id="7fa41-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fa41-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="7fa41-207">Daha düz dosyalar test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fa41-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="7fa41-208">Bu bölümün amacı daha düz dosyalarında Britta Simon adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7fa41-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="7fa41-209">**Daha düz dosyalarında Britta Simon adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fa41-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="7fa41-210">Oturum, **daha düz dosyalar** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="7fa41-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="7fa41-211">Sol gezinti bölmesinde tıklayın **ayarları**ve ardından **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Daha düz dosyalar kullanıcı oluştur](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="7fa41-213">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="7fa41-214">Üzerinde **Kullanıcı Ekle** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fa41-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Daha düz dosyalar kullanıcı oluştur](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="7fa41-216">a.</span><span class="sxs-lookup"><span data-stu-id="7fa41-216">a.</span></span> <span data-ttu-id="7fa41-217">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="7fa41-218">b.</span><span class="sxs-lookup"><span data-stu-id="7fa41-218">b.</span></span> <span data-ttu-id="7fa41-219">İçinde **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="7fa41-220">c.</span><span class="sxs-lookup"><span data-stu-id="7fa41-220">c.</span></span> <span data-ttu-id="7fa41-221">İçinde **e-posta adresi** metin kutusuna, Azure portalında Britta'nın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="7fa41-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="7fa41-222">d.</span><span class="sxs-lookup"><span data-stu-id="7fa41-222">d.</span></span> <span data-ttu-id="7fa41-223">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7fa41-224">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7fa41-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7fa41-225">Bu bölümde, Britta daha düz dosyalara erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7fa41-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7fa41-227">**Daha düz dosyalara Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fa41-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="7fa41-228">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7fa41-230">Uygulamalar listesinde **daha düz dosyalar**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-230">In the applications list, select **Flatter Files**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="7fa41-232">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7fa41-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7fa41-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fa41-234">Click **Add** button.</span></span> <span data-ttu-id="7fa41-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fa41-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7fa41-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7fa41-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7fa41-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fa41-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fa41-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fa41-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7fa41-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7fa41-240">Testing single sign-on</span></span>

<span data-ttu-id="7fa41-241">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7fa41-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7fa41-242">Erişim paneli daha düz dosyalar parçasında tıklattığınızda, otomatik olarak daha düz dosyalar uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="7fa41-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="7fa41-243">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fa41-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fa41-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7fa41-244">Additional resources</span></span>

* [<span data-ttu-id="7fa41-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="7fa41-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fa41-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7fa41-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

