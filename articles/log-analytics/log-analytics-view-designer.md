---
title: "aaaCreate OMS günlük analizi tooanalyze veri görünümleri | Microsoft Docs"
description: "Görünüm Tasarımcısı'nda günlük analizi sağlar, toocreate özel hello OMS ve Azure portalında gösterilir ve farklı görsel hello OMS depo veri içeren görünümler. Bu makale, Görünüm Tasarımcısı ve yordamları oluşturmak ve özel görünümler düzenlemek için genel bir bakış içerir."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Günlük analizi Görünüm Tasarımcısı toocreate özel görünümleri kullanma
Merhaba Görünüm Tasarımcısı içinde [günlük analizi](log-analytics-overview.md) hello OMS deposundaki verileri farklı görselleştirmesini içeren toocreate özel görünümler hello OMS konsolunda sağlar. Bu makale, Görünüm Tasarımcısı ve yordamları oluşturmak ve özel görünümler düzenlemek için genel bir bakış içerir.

Görünüm Tasarımcısı için kullanılabilir diğer makaleler şunlardır:

* [Döşeme başvuru](log-analytics-view-designer-tiles.md) -başvuru hello ayarlarının her hello için kendi özel görünümlerinizi de kullanılabilir toouse yerleştirir.
* [Görselleştirme bölümü başvuru](log-analytics-view-designer-parts.md) -başvuru hello ayarlarının her hello için kendi özel görünümlerinizi de kullanılabilir toouse yerleştirir.

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), tüm görünümleri sorgularda hello yazılmalıdır sonra [yeni sorgu dili](https://go.microsoft.com/fwlink/?linkid=856078).  Merhaba çalışma yükseltilmeden önce oluşturulan görünümleri dönüştürülen automtically olacaktır.

## <a name="concepts"></a>Kavramlar
Aşağıdaki tablonun hello hello öğelerinde Hello Görünüm Tasarımcısı ile oluşturulan görünümleri içerir.

| Bölümü | Açıklama |
|:--- |:--- |
| Döşeme |Merhaba ana günlük analizi genel bakış panosunda görüntülenir.  Bir görsel hello içerdiği hello bilgi özetlemeye içeren özel bir görünüm.  Döşeme farklı hello OMS deposu kayıtlarının farklı görselleştirmeleri sağlar.  Merhaba üzerinde döşeme tooopen hello Özel Görünüm'ı tıklatın. |
| Özel Görünüm |Merhaba kullanıcı döşeme hello üzerinde tıkladığında görüntülenir.  Bir veya daha fazla görselleştirme bölümleri içerir. |
| Görselleştirme bölümleri |Merhaba OMS depo veri görselleştirme dayalı bir veya daha fazla [oturum aramaları](log-analytics-log-searches.md).  Çoğu bölümleri üst düzey bir görsel öğe sağlayan üstbilgi ve hello üst sonuçlarının bir listesini içerir.  Farklı bölümü türleri hello OMS deposu kayıtlarının farklı görselleştirmeleri sağlar.  Merhaba bölümü tooperform öğelere ayrıntılı kayıtları sağlayan bir günlük Ara'yı tıklatın. |

![Görünüm Tasarımcısı genel bakış](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Görünüm Tasarımcısı tooyour çalışma Ekle
Görünüm Tasarımcısı Önizleme'de olsa da, bunu tooyour çalışma alanını seçerek eklemeniz gerekir **Önizleme özellikleri** hello içinde **ayarları** hello OMS portalı bölümü.

![Önizlemeyi Etkinleştir](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Oluşturma ve görünümler düzenleme
### <a name="create-a-new-view"></a>Yeni bir görünüm oluşturma
Yeni bir görünüm hello açmak **Görünüm Tasarımcısı** Görünüm Tasarımcısı hello üzerinde tıklayarak hello ana OMS panosunda döşeme.

![Görünüm Tasarımcısı döşeme](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Var olan bir görünümü düzenleme
tooedit hello Görünüm Tasarımcısı, döşemesinin hello ana OMS panosunda tıklayarak açık hello görünümü içinde var olan bir görünümü.  Merhaba ardından **Düzenle** düğmesini tooopen hello hello Görünüm Tasarımcısı görünümünde.

![Bir görünümü düzenleme](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Var olan bir görünümü kopyalama
Bir görünüm kopyaladığınızda yeni bir görünüm oluşturur ve hello Görünüm Tasarımcısı açar.  Merhaba yeni görünüm aynı hello "Kopyala" eklenmiş toohello ucu ile orijinal olarak ad hello sahip olur.  tooclone açık bir görünüm döşemesinin hello ana OMS panosunda tıklayarak var olan bir görünümü hello.  Merhaba ardından **kopya** düğmesini tooopen hello hello Görünüm Tasarımcısı görünümünde.

![Bir görünüm kopyalama](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Var olan bir görünümü Sil
toodelete varolan bir görünümü döşemesinin hello ana OMS panosunda tıklayarak açık hello görünümü.  Merhaba ardından **Düzenle** tooopen hello hello Görünüm Tasarımcısı görünümünde düğmesine tıklayın ve **Görünümü Sil'i**.

![Bir görünümü Sil](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Var olan bir görünümü dışarı aktarma
Başka bir çalışma alanına alma veya kullanmak bir görünüm tooa JSON dosyasını dışarı aktarabilirsiniz bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport varolan bir görünümü döşemesinin hello ana OMS panosunda tıklayarak açık hello görünümü.  Başlangıç'ı tıklatın **dışarı** düğmesi toocreate hello tarayıcının indirme klasöründe bulunan bir dosyadır.  Merhaba dosyasının Hello adı hello uzantılı hello görünümün hello adı olacaktır *omsview*.

![Görünüm verme](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Var olan bir görünümü alma
Alabileceğiniz bir *omsview* başka bir yönetim grubundan dışarı aktardığınız dosya.  Varolan bir görünümü tooimport önce yeni bir görünüm oluşturun.  Merhaba ardından **alma** düğmesi ve select hello *omsview* dosya.  Merhaba dosya Hello yapılandırmasında hello var olan görünüme kopyalanacak.

![Görünüm verme](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Görünüm Tasarımcısı ile çalışma
Merhaba Görünüm Tasarımcısı üç bölmesi vardır.  Merhaba **tasarım** bölmesinde hello özel görünüm temsil eder.  Eklediğinizde kutucukları ve bölümleri hello **denetim** bölmesinde toohello **tasarım** oldukları bölmesinde eklenen toohello görünümü.  Merhaba **özellikleri** bölmesinde hello döşeme veya seçili bölümü hello özelliklerini görüntüler.

![Görünüm Tasarımcısı](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Görünümü kutucuğu yapılandırın
Özel bir görünüm yalnızca tek bir döşeme olabilir.  Select hello **döşeme** hello sekmesinde **denetim** bölmesinde tooview hello geçerli döşeme veya alternatif bir tanesini seçin.  Merhaba **özellikleri** hello geçerli döşemeye hello Özellikler bölmesinde görüntülenir.  Merhaba döşeme özelliklerini yapılandırmak toohello according ayrıntılı hello bilgilerinde [döşeme başvuru](log-analytics-view-designer-tiles.md) tıklatıp **Uygula** toosave değişiklikleri.

### <a name="configure-visualization-parts"></a>Görselleştirme bölümleri yapılandırma
Bir görünüm görselleştirme bölümlerinin herhangi bir sayı içerebilir.  Select hello **Görünüm** sekmesini ve ardından bir görsel öğe Kısım tooadd toohello görünümü.  Merhaba **özellikleri** bölmesinde seçili hello bölümü hello özelliklerini görüntüler.  Merhaba görüntüleme yapılandırma toohello göre özellikleri ayrıntılı hello bilgilerinde [görselleştirme bölümü başvuru](log-analytics-view-designer-parts.md) tıklatıp **Uygula** toosave değişiklikler.

### <a name="delete-a-visualization-part"></a>Görselleştirme bölümü silin
Merhaba tıklayarak görselleştirme bölümü hello görünümünden kaldırabilirsiniz **X** hello sağ üst köşesinde hello bölümü düğmesini.

### <a name="rearrange-visualization-parts"></a>Görselleştirme bölümleri yeniden düzenleme
Görünümler yalnızca bir satır görselleştirme bölümlerinin gerekir.  Varolan bölümleri görünümünde tıklatarak ve sürükleyerek tooa yeni bir konuma yeniden düzenleyin.

## <a name="next-steps"></a>Sonraki adımlar
* Ekleme [kutucukları](log-analytics-view-designer-tiles.md) tooyour özel görünüm.
* Ekleme [görselleştirme bölümleri](log-analytics-view-designer-parts.md) tooyour özel görünüm.
