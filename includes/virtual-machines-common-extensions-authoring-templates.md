## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="64f0e-101">Azure Resource Manager şablonlarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="64f0e-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="64f0e-102">Azure Resource Manager şablonları izin toodeclaratively belirtin hello Azure Iaas altyapı Json dilde kaynakları arasındaki bağımlılıkların hello tanımlayarak.</span><span class="sxs-lookup"><span data-stu-id="64f0e-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="64f0e-103">Azure Resource Manager şablonları ayrıntılı bir genel bakış için lütfen aşağıdaki toohello makalesine başvurun:</span><span class="sxs-lookup"><span data-stu-id="64f0e-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="64f0e-104">Kaynak grubu genel bakış</span><span class="sxs-lookup"><span data-stu-id="64f0e-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="64f0e-105">Örnek şablon parçacığı VM uzantıları için</span><span class="sxs-lookup"><span data-stu-id="64f0e-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="64f0e-106">Bir Azure Resource Manager şablonu parçası gerektirdiği VM uzantıları toodeclaratively belirtin hello uzantı yapılandırması hello şablonunda.</span><span class="sxs-lookup"><span data-stu-id="64f0e-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="64f0e-107">Merhaba uzantı yapılandırması belirtmek için hello biçimi şöyledir.</span><span class="sxs-lookup"><span data-stu-id="64f0e-107">Here is hello format for specifying hello extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="64f0e-108">Hello yukarıdaki görebileceğiniz gibi hello uzantısı şablon iki ana bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="64f0e-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="64f0e-109">Uzantı adı, yayımcı ve sürüm</span><span class="sxs-lookup"><span data-stu-id="64f0e-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="64f0e-110">Uzantı yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="64f0e-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="64f0e-111">Merhaba yayımcı, türü ve uzantıyı typeHandlerVersion tanımlama</span><span class="sxs-lookup"><span data-stu-id="64f0e-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="64f0e-112">Azure VM uzantıları Microsoft tarafından yayınlanan ve güvenilir 3 taraf Yayımcılar ve her bir uzantı, yayımcı, türü ve hello typeHandlerVersion tarafından tanımlanan benzersiz olarak.</span><span class="sxs-lookup"><span data-stu-id="64f0e-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="64f0e-113">Bunlar aşağıdaki gibi belirlenebilir:</span><span class="sxs-lookup"><span data-stu-id="64f0e-113">These can be determined as following:</span></span>  

