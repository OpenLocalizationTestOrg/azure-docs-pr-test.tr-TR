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
# <a name="extend-your-experiment-with-r"></a>R ile denemenizi genişletme
Hello kullanarak Azure Machine Learning Studio hello işlevselliğini hello R diliyle genişletebilirsiniz [R betiği yürütün] [ execute-r-script] modülü.

Bu modül, birden çok giriş veri kümeleri kabul eder ve tek bir veri kümesini çıktı olarak üretir. Merhaba bir R betiği yazabilirsiniz **R betiği** hello parametresinin [R betiği yürütün] [ execute-r-script] modülü.

Her giriş bağlantı noktası hello modülünün benzer toohello aşağıdaki kodu kullanarak erişebilirsiniz:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Şu anda yüklü olan tüm paketleri listeleme
yüklü paketler Hello listesini değiştirebilirsiniz. Şu anda yüklü olan paketlerin listesini bulunabilir [R paketleri Azure Machine Learning tarafından desteklenen](https://msdn.microsoft.com/library/azure/mt741980.aspx).

Kod hello aşağıdaki hello girerek hello tam, güncel yüklü olan paketlerin listesini alabilirsiniz [R betiği yürütün] [ execute-r-script] Modülü:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Bu paketleri toohello çıkış bağlantı noktasına hello hello listesi gönderir [R betiği yürütün] [ execute-r-script] modülü.
tooview hello paket listesinde, bir dönüştürme modülü gibi bağlanmak [Dönüştür tooCSV] [ convert-to-csv] hello çıktısını sol toohello [R betiği yürütün] [ execute-r-script]modülü hello denemeyi çalıştırın, hello çıktı hello dönüştürme modülü seçin ve ardından **karşıdan**. 

!["TooCSV Dönüştür" modülü çıktısını indirme](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Paket alma
Merhaba komutlarda aşağıdaki hello kullanarak henüz yüklenmemişse paketleri içeri aktarabilirsiniz [R betiği yürütün] [ execute-r-script] Modülü:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

Burada hello `my_favorite_package.zip` dosyası paketinizi içerir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
