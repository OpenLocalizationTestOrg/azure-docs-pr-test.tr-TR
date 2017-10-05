---
title: "Veri içeri aktarma Machine Learning Studio'ya başka bir deneme | Microsoft Docs"
description: "Azure Machine Learning Studio'da eğitim verilerini kaydetme ve başka bir deney kullanmak üzere nasıl."
keywords: "Veri, verileri, veri kaynakları, eğitim verilerini içeri aktarma"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="2cfa5-104">Verilerinizi başka bir denemeden Azure Machine Learning Studio’ya alma</span><span class="sxs-lookup"><span data-stu-id="2cfa5-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="2cfa5-105">Bir deneme Ara bir sonuç almak ve başka bir deneme bir parçası olarak kullanmak istediğinizde kez olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="2cfa5-106">Bunu yapmak için bir veri kümesi modülü kaydedin:</span><span class="sxs-lookup"><span data-stu-id="2cfa5-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="2cfa5-107">Bir veri kümesi kaydetmek istediğiniz modülünün Çıkış'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="2cfa5-108">Tıklatın **veri kümesi Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="2cfa5-109">İstendiğinde, bir ad ve veri kümesi kolayca tanımlamanıza olanak tanır bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="2cfa5-110">Tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="2cfa5-111">Kaydetme sona erdiğinde, veri kümesi herhangi deneme çalışma alanınızdaki içinde kullanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="2cfa5-112">İçinde bulabileceğiniz **kaydedilen veri kümeleri** modül paletindeki listesi.</span><span class="sxs-lookup"><span data-stu-id="2cfa5-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

