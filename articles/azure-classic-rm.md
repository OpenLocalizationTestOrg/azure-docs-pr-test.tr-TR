---
title: "Resource Manager ve Service Management (Klasik) dağıtım modları | Microsoft Docs"
description: "Resource Manager ve klasik dağıtım modelleri arasındaki farklar hakkında bilgi edinin."
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
ms.openlocfilehash: 0f451efa239dd36d82229f01cc385d6df46654f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-deployment-models"></a>Azure Dağıtım Modelleri
Azure platformu geçiş durumunda.  Azure için yeni ya da yıldır kullanmakta olduğunuz olsun, platforma sırasında bu geçiş yapıyorsanız önemli değişikliklerden bazıları anlamak önemlidir.

Tüm Azure kaynaklarına birini veya her ikisini aşağıdaki dağıtım modellerini destekler:

* **Kaynak Yöneticisi:** Azure kaynakları için yeni dağıtım modeli budur. Çoğu yeni kaynakları zaten bu dağıtım modeli desteklemek ve sonunda tüm kaynakları olur.   
* **Klasik:** bu modeli bugün çoğu mevcut Azure kaynaklar tarafından desteklenir. Bu model için Azure eklenen yeni kaynaklar desteklemez.

Hangi hizmet bu modeller her Azure kaynak Ayrıntılar için belgelere ile oluşturulabilir.

## <a name="why-does-this-matter"></a>Bu neden önemli?
Aşağıdaki nedenlerle önemlidir:

