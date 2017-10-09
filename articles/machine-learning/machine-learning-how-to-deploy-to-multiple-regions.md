---
title: "bir Web hizmeti aaaHow toodeploy toomultiple bölgeler | Microsoft Docs"
description: "Adımları toodeploy (kopya) yeni Web hizmeti tooother bölgeleri."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Nasıl toodeploy bir Web hizmeti toomultiple bölgeleri
Merhaba yeni Azure Web Hizmetleri izin tooeasily birden çok abonelikleri veya çalışma alanları gerek kalmadan bir web hizmeti toomultiple bölgeler dağıtın. 

Fiyatlandırma belirli, bu nedenle hello web hizmeti dağıtacağınız her bölge için bir faturalandırma planı tanımlamanız gerekir bölgedir.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate başka bir bölgede bir planı
1. Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/).
2. Merhaba tıklatın **planları** menü seçeneği.
3. Görünüm sayfası üzerinden Hello planlarını temel tıklatın **yeni**.
4. Merhaba gelen **abonelik** açılan listesinde, hangi hello yeni plan bulunacağı select hello abonelik.
5. Merhaba gelen **bölge** açılan listesinde, hello yeni plan için bölge seçin. Merhaba planlama seçenekleri hello seçili bölgeye hello görüntüler **planlama seçenekleri** hello sayfasının bölümünde.
6. Merhaba gelen **kaynak grubu** bir kaynak grubu hello planlama açılan listesinde, seçin. Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).
7. İçinde **Plan adı** hello planının türü hello adı.
8. Altında **planı seçenekleri**, fatura düzeyi hello yeni plan hello'i tıklatın.
9. **Oluştur**'a tıklayın.

## <a name="deploying-hello-web-service-tooanother-region"></a>Merhaba web hizmeti tooanother bölge dağıtma
1. Merhaba tıklatın **Web Hizmetleri** menü seçeneği.
2. Merhaba, tooa yeni bölge dağıttığınız Web hizmeti seçin.
3. Tıklatın **kopya**.
4. İçinde **Web hizmeti adı**, hello web hizmeti için yeni bir ad yazın.
5. İçinde **Web hizmeti açıklaması**, hello web hizmeti için bir açıklama yazın.
6. Merhaba gelen **abonelik** açılan listesinde, hangi hello yeni web hizmeti bulunacağı select hello abonelik.
7. Merhaba gelen **kaynak grubu** bir kaynak grubu hello web hizmeti için açılan listesinde, seçin. Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).
8. Merhaba gelen **bölge** açılan listesinde, hangi toodeploy hello web hizmeti seçin hello bölgede.
9. Merhaba gelen **depolama hesabı** hangi toostore hello depolama hesabında web hizmeti açılan listesinde, seçin.
10. Merhaba gelen **fiyat planı** açılan listesinde, 8. adımda seçtiğiniz hello bölgede planı seçin.
11. Tıklatın **kopya**.

