# imageLoader
Right way to load an image - control it!

ImageLoader is a some sort of LazyLoad, but not lazy.
ImageLoader does nothing, but load images in controlled embodiment. And return an promise.

And Yes - ImageLoader is not exists!

```
imageLoader.load(url) -> Promise
imageLoader.load(function) -> Promice
imageLoader.load({
  url: {String|State|Function} // uniform resource locator and be anything,
  priority: {Number}           // priority of url
  channel : {String}           // channel
  returnAs: {url, dataURI, Renderable},
  flags: {Object} (for example - noProxy}
}

imageLoader.channels.(add|remove)(name, settings)

imageLoader.proxy.(add|remove)({
   matchURL: function (url, request){
      return {Number}
   },
   load: function (url, request){
      return {Promise}
   }
});
```

for example
```
// Create three channels - very fast, normal and slow.

imageLoader.channel.add('hight',{
   loadLimit:16,
   noProxy: true
});

imageLoader.channel.add('normal',{
   loadLimit:4,
   noProxy: true
});

imageLoader.channel.add('slow',{
   loadLimit:1,
   noProxy: true
});

// next create proxy
imageLoader.proxy.add({
   matchURL: function (url, request){
      return (url.match(somePattern);
   },
   load: function (url, request){
      var speed = 'normal';
      if (request.priority>1) speed = 'hight';
      if (request.priority<0) speed = 'low';
      return imageLoader.load({
        url:url+'#',
        channel: speed
      });
   }
});

//next grab all images, and
imageLoader.load({
  url: image.realSrc,
  priority: imageTop<topOfScreen
              ? return -2.0 + 1.0/(imageTop-topOfScreen)
              : return 1.0/(imageTop-bottomOfScreen)
});
```