* Kullandığınız Azure platformu özellikleri bu iki modeli üzerinden farklıdır.  Örneğin, Resource Manager kullanılarak oluşturulan kaynakları ile dağıtım modelini (veya yalnızca Resource Manager) oluşturulabilir [Azure Resource Manager şablonları](azure-resource-manager/resource-group-overview.md#template-deployment), Klasik dağıtım modeliyle oluşturulan kaynakları edilemez ise.
* Tek başına bir Azure kaynak özellikleri davranışları iki modeli üzerinden farklı veya yalnızca bir model veya diğer mevcut.  Örneğin, Yük Dengeleme trafiğini Klasik dağıtım modeliyle oluşturulan sanal makineler arasında olduğu *örtük* çünkü sanal makineleri bir Azure bulut hizmeti bir üyesidir ve yük otomatik olarak dengeli üzerinden sanal bir bulut hizmeti makinelerde. Resource Manager kullanılarak oluşturulan sanal makineler bir bulut hizmeti üyeleri değildir ve ayrı bir Azure yük dengeleyici kaynak olmalıdır *açıkça* birden fazla sanal makine arasında trafiği dengelemek yüklemek için oluşturulmuş.  
* Bu iki modelleri arasında nasıl oluşturma, yapılandırma ve Azure kaynaklarınızı yönetmek farklıdır.
* Bir dağıtım modeli kullanılarak oluşturulmuş kaynakları mutlaka farklı dağıtım modeli kullanılarak oluşturulmuş kaynaklarla işleyemez. Örneğin, bir dağıtım modeli kullanılarak oluşturulan Azure sanal makineleri yalnızca Azure sanal aynı dağıtım modeli kullanılarak oluşturulmuş ağlara bağlanabilir.    

Her dağıtım modellerinin arka plandaki her kaynak için bir uygulama programlama arabirimi (API) var.  Var olan bir [Resource Manager API](https://msdn.microsoft.com/library/azure/dn948464.aspx) Resource Manager dağıtım modeli için ve bir [Hizmet Yönetimi API'si](https://msdn.microsoft.com/library/azure/ee460799.aspx) Klasik dağıtım modeli için. Geliştiricilerin bu API'leri ile etkileşim kurmak için kod yazma *doğrudan*.  

BT uzmanları ancak, bu API'leri ile genellikle etkileşim *dolaylı olarak* bir web tarayıcısında grafik portalını kullanarak bir Windows bilgisayarda Azure PowerShell cmdlet'lerini kullanarak veya ya da Windows Azure komut satırı arabirimi (CLI) kullanarak , OS X ya da Linux bilgisayarı. BT uzmanı tarafından kullanılan bu dolaylı yöntemleri üçünü API'leri ile doğrudan etkileşim. Bu yeni işlevselliği Azure platformu ve kaynakların eklendiğinde, her zaman ilk olarak, API sağlandıktan sonra yeni kaynaklar ve özellikler için destek sağlamasını dolaylı yöntemleriyle API aracılığıyla doğrudan kullanılabilir olduğu anlamına gelir.  

Aşağıdaki bölümler nasıl Azure kaynaklarını açıklamak için üç dolaylı yöntem farklı dağıtım modeli kullanılarak yapılandırılır.

## <a name="portals"></a>Portallar
Azure iki portala sahiptir:

* **[Azure portal](https://manage.windowsazure.com):** , Azure biraz kullanıyorsanız, bu portalı kullanmış olduğunuz. Oluşturup Klasik dağıtım modelini destekleyen eski Azure kaynaklarını yapılandırmak için kullanılır. Oluşturma veya yalnızca Kaynak Yöneticisi'ni destekleyecek kaynaklarını yapılandırmak için kullanamazsınız. 
* **[Azure Önizleme portalını](https://azure.microsoft.com/overview/preview-portal/):** daha yeni bir Azure kaynak kullanıyorsanız büyük olasılıkla bu portalı kullandığınız. Oluşturmak ve bazı Azure kaynaklarını yapılandırmak için kullanılabilir. Sonunda oluşturabilir ve tüm Azure kaynakları ile yapılandırmanız. Her iki dağıtım modeli desteği bazı kaynaklar için bu portalı oluşturmak ve her iki dağıtım modeli kullanarak bir kaynak yapılandırmak için kullanılabilir. 

Bazı kaynaklar ve özellikleri yalnızca oluşturulabilir ve bir portal veya diğer yapılandırılmış. Bazı kaynaklar veya özellikler (henüz) olamaz oluşturulan veya ya da Portalı'nda yapılandırılmış ve yalnızca PowerShell, CLI veya her ikisi de yapılandırılabilir. Her Azure kaynak belgelerine ile oluşturulabilir hangi yöntemi ayrıntıları. 

## <a name="powershell"></a>PowerShell
İle [PowerShell](/powershell/azureps-cmdlets-docs) bir komut satırı veya yazar oluşturmak ve bir Windows bilgisayardan Azure kaynaklarını yapılandırmak için komut dosyalarını kullanabilirsiniz.  Tek tek Azure kaynaklarınız [Resource Manager cmdlet'lerini](/powershell/azure/overview), [Hizmet Yönetimi cmdlet'leri](/powershell/azure/overview?view=azuresmps-3.7.0), veya her ikisini de.  Bazı kaynaklar ve özellikleri yalnızca oluşturulabilir ve/veya PowerShell veya CLI kullanarak yapılandırılır. Resource Manager PowerShell cmdlet'lerini kullanırken kaynakta bağlı olarak oluşturma ve Azure kaynaklarını yapılandırma için iki seçeneğiniz olabilir:

* **PowerShell cmdlet'leri yalnızca:** oluşturabilir ve her kaynak için cmdlet öğelerini kullanarak tek tek her Azure kaynak yapılandırabilirsiniz. Bu, bir komut satırından veya bir depolayabileceğiniz PowerShell Betiği ve sürümü birden çok komut ekleyerek yapabilirsiniz.
* **PowerShell cmdlet'leri Azure Resource Manager şablonu ile:** bir Azure Resource Manager şablonu kullanarak Azure kaynaklarına oluşturmak için PowerShell'i kullanabilirsiniz. Şablonları kaydedilmiş ve sürümü tutulan olabilir. Okuyarak daha fazla bilgi edinin [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md) makalesi. Birkaç [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) indirdiğiniz ve değiştirdiğiniz çok yaygın çözümleri mevcut.

## <a name="cli"></a>CLI
Oluşturun ve CLI kullanarak Windows, OS X veya Linux bilgisayarlardan Azure kaynaklarını yapılandırın.  Okuma [Azure CLI yükleme](cli-install-nodejs.md) makale CLI tercih, işletim sistemine yükleyin. PowerShell gibi kullanarak kaynakları olup oluşturmakta olduğunuz bağlı olarak kullanılması gereken farklı komutlar vardır [Resource Manager](xplat-cli-azure-resource-manager.md) veya [Klasik (Hizmet Yönetimi)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) dağıtım modeli.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Anlamak için nasıl [tasarım şablonları](best-practices-resource-manager-design-templates.md).

