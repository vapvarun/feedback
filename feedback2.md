
# Code Review for Custom WooCommerce Product Stock Checker

## Assignment Overview

### Problem Statement:
You were tasked with creating custom WooCommerce functionality that allows customers to check a product's stock availability directly from the product page by entering their desired quantity. The check should be performed using AJAX, and the result should be displayed without reloading the page.

## Code Review

# Must Fix Issues for Custom WooCommerce Product Stock Checker

## 1. WooCommerce Dependency Handling

### Issue:
The plugin currently throws an error when WooCommerce is not active, which can break the site if WooCommerce is not installed or activated.

### Solution:
Implement a more graceful handling mechanism. The plugin should show an admin notice indicating that WooCommerce is required and deactivate itself without causing errors.

### Code Example:

```php
function akwsc_is_woocommerce_active() {
    // Check if WooCommerce is active
    if ( !class_exists( 'WooCommerce' ) ) {
        // WooCommerce is not active, prevent plugin activation
        add_action( 'admin_notices', 'akwsc_woocommerce_not_available_admin_notice' );
        deactivate_plugins( plugin_basename( __FILE__ ) );

        if ( isset( $_GET['activate'] ) ) {
            unset( $_GET['activate'] );
        }
    }
}

function akwsc_woocommerce_not_available_admin_notice() {
    ?>
    <div class="notice notice-error is-dismissible">
        <p>
            <strong><?php esc_html_e( 'AK WooCommerce Stock Checker requires WooCommerce to be installed and active. The plugin has been deactivated.', AKWSC_TEXT_DOMAIN ); ?></strong>
        </p>
    </div>
    <?php
}
add_action( 'admin_init', 'akwsc_is_woocommerce_active' );
```

---

## 2. Namespace Usage

### Issue:
The code lacks a namespace, which could lead to potential conflicts with other plugins or themes.

### Solution:
Introduce namespaces across all classes and functions to encapsulate the code and avoid conflicts.

### Code Example:

```php
namespace Akash\Akwsc;

class Akwsc_Admin {
    // Your code here...
}
```

---

## 3. Centralize Version and Plugin Name Definitions

### Issue:
Version and plugin name are defined in multiple places, which can lead to inconsistencies.

### Solution:
Define version and plugin name in one place (e.g., in the root file) and pass them to the public class during instantiation.

### Code Example:

**Root File:**

```php
// Root File - plugin bootstrap file
define( 'AKWSC__VERSION', '1.0.0' );
define( 'AKWSC_PLUGIN_NAME', 'AK WooCommerce Stock Checker' );
```

**Public Class:**

```php
class Akwsc_Public {
    private $plugin_name;
    private $version;

    public function __construct() {
        $this->plugin_name = AKWSC_PLUGIN_NAME;
        $this->version = AKWSC__VERSION;
    }

    // Use the version and plugin name consistently throughout the class
}
```

---

## 4. Enqueue Scripts and Styles with Versioning and Conditional Loading

### Issue:
The `enqueue_styles()` and `enqueue_scripts()` functions enqueue styles and scripts, but there are areas for improvement, particularly around versioning and dependency management.

### Solution:
- Always use the plugin's version constant (`$this->version`) when enqueuing scripts and styles.
- Ensure that any dependencies required by the script are correctly listed in the array parameter.
- If the CSS/JS files are only needed on specific pages, wrap the enqueue call in a conditional check.

### Code Example:

```php
public function enqueue_styles() {
    // Check if we are on a specific admin page
    $screen = get_current_screen();
    if ( $screen && $screen->id === 'woocommerce_page_stock_checker' ) {
        wp_enqueue_style( 
            $this->plugin_name, 
            plugin_dir_url( __FILE__ ) . 'css/akwsc-public.css', 
            array(), 
            $this->version, // Versioning to ensure proper caching
            'all' 
        );
    }
}

public function enqueue_scripts() {
    // Check if we are on a specific admin page
    $screen = get_current_screen();
    if ( $screen && $screen->id === 'woocommerce_page_stock_checker' ) {
        wp_enqueue_script( 
            $this->plugin_name, 
            plugin_dir_url( __FILE__ ) . 'js/akwsc-public.js', 
            array( 'jquery' ), // List dependencies here
            $this->version,  // Versioning to ensure proper caching
            true // Load in footer
        );

        // Localize script with dynamic data
        wp_localize_script( 
            $this->plugin_name, 
            'akwsc', 
            array(
                'ajaxurl' => admin_url('admin-ajax.php'),
                'nonce'   => wp_create_nonce( AKWSC_NONCE_KEY ),
            )
        );
    }
}
```

---

## 5. Improved Error Handling in AJAX Callback

### Issue:
The error handling in the AJAX callback could be more robust, providing better user feedback and logging.

### Solution:
Enhance error handling in the AJAX callback by validating inputs, sanitizing data, and logging errors.

### Code Example:

