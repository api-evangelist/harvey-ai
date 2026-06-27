---
title: "Building a Faster, More Reliable Upload Experience in Vault"
url: "https://www.harvey.ai/blog/faster-more-reliable-vault-uploads"
date: "2026-06-15"
feed_url: "https://www.harvey.ai/blog"
---
Harvey rearchitected Vault file uploads using Azure Blob Storage presigned URLs and a concurrent three-stage pipeline, enabling direct browser-to-cloud transfers instead of routing every byte through its backend. Weekly upload volume grew from 2.2 million files in mid-January to 15 million by May, reaching 200 million active files; the changes cut 1,000-file uploads from 2m 35s to 1m 6s (57% faster) and reduced average latency from 6.7s to 5.9s.
