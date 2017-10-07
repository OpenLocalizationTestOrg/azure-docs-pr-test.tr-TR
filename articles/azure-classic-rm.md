---
title: "aaaResource Yöneticisi ve Hizmet Yönetimi (Klasik) dağıtım modları | Microsoft Docs"
description: "Resource Manager ve klasik dağıtım modelleri arasında Hello farklar hakkında bilgi edinin."
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Azure Dağıtım Modelleri
Hello Azure platformu geçiş durumunda.  Yeni tooAzure olduğunuz veya yıl için kullanmakta olduğunuz, onu önemli toounderstand olup hello önemli değişikliklerden bazıları biz toohello platform bu geçiş sırasında değişiklik yapıyorsunuz.

Tüm Azure kaynaklarına birini veya her ikisini dağıtım modellerini aşağıdaki hello destekler:

* **Kaynak Yöneticisi:** hello Azure kaynakları için yeni dağıtım modeli budur. Çoğu yeni kaynakları zaten bu dağıtım modeli desteklemek ve sonunda tüm kaynakları olur.   
* **Klasik:** bu modeli bugün çoğu mevcut Azure kaynaklar tarafından desteklenir. Yeni kaynaklar tooAzure bu modeli desteklemeyecektir eklendi.

hangi hizmet bu modeller her Azure kaynak Ayrıntılar için Hello belgelerine ile oluşturulabilir.

## <a name="why-does-this-matter"></a>Bu neden önemli?
Aşağıdaki nedenlerden hello için önemlidir:

