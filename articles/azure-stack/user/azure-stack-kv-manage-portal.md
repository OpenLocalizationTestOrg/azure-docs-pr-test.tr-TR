---
title: "Portalı kullanarak Azure yığınında anahtar kasası yönetme | Microsoft Docs"
description: "Anahtar kasası Azure yığınında portalını kullanarak yönetmeyi öğrenin"
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: D4300668-461F-45F6-BF3B-33B502C39D17
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: mabrigg
ms.openlocfilehash: d76a1e188c5a5bf008ac2fba9b43741a6a8d97b1
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="manage-key-vault-in-azure-stack-by-using-the-portal"></a>Anahtar kasası Azure yığınında Portalı'nı kullanarak yönetme

Anahtar kasası Azure yığınında Azure yığın portalını kullanarak yönetebilirsiniz. Bu makalede oluşturmak ve bir anahtar kasası Azure yığınında yönetmek için çalışmaya başlamanıza yardımcı olur. 

## <a name="prerequisites"></a>Ön koşullar  

Azure anahtar kasası hizmetindeki içeren bir teklif abone olmalısınız.
 
## <a name="create-a-key-vault"></a>Bir anahtar kasası oluşturma 

1. Oturum [kullanıcı portalı](https://portal.local.azurestack.external).  

2. Panodan seçin **yeni** > **güvenlik + kimlik** > **anahtar kasası**.  

    ![Anahtar kasası ekranı](media/azure-stack-kv-manage-portal/image1.png)  

3. İçinde **anahtar kasası oluşturma** bölmesinde, Ata bir **adı** kasanız için. Kasa adı yalnızca alfasayısal karakterler ve özel karakter kısa çizgi (-) içerebilir. Bunlar, bir rakamla başlayamaz döndürmemelidir.  

4. Seçin bir **abonelik** kullanılabilir abonelikler listesinden. Anahtar kasası hizmeti sunan tüm abonelikleri aşağı açılan listede görüntülenir.  

5. Var olan seçin **kaynak grubu** veya yeni bir tane oluşturun.  

6. Seçin **fiyatlandırma katmanı**.  
    >[!NOTE]
    > Anahtar kasalarını Azure yığın Geliştirme Seti Destek **standart** SKU'ları yalnızca.

7. Varolan birini **erişim ilkeleri** veya yeni bir tane oluşturun. Bir erişim ilkesi, bir kullanıcı, uygulama veya bir güvenlik grubu bu kasaya işlemlerini gerçekleştirmek izinler sağlar.  

8. İsteğe bağlı olarak, seçin bir **Gelişmiş erişim ilkesi** özellikleri etkinleştirmek için gibi sanal makinelerle (VM'ler) dağıtımı için Resource Manager şablonu dağıtımı için Access'e ve erişmek için Azure Disk şifrelemesi için birim şifrelemesi. 
  
9.  Ayarlarını yapılandırdıktan sonra Seç **Tamam**ve ardından **oluşturma**. Bu, anahtar kasası dağıtım başlatır. 

## <a name="manage-keys-and-secrets"></a>Anahtarları ve gizli anahtarları Yönet

Bir kasası oluşturduktan sonra anahtarları ve gizli anahtarları kasa içinde oluşturmak ve yönetmek için aşağıdaki adımları kullanın.

### <a name="create-a-key"></a>Bir anahtar oluşturma

1. Oturum [kullanıcı portalı](https://portal.local.azurestack.external).  

2. Panodan seçin **tüm kaynakları**, daha önce oluşturduğunuz anahtar kasasının seçin ve ardından **anahtarları** döşeme.  

3. İçinde **anahtarları** bölmesinde, **Ekle**. 

4. İçinde **bir anahtar oluşturma** bölmesinden listesini **seçenekleri**, bir anahtar oluşturmak için kullanmak istediğiniz yöntemi seçin. Yapabilecekleriniz **Oluştur** yeni bir anahtar **karşıya** var olan bir anahtar veya kullanın **geri yedekleme** bir anahtar yedeklemesini seçmek için.  

5. Girin bir **adı** anahtarınız için. Anahtar adı yalnızca alfasayısal karakterler ve özel karakter kısa çizgi (-) içerebilir.  

6. İsteğe bağlı olarak, yapılandırma **ayarlamak etkinleştirme tarihi** ve **sona erme tarihi ayarlamak** anahtarınızın değerlerini.  

7. Seçin **oluşturma** dağıtımı başlatmak için.  

Anahtar başarıyla oluşturulduktan sonra bunu altında seçebilirsiniz **anahtarları** görüntülemek ve özelliklerini değiştirin. Özellikler bölümü içerir **anahtarı tanımlayıcısı**, bir Tekdüzen Kaynak Tanımlayıcısı (olarak dış uygulamalar bu anahtarı erişebilir URI) olduğu. Bu anahtar üzerinde işlemler sınırlamak için ayarları yapılandırma **işlemlerine izin**.

![URI anahtarı](media/azure-stack-kv-manage-portal/image4.png)  

### <a name="create-a-secret"></a>Gizli anahtar oluşturma 

1. Oturum [kullanıcı portalı](https://portal.local.azurestack.external).  
2. Panodan seçin **tüm kaynakları**, daha önce oluşturduğunuz anahtar kasasının seçin ve ardından **gizli** döşeme.  

3. Altında **gizli**seçin **Ekle**.  

4. Altında **gizli anahtar oluşturma**, listesinden **karşıya yükleme seçenekleri**, filtrelemede kullanmak istediğiniz bir gizli anahtar oluşturmak bir seçenek belirleyin. Gizli anahtar oluşturma **el ile** gizli veya karşıya yükleme için bir değer girerseniz, bir **sertifika** yerel makinenizden.  

5. Girin bir **adı** gizliliği için. Gizli anahtar adı yalnızca alfasayısal karakterler ve özel karakter kısa çizgi (-) içerebilir.  

6. İsteğe bağlı olarak, belirtin **içerik türü**ve değerlerini yapılandırmak **ayarlamak etkinleştirme tarihi** ve **sona erme tarihi ayarlamak** gizliliği için.  

7. Seçin **oluşturma** dağıtımı başlatmak için.  

Gizli başarıyla oluşturulduktan sonra bunu altında seçebilirsiniz **gizli** görüntülemek ve özelliklerini değiştirin. Özellikler bölümü içeren bir **gizli tanımlayıcısı**, olarak dış uygulamalar bu gizli erişebileceği bir URI değil. 

![URI gizli](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a>Sonraki adımlar
* [Anahtar kasasında depolanan parola alarak VM dağıtma](azure-stack-kv-deploy-vm-with-secret.md) 
* [Anahtar kasasında depolanan sertifika ile bir VM'yi dağıtmak](azure-stack-kv-push-secret-into-vm.md)     


