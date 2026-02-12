## What Apache Needs Access To & Why

### **READ access to everything:**

Apache needs to read ALL WordPress files to serve your website:

- PHP files (to execute them)
- CSS, JS, images (to serve to visitors)
- Theme and plugin files (to run your site)

### **WRITE access only to specific directories:**

1. **`wp-content/uploads/`** - When users upload images through the media library
2. **`wp-content/plugins/`** - When installing/updating plugins via dashboard
3. **`wp-content/themes/`** - When installing/updating themes via dashboard
4. **`wp-content/upgrade/`** - Temporary directory for updates
5. **`wp-content/cache/`** - If using caching plugins (if exists)

### **Optionally WRITE access for auto-updates:**

- **`wp-admin/`** - Core WordPress admin files
- **`wp-includes/`** - Core WordPress system files
- Root WordPress files (like `wp-config.php` during major updates)

## SELinux

You will probably need to set to Permissive on updates [[SELinux]]