* kullandığınız hello Azure platformu özellikleri bu iki modeli üzerinden farklıdır.  Örneğin, hello Resource Manager dağıtım modeli (veya yalnızca Resource Manager) kullanılarak oluşturulmuş kaynaklar ile oluşturulabilir [Azure Resource Manager şablonları](azure-resource-manager/resource-group-overview.md#template-deployment), hello Klasik dağıtım modeliyle oluşturulan kaynakları edilemez ise.
* tek başına bir Azure kaynak özellikleri hello veya davranışları hello iki modeli üzerinden farklı veya yalnızca bir model veya hello diğer mevcut.  Örneğin, Yük Dengeleme trafiğini hello Klasik dağıtım modeliyle oluşturulan sanal makineler arasında olduğu *örtük* çünkü sanal makineleri bir Azure bulut hizmeti bir üyesidir ve yük otomatik olarak dengeli üzerinden sanal bir bulut hizmeti makinelerde. Resource Manager kullanılarak oluşturulan sanal makineler bir bulut hizmeti üyeleri değildir ve ayrı bir Azure yük dengeleyici kaynak olmalıdır *açıkça* birden fazla sanal makine arasında tooload trafiği dengelemek oluşturuldu.  
* Bu iki modelleri arasında nasıl oluşturma, yapılandırma ve Azure kaynaklarınızı yönetmek farklıdır.
* Bir dağıtım modeli kullanılarak oluşturulmuş kaynakları mutlaka farklı dağıtım modeli kullanılarak oluşturulmuş kaynaklarla işleyemez. Örneğin, bir dağıtım modeli kullanılarak oluşturulan Azure sanal makineleri bağlı tooAzure sanal hello kullanılarak oluşturulan ağlar yalnızca olabilir aynı dağıtım modelinde.    

Her hello dağıtım modellerinin arka plandaki her kaynak için bir uygulama programlama arabirimi (API) var.  Var olan bir [Resource Manager API](https://msdn.microsoft.com/library/azure/dn948464.aspx) hello Resource Manager dağıtım modeli için ve bir [Hizmet Yönetimi API'si](https://msdn.microsoft.com/library/azure/ee460799.aspx) hello Klasik dağıtım modeli için. Geliştiricilerin bu API'leri ile kod toointeract yazma *doğrudan*.  

BT uzmanları ancak, bu API'leri ile genellikle etkileşim *dolaylı olarak* bir web tarayıcısında grafik portalı kullanarak Azure PowerShell kullanarak bir Windows bilgisayarda veya kullanarak cmdlet'leri Azure komut satırı arabirimi (CLI) üzerinde ya da hello bir Windows, OS X veya Linux bilgisayarı. Bu dolaylı yöntemlerin hello BT uzmanı tarafından kullanılan tüm üç hello ile doğrudan API'lerini etkileşim. Yeni işlevsellik sunulan toohello Azure olduğunda bunun anlamı platform veya kaynakları, her zaman ilk olarak, yeni kaynaklar hello desteği sağlamasını hello dolaylı yöntemleriyle hello API doğrudan kullanılabilir ve hello API sağlandıktan sonra özellikleri.  

Aşağıdaki bölümler Hello açıklayan nasıl Azure kaynaklarını hello üç dolaylı yöntemlerle hello farklı dağıtım modeli kullanılarak yapılandırılır.

## <a name="portals"></a>Portallar
Azure iki portala sahiptir:

* **[Azure portal](https://manage.windowsazure.com):** , Azure biraz kullanıyorsanız, bu portalı kullanmış olduğunuz. Bu kullanılan toocreate ve hello Klasik dağıtım modelini destekleyen eski Azure kaynaklarını yapılandırın. Toocreate kullanın veya yalnızca Kaynak Yöneticisi'ni destekleyecek kaynaklarını yapılandırın. 
* **[Azure Önizleme portalını](https://azure.microsoft.com/overview/preview-portal/):** daha yeni bir Azure kaynak kullanıyorsanız büyük olasılıkla bu portalı kullandığınız. Bazı Azure kaynaklarını yapılandırmak ve kullanılan toocreate olması. Sonunda mümkün toocreate olması ve tüm Azure kaynakları ile yapılandırmanız. Her iki dağıtım modeli desteklemek için bazı kaynaklar, bu portalı kullanılan toocreate olabilir ve her iki dağıtım modeli kullanarak bir kaynak yapılandırın. 

Bazı kaynaklar ve özellikleri yalnızca oluşturulabilir ve bir portal veya hello diğer yapılandırılmış. Bazı kaynaklar veya özellikler (henüz) oluşturulamıyor veya ya da portalında yapılandırılır ve yalnızca PowerShell ile yapılandırılabilir, CLI ya da her ikisini de hello. Her Azure kaynak Hello belgelerine ile oluşturulabilir hangi yöntemi ayrıntıları. 

## <a name="powershell"></a>PowerShell
İle [PowerShell](/powershell/azureps-cmdlets-docs) bir komut satırı veya yazar betikleri toocreate kullanın ve bir Windows bilgisayardan Azure kaynaklarını yapılandırın.  Tek tek Azure kaynaklarınız [Resource Manager cmdlet'lerini](/powershell/azure/overview), [Hizmet Yönetimi cmdlet'leri](/powershell/azure/overview?view=azuresmps-3.7.0), veya her ikisini de.  Bazı kaynaklar ve özellikleri yalnızca oluşturulabilir ve/veya PowerShell veya CLI hello kullanılarak yapılandırılmış. Resource Manager PowerShell cmdlet'lerini kullanırken Hello kaynakta bağlı olarak oluşturma ve Azure kaynaklarını yapılandırma için iki seçeneğiniz olabilir:

* **PowerShell cmdlet'leri yalnızca:** oluşturabilir ve her kaynak için hello cmdlet'lerini kullanarak tek tek her Azure kaynak yapılandırabilirsiniz. Bu, bir komut satırından veya bir depolayabileceğiniz PowerShell Betiği ve sürümü birden çok komut ekleyerek yapabilirsiniz.
* **PowerShell cmdlet'leri Azure Resource Manager şablonu ile:** PowerShell toocreate Azure kullanabileceğiniz bir Azure Resource Manager şablonu kullanarak kaynak. Şablonları kaydedilmiş ve sürümü tutulan olabilir. Merhaba okuyarak daha fazla bilgi edinin [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md) makalesi. Birkaç [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) indirdiğiniz ve değiştirdiğiniz çok yaygın çözümleri mevcut.

## <a name="cli"></a>CLI
Oluşturun ve hello CLI kullanarak Windows, OS X veya Linux bilgisayarlardan Azure kaynaklarını yapılandırın.  Okuma hello [yükleme hello Azure CLI](cli-install-nodejs.md) seçtiğiniz işletim sistemine makale tooinstall hello CLI. PowerShell gibi kullanarak kaynakları olup oluşturmakta olduğunuz bağlı olarak kullanılması gereken farklı komutlar vardır [Resource Manager](xplat-cli-azure-resource-manager.md) veya hello [Klasik (Hizmet Yönetimi)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) dağıtım modeli.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Nasıl çok anlamak[tasarım şablonları](best-practices-resource-manager-design-templates.md).

