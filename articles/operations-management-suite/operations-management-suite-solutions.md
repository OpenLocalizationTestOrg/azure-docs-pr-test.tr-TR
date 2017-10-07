---
title: aaaSolutions Operations Management Suite (OMS) | Microsoft Docs
description: "Çözümleri genişletmek hello işlevselliği Operations Management Suite (OMS) paketlenmiş yönetim senaryoları sağlayarak müşteriler tootheir OMS çalışma ekleyebilirsiniz.  Bu makalede, müşterileri ve ortakları tarafından oluşturulan nasıl özel çözümler hakkında ayrıntılar sağlar."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Yönetim çözümleri Operations Management Suite (OMS) (Önizleme) içinde ile çalışma
> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri için ön belgesidir.    
> 
> 

Yönetim çözümleri genişletmek hello işlevselliği Operations Management Suite (OMS) paketlenmiş yönetim senaryoları sağlayarak müşteriler tootheir ortamına ekleyebilirsiniz.  Ayrıca çok[Microsoft tarafından sağlanan çözüm](../log-analytics/log-analytics-add-solutions.md), iş ortakları ve müşterileri kendi ortamında kullanılan veya hello topluluk aracılığıyla kullanılabilir toocustomers yapılan yönetim çözümleri toobe oluşturabilirsiniz.

## <a name="finding-and-installing-management-solutions"></a>Bulma ve yönetim çözümleri yükleme
Bulma ve yönetim çözümleri hello aşağıdaki bölümlerde açıklandığı gibi yükleme için birden çok yöntem bulunmaktadır.

### <a name="azure-marketplace"></a>Azure Market
Yönetim çözümleri Microsoft tarafından sağlanan ve güvenilen ortaklar hello Azure Marketi hello Azure Portalı'ndan yüklenebilir.

