---
title: "Azure AD raporlama API'si erişmek için Önkoşullar. | Microsoft Belgeleri"
description: "Azure AD raporlama API'si erişmek için önkoşullar hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="04816-104">Azure AD raporlama API'si erişmek için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="04816-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="04816-105">[API'leri raporlama Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) verilere bir dizi REST tabanlı API'ler aracılığıyla programlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="04816-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="04816-106">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04816-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="04816-107">Raporlama API kullandığı [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) web API'leri erişim yetkisi vermek için.</span><span class="sxs-lookup"><span data-stu-id="04816-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="04816-108">Raporlama API erişiminizi hazırlamak için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="04816-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="04816-109">Azure AD kiracınızda uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="04816-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="04816-110">Azure AD verilere erişmek için uygulama uygun izinleri verin</span><span class="sxs-lookup"><span data-stu-id="04816-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="04816-111">Yapılandırma ayarları dizininizden toplayın</span><span class="sxs-lookup"><span data-stu-id="04816-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="04816-112">Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="04816-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="04816-113">Azure AD uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="04816-113">Create an Azure AD application</span></span>
<span data-ttu-id="04816-114">Azure AD raporlama API'si erişmek için dizininize yapılandırmak için Azure Klasik portalı, aynı zamanda Azure AD kiracınızda genel yönetici dizin rolünün bir üyesi olan bir Azure aboneliği yönetici hesabıyla oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="04816-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04816-115">Bu gibi "Yönetici" ayrıcalıkları olan kimlik bilgileri altında çalışan uygulamalar çok güçlü olabilir, bu nedenle Lütfen uygulamanın kimliği/parola kimlik bilgileri güvenli tutmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="04816-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="04816-116">İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04816-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="04816-118">Gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="04816-119">Üstteki menüde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="04816-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="04816-121">Alt çubuğunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="04816-121">On the bottom bar, click **Add**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="04816-123">Üzerinde **ne yapmak istiyorsunuz?** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="04816-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="04816-125">Üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="04816-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="04816-127">a.</span><span class="sxs-lookup"><span data-stu-id="04816-127">a.</span></span> <span data-ttu-id="04816-128">İçinde **adı** metin kutusuna, bir ad yazın (örneğin: Reporting API uygulaması).</span><span class="sxs-lookup"><span data-stu-id="04816-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="04816-129">b.</span><span class="sxs-lookup"><span data-stu-id="04816-129">b.</span></span> <span data-ttu-id="04816-130">Seçin **Web uygulaması ve/veya web API'si**.</span><span class="sxs-lookup"><span data-stu-id="04816-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="04816-131">c.</span><span class="sxs-lookup"><span data-stu-id="04816-131">c.</span></span> <span data-ttu-id="04816-132">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04816-132">Click **Next**.</span></span>
7. <span data-ttu-id="04816-133">Üzerinde **uygulama özellikleri** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="04816-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="04816-135">a.</span><span class="sxs-lookup"><span data-stu-id="04816-135">a.</span></span> <span data-ttu-id="04816-136">İçinde **oturum açma URL'si** metin kutusuna, türü `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="04816-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="04816-137">b.</span><span class="sxs-lookup"><span data-stu-id="04816-137">b.</span></span> <span data-ttu-id="04816-138">İçinde **uygulama kimliği URI'si** metin kutusuna, türü ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="04816-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="04816-139">c.</span><span class="sxs-lookup"><span data-stu-id="04816-139">c.</span></span> <span data-ttu-id="04816-140">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04816-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="04816-141">Uygulama API kullanma izni verin</span><span class="sxs-lookup"><span data-stu-id="04816-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="04816-142">İçinde [Klasik Azure portalı](https://manage.windowsazure.com/), sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04816-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="04816-144">Gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="04816-145">Üstteki menüde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="04816-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="04816-147">Uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-147">In the applications list, select your newly created application.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="04816-149">Üstteki menüde tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="04816-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="04816-151">İçinde **diğer uygulamalara izinler** bölümünde için **Azure Active Directory** kaynak tıklatın **uygulama izinleri** aşağı açılan listeyi ve ardından **dizin verilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="04816-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="04816-153">Alt çubuğunda **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="04816-153">On the bottom bar, click **Save**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="04816-155">Yapılandırma ayarları dizininizden toplayın</span><span class="sxs-lookup"><span data-stu-id="04816-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="04816-156">Bu bölüm, aşağıdaki ayarları dizininizden alma gösterir:</span><span class="sxs-lookup"><span data-stu-id="04816-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="04816-157">Etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="04816-157">Domain name</span></span>
* <span data-ttu-id="04816-158">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="04816-158">Client ID</span></span>
* <span data-ttu-id="04816-159">Gizli anahtar</span><span class="sxs-lookup"><span data-stu-id="04816-159">Client secret</span></span>

<span data-ttu-id="04816-160">Raporlama API çağrıları yapılandırırken bu değerleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="04816-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="04816-161">Etki alanı adınızı alma</span><span class="sxs-lookup"><span data-stu-id="04816-161">Get your domain name</span></span>
1. <span data-ttu-id="04816-162">İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04816-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="04816-164">Gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="04816-165">Üstteki menüde tıklatın **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="04816-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="04816-167">İçinde **etki alanı adı** sütun, etki alanı adınızı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="04816-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="04816-169">Uygulamanın istemci kimliği alın</span><span class="sxs-lookup"><span data-stu-id="04816-169">Get the application's client ID</span></span>
1. <span data-ttu-id="04816-170">İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04816-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="04816-172">Gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="04816-173">Üstteki menüde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="04816-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="04816-175">Uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-175">In the applications list, select your newly created application.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="04816-177">Üstteki menüde tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="04816-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="04816-179">Kopyalama, **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="04816-179">Copy your **Client ID**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="04816-181">Uygulamanın istemci parolası mı almak</span><span class="sxs-lookup"><span data-stu-id="04816-181">Get the application's client secret</span></span>
<span data-ttu-id="04816-182">Uygulamanızın istemci parolası mı almak için yeni bir anahtar oluşturun ve bu değer daha sonra artık almak mümkün olmadığı için yeni anahtarı kaydetme sırasında değerini kaydedin gerekir.</span><span class="sxs-lookup"><span data-stu-id="04816-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="04816-183">İçinde [Klasik Azure portalı](https://manage.windowsazure.com), sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04816-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="04816-185">Gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="04816-186">Üstteki menüde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="04816-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="04816-188">Uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="04816-188">In the applications list, select your newly created application.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="04816-190">Üstteki menüde tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="04816-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="04816-192">İçinde **anahtarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="04816-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="04816-194">a.</span><span class="sxs-lookup"><span data-stu-id="04816-194">a.</span></span> <span data-ttu-id="04816-195">Bir süre süre listesinden seçin</span><span class="sxs-lookup"><span data-stu-id="04816-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="04816-196">b.</span><span class="sxs-lookup"><span data-stu-id="04816-196">b.</span></span> <span data-ttu-id="04816-197">Alt çubuğunda **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="04816-197">On the bottom bar, click **Save**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="04816-199">c.</span><span class="sxs-lookup"><span data-stu-id="04816-199">c.</span></span> <span data-ttu-id="04816-200">Anahtar değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="04816-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04816-201">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="04816-201">Next Steps</span></span>
* <span data-ttu-id="04816-202">Verileri Azure AD raporlama API'si programlı bir şekilde erişmek ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="04816-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="04816-203">Kullanıma [Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="04816-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="04816-204">Azure Active Directory raporlama hakkında daha fazla bilgi edinmek istiyorsanız, bkz: [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="04816-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

