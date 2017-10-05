---
title: "Öğretici: Azure Active Directory Tümleştirme ile isteğe bağlı Proofpoint | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Proofpoint arasında isteğe bağlı yapılandırma konusunda bilgi edinin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="865cc-103">Öğretici: Azure Active Directory Tümleştirme ile Proofpoint isteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="865cc-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="865cc-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Proofpoint isteğe bağlı tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="865cc-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="865cc-105">İsteğe bağlı Proofpoint Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="865cc-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="865cc-106">İsteğe bağlı Proofpoint erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="865cc-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="865cc-107">Otomatik olarak Proofpoint isteğe bağlı (çoklu oturum açma) için Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="865cc-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="865cc-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="865cc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="865cc-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="865cc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="865cc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="865cc-110">Prerequisites</span></span>

<span data-ttu-id="865cc-111">İsteğe bağlı Proofpoint ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="865cc-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="865cc-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="865cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="865cc-113">İsteğe bağlı çoklu oturum açma etkin abonelik üzerinde Proofpoint</span><span class="sxs-lookup"><span data-stu-id="865cc-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="865cc-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="865cc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="865cc-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="865cc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="865cc-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="865cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="865cc-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="865cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="865cc-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="865cc-118">Scenario description</span></span>
<span data-ttu-id="865cc-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="865cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="865cc-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="865cc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="865cc-121">Galeriden isteğe bağlı Proofpoint ekleme</span><span class="sxs-lookup"><span data-stu-id="865cc-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="865cc-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="865cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="865cc-123">Galeriden isteğe bağlı Proofpoint ekleme</span><span class="sxs-lookup"><span data-stu-id="865cc-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="865cc-124">Azure AD ile isteğe bağlı Proofpoint tümleştirmesini yapılandırmak için Proofpoint isteğe bağlı Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="865cc-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="865cc-125">**Proofpoint Galeriden isteğe bağlı olarak eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="865cc-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="865cc-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="865cc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="865cc-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="865cc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="865cc-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="865cc-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="865cc-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="865cc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="865cc-133">Arama kutusuna **Proofpoint isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="865cc-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="865cc-135">Sonuçlar panelinde seçin **isteğe bağlı Proofpoint**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="865cc-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="865cc-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="865cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="865cc-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı isteğe bağlı Proofpoint ile test etme</span><span class="sxs-lookup"><span data-stu-id="865cc-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="865cc-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Proofpoint isteğe bağlı olarak bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="865cc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="865cc-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve isteğe bağlı Proofpoint ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="865cc-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="865cc-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Proofpoint isteğe bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="865cc-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="865cc-142">Yapılandırmak ve Azure AD çoklu oturum açma ile isteğe bağlı Proofpoint sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="865cc-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="865cc-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="865cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="865cc-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="865cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="865cc-145">**[Bir Proofpoint üzerinde isteğe bağlı test kullanıcısı oluşturma](#creating-a-proofpoint-on-demand-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı isteğe bağlı Proofpoint sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="865cc-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="865cc-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="865cc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="865cc-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="865cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="865cc-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="865cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="865cc-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, Proofpoint isteğe bağlı uygulama üzerinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="865cc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="865cc-150">**İsteğe bağlı Proofpoint ile Azure AD çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="865cc-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="865cc-151">Azure portalında üzerinde **Proofpoint isteğe bağlı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="865cc-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="865cc-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="865cc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="865cc-155">Üzerinde **Proofpoint isteğe bağlı etki alanı ve URL'ler hakkında** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="865cc-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="865cc-157">a.In **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="865cc-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="865cc-158">b.</span><span class="sxs-lookup"><span data-stu-id="865cc-158">b.</span></span> <span data-ttu-id="865cc-159">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="865cc-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="865cc-160">c.</span><span class="sxs-lookup"><span data-stu-id="865cc-160">c.</span></span>  <span data-ttu-id="865cc-161">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="865cc-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="865cc-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="865cc-162">These values are not the real.</span></span> <span data-ttu-id="865cc-163">Bu değerleri gerçek tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="865cc-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="865cc-164">Kişi [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="865cc-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="865cc-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="865cc-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="865cc-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="865cc-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="865cc-169">Üzerinde **isteğe bağlı yapılandırma Proofpoint** 'yi tıklatın **isteğe bağlı yapılandırma Proofpoint** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="865cc-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="865cc-170">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="865cc-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="865cc-172">Çoklu oturum açma yapılandırmak için **isteğe bağlı Proofpoint** yan, indirilen göndermek için ihtiyacınız **Certificate(Base64)**,**SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** için [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="865cc-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="865cc-173">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="865cc-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="865cc-174">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="865cc-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="865cc-175">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="865cc-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="865cc-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="865cc-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="865cc-177">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="865cc-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="865cc-179">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="865cc-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="865cc-180">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="865cc-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="865cc-182">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="865cc-182">These values are not the real.</span></span> <span data-ttu-id="865cc-183">Bu değerleri gerçek ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="865cc-183">Update these values with the actual</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="865cc-185">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="865cc-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="865cc-187">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="865cc-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="865cc-189">a.</span><span class="sxs-lookup"><span data-stu-id="865cc-189">a.</span></span> <span data-ttu-id="865cc-190">İçinde **adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="865cc-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="865cc-191">b.</span><span class="sxs-lookup"><span data-stu-id="865cc-191">b.</span></span> <span data-ttu-id="865cc-192">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="865cc-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="865cc-193">c.</span><span class="sxs-lookup"><span data-stu-id="865cc-193">c.</span></span> <span data-ttu-id="865cc-194">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="865cc-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="865cc-195">d.</span><span class="sxs-lookup"><span data-stu-id="865cc-195">d.</span></span> <span data-ttu-id="865cc-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="865cc-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="865cc-197">Bir Proofpoint üzerinde isteğe bağlı test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="865cc-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="865cc-198">Bu bölümde, Britta Simon Proofpoint isteğe bağlı olarak adlandırılan bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="865cc-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="865cc-199">Çalışmak [Proofpoint isteğe bağlı müşteri destek ekibi üzerinde](https://www.proofpoint.com/us/support-services) isteğe bağlı bir platformda Proofpoint kullanıcılar eklemek için.</span><span class="sxs-lookup"><span data-stu-id="865cc-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="865cc-200">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="865cc-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="865cc-201">Bu bölümde, isteğe bağlı Proofpoint için erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="865cc-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="865cc-203">**İsteğe bağlı Proofpoint Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="865cc-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="865cc-204">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="865cc-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="865cc-206">Uygulamalar listesinde **Proofpoint isteğe bağlı**.</span><span class="sxs-lookup"><span data-stu-id="865cc-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="865cc-208">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="865cc-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="865cc-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="865cc-210">Click **Add** button.</span></span> <span data-ttu-id="865cc-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="865cc-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="865cc-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="865cc-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="865cc-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="865cc-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="865cc-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="865cc-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="865cc-216">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="865cc-216">Testing single sign-on</span></span>

<span data-ttu-id="865cc-217">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="865cc-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="865cc-218">Tıkladığınızda **Proofpoint isteğe bağlı** döşeme erişim panelinde oturumunuz otomatik olarak isteğe bağlı uygulama üzerinde Proofpoint için.</span><span class="sxs-lookup"><span data-stu-id="865cc-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="865cc-219">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="865cc-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="865cc-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="865cc-220">Additional resources</span></span>

* [<span data-ttu-id="865cc-221">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="865cc-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="865cc-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="865cc-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

