---
title: "Azure RemoteApp görüntüsü aaaCreate | Microsoft Docs"
description: "Azure RemoteApp için görüntüleri oluşturmak için kullanılabilen hello seçenekleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Azure RemoteApp görüntüsü oluşturma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp Kullanıcılarınızla paylaşabilirsiniz görüntüleri toohold hello uygulamaları kullanır. (Biz görüntünüzü alın ve bunu Azure RemoteApp oturum açtığınızda ne hello kullanıcıların erişimi kullanıcının toocreate VM'ler - kullanın.) Bulut veya karma, olup toocreate uygulamaların tercih ettiğiniz ile bir Azure RemoteApp koleksiyonu, yüklü Bu uygulamalarla görüntü oluşturmaya başlayın. Ardından, bu görüntüyü kullanan bir koleksiyon oluşturun, toohello koleksiyonu kullanıcılar atayın ve uygulamaları toothose kullanıcılar yayımlama.

Oluşturma veya görüntüleri kullanmak için birkaç seçeneğiniz vardır. Merhaba temel [gereksinim](remoteapp-imagereqs.md) için görüntüyü Windows Server 2012 R2 çalıştıran ve hello Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü yüklü olması. Size nasıl şeyler ilginç nereden olur.

Tooimages geldiğinde seçenekleri aşağıdaki hello vardır:

* İçeri aktarma ve kullanabileceğiniz bir [görüntünün temel bir Azure sanal makinede](remoteapp-image-on-azurevm.md). Bu, özel ayarlar gerektiren satır iş kolu uygulamaları için uygundur. Merhaba görüntü toowork hello uygulama için özelleştirebilirsiniz.
* Yapabilecekleriniz [özel bir görüntü oluşturup](remoteapp-create-custom-image.md). Şirket içi Uzak Masaüstü Hizmetleri dağıtımınız için kullandığınız bir görüntü zaten varsa bu kullanışlıdır.
* Merhaba birini kullanabilirsiniz [şablon görüntüleri](remoteapp-images.md) RemoteApp aboneliğinize dahil. Bu görüntüleri oluşturulur ve hello RemoteApp ekibi tarafından korunan ve bazı standart uygulama kullanılabilir tooyour kullanıcılar yapabilir (gibi hello Office suite) içerir. Yalnızca bu hello Office 365 Pro Plus görüntüyü bir üretim ortamında kullanılabileceğini unutmayın.

Görüntünüzü nereden veya oluşturduğunuz nasıl bağımsız olarak toomake hello anladığınızdan emin isteyeceksiniz [uygulama gereksinimleri](remoteapp-appreqs.md) iyi Remoteapp'te uygulamanızı çalışır tooensure. Ardından, hello sonraki toocreate adımdır bir [bulut](remoteapp-create-cloud-deployment.md) veya [karma](remoteapp-create-hybrid-deployment.md) koleksiyonu.

