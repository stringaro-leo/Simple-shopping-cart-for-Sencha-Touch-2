Simple-shopping-cart-for-Sencha-Touch-2
=======================================

Simple yet powerful script for adding shopping cart features to Sencha Touch based mobile apps.

Author: Constantine V. Smirnov, kostysh(at)gmail.com, http://mindsaur.com    
License: GNU GPL v3.0    
Current version: 1.1    
ST2 version: 2.1.0 Beta1    
ST2 SDK Tools: 2.0.0 Beta 3    

Versions:
=========
- 1.1 New namespace, improved API and config, new carts archive feature, bug fixes, SDK updates
- 1.0.1 Various bug fixes and improvements
- 1.0 First release

Features:
=========
- Adding products to cart
- Cart indicator with total count of items and total sum badges
- Cart panel with list of added products, quantity management, cart submitting
- Archive of submitted carts (with ability to restore carts from archive)

Upgrade from 1.0.1 to 1.1:
===================
- Update src files
- Update app.js (add Archive controller)
- Remove cart items from localStorage (or localStorage.clear(); from console)
- Restart App

Installing:
===========
- Place src to your app folder;
- Configure custom path for cart components: 
<!-- language: lang-js -->
        
        Ext.Loader.setPath({
            'Ext.ux': 'src/ux'
        });
- Add cart controllers to Ext.application() config:
<!-- language: lang-js -->
        
        controllers: [
            'Ext.ux.Cart.controller.Indicator',
            'Ext.ux.Cart.controller.Panel',
            'Ext.ux.Cart.controller.Archive'
        ],
- Add path to cart css into app.json (or into index.html directly):
<!-- language: lang-js -->
        
        {
            "path": "src/ux/Cart/resources/css/cart.css",
            "update": "delta"
        }
- Initialize cart from 'launch' application method:
<!-- language: lang-js -->
        
        // Initialize shopping cart products store
        // Look for products store example in demo
        Cart.setProductsStore('Products_store_name');
    
        // Setup currency abr
        Cart.setCurrency('USD');
    
        // Setup cart submit callback
        Cart.setCallback(function(encData) {
            
            /**
             * You can use cart data as you want
             */
    
            console.log('Cart data submited', Ext.decode(encData));
    
            // For now we show message only
            Ext.Msg.alert(
                null,
                Ext.String.ellipsis(encData, 16, true) +
                ' more in console'
            );
        });


Cart API methods:
=============
<!-- language: lang-js -->
        
    Cart.create();// Create and activate new cart
    Cart.deactivate();// Deactivate current active cart
    Cart.add(id, qty);// Add new record to cart (or update existed)
    Cart.update(id, qty, increment);// Update cart item
    Cart.remove(id);// Remove product record from cart by Id
    Cart.removeAll();// Remove all products from cart
    Cart.getProductsCount();// Return count of products in active cart
    Cart.getTotalSum(id);// Get total sum of products in active cart
    Cart.getProductById(id);// Get product record by Id from products store
    Cart.isArchive();// Check for archived carts
    Cart.restore(id);// Restore archived cart by Id
    Cart.clearArchive();// Clear all archived carts

Script is fully commented, look into src/ux/Cart/src/Core.js

Live demo: 
==========
http://mindsaur.com/demo/cart

Known issues:
=============
- Current ST2 localStorage proxy not works correctly with hasMany data associations. 
This issue temporary fixed by override code from src/component/cart/utils/WebStor.js