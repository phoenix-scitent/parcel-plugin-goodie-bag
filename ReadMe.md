# parcel-plugin-goodie-bag

Provides high-level polyfills to keep parcel working on IE(11) for the following API's:

- Promise
- fetch APIs
- Object.assign
- Array.includes
- Array.find
- Object.entries
- Object.values
- Object.keys
- Array.findIndex
- URL (object)

## Why This Is Needed

TL;DR: multiple bundle support in Parcel, such as using the ability to require html partial files, makes direct use of both the `Promise` and `fetch` APIs, directly.

This plugin is born of my frustaration with the scenario outline in [parcel issue #2364](https://github.com/parcel-bundler/parcel/issues/2364). This requires additional intervention, since the native requirement of the potentially un-polyfilled APIs is prior to any polyfill via `babel-polyfill` and isn't something that can be influenced inside the application source itself; at least not without convoluted efforts.

## Installation

Add this to your projects `devDependencies`:

```json
"parcel-plugin-goodie-bag": "github:phoenix-scitent/parcel-plugin-goodie-bag"
```

## Usage

No additional configuration required. If your app is being bundled by parcel and you have this plugin installed, the processed application will build with:

- the `index.html` containing a `script` tag in its head pointing to the "goodie bag` script (the two polyfills)
- a "goodie bag" script file, placed in the destination directory (`outDir` to parcel, defaults to `dist`)
- the script tag will respect your configured `publicUrl` option with Parcel (e.g.- prefixed with default `/` or no root slash in the case of `.`)

## In Action

I made use of [a simple reproducible repository](https://github.com/edm00se/parcel-ie11-issue-demo) I had set up for tracking this issue.

| Before                       | After                      |
| ---------------------------- | -------------------------- |
| ![before](assets/before.jpg) | ![after](assets/after.jpg) |

## Contributing

If you see something fundamentally wrong with this, feel free to submit a PR.

## History

Parcel is an amazing bundler with superpowers. The fact that my ability to support IE(11), a requirement for my day job, was hampered by this limitation of a multiple bundle scenario meant that I had to solve the problem myself. It is my hope that one day the configuration of Parcel will allow for the surfacing of base level APIs, such as `Promise` and `fetch` to make this plugin unnecessary. Until then, I'll keep this available to provide some sanity.

## Todo

- Use [https://github.com/paulmillr/es6-shim](https://github.com/paulmillr/es6-shim) for polyfills.

## Credits

- [parcel](https://parceljs.org/)
- Repository forked from: https://github.com/edm00se/parcel-plugin-goodie-bag.

## License

MIT
