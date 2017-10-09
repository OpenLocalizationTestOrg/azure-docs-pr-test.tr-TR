---
title: "aaaLoad veri analizi için Azure depolama ortamlara | Microsoft Docs"
description: "Azure Blob depolama alanından veri tooand Taşı"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a>Analiz için depolama ortamlarına veri yükleme
Merhaba takım veri bilimi işlemi veri veya alınan işlenen veya hello en uygun şekilde hello işleminin her aşamada analiz farklı depolama ortamları toobe çeşitli yüklenen olmasını gerektirir. İşleme için yaygın olarak kullanılan veri hedefleri Azure Blob Storage, SQL Azure veritabanının SQL Server Azure VM, Hdınsight (Hadoop) ve Azure Machine Learning içerir. 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Bu **menü** burada hello veri depolanabilir ve işlenebilir ortamları nasıl hedef tooingest verileri bu açıklamak tootopics bağlar.

Teknik ve iş gereksinimlerinize yanı sıra, hello ilk konum, biçimlendirme ve hangi hello veri alınan toobe tooachieve hello hedefleri çözümleme gereken hello hedef ortamları verilerinizi boyutunu belirler. Çeşitli ortamlar tooachieve hello çeşitli görevleri gerekli tooconstruct Tahmine dayalı bir model arasında taşınan bir senaryo toorequire veri toobe seyrek değil. Bu görev dizisi, örneğin, veri keşfi, ön işleme, temizleme, aşağı örnekleme ve model eğitim içerebilir.

