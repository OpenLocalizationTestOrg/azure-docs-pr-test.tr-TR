---
title: "Machine Learning çalışma alanı aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure Machine Learning Studio'da bir çalışma alanı"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Bir Azure Machine Learning çalışma alanı oluşturma ve paylaşma
Bu menü hello yukarı tooset çeşitli veri bilimi ortamları hello Cortana analitik işlem (CAP) tarafından nasıl kullanılacağını açıklamaktadır tootopics bağlar.

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Azure Machine Learning Studio toouse toohave Machine Learning çalışma alanı gerekir. Bu çalışma alanı toocreate ihtiyacınız hello araçları içerir, yönetmek ve denemeler yayımlama.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate bir çalışma alanı
1. İçinde toohello oturum [Azure portalı](https://portal.azure.com/)

    > [!NOTE]
    > içinde toosign ve çalışma alanı oluşturma, toobe Azure Abonelik Yöneticisi gerekir. 
    >
    > 

2. Tıklatın **+ yeni**

3. Seçin **Intelligence + analiz**, tıklatın **Machine Learning çalışma alanı**, ardından **oluştur**

4. Çalışma alanı bilgilerinizi girin

    - Merhaba *çalışma alanı adı* too260 karakter, bir boşluk bitiş değil yukarı olabilir. Merhaba adı şu karakterleri içeremez:`< > * % & : \ ? + /`
    - Merhaba *web hizmeti planı* , seçin (veya oluşturun), ilişkili hello birlikte *fiyatlandırma katmanı* seçin, web hizmetleri bu çalışma alanından dağıtırsanız kullanılır.

    ![Yeni bir çalışma alanı oluşturma](media/machine-learning-create-workspace/create-new-workspace.png)

5. **Oluştur**'a tıklayın

Merhaba çalışma dağıtıldığında, Machine Learning Studio'da açabilirsiniz.

1. TooMachine Learning Studio Gözat adresindeki [https://studio.azureml.net/](https://studio.azureml.net/).

2. Çalışma alanınızı hello üst sağ taraftaki köşedeki seçin.

    ![Çalışma alanı seçin](media/machine-learning-create-workspace/open-workspace.png)

3. Tıklatın **denemelerim**.

    ![Açık denemeleri](media/machine-learning-create-workspace/my-experiments.png)

Çalışma alanınızı yönetme hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md).
Çalışma alanınızı oluşturulurken bir sorunla karşılaşırsanız, bkz: [sorun giderme kılavuzu: oluşturmak ve tooa Machine Learning çalışma alanı bağlanmak](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Bir Azure Machine Learning çalışma alanı paylaşımı
Machine Learning çalışma alanı oluşturulduktan sonra kullanıcılar tooyour çalışma tooshare erişim tooyour çalışma ve tüm alt denemeler, veri kümeleri, dizüstü bilgisayarlar, vb. davet edebilirsiniz. Kullanıcılar iki rolleri ekleyebilirsiniz:

* **Kullanıcı** -çalışma kullanıcı oluşturmak, açın, değiştirmek ve silmek denemeler, veri kümeleri, vb. hello çalışma alanında.
* **Sahibi** - sahibi davet edebilir ve Kaldır kullanıcıların eklenmesi toowhat bir kullanıcı olarak hello çalışma alanında yapabilirsiniz.

> [!NOTE]
> Merhaba çalışma alanı oluşturur hello yönetici hesabı, çalışma alanı sahibi olarak toohello çalışma alanı otomatik olarak eklenir. Ancak, abonelik olmayan, otomatik olarak diğer Yöneticiler veya kullanıcılar toohello çalışma erişim verilen - tooinvite ihtiyacınız bunları açıkça.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare bir çalışma alanı

1. Learning Studio'ya tooMachine içinde oturum [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. Merhaba sol panelinde tıklatın **ayarları**

3. Merhaba tıklatın **kullanıcılar** sekmesi

4. Tıklatın **daha fazla kullanıcı davet** hello sayfa hello altındaki

    ![Studio ayarları](media/machine-learning-create-workspace/settings.png)

5. Bir veya daha fazla e-posta adresi girin. Merhaba kullanıcıların geçerli bir Microsoft hesabı veya kurumsal bir hesap (Azure Active Directory'den) gerekir.

6. Sahibi veya kullanıcı olarak tooadd hello kullanıcılar istediğinizi seçin.

7. Merhaba tıklatın **Tamam** onay işareti düğmesine.

Eklediğiniz her bir kullanıcı çalışma toohello toosign nasıl paylaşılacağını hakkında yönergeler içeren bir e-posta alırsınız.

> [!NOTE]
> Kullanıcıların toobe mümkün toodeploy için veya bu çalışma alanında web hizmetleri yönetmek için katkıda bulunan veya hello Azure abonelik yöneticisi olmanız gerekir. 



