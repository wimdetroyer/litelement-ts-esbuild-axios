# litelement-ts-esbuild-axios

minimal reproducible example of following problem:


## Problem

I'm trying to add the axios dependency in the lit-element-ts-build: https://github.com/modernweb-dev/example-projects/tree/master/lit-element-ts-esbuild

Here's the changed MyElement.ts file:

```javascript

import axios from "axios";

export class MyElement extends LitElement {
  static styles = css`
    :host {
      display: block;
      padding: 25px;
      color: var(--my-element-text-color, #000);
    }
  `;

  @property({ type: String }) title = 'Hey there';

  @property({ type: Number }) counter = 5;

  __increment() {
    this.counter += 1;
    axios.get('https://example.com').then(
        res => {
          console.log(res)
        }
    )
  }

```

All great, but running npm start or npm test yields the following:

```javascript
Error while transforming node_modules/axios/lib/platform/node/classes/URLSearchParams.js: Could not resolve import "url".

  1 | 'use strict';
  2 | 
> 3 | import url from 'url';
    |       ^
  4 | export default url.URLSearchParams;
  5 | 
```

after adding the 'url' dependency via npm i url (which I already feel _shouldn't_ be part of the solution) that becomes:

```javascript
Error while transforming node_modules/axios/lib/adapters/http.js: Could not resolve import "http".

   6 | import buildURL from './../helpers/buildURL.js';
   7 | import {getProxyForUrl} from 'proxy-from-env';
>  8 | import http from 'http';
     |       ^
   9 | import https from 'https';
  10 | import followRedirects from 'follow-redirects';
  11 | import zlib from 'zlib';

```

But from this point on I'm stumped.

From what I can tell, axios is using the adapters it should use in a node.js environment, instead of the ones for the browser (?)


## how to reproduce

run either `npm run start` or `npm run test




