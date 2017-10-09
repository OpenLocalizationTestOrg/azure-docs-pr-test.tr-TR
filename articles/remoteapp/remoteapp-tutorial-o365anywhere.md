---
title: "aaaGet hello Azure RemoteApp ile herhangi bir cihazda aynı Office 365 deneyimini | Microsoft Docs"
description: "Bilgi nasıl tooshare kullanıcılarınız Azure RemoteApp kullanarak herhangi bir Office 365 uygulama."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get hello aynı Azure RemoteApp ile herhangi bir cihazda Office 365 deneyimini
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bu makalede ele alınacaktır nasıl toodeploy Office 365 şirket içinde herhangi bir cihazda. Kullanıcılarınızın aynı yetenekleri hello alabilir ve kullanıcı Arabirimi, Android, Apple ve Windows deneyimi.

Bunu Azure’da kullanıcıların bağlanabileceği ölçeklenebilir sanal makinelerde Office 365’i barındırmak için Azure RemoteApp kullanarak yapabiliriz. Bu sanal makineler kümesi "bulut koleksiyonu" olarak adlandırılır.

## <a name="create-a-cloud-collection"></a>Bulut koleksiyonu oluşturma
Bir Azure hesabı oluşturduktan sonra ilk çok gidin**RemoteApp** yan sol hello hello bağlantısına tıklayarak.
![Azure Portal hello üzerinde Azure RemoteApp gösteriliyor](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Tıklayarak devam **yeni** hello alt ve "Hızlı oluşturma" bir koleksiyon. Ad, hello bölge, hello abonelik, hello plan ve sağlamış olduğumuz "Office Proffesional 2013" hello görüntü sağlar.
![Oluştur İletişim Kutusu](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

İşiniz bittiğinde hello form hello koleksiyon oluşturma süreci başlamalıdır. Bu tooan saat veya bunu sürebilir.

![Bekleniyor](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Merhaba işlem tamamlandığında, aşağıdakine benzer görünecektir. **Yayımlama**’ya tıkladığımızda, çoğu Office uygulamasının bizim için zaten yayımlandığını görebiliriz.
![Oluşturulan koleksiyon](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Yayımlanan uygulamalar](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

Bu noktada ayrıca tıklayarak erişim toothis koleksiyonuna sahip daha fazla kullanıcı ekleyebilirsiniz **kullanıcı erişimini**.
![Kullanıcı erişimini yapılandırma](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Şimdi tooOffice 365 bağlanmayı deneyelim!

## <a name="connect-toooffice-365"></a>TooOffice 365 Bağlan
Biz üzerinden çok head[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), aşağı kaydırın ve tıklayın **istemcileri indir** kullandığınız hello aygıttaki tooinstall hello Azure RemoteApp istemcisi. Merhaba ekran görüntüleri Windows içindir.

Merhaba uygulaması başladıktan sonra (eski adıyla "Live ID") Microsoft hesabınızla oturum toosign istenir, kullanım hello aynı Azure hesabınızda şu an için. Oturum açtığınızda yeni davetlerle ilgili bir bildirim görürsünüz, buna tıkladığınızda aşağıdakine benzer bir liste görüntülenir. Azure hesabı sahibinin e-posta ile eşleşen hello daveti kabul edin.

![Yeni davet](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Yeni davetler olduğunda bu şekilde görünür.

![Uygulama kabul etme](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Merhaba daveti kabul ettikten sonra hello Azure RemoteApp istemcisindeki tüm hello Office uygulamalarını görmeniz gerekir.

![Uygulama listesi](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Bu Merhaba uygulaması hiçbirinde tıklattığınızda üzerinde hello Azure sanal makinesi ile başlamalı ve, hepsi bu kadar! Keyfini çıkarın!

![başlatma](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

