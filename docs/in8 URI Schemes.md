# Introduction to `in8` URI Schemes (Protocol Schemes)

## Supported in8 URI Schemes
| Scheme       | Description |
|--------------|-------------|
| `http://`    | HyperText Transfer Protocol (web pages) |
| `https://`   | Secure version of HTTP                  |
| `bundle://`  | RO bundled resource                     |
| `appdata://` | RW files found in the Application Support Directory |
| `file://`    | Local file access                       |


## Proposed extended in8 URI Schemes
| Scheme       | Description |
|--------------|-------------|
| `effects://` | --> `bundle://effects`                       |
| `images://`  | --> `bundle://images`                       |
| `music://`   | --> `bundle://music`                       |
| `samples://` | --> `bundle://samples`                       |


A **Uniform Resource Identifier (URI) scheme**, also known as a **protocol scheme**, is the prefix in a URI that specifies how to access a resource. Common examples include `http://`, `https://`, `file://`, and `mailto:`. These schemes define the method used to retrieve or interact with the resource.

## Common URI Schemes

| Scheme       | Description |
|-------------|-------------|
| `http://`   | HyperText Transfer Protocol (web pages) |
| `https://`  | Secure version of HTTP |
| `file://`   | Local file access |
| `ftp://`    | File Transfer Protocol |
| `mailto:`   | Open an email client with a prefilled recipient |
| `tel:`      | Initiate a phone call |
| `sms:`      | Open SMS messaging with a predefined number |
| `geo:`      | Open a geographic location |

## Platform-Specific URI Schemes

### iOS File Locations

On iOS, files are stored in specific directories, and Apple provides URI schemes to access them:

- **Bundled Files (Read-Only)**  
  `file://<app-bundle-path>/`  
  Example: `file:///var/containers/Bundle/Application/.../MyApp.app/resource.txt`

- **Application Support Directory**  
  `file://<app-support-path>/`  
  Example: `file:///var/mobile/Containers/Data/Application/.../Library/Application Support/myfile.txt`

- **Documents Directory (User Files)**  
  `file://<documents-path>/`  
  Example: `file:///var/mobile/Containers/Data/Application/.../Documents/myfile.txt`

- **Temporary Files**  
  `file://<tmp-path>/`  
  Example: `file:///var/mobile/Containers/Data/Application/.../tmp/tempfile.txt`

- **Cloud Storage (iCloud)**  
  `file://<icloud-container-path>/`  
  Example: `file:///private/var/mobile/Library/Mobile Documents/com~apple~CloudDocs/myfile.txt`

### Android File Locations

Android uses different storage directories, with URI schemes that allow access:

- **Assets (Read-Only, Bundled in APK)**  
  `file:///android_asset/`  
  Example: `file:///android_asset/index.html`

- **Raw Resources (Read-Only)**  
  `android.resource://<package-name>/raw/<resource-name>`  
  Example: `android.resource://com.example.app/raw/musicfile`

- **Internal Storage (Private to App)**  
  `file://<internal-storage-path>/`  
  Example: `file:///data/data/com.example.app/files/myfile.txt`

- **External Storage (Shared, Requires Permissions)**  
  `file://<external-storage-path>/`  
  Example: `file:///storage/emulated/0/Download/myfile.txt`

- **Content Provider URIs**  
  `content://<authority>/<path>`  
  Example: `content://com.example.app.provider/files/myfile.txt`

## Summary

URI schemes provide a structured way to access resources both locally and on the internet. Different platforms define their own schemes for accessing files and system services. When developing apps, it is important to use the correct URI format for the intended platform to ensure proper functionality and security.

