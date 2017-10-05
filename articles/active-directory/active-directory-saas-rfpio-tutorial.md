---
title: "Öğretici: Azure Active Directory Tümleştirme ile RFPIO | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile RFPIO arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="83041-103">Öğretici: Azure Active Directory Tümleştirme RFPIO ile</span><span class="sxs-lookup"><span data-stu-id="83041-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="83041-104">Bu öğreticide, Azure Active Directory (Azure AD) ile RFPIO tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="83041-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83041-105">RFPIO Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="83041-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83041-106">Denetleyebilirsiniz kimin RFPIO erişimi, Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="83041-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="83041-107">Otomatik olarak için RFPIO (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83041-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="83041-108">Hesaplarınızı bir merkezi konumda--Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="83041-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="83041-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83041-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83041-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83041-110">Prerequisites</span></span>

<span data-ttu-id="83041-111">Azure AD tümleştirme RFPIO ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="83041-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="83041-112">Bir Azure AD abonelik.</span><span class="sxs-lookup"><span data-stu-id="83041-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="83041-113">RFPIO tek bir oturum üzerinde etkin olmayan abonelik.</span><span class="sxs-lookup"><span data-stu-id="83041-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="83041-114">Bu öğreticide adımları test etmek için bir üretim ortamında kullanmanızı öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="83041-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="83041-115">Bu öğreticide adımları test etmek için aşağıdaki önerileri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="83041-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="83041-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="83041-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="83041-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83041-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83041-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="83041-118">Scenario description</span></span>
<span data-ttu-id="83041-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="83041-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83041-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="83041-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83041-121">RFPIO Galeriden ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="83041-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="83041-122">Yapılandırma ve Azure AD sınama çoklu oturum açmayı.</span><span class="sxs-lookup"><span data-stu-id="83041-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="83041-123">Galeriden RFPIO Ekle</span><span class="sxs-lookup"><span data-stu-id="83041-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="83041-124">Azure AD RFPIO tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden RFPIO eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="83041-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="83041-125">Galeriden RFPIO eklemek için</span><span class="sxs-lookup"><span data-stu-id="83041-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="83041-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti bölmesinde seçin **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="83041-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83041-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="83041-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="83041-130">Yeni bir uygulama eklemek için seçin **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="83041-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="83041-132">Arama kutusuna **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="83041-132">In the search box, type **RFPIO**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="83041-134">Sonuçlar panelinde seçin **RFPIO**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="83041-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="83041-136">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="83041-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="83041-137">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı RFPIO sınayın.</span><span class="sxs-lookup"><span data-stu-id="83041-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83041-138">Tekli çalışmaya oturum için Azure AD RFPIO karşılık gelen kullanıcı Azure AD'de kullanıcı arasındaki ilişki nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="83041-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="83041-139">Diğer bir deyişle, bir Azure AD kullanıcısının RFPIO ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="83041-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="83041-140">RFPIO içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="83041-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83041-141">Yapılandırma ve Azure AD çoklu oturum açma RFPIO ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="83041-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83041-142">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**--bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="83041-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83041-143">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**--Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="83041-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83041-144">**[RFPIO test kullanıcısı oluşturma](#creating-a-rfpio-test-user)**  --Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı RFPIO sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="83041-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83041-145">**[Azure AD test kullanıcısı atayın](#assigning-the-azure-ad-test-user)**--Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="83041-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83041-146">**[Test çoklu oturum açma](#testing-single-sign-on)**  --yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="83041-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="83041-147">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="83041-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="83041-148">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma RFPIO uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="83041-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="83041-149">**Azure AD çoklu oturum açma ile RFPIO yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="83041-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="83041-150">Azure portalında üzerinde **RFPIO** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="83041-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="83041-152">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="83041-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="83041-154">Üzerinde **RFPIO etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="83041-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="83041-156">a.</span><span class="sxs-lookup"><span data-stu-id="83041-156">a.</span></span> <span data-ttu-id="83041-157">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="83041-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="83041-159">b.</span><span class="sxs-lookup"><span data-stu-id="83041-159">b.</span></span> <span data-ttu-id="83041-160">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="83041-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="83041-161">c.</span><span class="sxs-lookup"><span data-stu-id="83041-161">c.</span></span> <span data-ttu-id="83041-162">İçinde **geçiş durumunu** metin kutusuna bir dize değeri girin.</span><span class="sxs-lookup"><span data-stu-id="83041-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="83041-163">Kişi [RFPIO destek ekibi](https://www.rfpio.com/contact/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="83041-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="83041-164">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="83041-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="83041-165">Uygulamada yapılandırmak istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="83041-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="83041-167">İçinde **URL üzerinde oturum** metin kutusuna, URL'yi yazın:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="83041-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="83041-168">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="83041-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="83041-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="83041-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="83041-172">Farklı bir web tarayıcı penceresinde, oturum açma **RFPIO** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="83041-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="83041-173">Alt Sol Köşe açılan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="83041-173">Click on the bottom left corner dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="83041-175">Tıklayın **kuruluş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="83041-175">Click on the **Organization Settings**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="83041-177">Tıklayın **özellikler ve tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="83041-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="83041-179">İçinde **SAML SSO yapılandırma** tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="83041-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="83041-181">Bu bölümde aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="83041-181">In this Section perform following actions:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="83041-183">a.</span><span class="sxs-lookup"><span data-stu-id="83041-183">a.</span></span> <span data-ttu-id="83041-184">İçeriği Kopyala **indirilen meta veri XML** ve yapıştırın **kimlik Yapılandırması** alan.</span><span class="sxs-lookup"><span data-stu-id="83041-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="83041-185">İndirilen içeriği kopyalamak için **meta veri XML** kullanım **not defteri ++** veya uygun **XML Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="83041-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="83041-186">b.</span><span class="sxs-lookup"><span data-stu-id="83041-186">b.</span></span> <span data-ttu-id="83041-187">Tıklatın **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="83041-187">Click **Validate**.</span></span>

    <span data-ttu-id="83041-188">c.</span><span class="sxs-lookup"><span data-stu-id="83041-188">c.</span></span> <span data-ttu-id="83041-189">' I tıklattıktan sonra **doğrulamak**Çevir, **SAML(Enabled)** için açık.</span><span class="sxs-lookup"><span data-stu-id="83041-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="83041-190">d.</span><span class="sxs-lookup"><span data-stu-id="83041-190">d.</span></span> <span data-ttu-id="83041-191">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="83041-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="83041-192">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="83041-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83041-193">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="83041-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83041-194">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83041-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="83041-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="83041-195">Create an Azure AD test user</span></span>
