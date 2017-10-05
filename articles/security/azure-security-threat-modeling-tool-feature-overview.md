---
title: "Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Tehdit modelleme aracında kullanılabilir tüm özellikler hakkında bilgi edinin"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 621ff305d7e782f85eeaae6c3fb02031673549c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="8d187-103">Tehdit modelleme aracı özelliğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="8d187-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="8d187-104">Biz gereksinimlerini modelleme, tehdit tehdit modelleme Aracı'nı kullanmak seçtiğiniz memnunuz!</span><span class="sxs-lookup"><span data-stu-id="8d187-104">We are glad you chose to use the Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="8d187-105">Bunu yapmadıysanız, ziyaret  **[tehdit modelleme aracı ile çalışmaya başlama](./azure-security-threat-modeling-tool-getting-started.md)**  temellerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8d187-105">If you haven’t done so, visit **[Getting Started with the Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** to learn the basics.</span></span>

> <span data-ttu-id="8d187-106">Aracımız sık sık güncelleştirilir, genellikle, en son özellikleri ve geliştirmeleri görmek için bu kılavuzu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="8d187-106">Our tool is updated often, so check this guide often to see our latest features and improvements.</span></span>

<span data-ttu-id="8d187-107">"Oluştur bir yeni Model" düğmesini tıklatarak aşağıdaki görüntü benzer boş başlangıç sayfasını açar:</span><span class="sxs-lookup"><span data-stu-id="8d187-107">Clicking on the "Create a New Model" button opens a blank start page, similar to the image below:</span></span>

![Boş başlangıç sayfası](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="8d187-109">Tehdit modeli kullanılarak oluşturulan bizim ekibi tarafından  **[Başlarken](./azure-security-threat-modeling-tool-getting-started.md)**  örnek, şimdi aracında kullanılabilir tüm özellikleri bugün göz atın.</span><span class="sxs-lookup"><span data-stu-id="8d187-109">Using the threat model created by our team in the **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all the features available in the tool today.</span></span>

![Temel tehdit modeli](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="8d187-111">Gezinme</span><span class="sxs-lookup"><span data-stu-id="8d187-111">Navigation</span></span>

<span data-ttu-id="8d187-112">İçinde yerleşik özellikler girmeden önce aracında bulunan ana bileşeni üzerinden edelim</span><span class="sxs-lookup"><span data-stu-id="8d187-112">Before diving into the built-in features, let’s go over the main components found in the tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="8d187-113">Menü öğeleri</span><span class="sxs-lookup"><span data-stu-id="8d187-113">Menu items</span></span>

<span data-ttu-id="8d187-114">Deneyimi diğer Microsoft ürünlerine benzer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8d187-114">The experience should be similar to other Microsoft products.</span></span> <span data-ttu-id="8d187-115">Üst düzey menü öğeleri arasında giderek başlayalım:</span><span class="sxs-lookup"><span data-stu-id="8d187-115">Let’s begin by going through the top-level menu items:</span></span>

![Menü öğeleri](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="8d187-117">Etiket</span><span class="sxs-lookup"><span data-stu-id="8d187-117">Label</span></span>                               | <span data-ttu-id="8d187-118">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8d187-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8d187-119">**Dosya**</span><span class="sxs-lookup"><span data-stu-id="8d187-119">**File**</span></span> | <ul><li><span data-ttu-id="8d187-120">Açın, kaydetme ve dosyaları kapatın</span><span class="sxs-lookup"><span data-stu-id="8d187-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="8d187-121">Oturum seçeneğinde OneDrive'nın hesapları</span><span class="sxs-lookup"><span data-stu-id="8d187-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="8d187-122">Paylaşım bağlantılar (Görünüm + Düzenle)</span><span class="sxs-lookup"><span data-stu-id="8d187-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="8d187-123">Dosya bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="8d187-123">View File Information</span></span></li><li><span data-ttu-id="8d187-124">Varolan modeli yeni şablonu Uygula</span><span class="sxs-lookup"><span data-stu-id="8d187-124">Apply New Template to Existing Models</span></span></li></ul> |
| <span data-ttu-id="8d187-125">**Düzenleme**</span><span class="sxs-lookup"><span data-stu-id="8d187-125">**Edit**</span></span> | <span data-ttu-id="8d187-126">Geri alma/Eylemler, iyi bir kopyalama, yapıştırma ve delete olarak yinele</span><span class="sxs-lookup"><span data-stu-id="8d187-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="8d187-127">**Görünümü**</span><span class="sxs-lookup"><span data-stu-id="8d187-127">**View**</span></span> | <ul><li><span data-ttu-id="8d187-128">Arasında geçiş **analiz** ve **tasarım** görünümleri</span><span class="sxs-lookup"><span data-stu-id="8d187-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="8d187-129">Açık kapalı windows (e.g.stencils, öğe özellikleri ve iletileri)</span><span class="sxs-lookup"><span data-stu-id="8d187-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="8d187-130">Düzen varsayılan ayarlarına sıfırlama</span><span class="sxs-lookup"><span data-stu-id="8d187-130">Reset layout to default settings</span></span></li></ul> |
| <span data-ttu-id="8d187-131">**Diyagramı**</span><span class="sxs-lookup"><span data-stu-id="8d187-131">**Diagram**</span></span> | <span data-ttu-id="8d187-132">Diyagramları ekleme/silme ve diyagramları "sekmeleri" arasında gidin</span><span class="sxs-lookup"><span data-stu-id="8d187-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="8d187-133">**Raporlar**</span><span class="sxs-lookup"><span data-stu-id="8d187-133">**Reports**</span></span> | <span data-ttu-id="8d187-134">Diğer kişilerle paylaşmak için HTML rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d187-134">Create HTML reports to share with others</span></span> |
| <span data-ttu-id="8d187-135">**Yardım**</span><span class="sxs-lookup"><span data-stu-id="8d187-135">**Help**</span></span> | <span data-ttu-id="8d187-136">Aracı'nı kullanmanıza yardımcı olmak için size yol gösterir</span><span class="sxs-lookup"><span data-stu-id="8d187-136">Guides to help you use the tool</span></span> |

<span data-ttu-id="8d187-137">Üst düzey menü kısayolları simgeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8d187-137">The icons are shortcuts for the top-level menus:</span></span>

| <span data-ttu-id="8d187-138">Simgesi</span><span class="sxs-lookup"><span data-stu-id="8d187-138">Icon</span></span>                               | <span data-ttu-id="8d187-139">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8d187-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8d187-140">**Açık**</span><span class="sxs-lookup"><span data-stu-id="8d187-140">**Open**</span></span> | <span data-ttu-id="8d187-141">Yeni bir dosya açar</span><span class="sxs-lookup"><span data-stu-id="8d187-141">Opens a new file</span></span> |
| <span data-ttu-id="8d187-142">**Kaydet**</span><span class="sxs-lookup"><span data-stu-id="8d187-142">**Save**</span></span> | <span data-ttu-id="8d187-143">Geçerli dosya kaydeder</span><span class="sxs-lookup"><span data-stu-id="8d187-143">Saves current file</span></span> |
| <span data-ttu-id="8d187-144">**Tasarım**</span><span class="sxs-lookup"><span data-stu-id="8d187-144">**Design**</span></span> | <span data-ttu-id="8d187-145">Tasarım görünümüne modelleri oluşturabileceğiniz gider</span><span class="sxs-lookup"><span data-stu-id="8d187-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="8d187-146">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="8d187-146">**Analyze**</span></span> | <span data-ttu-id="8d187-147">Tehditler ve bunların özelliklerini gösterir oluşturulan</span><span class="sxs-lookup"><span data-stu-id="8d187-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="8d187-148">**Diyagrama ekleyin**</span><span class="sxs-lookup"><span data-stu-id="8d187-148">**Add Diagram**</span></span> | <span data-ttu-id="8d187-149">Yeni Diyagram (Excel yeni sekmelerde benzer) ekler</span><span class="sxs-lookup"><span data-stu-id="8d187-149">Adds new diagram (similar to new tabs in Excel)</span></span> |
| <span data-ttu-id="8d187-150">**Diyagram Sil**</span><span class="sxs-lookup"><span data-stu-id="8d187-150">**Delete Diagram**</span></span> | <span data-ttu-id="8d187-151">Geçerli diyagram siler</span><span class="sxs-lookup"><span data-stu-id="8d187-151">Deletes current diagram</span></span> |
| <span data-ttu-id="8d187-152">**Kes/kopyala/yapıştır**</span><span class="sxs-lookup"><span data-stu-id="8d187-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="8d187-153">Keser/kopyaları/yapıştırır öğeleri</span><span class="sxs-lookup"><span data-stu-id="8d187-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="8d187-154">**Geri alma/yineleme**</span><span class="sxs-lookup"><span data-stu-id="8d187-154">**Undo/Redo**</span></span> | <span data-ttu-id="8d187-155">Eylemler alır/Yinele</span><span class="sxs-lookup"><span data-stu-id="8d187-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="8d187-156">**Yakınlaştırma / Uzaklaştır**</span><span class="sxs-lookup"><span data-stu-id="8d187-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="8d187-157">Ve daha iyi bir görünüm için diyagramı yakınlaştırır</span><span class="sxs-lookup"><span data-stu-id="8d187-157">Zooms in and out of the diagram for a better view</span></span> |
| <span data-ttu-id="8d187-158">**Geri Bildirim**</span><span class="sxs-lookup"><span data-stu-id="8d187-158">**Feedback**</span></span> | <span data-ttu-id="8d187-159">MSDN Forumu açar</span><span class="sxs-lookup"><span data-stu-id="8d187-159">Opens the MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="8d187-160">Tuvale</span><span class="sxs-lookup"><span data-stu-id="8d187-160">Canvas</span></span>

<span data-ttu-id="8d187-161">Burada, sürükleyip elemanlara alanı.</span><span class="sxs-lookup"><span data-stu-id="8d187-161">The space where you drag and drop elements into.</span></span> <span data-ttu-id="8d187-162">Sürükle ve bırak yoludur modelleri oluşturmak için hızlı ve en iyi yoldur.</span><span class="sxs-lookup"><span data-stu-id="8d187-162">Drag and drop is the quickest and most efficient way to build models.</span></span> <span data-ttu-id="8d187-163">Ayrıca, sağ tıklayın ve aşağıda gösterildiği gibi kullanmakta olduğunuz öğeleri genel sürümlerini ekler menüsünde seçin.</span><span class="sxs-lookup"><span data-stu-id="8d187-163">You may also right click and select from the menu, which adds generic versions of the elements you’re using, as shown below.</span></span>

#### <a name="dropping-the-stencil-on-the-canvas"></a><span data-ttu-id="8d187-164">Tuvalde şablon bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="8d187-164">Dropping the stencil on the canvas</span></span>

![Tuvale bırakma](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-the-stencil"></a><span data-ttu-id="8d187-166">Şablon üzerinde tıklatarak</span><span class="sxs-lookup"><span data-stu-id="8d187-166">Clicking on the stencil</span></span>

![Öğe özellikleri](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="8d187-168">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="8d187-168">Stencils</span></span>

<span data-ttu-id="8d187-169">Kullanılabilir tüm şablonlar bulabileceğiniz seçilen şablona dayalı.</span><span class="sxs-lookup"><span data-stu-id="8d187-169">Where you can find all stencils available to use based on the template selected.</span></span> <span data-ttu-id="8d187-170">Sağ öğeleri bulamazsanız, başka bir şablonu kullanmayı deneyin veya bir gereksinimlerinize uyacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8d187-170">If you can’t find the right elements, try using another template, or modify one to fit your needs.</span></span> <span data-ttu-id="8d187-171">Genellikle, kategoriler ve olanlar gibi bir birleşimini bulamıyor olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d187-171">Generally, you should be able to find a combination of categories like the ones below:</span></span>

| <span data-ttu-id="8d187-172">Şablon adı</span><span class="sxs-lookup"><span data-stu-id="8d187-172">Stencil Name</span></span>                               | <span data-ttu-id="8d187-173">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8d187-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8d187-174">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="8d187-174">**Process**</span></span> | <span data-ttu-id="8d187-175">Uygulamalar, tarayıcı eklentileri, iş parçacıkları, sanal makineler</span><span class="sxs-lookup"><span data-stu-id="8d187-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="8d187-176">**Dış etkileşen**</span><span class="sxs-lookup"><span data-stu-id="8d187-176">**External Interactor**</span></span> | <span data-ttu-id="8d187-177">Kimlik doğrulama sağlayıcıları, tarayıcıları, kullanıcılar, Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8d187-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="8d187-178">**Veri deposu**</span><span class="sxs-lookup"><span data-stu-id="8d187-178">**Data Store**</span></span> | <span data-ttu-id="8d187-179">Önbellek, depolama, yapılandırma dosyalarını, veritabanları, kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="8d187-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="8d187-180">**Veri akışı**</span><span class="sxs-lookup"><span data-stu-id="8d187-180">**Data Flow**</span></span> | <span data-ttu-id="8d187-181">İkili, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, adlandırılmış kanal, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="8d187-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="8d187-182">**Çizgi/Kenarlık sınır güven**</span><span class="sxs-lookup"><span data-stu-id="8d187-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="8d187-183">Şirket ağları, Internet, makine, korumalı alan, kullanıcı/çekirdek modu</span><span class="sxs-lookup"><span data-stu-id="8d187-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="8d187-184">Notlar/iletileri</span><span class="sxs-lookup"><span data-stu-id="8d187-184">Notes/Messages</span></span>

| <span data-ttu-id="8d187-185">Bileşen</span><span class="sxs-lookup"><span data-stu-id="8d187-185">Component</span></span>                               | <span data-ttu-id="8d187-186">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8d187-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8d187-187">**İletileri**</span><span class="sxs-lookup"><span data-stu-id="8d187-187">**Messages**</span></span> | <span data-ttu-id="8d187-188">Öğeler arasında hiçbir veri akışları gibi bir hata olduğunda kullanıcıları uyarır iç aracı mantığı</span><span class="sxs-lookup"><span data-stu-id="8d187-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="8d187-189">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="8d187-189">**Notes**</span></span> | <span data-ttu-id="8d187-190">Dosyaya mühendislik tasarımı ve gözden geçirme işlemi boyunca ekipleri tarafından eklenen el ile notları</span><span class="sxs-lookup"><span data-stu-id="8d187-190">Manual notes added to the file by engineering teams throughout the design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="8d187-191">Öğe özellikleri</span><span class="sxs-lookup"><span data-stu-id="8d187-191">Element properties</span></span>

<span data-ttu-id="8d187-192">Bunlar, seçili öğeler farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d187-192">These vary by the elements selected.</span></span> <span data-ttu-id="8d187-193">Güven sınırları dışında 3 genel seçimleri diğer tüm öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="8d187-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="8d187-194">Öğe özelliği</span><span class="sxs-lookup"><span data-stu-id="8d187-194">Element Property</span></span>                               | <span data-ttu-id="8d187-195">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8d187-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8d187-196">**Ad**</span><span class="sxs-lookup"><span data-stu-id="8d187-196">**Name**</span></span> | <span data-ttu-id="8d187-197">Yararlı, işlemler, depolar, interactors ve akışlar kolayca tanınması için adlandırma</span><span class="sxs-lookup"><span data-stu-id="8d187-197">Useful for naming your processes, stores, interactors and flows to be easily recognized</span></span> |
| <span data-ttu-id="8d187-198">**Kapsamının dışında**</span><span class="sxs-lookup"><span data-stu-id="8d187-198">**Out of Scope**</span></span> | <span data-ttu-id="8d187-199">Seçili olduğunda, öğe (önerilmez) tehdit nesil matris dışı alınır</span><span class="sxs-lookup"><span data-stu-id="8d187-199">If selected, the element is taken out of the threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="8d187-200">**Kapsam dışında nedeni**</span><span class="sxs-lookup"><span data-stu-id="8d187-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="8d187-201">Kapsam dışında neden bilmesini sağlamak üzere gerekçe alanları seçilmedi</span><span class="sxs-lookup"><span data-stu-id="8d187-201">Justification field to let users know why out of scope was selected</span></span> |

<span data-ttu-id="8d187-202">Özellikleri her öğe kategorisi altında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="8d187-202">Properties are changed under each element category.</span></span> <span data-ttu-id="8d187-203">Kullanılabilir seçenekler inceleyin veya daha fazla bilgi için şablon açmak için her öğesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8d187-203">Click on each element to inspect the available options, or open the template to learn more.</span></span> <span data-ttu-id="8d187-204">Şimdi özellikler alınamadı.</span><span class="sxs-lookup"><span data-stu-id="8d187-204">Let’s get into the features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="8d187-205">Hoş Geldiniz ekranı</span><span class="sxs-lookup"><span data-stu-id="8d187-205">Welcome screen</span></span>

<span data-ttu-id="8d187-206">Hoş Geldiniz ekranında uygulama açtığınızda gördüğünüz ilk şeydir.</span><span class="sxs-lookup"><span data-stu-id="8d187-206">The welcome screen is the first thing you see when you open the app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="8d187-207">Bir model açın</span><span class="sxs-lookup"><span data-stu-id="8d187-207">Open A model</span></span>

<span data-ttu-id="8d187-208">"Açık bir modeli" düğmenin üzerine getirildiğinde, 2 gizli seçeneklerini gösterir: "Dan bu bilgisayarı açma" ve "Aç onedrive"</span><span class="sxs-lookup"><span data-stu-id="8d187-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="8d187-209">İkinci, oturum açma işlemine aracılığıyla, OneDrive, başarılı bir kimlik doğrulamasından sonra dosya ve klasörleri seçmenize olanak sağlayan alır ancak ilk Dosya Aç ekranı açılır.</span><span class="sxs-lookup"><span data-stu-id="8d187-209">The first opens the File Open screen, while the second takes you through the sign in process for OneDrive, allowing you to pick folders and files after a successful authentication.</span></span>

![Açık modeli](./media/azure-security-threat-modeling-tool/openmodel.png)

![Bilgisayardan veya OneDrive Aç](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="8d187-212">Geri bildirim, öneriler ve sorunları</span><span class="sxs-lookup"><span data-stu-id="8d187-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="8d187-213">Bu seçeneğin belirlenmesi için SDL araçları MSDN Forumları olur.</span><span class="sxs-lookup"><span data-stu-id="8d187-213">Selecting this option will take you to the MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="8d187-214">Geçici çözümler ve yeni fikirleri dahil olmak üzere aracı hakkında başkalarının ne dediğini denetlemek için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="8d187-214">It’s a great way to check out what other people are saying about the tool, including workarounds and new ideas.</span></span>

![Geri Bildirim](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="8d187-216">Tasarım görünümü</span><span class="sxs-lookup"><span data-stu-id="8d187-216">Design view</span></span>

<span data-ttu-id="8d187-217">Her açın veya yeni bir model oluşturma Tasarım görünümüne gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="8d187-217">Whenever you open or create a new model, you’ll be taken to the design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="8d187-218">Öğeler ekleme</span><span class="sxs-lookup"><span data-stu-id="8d187-218">Adding elements</span></span>

<span data-ttu-id="8d187-219">Kılavuzda öğeler eklemek için 2 yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="8d187-219">There are 2 ways to add elements on the grid:</span></span>

- <span data-ttu-id="8d187-220">**Sürükleme ve bırakma** – İstenen öğe kılavuza sürükleyin ve ardından ek bilgi sağlamak için öğe özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d187-220">**Drag and Drop** – drag the desired element to the grid, then use the element properties to provide additional information.</span></span>
- <span data-ttu-id="8d187-221">**Sağ tıklayın** – sağ kılavuzda herhangi bir yere tıklayın ve açılan menüden seçin.</span><span class="sxs-lookup"><span data-stu-id="8d187-221">**Right Click** – right click anywhere on the grid and select from the dropdown menu.</span></span> <span data-ttu-id="8d187-222">Bu öğe genel bir gösterimini ekranında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8d187-222">A generic representation of that element will appear on the screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="8d187-223">Bağlama öğeleri</span><span class="sxs-lookup"><span data-stu-id="8d187-223">Connecting elements</span></span>

<span data-ttu-id="8d187-224">Öğeleri aracında bağlamak için 2 yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="8d187-224">There are 2 ways to connect elements in the tool:</span></span>

- <span data-ttu-id="8d187-225">**Sürükleme ve bırakma** – istenen veri akışı kılavuza sürükleyin ve uygun öğeleri için her iki ucuna bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8d187-225">**Drag and Drop** – drag the desired dataflow to the grid, and connect both ends to the appropriate elements.</span></span>
- <span data-ttu-id="8d187-226">**Shift + tıklayın** – (veri gönderme) ilk öğeyi tıklatın, tuşuna basın ve Shift tuşunu basılı tutun ve sonra da (veri alma) ikinci öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="8d187-226">**Click + Shift** – click on the first element (sending data), press and hold the Shift key, then select the second element (receiving data).</span></span> <span data-ttu-id="8d187-227">Sağ tıklatın ve "Bağlan" seçin</span><span class="sxs-lookup"><span data-stu-id="8d187-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="8d187-228">İki yönlü veri akışı kullanıyorsanız, sipariş gibi önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="8d187-228">If you’re using a bi-directional dataflow, the order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="8d187-229">Özellikler</span><span class="sxs-lookup"><span data-stu-id="8d187-229">Properties</span></span>

<span data-ttu-id="8d187-230">Diyagramda yerleştirilen şablonlar değiştirilebilir tüm özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d187-230">Shows all the properties that can be modified on the stencils placed in the diagram.</span></span> <span data-ttu-id="8d187-231">Özelliklerini görmek için şablon üzerinde tıklamanız yeterlidir ve bilgileri buna uygun olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="8d187-231">To see the properties, just click on the stencil and the information will be populated accordingly.</span></span> <span data-ttu-id="8d187-232">Aşağıdaki örnek, önce ve sonra "Şablon diyagram üzerine sürüklediğiniz bir veritabanı" gösterir:</span><span class="sxs-lookup"><span data-stu-id="8d187-232">The example below shows before and after a "Database" stencil is dragged onto the diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="8d187-233">Önce</span><span class="sxs-lookup"><span data-stu-id="8d187-233">Before</span></span>

![Önce](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="8d187-235">Sonra</span><span class="sxs-lookup"><span data-stu-id="8d187-235">After</span></span>

![Sonra](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="8d187-237">İletiler</span><span class="sxs-lookup"><span data-stu-id="8d187-237">Messages</span></span>

<span data-ttu-id="8d187-238">Bir tehdit modeli oluşturmak ve veri akışları öğelere bağlanmak unutursanız, ileti penceresinde hareket size bildirir. Yok sayın veya sorunu düzeltmek için yönergeleri izleyin seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d187-238">If you create a threat model and forget to connect data flows to elements, the message window notifies you to act. You can choose to ignore it or follow the instructions to fix the issue.</span></span> 

![İletiler](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="8d187-240">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d187-240">Notes</span></span>

<span data-ttu-id="8d187-241">İletileri sekmelerinden Notlar geçiş Notlar tüm düşüncelerinizi yakalamak için diyagrama eklemenize izin verir</span><span class="sxs-lookup"><span data-stu-id="8d187-241">Switching tabs from Messages to Notes allows you to add notes to your diagram to capture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="8d187-242">Analiz görünümü</span><span class="sxs-lookup"><span data-stu-id="8d187-242">Analysis view</span></span>

<span data-ttu-id="8d187-243">İşiniz bittiğinde, diyagram oluşturma, analiz görünümüne üst menü seçimleri gidip Büyüteç boyama palet yanındaki seçme geçebilir.</span><span class="sxs-lookup"><span data-stu-id="8d187-243">Once you're done building your diagram, switch over to analysis view by going to the top menu selections and choosing the magnifying glass next to the paint palette.</span></span>

![Analiz görünümü](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="8d187-245">Oluşturulan tehdit seçimi</span><span class="sxs-lookup"><span data-stu-id="8d187-245">Generated threat selection</span></span>

<span data-ttu-id="8d187-246">Üzerinde bir tehdit tıkladığınızda, üç benzersiz işlevler yararlanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8d187-246">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="8d187-247">Özellik</span><span class="sxs-lookup"><span data-stu-id="8d187-247">Feature</span></span>                               | <span data-ttu-id="8d187-248">Bilgi</span><span class="sxs-lookup"><span data-stu-id="8d187-248">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8d187-249">**Okuma göstergesi**</span><span class="sxs-lookup"><span data-stu-id="8d187-249">**Read Indicator**</span></span> | <p><span data-ttu-id="8d187-250">Tehdit şimdi kolayca zaten gittiğiniz aracılığıyla öğeleri izlemenize yardımcı olabilir okunur olarak işaretlendi</span><span class="sxs-lookup"><span data-stu-id="8d187-250">Threat is now marked as read, which can easily help you keep track of the items you already went through</span></span></p><p>![Okuma/okunmamış göstergesi](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="8d187-252">**Etkileşim odak**</span><span class="sxs-lookup"><span data-stu-id="8d187-252">**Interaction Focus**</span></span> | <p><span data-ttu-id="8d187-253">Tehdit vurgulanır ait diyagramdaki etkileşimi</span><span class="sxs-lookup"><span data-stu-id="8d187-253">Interaction in the diagram belonging to that threat is highlighted</span></span></p><p>![Etkileşim odak](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="8d187-255">**İş parçacığı özellikleri**</span><span class="sxs-lookup"><span data-stu-id="8d187-255">**Threat Properties**</span></span> | <p><span data-ttu-id="8d187-256">Tehdit hakkında ek bilgi tehdit Özellikler penceresinde doldurulur</span><span class="sxs-lookup"><span data-stu-id="8d187-256">Additional information about the threat is populated in the threat properties window</span></span></p><p>![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="8d187-258">Öncelik değiştirme</span><span class="sxs-lookup"><span data-stu-id="8d187-258">Priority change</span></span>

<span data-ttu-id="8d187-259">Oluşturulan her tehdit öncelik düzeyini değiştirme, yüksek, Orta ve düşük öncelik tehditleri tanımlamak kolaylaştırmak için kendi renkleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8d187-259">Changing the priority level of each generated threat also changes their colors to make it easy to identify high, medium and low priority threats.</span></span>

![Öncelik değiştirme](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="8d187-261">Tehdit özellikleri düzenlenebilir alanları</span><span class="sxs-lookup"><span data-stu-id="8d187-261">Threat properties editable fields</span></span>

<span data-ttu-id="8d187-262">Yukarıdaki resimde görüldüğü gibi kullanıcılar aracı tarafından oluşturulan bilgileri değiştirebilir bir gerekçe gibi bazı alanları ayrıca bilgi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d187-262">As seen in the image above, users can change the information generated by the tool an also add information to certain fields, such as justification.</span></span> <span data-ttu-id="8d187-263">Bu alanların şablon tarafından oluşturulan her tehdit için daha fazla bilgiye ihtiyacınız varsa, değişiklikler yapmak için kullanmaları için.</span><span class="sxs-lookup"><span data-stu-id="8d187-263">These fields are generated by the template, so if you need more information for each threat, you're encouraged to make modifications.</span></span>

![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="8d187-265">Reports</span><span class="sxs-lookup"><span data-stu-id="8d187-265">Reports</span></span>

<span data-ttu-id="8d187-266">Bir kez değişen öncelikleri işiniz bittiğinde ve oluşturulan her tehdit durumunu güncelleştirme, siz dosyayı kaydedin veya "Rapor" ve ardından "Tam rapor oluştur." giderek bir raporu yazdırma</span><span class="sxs-lookup"><span data-stu-id="8d187-266">Once you're done changing priorities and updating the status of each generated threat, you can save the file and/or print out a report by going to "Report" and then "Create Full Report."</span></span> <span data-ttu-id="8d187-267">Rapor adı istenir ve bunu yaptığınızda, aşağıdaki görüntü benzer bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d187-267">You'll be asked to name the report, and once you do, you should see something similar to the image below:</span></span>

![Rapor](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="8d187-269">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d187-269">Next steps</span></span>

<span data-ttu-id="8d187-270">Bir şablon için topluluğa katkıda bulunmak için lütfen Git bizim  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  sayfası.</span><span class="sxs-lookup"><span data-stu-id="8d187-270">To contribute a template for the community, please go to our **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="8d187-271">**[Karşıdan](https://aka.ms/tmtpreview)**  bugün başlamak için aracı.</span><span class="sxs-lookup"><span data-stu-id="8d187-271">**[Download](https://aka.ms/tmtpreview)** the tool to get started today.</span></span>
