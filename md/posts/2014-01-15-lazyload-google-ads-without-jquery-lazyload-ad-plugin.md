{:title "Lazyload Google ads without jQuery LazyLoad ad plugin"
 :layout :post
 :tags  []
 :toc true}

I had mentioned in one of my previous articles [here](http://www.golb.in/more-exciting-new-features-for-golbin-25.html), that we had changed our lazyloading technique for google-ads on [Golbin!](http://www.golb.in/) pages. Today I will show you how we did it.

Previously, we were using the awesome jQuery lazyload Ad plugin as shown in their documentation [here](http://jqueryad.web2ajax.fr/). However, the plugin itself added about 8.4Kb to the page-weight. Even though Golbin! was using measures to lazyload the plugin itself, it was still additional page-weight, especially for first time (with browser cache empty) users.

Then, recently, we noticed that google had made some changes to their [adsense](https://support.google.com/adsense/answer/3221666) code because of which the ads would be rendered asynchronously, thus removing the need for the jQuery lazyload Ad plugin. Sample code looks like below:

```
<script async src="http://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
    style="display:inline-block;width:300px;height:250px"
    data-ad-client="ca-pub-xxxxxxxxxxxxxxxx"
    data-ad-slot="6440411535">
</ins>
<script> (adsbygoogle = window.adsbygoogle || []).push({}); </script>
```

So far so good. However, we wanted to go a step further than this because:

* In our experience, if we put the script in the bottom of the page (just before the ending "" tag), then the ads did not get rendered at all. Putting the js script at page bottom is good performance practice (see [here](http://developer.yahoo.com/performance/rules.html) and [here](https://developers.google.com/speed/docs/insights/rules) for best practices for website frontend performance).
* Golbin! was already using a technique to lazyload the javascript files needed by the page itself. And we wanted to continue using this technique for the new script too.

Fortunately, one needs to include the script tag only once in the page irrespective of how many ad units were present on the page; this went well with our technique, because then we could lazyload the adsense script and use some JS to invoke some function to show the ads in the correct place.

Our initial HTML markup snippet looks something similar to:

```
<div class="g-ad">
    <ins class="adsbygoogle"
        style="display:inline-block;width:300px;height:250px"
        data-ad-client="ca-pub-xxxxxxxxxxxxxxxx"
        data-ad-slot="6440411535"></ins>
</div>
```

and the supporting javascript code looks like:

```
$.getScript("//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js",
    function (data, textStatus, jqxhr) {
        var script = document.createElement("script");
        script.type = "text/javascript";
        script.text = "(adsbygoogle = window.adsbygoogle || []).push({})";
        for (var a = null, arr = $("div.g-ad"), i = 0; i < arr.length; i += 1) {
            a = arr[i];
            $(a).append(script);
       };
    }
);
```

If you have ever used jQuery, you will notice that what the above javascript snippet does is that it lazyloads the adsense javascript via the getScript function. And when the adsense javascript is loaded, the anonymous function is called which does the following steps

* creates a script tag having the code shown in the adsense documentation
* finds all "div" elements having the class "g-ad"
* loops through the divs found in the above step and adds the script tag to the div

And voila, we're done! We have now successfully reduced 8.4Kb of page-weight, which means faster pages for our readers :)

The only drawback of this method is that it is impossible to debug it in the javascript debugger (in both firefox and chrome browsers), because the newly added script does not show up in the DOM :(

But don't worry. If this technique has worked for us, it should for you too. So, go ahead and give it a try! And don't forget to share your experiences back :)
