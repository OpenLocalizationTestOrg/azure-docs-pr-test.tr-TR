---
title: "Öğretici: Azure Active Directory Tümleştirme Pasifik zaman çizelgesi ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Pasifik zaman çizelgesi arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: fda06c340430d19bea035a2cab2f318fe8a5998c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="727fe-103">Öğretici: Azure Active Directory Tümleştirme ile Pasifik zaman çizelgesi</span><span class="sxs-lookup"><span data-stu-id="727fe-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="727fe-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Pasifik zaman çizelgesi tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="727fe-104">In this tutorial, you learn how to integrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="727fe-105">Pasifik zaman çizelgesi Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="727fe-105">Integrating Pacific Timesheet with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="727fe-106">Pasifik zaman çizelgesi erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="727fe-106">You can control in Azure AD who has access to Pacific Timesheet</span></span>
- <span data-ttu-id="727fe-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) Pasifik çizelgesine açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="727fe-107">You can enable your users to automatically get signed-on to Pacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="727fe-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="727fe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="727fe-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="727fe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="727fe-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="727fe-110">Prerequisites</span></span>

<span data-ttu-id="727fe-111">Azure AD tümleştirme Pasifik zaman çizelgesi ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="727fe-111">To configure Azure AD integration with Pacific Timesheet, you need the following items:</span></span>

- <span data-ttu-id="727fe-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="727fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="727fe-113">Bir Pasifik zaman çizelgesi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="727fe-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="727fe-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="727fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="727fe-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="727fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="727fe-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="727fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="727fe-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="727fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="727fe-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="727fe-118">Scenario description</span></span>
<span data-ttu-id="727fe-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="727fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="727fe-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="727fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="727fe-121">Galeriden Pasifik zaman çizelgesi ekleme</span><span class="sxs-lookup"><span data-stu-id="727fe-121">Adding Pacific Timesheet from the gallery</span></span>
2. <span data-ttu-id="727fe-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="727fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-the-gallery"></a><span data-ttu-id="727fe-123">Galeriden Pasifik zaman çizelgesi ekleme</span><span class="sxs-lookup"><span data-stu-id="727fe-123">Adding Pacific Timesheet from the gallery</span></span>
<span data-ttu-id="727fe-124">Azure AD Pasifik zaman çizelgesi tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Pasifik zaman çizelgesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="727fe-124">To configure the integration of Pacific Timesheet into Azure AD, you need to add Pacific Timesheet from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="727fe-125">**Galeriden Pasifik zaman çizelgesi eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="727fe-125">**To add Pacific Timesheet from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="727fe-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="727fe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="727fe-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="727fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="727fe-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="727fe-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="727fe-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="727fe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="727fe-133">Arama kutusuna **Pasifik zaman çizelgesi**.</span><span class="sxs-lookup"><span data-stu-id="727fe-133">In the search box, type **Pacific Timesheet**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="727fe-135">Sonuçlar panelinde seçin **Pasifik zaman çizelgesi**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="727fe-135">In the results panel, select **Pacific Timesheet**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="727fe-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="727fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="727fe-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Pasifik "Britta Simon" adlı bir test kullanıcıyı temel alarak zaman çizelgesi ile test etme.</span><span class="sxs-lookup"><span data-stu-id="727fe-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="727fe-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Pasifik çizelgesinde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="727fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pacific Timesheet is to a user in Azure AD.</span></span> <span data-ttu-id="727fe-140">Diğer bir deyişle, bir Azure AD kullanıcısının Pasifik zaman çizelgesi ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="727fe-140">In other words, a link relationship between an Azure AD user and the related user in Pacific Timesheet needs to be established.</span></span>

