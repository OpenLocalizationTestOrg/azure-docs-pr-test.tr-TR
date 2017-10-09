---
title: "Linux VM'ler için Azure'da sorular aaaFrequently | Microsoft Docs"
description: "Merhaba hello Resource Manager modeli ile oluşturulan Linux sanal makineleri hakkında sık sorulan sorular, yanıtlar toosome sağlar."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Linux sanal makineleri hakkında sık sorulan sorular
Bu makalede, Azure'da hello Resource Manager dağıtım modeli kullanarak oluşturulan Linux sanal makineleri hakkında bazı sık sorulan soruları giderir. Merhaba Windows sürümü bu konu için bkz: [Windows sanal makineler hakkında sık sorulan bir soru](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Azure sanal makinesinde ne çalıştırabilirim?
Tüm aboneler bir Azure sanal makinesinde sunucu yazılımı çalıştırabilir. Daha fazla bilgi için bkz: [Azure-Endorsed dağıtımları Linux'ta](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Bir sanal makineyle birlikte ne kadar depolama alanı kullanabilirim?
Her veri diski too1 TB olabilir. Merhaba kullanabileceğiniz veri diski sayısı hello hello sanal makine boyutuna bağlıdır. Ayrıntılar için bkz. [Virtual Machines boyutları](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bir Azure depolama hesabı hello işletim sistemi diski ve veri diskleri için depolama sağlar. Her disk bir sayfa blobu olarak depolanan bir .vhd dosyasıdır. Fiyatlandırma ayrıntıları için bkz. [Depolama Fiyatlandırma Ayrıntıları](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Sanal Makinem nasıl erişebilir mi?
Uzak bağlantı toolog güvenli Kabuk (SSH) kullanarak toohello sanal makinedeki kurun. Merhaba yönergeleri hakkında bkz tooconnect [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [Linux ve Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Varsayılan olarak, SSH en fazla 10 eş zamanlı bağlantıya izin verir. Merhaba yapılandırma dosyasını düzenleyerek bu sayıyı artırabilirsiniz.

Sorun yaşıyorsanız, kullanıma [sorun giderme güvenli Kabuk (SSH) bağlantı](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>Merhaba geçici disk (/ dev/sdb1) toostore verileri kullanabilir miyim?
Merhaba geçici disk (/ dev/sdb1) toostore veri kullanmayın. Yalnızca geçici depolama için yoktur. Kurtarılamaz veri kaybı riski oluşur.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>I kopyalayabilir veya mevcut bir Azure VM'yi kopyalama?
Evet. Yönergeler için bkz: [nasıl toocreate bir bir Linux sanal makine kopyasını hello Resource Manager dağıtım modeli](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Neden Kanada merkezi ve Doğu Kanada bölgeler arasında Azure Resource Manager görüyorum değil mi?
Merhaba iki yeni bölgeler Kanada merkezi ve Doğu Kanada otomatik olarak mevcut Azure abonelikleri için sanal makine oluşturmak için kayıtlı değil. Bu kayıt aracılığıyla bir sanal makine dağıtıldığında otomatik olarak yapılır Azure portal tooany Azure Kaynak Yöneticisi'ni kullanarak diğer bölge hello. Bir sanal makine sonra diğer Azure bölgesi dağıtılan tooany olan hello yeni bölgeler sonraki sanal makineler için kullanılabilir.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>NIC toomy VM, oluşturulduktan sonra ekleyebilir miyim?
Evet, bu artık mümkündür. Merhaba VM ilk gereksinimlerini toobe deallocated durduruldu. Bir NIC ekleyip sonra (olduğu sürece son NIC hello VM üzerinde hello). 

## <a name="are-there-any-computer-name-requirements"></a>Herhangi bir bilgisayar adı gereksinimleri var mı?
Evet. Merhaba bilgisayar adı en fazla 64 karakter uzunluğunda olabilir. Bkz: [adlandırma kuralları kuralları ve sınırlamaları](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kaynaklarınızı adlandırma geçici daha fazla bilgi için.

## <a name="are-there-any-resource-group-name-requirements"></a>Herhangi bir kaynak grubu adı gereksinimleri var mı?
Evet. Merhaba kaynak grubu adı en fazla 90 karakter uzunluğunda olabilir. Bkz: [adlandırma kuralları kuralları ve sınırlamaları](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kaynak grupları hakkında daha fazla bilgi için.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Bir VM oluşturulurken hello kullanıcıadı gereksinimleri nelerdir?
Kullanıcı adları, 1-64 karakter uzunluğunda olmalıdır.

kullanıcı adlarını aşağıdaki hello izin verilmiyor:

<table>
    <tr>
        <td style="text-align:center">Yönetici </td><td style="text-align:center"> Yönetici </td><td style="text-align:center"> Kullanıcı </td><td style="text-align:center"> Kullanıcı1</td>
    </tr>
    <tr>
        <td style="text-align:center">test etme </td><td style="text-align:center"> Kullanıcı2 </td><td style="text-align:center"> Test1 </td><td style="text-align:center"> KULLANICI3</td>
    </tr>
    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> bir</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> ASPNET</td>
    </tr>
    <tr>
        <td style="text-align:center">yedekleme </td><td style="text-align:center"> Konsol </td><td style="text-align:center"> David </td><td style="text-align:center"> Konuk</td>
    </tr>
    <tr>
        <td style="text-align:center">John </td><td style="text-align:center"> Sahibi </td><td style="text-align:center"> kök </td><td style="text-align:center"> sunucu</td>
    </tr>
    <tr>
        <td style="text-align:center">SQL </td><td style="text-align:center"> Destek </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">Test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> Kullanıcı4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Bir VM oluşturulurken hello parola gereksinimleri nelerdir?
Parolalar 6 72 karakter uzunluğunda ve 3 4 karmaşıklık gereksinimlerini aşağıdaki hello dışında karşılaması gerekir:

* Alt karakterler
* Üst karakter
* Bir rakam olması
* (Regex eşleşen [\W_]) bir özel karakter sahip

parolaları aşağıdaki hello izin verilmiyor:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$ $word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Parola!</td>
        <td style="text-align:center">Parola1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">ILOVEYOU veya!</td>
    </tr>
</table>
