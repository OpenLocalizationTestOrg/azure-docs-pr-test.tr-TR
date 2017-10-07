---
title: "aaaMicrosoft Azure StorSimple ve bulut çözümleri sağlayıcısı Program genel bakış | Microsoft Docs"
description: "StorSimple iş ortakları için bir genel bakış hello StorSimple ve CSP hakkında."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a>StorSimple sanal dizinin bulut çözümü sağlayıcısı programı için dağıtma

## <a name="overview"></a>Genel Bakış

StorSimple sanal dizinin müşterileri için hello bulut çözümü sağlayıcısı (CSP) iş ortakları tarafından dağıtılabilir. Bir CSP ortak bir StorSimple cihaz Yöneticisi hizmeti oluşturabilirsiniz. Bu hizmet, ardından kullanılan toodeploy olması ve StorSimple sanal dizinin yönetmek ve paylaşımları, birimler ve yedekleme hello ilişkili.

Bu makalede, nasıl bir CSP ortak bir müşteri veya yeni bir abonelik tooan varolan müşteri ekleyin ve sonra hizmet toodeploy bir StorSimple sanal dizi CSP oluşturun açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce emin olun:

- Merhaba CSP program altında kaydedilir.
- Geçerli sahip [ortağı Merkezi'nde](http://partnercenter.microsoft.com/) oturum açma kimlik bilgileri. Merhaba kimlik toosign toohello iş ortağı portalı tooadd yeni müşteriler etkinleştirmek, müşteriler için arama veya tooa müşteri hesabı hello iş ortağı panosundan gidin. Merhaba CSP hello Azure portal hello müşteri adına bir StorSimple Yöneticisi olarak işlev görebilir.
                             
## <a name="add-a-customer"></a>Bir müşteri ekleyin

Bir müşteri eklerseniz, bir abonelik otomatik olarak oluşturulur. bir müşteri tooadd (ve otomatik olarak bir abonelik oluşturun), hello aşağıdaki hello iş ortağı Portalı'ndaki adımları gerçekleştirin.

1. Toohello Git [ortağı Merkezi'nde](http://partnercenter.microsoft.com/) ve CSP kimlik bilgilerinizi kullanarak oturum açın. Tıklatın **Pano**.

     ![İş ortağı Merkezi'nde Panosu](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. Merhaba sol-bölmesinde **müşteriler**. Merhaba sağ-bölmesinde **müşteriler eklemek**. Merhaba müşteri Hello ayrıntılarını girin. Tıklatın **sonraki: abonelikleri** toocreate bir müşteri aboneliğe.

    ![Müşteri ekleme](./media/storsimple-partner-csp-deploy/image2.png)

3.  Seçin **Microsoft Azure** sunar. Kaydırma toohello alt hello sayfasını tıklatın ve **gözden**.

    ![Abonelik bilgileri gözden geçirin](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. Merhaba bilgileri gözden geçirin ve tıklayın **gönderme**.

    ![Abonelik gönderme](./media/storsimple-partner-csp-deploy/image4.png)

5. İleride kullanılmak üzere Hello onay bilgilerini kaydedin.

    ![Kaydetme onayı](./media/storsimple-partner-csp-deploy/image5.png)

6. Bulma veya yeni eklediğiniz toohello müşteri gidin. Merhaba tıklatın **şirket adı** hello ayrıntıları içine aşağı toodrill.

    ![Merhaba müşteri arayın](./media/storsimple-partner-csp-deploy/image6.png)  

7. Merhaba sol bölmede seçin **Hizmet Yönetimi**. Merhaba altında sağ bölmede, içinde **yönetmek Hizmetleri**, tıklatın **Microsoft Azure Yönetim Portalı** içinde toosign müşteri için Azure yönetici olarak.

    ![TooAzure Portalı'nda oturum açın](./media/storsimple-partner-csp-deploy/image9.png)

8. toocreate StorSimple cihaz Yöneticisi tıklatın **+ yeni** ve arayın veya çok gidin**StorSimple sanal cihaz seri**. Daha fazla bilgi için çok Git[StorSimple Aygıt Yöneticisi'ni hizmet dağıtma](storsimple-virtual-array-manage-service.md).

    ![StorSimple cihaz Yöneticisi hizmeti oluşturma](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a>Bir abonelik Ekle

Bazı durumlarda, varolan bir müşteri olabilir ve tooadd bir abonelik gerekiyor. tooadd bir abonelik tooan varolan müşteri hello aşağıdaki hello iş ortağı Portalı'ndaki adımları gerçekleştirin.

1. Toohello Git [ortağı Merkezi'nde](http://partnercenter.microsoft.com/) ve CSP kimlik bilgilerinizi kullanarak oturum açın. Tıklatın **Pano**.

     ![İş ortağı Merkezi'nde Panosu](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. Merhaba sol-bölmesinde **müşteriler**. Bulma veya aboneliği tooadd istediğiniz toohello müşteri gidin. Merhaba tıklatın ![genişletme onay simgesi](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) simgesi tooexpand hello satır hello şirket adı, müşteriniz için. Merhaba Ayrıntılar tıklatın **abonelik ekleme**.

    ![Müşteriler](./media/storsimple-partner-csp-deploy/image10.png)

3. Denetleyin **Microsoft Azure** hello için **üst teklifleri** hello abonelik ve tıklatın **gönderme**. Bu, yeni bir abonelik oluşturur.

    ![Yeni Abonelik Ekle](./media/storsimple-partner-csp-deploy/image11.png)

6. Yeni bir abonelik oluşturulduktan sonra tıklatın **<--müşteriler** hello sol bölmede tooreturn toohello içinde **müşteriler** sayfası. Kendisi için bir abonelik oluşturduğunuz hello müşteri arayın. Merhaba tıklatın **şirket adı** hello ayrıntıları içine aşağı toodrill.

    ![Merhaba müşteri arayın](./media/storsimple-partner-csp-deploy/image6.png)  

7. Merhaba sol bölmede seçin **Hizmet Yönetimi**. Merhaba altında sağ bölmede, içinde **yönetmek Hizmetleri**, tıklatın **Microsoft Azure Yönetim Portalı** içinde toosign müşteri için Azure yönetici olarak.

    ![TooAzure Portalı'nda oturum açın](./media/storsimple-partner-csp-deploy/image9.png)

8. toocreate StorSimple cihaz Yöneticisi tıklatın **+ yeni** ve arayın veya çok gidin**StorSimple sanal cihaz seri**. Daha fazla bilgi için çok Git[StorSimple Aygıt Yöneticisi'ni hizmet dağıtma](storsimple-virtual-array-manage-service.md).

    ![StorSimple cihaz Yöneticisi hizmeti oluşturma](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a>Sonraki adımlar

- CSP hello StorSimple daha fazla sorularınız varsa, çok gidin[CSP StorSimple: sık sorulan sorular](storsimple-partner-csp-faq.md).
- Kullanıyorsanız toodeploy, StorSimple Git çok hazır[, StorSimple CSP içinde dağıtmak](storsimple-partner-csp-deploy.md).
