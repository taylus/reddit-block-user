> OK, I managed to get blocking to work. Here's a script you can use that will add block buttons to the messages page (or maybe elsewhere; I haven't tested it there though):
>
> Use this by opening up your browser's console (on most browsers F12 will show it), pasting in that code, and then pressing enter -- "Block user" buttons will be added to the page (you'll need to run the script each time you reload the page -- combining it with the high limit page I previously linked would be a good idea).
> 
> Uncompressed:
> ```javascript
> buttonLists = $(".flat-list.buttons");
> for (i = 0; i < buttonLists.length; i++) {
>     blockButton = document.createElement("LI");
>     blockButton.innerHTML = "<form class=\"toggle block-button \" action=\"#\" method=\"get\"><input name=\"executed\" type=\"hidden\" value=\"blocked\"><span class=\"option main active\"><a class=\"togglebutton\" onclick=\"return toggle(this)\" href=\"#\">block author (hide post)</a></span><span class=\"option error\">are you sure?  <a class=\"yes\" onclick='change_state(this, \"block\", hide_thing, undefined, null)' href=\"javascript:void(0)\">yes</a> / <a class=\"no\" onclick=\"return toggle(this)\" href=\"javascript:void(0)\">no</a></span></form>";
>     buttonLists[i].appendChild(blockButton);
> }
> ```

[Original post](https://www.reddit.com/r/redditdev/comments/3nvrdi/deleting_post_replies_from_inbox_i_need_help_and/cvrttje/?context=7)
