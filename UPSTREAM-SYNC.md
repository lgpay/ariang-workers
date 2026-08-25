# Upstream synchronization

The workflow `.github/workflows/sync-upstream.yml` checks the upstream AriaNg repository once per day and can also be started manually from the **Actions** tab.

It merges `mayswind/AriaNg:master` into this repository's `master` branch. Local Cloudflare Workers files are kept as part of the merge. If both repositories change the same lines, the workflow stops so the conflict can be resolved manually.
