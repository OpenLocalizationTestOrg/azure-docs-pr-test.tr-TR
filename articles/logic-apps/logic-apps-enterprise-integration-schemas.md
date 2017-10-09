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
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>XML şemaları ile Azure Logic Apps ve Enterprise Integration Pack Merhaba doğrulayın

Şemalar aldığınız hello XML belgelerinin geçerli ve hello verileri önceden tanımlanmış bir biçimde beklenen sahip olduğunu onaylayın. Şemalar, B2B senaryoda alınıp verilen iletileri doğrulamak yardımcı olur.

## <a name="add-a-schema"></a>Bir şema ekleyin

1. Hello Azure portal, seçin **daha fazla hizmet**.

    ![Azure portalı, "Daha fazla Hizmetleri"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Merhaba filtre arama kutusuna **tümleştirme**seçip **tümleştirme hesapları** hello sonuçları listesinden.

    ![Filtre Arama kutusu](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Select hello **tümleştirme hesabını** tooadd hello şema istediğiniz.

    ![Tümleştirme hesapları listesi](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Merhaba seçin **şemaları** döşeme.

    ![Örnek tümleştirme hesabını, "Şemaları"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>2 MB'den küçük bir şema dosyası ekleme

1. Merhaba, **şemaları** (hello) önceki adımları, açıldığını seçin dikey **Ekle**.

    ![Şemalar dikey penceresinde, "Ekle"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Şemanızı için bir ad girin. Başlangıç klasörü simgesi sonraki toohello seçerek Hello şema dosyası karşıya **şema** kutusu. Merhaba karşıya yükleme işlemi tamamlandıktan sonra Seç **Tamam**.

    ![Şemanın"Ekle", "küçük dosyası vurgulanmış" ile ekran görüntüsü](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>2 MB (yukarı too8 MB maksimum) daha büyük bir şema dosyası ekleme

Bu adımları hello blob kapsayıcı erişim düzeyine göre farklılık: **ortak** veya **anonim erişim yok**.

**toodetermine bu erişim düzeyi**

1.  Açık **Azure Storage Gezgini**. 

2.  Altında **Blob kapsayıcıları**seçin, istediğiniz hello blob kapsayıcısı. 

3.  Seçin **güvenlik**, **erişim düzeyine**.

Merhaba blob güvenlik erişim düzeyini ise **ortak**, şu adımları izleyin.

!["Blob kapsayıcıları", "Güvenlik" ve "Genel" vurgulanmış olan Azure Depolama Gezgini](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Merhaba şema tooyour depolama hesabı karşıya yükleme ve hello URI kopyalayın.

    ![Vurgulanan URI ile depolama hesabı](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. İçinde **Şema Ekle**seçin **büyük dosya**ve hello hello URI sağlayın **içerik URI** metin kutusu.

    !["Ekle" düğmesi ve "büyük dosyası vurgulanmış" ile şemaları](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Merhaba blob güvenlik erişim düzeyini ise **anonim erişim yok**, şu adımları izleyin.

!["Blob kapsayıcıları", "Güvenlik" ve "vurgulanmış anonim erişim yok" ile Azure Depolama Gezgini](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Merhaba şema tooyour depolama hesabı karşıya yükleyin.

    ![Depolama hesabı](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Merhaba şema için bir paylaşılan erişim imzası oluşturur.

    ![Depolama hesabıyla vurgulanmış paylaşılan erişim İmzalar sekmesi](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. İçinde **Şema Ekle**seçin **büyük dosya**ve hello hello paylaşılan erişim imzası URI sağlayın **içerik URI** metin kutusu.

    !["Ekle" düğmesi ve "büyük dosyası vurgulanmış" ile şemaları](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. Merhaba, **şemaları** tümleştirme hesabınızın dikey penceresinde, yeni eklenen şemanızı görünmelidir.

    !["Şemaları" ve vurgulanmış hello yeni şema ile tümleştirme hesabınız](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Şemalar Düzenle

1. Merhaba seçin **şemaları** döşeme.

2. Merhaba sonra **şemaları** dikey pencere açılır, select hello şema tooedit istiyor.

3. Merhaba üzerinde **şemaları** dikey penceresinde, seçin **Düzenle**.

    ![Şemalar dikey penceresi](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. Tooedit istediğiniz sonra seçin select hello şema dosyası **açık**.

    ![Açık şema dosyası tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Şema hello azure gösterir bir ileti başarıyla karşıya yüklendi.

## <a name="delete-schemas"></a>Şemalar Sil

1. Merhaba seçin **şemaları** döşeme.

2. Merhaba sonra **şemaları** dikey pencere açılır, select hello şema toodelete istiyor.

3. Merhaba üzerinde **şemaları** dikey penceresinde, seçin **silmek**.

    ![Şemalar dikey penceresi](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm toodelete hello istediğiniz seçili şema, seçin **Evet**.

    !["Şema delete" onay iletisi](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    Merhaba, **şemaları** dikey penceresinde hello şema listesini yeniler ve artık sildiğiniz hello şeması içerir.

    ![Tümleştirme hesabıyla "vurgulanmış şemaları"](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "hello Kurumsal tümleştirme paketi hakkında bilgi edinin").  

