---
layout: default
title: Customizing the Web Interface
nav_order: 5
parent: How To
---

## Customizing the UI theme
The UI uses Twitter Bootstrap to control the styling and layout. The default theme is simply the default theme for Bootstrap. There's a number of additional themes included. If you'd like to create your own theme, see <a href="http://bootswatch.com/help/" target="top">http://bootswatch.com/help/</a> for instructions on creating a theme for Bootstrap. Once complete, you'll have a css file containing your custom theme styles. To install your theme:

* Copy your custom theme css file to the "wwwroot\css\themes" subfolder

* Open the themes.xml file and add an entry for your theme. For example:

        <Theme>
          <Name>MyCustomTheme</Name>
          <PrimaryStylesheet>/css/themes/mycustomtheme.css</PrimaryStylesheet>
        </Theme>

## Custom JavaScript and CSS
You can now include files named custom.js and custom.css in your project folder. These files can contain any custom JavaScript or CSS that you want loaded when the web UI loads. For example, to change the page background color, add the following to custom.css:

    body {background-color: yellow;}

Here's how you'd override the log function of the logger with custom behavior:

    $(document).ready(function() {
    	var logger = require('logger');
    	logger.log = function(msg) {
    		window.alert(msg);
    	}
        })

## Customizing the Preview window
The Preview window has its own style sheet, PreviewCustom.css in the Content folder. For example, to change the amount of space at the top of the window, change padding-top to the desired value.