<span data-ttu-id="83041-196">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="83041-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="83041-198">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="83041-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83041-199">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="83041-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83041-201">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="83041-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83041-203">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="83041-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83041-205">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="83041-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83041-207">a.</span><span class="sxs-lookup"><span data-stu-id="83041-207">a.</span></span> <span data-ttu-id="83041-208">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83041-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83041-209">b.</span><span class="sxs-lookup"><span data-stu-id="83041-209">b.</span></span> <span data-ttu-id="83041-210">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="83041-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83041-211">c.</span><span class="sxs-lookup"><span data-stu-id="83041-211">c.</span></span> <span data-ttu-id="83041-212">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="83041-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83041-213">d.</span><span class="sxs-lookup"><span data-stu-id="83041-213">d.</span></span> <span data-ttu-id="83041-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83041-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="83041-215">RFPIO test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="83041-215">Create a RFPIO test user</span></span>

<span data-ttu-id="83041-216">Azure AD kullanıcıları için RFPIO oturum açmak etkinleştirmek için bunların RFPIO sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83041-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="83041-217">RFPIO söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="83041-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="83041-218">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="83041-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="83041-219">RFPIO şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="83041-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="83041-220">Alt Sol Köşe açılan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="83041-220">Click on the bottom left corner dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="83041-222">Tıklayın **kuruluş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="83041-222">Click on the **Organization Settings**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="83041-224">Tıklatın **ekip ÜYELERİNİN**.</span><span class="sxs-lookup"><span data-stu-id="83041-224">Click **TEAM MEMBERS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="83041-226">Tıklayın **ÜYELER Ekle**.</span><span class="sxs-lookup"><span data-stu-id="83041-226">Click on **ADD MEMBERS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="83041-228">İçinde **eklediğiniz yeni üyeler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="83041-228">In the **Add New Members** section.</span></span> <span data-ttu-id="83041-229">Aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="83041-229">Perform following actions:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="83041-231">a.</span><span class="sxs-lookup"><span data-stu-id="83041-231">a.</span></span> <span data-ttu-id="83041-232">ENTER **e-posta adresi** içinde **satır başına bir e-posta girin** alan.</span><span class="sxs-lookup"><span data-stu-id="83041-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="83041-233">b.</span><span class="sxs-lookup"><span data-stu-id="83041-233">b.</span></span> <span data-ttu-id="83041-234">Lütfen seçin **rol** gereksinimlerinize göre.</span><span class="sxs-lookup"><span data-stu-id="83041-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="83041-235">c.</span><span class="sxs-lookup"><span data-stu-id="83041-235">c.</span></span> <span data-ttu-id="83041-236">Tıklatın **ÜYELER Ekle**.</span><span class="sxs-lookup"><span data-stu-id="83041-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="83041-237">Azure Active Directory hesap sahibi bir e-posta alır ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izler.</span><span class="sxs-lookup"><span data-stu-id="83041-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="83041-238">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="83041-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="83041-239">Bu bölümde, Britta RFPIO için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="83041-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="83041-241">**RFPIO için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="83041-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="83041-242">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="83041-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="83041-244">Uygulamalar listesinde **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="83041-244">In the applications list, select **RFPIO**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="83041-246">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="83041-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="83041-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="83041-248">Click **Add** button.</span></span> <span data-ttu-id="83041-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="83041-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="83041-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="83041-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83041-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="83041-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83041-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="83041-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="83041-254">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="83041-254">Test single sign-on</span></span>

<span data-ttu-id="83041-255">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="83041-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="83041-256">Erişim paneli RFPIO parçasında tıklattığınızda, otomatik olarak RFPIO uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="83041-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="83041-257">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="83041-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83041-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="83041-258">Additional resources</span></span>

* [<span data-ttu-id="83041-259">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile ilgili öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="83041-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83041-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="83041-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

