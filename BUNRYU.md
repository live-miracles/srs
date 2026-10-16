# SRS for Bunryu

This branch is upstream SRS 6.0 with the fixes Bunryu needs before upstream ships them. Each change is
one commit, and each one is also proposed upstream, so it can be dropped once a 6.0 release has it.

| Commit | Upstream |
|---|---|
| SRT: Fix AAC frame timestamps for 48kHz and other sample rates in srt_to_rtmp. | #4765 (develop), #4774 (6.0release) |

## Release

Push a tag `bunryu-v6.0-rN-M`, where `v6.0-rN` is the upstream base and `M` counts our builds on it. The
`Bunryu release` workflow builds the package the way upstream does (CentOS 7, without ASan) and publishes
`SRS-CentOS7-x86_64-6.0-rN-M.zip` with its SHA-256 as a release on this repository.

## A new upstream release

Rebase onto the new tag, drop the commits upstream now has, and run the utests:

```sh
git rebase --onto v6.0-rN+1 v6.0-rN bunryu/6.0
```

The upstream `release.yml` and `codeql-analysis.yml` workflows are removed on this branch, so that our
tags and pushes don't trigger upstream's release.
