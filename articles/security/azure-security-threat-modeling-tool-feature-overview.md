---
title: "aaaMicrosoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Merhaba tehdit modelleme aracı kullanılabilir tüm hello özellikler hakkında bilgi edinin"
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
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="a48d1-103">Tehdit modelleme aracı özelliğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="a48d1-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="a48d1-104">Biz toouse hello tehdit modelleme aracı gereksinimlerini modelleme, tehdit için seçtiğiniz memnunuz!</span><span class="sxs-lookup"><span data-stu-id="a48d1-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="a48d1-105">Bunu yapmadıysanız, ziyaret  **[hello tehdit modelleme aracı ile çalışmaya başlama](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn hello temelleri.</span><span class="sxs-lookup"><span data-stu-id="a48d1-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="a48d1-106">Aracımız sık sık güncelleştirilir, böylece bu denetleyin genellikle toosee bizim en son özellikleri ve geliştirmeleri Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="a48d1-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="a48d1-107">Merhaba "Oluşturmak bir yeni Model" düğmesini tıklatarak boş başlangıç sayfası, benzer toohello görüntünün altına açar:</span><span class="sxs-lookup"><span data-stu-id="a48d1-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Boş başlangıç sayfası](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="a48d1-109">Merhaba tehdit modeli kullanılarak oluşturulan ekibimiz hello içinde tarafından  **[Başlarken](./azure-security-threat-modeling-tool-getting-started.md)**  örnek, şimdi hello aracında kullanılabilir tüm hello özellikler bugün göz atın.</span><span class="sxs-lookup"><span data-stu-id="a48d1-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Temel tehdit modeli](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="a48d1-111">Gezinme</span><span class="sxs-lookup"><span data-stu-id="a48d1-111">Navigation</span></span>

<span data-ttu-id="a48d1-112">Merhaba yerleşik özellikleri girmeden önce hello aracında bulunan hello ana bileşeni üzerinden edelim</span><span class="sxs-lookup"><span data-stu-id="a48d1-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="a48d1-113">Menü öğeleri</span><span class="sxs-lookup"><span data-stu-id="a48d1-113">Menu items</span></span>

<span data-ttu-id="a48d1-114">Merhaba deneyimi benzer tooother Microsoft ürünleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a48d1-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="a48d1-115">Merhaba en üst düzey menü öğeleri arasında giderek başlayalım:</span><span class="sxs-lookup"><span data-stu-id="a48d1-115">Let’s begin by going through hello top-level menu items:</span></span>

![Menü öğeleri](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="a48d1-117">Etiket</span><span class="sxs-lookup"><span data-stu-id="a48d1-117">Label</span></span>                               | <span data-ttu-id="a48d1-118">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a48d1-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="a48d1-119">**Dosya**</span><span class="sxs-lookup"><span data-stu-id="a48d1-119">**File**</span></span> | <ul><li><span data-ttu-id="a48d1-120">Açın, kaydetme ve dosyaları kapatın</span><span class="sxs-lookup"><span data-stu-id="a48d1-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="a48d1-121">Oturum seçeneğinde OneDrive'nın hesapları</span><span class="sxs-lookup"><span data-stu-id="a48d1-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="a48d1-122">Paylaşım bağlantılar (Görünüm + Düzenle)</span><span class="sxs-lookup"><span data-stu-id="a48d1-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="a48d1-123">Dosya bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a48d1-123">View File Information</span></span></li><li><span data-ttu-id="a48d1-124">Yeni şablon tooExisting modelleri Uygula</span><span class="sxs-lookup"><span data-stu-id="a48d1-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="a48d1-125">**Düzenleme**</span><span class="sxs-lookup"><span data-stu-id="a48d1-125">**Edit**</span></span> | <span data-ttu-id="a48d1-126">Geri alma/Eylemler, iyi bir kopyalama, yapıştırma ve delete olarak yinele</span><span class="sxs-lookup"><span data-stu-id="a48d1-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="a48d1-127">**Görünümü**</span><span class="sxs-lookup"><span data-stu-id="a48d1-127">**View**</span></span> | <ul><li><span data-ttu-id="a48d1-128">Arasında geçiş **analiz** ve **tasarım** görünümleri</span><span class="sxs-lookup"><span data-stu-id="a48d1-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="a48d1-129">Açık kapalı windows (e.g.stencils, öğe özellikleri ve iletileri)</span><span class="sxs-lookup"><span data-stu-id="a48d1-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="a48d1-130">Düzen toodefault ayarlarını sıfırla</span><span class="sxs-lookup"><span data-stu-id="a48d1-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="a48d1-131">**Diyagramı**</span><span class="sxs-lookup"><span data-stu-id="a48d1-131">**Diagram**</span></span> | <span data-ttu-id="a48d1-132">Diyagramları ekleme/silme ve diyagramları "sekmeleri" arasında gidin</span><span class="sxs-lookup"><span data-stu-id="a48d1-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="a48d1-133">**Raporlar**</span><span class="sxs-lookup"><span data-stu-id="a48d1-133">**Reports**</span></span> | <span data-ttu-id="a48d1-134">HTML raporları tooshare başkalarıyla oluşturma</span><span class="sxs-lookup"><span data-stu-id="a48d1-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="a48d1-135">**Yardım**</span><span class="sxs-lookup"><span data-stu-id="a48d1-135">**Help**</span></span> | <span data-ttu-id="a48d1-136">Kılavuzlar toohelp hello aracını kullanın</span><span class="sxs-lookup"><span data-stu-id="a48d1-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="a48d1-137">Merhaba en üst düzey menü kısayolları Hello simgeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a48d1-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="a48d1-138">Simgesi</span><span class="sxs-lookup"><span data-stu-id="a48d1-138">Icon</span></span>                               | <span data-ttu-id="a48d1-139">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a48d1-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="a48d1-140">**Açık**</span><span class="sxs-lookup"><span data-stu-id="a48d1-140">**Open**</span></span> | <span data-ttu-id="a48d1-141">Yeni bir dosya açar</span><span class="sxs-lookup"><span data-stu-id="a48d1-141">Opens a new file</span></span> |
| <span data-ttu-id="a48d1-142">**Kaydet**</span><span class="sxs-lookup"><span data-stu-id="a48d1-142">**Save**</span></span> | <span data-ttu-id="a48d1-143">Geçerli dosya kaydeder</span><span class="sxs-lookup"><span data-stu-id="a48d1-143">Saves current file</span></span> |
| <span data-ttu-id="a48d1-144">**Tasarım**</span><span class="sxs-lookup"><span data-stu-id="a48d1-144">**Design**</span></span> | <span data-ttu-id="a48d1-145">Tasarım görünümüne modelleri oluşturabileceğiniz gider</span><span class="sxs-lookup"><span data-stu-id="a48d1-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="a48d1-146">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="a48d1-146">**Analyze**</span></span> | <span data-ttu-id="a48d1-147">Tehditler ve bunların özelliklerini gösterir oluşturulan</span><span class="sxs-lookup"><span data-stu-id="a48d1-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="a48d1-148">**Diyagrama ekleyin**</span><span class="sxs-lookup"><span data-stu-id="a48d1-148">**Add Diagram**</span></span> | <span data-ttu-id="a48d1-149">Yeni Diyagram (Excel'de benzer toonew sekmeleri) ekler</span><span class="sxs-lookup"><span data-stu-id="a48d1-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="a48d1-150">**Diyagram Sil**</span><span class="sxs-lookup"><span data-stu-id="a48d1-150">**Delete Diagram**</span></span> | <span data-ttu-id="a48d1-151">Geçerli diyagram siler</span><span class="sxs-lookup"><span data-stu-id="a48d1-151">Deletes current diagram</span></span> |
| <span data-ttu-id="a48d1-152">**Kes/kopyala/yapıştır**</span><span class="sxs-lookup"><span data-stu-id="a48d1-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="a48d1-153">Keser/kopyaları/yapıştırır öğeleri</span><span class="sxs-lookup"><span data-stu-id="a48d1-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="a48d1-154">**Geri alma/yineleme**</span><span class="sxs-lookup"><span data-stu-id="a48d1-154">**Undo/Redo**</span></span> | <span data-ttu-id="a48d1-155">Eylemler alır/Yinele</span><span class="sxs-lookup"><span data-stu-id="a48d1-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="a48d1-156">**Yakınlaştırma / Uzaklaştır**</span><span class="sxs-lookup"><span data-stu-id="a48d1-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="a48d1-157">Ve daha iyi bir görünüm için hello diyagramı yakınlaştırır</span><span class="sxs-lookup"><span data-stu-id="a48d1-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="a48d1-158">**Geri Bildirim**</span><span class="sxs-lookup"><span data-stu-id="a48d1-158">**Feedback**</span></span> | <span data-ttu-id="a48d1-159">Açılır hello MSDN Forumu</span><span class="sxs-lookup"><span data-stu-id="a48d1-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="a48d1-160">Tuvale</span><span class="sxs-lookup"><span data-stu-id="a48d1-160">Canvas</span></span>

<span data-ttu-id="a48d1-161">Burada, sürükleyip elemanlara hello alanı.</span><span class="sxs-lookup"><span data-stu-id="a48d1-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="a48d1-162">Sürükle ve bırak olan hello hızlı ve en verimli şekilde toobuild modeller.</span><span class="sxs-lookup"><span data-stu-id="a48d1-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="a48d1-163">Ayrıca, sağ tıklayın ve aşağıda gösterildiği gibi kullanmakta olduğunuz hello öğeleri genel sürümlerini ekler hello menüsünden seçin.</span><span class="sxs-lookup"><span data-stu-id="a48d1-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="a48d1-164">Merhaba şablon hello tuvalde bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="a48d1-164">Dropping hello stencil on hello canvas</span></span>

![Tuvale bırakma](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="a48d1-166">Merhaba şablonda tıklatarak</span><span class="sxs-lookup"><span data-stu-id="a48d1-166">Clicking on hello stencil</span></span>

![Öğe özellikleri](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="a48d1-168">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="a48d1-168">Stencils</span></span>

<span data-ttu-id="a48d1-169">Bulabileceğiniz burada tüm şablonlar seçili hello şablonunu temel alan kullanılabilir toouse.</span><span class="sxs-lookup"><span data-stu-id="a48d1-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="a48d1-170">Merhaba sağ öğeleri bulamazsanız, başka bir şablonu kullanmayı deneyin veya bir toofit gereksinimlerinizi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a48d1-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="a48d1-171">Genellikle, mümkün toofind kategoriler altında olanları hello gibi bir birleşimi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a48d1-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="a48d1-172">Şablon adı</span><span class="sxs-lookup"><span data-stu-id="a48d1-172">Stencil Name</span></span>                               | <span data-ttu-id="a48d1-173">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a48d1-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="a48d1-174">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="a48d1-174">**Process**</span></span> | <span data-ttu-id="a48d1-175">Uygulamalar, tarayıcı eklentileri, iş parçacıkları, sanal makineler</span><span class="sxs-lookup"><span data-stu-id="a48d1-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="a48d1-176">**Dış etkileşen**</span><span class="sxs-lookup"><span data-stu-id="a48d1-176">**External Interactor**</span></span> | <span data-ttu-id="a48d1-177">Kimlik doğrulama sağlayıcıları, tarayıcıları, kullanıcılar, Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a48d1-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="a48d1-178">**Veri deposu**</span><span class="sxs-lookup"><span data-stu-id="a48d1-178">**Data Store**</span></span> | <span data-ttu-id="a48d1-179">Önbellek, depolama, yapılandırma dosyalarını, veritabanları, kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="a48d1-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="a48d1-180">**Veri akışı**</span><span class="sxs-lookup"><span data-stu-id="a48d1-180">**Data Flow**</span></span> | <span data-ttu-id="a48d1-181">İkili, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, adlandırılmış kanal, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="a48d1-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="a48d1-182">**Çizgi/Kenarlık sınır güven**</span><span class="sxs-lookup"><span data-stu-id="a48d1-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="a48d1-183">Şirket ağları, Internet, makine, korumalı alan, kullanıcı/çekirdek modu</span><span class="sxs-lookup"><span data-stu-id="a48d1-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="a48d1-184">Notlar/iletileri</span><span class="sxs-lookup"><span data-stu-id="a48d1-184">Notes/Messages</span></span>

| <span data-ttu-id="a48d1-185">Bileşen</span><span class="sxs-lookup"><span data-stu-id="a48d1-185">Component</span></span>                               | <span data-ttu-id="a48d1-186">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a48d1-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="a48d1-187">**İletileri**</span><span class="sxs-lookup"><span data-stu-id="a48d1-187">**Messages**</span></span> | <span data-ttu-id="a48d1-188">Öğeler arasında hiçbir veri akışları gibi bir hata olduğunda kullanıcıları uyarır iç aracı mantığı</span><span class="sxs-lookup"><span data-stu-id="a48d1-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="a48d1-189">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="a48d1-189">**Notes**</span></span> | <span data-ttu-id="a48d1-190">El ile notları eklenen toohello dosyası mühendislik ekipleri tarafından baştan tasarım hello ve işlem gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="a48d1-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="a48d1-191">Öğe özellikleri</span><span class="sxs-lookup"><span data-stu-id="a48d1-191">Element properties</span></span>

<span data-ttu-id="a48d1-192">Bunlar, seçili hello öğeleri tarafından farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-192">These vary by hello elements selected.</span></span> <span data-ttu-id="a48d1-193">Güven sınırları dışında 3 genel seçimleri diğer tüm öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a48d1-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="a48d1-194">Öğe özelliği</span><span class="sxs-lookup"><span data-stu-id="a48d1-194">Element Property</span></span>                               | <span data-ttu-id="a48d1-195">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a48d1-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="a48d1-196">**Ad**</span><span class="sxs-lookup"><span data-stu-id="a48d1-196">**Name**</span></span> | <span data-ttu-id="a48d1-197">Kolay tanınan, işlemler, depolar, interactors ve akışlar toobe adlandırma yararlı</span><span class="sxs-lookup"><span data-stu-id="a48d1-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="a48d1-198">**Kapsamının dışında**</span><span class="sxs-lookup"><span data-stu-id="a48d1-198">**Out of Scope**</span></span> | <span data-ttu-id="a48d1-199">Seçili olduğunda, hello öğesi hello tehdit nesil matris (önerilmez) dışında alınır</span><span class="sxs-lookup"><span data-stu-id="a48d1-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="a48d1-200">**Kapsam dışında nedeni**</span><span class="sxs-lookup"><span data-stu-id="a48d1-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="a48d1-201">Doğrulama alanı toolet kullanıcılar kapsamının dışında seçilmedi neden bilmeniz</span><span class="sxs-lookup"><span data-stu-id="a48d1-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="a48d1-202">Özellikleri her öğe kategorisi altında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-202">Properties are changed under each element category.</span></span> <span data-ttu-id="a48d1-203">Öğesi her tooinspect hello kullanılabilir Seçenekler'i tıklatın veya daha fazla hello şablonu toolearn açın.</span><span class="sxs-lookup"><span data-stu-id="a48d1-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="a48d1-204">Şimdi hello özellikler alınamadı.</span><span class="sxs-lookup"><span data-stu-id="a48d1-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="a48d1-205">Hoş Geldiniz ekranı</span><span class="sxs-lookup"><span data-stu-id="a48d1-205">Welcome screen</span></span>

<span data-ttu-id="a48d1-206">Merhaba Hoş Geldiniz ekranı hello uygulama açtığınızda gördüğünüz hello ilk şeydir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="a48d1-207">Bir model açın</span><span class="sxs-lookup"><span data-stu-id="a48d1-207">Open A model</span></span>

<span data-ttu-id="a48d1-208">"Açık bir modeli" düğmenin üzerine getirildiğinde, 2 gizli seçeneklerini gösterir: "Dan bu bilgisayarı açma" ve "Aç onedrive"</span><span class="sxs-lookup"><span data-stu-id="a48d1-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="a48d1-209">Merhaba ikinci, hello oturum açma işlemine aracılığıyla OneDrive, başarılı bir kimlik doğrulamasından sonra toopick klasörleri ve dosyaları izin verme işlenirken hello hello Dosya Aç ekran, ilk açılır.</span><span class="sxs-lookup"><span data-stu-id="a48d1-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Açık modeli](./media/azure-security-threat-modeling-tool/openmodel.png)

![Bilgisayardan veya OneDrive Aç](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="a48d1-212">Geri bildirim, öneriler ve sorunları</span><span class="sxs-lookup"><span data-stu-id="a48d1-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="a48d1-213">Bu seçeneğin belirlenmesi için SDL araçları toohello MSDN Forumları olur.</span><span class="sxs-lookup"><span data-stu-id="a48d1-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="a48d1-214">Geçici çözümler ve yeni fikirleri gibi hello aracı hakkında başkalarının ne dediğini çıkışı mükemmel şekilde toocheck olur.</span><span class="sxs-lookup"><span data-stu-id="a48d1-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Geri Bildirim](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="a48d1-216">Tasarım görünümü</span><span class="sxs-lookup"><span data-stu-id="a48d1-216">Design view</span></span>

<span data-ttu-id="a48d1-217">Her açın veya yeni bir model oluşturma toohello Tasarım görünümüne gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="a48d1-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="a48d1-218">Öğeler ekleme</span><span class="sxs-lookup"><span data-stu-id="a48d1-218">Adding elements</span></span>

<span data-ttu-id="a48d1-219">Merhaba kılavuzda tooadd öğeleri 2 yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="a48d1-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="a48d1-220">**Sürükleme ve bırakma** – hello İstenen öğe toohello kılavuz sürükleyin sonra hello öğe özellikleri tooprovide ek bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a48d1-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="a48d1-221">**Sağ tıklayın** – sağ hello kılavuz üzerinde herhangi bir yere tıklayın ve hello açılır menüsünden seçin.</span><span class="sxs-lookup"><span data-stu-id="a48d1-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="a48d1-222">Bu öğe genel bir gösterimini Merhaba ekranında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="a48d1-223">Bağlama öğeleri</span><span class="sxs-lookup"><span data-stu-id="a48d1-223">Connecting elements</span></span>

<span data-ttu-id="a48d1-224">Merhaba aracında tooconnect öğeleri 2 yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="a48d1-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="a48d1-225">**Sürükleme ve bırakma** – hello istenen veri akışı toohello kılavuz sürükleyin ve her iki uca toohello uygun öğeleri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a48d1-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="a48d1-226">**Shift + tıklayın** – (veri gönderme) hello ilk öğesini tıklatın, basılı hello SHIFT tuşunu sonra select hello ikinci öğesi (veri alma).</span><span class="sxs-lookup"><span data-stu-id="a48d1-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="a48d1-227">Sağ tıklatın ve "Bağlan" seçin</span><span class="sxs-lookup"><span data-stu-id="a48d1-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="a48d1-228">İki yönlü veri akışı kullanıyorsanız, hello sırası gibi önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="a48d1-229">Özellikler</span><span class="sxs-lookup"><span data-stu-id="a48d1-229">Properties</span></span>

<span data-ttu-id="a48d1-230">Merhaba şemada yerleştirilen hello şablonlar değiştirilebilir tüm hello özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="a48d1-231">toosee hello özellikler, yalnızca hello şablonda tıklayın ve hello bilgileri buna uygun olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="a48d1-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="a48d1-232">önce ve sonra "Şablon hello diyagram üzerine sürüklediğiniz bir veritabanı" Merhaba örnekte gösterilir:</span><span class="sxs-lookup"><span data-stu-id="a48d1-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="a48d1-233">Önce</span><span class="sxs-lookup"><span data-stu-id="a48d1-233">Before</span></span>

![Önce](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="a48d1-235">Sonra</span><span class="sxs-lookup"><span data-stu-id="a48d1-235">After</span></span>

![Sonra](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="a48d1-237">İletiler</span><span class="sxs-lookup"><span data-stu-id="a48d1-237">Messages</span></span>

<span data-ttu-id="a48d1-238">Merhaba ileti penceresinde bir tehdit modeli oluşturmak ve tooelements tooconnect veri akışları unutursanız, tooact bildirir.</span><span class="sxs-lookup"><span data-stu-id="a48d1-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="a48d1-239">Tooignore veya izleyin seçebilirsiniz hello yönergeleri toofix hello sorun.</span><span class="sxs-lookup"><span data-stu-id="a48d1-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![İletiler](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="a48d1-241">Notlar</span><span class="sxs-lookup"><span data-stu-id="a48d1-241">Notes</span></span>

<span data-ttu-id="a48d1-242">İletileri tooNotes sekmelerinden değiştirme, tooadd notları tooyour diyagramı toocapture tüm düşüncelerinizi sağlar</span><span class="sxs-lookup"><span data-stu-id="a48d1-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="a48d1-243">Analiz görünümü</span><span class="sxs-lookup"><span data-stu-id="a48d1-243">Analysis view</span></span>

<span data-ttu-id="a48d1-244">İşiniz bittiğinde, diyagram oluşturma, tooanalysis görünüm giderek toohello üst menü seçimlerini ve hello Büyüteç sonraki toohello boyama paleti seçme geçiş.</span><span class="sxs-lookup"><span data-stu-id="a48d1-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Analiz görünümü](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="a48d1-246">Oluşturulan tehdit seçimi</span><span class="sxs-lookup"><span data-stu-id="a48d1-246">Generated threat selection</span></span>

<span data-ttu-id="a48d1-247">Üzerinde bir tehdit tıkladığınızda, üç benzersiz işlevler yararlanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a48d1-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="a48d1-248">Özellik</span><span class="sxs-lookup"><span data-stu-id="a48d1-248">Feature</span></span>                               | <span data-ttu-id="a48d1-249">Bilgi</span><span class="sxs-lookup"><span data-stu-id="a48d1-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="a48d1-250">**Okuma göstergesi**</span><span class="sxs-lookup"><span data-stu-id="a48d1-250">**Read Indicator**</span></span> | <p><span data-ttu-id="a48d1-251">Tehdit şimdi kolayca zaten gittiğiniz aracılığıyla hello öğeleri izlemenize yardımcı olabilir okunur olarak işaretlendi</span><span class="sxs-lookup"><span data-stu-id="a48d1-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Okuma/okunmamış göstergesi](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="a48d1-253">**Etkileşim odak**</span><span class="sxs-lookup"><span data-stu-id="a48d1-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="a48d1-254">Etkileşim toothat tehdit ait hello diyagramındaki vurgulanmış</span><span class="sxs-lookup"><span data-stu-id="a48d1-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Etkileşim odak](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="a48d1-256">**İş parçacığı özellikleri**</span><span class="sxs-lookup"><span data-stu-id="a48d1-256">**Threat Properties**</span></span> | <p><span data-ttu-id="a48d1-257">Merhaba tehdit Özellikler penceresinde hello tehdit hakkında ek bilgi doldurulur</span><span class="sxs-lookup"><span data-stu-id="a48d1-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="a48d1-259">Öncelik değiştirme</span><span class="sxs-lookup"><span data-stu-id="a48d1-259">Priority change</span></span>

<span data-ttu-id="a48d1-260">Oluşturulan her tehdit Hello öncelik düzeyini değiştirme de kendi renkleri toomake değiştirir, kolay tooidentify yüksek, Orta ve düşük öncelik tehditleri.</span><span class="sxs-lookup"><span data-stu-id="a48d1-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Öncelik değiştirme](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="a48d1-262">Tehdit özellikleri düzenlenebilir alanları</span><span class="sxs-lookup"><span data-stu-id="a48d1-262">Threat properties editable fields</span></span>

<span data-ttu-id="a48d1-263">Yukarıdaki Hello resimde görüldüğü gibi kullanıcılar hello aracı tarafından oluşturulan hello bilgilerini değiştirebilir bir ayrıca gerekçe gibi bilgi toocertain alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a48d1-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="a48d1-264">Bu alanların hello şablon tarafından oluşturulan her tehdit için daha fazla bilgiye ihtiyacınız varsa, kullanmaları toomake değişiklikleri olacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="a48d1-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="a48d1-266">Reports</span><span class="sxs-lookup"><span data-stu-id="a48d1-266">Reports</span></span>

<span data-ttu-id="a48d1-267">Değişen öncelikleri işiniz bittiğinde ve tehdit her güncelleştirme hello durumunu oluşturulan sonra siz hello dosyasını kaydedin veya çok "rapor" giderek ve ardından "tam rapor oluştur." bir raporu yazdırın</span><span class="sxs-lookup"><span data-stu-id="a48d1-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="a48d1-268">Tooname hello rapor istenir ve bunu yaptığınızda, aşağıdaki benzeri toohello görüntü görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a48d1-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Rapor](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="a48d1-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a48d1-270">Next steps</span></span>

<span data-ttu-id="a48d1-271">Lütfen gidin tooour toocontribute hello topluluk için bir şablon  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  sayfası.</span><span class="sxs-lookup"><span data-stu-id="a48d1-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="a48d1-272">**[Karşıdan](https://aka.ms/tmtpreview)**  hello aracı tooget kullanmaya bugün.</span><span class="sxs-lookup"><span data-stu-id="a48d1-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
