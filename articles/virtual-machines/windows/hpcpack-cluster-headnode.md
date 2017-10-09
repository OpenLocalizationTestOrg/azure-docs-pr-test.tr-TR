---
title: "bir Azure VM'de HPC paketi üstbilgi düğümü aaaCreate | Microsoft Docs"
description: "Nasıl toouse hello Azure portal ve hello Resource Manager dağıtım modeli toocreate bir Azure VM Microsoft HPC Pack 2012 R2 baş düğümünde öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Market görüntüsü olan bir Azure VM'de HPC paketi küme baş düğümüne Hello oluşturma
Kullanım bir [Microsoft HPC Pack 2012 R2 sanal makine görüntüsü](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Marketi ve hello Azure portal toocreate hello baş düğümünden bir HPC Kümesi. Bu HPC Pack VM görüntüsü, Windows Server 2012 R2 Datacenter HPC Pack 2012 R2 güncelleştirme 3'de önceden yüklenmiş olan dayanır. Azure HPC Pack dağıtımının kavram kanıtı için bu baş düğümü kullanın. İşlem düğümleri toohello küme toorun HPC iş yüklerini daha sonra ekleyebilirsiniz.

> [!TIP]
> azure'da hello baş düğüm ve işlem düğümlerini içeren tam bir HPC Pack 2012 R2 küme toodeploy, otomatik olarak yöntemi kullanmanızı öneririz. Seçenekleriniz hello [HPC Pack Iaas dağıtım betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) ve Resource Manager şablonları hello gibi [HPC paketi küme iş yükleri için](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Resource Manager şablonları için kullanılabilen de [Microsoft HPC Pack 2016 kümeleri](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Planlama konusunda dikkat edilmesi gerekenler
Hello aşağıdaki şekilde gösterildiği gibi bir Active Directory etki alanı içindeki bir Azure sanal ağı hello HPC paketi üstbilgi düğümü dağıtın.

![HPC paketi üstbilgi düğümü][headnode]

* **Active Directory etki alanı**: hello VM üzerinde hello HPC Hizmetleri başlamadan önce hello HPC Pack 2012 R2 baş düğüm olmalıdır Azure tooan Active Directory etki alanına katılmış. Bu makalede, kanıt kavramı dağıtım için gösterildiği gibi hello hello HPC Hizmetleri başlatmadan önce bir etki alanı denetleyicisi olarak oluşturduğunuz hello baş düğüm için VM yükseltebilirsiniz. Başka bir seçenek toodeploy ayrı etki alanı denetleyicisi ve size katılmasını Azure toowhich ormanda hello üstbilgi düğüm VM'ine.

* **Dağıtım modeli**: çoğu yeni dağıtımlar için Microsoft hello Resource Manager dağıtım modeli kullanmanızı önerir. Bu makale, bu dağıtım modeli kullanan varsaymaktadır.

* **Azure sanal ağı**: hello Resource Manager dağıtım modeli toodeploy hello baş düğüm kullandığınızda, belirtin veya bir Azure sanal ağı oluşturun. Toojoin hello baş düğüm tooan var olan Active Directory etki alanı gerekirse hello sanal ağ kullanın. Ayrıca, sonraki tooadd işlem düğümü VM'ler toohello küme gerekir.

## <a name="steps-toocreate-hello-head-node"></a>Adımları toocreate hello baş düğüm
Aşağıda hello Resource Manager dağıtım modeli kullanarak üst düzey adımları toouse hello Azure portal toocreate hello HPC paketi üstbilgi düğümü için bir Azure VM verilmiştir. 

1. Yeni bir Active Directory ormanı Azure sanal makineleri ayrı etki alanı denetleyicisiyle toocreate istiyorsanız, bir toouse seçenektir bir [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Kavram kanıtı dağıtımı, basit kanıt için olan bu adımı tooomit ince ve hello üstbilgi düğüm VM'ine kendisini bir etki alanı denetleyicisi olarak yapılandırın. Bu seçenek bu makalenin sonraki bölümlerinde açıklanmıştır.
2. Merhaba üzerinde [HPC Pack 2012 R2 Windows Server 2012 R2 sayfasında](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Market, tıklatın **sanal makine oluşturma**. 
3. Merhaba portalında, hello **HPC Pack 2012 R2'de Windows Server 2012 R2** sayfası, select hello **Resource Manager** dağıtım modeli ve ardından **oluşturma**.
   
    ![HPC Pack görüntü][marketplace]
4. Merhaba portal tooconfigure hello ayarları kullanmak ve hello VM oluşturun. Yeni tooAzure değilseniz, hello öğreticisini izleyin [hello Azure portalında bir Windows sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Kanıt kavram kanıtı dağıtımı için genellikle hello varsayılan kabul edebilir veya önerilen ayarlar.
   
   > [!NOTE]
   > Azure Active Directory etki alanına varolan toojoin hello baş düğüm tooan istiyorsanız, o etki alanı için sanal ağ hello hello VM oluşturulurken belirttiğinizden emin olun.
   > 
   > 
5. Merhaba VM oluşturun ve hello VM çalışıyorsa, sonra [toohello VM bağlanmak](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Uzak Masaüstü tarafından. 
6. Merhaba VM tooan Active Directory etki alanı ormanı seçenekleri aşağıdaki hello birini seçerek Katıl:
   
   * Var olan bir etki alanı ormanı ile bir Azure sanal ağında hello VM oluşturduysanız, standart sunucu yöneticisi veya Windows PowerShell araçlarını kullanarak hello VM toohello orman katılın. Yeniden başlatın.
   * Yeni bir sanal ağ (olmadan var olan bir etki alanı ormanı) hello VM oluşturduysanız hello VM bir etki alanı denetleyicisi olarak yükseltin. Standart adımları tooinstall kullanın ve hello Active Directory etki alanı Hizmetleri rolünü hello baş düğümünde yapılandırın. Ayrıntılı adımlar için bkz: [yeni bir Windows Server 2012 Active Directory ormanı yüklemek](https://technet.microsoft.com/library/jj574166.aspx).
7. VM çalışıyor ve birleştirilmiş tooan Active Directory ormanı hello sonra hello HPC Pack Hizmetleri aşağıda gösterildiği gibi başlatın:
   
    a. Toohello üstbilgi düğüm VM'ine hello yerel Yöneticiler grubunun bir üyesi olan bir etki alanı hesabı kullanarak bağlanın. Örneğin, hello baş düğüm VM oluşturduğunuz sırada ayarladığınız hello yönetici hesabı kullanın.
   
    b. Varsayılan bir baş düğüm yapılandırma için Windows PowerShell'i yönetici olarak başlatın ve hello aşağıdakileri yazın:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Merhaba HPC Pack Hizmetleri toostart için birkaç dakika sürebilir.
   
    Ek baş düğümü yapılandırma seçenekleri için yazın `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Sonraki adımlar
* Şimdi hello baş düğümüne HPC Pack kümenizi ile çalışabilirsiniz. Örneğin, başlangıç HPC Küme Yöneticisi'ni ve tam hello [dağıtım Yapılacaklar listesi](https://technet.microsoft.com/library/jj884141.aspx).
* Tooincrease hello küme bilgi işlem kapasitesi isteğe bağlı istiyorsanız ekleyin [Azure veri bloğu düğümleri](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) bir bulut hizmetinde. 
* Bir test iş yükü hello kümede çalıştırmayı deneyin. HPC Pack Merhaba bir örnek için bkz: [Başlangıç Kılavuzu](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
