---
title: "aaaSample verileri Azure blob kapsayıcılar, SQL Server'ı ve tabloları Hive | Microsoft Docs"
description: "Çeşitli Azure enviromnents tooexplore verilerin depolanma."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="abaae-103"><a name="heading"></a>Örnek verileri Azure blob kapsayıcılar, SQL Server'ı ve tabloları Hive</span><span class="sxs-lookup"><span data-stu-id="abaae-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="abaae-104">Bu belgede ele alınmaktadır tootopics bağlantıları nasıl üç farklı Azure konumlardan birinde depolanan toosample veriler:</span><span class="sxs-lookup"><span data-stu-id="abaae-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="abaae-105">**Azure blob kapsayıcı verileri** programlı olarak karşıdan yükleyip örnek Python kodu ile örnekleme örneklenen.</span><span class="sxs-lookup"><span data-stu-id="abaae-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="abaae-106">**SQL Server verilerini** hem SQL hem de hello Python programlama dili kullanılarak örneklenen.</span><span class="sxs-lookup"><span data-stu-id="abaae-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="abaae-107">**Tablo verisi hive** Hive sorgularını kullanarak örneklenen.</span><span class="sxs-lookup"><span data-stu-id="abaae-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="abaae-108">Merhaba aşağıdaki **menü** açıklayan toohello konulara bağlantılar nasıl her bu Azure depolama ortamlarının toosample verileri.</span><span class="sxs-lookup"><span data-stu-id="abaae-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="abaae-109">Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="abaae-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="abaae-110">**Neden veri örneği?**</span><span class="sxs-lookup"><span data-stu-id="abaae-110">**Why sample data?**</span></span>

<span data-ttu-id="abaae-111">Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu.</span><span class="sxs-lookup"><span data-stu-id="abaae-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="abaae-112">Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="abaae-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="abaae-113">Kendi hello Cortana Analytics işlem içinde tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına rolüdür.</span><span class="sxs-lookup"><span data-stu-id="abaae-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

