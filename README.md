# UAEJobs

UAEJobs is a local-first job-search companion for LinkedIn. It combines a Chrome extension with a private command-line application to help you review job listings, compare them with your profile, save promising roles, and track applications—all while keeping your personal data on your Mac.

## What it does

- Analyzes the LinkedIn job currently open in Chrome.
- Shows an explainable match score, job highlights, and potential concerns.
- Sends approved jobs to a local SQLite inbox without creating duplicates.
- Tracks saved, applied, and interview statuses.
- Imports LinkedIn job-alert emails through read-only Gmail access.
- Runs optional automatic Gmail synchronization every 30 minutes on macOS.
- Stores candidate preferences and approved résumé details locally.

## Privacy and security

UAEJobs is designed around local storage. Your job database, résumé profile, Gmail authorization token, application history, and logs stay on your Mac. The browser extension connects only to a local service at `127.0.0.1:8765` and does not automatically apply for jobs.

The Gmail integration requests read-only access. It cannot send, modify, or delete email.

## Project status

The stable build currently contains:

- UAEJobs CLI `0.18.1`
- UAEJobs LinkedIn Analyzer `1.0.38`
- 77 passing automated tests

## Website

- [UAEJobs homepage](https://mattldsouza.github.io/uaejobs/)
- [Privacy policy](https://mattldsouza.github.io/uaejobs/privacy/)

## Availability

UAEJobs is currently a personal macOS project. Installation packages and detailed setup instructions will be provided through GitHub Releases.
