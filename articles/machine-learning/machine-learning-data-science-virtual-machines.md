---
title: "Azure veri bilimi sanal makineleri IPython not defteri sunucuları olarak aaaProvision | Microsoft Docs"
description: "Bir veri bilimi sanal makineyi bir IPython Not Defteri Sunucusu Araçları destekleme ile olarak ayarlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>IPython dizüstü sunucuları olarak sağlama Azure veri bilimi sanal makineler
Yönergelerdir burada açıklayan sağlanan nasıl bir Azure VM ve SQL Hizmeti ile bir Azure VM tooset IPython dizüstü sunucuları olarak. Hello Windows sanal makine IPython Not Defteri, Azure Storage Gezgini ve AzCopy yanı sıra veri bilimi projeleri için yararlı olan diğer yardımcı programları gibi araçları destekleme ile yapılandırılır. Azure Storage Gezgini ve AzCopy, örneğin, sağlayan uygun şekilde tooupload veri tooAzure depolama nızdan yerel makine veya toodownload bu depolama yerel makineden tooyour. 

Bu menü hello yukarı tooset çeşitli veri bilimi ortamları hello tarafından nasıl kullanılacağını açıklamaktadır tootopics bağlantıları [takım veri bilimi işlem (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Azure sanal makineleri çeşitli türleri sağlanabilir ve bulut tabanlı veri bilimi ortamının bir parçası kullanılan toobe yapılandırılır. machine learning ve bu verileri hello bulutta hello hedef sanal makine hangi örneğinizin hakkında toouse hello türü ve veri toobe miktarını bağlıdır hello karar modellenir. 

* Bu karar verirken hello soruları tooconsider hakkında yönergeler için bkz [planlama Azure Machine Learning veri bilimi ortamınıza](machine-learning-data-science-plan-your-environment.md). 
* Bazı gelişmiş analizler yaparken karşılaşabileceğiniz hello senaryoları kataloğu için bkz: [senaryolar için Gelişmiş analitik işlemi ve Azure Machine Learning teknolojisinde hello](machine-learning-data-science-plan-sample-scenarios.md)

İki ayrı yönerge sağlanır:

* [Bir Azure sanal makinesini gelişmiş analizler için bir IPython dizüstü sunucu olarak ayarlamak](machine-learning-data-science-setup-virtual-machine.md) toodo veri bilimi tooprovision IPython dizüstü bilgisayar ve diğer araçları ile bir Azure sanal makine için hangi durumlarda nasıl kullanılacağını gösterir SQL Azure depolama biçimi kullanılan toostore hello veriler olabilir.
* [Bir Azure SQL Server sanal makinesini gelişmiş analizler için bir IPython dizüstü sunucu olarak ayarlamak](machine-learning-data-science-setup-sql-server-virtual-machine.md) toodo veri bilimi tooprovision IPython dizüstü bilgisayar ve diğer araçları ile bir Azure SQL Server sanal makine için hangi durumlarda nasıl kullanılacağını gösteren bir SQL veritabanı kullanılan toostore hello veriler olabilir.

Sağlanan ve yapılandırılmış sonra IPython dizüstü sunucuları hello araştırması ve veri işleme ve Azure Machine Learning ve hello takım veri bilimi işlem (TDSP) ile birlikte gereken diğer görevleri olarak bu sanal makineleri, kullanıma hazır. Merhaba hello veri bilimi işlemindeki sonraki adımlar hello eşlenen [TDSP öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve SQL Server ya da Hdınsight, verileri işlemek ve onu var. Azure ile Merhaba verilerden öğrenmeyi hazırlığı örnek taşıma adımları içerebilir Machine Learning.

> [!NOTE]
> Azure sanal makineler olarak fiyatlandırılır **yalnızca kullandıklarınız için ödeme**. değil yükleniyor tooensure sanal makineniz kullanmadığınızda faturalandırılır, toobe hello sahip **durduruldu (Deallocated)** hello durumu [Klasik Azure portalı](http://manage.windowsazure.com/). Adım adım yönergeler için veya nasıl toodeallocate, sanal makine bkz [kapatma ve sanal makine kullanılmadığında serbest bırakma](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

