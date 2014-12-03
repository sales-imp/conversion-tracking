conversion-tracking
===================

Shop Footer JS code to collect adobe omniture data on the checkout page and transform it into universal analytics (google), adwords conversion tracking (google) and facebook tracking. You'll need to replace some placeholders with your tracking IDs.

== How it works ==

In the checkout page a var is found named s.products (Omniture Analytics). It's a string containing all orders with their productID, name, total price and quantity. The script converts this string back to an array of item objects conaining id, name, unit price and quantity. It then sends each item to the tracking systems.

== What belongs to which tracking system? ==

**** UNIVERSAL ANALYTICS ****
<pre>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', 'ANALYTICS_TRACKING_ID', 'auto');
ga('send', 'pageview');

ga('require', 'ecommerce');

ga('ecommerce:addItem', {
        'id': productList[e].id, // Use spreadshirt Product ID
        'name': productList[e].name, // Use spreadshirt item name
        'sku': productList[e].id, // Currently product ID = SKU, change if needed
        'category': 'spreadshirt product', // Product category
        'price': productList[e].price, // single item price
        'quantity': productList[e].count // how many items of this type were bought
      });
</pre>
**** FACEBOOK ANALYTICS ****
<pre>
(function() {
  var _fbq = window._fbq || (window._fbq = []);
  if (!_fbq.loaded)
  { var fbds = document.createElement('script'); 
    fbds.async = true; 
    fbds.src = '//connect.facebook.net/en_US/fbds.js'; 
    var s = document.getElementsByTagName('script')[0]; 
    s.parentNode.insertBefore(fbds, s); _fbq.loaded = true; }
  })();
window._fbq = window._fbq || [];

window._fbq.push(['track', 'FACEBOOK_TRACKING_ID', {'value':productList[e].price,'currency':'USD'}]);
</pre>
**** GOOGLE REMARKETING TAG ****
<pre>
<script type="text/javascript" src="http://www.googleadservices.com/pagead/conversion_async.js" charset="utf-8"></script>

window.google_trackConversion({
        google_conversion_id: GOOGLE_CONVERSION_ID,
        google_custom_params: {
          ecomm_prodid: productList[e].id,
          ecomm_pagetype: "checkout",
          ecomm_totalvalue : productList[e].price
        },
        google_remarketing_only: true
      });
</pre>
####################################################################################

You can safely remove the entries of a tracking system if not needed.
