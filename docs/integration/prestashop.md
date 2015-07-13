# PrestaShop

PrestaShop is a comprehensive e-commerce platform, allowing any business owner to quickly create an online shop for all sorts of products. But to ensure high quality service and build strong customer relationships, every e-commerce website should have a reliable support system. DiamanteDesk is a perfect solution for that.

DiamanteDesk PrestaShop module allows both administrator and any customer to create, edit and view tickets directly on a PrestaShop e-commerce website. All the tickets can be grouped into Branches. To learn more about branches in DiamanteDesk, see the **Branches** section in User Guide.

## Installing DiamanteDesk Module

1. Log in the PrestaShop Admin Panel.
2. On the navigation panel head over to _Modules > Modules and Themes Catalog_ for automatic installation.
![Prestashop Admin panel](img/prestashop_admin_panel.png)

###### Automatic installation

1. On the **Modules** screen head over to the PrestaShop **Modules List**.
![Prestashop Module list](img/prestashop_modules_list.png)
1. Enter **DiamanteDesk** in the **Search Plugins** field and press Enter.
1. Click **Install**.

###### Manual installation

**Option 1 - Installation via FTP:**

1. Upload the addthis folder to the `modules/` directory.
1. Head over to the PrestaShop admin area and connect DiamanteDesk and PrestaShop (please see the **Connecting DiamanteDesk to PrstaShop** section).

**Option 2 - Installation via archive:**

1. Download DiamanteDesk module for PrestaShop from Github.
2. On the top right corner of the **Modules** screen click **Add a new module**.
2. Select the downloaded zip file from your computer.
3. Click **Install Now** and activate the plugin.
4. Head over to **Add a new module** section.
![Add a new module section](img/prestashop_new_module.png)
5. Click **Choose a file** and find a required file on your local machine.
6. Click **Upload this module**.
7. After the module has been successfully installed, head over to the PrestaShop **Modules List**.
![Prestashop Module list](img/prestashop_modules_list.png)
8. Enter **DiamanteDesk** in the **Search Plugins** field and press Enter.
1. Click **Install**.

___
>_Note:_ Make sure that you clear the PrestaShop caches to complete the installation of an extension.

## Connecting DiamanteDesk to PrstaShop

After the module has been successfully installed, the DiamanteDesk module configuration page opens. The module shall be configured for the proper work of a help desk.

In order to do that, complete the following steps:

1. Acquire [API credentials](api-credentials.md) from your CRM.
5. Get back to DiamanteDesk module configuration page at **Prestashop**.
![Prestashop module configuration](img/prestashop_config.png)
7. Provide the link to the server in the **Server Address** field.
8. Enter the **Username** and **Api Key** from your CRM.
9. Click **Save**.
10. If the credentials are correct and the connection between PrestaShop and DiamanteDesk has been successfully made, a new **Default Branch** field will be added to the DiamanteDesk configuration. 
![Prestashop branches](img/prestashop_branches.png)
12. Select a default branch from the drop-down list.
13. Click **Save**.