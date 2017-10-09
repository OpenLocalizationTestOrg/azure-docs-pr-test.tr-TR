---
title: aaaPrerequisites tooaccess hello Azure AD raporlama API'si. | Microsoft Belgeleri
description: "Merhaba Önkoşullar tooaccess hello Azure AD raporlama API'si hakkında bilgi edinin"
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="e4411-104">Önkoşullar tooaccess hello Azure AD raporlama API'si</span><span class="sxs-lookup"><span data-stu-id="e4411-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="e4411-105">Merhaba [API'leri raporlama Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello verilerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e4411-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="e4411-106">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4411-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="e4411-107">API kullandığı raporlama hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize erişim toohello web API'leri.</span><span class="sxs-lookup"><span data-stu-id="e4411-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="e4411-108">tooprepare raporlama API'si, erişim toohello yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4411-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="e4411-109">Azure AD kiracınızda uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4411-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="e4411-110">Azure AD Veri GRANT hello uygulama uygun izinleri tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="e4411-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="e4411-111">Yapılandırma ayarları dizininizden toplayın</span><span class="sxs-lookup"><span data-stu-id="e4411-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="e4411-112">Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e4411-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="e4411-113">Azure AD uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="e4411-113">Create an Azure AD application</span></span>
<span data-ttu-id="e4411-114">tooconfigure, dizin tooaccess hello Azure AD raporlama API'si, toohello Klasik Azure portalı, aynı zamanda Azure AD kiracınızda hello genel yönetici dizin rolünün bir üyesi olan bir Azure aboneliği yönetici hesabıyla oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4411-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4411-115">Bu gibi "Yönetici" ayrıcalıkları olan kimlik bilgileri altında çalışan uygulamalar çok güçlü olabilir, bu nedenle lütfen emin tookeep hello uygulamanın kimliği/parola kimlik bilgileri güvenli.</span><span class="sxs-lookup"><span data-stu-id="e4411-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="e4411-116">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4411-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="e4411-118">Merhaba gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="e4411-119">Hello içinde hello üst menüsünde **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e4411-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="e4411-121">Merhaba alt çubuğunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e4411-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="e4411-123">Merhaba üzerinde **neler toodo istediğiniz?** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e4411-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="e4411-125">Merhaba üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4411-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="e4411-127">a.</span><span class="sxs-lookup"><span data-stu-id="e4411-127">a.</span></span> <span data-ttu-id="e4411-128">Merhaba, **adı** metin kutusuna, bir ad yazın (örneğin: Reporting API uygulaması).</span><span class="sxs-lookup"><span data-stu-id="e4411-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="e4411-129">b.</span><span class="sxs-lookup"><span data-stu-id="e4411-129">b.</span></span> <span data-ttu-id="e4411-130">Seçin **Web uygulaması ve/veya web API'si**.</span><span class="sxs-lookup"><span data-stu-id="e4411-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="e4411-131">c.</span><span class="sxs-lookup"><span data-stu-id="e4411-131">c.</span></span> <span data-ttu-id="e4411-132">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4411-132">Click **Next**.</span></span>
7. <span data-ttu-id="e4411-133">Merhaba üzerinde **uygulama özellikleri** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4411-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="e4411-135">a.</span><span class="sxs-lookup"><span data-stu-id="e4411-135">a.</span></span> <span data-ttu-id="e4411-136">Merhaba, **oturum açma URL'si** metin kutusuna, türü `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e4411-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="e4411-137">b.</span><span class="sxs-lookup"><span data-stu-id="e4411-137">b.</span></span> <span data-ttu-id="e4411-138">Merhaba, **uygulama kimliği URI'si** metin kutusuna, türü ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="e4411-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="e4411-139">c.</span><span class="sxs-lookup"><span data-stu-id="e4411-139">c.</span></span> <span data-ttu-id="e4411-140">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4411-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="e4411-141">Uygulama izni toouse hello API verin</span><span class="sxs-lookup"><span data-stu-id="e4411-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="e4411-142">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4411-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="e4411-144">Merhaba gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="e4411-145">Hello içinde hello üst menüsünde **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e4411-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="e4411-147">Merhaba uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-147">In hello applications list, select your newly created application.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="e4411-149">Hello içinde hello üst menüsünde **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="e4411-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="e4411-151">Merhaba, **izinleri tooother uygulamaları** hello için bölüm **Azure Active Directory** kaynak hello tıklatın **uygulama izinleri** aşağı açılan listesinde ve ardından seçin **dizin verilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="e4411-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="e4411-153">Merhaba alt çubuğunda **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e4411-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="e4411-155">Yapılandırma ayarları dizininizden toplayın</span><span class="sxs-lookup"><span data-stu-id="e4411-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="e4411-156">Bu bölümde, nasıl gösterilir dizininizden ayarları aşağıdaki tooget hello:</span><span class="sxs-lookup"><span data-stu-id="e4411-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="e4411-157">Etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="e4411-157">Domain name</span></span>
* <span data-ttu-id="e4411-158">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="e4411-158">Client ID</span></span>
* <span data-ttu-id="e4411-159">Gizli anahtar</span><span class="sxs-lookup"><span data-stu-id="e4411-159">Client secret</span></span>

