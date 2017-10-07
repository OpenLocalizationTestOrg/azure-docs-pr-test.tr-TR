---
title: "OMS içinde aaaSolution hedefleme | Microsoft Docs"
description: "Çözüm hedefleme Operations Management Suite (OMS) toolimit yönetim çözümleri tooa belirli kümesini aracıları verir bir özelliktir.  Bu makalede nasıl toocreate kapsam yapılandırması ve tooa çözüm uygulayabilirsiniz."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Operations Management Suite (OMS) tooscope yönetim çözümleri toospecific aracıları (Önizleme) hedefleme çözümü kullanın
Bir çözüm tooOMS eklediğinizde, varsayılan tooall Windows ve Linux aracıları bağlı tooyour günlük analizi çalışma alanı tarafından otomatik olarak dağıtılır.  Tooa belirli aracıları kümesini sınırlayarak yönelik bir çözüm, maliyetleri ve sınırı hello veri miktarını toplanan toomanage isteyebilirsiniz.  Bu makalede nasıl toouse **çözüm hedefleme** tooapply bir kapsam olanak tanıyan bir OMS özelliği olduğu tooyour çözümler.

## <a name="how-tootarget-a-solution"></a>Nasıl tootarget bir çözümü
Üç adımları tootargeting bir çözüm hello aşağıdaki bölümlerde açıklandığı gibi vardır.  Merhaba OMS portalı ve hello Azure portal için farklı adımlar gerekeceğini unutmayın.


### <a name="1-create-a-computer-group"></a>1. Bir bilgisayar grubu oluşturun
Oluşturarak kapsamdaki tooinclude istediğiniz hello bilgisayarları belirttiğiniz bir [bilgisayar grubu](../log-analytics/log-analytics-computer-groups.md) günlük analizi içinde.  Merhaba bilgisayar grubu günlük aramaya bağlı veya Active Directory ya da WSUS grupları gibi diğer kaynaklardan alınamadı. Olarak [aşağıda açıklanan](#solutions-and-agents-that-cant-be-targeted), doğrudan bilgisayarları Analytics hello kapsamda dahil edilir tooLog bağlı sadece.

Sonra çalışma alanınızda oluşturulan hello bilgisayar grubu oluşturduktan sonra uygulanan tooone ya da daha fazla çözümleri bir kapsam yapılandırmasında dahil.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. Bir kapsam yapılandırması oluştur
 A **kapsam yapılandırması** uygulanan tooone ya da daha fazla çözümleri olabilir ve bir veya daha fazla bilgisayar gruplarını içerir. 
 
 İşlemi aşağıdaki hello kullanarak bir kapsam yapılandırmasını oluşturun.  

 1. İçinde Azure portal Merhaba, çok gidin**günlük analizi** ve çalışma alanınızı seçin.
 2. Merhaba çalışma alanındaki hello özelliklerinde **çalışma veri kaynakları** seçin **kapsam yapılandırmaları**.
 3. Tıklatın **Ekle** toocreate yeni bir kapsam yapılandırması.
 4. Tür a **adı** hello kapsam yapılandırması için.
 5. Tıklatın **bilgisayar gruplarını seçin**.
 6. Oluşturduğunuz hello bilgisayar grubu ve isteğe bağlı olarak herhangi diğer grupları tooadd toohello bir yapılandırma seçin.  **Seç**'e tıklayın.  
 6. Tıklatın **Tamam** toocreate hello kapsam yapılandırması. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Merhaba kapsam yapılandırma tooa çözümü uygulayın.
Bir kapsam yapılandırması olduktan sonra daha sonra onu tooone veya diğer çözümleri uygulayabilirsiniz.  Tek bir kapsam yapılandırma ile birden çok çözümler kullanılabilse de, her bir çözüm için yalnızca bir kapsam yapılandırması kullanabilirsiniz.

İşlemi aşağıdaki hello kullanarak kapsam yapılandırma uygulayın.  

 1. İçinde Azure portal Merhaba, çok gidin**günlük analizi** ve çalışma alanınızı seçin.
 2. Merhaba çalışma hello özelliklerinde seçin **çözümleri**.
 3. Tıklatın hello çözüm üzerinde tooscope istiyor.
 4. Merhaba çözümü hello özelliklerinde **çalışma veri kaynakları** seçin **çözüm hedefleme**.  Merhaba seçeneği kullanılabilir değilse, ardından [Bu çözüm hedefleyemez](#solutions-and-agents-that-cant-be-targeted).
 5. Tıklatın **Ekle kapsam yapılandırması**.  Uygulanan yapılandırma toothis Çözüm zaten varsa bu seçenek kullanılamaz.  Başka bir tane eklemeden önce mevcut yapılandırma hello kaldırmanız gerekir.
 6. Oluşturduğunuz hello kapsam yapılandırma'ya tıklayın.
 7. Gözcü hello **durum** onu gösterir hello yapılandırma tooensure, **başarılı**.  Merhaba durum bir hata olduğunu gösteriyorsa, hello elips toohello sağ hello yapılandırma ve Seç'ı tıklatın **Düzen kapsam yapılandırması** toomake değişiklikler.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Çözümler ve hedefleyemez aracıları
Aracıları ve çözüm hedeflemede kullanılamaz çözümleri hello ölçütlerini verilmiştir.

- Çözüm hedefleme yalnızca tooagents dağıtmak toosolutions için geçerlidir.
- Çözüm hedefleme yalnızca Microsoft tarafından sağlanan toosolutions için geçerlidir.  Toosolutions uygulanmaz [kendiniz veya iş ortakları tarafından oluşturulan](operations-management-suite-solutions-creating.md).
- Yalnızca tooLog Analytics doğrudan bağlanan aracıları filtreleyebilirsiniz.  Çözümleri, bunlar bir kapsam yapılandırmada olup olmadığına dahil edildiklerini bağlı bir Operations Manager yönetim grubunun parçası olan tooany aracıları otomatik olarak dağıtacaktır.

### <a name="exceptions"></a>Özel durumlar
Çözüm hedefleme ile Merhaba kullanılamaz hello uygun olsa da çözümleri aşağıdaki belirtilen ölçütleri.

- Aracı sistem durumu değerlendirmesi

## <a name="next-steps"></a>Sonraki adımlar
- Ortamınızdaki kullanılabilir tooinstall hello çözümleri dahil olmak üzere yönetim çözümleri hakkında daha fazla bilgi [eklemek Azure günlük analizi yönetim çözümleri tooyour çalışma](../log-analytics/log-analytics-add-solutions.md).
- Bilgisayar gruplarının oluşturma hakkında daha fazla bilgi [günlük analizi bilgisayar gruplarında oturum aramaları](../log-analytics/log-analytics-computer-groups.md).