---
title: "aaaMulti coğrafi Yardım belgelerine | Microsoft Docs"
description: "Bilgi nasıl toocreate bir çalışma alanı ve bir web hizmeti hello Güney Orta Amerika Birleşik Devletleri (SCUS) farklı bir Azure bölgesi yayımlamak Azure bölgesi."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Çoklu Coğrafi Bölge Yardım belgeleri
Bu makalede, nasıl bir çalışma alanı oluşturmak ve bir web hizmeti farklı Azure bölgelerinde yayımlama açıklanır.  Merhaba [Azure ürünleri bölge sayfası tarafından](https://azure.microsoft.com/en-us/regions/services/) Azure Machine Learning olduğu kullanılabilir bölgeleri listeler.

## <a name="create-a-workspace"></a>Çalışma alanı oluşturma
1. Toohello Klasik Azure Portalı ' oturum açın.
2. Tıklatın **+ yeni** > **Veri Hizmetleri** > **MACHINE LEARNING** > **hızlı Oluştur**.  Altında **konumu** gibi başka bir bölge seçin **Güneydoğu Asya**.
   ![Birden çok coğrafi yardımcı görüntü 1][1]
3. Merhaba çalışma alanını seçin ve ardından **oturum açma Studio tooML**.
   ![Birden çok coğrafi yardımcı görüntü 2][2]
4. Diğer çalışma gibi kullanabilir, başka bir bölgede bir çalışma alanı artık sahipsiniz. Görünüm toohello üst ekranınızın sağ tooswitch, çalışma alanları arasında. Merhaba açılır, select hello bölge ve ardından hello çalışma tıklatın. Her şeyin yerel toohello çalışma bölgedir.  Örneğin, bir çalışma alanından oluşturulan web hizmetlerinizi tümünün aynı bölge hello çalışma alanında bulunan hello olacaktır.
   ![Birden çok coğrafi yardımcı görüntü 3][3]

## <a name="open-an-experiment-from-gallery"></a>Galeriden bir denemeyi açın
Galeriden bir denemeyi açarsanız, hangi bölgede toocopy hello deneme istediğiniz de seçebilirsiniz.

![Birden çok coğrafi yardımcı görüntü 4][4a]

## <a name="web-service-management"></a>Web Hizmeti Yönetimi
tooprogrammatically yönetme web Hizmetleri gibi yeniden eğitme için bölgeye özgü adresini hello kullan:

* https://asiasoutheast.Management.azureml.NET
* https://europewest.Management.azureml.NET

### <a name="things-toonote"></a>Şeyler toonote
1. Yalnızca denemeler toohello ait çalışma alanları arasında kopyalayabilirsiniz aynı bölgede bu şekilde. Toocopy deneme gerekiyorsa hello kullanabileceğiniz farklı bölgelerdeki çalışma alanları arasında [PowerShell](http://aka.ms/amlps) komutunu [ *kopya AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish. Başka bir çözüm toopublish hello deneme Galerisi içine listelenmemiş modundayken sonra diğer bölge hello hello çalışma alanını açın.
2. Hello bölge Seçici aynı anda yalnızca tek bir bölge için çalışma alanları gösterir.  
3. Ücretsiz çalışma alanında ya da konuk erişimi (anonim) çalışma oluşturulacak ve ABD merkezi Güney içinde barındırılan  
4. Güneydoğu Asya Güneydoğu Asya, bir çalışma alanından dağıtılan web hizmetleri de barındırılacak.  

## <a name="more-information"></a>Daha fazla bilgi
Bir soru sorun üzerinde hello [Azure Machine Learning Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
