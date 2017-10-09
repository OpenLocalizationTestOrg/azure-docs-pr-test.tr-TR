---
title: "azure'da Windows sanal makine sorunlarını dağıtma aaaTroubleshoot | Microsoft Docs"
description: "Azurethe Resource Manager dağıtım modelinde dağıtma Windows sanal makine sorunlarını giderin."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a>Azure'da dağıtma Windows sanal makine sorunlarını giderme

tootroubleshoot sanal makine (VM) dağıtım sorunları, azure'da hello gözden [üst sorunları](#top-issues) yaygın hatalar ve çözümleri için.

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.

## <a name="top-issues"></a>Üst sorunları
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>Merhaba küme destekleyemez hello istenen VM boyutu
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.
- Merhaba, hello VM değiştirilemez istenen boyut:
    - Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun. Tıklatın **kaynak grupları** > kaynak grubunuz > **kaynakları** > kullanılabilirlik kümesi > **sanal makineleri** > sanal makineniz > **durdurmak**.
    - Tüm VM'ler Dur Merhaba, istenen hello boyutunda hello VM oluşturun.
    - Başlangıç yeni VM ilk hello ve ardından hello teker VM'ler durduruldu ve Başlat'ı tıklatın.


## <a name="hello-cluster-does-not-have-free-resources"></a>Merhaba küme kaynakları serbest bırakmak yok
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Merhaba isteği daha sonra yeniden deneyin.
- Merhaba yeni VM yapabiliyorsanız, farklı bir kullanılabilirlik parçası ayarlanması
    - Farklı bir kullanılabilirlik kümesinde bir VM oluşturun (Merhaba içinde aynı bölge).
    - Merhaba yeni VM toohello eklemek aynı sanal ağ.

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a>Nasıl kullanın ve windows istemci görüntüsünü Azure'a dağıtabilirsiniz?

Uygun bir Visual Studio (önceki adıyla MSDN) aboneliğiniz varsa, Windows 7, Windows 8 veya Windows 10 Azure üzerinde geliştirme ve test senaryoları için kullanabilirsiniz. Bu [makale](client-images.md) anahatları hello Azure galeri görüntüleri Windows İstemcisi Azure ve hello kullanımlarını çalıştırmak için uygunluk gereksinimler.

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a>Merhaba karma kullanımı Avantajı (HUB) kullanarak bir sanal makine nasıl dağıtabilir miyim?

Birkaç farklı şekilde toodeploy Windows sanal makinelerin hello Azure karma kullanımı avantajı vardır.

Bir Kurumsal Anlaşma abonelik için:

• Azure karma kullanımı avantajı ile önceden yapılandırılmış belirli Market görüntülerden sanal makineleri dağıtma.

Kurumsal Anlaşma için:

