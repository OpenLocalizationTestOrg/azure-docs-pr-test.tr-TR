## <a name="overview-of-azure-resource-manager-templates"></a>Azure Resource Manager şablonlarına genel bakış
Azure Resource Manager şablonları izin toodeclaratively belirtin hello Azure Iaas altyapı Json dilde kaynakları arasındaki bağımlılıkların hello tanımlayarak. Azure Resource Manager şablonları ayrıntılı bir genel bakış için lütfen aşağıdaki toohello makalesine başvurun:

[Kaynak grubu genel bakış](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Örnek şablon parçacığı VM uzantıları için
Bir Azure Resource Manager şablonu parçası gerektirdiği VM uzantıları toodeclaratively belirtin hello uzantı yapılandırması hello şablonunda.
Merhaba uzantı yapılandırması belirtmek için hello biçimi şöyledir.

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

Hello yukarıdaki görebileceğiniz gibi hello uzantısı şablon iki ana bölümleri içerir:

1. Uzantı adı, yayımcı ve sürüm
2. Uzantı yapılandırması.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Merhaba yayımcı, türü ve uzantıyı typeHandlerVersion tanımlama
Azure VM uzantıları Microsoft tarafından yayınlanan ve güvenilir 3 taraf Yayımcılar ve her bir uzantı, yayımcı, türü ve hello typeHandlerVersion tarafından tanımlanan benzersiz olarak. Bunlar aşağıdaki gibi belirlenebilir:  

