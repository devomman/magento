# Magento 2.4.1 Local Setup using XAMPP
[![N|Solid](https://raw.githubusercontent.com/omman/magento/2183eafe35417197adf8ea0f94ece7bceab83be2/xampp-magento.svg)](https://github.com/omman/magento/)

* [Requirements](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) - System Requirements.
* [Elastic Search](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/elasticsearch.html) - Required Elastic Search.
* [Diagram](https://devdocs.magento.com/guides/v2.4/install-gde/install-flow-diagram.html) - Installation Flow Chart.
* [Magento](https://magento.com/tech-resources/download)- Download Magento.
* [XAMPP](https://www.apachefriends.org/download.html)- Download Apache Server For Local.
* [Composer](https://getcomposer.org/) - Download Composer.
* [Elastic Search](https://www.elastic.co/downloads/elasticsearch) - Download Elastic Search.


## Folow Step by Step

  1. Download [XAMPP](https://www.apachefriends.org/download.html) and install and Run.
  2. Download [Composer](https://getcomposer.org/) and install.
  3. While Installing Composer Select "C:\xampp\php\php.exe" then finish installing.
  5. Download [Elastic Search](https://www.elastic.co/downloads/elasticsearch) Zip File.
  6. Extract zip to "C:\xampp\htdocs\" and Rename folder "elasticsearch" inside "C:\xampp\htdocs\"
  7. Now Goto "C:\xampp\htdocs\elasticsearch\bin\elasticsearch.bat" and RunAs Administrator also Check in Browser Working or Not:
  ```
  http://localhost:9200/
  ```
  8. Don't Close Or Terminate "elasticsearch.bat" until magento install has done.
  9. Download [Magento](https://magento.com/tech-resources/download) zip file. (Choose Sample Data or Empty then Signin/Signup to Download)
  10. Extract zip to "C:\xampp\htdocs\" and Rename folder "yourdomain.com" inside "C:\xampp\htdocs\"
  11. Now Goto "C:\xampp\htdocs\yourdomain.com\vendor\magento\framework\Image\Adapter\Gd2.php" file and open it Any Editor.
  12. Areound Line 86. Replace the code below:
  ```
  private function validateURLScheme(string $filename) : bool
  {
      $allowed_schemes = ['ftp', 'ftps', 'http', 'https'];
      $url = parse_url($filename);
      if ($url && isset($url['scheme']) && !in_array($url['scheme'], $allowed_schemes) && !file_exists($filename)) {
          return false;
      }

      return true;
  }
  ```
  13. Now Check in Browser "Localhost/yourdomain.com" and it's asking to setup with command line Ex. Below:
  
      Welcome to Magento Admin, your online store headquarters.\
      Please review Terms & Agreement and read [Getting Started](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli.html) to learn\
      how to install Magento using the command line.
  14. Now Open Browser and Type 
  ```
  http://localhost/phpmyadmin/
  ```
  15. Goto: Database Tab >> Type: magentolocal_db >> Click: Create
  16. Now goto "C:\xampp\htdocs\yourdomain.com\" and Address Bar Type "cmd" to run the command same folder or Goto same directory using command line.
  17. Now Run below command and chnage yours a) Domain Name, DB Name, User, Email & Password:
  ```
    php bin/magento setup:install --base-url="http://localhost/yourdomain.com" --db-host="localhost" --db-name="magentolocal_com_db" --db-user="root" --db-password="" --admin-firstname="system" --admin-lastname="admin" --admin-email="devomman@gmail.com" --admin-user="systemadmin" --admin-password="@dminPass1" --use-rewrites="1" --backend-frontname="admin"
  ```
  18. First Time Xampp User Getting this Error Below will Appear in Command Line:

      In Installer.php line 545:\
      <table><tr><td bgcolor=#d73a49>Missing following extensions: 'intl' 'soap' 'xsl' 'sockets'</td></tr></table>

  19. So Now We have enable following extensions in "C:\xampp\php\php.ini" open php.ini file in Editor
  ```
  ;extension=intl
  ;extension=soap
  ;extension=xsl
  ;extension=sockets
  ```
  20. Search one by one extension line in editor and uncomment the line to enable.
  21. Once you enable then stop and exit XAMPP Server and Restart don't close/terminate elastic search until the setup process completely done.
  22. Now Follow the Same ```Step 16 - Step 17.``` Again and the ```result:``` will appear Below ex:

  <font color = "# 006600"> [SUCCESS]: Magento installation complete.</font><br /> 
  <font color = "# 006600"> [SUCCESS]: Magento Admin URI: /admin</font><br /> 
  <font color = "# 006600"> [SUCCESS]: Nothing to import.</font>
  
  23. Now Follow the Same ```Step 16``` and Type in Command Line Below:
  ```
  php bin/magento indexer:reindex
  php bin/magento setup:upgrade
  php bin/magento setup:static-content:deploy -f
  php bin/magento cache:clean
  php bin/magento cache:flush
  ```
  24. After Done >> Goto "C:\xampp\htdocs\yourdomain.com\app\etc\di.xml" and Open in Editor
  25. Search "Symlink" and Replace to "Copy"  <font color = "# 006600">  ***This Step is Not Required - try without this step*** </font>
  26. Now Goto "C:\xampp\htdocs\yourdomain.com\vendor\magento\framework\View\Element\Template\File\Validator.php" and Open in Editor
  27. Chnage the Line Around 138 Below:
  ```
  $realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));
  ```
  28. Now Follow the Same ```Step 16``` and Type in Command Line Below and Done!
  ```
  php bin/magento cache:flush
  ```
  29. Disable Magento_TwoFactorAuth if Needed Follow the Same ```Step 16``` and Type in Command Line:
  ```
  php bin/magento module:disable Magento_TwoFactorAuth
  ```
### Requied Download Files
Note: Please download this files before you start.

| Download | Link |
| ------ | ------ |
| Magento | [https://magento.com/tech-resources/download][Magento] |
| XAMPP | [https://www.apachefriends.org/download.html][XAMPP] |
| Composer | [https://getcomposer.org/][Composer] |
| Elastic Search | [https://www.elastic.co/downloads/elasticsearch][Elastic Search] |


**Thanks to Muhammad Omman | Email: devomman@gmail.com**

[//]: # (Download Files Links)
[Magento]: <https://magento.com/tech-resources/download>
[XAMPP]: <https://www.apachefriends.org/download.html>
[Composer]: <https://getcomposer.org/>
[Elastic Search]: <https://www.elastic.co/downloads/elasticsearch>