<span data-ttu-id="727fe-141">Değeri Pasifik çizelgesinde atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="727fe-141">In Pacific Timesheet, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="727fe-142">Yapılandırma ve Azure AD çoklu oturum açma Pasifik zaman çizelgesi ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="727fe-142">To configure and test Azure AD single sign-on with Pacific Timesheet, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="727fe-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="727fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="727fe-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="727fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="727fe-145">**[Pasifik zaman çizelgesi test kullanıcısı oluşturma](#creating-a-pacific-timesheet-test-user)**  - Britta Simon, karşılık gelen Pasifik kullanıcı Azure AD gösterimini bağlantılı zaman çizelgesi sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="727fe-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - to have a counterpart of Britta Simon in Pacific Timesheet that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="727fe-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="727fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="727fe-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="727fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="727fe-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="727fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="727fe-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Pasifik zaman çizelgesi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="727fe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="727fe-150">**Azure AD çoklu oturum açma Pasifik zaman çizelgesi ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="727fe-150">**To configure Azure AD single sign-on with Pacific Timesheet, perform the following steps:**</span></span>

1. <span data-ttu-id="727fe-151">Azure portalında üzerinde **Pasifik zaman çizelgesi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="727fe-151">In the Azure portal, on the **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="727fe-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="727fe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="727fe-155">Üzerinde **Pasifik zaman çizelgesi etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="727fe-155">On the **Pacific Timesheet Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="727fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="727fe-157">a.</span></span> <span data-ttu-id="727fe-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="727fe-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="727fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="727fe-159">b.</span></span> <span data-ttu-id="727fe-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="727fe-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="727fe-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="727fe-161">These values are not real.</span></span> <span data-ttu-id="727fe-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="727fe-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="727fe-163">Kişi [Pasifik zaman çizelgesi destek ekibi](http://www.pacifictimesheet.com/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="727fe-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to get these values.</span></span>
 
4. <span data-ttu-id="727fe-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="727fe-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="727fe-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="727fe-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="727fe-168">Üzerinde **Pasifik zaman çizelgesi yapılandırma** 'yi tıklatın **Pasifik zaman çizelgesi yapılandırmak** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="727fe-168">On the **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** to open **Configure sign-on** window.</span></span> <span data-ttu-id="727fe-169">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="727fe-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="727fe-171">Çoklu oturum açma yapılandırmak için **Pasifik zaman çizelgesi** yan, indirilen göndermek için ihtiyacınız **sertifika (Base64)**, **SAML çoklu oturum açma hizmet URL'si**ve **SAML varlık kimliği** için [Pasifik zaman çizelgesi destek ekibi](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="727fe-171">To configure single sign-on on **Pacific Timesheet** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="727fe-172">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="727fe-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="727fe-173">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="727fe-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="727fe-174">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="727fe-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="727fe-175">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="727fe-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="727fe-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="727fe-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="727fe-177">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="727fe-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="727fe-179">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="727fe-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="727fe-180">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="727fe-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="727fe-182">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="727fe-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="727fe-184">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="727fe-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="727fe-186">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="727fe-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="727fe-188">a.</span><span class="sxs-lookup"><span data-stu-id="727fe-188">a.</span></span> <span data-ttu-id="727fe-189">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="727fe-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="727fe-190">b.</span><span class="sxs-lookup"><span data-stu-id="727fe-190">b.</span></span> <span data-ttu-id="727fe-191">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="727fe-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="727fe-192">c.</span><span class="sxs-lookup"><span data-stu-id="727fe-192">c.</span></span> <span data-ttu-id="727fe-193">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="727fe-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="727fe-194">d.</span><span class="sxs-lookup"><span data-stu-id="727fe-194">d.</span></span> <span data-ttu-id="727fe-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="727fe-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="727fe-196">Pasifik zaman çizelgesi test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="727fe-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="727fe-197">Bu bölümde, Pasifik zaman çizelgesinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="727fe-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="727fe-198">Çalışmak [Pasifik zaman çizelgesi destek ekibi](http://www.pacifictimesheet.com/support) uygulamada bir kullanıcı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="727fe-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to create a user in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="727fe-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="727fe-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="727fe-200">Bu bölümde, Britta Pasifik zaman çizelgesine erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="727fe-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pacific Timesheet.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="727fe-202">**Pasifik zaman çizelgesine Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="727fe-202">**To assign Britta Simon to Pacific Timesheet, perform the following steps:**</span></span>

1. <span data-ttu-id="727fe-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="727fe-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="727fe-205">Uygulamalar listesinde **Pasifik zaman çizelgesi**.</span><span class="sxs-lookup"><span data-stu-id="727fe-205">In the applications list, select **Pacific Timesheet**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="727fe-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="727fe-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="727fe-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="727fe-209">Click **Add** button.</span></span> <span data-ttu-id="727fe-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="727fe-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="727fe-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="727fe-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="727fe-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="727fe-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="727fe-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="727fe-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="727fe-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="727fe-215">Testing single sign-on</span></span>

<span data-ttu-id="727fe-216">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="727fe-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="727fe-217">Erişim paneli Pasifik zaman çizelgesi parçasında tıklattığınızda, otomatik olarak Pasifik zaman çizelgesi uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="727fe-217">When you click the Pacific Timesheet tile in the Access Panel, you should get automatically signed-on to your Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="727fe-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="727fe-218">Additional resources</span></span>

* [<span data-ttu-id="727fe-219">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="727fe-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="727fe-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="727fe-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

