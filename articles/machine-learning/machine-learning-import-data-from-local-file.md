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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="1e694-105">Eğitim verileri sabit sürücünüze Machine Learning Studio üzerindeki bir dosyadan içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="1e694-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="1e694-106">Nasıl tooupload bir veri dosyası, sabit sürücü toouse Azure Machine Learning Studio'da eğitim verilerini olarak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1e694-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="1e694-107">Merhaba veri dosyasını içeri aktararak, çalışma alanınızda kullanıma hazır bir veri kümesi modülü vardır.</span><span class="sxs-lookup"><span data-stu-id="1e694-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="1e694-108">Yerel bir dosya adımları tooimport verileri</span><span class="sxs-lookup"><span data-stu-id="1e694-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="1e694-109">yerel sabit sürücüye tooimport verilerden hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="1e694-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="1e694-110">Tıklatın **+ yeni** hello Machine Learning Studio penceresinin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="1e694-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="1e694-111">Seçin **DATASET** ve **yerel DOSYADAN**.</span><span class="sxs-lookup"><span data-stu-id="1e694-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="1e694-112">Merhaba, **yeni bir veri kümesi karşıya** iletişim kutusunda, tooupload istediğiniz gözatma toohello dosyası</span><span class="sxs-lookup"><span data-stu-id="1e694-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="1e694-113">Bir ad girin, hello veri türünü tanımlayın ve isteğe bağlı olarak bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="1e694-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="1e694-114">Bir açıklama önerilen - toorecord tanır hello veri hello gelecekte kullanırken tooremember istediğiniz hello verileri hakkında hiçbir özellikleri.</span><span class="sxs-lookup"><span data-stu-id="1e694-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="1e694-115">onay kutusu hello **hello yeni bir sürümü mevcut bir veri kümesini budur** tooupdate yeni verileri içeren varolan bir veri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e694-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="1e694-116">Bu onay kutusuna tıklayın ve ardından var olan bir dataset hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="1e694-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Yeni bir veri kümesi karşıya yükle](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="1e694-118">Karşıya yükleme sırasında dosyanızı karşıya yüklenen bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1e694-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="1e694-119">Karşıya yükleme zamanı hello veri ve hello hızınızı bağlantı toohello hizmetinizin boyutuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1e694-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="1e694-120">Merhaba dosya uzun sürmesi biliyorsanız, beklerken Machine Learning Studio içinde başka şeyler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e694-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="1e694-121">Ancak, hello tarayıcının kapanması hello verileri karşıya yükleme toofail neden olur.</span><span class="sxs-lookup"><span data-stu-id="1e694-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="1e694-122">Kullanıma hazır olduğundan veri kümesi Modülü</span><span class="sxs-lookup"><span data-stu-id="1e694-122">Dataset module is ready for use</span></span>
<span data-ttu-id="1e694-123">Verileriniz yüklendikten sonra bir veri kümesi modülünde depolanır ve çalışma alanınızdaki kullanılabilir tooany deneme olduğu.</span><span class="sxs-lookup"><span data-stu-id="1e694-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="1e694-124">Bir deneme düzenlerken hello oluşturduğunuz hello veri kümeleri bulabilirsiniz **My veri kümeleri** listesi hello altında **kaydedilen veri kümeleri** hello modül paleti listesinde.</span><span class="sxs-lookup"><span data-stu-id="1e694-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="1e694-125">Ek analizler ve makine öğrenme toouse hello dataset istediğinizde hello dataset hello deneme tuvale sürükleyip bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e694-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
