## <a name="clean-up-deployment"></a><span data-ttu-id="4819b-101">Dağıtım temizleme</span><span class="sxs-lookup"><span data-stu-id="4819b-101">Clean up deployment</span></span> 

<span data-ttu-id="4819b-102">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, Azure Redis önbelleği örneği ve ilgili kaynakları kaynak grubunu kaldırmak için izleme komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4819b-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```