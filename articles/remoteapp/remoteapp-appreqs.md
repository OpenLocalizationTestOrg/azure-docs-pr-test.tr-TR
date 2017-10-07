---
title: "Azure RemoteApp için aaaApp gereksinimleri | Microsoft Docs"
description: "Azure remoteapp'te toouse istediğiniz uygulamalar için hello gereksinimleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Uygulama gereksinimleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp akış 32 bit veya 64-bit Windows tabanlı uygulamalar bir Windows Server 2012 R2 görüntüsünden destekler. Varolan 32 bit veya 64-bit Windows tabanlı uygulamaların çoğu Azure Remoteapp'te "olduğu gibi" çalıştırın (Uzak Masaüstü Hizmetleri veya Terminal Hizmetleri önceden bilinen) ortamı. Ancak, çalıştırma ve iyi çalışmasını arasında bir fark - bazı uygulamalar düzgün ve diğerlerinin desteklemediği olsa da gerçekleştirin. Aşağıdaki bilgilerle hello bir Uzak Masaüstü Hizmetleri ortamında uygulamaları geliştirme ve test etme tooensure uyumluluk için yönergeler sağlanmaktadır.

İpucu: Bazı uygulamalar çalışma örnekleri için oluşturduğunuz üzerinde çalışıyoruz. Microsoft Access, QuickBooks ve App-V Remoteapp'te görüşmeniz yeni konular görürsünüz.

## <a name="requirements"></a>Gereksinimler
Bu üç gereksinimleri izlediyseniz, iyi Remoteapp'te çalıştırmak, uygulamanızın yardımcı olur:

1. Tümüne uyan uygulamalar [Windows Masaüstü uygulamaları için sertifika gereksinimleri](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) ve çok uyması[yönergeleri programlama Uzak Masaüstü Hizmetleri](https://msdn.microsoft.com/library/aa383490.aspx) RemoteApp ile tam uyumluluk sahip olur.
2. Uygulamaları hiç veri yerel olarak hello görüntü veya kaybolabilir RemoteApp örnekleri depolamanız gerekir.  RemoteApp koleksiyonu oluşturduktan sonra hello örnekleri kopyalandığı ve durum bilgisiz ve uygulamalar yalnızca içermelidir. Bir dış kaynağa veya hello kullanıcının profilindeki verileri depolar.
3. Özel resimler hiçbir zaman kaybolabilir veri içermelidir.  

## <a name="testing-your-apps"></a>Uygulamalarınızı test etme
Bu adımları tootesting uygulamaları kullanın:

1. Windows Server 2012 R2 ve uygulamanızı yükleyin
2. Uzak Masaüstü'nü etkinleştirme
3. UserA ve userb adlı iki kullanıcı hesapları toohello Uzak Masaüstü güvenlik grubuna ekleme, iki kullanıcı hesabı oluşturun.
4. İki eşzamanlı RDS oturumları toohello PC hello uygulama başlatılırken oluşturarak çoklu oturum uyumluluğunu denetleyin.
5. Uygulamanızın davranışını doğrula

## <a name="application-development-guidelines"></a>Uygulama geliştirme yönergeleri
RemoteApp uygulamaları geliştirmek için yönergeleri izleyerek hello kullanın.

### <a name="multiple-users"></a>Birden çok kullanıcı
* Yükleme bir [tek bir kullanıcı için uygulama ](https://msdn.microsoft.com/library/aa380661.aspx)çok kullanıcılı bir ortamda sorunlara neden olabilir.
* Uygulamaları gereken [kullanıcıya özgü bilgileri depolamak](https://msdn.microsoft.com/library/aa383452.aspx) kullanıcıya özgü konumlarda ayrı olarak genel bilgileri, tooall kullanıcılar geçerlidir.
* RemoteApp kullanan birden çok [çekirdek nesneler için ad alanları](https://msdn.microsoft.com/library/aa382954.aspx); genel ad alanı öncelikle istemci/sunucu uygulamaları hizmetleri tarafından kullanılır.
* Bilgisayar adı veya hello hello güvenli tooassume değil [IP adresi](https://msdn.microsoft.com/library/aa382942.aspx) birden çok kullanıcı aynı anda tooa üzerinde Uzak Masaüstü oturumu ana bilgisayarı (RD Oturumu kaydedilebilir çünkü atanan toohello bilgisayarı tek bir kullanıcıyla ilişkili Ana bilgisayarı) sunucusu.

### <a name="performance"></a>Performans
* Devre dışı [grafik efektleri](https://msdn.microsoft.com/library/aa380822.aspx) uygulama tooRemoteApp eklemeden önce.
* tüm kullanıcılar için toomaximize CPU kullanılabilirlik ya da devre dışı [arka plan görevleri ](https://msdn.microsoft.com/library/aa380665.aspx) veya kaynak kullanımı yoğun olmayan verimli arka plan görevleri oluşturun.
* Ayarlama ve uygulama Bakiye [iş parçacığı kullanımı](https://msdn.microsoft.com/library/aa383520.aspx) çok kullanıcılı, çok işlemcili bir ortam için.
* toooptimize performans, çok uygulamalar için iyi bir uygulama olan[algılamak](https://msdn.microsoft.com/library/aa380798.aspx) çalıştırdıkları bir istemci oturumunda.