```php
public function akwsc_stock_check_action_callback() {
    // Validate the AJAX request and nonce
    if ( ! defined( 'DOING_AJAX' ) || ! DOING_AJAX || ! isset( $_POST['nonce'] ) || ! wp_verify_nonce( $_POST['nonce'], AKWSC_NONCE_KEY ) ) {
        wp_send_json_error( array( 'message' => Akwsc_Plugin_Messages::get_error_message( 'invalid_request' ) ) );
    }

    try {
        // Sanitize and validate input
        $product_id    = filter_input( INPUT_POST, 'product_id', FILTER_SANITIZE_NUMBER_INT );
        $requested_qty = filter_input( INPUT_POST, 'requested_qty', FILTER_SANITIZE_NUMBER_INT );

        if ( ! $product_id || ! $requested_qty || $requested_qty < 1 ) {
            wp_send_json_error( array( 'message' => Akwsc_Plugin_Messages::get_error_message( 'invalid_params' ) ) );
        }

        // Perform stock check logic...

    } catch ( Exception $e ) {
        error_log( 'Error in akwsc_stock_check_action_callback: ' . $e->getMessage() );
        wp_send_json_error( array( 'message' => esc_html__( 'An unexpected error occurred. Please try again later.', AKWSC_TEXT_DOMAIN ) ) );
    }
}
```

---

# General Suggestions for Custom WooCommerce Product Stock Checker

## 1. Code Organization and Structure

### Issue:
The code could benefit from better organization to improve readability and maintainability.

### Suggestion:
- Break down larger functions into smaller, more manageable pieces.
- Group related functionalities together to make the code easier to navigate.

### Code Example:

Instead of having a single large function that handles multiple tasks, consider breaking it down:

```php
public function handle_stock_check() {
    if ($this->is_grouped_product()) {
        $this->handle_grouped_product_stock_check();
    } else {
        $this->handle_single_product_stock_check();
    }
}

private function is_grouped_product() {
    // Logic to check if the product is grouped
}

private function handle_grouped_product_stock_check() {
    // Logic to handle stock check for grouped products
}

private function handle_single_product_stock_check() {
    // Logic to handle stock check for single products
}
```

---

## 2. Improved Documentation

### Issue:
While the code has some documentation, it could be more detailed, especially for more complex functions.

### Suggestion:
- Provide clear, concise comments explaining the purpose of each function and complex logic.
- Use PHPDoc comments for all public methods and properties, detailing parameters, return values, and any exceptions thrown.

### Code Example:

```php
/**
 * Handles the stock check for grouped products.
 *
 * This method iterates through the provided product data, checks the stock status of each
 * child product in a grouped product, and constructs appropriate messages based on stock availability.
 * It then sends a JSON response indicating whether sufficient stock is available or not.
 *
 * @param array $products_data  Array of child products' data, each containing 'product_id' and 'requested_qty'.
 * 
 * @return void
 */
private function handle_grouped_product_stock_check($products_data) {
    // Method logic here
}
```

---

## 3. Client-Side Validation

### Issue:
Client-side validation is not fully implemented, which can lead to a poor user experience.

### Suggestion:
- Implement comprehensive client-side validation to ensure that user inputs are validated before the AJAX request is made.

### Code Example:

```javascript
$(document).on('click.akwsc', '#akwsc-check-availability-button', function(e) {
    var qty = parseInt($('#akwsc_quantity_input').val(), 10);
    if (isNaN(qty) || qty < 1) {
        $('#akwsc-message-box').html('<p>Please enter a valid quantity greater than 0.</p>');
        return;
    }

    // Proceed with AJAX request if validation passes...
});
```

---

## 4. Error Messages and User Feedback

### Issue:
Error messages and user feedback could be more descriptive and user-friendly.

### Suggestion:
- Ensure that error messages provide clear guidance to the user about what went wrong and how they can fix it.
- Use WordPress translatable functions (`__()` or `esc_html__()`) for all user-facing messages to support localization.

### Code Example:

```php
wp_send_json_error([
    'message' => esc_html__('The requested quantity is not available. Please adjust the quantity and try again.', AKWSC_TEXT_DOMAIN)
]);
```

---

## 5. Considerations for Edge Cases

### Issue:
Some edge cases may not be fully considered, such as handling products with variations or dealing with zero stock scenarios.

### Suggestion:
- Implement additional checks and logic to handle edge cases, ensuring that the plugin behaves correctly under all circumstances.

### Code Example:

```php
if ($product->is_type('variable')) {
    // Handle stock check for variable products
} elseif ($product->get_stock_quantity() === 0) {
    wp_send_json_error([
        'message' => esc_html__('This product is currently out of stock.', AKWSC_TEXT_DOMAIN)
    ]);
}
```

---

These general suggestions aim to improve the overall quality, usability, and maintainability of the plugin.

### Code Review Summary

- **Original Code:**
   - The code demonstrates a solid understanding of AJAX and WordPress hooks.
   - Proper use of object-oriented principles.

- **Suggested Improvements:**
   - **WooCommerce Dependency:** Implement better handling for when WooCommerce is not active.
   - **Namespace Usage:** Add namespaces to prevent conflicts.
   - **Error Handling:** Improve error handling in AJAX.
   - **Validation:** Enhance client-side validation.
   - **Consistent Constants:** Use consistent naming conventions for constants.

## Final

Overall, the code meets many assignment requirements but could benefit from key improvements to ensure robustness, maintainability, and a better user experience. Addressing the issues mentioned above will make the plugin more reliable and user-friendly.

