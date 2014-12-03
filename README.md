conversion-tracking
===================

Shop Footer JS code to collect adobe omniture data on the checkout page and transform it into universal analytics (google), adwords conversion tracking (google) and facebook tracking. You'll need to replace some placeholders with your tracking IDs.

== How it works ==

In the checkout page a var is found named s.products (Omniture Analytics). It's a string containing all orders with their productID, name, total price and quantity. The script converts this string back to an array of item objects conaining id, name, unit price and quantity. It then sends each item to the tracking systems.