• Özel bir VM karşıya yükleyin ve bir Resource Manager şablonu veya Azure PowerShell kullanarak dağıtın.

Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

 - [Azure karma kullanımı avantajı genel bakış](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [İndirilebilir SSS](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - [Windows Server ve Windows İstemcisi için Azure karma kullanımı avantajı](hybrid-use-benefit-licensing.md).

 - [Azure'da hello karma kullanma avantajını nasıl kullanabilirim](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Visual studio Enterprise (BizSpark) için aylık my kredi nasıl etkinleştirilsin mi

tooactivate, aylık kredi, bu bkz [makale](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a>Nasıl tooadd Enterprise geliştirme ve Test toomy Kurumsal Anlaşma (Kurumsal Sözleşme) tooget tooWindow istemci görüntüleri erişim?

Enterprise geliştirme ve Test Hello üzerinde temel hello özelliği toocreate abonelikler sunma olduğu toodo izin verilen sınırlı tooAccount sahiplerine tarafından kuruluş yöneticisi bunu. Merhaba hesap sahibi hello Azure hesap Portalı aracılığıyla abonelikleri oluşturur ve ardından etkin Visual Studio abonelerinden ortak yönetici olarak eklemeniz gerekir. Yönetme ve geliştirme ve test için gerekli olan hello kaynaklarını kullanmak böylece. Daha fazla bilgi için bkz: [Enterprise geliştirme ve Test](https://azure.microsoft.com/offers/ms-azr-0148p/).

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a>My sürücüleri için Windows N-serisi VM'ime eksik

Windows tabanlı VM'ler için sürücülerin bulunduğu [burada](n-series-driver-setup.md).

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>GPU örneği N-serisi VM'im içinde bulunamıyor

tootake yeteneklerinden hello GPU Windows Server 2016 çalıştıran Azure N-serisi VM'lerin veya Windows Server 2012 R2, dağıtımdan sonra her VM NVIDIA grafik sürücüleri yüklemeniz gerekir. Sürücü Kurulum bilgileri yüklenebilir [Windows Vm'lerini](n-series-driver-setup.md) ve [Linux VM'ler](../linux/n-series-driver-setup.md).

## <a name="are-client-images-supported-for-n-series"></a>İstemci görüntüleri N-seri için destekleniyor mu?

Şu anda Azure yalnızca Windows Server ve Linux işletim sistemlerini çalıştıran sanal makinelerin N-serisi destekler.

## <a name="is-n-series-vms-available-in-my-region"></a>N-serisi VM'ler bulunduğum bölgede var mı?

Merhaba hello kullanılabilirlik denetleyebilirsiniz [bölge tablosu tarafından kullanılabilen ürünler](https://azure.microsoft.com/regions/services)ve fiyatlandırma [burada](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a>Hangi istemci görüntüleri ı kullanabilir ve Azure'da dağıtmak ve tooI nereden bunları?

Windows 10 azure'da geliştirme ve test senaryoları için uygun bir Visual Studio (önceki adıyla MSDN) aboneliğiniz olması koşuluyla veya Windows 7, Windows 8 kullanabilirsiniz. 

- Windows 10 görüntüleri kullanılabilir içinde hello Azure galerisinden [uygun geliştirme ve test sunar](client-images.md#eligible-offers). 
- Visual Studio abonelerinden teklif herhangi bir türde içinde için de [yeterli hazırlayın ve oluşturun](prepare-for-upload-vhd-image.md) bir 64-bit Windows 7, Windows 8 veya Windows 10 görüntüsü ve ardından [tooAzure karşıya](upload-generalized-managed.md). Hello kullan sınırlı toodev ve test etkin Visual Studio aboneler tarafından kalır.

Bu [makale](client-images.md) anahatları hello Azure galeri görüntüleri Windows İstemcisi Azure ve hello kullanımını çalıştırmak için uygunluk gereksinimler.

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>VM'im yeniden boyutlandırılırken istediğiniz mümkün toosee VM boyutu ailesi değil ben.

Bir VM çalışırken, dağıtılan tooa fiziksel sunucusu var. Merhaba fiziksel sunucuları Azure bölgelerindeki ortak fiziksel donanım kümelerde gruplandırılır. Merhaba VM taşınmış toobe toodifferent donanım kümeleri gerektiren bir VM'yi yeniden boyutlandırılırken kullanılan toodeploy hello VM was bağlı olarak hangi dağıtım modeli farklıdır.

- Klasik dağıtım modeli hello bulut hizmeti dağıtımı dağıtılan VM'ler kaldırılmalıdır ve toochange hello VM'ler tooa boyutu başka bir boyutu ailesindeki imzalanmasını.

- Resource Manager dağıtım modelinde dağıtılan VM'ler hello kullanılabilirlik hello hello kullanılabilirlik kümesindeki herhangi bir VM boyutunu değiştirmeden önce kümesindeki tüm VM'ler durdurmanız gerekir.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Merhaba listelenen VM boyutu kullanılabilirlik kümesinde dağıtırken desteklenmiyor.

Merhaba kullanılabilirlik kümesinin kümede desteklenen bir boyutu seçin. Kullanılabilirlik kümesi, ilk dağıtım toohello olması gerekir ve sahip düşündüğünüz toochoose hello en büyük VM boyutu kullanılabilirlik kümesi oluştururken önerilir.

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Varolan Klasik VM tooan kullanılabilirlik kümesini ekleyebilir miyim?

Evet. Bir varolan Klasik VM tooa yeni ekleyebilir veya var olan kullanılabilirlik kümesi. Daha fazla bilgi için bkz: [ekleme varolan bir sanal makine tooan kullanılabilirlik kümesini](classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).

Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.
