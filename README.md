# Day 3: Work with Configuration & Features

## Setup Development and Production Environments

1. **Create Two Drupal Projects**:
   - One for the **development environment**.
   - One for the **production environment**.

   Run the following commands:

   ```bash
   composer create-project drupal/recommended-project:^10 drupal_dev_env
   composer create-project drupal/recommended-project:^10 drupal_prod_env
   ```

2. **Install Drush and Devel in the Development Environment**:
   - Install Drush:
     ```bash
     composer require drush/drush
     ```
   - Install Devel:
     ```bash
     composer require drupal/devel
     ```
   - Enable Devel:
     ```bash
     drush en devel -y
     ```

   ![Enable Devel Module](https://github.com/user-attachments/assets/8b981a63-b247-4799-8de5-bfcf44f05c30)

---

## Create a Content Type: "Blog"

1. **Create the "Blog" Content Type**:
   - Go to `/admin/structure/types/add` and create a new content type named "Blog".

   ![Create Blog Content Type](https://github.com/user-attachments/assets/eee52348-165a-4ffa-b729-6a223cf2e5b1)

2. **Add Fields**:
   - Add fields to the "Blog" content type.
   - Add a reference field to the **"Product Type" taxonomy** (created earlier).

   ![Add Fields to Blog Content Type](https://github.com/user-attachments/assets/ae69e6cd-f9b3-48fd-adf7-8e3f2c3cae2b)

---

## Create a "Content Manager" Role

1. **Add a New Role**:
   - Go to `/admin/people/roles/add` and create a new role named **"Content Manager"**.

   ![Create Content Manager Role](https://github.com/user-attachments/assets/b087bf18-db7a-479b-a04c-f87fdc64bbf6)

2. **Set Permissions**:
   - Grant the **"Content Manager"** role permissions to manage the "Blog" content type.
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/25f3b6cf-f083-42b2-9793-863818f48b43" />

devel generate taxonomy
<img width="1420" alt="image" src="https://github.com/user-attachments/assets/733b5dff-e7cf-4ce8-b6b1-c0b0ce885fb7" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/5aaa47bd-5b9c-49df-9387-4379a3f1692d" />

devel generate blog
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/8bed1ac7-8c7f-4e1a-a393-be310614d41e" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/893aa3f9-4342-450f-9226-f713cbef3f20" />


## Practice Configuration Sync
To prevent Devel from being exported to production, use the Config Split module.
1. Install Config Split in Development Environment
```bash
composer require drupal/config_split
drush en config_split -y
```
2. Configure Config Split to exclude devel module in production environments
<img width="1375" alt="image" src="https://github.com/user-attachments/assets/cb8e9492-0f70-4aab-8449-aabfc3668c4a" />

3. Export Configuration of our development enviromenet
   using the command :
   ```bash
   drush config:export
   ```
<img width="720" alt="image" src="https://github.com/user-attachments/assets/e5b3d83a-2dbe-4c46-af9e-c8d85d799ed9" />

then we copy the directory confit/sync to production drupal project and change the settings.php to add the path of confit/sync
<img width="1036" alt="image" src="https://github.com/user-attachments/assets/d60d3d27-2452-4487-8be6-3e709055f652" />

next type the command line to import the exported config : 
```bash
drush config:import
```
<img width="1124" alt="image" src="https://github.com/user-attachments/assets/b8ef17e2-ac1d-4b9c-9c47-05e54c9e26b8" />
<img width="1122" alt="image" src="https://github.com/user-attachments/assets/f717677a-bc9e-4654-8a72-fa214ac75e15" />

now, let's verify the ui interface if the taxonomy "Product Type" and the content type "Blog" exists: 

<img width="1439" alt="image" src="https://github.com/user-attachments/assets/17e9b661-5c39-4305-9900-5860901b0812" />

<img width="1440" alt="image" src="https://github.com/user-attachments/assets/b2bb1c87-b41e-46e5-94ad-43a78fc022a8" />

## Question: Was devel installed in the production environement ? Devel is dev tool and should not be present in the production
No, Devel is a development tool and should not be present in the production environment. And we prevent Devel from being exported to production, using the Config Split module.

# Practice Features

1. Install and Enable the Features Module
In your development environment, install the Features module:

```bash
composer require 'drupal/features:^3.14'
drush en features -y
```
2. Go to /admin/config/development/features in your development environment.

Click "Create Feature".

Provide a name for your feature module custom_feature.

Select the components you want to include (content type (Blog), Taxonomy (Product Type)).
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/864745c8-442a-444c-83fa-8f29fdf73f6c" />
<img width="1430" alt="image" src="https://github.com/user-attachments/assets/28c7f770-a17a-4c63-a132-2cf32f93a74d" />
Click "Download Feature" to generate the module (custom_feature.tar.gz).
3. Transfer the Feature Module to Production
Copy the generated feature module (my_blog) from the modules/custom directory in your development environment to the modules/custom directory in your production environment.

4. Enable the Feature Module in Production
In your production environment, enable the feature module using Drush:

This will import the configuration from the feature module.
<img width="897" alt="image" src="https://github.com/user-attachments/assets/1e3bf95e-b35b-40ea-ae08-3ca09989a2bc" />

blog 
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/02612d0a-0a5b-4ee2-9cbc-c36f701b810a" />
tax
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/1e1b25f1-3754-4130-be6f-6ee4f1f60362" />

2. Edit the Content Type in Production

In your production environment, edit the content type (e.g., change its name):
<img width="1406" alt="image" src="https://github.com/user-attachments/assets/3ce78461-5293-4313-9ea4-359a63b3a792" />
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/18c9d567-079c-4fc1-8e54-9f881ab4d223" />


3. Add a New Field in Development
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/771a6962-bb06-4bee-8d5c-1abe0a1257a0" />

reset the blog name 
<img width="1437" alt="image" src="https://github.com/user-attachments/assets/ec45c7da-7cea-4acf-a8ea-c390cfb3812f" />

filed added 
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/9d843c21-15c0-42fd-a543-7df1c8929d31" />

# Question: Was their any conflicts that needed to be resolved ?
no their wasn't any error , when i change the name of content type in the first feature module in production env (blog -> blog_edit) then i add new field in the developement enviroment (new_field) , then i enable the last one in the prod env it works normally and in the ui it add the new field that add in the developement env, and also it reset the name of the changed one in the production to blog
