Easylife Switcher
========

Configurable products switcher v1.2.0

**Release Notes 1.2.0 - 2014-10-22**

|Type|Issue|Comment|
|----|-----|-----|
|Feature|Manually set attributes to be transformed to labels|You can  now choose to transform only specific dropdowns to labels. You have the option to transform all, none, or select the attributes to be turned into labels|
|Feature|Keep selected values|You can keep selected values when changing attributes above the current one. See example on the configuration section for field **Keep previously selected values**|
|Feature|When the image is switched, you can use the cofigurable product image if the simple product does not have its own image| ([35](https://github.com/tzyganu/Switcher/issues/35))|
|Bug Fix|If you choose to show out of stock combinations all the products that are visible in the configurable products page (related, up-sells) are seen as in stock|[55](https://github.com/tzyganu/Switcher/issues/35). This is partially fixed. All the products that are displayed in the configurable product page but are rendered before the main configurable product will still appear in stock even if they are not. All theproducts rendered after the main product will appear with their real stock state. I have a solution to fix this for all the products but it involves rewriting a block or observing the event `core_block_abstract_to_html_before` and I don't want to do either of them.|
|Bug Fix|Images are not switched when the configurable product does not have an image|If the configurable product does not have an image and displays the placeholder, images could not be switched with the ones from the simple product. In the default theme this is fixed changing the main image dom selector to `$('image') || $$('.product-image img')[0]`|

**Release Notes 1.1.0 - 2014-09-05**

|Type|Issue|Comment|
|----|-----|-----|
|Feature|Added support for color hexacodes and fixed images for different attribute values. Thanks @carco for the great code.|Manually merged <a href="https://github.com/tzyganu/Switcher/pull/4">#4</a>|


**Release Notes 1.0.2 - 2014-09-01**

|Type|Issue|Comment|
|----|-----|-----|
|Bug Fix|When you select to show out of stock combinations, it affects the independent simple out of stock products. They are shown in stock.|<a href="https://github.com/tzyganu/Switcher/issues/32" target="_blank">#32</a>|

**Release Notes 1.0.1 - 2014-07-28**

|Type|Issue|Comment|
|----|-----|-----|
|Improvement|You can now show out-of-stock combinations and keep the selects, the out of stock combination options are greyed out and cannot be selected|<a href="https://github.com/tzyganu/Switcher/issues/8" target="_blank">#8</a>|
|Improvement|You can now decide if the first option is selected my default if one is not specified|<a href="https://github.com/tzyganu/Switcher/issues/24" target="_blank">#24</a> - not a full implementation but it will do for now|
|Improvement|Out of the box support for CE-1.9|<a href="https://github.com/tzyganu/Switcher/issues/21" _target="blank">#21</a> - when installing on CE-1.9 some config values are changed|

**Release Notes 1.0.0 - 2014-06-13**

|Type|Issue|
|----|-----|
|Bug Fix|A default configuration could  not be set when creating a configurable product. Only on edit|
|Feature|You can no choose from the configuration panel to show or not the price difference in the labels for configurable attributes. Thanks @thschwz for the idea and the help.|


**Release Notes 0.1.0 - 2014-02-21**

|Type|Issue|
|----|-----|
|Bug Fix|The extension disabled the creation of simple products from the configurable product admin page.|

----------

This Magento extension affects the configurable products display.

Requirements:
---------
 - Magento CE 1.7.0.2 or CE 1.8.0.0.
 - Some minimum js programming skills may be needed to make it work properly on a "very" custom theme. See the *Configuration* section.
 - Your Magento instance must not contain an attribute with the code `default_configuration_id`. If that attribute exists (chances are it doesn't) then edit the file `app/code/community/Easylife/Switcher/Helper/Data.php` and change the value of the constant `DEFAULT_CONFIGURATION_ATTRIBUTE_CODE` to an attribute code that does not exist. Do this before the installation. After...it's too late.

What it does
----------------
Frontend:  

 - it can change the configurable products dropdowns to text or image labels <br />  <img src="http://i.imgur.com/FdHVLAu.png" alt="config" />  
 - it allows you do display the out of stock combinations of configurable products with a "not available" overlay (see image above - medium size). The out of stock products may be selectable or not. Your choice.  
 - it can change the main image in the product page when a combination is selected, if an image is available for the simple product. You can set the attributes that change the image.  
 - it can change the full media block in the product page when a combination is selected, if at least the main image is available for the simple product. You can set the attributes that change the media section.  
 - Starting version 1.1.0 you can use color hex codes and fixed images for attribute values. ![Color](http://i.imgur.com/aJcjgU5.png)  

Backend: 

 - it allows you to set a default configuration to be selected while accessing the configurable product page.<br /> <img src="http://i.imgur.com/zygt7o2.png" alt="backend" />  

How to use:
---------
 - After installation clear the cache and logout & log in the backend.
 - By default the extension is disabled in the backend. To enable it go to *System->Configuration->Easylife Switcher* and read the *Configuration* section.
 - After enabling it you will see an additional column in the `Associated Products` tab of a configurable product that allows you to set a default configuration. To reset the default configuration just uncheck the checkbox near the selected radio element and check it back again.

Configuration:
------------
 - **Enabled**: This can enable or disable the extension.
 - **Keep previously selected values** - If set to `Yes` it will allow you to keep selected values when changing attributes from above. Example: You have a t-shirt configurable by color and size in the following combinations: Size S in Red and Green, Size L in Red and Green and Blue, Size XL in Blue. If you first select S Red, then change the size to L, the Red color will still be selected. If you change the size to XL nothing will be selected for color because the XL shirt has only Blue available. .
 - **Transform dropdowns to labels**: If set to `All` then in the frontend the default dropdowns for the configurable products will be replaced by labels. If set to `Specific` you can select the attributes to be changed to labels.
 - **Transform only the following attributes**: Available only the attributes that you would like to be changed to labels. The rest will remain dropdowns.
 - **Show added configurable prices in label**: If you set this to `No`, you will not get in the labels or the dropdowns with the configurable attributes the price difference for the different combinations.
 - **Show out of stock configurations**: If set to `Yes` then you will see in the configurable product page the out of stock simple product combinations. By default this is disabled in Magento.
 - **Allow out of stock products to be selected**: If this is set to `Yes` then the customer will be able to click on the labels for the out of stock combinations and select them. He will still get an error when trying to add it to the cart. If it is set to `No` the labels for out of stock combinations will be disabled.
 - **Use simple product images instead of labels for attributes**: This allows you to select the attributes that will have images instead of labels. (useful if you have different color combinations). If the simple product does not have an image available then the label with the attribute value will be displayed. (see the first image for the "color" attribute).
 - **Use this image attribute**: From here you can select the attribute image (image, small_image, thumbnail) to be used for image labels.
 - **Use option image or hexa code instead of label for attributes**. Allows you to select which attributes can use fixed images and color hex codes. For the attributes you select here you will see an additional tab when editing the attribute in `Catalog->Attributes->Manage Attributes`. Those images or hex codes will be used in frontend for the labels of the configurable attributes.
 - **Switch product images**: This allows you to change the product image or the whole media block when an attribute combination is changed. If you choose to change the image, this will be changed only if there is one available for the simple product. If you have a lot of simple product combinations and choose to change the whole media block it can lead to performance issues.
 - **Change images when these attributes are changed**: It appears only if you choose to change only the main image and allows you to select which attribute change triggers the image change also.
 - **Dom selector for main image**: It appears only if you choose to change only the main image. This should be the prototype selector for the main image element. by default it looks for the element with id `image`.
 - **Use configurable product image if the simple one does not have images** - If set to `Yes` it will use for simple products that don't have their own image, the configurable product image.
 - **Main image size**: It appears only if you choose to change only the main image. You can specify here the main image size, because I cannot read it from the media block. If empty then the image won't be resized.
 - **Js Callback after main image change**: It appears only if you choose to change only the main image. This is the javascript code that will be executed after the image changes. Useful if you have image zoom.
 - **Change media content when these attributes are changed**: It appears only if you choose to change the media block and it allows you to select which attribute change triggers the media block change also.
 - **Dom Media block selector**: It appears only if you choose to change the media block. This is the prototype selector of the element that contains the media block.
 - **Js Callback after media change**: It appears only if you choose to change the media block. This is the JS code that is executed after the media block is changed
 - **Media block alias**: It appears only if you choose to change the media block. It allows you to specify which block is used for rendering the media section. It's useful if you have extensions that change the media block. Leave empty to use default (`catalog/product_view_media`).
 - **Media block template**: It appears only if you choose to change the media block. It allows you to specify the template used for rendering the media section. It's useful if you have extensions that change the media template. Leave empty to use default (`catalog/product/view/media.phtml`).

Uninstall:
---------

To unsintall the extension remove the following files and folders  

 - app/code/community/Easylife/Switcher/  
 - app/design/adminhtml/default/default/layout/easylife_switcher.xml  
 - app/design/adminhtml/default/default/template/easylife_switcher/  
 - app/design/frontend/base/default/layout/easylife_switcher.xml  
 - app/design/frontend/base/default/template/easylife_switcher/  
 - etc/modules/Easylife_Switcher.xml  
 - app/local/en_US/Easylife_Switcher.csv  
 - js/easylife_switcher/  
 - skin/frontend/base/default/css/easylife_switcher/  
 - skin/frontend/base/default/images/easylife_switcher/  

Run these queries on your database (add table prefix if you have one):

 - `DELETE FROM core_config_data WHERE path LIKE 'easylife_switcher/%'`;  
 - `DELETE FROM core_resource WHERE code = 'easylife_switcher_setup'`;  
 - `DROP TABLE `easylife_switcher_hascode`;  

The extension adds a new attribute to the configurable products. To identify it run this query (if you changed the attribute code before install change it in this query also):  
<pre><code>SELECT 
    e.attribute_id, e.attribute_code 
FROM 
    eav_attribute e 
    LEFT JOIN eav_entity_type et 
    ON e.entity_type_id = et.entity_type_id 
WHERE 
    e.attribute_code = 'default_configuration_id' AND 
    et.entity_type_code = 'catalog_product'`</code></pre>    
To delete it just run  

`DELETE FROM eav_attribute where attribute_id = 'ATTRIBUTE ID FROM PREVIOUS SELECT'`.

Known issues:
---------
If you choose to make the out of stock combinations not selectable and you set for default configuration an out of stock simple product, on the initial page load the out of stock combination will still be selected.
Any ideas on how to handle this are welcomed.

Tests:
-------
The extension was tested on Magento CE 1.7.0.2 & 1.8.0.0 with the sample data for 1.6.0.0 and themes: default, modern and blank.  
Also works on CE 1.9. Tested with sample data for 1.9

The extension does not rewrite any core classes.  
The extension does not replace any js classes. It just extends 2 of them.  
<a href="http://magento.stackexchange.com/q/7608/146" target="_blank">Thanks to @Fooman for explaining how to manage js "class" extension: </a>

Conflicts:
----------
The extension **might** conflict with other extensions that handle image switching on attribute change.
The extension might not work if the js variable used for configurable products page is not named `spConfig`.
If you changed it's name, change it in this file also: `app/design/frontend/base/default/template/easylife_switcher/catalog/product/view/type/configurable/config.phtml`

If you are using cloudzoom as an image zoomer You need to set this configuration to make both extensions work:
 - **DOM selector for main image:** `$$('#zoom1 img')[0]` - if you are using cloudzoom with ultimo theme. Otherwise this may be different.
 - **Js Callback after image change**: `jQuery('#zoom1').data('zoom').destroy();jQuery('#zoom1').attr('href', jQuery('#zoom1 img:first').attr('src'));jQuery('#zoom1').CloudZoom();`
 - **Js Callback after media change**: `jQuery('.cloud-zoom, .cloud-zoom-gallery').CloudZoom()`

Bug report:
-----------
<a href="https://github.com/tzyganu/Switcher/issues">Please submit any bugs or feature requests here</a>.
