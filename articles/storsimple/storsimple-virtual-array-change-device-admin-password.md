---
title: "Değişiklik StorSimple sanal dizinin cihaz Yönetici parolasının | Microsoft Docs"
description: "Cihaz Yöneticisi parolasını değiştirmek için Azure portal ya da StorSimple sanal dizinin web kullanıcı Arabirimi kullanmayı açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>StorSimple sanal dizinin cihaz Yöneticisi parolasını StorSimple cihaz Yöneticisi aracılığıyla değiştirme

## <a name="overview"></a>Genel Bakış

StorSimple sanal dizisine erişmek için Windows PowerShell arabirimini kullandığınızda, bir cihaz Yöneticisi parolası girmeniz gerekir. StorSimple cihazı ilk sağlandığında başlatıldı ve varsayılan paroladır *Parola1*. Verilerinizin güvenliği için varsayılan parola, oturum açın ve bu parolayı değiştirmek için gerekli ilk kez süresi dolar.

Cihaz, üretim ortamınızda dağıtıldıktan sonra herhangi bir zamanda cihaz Yöneticisi parolasını değiştirmek için yerel web kullanıcı Arabirimi veya Azure portalını kullanabilirsiniz. Bu makalede bu yordamların her biri açıklanmıştır.

 ![Aygıtları dikey penceresi](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a>Parolayı değiştirmek için Azure portalını kullanın

Azure Portalı aracılığıyla cihaz Yöneticisi parolasını değiştirmek için aşağıdaki adımları gerçekleştirin.

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a>Azure Portalı aracılığıyla cihaz Yöneticisi parolasını değiştirmek için

1. Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından içinde **Yönetim** 'yi tıklatın **aygıtları**. Bu açılır **aygıtları** tüm StorSimple sanal dizinin aygıtlarını listeler dikey.

2. İçinde **aygıtları** dikey penceresinde parola değişikliği gerektiren aygıtı çift tıklatın.

3. İçinde **ayarları** , cihazınız için dikey tıklayın **güvenlik**.

4. İçinde **güvenlik ayarları** dikey penceresinde aşağıdakileri yapın:
   
   1. Ekranı aşağı kaydırarak **cihaz Yöneticisi parolasını** bölümü. 8'den 15 karakter içeren bir yönetici parolasını belirtin.
   2. Parolayı onaylayın.
   3. Tıklatın **kaydetmek** dikey pencerenin üstündeki.

Cihaz Yöneticisi parolası şimdi güncelleştirildi. Cihaz yerel olarak erişmek için bu değiştirilmiş parolayı kullanabilirsiniz.

![Güvenlik ayarları dikey penceresi](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a>Parolayı değiştirmek için yerel web kullanıcı arabirimini kullanın

Yerel web kullanıcı Arabirimi aracılığıyla cihaz Yöneticisi parolasını değiştirmek için aşağıdaki adımları gerçekleştirin.

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a>Yerel web kullanıcı Arabirimi aracılığıyla cihaz Yöneticisi parolasını değiştirmek için

1. Yerel web kullanıcı Arabirimi, tıklatın **Bakım** > **parola değişikliği** cihazınız için.
   
    ![Parola1 değiştirme](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Girin **geçerli parola**.
3. Sağlayan bir **yeni parola**. Parola en az 8 karakter uzunluğunda olmalıdır. 3 4 birini içermelidir: büyük harf, küçük harfler, sayısal ve özel karakter.
   
    Parolanızı son 24 parola ile aynı olamayacağını unutmayın.
4. Onaylamak için parolayı yeniden girin.
   
    ![Parola2 değiştirme](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Sayfanın alt kısmındaki tıklatın **Uygula**. Yeni parola şimdi uygulanır. Parola değiştirme başarısız olursa, aşağıdaki hatayı görürsünüz:
   
    ![parola hatası](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Parola başarıyla güncelleştirildikten sonra size bildirilir. Bu değiştirilmiş parola sonra cihaz yerel olarak erişmek için de kullanabilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar
Bilgi edinmek için nasıl [StorSimple sanal dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

