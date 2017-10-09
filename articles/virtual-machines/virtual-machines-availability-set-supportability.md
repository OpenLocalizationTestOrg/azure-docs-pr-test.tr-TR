---
title: "Azure VM'ler tooan varolan kullanılabilirlik kümesi ekleme aaaSupportability | Microsoft Docs"
description: "Azure VM'ler tooan varolan kullanılabilirlik kümesi ekleme desteklenebilirlik."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Azure VM'ler tooan varolan kullanılabilirlik kümesi ekleme desteklenebilirlik

Yeni sanal makineleri (VM'ler) tooan varolan kullanılabilirlik kümesi eklediğinizde sınırlamaları bazen karşılaşabilirsiniz. Merhaba aşağıdaki ayrıntıları karıştırabilir miyim hangi VM dizisi aynı kullanılabilirlik kümesinde hello grafik.

Merhaba desteklenebilirlik matris toomix farklı türlerde VM'ler şöyledir:

Seri & kullanılabilirlik kümesi|İkinci VM|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|İlk VM|||||||
|A||TAMAM|TAMAM|TAMAM|TAMAM|TAMAM|
|Av2||TAMAM|TAMAM|TAMAM|TAMAM|TAMAM|
|D||TAMAM|TAMAM|TAMAM|TAMAM|TAMAM|
|Dv2||TAMAM|TAMAM|TAMAM|TAMAM|TAMAM|
|Dv3||TAMAM|TAMAM|TAMAM|TAMAM|TAMAM|

Diğer tüm serisi hello belirli donanım gerektirdiğinden aynı kullanılabilirlik kümesi bulunamadı.
