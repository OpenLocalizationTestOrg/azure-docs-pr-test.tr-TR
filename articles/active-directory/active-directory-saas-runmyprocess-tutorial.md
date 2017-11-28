---
title: "Öğretici: Azure Active Directory Tümleştirme ile RunMyProcess | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile RunMyProcess arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="65594-103">Öğretici: Azure Active Directory Tümleştirme RunMyProcess ile</span><span class="sxs-lookup"><span data-stu-id="65594-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="65594-104">Bu öğreticide, Azure Active Directory (Azure AD) ile RunMyProcess tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="65594-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65594-105">RunMyProcess Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="65594-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65594-106">RunMyProcess erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="65594-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="65594-107">Otomatik olarak için RunMyProcess (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="65594-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65594-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="65594-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65594-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65594-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65594-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65594-110">Prerequisites</span></span>

<span data-ttu-id="65594-111">Azure AD tümleştirme RunMyProcess ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="65594-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="65594-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="65594-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65594-113">Bir RunMyProcess çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="65594-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65594-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="65594-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65594-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="65594-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65594-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="65594-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65594-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz:[deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65594-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65594-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="65594-118">Scenario description</span></span>
<span data-ttu-id="65594-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="65594-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65594-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="65594-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65594-121">Galeriden RunMyProcess ekleme</span><span class="sxs-lookup"><span data-stu-id="65594-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="65594-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="65594-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="65594-123">Galeriden RunMyProcess ekleme</span><span class="sxs-lookup"><span data-stu-id="65594-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="65594-124">Azure AD RunMyProcess tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden RunMyProcess eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65594-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65594-125">**Galeriden RunMyProcess eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65594-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65594-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65594-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65594-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="65594-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65594-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65594-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="65594-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65594-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="65594-133">Arama kutusuna **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="65594-133">In the search box, type **RunMyProcess**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="65594-135">Sonuçlar panelinde seçin **RunMyProcess**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65594-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65594-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="65594-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65594-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı RunMyProcess sınayın.</span><span class="sxs-lookup"><span data-stu-id="65594-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65594-139">Tekli çalışmaya oturum için Azure AD RunMyProcess karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="65594-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="65594-140">Diğer bir deyişle, bir Azure AD kullanıcısının RunMyProcess ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65594-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="65594-141">RunMyProcess içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="65594-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65594-142">Yapılandırma ve Azure AD çoklu oturum açma RunMyProcess ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="65594-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65594-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="65594-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65594-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="65594-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65594-145">**[RunMyProcess test kullanıcısı oluşturma](#creating-a-runmyprocess-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı RunMyProcess sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="65594-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65594-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="65594-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65594-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="65594-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65594-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="65594-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65594-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma RunMyProcess uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="65594-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="65594-150">**Azure AD çoklu oturum açma ile RunMyProcess yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65594-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="65594-151">Azure portalında üzerinde **RunMyProcess** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="65594-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="65594-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="65594-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="65594-155">Üzerinde **RunMyProcess etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65594-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="65594-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="65594-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65594-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="65594-158">The value is not real.</span></span> <span data-ttu-id="65594-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="65594-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="65594-160">Kişi [RunMyProcess istemci destek ekibi](mailto:support@runmyprocess.com) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="65594-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="65594-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="65594-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="65594-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65594-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65594-165">Üzerinde **RunMyProcess yapılandırma** 'yi tıklatın **yapılandırma RunMyProcess** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="65594-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65594-166">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="65594-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="65594-168">Farklı web tarayıcısı penceresinde RunMyProcess kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="65594-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="65594-169">Sol gezinti panelinde tıklatın **hesap** seçip **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="65594-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="65594-171">Git **kimlik doğrulama yöntemini** bölümünde ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65594-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="65594-173">a.</span><span class="sxs-lookup"><span data-stu-id="65594-173">a.</span></span> <span data-ttu-id="65594-174">Olarak **yöntemi**seçin **Samlv2 SSO'su**.</span><span class="sxs-lookup"><span data-stu-id="65594-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="65594-175">b.</span><span class="sxs-lookup"><span data-stu-id="65594-175">b.</span></span> <span data-ttu-id="65594-176">İçinde **SSO yeniden yönlendirme** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65594-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65594-177">c.</span><span class="sxs-lookup"><span data-stu-id="65594-177">c.</span></span> <span data-ttu-id="65594-178">İçinde **oturumu kapatıp yeniden yönlendirme** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="65594-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65594-179">d.</span><span class="sxs-lookup"><span data-stu-id="65594-179">d.</span></span> <span data-ttu-id="65594-180">İçinde **ad kimliği biçimi** metin değerini yazın **ad tanımlayıcısı biçimi** olarak **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="65594-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="65594-181">e.</span><span class="sxs-lookup"><span data-stu-id="65594-181">e.</span></span> <span data-ttu-id="65594-182">İndirilen sertifika dosyasının içeriğini kopyalayın ve ardından yapıştırın **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="65594-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="65594-183">f.</span><span class="sxs-lookup"><span data-stu-id="65594-183">f.</span></span> <span data-ttu-id="65594-184">Tıklatın **kaydetmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65594-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="65594-185">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="65594-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65594-186">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="65594-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65594-187">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65594-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65594-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65594-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="65594-189">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="65594-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="65594-191">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65594-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65594-192">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="65594-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65594-194">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="65594-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65594-196">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="65594-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65594-198">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65594-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65594-200">a.</span><span class="sxs-lookup"><span data-stu-id="65594-200">a.</span></span> <span data-ttu-id="65594-201">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65594-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65594-202">b.</span><span class="sxs-lookup"><span data-stu-id="65594-202">b.</span></span> <span data-ttu-id="65594-203">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="65594-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65594-204">c.</span><span class="sxs-lookup"><span data-stu-id="65594-204">c.</span></span> <span data-ttu-id="65594-205">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="65594-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65594-206">d.</span><span class="sxs-lookup"><span data-stu-id="65594-206">d.</span></span> <span data-ttu-id="65594-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65594-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="65594-208">RunMyProcess test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65594-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="65594-209">Azure AD kullanıcıları için RunMyProcess oturum açmak etkinleştirmek için bunların RunMyProcess sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="65594-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="65594-210">RunMyProcess söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="65594-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="65594-211">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65594-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="65594-212">RunMyProcess şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65594-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="65594-213">Tıklatın **hesap** seçip **kullanıcılar** sol gezinti panelinde, ardından **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="65594-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="65594-214">![Yeni kullanıcı](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="65594-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="65594-215">İçinde **kullanıcı ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65594-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="65594-216">![Profil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profili")</span><span class="sxs-lookup"><span data-stu-id="65594-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="65594-217">a.</span><span class="sxs-lookup"><span data-stu-id="65594-217">a.</span></span> <span data-ttu-id="65594-218">Tür **adı** ve **e-posta** geçerli bir Azure AD hesabının istediğiniz ilgili metin kutularına sağlamayı.</span><span class="sxs-lookup"><span data-stu-id="65594-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="65594-219">b.</span><span class="sxs-lookup"><span data-stu-id="65594-219">b.</span></span> <span data-ttu-id="65594-220">Seçin bir **IDE dil**, **dil**, ve **profil**.</span><span class="sxs-lookup"><span data-stu-id="65594-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="65594-221">c.</span><span class="sxs-lookup"><span data-stu-id="65594-221">c.</span></span> <span data-ttu-id="65594-222">Seçin **Gönder hesap oluşturma e-posta bana**.</span><span class="sxs-lookup"><span data-stu-id="65594-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="65594-223">d.</span><span class="sxs-lookup"><span data-stu-id="65594-223">d.</span></span> <span data-ttu-id="65594-224">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65594-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="65594-225">API tarafından RunMyProcess sağlamak için Azure Active Directory kullanıcı hesapları sağlanan veya herhangi diğer RunMyProcess kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65594-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65594-226">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="65594-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65594-227">Bu bölümde, Britta RunMyProcess için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="65594-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="65594-229">**RunMyProcess için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="65594-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="65594-230">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="65594-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="65594-232">Uygulamalar listesinde **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="65594-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="65594-234">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="65594-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="65594-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65594-236">Click **Add** button.</span></span> <span data-ttu-id="65594-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65594-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="65594-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="65594-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65594-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65594-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65594-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="65594-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65594-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="65594-242">Testing single sign-on</span></span>

<span data-ttu-id="65594-243">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="65594-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="65594-244">Erişim paneli RunMyProcess parçasında tıklattığınızda, otomatik olarak RunMyProcess uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="65594-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65594-245">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="65594-245">Additional resources</span></span>

* [<span data-ttu-id="65594-246">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="65594-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65594-247">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="65594-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