1. Toohello Azure portalında oturum açın.
2. Merhaba sol bölmesinde seçin **daha fazla hizmet**.
3. Ya da aşağı kaydırın çok**çözümleri** veya türü *çözümleri* hello içine **filtre** iletişim.
4. Merhaba tıklatın **+ Ekle** düğmesi.
5. Arama ya giderek, ilgilendiğiniz çözümleri için hello tıklatarak **filtre** düğmesini veya hello yazarak **arama Everthing** kutusu.
6. Market öğesi tooview ayrıntılı bilgilerini'ı tıklatın.
7. Tıklatın **oluşturma** tooopen hello **Çözüm Ekle** bölmesi.
8. Hello gibi istendiğinde toorequired bilgileri olacaktır [OMS çalışma ve Automation hesabı](#oms-workspace-and-automation-account) toovalues herhangi bir parametre için çözüm ayrıca hello.
9. Tıklatın **oluşturma** tooinstall hello çözümü.

### <a name="oms-portal"></a>OMS portalı
Microsoft tarafından sağlanan yönetim çözümleri hello Çözümleri Galerisi hello OMS Portalı'ndan yüklenebilir.

1. İçinde toohello OMS portalında oturum açın.
2. Merhaba tıklatın **Çözümleri Galerisi** döşeme.
3. Merhaba OMS Çözümleri Galerisi sayfasında, her kullanılabilir bir çözüm hakkında bilgi edinin. Merhaba çözüm tooadd tooOMS istediğiniz Hello adına tıklayın.
4. Seçtiğiniz hello çözüm başlangıç sayfasında, hello çözümü hakkında ayrıntılı bilgi görüntülenir. **Ekle**'ye tıklayın.
5. OMS genel bakış sayfasında hello ve verilerinizi hello OMS hizmetine işledikten sonra kullanmaya başlayabilmeniz için görünür eklenen hello çözüm için yeni bir kutucuk.

### <a name="azure-quickstart-templates"></a>Azure Hızlı Başlangıç Şablonları
Merhaba topluluk üyeleri yönetim çözümleri tooAzure hızlı başlangıç şablonlarını gönderebilirsiniz.  Sonraki yüklemesi için bu şablonları yükleyebilirsiniz veya bunları nasıl çok toolearn incelemek[kendi çözümleri oluşturma](#creating-a-solution).

1. Açıklanan hello süreci izleyin [OMS çalışma ve Automation hesabı](#oms-workspace-and-automation-account) toolink çalışma ve hesap.
2. Çok Git[Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).  
3. İlgilendiğiniz bir çözüm arayın.
4. Merhaba çözümü hello sonuçları tooview ayrıntılarını seçin.
5. Merhaba tıklatın **tooAzure dağıtmak** düğmesi.
6. Merhaba kaynak grubunu ve konumu toplama toovalues hello çözümdeki herhangi bir parametre için de gibi istendiğinde tooprovide bilgileri olacaktır.
7. Tıklatın **satın alma** tooinstall hello çözümü.

### <a name="deploy-azure-resource-manager-template"></a>Azure Resource Manager şablonu dağıtma
Merhaba topluluk veya sizin alma çözümleri [kendiniz oluşturmanız](#creating-a-solution) Resource Manager şablonu uygulanır ve hello için standart yöntemlerden herhangi birini kullanabilirsiniz [bir şablonu dağıtmayı](../azure-resource-manager/resource-group-template-deploy-portal.md).  Merhaba çözüm yüklemeden önce oluşturmalı ve bağlantı hello olduğunu Not [OMS çalışma ve Automation hesabı](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>OMS çalışma ve Automation hesabı
Çoğu yönetim çözümleri gerektiren bir [OMS çalışma](../log-analytics/log-analytics-manage-access.md) toocontain görünümleri ve bir [Otomasyon hesabı](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook'ları ve ilgili kaynakları. Çalışma alanı hello ve hesap hello aşağıdaki gereksinimleri karşılaması gerekir.

* Bir çözümü, yalnızca bir OMS çalışma ve bir Automation hesabı kullanabilirsiniz.  
* Merhaba OMS çalışma ve bir çözüm tarafından kullanılan Otomasyon hesabı bağlı tooone olmalıdır başka bir. Bir OMS çalışma yalnızca bağlantılı tooone Otomasyon hesabı olabilir ve bir Otomasyon hesabı yalnızca bağlantılı tooone OMS çalışma olabilir.
* toobe bağlı, hello OMS çalışma ve hello aynı kaynak grubu ve bölge Otomasyon hesabı olması gerekir.  Merhaba istisnadır Doğu ABD bölgesinde bir OMS çalışma ve ve Automation hesabında Doğu ABD 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Bir OMS çalışma ve Otomasyon hesabı arasında bir bağlantı oluşturuluyor
Nasıl hello OMS çalışma alanını ve Automation hesabı hello yükleme yöntemi, çözümünüz için bağlıdır.

* Microsoft Çözüm hello OMS portalı üzerinden yüklediğinizde hello geçerli OMS çalışma alanında yüklenir ve herhangi bir Otomasyon hesabı gereklidir.
* Hello Azure Market üzerinden bir çözüm yüklediğinizde, bir OMS çalışma ve Otomasyon hesabı için istenir ve aralarındaki hello bağlantı sizin için oluşturulur.  
* Hello Azure Market dışında çözümleri için hello OMS çalışma ve Automation hesabı hello çözüm yüklemeden önce bağlanmalıdır.  Hello Azure Marketi herhangi bir çözüm ve hello OMS çalışma ve Automation hesabı seçerek bunu yapabilirsiniz.  Merhaba OMS çalışma ve Automation hesabı seçili hemen hello bağlantı oluşturulacağından hello çözümü yüklemek tooactually yok.  Ardından Hello bağlantısı oluşturulduktan sonra herhangi bir çözümü bu OMS çalışma ve Automation hesabı kullanabilirsiniz. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Bir OMS çalışma ve Otomasyon hesabı arasında Hello bağlantı doğrulanıyor
Bir OMS çalışma ve hello aşağıdaki yordamı kullanarak bir Otomasyon hesabı arasında hello bağlantı doğrulayabilirsiniz.

1. Hello Azure portal Hello Otomasyon hesabı seçin.
2. Merhaba kaydırma toohello alt **ayarları** bölmesi.
3. Adlı bir bölüm olup olmadığını **OMS Kaynakları** hello içinde **ayarları** bölmesi, sonra bu hesabı ekli tooan OMS çalışma alanıdır.
4. Seçin **çalışma** tooview hello hello OMS çalışma ayrıntılarını toothis Otomasyon hesabına bağlanır.

## <a name="listing-management-solutions"></a>Yönetim çözümleri listeleme
Aşağıdaki yordam tootooview hello yönetim çözümlerine hello çalışma alanları bağlantılı tooyour Azure aboneliği hello kullanın.

1. Toohello Azure portalında oturum açın.
2. Merhaba sol bölmesinde seçin **daha fazla hizmet**.
3. Ya da aşağı kaydırın çok**çözümleri** veya türü *çözümleri* hello içine **filtre** iletişim.
4. Tüm çalışma alanlarında yüklü çözümleri listelenir.

Merhaba geçerli çalışma hello OMS portalı kullanarak alanında yalnızca hello Microsoft çözümleri görüntüleyebilirsiniz unutmayın.

## <a name="removing-a-management-solution"></a>Bir yönetim çözümü kaldırma
Bir yönetim çözümü kaldırıldığında, hello Çözümdeki tüm kaynaklar da kaldırılır.  

1. Merhaba çözüm hello Azure bulun hello yordamda kullanarak portal [çözümleri listeleme](#listing-solutions).
2. Tooremove istediğiniz hello çözümü seçin.
3. Merhaba tıklatın **silmek** düğmesi.

## <a name="creating-a-management-solution"></a>Bir yönetim çözümü oluşturma
Yönetim çözümleri oluşturma konusunda tam yönergeler şurada bulunabilir [Operations Management Suite (OMS) çözümleri oluşturma](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Sonraki adımlar
* Arama [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates) farklı Resource Manager şablonları örneklerini için.
* Kendinizinkini oluşturun [yönetim çözümleri](operations-management-suite-solutions-creating.md).

