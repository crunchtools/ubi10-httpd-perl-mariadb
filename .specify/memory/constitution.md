# ubi10-httpd-perl-mariadb Constitution

> **Version:** 1.1.0
> **Ratified:** 2026-03-10
> **Amended:** 2026-10-02
> **Status:** Active
> **Inherits:** [crunchtools/constitution](https://github.com/crunchtools/constitution) v1.21.0
> **Profile:** Container Image

This file holds what is specific to ubi10-httpd-perl-mariadb. The fleet rules and the Container
Image profile (license, versioning, LABELs, the RHSM secret-mount pattern,
systemd conventions, registry, testing and quality gates) apply at the
inherited version and are checked against this repo's files by
`constitution.yml`. They are not restated here.

## Purpose

UBI 10 Perl + MariaDB leaf image for Request Tracker. Published as
`quay.io/crunchtools/ubi10-httpd-perl-mariadb`.

## Parent Image

`quay.io/crunchtools/ubi10-httpd-perl:latest`. It inherits httpd, mod_fcgid,
Perl and everything ubi10-core provides.

## RHSM Use

`mariadb-server` is not in the UBI repos, so this image registers with RHSM
at build time. Register, install and unregister run in one `RUN` layer, with
the secrets mounted as `RHSM_ACTIVATION_KEY` and `RHSM_ORG_ID`.

## Packages and Services

- **Packages:** mariadb-server, mariadb.
- **Enabled:** mariadb (httpd comes enabled from the parent).

## Smoke Test Coverage

`tests/smoke-test.sh` asserts httpd and mariadb are active, runs a MariaDB CRUD cycle
(CREATE DATABASE, CREATE TABLE, INSERT, SELECT, DROP DATABASE), and checks
mod_fcgid, Perl and the inherited packages.

## Downstream Consumers

Request Tracker (`crunchtools/rt`). Build dispatches `parent-image-updated`
to rt on push. No downstream container images.

## History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-03-10 | Initial constitution, tier 3c leaf |
| 1.0.1 | 2026-09-25 | Gatehouse review, triage and pre-commit gates |
| 1.1.0 | 2026-10-02 | Manifest under constitution v1.18.0: profile restatement removed, image specifics kept |
