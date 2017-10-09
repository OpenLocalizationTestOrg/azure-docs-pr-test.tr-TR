---
title: "aaaSave arar ve Azure veri Kataloğu'nda PIN veri varlıkları | Microsoft Docs"
description: "Veri kaynakları ve daha sonra kullanmak için veri varlıklarını kaydetme nasıl tooarticle vurgulama yetenekleri Azure veri Kataloğu'nda."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="fc118-103">Azure veri Kataloğu'nda arama ve PIN veri varlıklarını kaydetme</span><span class="sxs-lookup"><span data-stu-id="fc118-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="fc118-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="fc118-104">Introduction</span></span>
<span data-ttu-id="fc118-105">Azure veri Kataloğu, veri kaynağı bulma için yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc118-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="fc118-106">Hızlı bir şekilde arayın ve da hello katalog toolocate veri kaynakları filtre ve amaçlarının, elinizdeki hello işi için daha kolay toofind hello doğru verilerin sağlama anlama.</span><span class="sxs-lookup"><span data-stu-id="fc118-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="fc118-107">Ancak tooregularly ihtiyacınız yoksa ne hello ile aynı iş veri?</span><span class="sxs-lookup"><span data-stu-id="fc118-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="fc118-108">Ve ne sizin ve diğer kullanıcıların düzenli olarak bilgi toohello katkıda hello katalog aynı veri kaynaklarında?</span><span class="sxs-lookup"><span data-stu-id="fc118-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="fc118-109">Bu durumda, aynı hello toorepeatedly sorun yaşıyor aramaları verimsiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc118-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="fc118-110">Kayıtlı arama ve sabitlenmiş veri varlıkları olduğu yardımcı olabilir budur.</span><span class="sxs-lookup"><span data-stu-id="fc118-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="fc118-111">Kaydedilen aramalar</span><span class="sxs-lookup"><span data-stu-id="fc118-111">Saved searches</span></span>
<span data-ttu-id="fc118-112">Veri Kataloğu'nda kaydedilmiş bir aramayı bir yeniden kullanılabilir, kullanıcı başına arama tanımıdır.</span><span class="sxs-lookup"><span data-stu-id="fc118-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="fc118-113">Arama terimleri, etiketler ve diğer filtreleri gibi bir arama tanımlamak ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fc118-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="fc118-114">Kaydedilen hello arama tanımı yeniden çalıştırabilirsiniz sonraki tooreturn kendi arama ölçütleriyle eşleşen hiçbir veri varlıklarını.</span><span class="sxs-lookup"><span data-stu-id="fc118-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="fc118-115">Kaydedilmiş bir aramayı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc118-115">Create a saved search</span></span>
<span data-ttu-id="fc118-116">toocreate kaydedilmiş bir aramayı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="fc118-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="fc118-117">Hello Azure veri Kataloğu portalında, hello **geçerli aramayı** penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fc118-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Geçerli arama ayarları Kaydet bağlantısı](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="fc118-119">Tooreuse istediğiniz ve ardından hello arama ölçütlerini girin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fc118-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Kaydedilen arama adı geçerli arama ayarları](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="fc118-121">İstendiğinde, kaydedilmiş aramayı hello için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="fc118-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="fc118-122">Anlamlı bir ad seçin ve hello araması tarafından döndürülen hello veri varlıklarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="fc118-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="fc118-123">Kaydedilmiş aramaları Yönet</span><span class="sxs-lookup"><span data-stu-id="fc118-123">Manage saved searches</span></span>
<span data-ttu-id="fc118-124">Bir veya daha fazla aramalar, kaydettiğiniz sonra bir **kayıtlı aramaları** seçeneği hello altında görüntülenen **geçerli aramayı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fc118-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="fc118-125">Merhaba listesi genişletildiğinde tüm kaydedilmiş aramaları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fc118-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Kaydedilmiş aramaları listesi](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="fc118-127">Merhaba aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="fc118-127">Do any of hello following:</span></span>

* <span data-ttu-id="fc118-128">bir arama tooexecute kaydedilmiş bir aramayı hello listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="fc118-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="fc118-129">tooview kaydedilmiş bir aramayı Yönetimi seçeneklerinin listesi hello aşağı ok sonraki toohello arama adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fc118-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Kaydedilmiş aramaları yönetmek için Seçenekler](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="fc118-131">tooenter hello kaydedilen arama için yeni bir ad seçin **yeniden adlandırma**.</span><span class="sxs-lookup"><span data-stu-id="fc118-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="fc118-132">Merhaba arama tanımı değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="fc118-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="fc118-133">tooremove hello kaydedilen arama seçin, listeden **silmek**ve ardından hello silme işlemini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="fc118-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="fc118-134">toomark hello kaydedilen arama seçin, varsayılan arama olarak **varsayılan olarak Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="fc118-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="fc118-135">"Boş" arama hello Azure veri Kataloğu giriş sayfasından gerçekleştirirseniz, varsayılan aramanızı yürütülür.</span><span class="sxs-lookup"><span data-stu-id="fc118-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="fc118-136">Ayrıca, hello varsayılan arama hello hello üst kısmında görüntülenir olarak işaretlenen arama hello **kayıtlı aramaları** listesi.</span><span class="sxs-lookup"><span data-stu-id="fc118-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="fc118-137">Kuruluş Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="fc118-137">Organizational saved searches</span></span>
<span data-ttu-id="fc118-138">Kuruluşunuzdaki tüm kullanıcı kendi kullanmak için aramaları kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc118-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="fc118-139">Veri Kataloğu yöneticilerinin hello kuruluşunuzdaki tüm kullanıcılar için aramaları da kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc118-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="fc118-140">Yöneticiler bir aramayı kaydettiğinizde, bunlar ile sunulan bir **paylaşımı hello şirket içinde** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="fc118-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="fc118-141">Bu seçenek paylaşımları hello kaydedilmiş hello kuruluşunuzdaki tüm kullanıcılar için arama seçme.</span><span class="sxs-lookup"><span data-stu-id="fc118-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Kuruluş Kaydedilmiş aramaları](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="fc118-143">Sabitlenmiş veri varlıklarını</span><span class="sxs-lookup"><span data-stu-id="fc118-143">Pinned data assets</span></span>
<span data-ttu-id="fc118-144">Kaydedilmiş aramaları ile kaydedebilir ve arama tanımları yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc118-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="fc118-145">Merhaba aramaları tarafından döndürülen hello veri varlıklarını hello katalog değişiklik Merhaba içeriğine olarak zaman içinde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="fc118-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="fc118-146">Veri varlıklarını PIN ne zaman, belirli veri varlıklarını toomake açıkça tanımlayabilirsiniz bunları toouse arama gerek olmadan daha kolay tooaccess.</span><span class="sxs-lookup"><span data-stu-id="fc118-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="fc118-147">Bir veri varlığına sabitleme basittir.</span><span class="sxs-lookup"><span data-stu-id="fc118-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="fc118-148">tooadd hello veri varlık sabitlenmiş tooyour listesi, yalnızca tıklattığınız hello **PIN** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fc118-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="fc118-149">Merhaba simgesi hello köşesine hello varlık hello döşeme görünümünü ve hello en solundaki sütun hello Azure veri Kataloğu portalında hello liste görünümünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fc118-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![Merhaba veri varlığına PIN simgesi](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="fc118-151">Bir veri varlığına kaldırıldığında eşit olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="fc118-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="fc118-152">Merhaba tıklamanız yeterlidir **sabitleme** hello seçili varlık için simge tootoggle hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="fc118-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![Merhaba veri varlığına sabitleme simgesi](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="fc118-154">Merhaba My varlıklar bölümü</span><span class="sxs-lookup"><span data-stu-id="fc118-154">hello My Assets section</span></span>
<span data-ttu-id="fc118-155">Merhaba veri Kataloğu portalı giriş sayfasını içeren bir **My varlıklar** ilgi toohello geçerli kullanıcının varlıklar görüntüler bölümü.</span><span class="sxs-lookup"><span data-stu-id="fc118-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="fc118-156">Bu bölümde her iki sabitlenmiş varlıkları içerir ve kayıtlı aramalar.</span><span class="sxs-lookup"><span data-stu-id="fc118-156">This section includes both pinned assets and saved searches.</span></span>

![Merhaba hello giriş sayfasındaki My varlıklar bölümü](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="fc118-158">Özet</span><span class="sxs-lookup"><span data-stu-id="fc118-158">Summary</span></span>
<span data-ttu-id="fc118-159">Azure veri Kataloğu sizin ve diğer kuruluş üyelerinin verileri ve daha fazla süre ile çalışmak için arayan daha az süre beklemesini, böylece daha kolay toodiscover hello veri kaynakları ihtiyacınız olun yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc118-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="fc118-160">Kayıtlı aramalar ve kullanıcılar ile art arda çalıştıkları veri kaynaklarını kolayca tanıyacak şekilde varlıklar bu çekirdek özellikler yapı veri sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="fc118-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
