---
title: aaaExtend R ile denemenizi | Microsoft Docs
description: "Nasıl tooextend hello Azure Machine Learning Studio işlevselliğini hello R diliyle hello R betiği yürütün modülünü kullanarak."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="1bdfb-103">R ile denemenizi genişletme</span><span class="sxs-lookup"><span data-stu-id="1bdfb-103">Extend your experiment with R</span></span>
<span data-ttu-id="1bdfb-104">Hello kullanarak Azure Machine Learning Studio hello işlevselliğini hello R diliyle genişletebilirsiniz [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="1bdfb-105">Bu modül, birden çok giriş veri kümeleri kabul eder ve tek bir veri kümesini çıktı olarak üretir.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="1bdfb-106">Merhaba bir R betiği yazabilirsiniz **R betiği** hello parametresinin [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="1bdfb-107">Her giriş bağlantı noktası hello modülünün benzer toohello aşağıdaki kodu kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1bdfb-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="1bdfb-108">Şu anda yüklü olan tüm paketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="1bdfb-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="1bdfb-109">yüklü paketler Hello listesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-109">hello list of installed packages can change.</span></span> <span data-ttu-id="1bdfb-110">Şu anda yüklü olan paketlerin listesini bulunabilir [R paketleri Azure Machine Learning tarafından desteklenen](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bdfb-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="1bdfb-111">Kod hello aşağıdaki hello girerek hello tam, güncel yüklü olan paketlerin listesini alabilirsiniz [R betiği yürütün] [ execute-r-script] Modülü:</span><span class="sxs-lookup"><span data-stu-id="1bdfb-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="1bdfb-112">Bu paketleri toohello çıkış bağlantı noktasına hello hello listesi gönderir [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="1bdfb-113">tooview hello paket listesinde, bir dönüştürme modülü gibi bağlanmak [Dönüştür tooCSV] [ convert-to-csv] hello çıktısını sol toohello [R betiği yürütün] [ execute-r-script]modülü hello denemeyi çalıştırın, hello çıktı hello dönüştürme modülü seçin ve ardından **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

!["TooCSV Dönüştür" modülü çıktısını indirme](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="1bdfb-115">Paket alma</span><span class="sxs-lookup"><span data-stu-id="1bdfb-115">Importing packages</span></span>
<span data-ttu-id="1bdfb-116">Merhaba komutlarda aşağıdaki hello kullanarak henüz yüklenmemişse paketleri içeri aktarabilirsiniz [R betiği yürütün] [ execute-r-script] Modülü:</span><span class="sxs-lookup"><span data-stu-id="1bdfb-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="1bdfb-117">Burada hello `my_favorite_package.zip` dosyası paketinizi içerir.</span><span class="sxs-lookup"><span data-stu-id="1bdfb-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
