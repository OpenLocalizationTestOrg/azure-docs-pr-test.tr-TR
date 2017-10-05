---
title: "Azure veri bilimi sanal makineleri IPython dizüstü sunucuları olarak sağlama | Microsoft Docs"
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
ms.openlocfilehash: db1ffb2a226a087ecea2ea6f560c6b803e33d8c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>IPython dizüstü sunucuları olarak sağlama Azure veri bilimi sanal makineler
Yönergeler, bir Azure VM ve SQL Hizmeti ile bir Azure VM IPython dizüstü sunucuları olarak nasıl ayarlanacağını açıklar burada verilmiştir. Windows sanal makine IPython Not Defteri, Azure Storage Gezgini ve AzCopy yanı sıra veri bilimi projeleri için yararlı olan diğer yardımcı programları gibi araçları destekleme ile yapılandırılır. Örneğin, Azure Depolama Gezgini ve AzCopy, verileri Azure depolama alanına yerel makinenizden karşıya yüklemek veya bir depolama biriminden yerel makinenize indirmek için uygun şekilde girin. 

Tarafından kullanılan çeşitli veri bilimi ortamları ayarlamak nasıl açıklayan konuları için bu menüyü bağlantıları [takım veri bilimi işlem (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Azure sanal makineleri çeşitli türleri sağlanabilir ve bulut tabanlı veri bilimi ortamının bir parçası kullanılmak üzere yapılandırılmış. Machine learning ve bu verileri bulutta için hedef ile modellenebilir veri miktarını ve türünü kullanmak için sanal makinenin karar hangi özellik hakkında bağlı. 

* Bu karar verirken göz önüne almanız gereken soruları hakkında yönergeler için bkz [planlama Azure Machine Learning veri bilimi ortamınıza](machine-learning-data-science-plan-your-environment.md). 
* Bazı gelişmiş analizler yaparken karşılaşabileceğiniz senaryo kataloğu için bkz: [Gelişmiş analiz işlem ve Azure Machine Learning teknolojisinde için senaryolar](machine-learning-data-science-plan-sample-scenarios.md)

İki ayrı yönerge sağlanır:

* [Bir Azure sanal makinesini gelişmiş analizler için bir IPython dizüstü sunucu olarak ayarlamak](machine-learning-data-science-setup-virtual-machine.md) IPython dizüstü bilgisayar ve veri bilimi, Azure depolama SQL dışında bir form için durumlarda yapmak için kullanılan diğer araçları ile bir Azure sanal makine sağlamak nasıl gösterir verileri depolamak için kullanılacak.
* [Bir Azure SQL Server sanal makinesini gelişmiş analizler için bir IPython dizüstü sunucu olarak ayarlamak](machine-learning-data-science-setup-sql-server-virtual-machine.md) IPython dizüstü bilgisayar ve veri bilimi durumlarda, bir SQL veritabanı için yapmak için kullanılan diğer araçları ile bir Azure SQL Server sanal makine sağlamak nasıl gösterir verileri depolamak için kullanılacak.

Sağlanan ve yapılandırılmış sonra IPython dizüstü sunucuları araştırması ve veri işleme ve Azure Machine Learning ve takım veri bilimi işlem (TDSP) ile birlikte gereken diğer görevler için bu sanal makineleri, kullanıma hazır. İçinde veri bilimi işlemi sonraki adımlarda eşlenen [TDSP öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve SQL Server ya da Hdınsight, verileri işlemek ve Azure makineyle var. Bu örnek verilerden öğrenmeyi hazırlığı taşıma adımları içerebilir Öğrenme.

> [!NOTE]
> Azure sanal makineler olarak fiyatlandırılır **yalnızca kullandıklarınız için ödeme**. Sanal makinenize kullanmadığınızda ücretlendirilen değil emin olmak için onu olduğu sahip **durduruldu (Deallocated)** durumu [Klasik Azure portalı](http://manage.windowsazure.com/). Adım adım yönergeler veya sanal makine ayırması nasıl için bkz: [kapatma ve sanal makine kullanılmadığında serbest bırakma](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

