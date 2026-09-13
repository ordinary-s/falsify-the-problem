# Pages publishing and Bing discovery

This is the single maintenance guide for the two static introduction pages.
Content clarity and crawlable pages are the scope of this work. No search ranking,
indexing deadline, traffic increase, installation count, or model advantage is promised.

## Publication status — 2026-09-13

The maintainer authorized publication after local implementation and checks.

- The initial site was committed and pushed as `a90ec94`.
  The [first Pages deployment](https://github.com/ordinary-s/falsify-the-problem/actions/runs/34754228505)
  completed successfully.
- GitHub Pages publishes from `master`, folder `/docs`, with HTTPS enforced
  and no custom domain. No custom Actions workflow was added.
- Public GET checks returned HTTP 200 for both language pages, the stylesheet,
  and Sitemap. Response bodies matched the local files byte-for-byte; content
  types and final URLs were correct, with no `X-Robots-Tag` indexing restriction.
- Repository About and Website were updated after these checks. Both READMEs
  link to their respective public language pages. The five existing Topics remain.
- Bing account verification and Sitemap submission remain pending: no real
  account verification tag or file was provided. IndexNow remains optional and
  has not been enabled or used. No indexing or search-performance result is claimed.

Before publication, inspection of `a43ab07` found Pages disabled, Website empty,
and the proposed public URL returning HTTP 404. Those were the starting conditions,
not the current deployment state.

## Repository metadata

Published **About** text:

> An open-source Agent Skill for problem framing and assumption testing across coding, debugging, architecture, scientific research, and product decisions.

Keep the existing relevant **Topics**:
`agent-skills`, `ai-agents`, `hypothesis-testing`, `markdown`, `problem-framing`.
Topics describe the project; they are not ranking guarantees.

Published **Website**: <https://ordinary-s.github.io/falsify-the-problem/>.

## Publish with GitHub Pages

The prepared source is plain HTML and CSS in `docs/`, with `.nojekyll`.
There is no build step or custom Actions workflow to maintain.

For future authorized releases:

1. Review the local diff and validation results, then commit and push.
   If changes are reviewed on another branch, merge them into `master` before
   using that branch as the publishing source.
2. In repository **Settings → Pages → Build and deployment**, choose
   **Deploy from a branch**, branch **master**, folder **/docs**, then Save.
3. Inspect the deployment result and the actual published URL. GitHub can run
   its own Pages deployment workflow even when publishing from a branch.
4. Verify the public resources below. If GitHub reports a different domain or
   redirects to one, update both pages' canonical, hreflang and `og:url`, plus
   both Sitemap URLs and this guide, together before search submission.
5. After successful public checks, update Website and both README website links
   if the published address has changed. Keep About and Topics accurate.

Public resources verified on 2026-09-13:

| Resource | Public URL | Check |
| --- | --- | --- |
| English | `https://ordinary-s.github.io/falsify-the-problem/` | HTTP 200, English HTML |
| 简体中文 | `https://ordinary-s.github.io/falsify-the-problem/zh/` | HTTP 200, Chinese HTML |
| Styles | `https://ordinary-s.github.io/falsify-the-problem/assets/site.css` | HTTP 200, CSS content type and body |
| Sitemap | `https://ordinary-s.github.io/falsify-the-problem/sitemap.xml` | HTTP 200, valid XML with exactly the two canonical URLs |

Use a real GET request and inspect the body, not only a successful redirect or a
HEAD response. In Windows PowerShell use `curl.exe`; in macOS/Linux shells use
`curl`, for example `curl -i https://ordinary-s.github.io/falsify-the-problem/`.
Repeat for the other three URLs. Check final URLs, response headers for accidental
indexing restrictions, language switching, styles, anchors, and mobile layout.
A locally reachable page does not establish public deployment.

Publishing-source reference:
[GitHub Pages configuration](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Bing Webmaster Tools

After publication, add the **actual Pages project URL** to your Bing Webmaster
Tools account. A project-path property is different from ownership of the entire
`github.io` host or the `github.com` repository domain.

1. Use the verification method and exact page/file path shown in your account.
   For an HTML meta method, insert the real account-provided tag into the
   designated page's `<head>`. For a file method, publish the exact supplied file
   at the required URL and verify its public response before requesting verification.
2. If a requested path lies outside `/falsify-the-problem/`, this project's
   `docs/` folder cannot serve it. Choose a supported method within your control
   or arrange control of the required location; do not claim it has been verified.
3. No verification tag or file has been included in the initial site. Obtain the
   real value from the maintainer's Bing account; do not insert a dummy code.
   Missing account verification does not prevent local README or page work.
4. Once the site is live and ownership is verified, submit the
   actual Sitemap URL in the account. Inspect Sitemap processing and each page
   with URL Inspection, including its live fetch and indexed status.

Owning a GitHub repository does not prove control of `github.com` to Bing.
Follow the current account UI if its verification choices differ.

References: [Add and verify a site](https://www.bing.com/webmasters/help/add-and-verify-site-12184f8b)
and [Bing Webmaster Guidelines](https://www.bing.com/webmasters/help/webmaster-guidelines-30fba23a).
During the 2026-09-13 documentation check, direct retrieval of these two pages
returned the help shell without readable article bodies. Official search-cached
text was available; a full live-article review was not completed. The instructions
above defer account-specific verification choices and paths to the UI.

## Optional later step: IndexNow

IndexNow is not enabled by this first version. No key has been generated, no URLs
have been submitted, and no submission script or daily job is provided.

If the maintainer later approves it:

1. Confirm that the content pages are publicly available at their canonical URLs.
2. Create a real IndexNow key and a UTF-8 text file whose contents are that key.
   Publish the file under this project path and confirm its real public response.
3. In a submission, use `host` equal to `ordinary-s.github.io` and `keyLocation`
   equal to the **full public URL of that actual key file**. Because the file is
   inside `/falsify-the-problem/`, only URLs under that directory are in scope.
   Recheck the host and scope if the real site uses another domain.
4. Submit only relevant new, changed, or deleted Pages URLs after approval.
   A Pages key cannot authorize submission of `github.com` repository URLs.
   Do not resubmit unchanged pages every day.

The IndexNow key file and Bing Webmaster Tools site verification are separate
mechanisms. HTTP 200 means the URLs were received; HTTP 202 means key validation
is pending. Neither means a page is indexed or its ranking improved.
See the [IndexNow protocol](https://www.indexnow.org/documentation).

## Observe results without overstating them

Use the reports Bing actually makes available for this property: indexing and
crawl status, impressions, clicks, CTR, and search queries. Record the date range
and actual page/query scope before comparing periods. Mark unavailable data
as unavailable; zero and unavailable are different states.

Keep these routes distinct:

- **Bing → GitHub:** traffic arrives directly at the repository. Repository
  traffic/referrer reports, where available, are limited and do not provide
  ownership-based Bing reports for `github.com`.
- **Bing → Pages → GitHub:** Bing reports can describe the Pages search entry.
  With no visitor tracking installed, this site does not measure the subsequent
  click to GitHub or attribute it to a specific search query.

GitHub clones do not equal skill installations or active usage. Search results
vary; failing to find a page in a manual search is not sufficient evidence that
it is absent from the index. Do not promise days to indexing, first-page placement,
or a fixed growth rate.

## Local preview and checks

Use Python 3's standard library with the project prefix. No dependency install is
needed. From the repository root, save the following temporary script **outside
the repository**, then run it with `python` on Windows or `python3` on macOS/Linux.
The script serves only `docs/` at the intended project path and binds to loopback.

```python
from http.server import SimpleHTTPRequestHandler, ThreadingHTTPServer
from pathlib import Path
from urllib.parse import urlsplit

docs = Path.cwd() / "docs"
assert (docs / "index.html").is_file(), "Run from the repository root"

class Preview(SimpleHTTPRequestHandler):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, directory=str(docs), **kwargs)

    def do_GET(self):
        prefix = "/falsify-the-problem/"
        if not urlsplit(self.path).path.startswith(prefix):
            self.send_error(404)
            return
        self.path = "/" + self.path[len(prefix):]
        super().do_GET()

ThreadingHTTPServer(("127.0.0.1", 8000), Preview).serve_forever()
```

Open `http://127.0.0.1:8000/falsify-the-problem/` and
`http://127.0.0.1:8000/falsify-the-problem/zh/`. Stop with Ctrl+C.
Check both languages at approximately 1440px and at 432 × 932, including:

- Links, language switching, section anchors and stylesheet responses under the
  project prefix; no accidental host-root `/assets/` references.
- Closed and expanded installation sections, keyboard focus, code scrolling, and
  no horizontal page overflow. The body and navigation work without JavaScript.
- One H1 per page; distinct titles/descriptions and correct `lang`.
  Each canonical matches that language's URL. Hreflang lists both languages,
  including self; Sitemap entries match the two canonicals.
- No dummy verification, temporary asset paths, stale live-site claims, or
  accidental `noindex`. The repository has no share image, so `og:image` is omitted.
- `git diff --check` and a review of untracked files. Keep `SKILL.md` and every
  file under `evals/` byte-for-byte unchanged; preserve their original snapshots.

Run installation-command checks only in isolated temporary locations; do not
overwrite a user's existing skill folder. Command syntax or clone success does
not prove actual Codex discovery or successful invocation. macOS/Linux execution
and cross-host behavior remain unverified by this documentation change.

Keep screenshots and temporary validation helpers outside the repository.
Record completed checks and tool failures honestly; no model evaluation rerun is
required for this content-only change.

## Keep the site small

Maintain only the two language pages and their shared stylesheet. All core
content is HTML text. There is no JavaScript, external font, tracker, cookie UI,
advertisement, or automatic language redirect.

Sitemap lists only the two formal content URLs, with no invented `lastmod`.
No project-directory `robots.txt` is added: this repository has not established
control of the host-root `/robots.txt`. No `llms.txt`, JSON-LD, extra CMS,
submission automation, or additional instruction framework is needed.
Canonical and hreflang keep language URLs explicit; neither is a ranking guarantee.

Codex paths and CLI / IDE invocation were checked against the
[official local-skills documentation](https://learn.chatgpt.com/docs/build-skills),
the current redirect destination of the supplied
[Codex Skills URL](https://developers.openai.com/codex/skills).
