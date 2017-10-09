### <a name="install-via-composer"></a>Oluşturucu yükleyin
1. [Git'i yükleyin][install-git]. Windows üzerinde ayrıca hello Git yürütülebilir tooyour PATH ortam değişkeni eklemeniz gerektiğini unutmayın. 
2. Adlı bir dosya oluşturun **composer.json** hello projenizin kök ve kod tooit aşağıdaki hello ekleyin:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Karşıdan  **[composer.phar] [ composer-phar]**  proje kök.
4. Bir komut istemi açın ve proje kök komutunda aşağıdaki hello yürütme
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
