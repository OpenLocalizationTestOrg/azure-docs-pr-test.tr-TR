---
title: aaaPrerequisites tooaccess hello Azure AD raporlama API'si | Microsoft Docs
description: "Merhaba Önkoşullar tooaccess hello Azure AD raporlama API'si hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="dcfbe-103">Önkoşullar tooaccess hello Azure AD raporlama API'si</span><span class="sxs-lookup"><span data-stu-id="dcfbe-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="dcfbe-104">Merhaba [API'leri raporlama Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello verilerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="dcfbe-105">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="dcfbe-106">API kullandığı raporlama hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize erişim toohello web API'leri.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="dcfbe-107">tooget erişim toohello raporlama verileri hello API aracılığıyla, toohave atanan rollerin aşağıdaki hello biri gerekir:</span><span class="sxs-lookup"><span data-stu-id="dcfbe-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="dcfbe-108">Güvenlik okuyucusu</span><span class="sxs-lookup"><span data-stu-id="dcfbe-108">Security Reader</span></span>
- <span data-ttu-id="dcfbe-109">Güvenlik Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="dcfbe-109">Security Admin</span></span>
- <span data-ttu-id="dcfbe-110">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="dcfbe-110">Global Admin</span></span>


<span data-ttu-id="dcfbe-111">tooprepare raporlama API'si, erişim toohello yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="dcfbe-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="dcfbe-112">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="dcfbe-112">Register an application</span></span> 
2. <span data-ttu-id="dcfbe-113">İzinleri</span><span class="sxs-lookup"><span data-stu-id="dcfbe-113">Grant permissions</span></span> 
3. <span data-ttu-id="dcfbe-114">Yapılandırma ayarlarını toplayın</span><span class="sxs-lookup"><span data-stu-id="dcfbe-114">Gather configuration settings</span></span> 

<span data-ttu-id="dcfbe-115">Sorularınız, sorunları veya Geri bildiriminiz için lütfen [bir destek bileti dosya](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="dcfbe-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="dcfbe-116">Bir Azure Active Directory uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="dcfbe-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="dcfbe-117">Bir komut dosyası kullanarak API raporlama hello erişiyorsanız bile tooregister uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="dcfbe-118">Bu size verir bir **uygulama kimliği**, yetkilendirme çağrısı için gerekli olduğu ve kod tooreceive belirteçleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="dcfbe-119">tooconfigure dizin tooaccess hello Azure AD raporlama API'nizi, Azure portalı, aynı zamanda hello üyesi olan Azure yönetici hesabı ile toohello içinde imzalamalısınız **genel yönetici** Azure AD kiracınızda dizin rolü .</span><span class="sxs-lookup"><span data-stu-id="dcfbe-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcfbe-120">Bu gibi "Yönetici" ayrıcalıkları olan kimlik bilgileri altında çalışan uygulamalar çok güçlü olabilir, bu nedenle lütfen emin tookeep hello uygulamanın kimliği/parola kimlik bilgileri güvenli.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="dcfbe-121">**bir Azure Active Directory uygulaması tooregister:**</span><span class="sxs-lookup"><span data-stu-id="dcfbe-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="dcfbe-122">Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dcfbe-124">Merhaba üzerinde **Azure Active Directory** dikey penceresinde tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="dcfbe-126">Merhaba üzerinde **uygulama kayıtlar** hello araç çubuğunda hello üstte dikey tıklayın **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="dcfbe-128">Merhaba üzerinde **oluşturma** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dcfbe-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="dcfbe-130">a.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-130">a.</span></span> <span data-ttu-id="dcfbe-131">Merhaba, **adı** metin kutusuna, türü `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="dcfbe-132">b.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-132">b.</span></span> <span data-ttu-id="dcfbe-133">Olarak **uygulama türü**seçin **Web uygulaması / API**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="dcfbe-134">c.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-134">c.</span></span> <span data-ttu-id="dcfbe-135">Merhaba, **oturum açma URL'si** metin kutusuna, türü `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="dcfbe-136">d.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-136">d.</span></span> <span data-ttu-id="dcfbe-137">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="dcfbe-138">İzinleri</span><span class="sxs-lookup"><span data-stu-id="dcfbe-138">Grant permissions</span></span> 

<span data-ttu-id="dcfbe-139">Merhaba amacı, bu adımı uygulamanız toogrant olan **dizin verilerini okuma** izinleri toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="dcfbe-141">**toogrant, API uygulama izni toouse hello:**</span><span class="sxs-lookup"><span data-stu-id="dcfbe-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="dcfbe-142">Merhaba üzerinde **uygulama kayıtlar** hello uygulamalar listesinde, dikey tıklayın **raporlama API'si uygulama**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="dcfbe-143">Merhaba üzerinde **raporlama API'si uygulama** hello araç çubuğunda hello üstte dikey tıklayın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="dcfbe-145">Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="dcfbe-147">Merhaba üzerinde **gerekli izinleri** dikey penceresinde hello **API** tıklatın **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="dcfbe-149">Merhaba üzerinde **erişimi etkinleştir** dikey penceresinde, select **dizin verilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="dcfbe-151">Merhaba üstte Hello araç çubuğunda **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="dcfbe-153">Yapılandırma ayarlarını toplayın</span><span class="sxs-lookup"><span data-stu-id="dcfbe-153">Gather configuration settings</span></span> 
<span data-ttu-id="dcfbe-154">Bu bölümde, nasıl gösterilir dizininizden ayarları aşağıdaki tooget hello:</span><span class="sxs-lookup"><span data-stu-id="dcfbe-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="dcfbe-155">Etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="dcfbe-155">Domain name</span></span>
* <span data-ttu-id="dcfbe-156">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="dcfbe-156">Client ID</span></span>
* <span data-ttu-id="dcfbe-157">Gizli anahtar</span><span class="sxs-lookup"><span data-stu-id="dcfbe-157">Client secret</span></span>

<span data-ttu-id="dcfbe-158">Bu değerleri çağrıları toohello raporlama API yapılandırırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="dcfbe-159">Etki alanı adınızı alma</span><span class="sxs-lookup"><span data-stu-id="dcfbe-159">Get your domain name</span></span>

<span data-ttu-id="dcfbe-160">**tooget etki alanı adınızı:**</span><span class="sxs-lookup"><span data-stu-id="dcfbe-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="dcfbe-161">Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dcfbe-163">Merhaba üzerinde **Azure Active Directory** dikey penceresinde tıklatın **etki alanı adları**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="dcfbe-165">Etki alanı adınızı hello etki alanları listesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="dcfbe-166">Uygulamanızın istemci kimliği alın</span><span class="sxs-lookup"><span data-stu-id="dcfbe-166">Get your application's client ID</span></span>

<span data-ttu-id="dcfbe-167">**tooget uygulamanızın istemci kimliği:**</span><span class="sxs-lookup"><span data-stu-id="dcfbe-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="dcfbe-168">Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dcfbe-170">Merhaba üzerinde **uygulama kayıtlar** hello uygulamalar listesinde, dikey tıklayın **raporlama API'si uygulama**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="dcfbe-171">Merhaba üzerinde **raporlama API'si uygulama** dikey penceresine, hello **uygulama kimliği**,'ı tıklatın **tıklatın toocopy**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="dcfbe-173">Uygulamanızın istemci parolası mı almak</span><span class="sxs-lookup"><span data-stu-id="dcfbe-173">Get your application's client secret</span></span>
<span data-ttu-id="dcfbe-174">tooget uygulamanızın istemci gizli, toocreate yeni bir anahtar gerekir ve bu değer daha sonra artık olası tooretrieve olmadığından hello yeni anahtarı kaydetme sırasında değerini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="dcfbe-175">**tooget uygulamanızın istemci parolası:**</span><span class="sxs-lookup"><span data-stu-id="dcfbe-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="dcfbe-176">Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dcfbe-178">Merhaba üzerinde **uygulama kayıtlar** hello uygulamalar listesinde, dikey tıklayın **raporlama API'si uygulama**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="dcfbe-179">Merhaba üzerinde **raporlama API'si uygulama** hello araç çubuğunda hello üstte dikey tıklayın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="dcfbe-181">Merhaba üzerinde **ayarları** dikey penceresinde hello **APIR erişim** 'yi tıklatın **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="dcfbe-183">Merhaba üzerinde **anahtarları** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dcfbe-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="dcfbe-185">a.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-185">a.</span></span> <span data-ttu-id="dcfbe-186">Merhaba, **açıklama** metin kutusuna, türü `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="dcfbe-187">b.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-187">b.</span></span> <span data-ttu-id="dcfbe-188">Olarak **Expires**seçin **2 yıl içinde**.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="dcfbe-189">c.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-189">c.</span></span> <span data-ttu-id="dcfbe-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-190">Click **Save**.</span></span>

    <span data-ttu-id="dcfbe-191">d.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-191">d.</span></span> <span data-ttu-id="dcfbe-192">Merhaba anahtar değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dcfbe-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dcfbe-193">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="dcfbe-193">Next Steps</span></span>
* <span data-ttu-id="dcfbe-194">, Tooaccess hello Azure AD verilerden hello gibi raporlama API programlı bir şekilde?</span><span class="sxs-lookup"><span data-stu-id="dcfbe-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="dcfbe-195">Kullanıma [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcfbe-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="dcfbe-196">Merhaba toofind Azure Active Directory raporlama hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="dcfbe-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

