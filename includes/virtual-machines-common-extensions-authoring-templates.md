## <a name="overview-of-azure-resource-manager-templates"></a>Azure Resource Manager şablonlarına genel bakış
Azure Resource Manager şablonları bildirimli olarak Azure Iaas altyapı Json dilde kaynakları arasındaki bağımlılıkların tanımlayarak belirtmenizi sağlar. Azure Resource Manager şablonları ayrıntılı bir genel bakış için lütfen aşağıdaki makaleye bakın:

[Kaynak grubu genel bakış](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Örnek şablon parçacığı VM uzantıları için
Bir Azure Kaynak Yöneticisi'nin bir parçası olarak VM uzantıları şablonu şablonda uzantı yapılandırması bildirimli olarak belirtmenizi gerektirir.
Uzantı yapılandırması belirtmek için biçimi şöyledir.

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

Yukarıdaki görebileceğiniz gibi uzantısı şablon iki ana bölümleri içerir:

1. Uzantı adı, yayımcı ve sürüm
2. Uzantı yapılandırması.

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a>Yayımcı, türü ve uzantıyı typeHandlerVersion tanımlama
Azure VM uzantıları Microsoft tarafından yayınlanan ve güvenilir 3 taraf Yayımcılar ve her uzantı benzersiz olarak tanımlanır, yayımcısı, türü ve typeHandlerVersion. Bunlar aşağıdaki gibi belirlenebilir:  

