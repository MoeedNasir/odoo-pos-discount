**Custom POS Discount Module**
A custom Odoo module that adds advanced discount functionality to the Point of Sale (POS) system, allowing amount-based discounts and free product capabilities.

**Features**
Amount-Based Discounts: Apply specific discount amounts to order lines

Free Products: Automatically set products as free when the discount exceeds the line total

Visual Discount Display: See discount amounts directly in the order line

User-Friendly Interface: Simple dollar button input in the POS interface

Persistent Data: Discounts are saved and persist through order sessions

**Installation**
**Method 1: Standard Odoo Module Installation**
Clone this repository to your Odoo addons directory:
bash
cd /path/to/odoo/addons
git clone https://github.com/yourusername/custom-pos-discount.git
Install the module:
Go to the Odoo Apps menu
Search for "Custom POS Discount"
Click Install

**Method 2: Manual Installation**
Copy the module folder to your Odoo addons directory
Update the apps list:
bash
./odoo-bin -d your_database --addons-path=addons --update=custom_pos_discount
Configuration
Enable Developer Mode in Odoo
Go to Point of Sale → Configuration → Point of Sale
Select your POS configuration
Ensure the module is loaded by checking the POS assets

**Usage**
Applying Discounts
Open POS Session: Start a new POS session
Add Products: Add products to the order as usual
Apply Discount:
Select the order line you want to discount
Click the $ (Dollar) button in the control buttons area
Enter the discount amount in the input field
Press Enter to apply the discount

**Discount Behavior**
Regular Discount: Enter an amount less than the line total to apply a partial discount
Free Product: Enter an amount equal to or greater than the line total to make the product free
Visual Feedback: Discounted amounts are displayed below the product price in the order line

**Technical Details**
**Module Structure**

custom_pos_discount/
├── __init__.py
├── __manifest__.py
├── static/
│   └── src/
│       ├── js/
│       │   └── discount.js             # Main discount functionality
│       └── xml/
│           ├── discount_button.xml     # POS UI button
│           └── orderline_ui.xml        # Discount display in order lines
├── views/
│   ├── views.xml
│   └── templates.xml
└── README.md

**Key Components**
ControlButtons Patch (discount.js):
Adds discount input toggle functionality
Handles discount amount calculations
Manages free product logic
Orderline Model Patch (discount.js):
Extends Orderline with the discount_amount field
Adds display data formatting for discounts
Implements JSON serialization for persistence
Orderline Component Patch (orderline_component.js):
Allows discount_amount prop in component validation
Ensures proper type checking

**Dependencies**
Odoo 16.0+ (Point of Sale module)
Base module

**Customization**
Modifying Discount Behavior
Edit static/src/js/discount.js to change discount logic:
**javascript**
// Example: Change free product threshold
if (value >= lineTotal * 0.9) {  // 90% discount makes product free
    line.discount_amount = lineTotal;
    line.set_unit_price(0);
}
Styling Discount Display
Modify static/src/xml/orderline_ui.xml to change the discount appearance:
**xml**
<div class="discount-amount custom-style">
    <span class="discount-label">Custom Label: </span>
    <span class="discount-value" t-esc="props.line.discount_amount"/>
</div>

**Troubleshooting**
Common Issues
Module Not Loading:
Check Odoo server logs for errors
Verify module is in the correct addons path
Ensure the POS is restarted after installation
Discount Button Not Appearing:
Verify the POS configuration is active
Check the browser console for JavaScript errors
Clear the browser cache and reload the POS
Discounts Not Saving:
Check database permissions
Verify module dependencies are met
Review server logs for JSON serialization errors
Debug Mode
Enable Odoo debug mode for detailed error information:
Add ?debug=1 to Odoo URL
Check the browser console for JavaScript errors
Review Odoo server logs for backend issues

**Contributing**
Fork the repository
Create a feature branch: git checkout -b feature/new-feature
Commit changes: git commit -am 'Add new feature'
Push to branch: git push origin feature/new-feature
Submit a pull request

**License**
This module is licensed under LGPL-3, same as Odoo. See LICENSE file for details.

**Support**
For issues and questions:
Create an issue on GitHub
Check existing issues for solutions
Provide detailed error messages and Odoo version

**Version History**
v0.1 (Current): Initial release
Basic amount-based discounts
Free product functionality
POS interface integration

**Acknowledgments**
Odoo Community Association for the base POS system

Contributors and testers
