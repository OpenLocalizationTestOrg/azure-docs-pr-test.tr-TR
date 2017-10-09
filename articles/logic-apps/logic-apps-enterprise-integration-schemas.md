---
title: "XML doğrulama - Azure Logic Apps için aaaSchemas | Microsoft Docs"
description: "XML belgeleri şemalarda Azure Logic Apps ve kurumsal tümleştirme paketi için doğrulama"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="ad44b-103">XML şemaları ile Azure Logic Apps ve Enterprise Integration Pack Merhaba doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ad44b-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="ad44b-104">Şemalar aldığınız hello XML belgelerinin geçerli ve hello verileri önceden tanımlanmış bir biçimde beklenen sahip olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="ad44b-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="ad44b-105">Şemalar, B2B senaryoda alınıp verilen iletileri doğrulamak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ad44b-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="ad44b-106">Bir şema ekleyin</span><span class="sxs-lookup"><span data-stu-id="ad44b-106">Add a schema</span></span>

1. <span data-ttu-id="ad44b-107">Hello Azure portal, seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-107">In hello Azure portal, select **More services**.</span></span>

    ![Azure portalı, "Daha fazla Hizmetleri"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="ad44b-109">Merhaba filtre arama kutusuna **tümleştirme**seçip **tümleştirme hesapları** hello sonuçları listesinden.</span><span class="sxs-lookup"><span data-stu-id="ad44b-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Filtre Arama kutusu](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="ad44b-111">Select hello **tümleştirme hesabını** tooadd hello şema istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ad44b-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Tümleştirme hesapları listesi](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="ad44b-113">Merhaba seçin **şemaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ad44b-113">Choose hello **Schemas** tile.</span></span>

    ![Örnek tümleştirme hesabını, "Şemaları"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="ad44b-115">2 MB'den küçük bir şema dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="ad44b-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="ad44b-116">Merhaba, **şemaları** (hello) önceki adımları, açıldığını seçin dikey **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Şemalar dikey penceresinde, "Ekle"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="ad44b-118">Şemanızı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="ad44b-118">Enter a name for your schema.</span></span> <span data-ttu-id="ad44b-119">Başlangıç klasörü simgesi sonraki toohello seçerek Hello şema dosyası karşıya **şema** kutusu.</span><span class="sxs-lookup"><span data-stu-id="ad44b-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="ad44b-120">Merhaba karşıya yükleme işlemi tamamlandıktan sonra Seç **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-120">After hello upload process completes, select **OK**.</span></span>

    ![Şemanın"Ekle", "küçük dosyası vurgulanmış" ile ekran görüntüsü](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="ad44b-122">2 MB (yukarı too8 MB maksimum) daha büyük bir şema dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="ad44b-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="ad44b-123">Bu adımları hello blob kapsayıcı erişim düzeyine göre farklılık: **ortak** veya **anonim erişim yok**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="ad44b-124">**toodetermine bu erişim düzeyi**</span><span class="sxs-lookup"><span data-stu-id="ad44b-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="ad44b-125">Açık **Azure Storage Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="ad44b-126">Altında **Blob kapsayıcıları**seçin, istediğiniz hello blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ad44b-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="ad44b-127">Seçin **güvenlik**, **erişim düzeyine**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="ad44b-128">Merhaba blob güvenlik erişim düzeyini ise **ortak**, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ad44b-128">If hello blob security access level is **Public**, follow these steps.</span></span>

!["Blob kapsayıcıları", "Güvenlik" ve "Genel" vurgulanmış olan Azure Depolama Gezgini](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="ad44b-130">Merhaba şema tooyour depolama hesabı karşıya yükleme ve hello URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ad44b-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Vurgulanan URI ile depolama hesabı](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="ad44b-132">İçinde **Şema Ekle**seçin **büyük dosya**ve hello hello URI sağlayın **içerik URI** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ad44b-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    !["Ekle" düğmesi ve "büyük dosyası vurgulanmış" ile şemaları](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="ad44b-134">Merhaba blob güvenlik erişim düzeyini ise **anonim erişim yok**, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ad44b-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

!["Blob kapsayıcıları", "Güvenlik" ve "vurgulanmış anonim erişim yok" ile Azure Depolama Gezgini](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="ad44b-136">Merhaba şema tooyour depolama hesabı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad44b-136">Upload hello schema tooyour storage account.</span></span>

    ![Depolama hesabı](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="ad44b-138">Merhaba şema için bir paylaşılan erişim imzası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad44b-138">Generate a shared access signature for hello schema.</span></span>

    ![Depolama hesabıyla vurgulanmış paylaşılan erişim İmzalar sekmesi](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="ad44b-140">İçinde **Şema Ekle**seçin **büyük dosya**ve hello hello paylaşılan erişim imzası URI sağlayın **içerik URI** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ad44b-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    !["Ekle" düğmesi ve "büyük dosyası vurgulanmış" ile şemaları](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="ad44b-142">Merhaba, **şemaları** tümleştirme hesabınızın dikey penceresinde, yeni eklenen şemanızı görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="ad44b-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    !["Şemaları" ve vurgulanmış hello yeni şema ile tümleştirme hesabınız](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="ad44b-144">Şemalar Düzenle</span><span class="sxs-lookup"><span data-stu-id="ad44b-144">Edit schemas</span></span>

1. <span data-ttu-id="ad44b-145">Merhaba seçin **şemaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ad44b-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="ad44b-146">Merhaba sonra **şemaları** dikey pencere açılır, select hello şema tooedit istiyor.</span><span class="sxs-lookup"><span data-stu-id="ad44b-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="ad44b-147">Merhaba üzerinde **şemaları** dikey penceresinde, seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Şemalar dikey penceresi](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="ad44b-149">Tooedit istediğiniz sonra seçin select hello şema dosyası **açık**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Açık şema dosyası tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="ad44b-151">Şema hello azure gösterir bir ileti başarıyla karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="ad44b-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="ad44b-152">Şemalar Sil</span><span class="sxs-lookup"><span data-stu-id="ad44b-152">Delete schemas</span></span>

1. <span data-ttu-id="ad44b-153">Merhaba seçin **şemaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ad44b-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="ad44b-154">Merhaba sonra **şemaları** dikey pencere açılır, select hello şema toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="ad44b-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="ad44b-155">Merhaba üzerinde **şemaları** dikey penceresinde, seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Şemalar dikey penceresi](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="ad44b-157">tooconfirm toodelete hello istediğiniz seçili şema, seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ad44b-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    !["Şema delete" onay iletisi](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="ad44b-159">Merhaba, **şemaları** dikey penceresinde hello şema listesini yeniler ve artık sildiğiniz hello şeması içerir.</span><span class="sxs-lookup"><span data-stu-id="ad44b-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Tümleştirme hesabıyla "vurgulanmış şemaları"](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="ad44b-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad44b-161">Next steps</span></span>
* <span data-ttu-id="ad44b-162">[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "hello Kurumsal tümleştirme paketi hakkında bilgi edinin").</span><span class="sxs-lookup"><span data-stu-id="ad44b-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

