---
title: Azure Machine Learning Studio'da bir dosyaya aaaImport verilerden | Microsoft Docs
description: "Nasıl tooupload bir eğitim veri dosyası sabit sürücü tooAzure Machine Learning Studio hakkında bilgi edinin. Bu veri kümesi modülü hello çalışma alanında oluşturur."
keywords: "veriler, veri biçimi, veri türleri, veri kaynakları, eğitim verilerini içeri aktarma"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Eğitim verileri sabit sürücünüze Machine Learning Studio üzerindeki bir dosyadan içeri aktarma
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Nasıl tooupload bir veri dosyası, sabit sürücü toouse Azure Machine Learning Studio'da eğitim verilerini olarak öğrenin. Merhaba veri dosyasını içeri aktararak, çalışma alanınızda kullanıma hazır bir veri kümesi modülü vardır.

## <a name="steps-tooimport-data-from-a-local-file"></a>Yerel bir dosya adımları tooimport verileri
yerel sabit sürücüye tooimport verilerden hello aşağıdaki:

1. Tıklatın **+ yeni** hello Machine Learning Studio penceresinin hello altındaki.
2. Seçin **DATASET** ve **yerel DOSYADAN**.
3. Merhaba, **yeni bir veri kümesi karşıya** iletişim kutusunda, tooupload istediğiniz gözatma toohello dosyası
4. Bir ad girin, hello veri türünü tanımlayın ve isteğe bağlı olarak bir açıklama girin. Bir açıklama önerilen - toorecord tanır hello veri hello gelecekte kullanırken tooremember istediğiniz hello verileri hakkında hiçbir özellikleri.
5. onay kutusu hello **hello yeni bir sürümü mevcut bir veri kümesini budur** tooupdate yeni verileri içeren varolan bir veri kümesi sağlar. Bu onay kutusuna tıklayın ve ardından var olan bir dataset hello adını girin.

![Yeni bir veri kümesi karşıya yükle](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Karşıya yükleme sırasında dosyanızı karşıya yüklenen bir ileti görürsünüz. Karşıya yükleme zamanı hello veri ve hello hızınızı bağlantı toohello hizmetinizin boyutuna bağlıdır. Merhaba dosya uzun sürmesi biliyorsanız, beklerken Machine Learning Studio içinde başka şeyler yapabilirsiniz. Ancak, hello tarayıcının kapanması hello verileri karşıya yükleme toofail neden olur.

## <a name="dataset-module-is-ready-for-use"></a>Kullanıma hazır olduğundan veri kümesi Modülü
Verileriniz yüklendikten sonra bir veri kümesi modülünde depolanır ve çalışma alanınızdaki kullanılabilir tooany deneme olduğu.

Bir deneme düzenlerken hello oluşturduğunuz hello veri kümeleri bulabilirsiniz **My veri kümeleri** listesi hello altında **kaydedilen veri kümeleri** hello modül paleti listesinde. Ek analizler ve makine öğrenme toouse hello dataset istediğinizde hello dataset hello deneme tuvale sürükleyip bırakabilirsiniz.
