---
title: "R ile denemenizi genişletme | Microsoft Docs"
description: "R betiği yürütün modülünü kullanarak Azure Machine Learning Studio işlevselliğini R diliyle genişletmek nasıl."
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
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="cb0df-103">R ile denemenizi genişletme</span><span class="sxs-lookup"><span data-stu-id="cb0df-103">Extend your experiment with R</span></span>
<span data-ttu-id="cb0df-104">Kullanarak Azure Machine Learning Studio işlevselliğini R diliyle genişletebilirsiniz [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="cb0df-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="cb0df-105">Bu modül, birden çok giriş veri kümeleri kabul eder ve tek bir veri kümesini çıktı olarak üretir.</span><span class="sxs-lookup"><span data-stu-id="cb0df-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="cb0df-106">Bir R betiği içine yazabilirsiniz **R betiği** parametresinin [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="cb0df-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="cb0df-107">Her giriş bağlantı noktası modülün aşağıdakine benzer bir kod kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cb0df-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="cb0df-108">Şu anda yüklü olan tüm paketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="cb0df-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="cb0df-109">Yüklü olan paketlerin listesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb0df-109">The list of installed packages can change.</span></span> <span data-ttu-id="cb0df-110">Şu anda yüklü olan paketlerin listesini bulunabilir [R paketleri Azure Machine Learning tarafından desteklenen](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb0df-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="cb0df-111">Aşağıdaki kodu girerek yüklü paketleri tam, güncel listesini alabilirsiniz [R betiği yürütün] [ execute-r-script] Modülü:</span><span class="sxs-lookup"><span data-stu-id="cb0df-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="cb0df-112">Bu paket listesini çıkış bağlantı noktasına gönderir [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="cb0df-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="cb0df-113">Connect gibi bir dönüştürme modülü paket listesini görüntülemek için [CSV'ye Dönüştür] [ convert-to-csv] sol çıktısı için [R betiği yürütün] [ execute-r-script] modülü denemeyi çalıştırın, çıktı dönüştürme modülü seçin ve ardından **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="cb0df-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

!["CSV Dönüştür" modülü çıktısını indirme](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="cb0df-115">Paket alma</span><span class="sxs-lookup"><span data-stu-id="cb0df-115">Importing packages</span></span>
<span data-ttu-id="cb0df-116">Aşağıdaki komutları kullanarak henüz yüklenmemişse paketleri içeri aktarabilirsiniz [R betiği yürütün] [ execute-r-script] Modülü:</span><span class="sxs-lookup"><span data-stu-id="cb0df-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="cb0df-117">Burada `my_favorite_package.zip` dosyası paketinizi içerir.</span><span class="sxs-lookup"><span data-stu-id="cb0df-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
