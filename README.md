# GameHubApp Web Platform

A web portal built from static HTML pages, local frontend assets, and PHP integration endpoints. It includes guides, a blog, account-access information, SEO resources, visitor statistics, and a privately configured Telegram support workflow.

## Features

- Static landing pages, guide pages, and blog articles.
- Responsive CSS, JavaScript, images, and media assets.
- PHP endpoints for visitor statistics and Telegram support.
- SEO metadata, sitemaps, crawler files, and Apache security rules.
- Guarded content updates and manual deployment with a restricted upload list.

The repository does not implement the external gaming platform's account system. Account-access pages and outbound links should not be treated as a local authentication backend.

## Requirements

- PHP 8.3 with cURL for integration endpoints.
- Apache with `mod_headers` and the modules used by `.htaccess` for production behavior.
- Node.js 22 and configured repository secrets only for the optional Codex content workflow.

There is no npm package manifest or frontend build step for the website.

## Local preview

```sh
git clone https://github.com/fumakill4/gamehubapp-co.git
cd gamehubapp-co
php -S 127.0.0.1:8080 -t .
```

Open [the local homepage](http://127.0.0.1:8080/). This previews static content and PHP routing but does not apply Apache `.htaccess` protections. Keep the development server on the loopback interface and use Apache when checking production headers and access rules.

Bot and statistics endpoints need private server configuration; a frontend preview does not require production credentials or a live Telegram account.

## Repository layout

| Path | Purpose |
| --- | --- |
| `index.html` | Main landing page |
| Guide directories | Topic-specific static pages |
| `blog/` | Blog listing, articles, and article assets |
| `assets/` | Images, media, scripts, and styles |
| `api/telegram-support.php` | Privately configured Telegram support entry point |
| `api/page-visit-counter.php` | Visitor tracking and statistics |
| `.htaccess` | Apache access rules and response headers |
| `.github/` | Content automation, guards, and manual deployment |
| `sitemap.xml`, `robots.txt`, `llms.txt` | Discovery and crawler resources |

## Private integrations

The Telegram endpoint expects private configuration and state in a sibling `private_bot` directory outside the public document root. It uses configured bot credentials, webhook verification, and optional support/panel settings. These values and account mappings must be supplied privately by an authorized operator.

Never commit Telegram tokens, administrator identities, panel credentials, member records, redemption/recharge records, visitor state, or local environment files. A customer's entered account identifier does not independently prove ownership.

## Validation

Check changed PHP endpoints before publishing:

```sh
php -l api/telegram-support.php
php -l api/page-visit-counter.php
```

For HTML content, verify canonical URLs, sitemap entries, images, outbound links, and mobile layout. Use nonproduction fixtures when validating integration behavior.

## Deployment

The **Manual Safe Deploy** workflow defaults to a dry run and uploads only the paths in its allowlist. It protects important application files, including API and account-access paths. Configure credentials through GitHub Actions secrets and inspect the proposed upload list before deployment. Backend and server configuration changes need their own controlled rollout.

## Security status

Bot authentication, account ownership, visitor privacy, and deployment verification changes are being reviewed in [security PR #2](https://github.com/fumakill4/gamehubapp-co/pull/2). Review and deploy those changes before opening administrative or account-sensitive functionality to the public. Store secret configuration and runtime data outside the web root.

The presence of this README does not certify the deployed environment or remove sensitive data from earlier Git history. Production policies and historical copies require separate review.

## Maintenance

Maintained by **i729**. Preserve upstream attribution and check the licensing of third-party assets before redistribution.
