### <a name="app-service-plan"></a><span data-ttu-id="ce62e-101">App Service planı</span><span class="sxs-lookup"><span data-stu-id="ce62e-101">App Service plan</span></span>
<span data-ttu-id="ce62e-102">Web uygulamasını barındırmak için hizmet planını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce62e-102">Creates the service plan for hosting the web app.</span></span> <span data-ttu-id="ce62e-103">Planı aracılığıyla adını sağlayın **hostingPlanName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="ce62e-103">You provide the name of the plan through the **hostingPlanName** parameter.</span></span> <span data-ttu-id="ce62e-104">Kaynak grubu için kullanılan aynı konuma plan konumudur.</span><span class="sxs-lookup"><span data-stu-id="ce62e-104">The location of the plan is the same location used for the resource group.</span></span> <span data-ttu-id="ce62e-105">Fiyatlandırma katmanı ve çalışan boyutu belirtilir **sku** ve **workerSize** parametreleri</span><span class="sxs-lookup"><span data-stu-id="ce62e-105">The pricing tier and worker size are specified in the **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

