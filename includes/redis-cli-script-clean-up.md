## <a name="clean-up-deployment"></a><span data-ttu-id="617f2-101">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="617f2-101">Clean up deployment</span></span> 

<span data-ttu-id="617f2-102">Merhaba komut dosyası örneği çalıştırdıktan sonra hello izleyin komutu kullanılan tooremove hello kaynak grubu, Azure Redis önbelleği örneği ve ilgili kaynakları hello kaynak grubunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="617f2-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```