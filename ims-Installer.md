## Application Installation

### Software

This application needs below software and provided under C:\OnlineApp\installer. Install these software with default instructions.

Java version 17

-  Run **jdk-17_windows-x64_bin.exe**
- to check installation run command **java -version** 

Node version 22

- Run node-v22.8.0-x64.msi
- To check installation run command **node --version**



## Database setup 1

#### Create Tables

Execute provided create table sql in master schema

#### Create user SUPERADMIN

`INSERT INTO master.mst_admin_user (user_code, username, active, email, password, otp, user_type, upd_user)`
`VALUES ('99999', 'SUPERADMIN', TRUE, 'SUPERADMIN', 'test1', NULL, 'S', 'Admin');`

#### Create Reference data

`INSERT INTO sys_po_group (po_group_code, po_group_desc, status, upd_user)`
`VALUES`
`('CITY', 'City', NULL, 'admin'),`
`('CNTRY', 'Contries', TRUE, 'admin'),`
`('FFREQ', 'Filing Frequencey', NULL, 'admin'),`
`('REGTY', 'Registration Type', NULL, 'admin'),`
`('STATE', 'States', NULL, 'admin');`

`INSERT INTO sys_po_group (po_group_code, po_data_code, po_data_desc, status, upd_user)`
`VALUES`
`('CITY', 'MUM', 'Mumbai', FALSE, 'admin'),`
`('CITY', 'NAG', 'Nagpur', FALSE, 'admin'),`
`('CNTRY', 'India', 'India', FALSE, 'admin'),`
`('FFREQ', 'M', 'Monthly', FALSE, 'admin'),`
`('REGTY', 'R', 'Regn Type', FALSE, 'admin'),`
`('STATE', 'MH', 'Maharashtra', FALSE, 'admin');`



## Start/Stop Server

Start Server by running `start-application.bat`

Stop Server by running `stop-application.bat`



#### Create Company

- Login with SUPERADMIN
- Go to application and create company
- Generate key and Token for shop admin 



## Database setup 2

#### Create user SHOPADMIN 

`INSERT INTO master.mst_app_user (company_code, user_code, username, active, email, password, otp, user_type, upd_user)`
`VALUES ('<Company_code>', '99999', 'SHOPADMIN', TRUE, 'SHOPADMIN', 'test1', NULL, 'A', 'Admin' );`



#### Create Roles

`INSERT INTO master.mst_role (company_code, role_name, upd_user)`
`VALUES (<Company_code>, 'Customer', 'Admin');`

`INSERT INTO master.mst_role (company_code, role_name, upd_user)`
`VALUES (<Company_code>, 'Shop Admin', 'Admin');`

`INSERT INTO master.mst_role (company_code, role_name, upd_user)`
`VALUES (<Company_code>, 'Super Admin', 'Admin');`



#### Create data for Autonumbering

`INSERT INTO master.mst_data_sequence (company_code, tablename, prefix, counter, padding)` 
`VALUES` 
`(<Company_code>, 'mst_app_user', NULL, '0', '5'),`
`(<Company_code>, 'tran_order', NULL, '0', '10');`



## Integration

#### Product Upload

Product upload can be done through .csv file for online application. Sample template provided in installer.

###### How to upload data 

command file is provided to upload data (product-upload.bat). 

| Parameter   | Description                                     | Example                      |
| ----------- | ----------------------------------------------- | ---------------------------- |
| source-file | .csv file path                                  | c:/temp/product.csv          |
| logs        | output logs for api to upload product data      | c:/temp/product.log          |
| delete      | flag to decide to delete all product and import | true                         |
| key         | secret key for api                              | jcGdwYkpKWtZrBP.......       |
| token       | token for api                                   | eyJhbGciOiJSUzI1NiJ9.ey..... |

**product-upload** C:\OnlineApp\integration\mst_product.csv C:\OnlineApp\integration\test\logs true jcGdwYkpKWtZrBPyT5p..... eyJhbGciOiJSUzI1NiJ9.eyJzdWIi....

#### Image Upload

User can bulk upload product images using this API.

###### How to upload images 

command file is provided to upload data (product-image-upload.bat). 

| Parameter     | Description        | Example                      |
| ------------- | ------------------ | ---------------------------- |
| source-folder | .csv file path     | c:/temp/image                |
| key           | secret key for api | jcGdwYkpKWtZrBP.......       |
| token         | token for api      | eyJhbGciOiJSUzI1NiJ9.ey..... |

**product-image-upload** C:\OnlineApp\integration\img jcGdwYkpKWtZrBPyT5p..... eyJhbGciOiJSUzI1NiJ9.eyJzdWIi....

| Image type            | image name                               | Instructions                                      |
| --------------------- | ---------------------------------------- | ------------------------------------------------- |
| Product images        | <product name>.jpg                       | aspect ratio must be 1X1 (recommended size 50kb   |
| Default product image | default.jpg                              | aspect ratio must be 1X1 (recommended size 50kb)  |
| Banners               | banner-1.jpg, banner-2.jpg, banner-3.jpg | aspect ratio must be 1X8 (recommended size 150kb) |
| logo                  | site-logo.jpg                            | aspect ratio must be 1X1 or 1X2 (size 20kb)       |
| Home Page             | home-page.jpg                            | aspect ratio must be 1X2 (recommended 100kb)      |

