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

