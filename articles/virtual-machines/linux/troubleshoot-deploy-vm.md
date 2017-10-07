---
title: "azure'daki Linux sanal makine sorunlarını dağıtma aaaTroubleshoot | Microsoft Docs"
description: "Azurethe Resource Manager dağıtım modelinde dağıtma Linux sanal makine sorunlarını giderin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
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
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Azure'da dağıtma Linux sanal makine sorunlarını giderme

tootroubleshoot sanal makine (VM) dağıtım sorunları, azure'da hello gözden [üst sorunları](#top-issues) yaygın hatalar ve çözümleri için.

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.

## <a name="top-issues"></a>Üst sorunları
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

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

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Visual studio Enterprise (BizSpark) için aylık my kredi nasıl etkinleştirilsin mi

tooactivate, aylık kredi, bu bkz [makale](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Neden hello GPU sürücüsünün bir Ubuntu NV VM için yükleyebilir miyim değil mi?

Linux GPU desteği şu anda yalnızca Azure NC Ubuntu Server 16.04 LTS çalıştıran Vm'lerinde olarak kullanılabilir. Daha fazla bilgi için bkz: [GPU sürücüleri Linux çalıştıran N-serisi VM'ler için ayarlanmış](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>My sürücüleri için Linux N-serisi VM'ime eksik

Linux tabanlı VM'ler için sürücülerin bulunduğu [burada](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>GPU örneği N-serisi VM'im içinde bulunamıyor

tootake yeteneklerinden hello GPU Windows Server 2016 çalıştıran Azure N-serisi VM'lerin veya Windows Server 2012 R2, dağıtımdan sonra her VM NVIDIA grafik sürücüleri yüklemeniz gerekir. Sürücü Kurulum bilgileri yüklenebilir [Windows Vm'lerini](../windows/n-series-driver-setup.md) ve [Linux VM'ler](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>N-serisi VM'ler bulunduğum bölgede var mı?

Merhaba hello kullanılabilirlik denetleyebilirsiniz [bölge tablosu tarafından kullanılabilen ürünler](https://azure.microsoft.com/regions/services)ve fiyatlandırma [burada](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>VM'im yeniden boyutlandırılırken istediğiniz mümkün toosee VM boyutu ailesi değil ben.

Bir VM çalışırken, dağıtılan tooa fiziksel sunucusu var. Merhaba fiziksel sunucuları Azure bölgelerindeki ortak fiziksel donanım kümelerde gruplandırılır. Merhaba VM taşınmış toobe toodifferent donanım kümeleri gerektiren bir VM'yi yeniden boyutlandırılırken kullanılan toodeploy hello VM was bağlı olarak hangi dağıtım modeli farklıdır.

- Klasik dağıtım modeli hello bulut hizmeti dağıtımı dağıtılan VM'ler kaldırılmalıdır ve toochange hello VM'ler tooa boyutu başka bir boyutu ailesindeki imzalanmasını.

- Resource Manager dağıtım modelinde dağıtılan VM'ler hello kullanılabilirlik hello hello kullanılabilirlik kümesindeki herhangi bir VM boyutunu değiştirmeden önce kümesindeki tüm VM'ler durdurmanız gerekir.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Merhaba listelenen VM boyutu kullanılabilirlik kümesinde dağıtırken desteklenmiyor.

Merhaba kullanılabilirlik kümesinin kümede desteklenen bir boyutu seçin. Kullanılabilirlik kümesi, ilk dağıtım toohello olması gerekir ve sahip düşündüğünüz toochoose hello en büyük VM boyutu kullanılabilirlik kümesi oluştururken önerilir.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Hangi Linux dağıtımları/sürümleri, Azure üzerinde desteklenir?

Linux hello listesini bulabilirsiniz [Azure-Endorsed dağıtımları](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Varolan Klasik VM tooan kullanılabilirlik kümesini ekleyebilir miyim?

Evet. Bir varolan Klasik VM tooa yeni ekleyebilir veya var olan kullanılabilirlik kümesi. Daha fazla bilgi için bkz: [ekleme varolan bir sanal makine tooan kullanılabilirlik kümesini](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).

Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.
