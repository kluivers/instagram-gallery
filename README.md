# instagram-gallery

A small javascript component to load instagram photos for a user, optionally filtered by tags.

Since the Instagram API doesn't support Cross-Origin Resource Sharing (CORS) the user feed is loaded by inserting a script tag with a callback parameter specified in the URL, also known as JSONP. 

This component uses multiple API requests until either the maximum posts count has been satisfied or no more posts are available.

Written in vanilla js, no external javascript dependencies required.

## Usage
Add the following script anywhere to your document. Make sure the `src` property of the generated script tag points to the `ig-gallery.js` script on your server. 

Configure the component using the options dictionary.

	<script type="text/javascript">
		var options = {
			"container": "gallery",
			"maxPostCount": 12,
			"userId": "76675",
			"clientId": "INSTAGRAM_API_CLIENT_ID",
			"tags": ["windsurfing"]
		};
		
		(function() {
			var s = document.createElement('script');
			s.type = 'text/javascript';
			s.async = true;
			s.src = 'js/ig_gallery.js';
			
			s.onload = s.onreadystatechange = function() {
				var rs = this.readyState; if (rs) {
					if (rs != 'complete' && rs != 'loaded') return;
				}
				
				try { new Gallery(options); } catch (e) {}
			}
			
			var st = document.getElementsByTagName('script')[0];
			st.parentNode.insertBefore(s, st);
		})();
	</script>

## Configuration

The following options can be used to customize the gallery component.

- **userId**: required. The instagram user ID.
- **clientId**: required. Instagra API client ID.
- **container**: required. The DOM id of the element to generate the gallery in.
- **maxPostCount**: Optional maximum number of posts to show. Defaults to 20.
- **tags**: optional array of tags to filter on. Posts that do not have any of the tags specified will be ignored and not counted to the maximum number of posts to display. By default all posts will be included.

## Demo

This script is currently in use with the above configuration options on [NED139.nl](http://ned139.nl) (NED-139 is my windsurf sail number)




