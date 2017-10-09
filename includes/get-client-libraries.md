### <a name="install-via-composer"></a><span data-ttu-id="b8159-101">Oluşturucu yükleyin</span><span class="sxs-lookup"><span data-stu-id="b8159-101">Install via Composer</span></span>
1. <span data-ttu-id="b8159-102">[Git'i yükleyin][install-git].</span><span class="sxs-lookup"><span data-stu-id="b8159-102">[Install Git][install-git].</span></span> <span data-ttu-id="b8159-103">Windows üzerinde ayrıca hello Git yürütülebilir tooyour PATH ortam değişkeni eklemeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b8159-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="b8159-104">Adlı bir dosya oluşturun **composer.json** hello projenizin kök ve kod tooit aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b8159-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="b8159-105">Karşıdan  **[composer.phar] [ composer-phar]**  proje kök.</span><span class="sxs-lookup"><span data-stu-id="b8159-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="b8159-106">Bir komut istemi açın ve proje kök komutunda aşağıdaki hello yürütme</span><span class="sxs-lookup"><span data-stu-id="b8159-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
