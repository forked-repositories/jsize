<h1 align="center">
  <a href="https://github.com/antonmedv/jsize">
    <img src="https://user-images.githubusercontent.com/141232/29957332-1d50d0be-8f17-11e7-91cc-2329a01d5b23.png" width="600">
  </a>
</h1>

Find out minified and gzipped npm package size.
```
npm install -g jsize
```

## Features
* [Scoped packages](https://docs.npmjs.com/misc/scope)
* Individual files within packages
* Multiple packages at once
* Easy CLI and programmatic usage

## CLI Usage

```
$ jsize react + react-dom angular vue

   react + react-dom  =  44.2 kB (gzipped)
   angular            =  61.5 kB (gzipped)
   vue                =  20.9 kB (gzipped)
   
```   

```
$ jsize @cycle/dom + @cycle/run

   @cycle/dom + @cycle/run  =  16.7 kB (gzipped)

```

```
$ jsize lodash/map + lodash/filter redux

   lodash/map + lodash/filter  =  5.88 kB (gzipped)
   redux                       =  2.77 kB (gzipped)
   
```

```
$ jsize --verbose jquery

   Package     Initial  Minified  Gzipped
  
   jquery   =  271 kB   88.6 kB   30.8 kB

```

### Options

* #### `-v, --verbose`

  Display initial size, minified size and gzip size.

  ```
  $ jsize jquery -v

     Package     Initial  Minified  Gzipped

     jquery   =  271 kB   87.3 kB   30.6 kB

  ```

## Programmatic Usage

```js
import jsize from 'jsize'

jsize('lodash').then(({ initial, minified, gzipped }) => {
  // Work with values (all in bytes).
})

// Also supports multiple entries.
jsize(['lodash/map', 'lodash/filter'])
```

## Total size of multiple entries

You can add up multiple entries by using `+` between entry names.
This is useful because in some cases like in lodash there is a runtime which is a one time cost.

```js
$ jsize lodash/map + lodash/assign + lodash/filter

   lodash/map + lodash/assign + lodash/filter  =  6.63 kB (gzipped)

```

Sizes look much larger when comparing individually because it doesn't account for the shared runtime.

```js
$ jsize lodash/map lodash/assign lodash/filter

   lodash/map     =  5.89 kB (gzipped)
   lodash/assign  =  2.78 kB (gzipped)
   lodash/filter  =  5.85 kB (gzipped)

```

## Peer Dependencies

When a package has `peerDependencies` they are automatically excluded from the bundle size.
To have a better idea of the total size of all dependencies you must add up all peers as well.

```
$ jsize react

   react  =  7.23 kB (gzipped)

$ jsize react+react-dom

   react + react-dom  =  43.6 kB (gzipped)

```

## License

Licensed under the [MIT license](https://github.com/antonmedv/jsize/blob/master/LICENSE).
