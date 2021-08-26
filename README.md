# Nextjs Google Analytics

Google Analytics for Next.js, based on the [next.js / example / with-google-analytics](https://github.com/vercel/next.js/tree/master/examples/with-google-analytics).

It will only be loaded on `production` environments. To test it, you can run the development server with set `NODE_ENV` to `production`, for example:

`NODE_ENV=production npm run dev`

## Installation

```
npm install --save nextjs-google-analytics
```

## Usage

Add the `gtag` script inside the `Head` to a custom document using the `GoogleAnalytics` component:

```js
// pages/_document.js

import Document, { Html, Head, Main, NextScript } from "next/document";

import { GoogleAnalytics } from "nextjs-google-analytics";

export default class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          <GoogleAnalytics />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}
```

## Page views

Call the `usePageView` hook inside `_app.js`:

```js
// /pages/_app.js

import { useEffect } from 'react'
import { useRouter } from 'next/router'
import { usePageView } from "nextjs-google-analytics";

const App = ({ Component, pageProps }) => {
  usePageView();
  const router = useRouter()

  return <Component {...pageProps} />
}

export default
```

## Custom event

You can import the `event` function to track a custom event:

```js
import { useState } from "react";
import Page from "../components/Page";
import { event } from "nextjs-google-analytics";

export function Contact() {
  const [message, setMessage] = useState("");

  const handleInput = (e) => {
    setMessage(e.target.value);
  };

  const handleSubmit = (e) => {
    e.preventDefault();

    event({
      action: "submit_form",
      category: "Contact",
      label: this.state.message,
    });

    setState("");
  };

  return (
    <Page>
      <h1>This is the Contact page</h1>
      <form onSubmit={handleSubmit}>
        <label>
          <span>Message:</span>
          <textarea onChange={handleInput} value={message} />
        </label>
        <button type="submit">submit</button>
      </form>
    </Page>
  );
}
```

## LICENSE

[MIT](./LICENSE)
