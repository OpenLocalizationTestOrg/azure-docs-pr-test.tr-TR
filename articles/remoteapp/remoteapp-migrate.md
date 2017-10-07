---
title: "Azure RemoteApp aaaMigrate kullanıcı verilerini | Microsoft Docs"
description: "Bilgi nasıl toomigrate kullanıcı verilerinizi Azure RemoteApp ve."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>Nasıl toomigrate veri içine ve dışına Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Birçok farklı araçlar ve yöntemleri tootransfer kullanabileceğiniz [kullanıcı verilerini](remoteapp-upd.md) içine ve dışına Azure RemoteApp. Bazı yöntemler şunlardır:

* Kopyala ve Yapıştır Pano paylaşımını kullanma
* Dosyaları ve verileri tooa dosya sunucusuna kopyalayın
* Dosyaları tooOneDrive iş için bir tarayıcı üzerinden kopyalayın.
* Yeniden yönlendirme kullanarak dosyaları kopyalama

> [!NOTE]
> Merhaba OneDrive iş veya tüketici eşitleme aracılar için - etkinleştiremiyor bunlar [desteklenmez](remoteapp-onedrive.md) Azure remoteapp'te.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Kopyala ve Yapıştır dosya Gezgini'nde kullanın
Kopyala ve Yapıştır hello Pano kullanarak RemoteApp dağıtımlarda etkin [varsayılan](remoteapp-redirection.md). Bu, kullanıcıların kendi yerel bilgisayar ve RemoteApp uygulamalar arasında dosya kopyalama sağlar. Genellikle, RemoteApp uygulamaları kullanmanın hello normal seyrinde, kullanıcıların dosyalarını tootheir UPD - RemoteApp dışında veri kadar kolay olduğunu taşıma kaydetmiş:

1. [Bir uygulama olarak dosya Gezgini yayımlama](remoteapp-publish.md) RemoteApp koleksiyonunda. (Bu bir yönetim görevi olduğunu unutmayın.)
2. Kullanıcıların toolaunch hello dosya Gezgini uygulamasını yayımladığınız ve toouse toocopy ve Yapıştır dosyaların hem kendi UPD içine ve onu dışına doğrudan.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Standart ağ dosya kopyalama kullanarak dosyaları ve verileri tooa dosya sunucusu yükleyin
Genellikle kuruluş dosya sunucuları toostore genel verileri kullanır. Hello sunucu adı veya konumu biliyorsanız, kullanıcılarınızın hello sunucusu yerel ağa hello göz atın ve çok yukarıda menülerin gibi kendi dosyalarını kopyalayın. Yeniden toopublish dosya Gezgini tooRemoteApp istediğiniz ve kullanıcılarınızla paylaşabilirsiniz.

> [!NOTE]
> Merhaba dosya sunucusu ağda RemoteApp içine dağıtılan hello yönlendirilebilir olmalıdır.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>İş için dosyaları tooOneDrive kopyalama
Merhaba OneDrive iş eşitleme Aracısı remoteapp'te etkinleştiremiyor rağmen hala dosyaları, UPD tooOneDrive iş için bir tarayıcı üzerinden kopyalayabilirsiniz. 

1. Dosya Gezgini tooRemoteApp yayımlayabilir ve kullanıcıların tooaccess dosyalar bu uygulama ile Merhaba söyleyin. 
2. Sıkıştırılma biçimini, kullanıcıların tüm hello dosyaları toomove tooOneDrive iş için içeren bir .zip dosyası oluşturmanız gerekir böylece kolay tootransfer dosyaları olur.
3. Kullanıcılar toogo toohello Office 365 portalı, isteyin ve sonra tooOneDrive gidin ve hello .zip dosyasını karşıya yükleyin.

## <a name="copy-files-by-using-drive-redirection"></a>Sürücü yeniden yönlendirme kullanarak dosyaları kopyalayın
Etkinleştirdiyseniz [sürücüyü yeniden yönlendirme](remoteapp-redirection.md), kullanıcılarınız için eşlenmiş bir sürücüyü zaten oluşturulmuş. Bu durumda, bunlar kendi dosyaları yeniden yönlendirilen hello sürücüde zip ve bunları tootheir kaydedin yerel bilgisayar.

## <a name="how-administrators-can-export-data"></a>Yöneticiler verileri nasıl verebilirsiniz

Abonelik tooAzure Azure PowerShell kullanarak depolama içinde tüm koleksiyonlar için tüm kullanıcı profili diskleri (UPD) Azure RemoteApp verebilirsiniz için yönetir cmdlet, dışa aktarma AzureRemoteAppUserDisk.  Hiçbir özelliği tooselect tek tek UPD's yoktur.  Merhaba PowerShell komut çalıştırıldığında, her kullanıcı disk sabit disk boyutu 50 gb olması ve dışarı aktarılan tooAzure depolama.  Azure depolama maliyetinden hemen bu depolama için uygulanabilir.  Bu komutu çalıştırmak olun Aksi takdirde hello dışarı aktarma başarısız olur hiçbir oturum vardır.

UPD bilgisayarın etki alanına katılmış Azure RemoteApp dağıtımları için bir RDS dağıtımda yalnızca bir yeniden kullanılabilir, etki alanı olmayan birleştirilmiş dağıtımları kullanılamaz.  Bu diskleri bir RDS dağıtımında kullanılacaksa toouse öneririz bizim [betikleri otomatik](https://github.com/arcadiahlyy/aramigration) , aktarın, dönüştürme ve hello UPD'ın bir RDS dağıtımı ile aktarın.

