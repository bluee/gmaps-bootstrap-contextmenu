google-maps-api-contextmenu
===========================

This is a fork of [Martin Pearman's ContextMenu](http://code.martinpearman.co.uk/googlemapsapi/contextmenu/)
Inspired by the following [github repository](https://github.com/knezmilos13/google-maps-api-contextmenu/)

The context menu is rewritten to work well with Bootstrap 3.

A contextMenu for google.maps.api v3

The usage pattern consists of following steps:

1. Prepare class names for context menu elements. Class names will be
   added to corresponding element types (menu, menu separator).

        var menuStyle = {
			    menu: 'dropdown-menu',
        	menuSeparator: 'divider'
        };

2. Prepare options object containing menu items and display settings.

        var contextMenuOptions  = {
        	classNames: menuStyle,
        	menuItems: [
        		{ label:'option1', id:'menu_option1', 
        			className: 'menu_item', eventName:'option1_clicked' },
        		{ label:'option2', id:'menu_option2', 
        			className: 'menu_item', eventName:'option2_clicked' }
        	],
        	pixelOffset: new google.maps.Point(10, -5),
        	zIndex: 5
        };

3. Construct context menu

        var contextMenu = new ContextMenu(map, contextMenuOptions);

4. Add listener to follow menu item clicks. The listener will receive three 
   parameters - latLng (position supplied when menu was shown, likely mouse
   position), eventName (name set for each menu item in second step), and 
   source (map element that upon which the context menu is shown, e.g map 
   marker or entire map)

        google.maps.event.addListener(contextMenu, 'menu_item_selected', 
        	function(latLng, eventName, source){
        	switch(eventName){
        		case 'option1_clicked':
        			// do something
        			break;
        		case 'option2_clicked':
        			// do something else
        			break;
        		default:
        			// freak out
        			break;
        	}
        });

5. Show menu on some user event, e.g. right click on map. Method show accepts
   two parameters - mouse position, and the element for which the
   menu is shown (map in this example, map markers are also a common scenario):

        google.maps.event.addListener(map, 'rightclick', function(mouseEvent) {
        	contextMenu.show(mouseEvent.latLng, map);
        });