<span data-ttu-id="e4411-160">Bu değerleri çağrıları toohello raporlama API yapılandırırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4411-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="e4411-161">Etki alanı adınızı alma</span><span class="sxs-lookup"><span data-stu-id="e4411-161">Get your domain name</span></span>
1. <span data-ttu-id="e4411-162">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4411-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="e4411-164">Merhaba gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="e4411-165">Hello içinde hello üst menüsünde **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="e4411-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="e4411-167">Merhaba, **etki alanı adı** sütun, etki alanı adınızı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e4411-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="e4411-169">Merhaba uygulamanın istemci kimliği alın</span><span class="sxs-lookup"><span data-stu-id="e4411-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="e4411-170">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4411-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="e4411-172">Merhaba gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="e4411-173">Hello içinde hello üst menüsünde **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e4411-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="e4411-175">Merhaba uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-175">In hello applications list, select your newly created application.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="e4411-177">Hello içinde hello üst menüsünde **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="e4411-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="e4411-179">Kopyalama, **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="e4411-179">Copy your **Client ID**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="e4411-181">Merhaba uygulamanın istemci parolası mı almak</span><span class="sxs-lookup"><span data-stu-id="e4411-181">Get hello application's client secret</span></span>
<span data-ttu-id="e4411-182">tooget uygulamanızın istemci gizli, toocreate yeni bir anahtar gerekir ve bu değer daha sonra artık olası tooretrieve olmadığından hello yeni anahtarı kaydetme sırasında değerini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e4411-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="e4411-183">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4411-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="e4411-185">Merhaba gelen **active directory** listesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="e4411-186">Hello içinde hello üst menüsünde **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e4411-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="e4411-188">Merhaba uygulamalar listesinde yeni oluşturulan uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4411-188">In hello applications list, select your newly created application.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="e4411-190">Hello içinde hello üst menüsünde **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="e4411-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="e4411-192">Merhaba, **anahtarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4411-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="e4411-194">a.</span><span class="sxs-lookup"><span data-stu-id="e4411-194">a.</span></span> <span data-ttu-id="e4411-195">Merhaba süre listesinden bir süre seçin</span><span class="sxs-lookup"><span data-stu-id="e4411-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="e4411-196">b.</span><span class="sxs-lookup"><span data-stu-id="e4411-196">b.</span></span> <span data-ttu-id="e4411-197">Merhaba alt çubuğunda **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e4411-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="e4411-199">c.</span><span class="sxs-lookup"><span data-stu-id="e4411-199">c.</span></span> <span data-ttu-id="e4411-200">Merhaba anahtar değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e4411-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4411-201">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e4411-201">Next Steps</span></span>
* <span data-ttu-id="e4411-202">, Tooaccess hello Azure AD verilerden hello gibi raporlama API programlı bir şekilde?</span><span class="sxs-lookup"><span data-stu-id="e4411-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="e4411-203">Kullanıma [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e4411-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="e4411-204">Merhaba toofind Azure Active Directory raporlama hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e4411-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

