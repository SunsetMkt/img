![Generated image][cover image]

# 🌠 Imagegen as a Service (Next.js)

[![Deployment status][deployment status]][deployment url]
[![Checks status][checks status]][checks url]
[![Dependabot status][dependabot status]][dependabot url]
[![Code style][code style]][code style url]
[![License info][license info]][license url]

Imagegen (image generator) as a Service, built with [Next.js] and [Vercel].

[![Deploy with Vercel][vercel button]][vercel deploy url]

> ℹ️ If you prefer Node.js + Docker (DigitalOcean, AWS, GCP) over Next.js + Vercel, [checkout this
> repository][node-based repo].

## What is this?

This is a (REST) API service that generates dynamic images for different purposes, is especially useful to generate cover images for content distribution:

- Blogging & writing.

- Videos' thumbnails.

- Open-source repositories' social images.

- etc.

It's built and deployed _serverlessly_ thanks to Next.js and Vercel, so there is nothing to maintain. Moreover, thanks to Vercel's generous hobby plan, this service is **completely free** for _non-commercial_ use.

### Example

The [above image][cover image] is a dynamic image generated by this service, copy and paste the URL below on your browser to see it yourself:

```
https://img.phuctm97.com/api/v2/%F0%9F%8E%86%20**Imagegen**%20as%20a%20Service?&icons=Next.js&icons=Vercel
```

## How should you use it?

There is a [limit to Vercel's free plan][vercel limit], so feel free to test the API on my website but please don't use it directly on yours. Instead:

- [Fork the repository][fork repo].

- Make changes to fit your needs (see below, it's easy).

- Create a new Vercel project and import **your forked repository** (you'll [need a Vercel account][vercel signup]).

- Done 🎉. Vercel will give you a deployment URL, check it out!

## API

### V1

Generic, non-personalized, fewer features.

**URL**: `GET /api/v1/[slug]`

**Query params**:

```yml
text: string.(png|jpg)
theme: "light" | "dark"
md: boolean # Enable/disable basic Markdown syntax
fontSize: string
images: string[]
widths: string[]
heights: string[]
```

All query params are optional, reasonable defaults are used when necessary.

**Example**:

```
https://img.phuctm97.com/api/v1/**Hello**%20World.png?theme=light&md=1&fontSize=100px&images=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Ffront%2Fassets%2Fdesign%2Fvercel-triangle-black.svg
```

### V2

Personalized, more features.

**URL**: `GET /api/v2/[slug]`

**Query params**:

```yml
text: markdown.(png|jpg)
target: "og" | "devto"
theme: "light" | "dark"
icons: string[]
colors: string[]
```

- **text** supports basic Markdown syntax. Emojis are replaced with [Twemoji] variants.

- **target** defines format suitable for distribution to a specific channel, currently supports Open Graph (`og`) and DEV.to (`devto`) .

- **icons** are loaded from [Simple Icons]. Use names appearing on Simple Icons' website as API inputs. Not found icons are ignored.

- **colors** are valid CSS colors, or `default` to use Simple Icons' suggested colors, or `invert` to invert the default colors.

All query params are optional, reasonable defaults are used when necessary.

**Example**:

```
https://img.phuctm97.com/api/v2/%F0%9F%8E%86%20**Imagegen**%20as%20a%20Service?&icons=Next.js&icons=Vercel
```

## Project structure

The project uses [Puppeteer] to launch and capture screenshots from a headless Chrome. Responses are cached for 7 days to increase performance and reduce loads.

- **server/v1**: parse API v1 requests and generate static HTML.

  - Change `parser.ts` to update query API.
  - Change `template.ts` to customize output images.

- **server/v2**: parse API v2 requests and generate static HTML.

  - Change `parser.ts` to update query API.
  - Change `template.ts` to customize output images.

- **images/avatar.jpg**: author's avatar used in v2. Replace with yours.

- **server/\*.ts**: utils to process HTML and capture screenshots.

- **pages/api/v1**, **pages/api/v2**: Next.js API routes to receive requests (you probably won't need to change this).

- **fonts**: Fonts are loaded locally in **server/\*/template.ts**. Replace with your fonts (if necessary).

**Recommended approach**: copy **api/v1** + **server/v1** (or **api/v2** + **server/v2**) to **v3**, then make changes arcordingly. It won't accidentially crash your code this way.

## Development

### Requirements

- Node.js 12.

- Yarn 1.22+.

- Google Chrome.

### Setup

Install dependencies:

```bash
yarn
```

Start development server:

```bash
yarn dev
```

See [package.json] for all pre-configured scripts.

## Author

Made by ([@phuctm97]).

## Thanks

Heavily inspired by Vercel's [og-image].

<!-- Badges -->

[deployment status]: https://img.shields.io/github/deployments/phuctm97/img/production?label=deployment&logo=Vercel
[checks status]: https://img.shields.io/github/checks-status/phuctm97/img/master?logo=Github
[dependabot status]: https://img.shields.io/badge/dependabot-enabled-025e8c?logo=Dependabot
[license info]: https://img.shields.io/github/license/phuctm97/img
[code style]: https://img.shields.io/badge/code%20style-prettier-F7B93E?logo=Prettier
[vercel button]: https://vercel.com/button
[deployment url]: https://github.com/phuctm97/img/deployments/activity_log?environment=Production
[checks url]: https://github.com/phuctm97/img/actions?query=workflow%3APR+branch%3Amaster
[dependabot url]: https://github.com/phuctm97/img/blob/master/.github/dependabot.yml
[code style url]: https://prettier.io
[license url]: /LICENSE
[vercel deploy url]: https://vercel.com/new/git/external?repository-url=https%3A%2F%2Fgithub.com%2Fphuctm97%2Fimg

<!-- Links -->

[cover image]: https://img.phuctm97.com/api/v2/%F0%9F%8E%86%20**Imagegen**%20as%20a%20Service?&icons=Next.js&icons=Vercel
[fork repo]: https://github.com/phuctm97/img/fork
[node-based repo]: https://github.com/phuctm97/img-nodejs
[@phuctm97]: https://twitter.com/phuctm97
[package.json]: /package.json
[next.js]: https://nextjs.org
[vercel]: https://vercel.com
[vercel limit]: https://vercel.com/docs/platform/fair-use-policy#typical-monthly-usage-guidelines
[vercel signup]: https://vercel.com/signup
[simple icons]: https://simpleicons.org
[twemoji]: https://twemoji.twitter.com
[og-image]: https://github.com/vercel/og-image
[puppeteer]: https://github.com/puppeteer/puppeteer
