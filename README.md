## Configure Laravel for SQL Server

After installing SQL Server, you need to configure your Laravel application to use SQL Server as its database backend. Follow these steps to set up your Laravel project:

1. **Open SQL Server Configuration Manager**:

   - Open the Start menu and search for "SQL Server Configuration Manager."
   - Launch SQL Server Configuration Manager from the search results.
   - If you not found on windows please follow this [link](https://learn.microsoft.com/en-us/answers/questions/166724/sql-server-configuration-manager-not-showing-in-wi)
2. **Select "Protocols for MSSQLSERVER" (or Your SQL Server Instance Name)**:

   - In SQL Server Configuration Manager, navigate to "SQL Server Network Configuration" in the left pane.
   - Locate and select "Protocols for MSSQLSERVER" (or the name of your SQL Server instance if it's different).
3. **Enable the "TCP/IP" Protocol**:

   - In the right pane, you should see a list of protocols. Find "TCP/IP" and double-click it or right-click and select "Properties."
   - In the "TCP/IP Properties" window, go to the "Protocol" tab.
   - Change the "Enabled" property to "Yes" by selecting it from the dropdown menu.
   - Optionally, you can also specify a specific TCP port in the "IPAll" section, but you can leave it blank to use the default port (1433).
4. **Restart SQL Server**:

   - After making changes to the network protocols, you need to restart the SQL Server service to apply the settings.
   - In SQL Server Configuration Manager, go to "SQL Server Services" in the left pane.
   - Right-click on your SQL Server instance (usually named "SQL Server (MSSQLSERVER)") and select "Restart."
5. **Set Up Environment Variables**:

   - In your Laravel project directory, create or edit the `.env` file. This file contains environment-specific settings for your application.

     ```env
     DB_CONNECTION=sqlsrv
     DB_HOST=127.0.0.1
     DB_PORT=1433
     DB_DATABASE=your_database_name
     DB_USERNAME=your_database_username
     DB_PASSWORD=your_database_password
     ```

     - Replace placeholders (`your_database_name`, `your_database_username`, and `your_database_password`) with your actual SQL Server database credentials.
6. **Install SQL Server Driver for PHP**:

   - Download the appropriate version of the SQL Server driver for PHP from [Microsoft's website](https://docs.microsoft.com/en-us/sql/connect/php/download-drivers-php-sql-server).
7. **Enable SQL Server Extension in PHP**:

   - Open your `php.ini` configuration file, which is located in your PHP installation directory.
   - Ensure the following lines are uncommented (remove the semicolon at the beginning of each line):

     ```ini
     extension=sqlsrv
     extension=pdo_sqlsrv
     ```

     - Save the `php.ini` file.

     **If you are using on WampServer**:

     1. **Copy Extension Files**:

     - Download the necessary PHP extension files for SQL Server (`php_pdo_sqlsrv_7x_ts.dll` and `php_sqlsrv_7x_ts.dll`) from a trusted source or the official Microsoft website.
     - Paste these extension files into the `ext` directory of your PHP installation, typically located at `C:\wamp64\bin\php\php7.x\ext`.

     2. **Edit PHP Configuration (`php.ini`) for PHP CLI**:

     - Open the `php.ini` file in the PHP directory, usually found at `C:\wamp64\bin\php\php7.x\php.ini`.
     - Add the following lines to enable the SQL Server extensions for PHP CLI:

       ```ini
       extension=php_pdo_sqlsrv_7x_ts.dll
       extension=php_sqlsrv_7x_ts.dll
       ```
     3. **Edit PHP Configuration (`php.ini`) for Apache**:
     - Open the `php.ini` file used by Apache. This file is typically located in the Apache directory, usually at `C:\wamp64\bin\apache\apache2.4.xx\bin\php.ini`.
     - Add the same lines as in step 2 to enable the SQL Server extensions for PHP within the Apache environment:

         ```ini
         extension=php_pdo_sqlsrv_7x_ts.dll
         extension=php_sqlsrv_7x_ts.dll
         ```
     4. **Restart WAMPP Server**:
     - Save the changes to the `php.ini` files.
     - Restart the WAMPP server to apply the configuration changes.


8. **Download the ODBC Driver for SQL Server**:

   - Visit the Microsoft Download Center's [ODBC Driver for SQL Server](https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server) page.
   - Select the version of the ODBC driver that matches your operating system architecture (e.g., 32-bit or 64-bit). Choose the appropriate download link.
9. **Restart PC**:

    - Please restart your pc to complete these steps.
10. **Run Database Migrations**:

- In your Laravel project directory, open a terminal and run the following command to create the necessary tables in your SQL Server database:

  ```bash
  php artisan migrate
  ```

You have successfully configured Laravel to use SQL Server as the database backend for your application. You can now start developing your Laravel project with SQL Server.
