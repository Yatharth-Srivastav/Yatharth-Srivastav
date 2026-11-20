# Profile maintenance

GitHub displays the root `README.md` on [Yatharth’s Overview](https://github.com/Yatharth10-bit). Edit the introduction, selected projects and contact links there. Keep the activity markers intact so the daily refresh can update that section.

The light and dark banners, portfolio button and project tiles live in `assets/`. Edit `scripts/brand.mjs` and run `node scripts/brand.mjs` to rebuild the brand artwork. `scripts/portrait.json` supplies the portrait pattern. Run `node --test tests/profile.test.mjs` from the repository root before opening a pull request.

The refresh runs on pushes to `main` and daily at 04:27 UTC (09:57 IST). To start it manually, open **Actions → Refresh profile → Run workflow**, choose `main`, then click **Run workflow**.

## Activity definitions

The daily job uses the built-in token on the runner. It requests only owned public repositories through the public user-repositories endpoint. Forks and the profile repository are excluded. The language mix ranks GitHub Linguist bytes across the remaining repositories. It includes archived repos. Recent projects are the most recently pushed non-archived, nonempty repositories.

The calendar covers the trailing 365 UTC dates. It counts unique commit SHAs in the default-branch history returned for the owner's GitHub author login, using the committer timestamp. Other branches, issue/PR activity and private contributions are outside the displayed scope. An active streak may end today or yesterday and is capped by the displayed 365-day window. Since the generator never reads private contributions its numbers can differ from the account-wide GitHub graph.

All API results must succeed before the two assets and recent-project block are written. Failed API requests, rate limits or conflicting pushes leave the last committed snapshot visible. Run the workflow again after resolving the failure. No service token, browser JavaScript or external card host is necessary.

